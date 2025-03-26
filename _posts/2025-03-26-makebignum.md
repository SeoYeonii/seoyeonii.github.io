---
layout: article
title: 코딩테스트 - 큰 수 만들기
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

[큰 수 만들기](https://school.programmers.co.kr/learn/courses/30/lessons/42883)

### 답

```js
function solution(number, k) {
  const s = [];
  let cnt = 0;
  for (let i = 0; i < number.length; i += 1) {
    const cur = number[i];

    while (s.length > 0 && cnt < k && s[s.length - 1] < cur) {
      s.pop();
      cnt += 1;
    }

    s.push(cur);
  }
  return s.slice(0, number.length - k).join("");
}
```

---

> 앞에서부터 스택으로 탐색하면서 현재 수가 더 크면 이전 수를 지운다.

이 아이디어로 구현해서 풀 수 있었습니다.
