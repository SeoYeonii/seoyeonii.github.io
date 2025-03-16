---
layout: article
title: 코딩테스트 - 약수의 합
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

[약수의 합](https://school.programmers.co.kr/learn/courses/30/lessons/12928)

### 문제 설명

정수 n을 입력받아 n의 약수를 모두 더한 값을 리턴하는 함수를 작성하는 문제입니다.

### 답

```js
function solution(n) {
  var answer = 0;
  for (let i = 1; i <= n / 2; i += 1) {
    if (n % i === 0) answer += i;
  }
  return answer + n;
}
```

---

제일 처음

```js
function solution(n) {
  var answer = 1;
  for (let i = 2; i <= n; i += 1) {
    if (n % i === 0) answer += i;
  }
  return answer;
}
```

이렇게 답을 작성 했었는데, 제풀해보니 #16번에서 오답이 났었습니다.

왜그럴까? 생각해보니 문제 조건이
`n은 0 이상 3000이하인 정수입니다.` 였습니다...
나름 하나라도 연산량 줄이려고 1부터 시작했는데
0을 고려를 못했습니다..

그래서 0을 고려해 다시 0부터 시작했고 최적화를 위해 `n/2`까지만 연산하고
("어떤 수 a가 n의 약수라면 n / a도 반드시 n의 약수"인 점을 이용)
마지막에 n을 더해서 제출하니 정답처리가 되었습니다.

앞으로 어떠한 문제라도 잘 읽어보고 풀어야겠습니다.

## 후기

병가를 내고 돌아온 후 정말 많은 일이 있었습니다...
잘 진행되던 프로젝트도 모두 사라지고 이직을 결심하게 되었습니다.

그래서 대학생때 공부하던 코딩테스트를 오랜만에 풀어보는데,
이럴수가... 연습문제를 그냥 풀다가 너무 쉬운 문제에서 오답이 하나 나왔습니다...

프로그래머스에 문제가 100여개 밖에 없길래 후딱 풀고 실무 문제 풀어봐야겠다 생각했으나.. 틀린 문제가 있으므로 오답노트를 만들려 합니다...
