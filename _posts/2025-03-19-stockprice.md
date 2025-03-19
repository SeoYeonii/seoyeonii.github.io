---
layout: article
title: 코딩테스트 - 주식 가격
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

[주식 가격](https://school.programmers.co.kr/learn/courses/30/lessons/42584)

### 답

```js
function solution(prices) {
  const arr = [];
  let index = -1;
  while (index < prices.length) {
    index += 1;
    const cur = prices[index];
    for (let i = index + 1; i <= prices.length; i += 1) {
      if (i === prices.length) arr.push(prices.length - index - 1);
      else if (prices[i] < cur) {
        arr.push(i - index);
        break;
      }
    }
  }
  return arr;
}
```

---

처음에는 아래와 같이 `shift` method를 사용해서 쉽게 문제를 해결하려고 했습니다.
그런데 이렇게 푸니 효율성에서 6.7%가 나왔습니다...

왜인가 하니 shift를 하면 배열의 모든 원소를 다 옮겨야 하므로 shift()는 O(N) 연산이 되고,
이 shift를 n번 도는 for문 안에서 사용하고 있으므로 총 O(N²) 시간 복잡도가 발생해서 비효율적이 된 것이었습니다.

그래서 그냥 단순히 shift를 사용하지 않고 index를 담은 값 하나 설정해두어서 푸니 바로 해결되었습니다.

```js
function solution(prices) {
  const arr = [];
  while (prices.length > 0) {
    const cur = prices.shift();
    for (let i = 0; i <= prices.length; i += 1) {
      if (i === prices.length) arr.push(i);
      else if (prices[i] < cur) {
        arr.push(i + 1);
        break;
      }
    }
  }
  return arr;
}
```
