---
layout: article
title: 코딩테스트 - 제일 작은 수 제거하기
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

[제일 작은 수 제거하기](https://school.programmers.co.kr/learn/courses/30/lessons/12935)

### 문제 설명

정수를 저장한 배열, arr 에서 가장 작은 수를 제거한 배열을 리턴하는 함수, solution을 완성해주세요. 단, 리턴하려는 배열이 빈 배열인 경우엔 배열에 -1을 채워 리턴하세요. 예를들어 arr이 [4,3,2,1]인 경우는 [4,3,2]를 리턴 하고, [10]면 [-1]을 리턴 합니다.

### 제한 사항

- arr은 길이 1 이상인 배열입니다.
- 인덱스 i, j에 대해 i ≠ j이면 arr[i] ≠ arr[j] 입니다.

### 답

```js
function solution(arr) {
  const n = JSON.parse(JSON.stringify(arr))
    .sort((a, b) => a - b)
    .shift();
  console.log(n);
  const res = arr.filter((x) => x !== n);
  if (res.length === 0) return [-1];
  return res;
}
```

---

`const n = JSON.parse(JSON.stringify(arr)).sort().shift();`

처음에 첫줄 sort를 그냥 위와 같이 비워놨었는데, 그러다 보니 틀린 답이 있었습니다.

자바스크립트의 sort()는 기본적으로 문자열 정렬을 하기 때문에, 숫자를 정렬할 때 의도치 않은 결과를 일으킬 수 있습니다.

ex)

```js
console.log([10, 2, 1].sort());
// ["1", "10", "2"] → 문자 순 정렬
```

### 후기

늘 쓰는 sort의 특성도 막상 문제를 풀려니 생각이 안나기도 합니다.. 조심해야겠군요..
저런..
