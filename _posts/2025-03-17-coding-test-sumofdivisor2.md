---
layout: article
title: 코딩테스트 - 약수의 개수와 덧샘
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

[약수의 개수와 덧샘](https://school.programmers.co.kr/learn/courses/30/lessons/77884)

### 문제 설명

두 정수 left와 right가 매개변수로 주어집니다. left부터 right까지의 모든 수들 중에서, 약수의 개수가 짝수인 수는 더하고, 약수의 개수가 홀수인 수는 뺀 수를 return 하도록 solution 함수를 완성해주세요.

### 제한사항

1 ≤ left ≤ right ≤ 1,000

### 답

```js
function solution(left, right) {
  let res = 0;
  for (let i = left; i <= right; i++) {
    if (parseInt(Math.sqrt(i)) === Math.sqrt(i)) res -= i;
    else res += i;
  }
  return res;
}
```

보통 일반적으로 수는 짝수개의 약수를 갖는데, 약수 개수가 홀수인 경우는 그 수가 완전제곱수 일 때 입니다. (ex: 4 -> 1, 2, 4)

이걸 생각하고 풀면 금방 풀립니다.

---

솔직히 레벨 1이라, 제한 사항이 빡빡하지 않기 때문에 아무생각 없이 이렇게 풀어도 되긴 합니다.

그래도 효율성, 코드 간결성 생각하면 한 번 더 생각하는 것이 좋을 듯 합니다.

```js
const getNum = (n) => {
  let cnt = 0;
  for (let i = 1; i <= n / 2; i++) {
    if (n % i === 0) cnt += 1;
  }
  return cnt + 1;
};

function solution(left, right) {
  let res = 0;
  for (let i = left; i <= right; i++) {
    const num = getNum(i);
    if (num % 2 === 0) res += i;
    else res -= i;
  }
  return res;
}
```
