---
layout: article
title: 코딩테스트 - 다리를 지나는 트럭
article_header:
  type: overlay
  theme: dark
  background_color: "#203028"
#   background_image:
#     gradient: "linear-gradient(135deg, rgba(34, 139, 87 , .4), rgba(139, 34, 139, .4))"
#     src: /assets/images/banners/jwt.png
author: SeoYeonii
categories: coding-test
tags: [coding-test]
# top: 1
# sidebar: []
---

## 문제

[다리를 지나는 트럭](https://school.programmers.co.kr/learn/courses/30/lessons/42583)

### 답

```js
function solution(bridge_length, weight, truck_weights) {
  let time = 0;
  let q = Array(bridge_length).fill(0);
  let b = 0; // 다리의 현재 무게

  while (truck_weights.length > 0 || b > 0) {
    time++;
    b -= q.shift();
    if (truck_weights.length > 0) {
      if (b + truck_weights[0] <= weight) {
        const t = truck_weights.shift();
        q.push(t);
        b += t;
      } else {
        q.push(0);
      }
    }
  }

  return time;
}
```

---

문제를 설명하는 방식 그대로 문제를 해결했습니다.
킥은 다리에 트럭이 못 올라가는 상황에 0을 올려서 계산하는 부분이었습니다.
