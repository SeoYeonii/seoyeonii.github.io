---
layout: article
title: 코딩테스트 - 나머지가 1이되는 수 찾기
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
# 약수는 짝을 이루며 존재~
---

## 문제

[나머지가 1이되는 수 찾기](https://school.programmers.co.kr/learn/courses/30/lessons/87389)

### 문제 설명

자연수 n이 매개변수로 주어집니다. n을 x로 나눈 나머지가 1이 되도록 하는 가장 작은 자연수 x를 return 하도록 solution 함수를 완성해주세요. 답이 항상 존재함은 증명될 수 있습니다.

### 제한 사항

3 ≤ n ≤ 1,000,000

### 답

```js
function solution(n) {
  let t = n - 1;
  for (let i = 2; i * i <= t; i++) {
    if (t % i === 0) return i;
  }
  return t;
}
```

---

그냥 for문 돌려서 값을 찾으려다가.. n이 100만이라는 점이 걸려 조금 더 생각을 해 본 결과, 그냥 (n - 1)의 약수 중 1을 제외 한 가장 작은 값을 찾으면 되겠다는 생각을 했습니다.
가장 작은 약수이므로 √(n-1) 여기까지만 검색하면 되니, 시간 복잡도도 √n 로 n보다는 확실히 줄일 수 있었습니다.

### 후기

lv1 맞나.. 문제 푸는데 진짜 오랜만에 루트까지 나와야 하나... 하고 그냥 for문 돌린 답을 제출해보니 이 답도 정답으로 인정되었습니다..ㅎ

저런..
