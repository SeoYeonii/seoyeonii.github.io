---
layout: article
title: 코딩테스트 - 구명보트
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

[구명보트](https://school.programmers.co.kr/learn/courses/30/lessons/42885)

### 답

```js
function solution(people, limit) {
  let cnt = 0;
  const p = people.sort((a, b) => a - b);
  let light = 0;
  let heavy = p.length - 1;

  while (light <= heavy) {
    if (people[light] + people[heavy] <= limit) light += 1;
    heavy -= 1;
    cnt += 1;
  }

  return cnt;
}
```

---

> 투 포인터로 가장 무게 적게 나가는 사람, 많이 나가는 사람 표시해서 해결

이 아이디어로 효율성도 고려해서 풀 수 있었습니다.
