---
layout: article
title: 코딩테스트 - 주식 가격
article_header:
  type: overlay
  theme: dark
  background_color: "#203028"
author: SeoYeonii
categories: coding-test
tags: [coding-test]
# top: 1
# sidebar: []
---

## 문제

[디스크 컨트롤러](https://school.programmers.co.kr/learn/courses/30/lessons/42627)

### 답

```js
// [소요시간, 요청시간, index]
class MinHeap {
  constructor() {
    this.heap = [];
  }

  compare(a, b) {
    if (a[0] !== b[0]) return a[0] - b[0];
    if (a[1] !== b[1]) return a[1] - b[1];
    return a[2] - b[2];
  }

  push(value) {
    this.heap.push(value);
    let i = this.heap.length - 1;

    while (i > 0) {
      const pi = Math.floor((i - 1) / 2);
      if (this.compare(this.heap[pi], this.heap[i]) <= 0) break;
      [this.heap[pi], this.heap[i]] = [this.heap[i], this.heap[pi]];
      i = pi;
    }
  }

  pop() {
    if (this.heap.length === 0) return null;
    if (this.heap.length === 1) return this.heap.pop();

    const min = this.heap[0];
    this.heap[0] = this.heap.pop();
    let pi = 0;

    while (true) {
      let li = pi * 2 + 1;
      let ri = pi * 2 + 2;
      let si = pi;

      if (
        li < this.heap.length &&
        this.compare(this.heap[li], this.heap[si]) < 0
      ) {
        si = li;
      }

      if (
        ri < this.heap.length &&
        this.compare(this.heap[ri], this.heap[si]) < 0
      ) {
        si = ri;
      }

      if (si === pi) break;
      [this.heap[pi], this.heap[si]] = [this.heap[si], this.heap[pi]];
      pi = si;
    }

    return min;
  }

  size() {
    return this.heap.length;
  }
}

function solution(Jobs) {
  // [소요시간, 요청시간, index]
  let jobs = Jobs.map((job, i) => [job[1], job[0], i]);
  jobs.sort((a, b) => b[1] - a[1]); // 요청 시각 기준 내림차순

  const scheduler = new MinHeap();
  let time = 0;
  let totalWait = 0;
  let count = 0;

  while (jobs.length > 0 || scheduler.size() > 0) {
    // 현재 시간까지 들어온 작업들을 모두 대기큐에 넣기
    while (jobs.length > 0 && jobs[jobs.length - 1][1] <= time) {
      scheduler.push(jobs.pop());
    }

    if (scheduler.size() > 0) {
      const [duration, requestTime, _] = scheduler.pop();
      time += duration;
      totalWait += time - requestTime;
      count += 1;
    } else {
      // 처리할 작업이 없으면 다음 작업의 요청 시각으로 점프
      time = jobs[jobs.length - 1][1];
    }
  }

  return Math.floor(totalWait / count);
}
```

---

이 문제도 역시 우선순위 큐를 구성하기 위해 minHeap을 구현해서 풀었습니다.
다만 비교할 때 1. 소요시간 2. 요청시간 3. 작업번호 순서대로 비교하기 위해 compare method를 하나 추가한 형태로 구현했습니다.

그리고 이 minHeap을 가지고 문제를 풀때, 시간이 흘러가고 있다는 가정 하에

1. 현재 시점의 시간까지 들어온 작업 들은 모두 대기 큐에 넣기,
2. 대기큐에 작업이 있으면 대기큐에서 최우선순위 pop해서 시간에 소요시간 더하고, 해당 작업에 대해 반환시간 구해서 더하고 작업 처리 개수 + 1 하기
3. 대기 큐 없으면 이제 다음 처리할 작업 시간으로 점프

하는 방식으로 구현했습니다.

heap 구현보다 어떻게 heap을 사용할지를 더 고민했던 문제였습니다.
