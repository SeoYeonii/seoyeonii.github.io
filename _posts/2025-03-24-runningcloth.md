---
layout: article
title: 코딩테스트 - 체육복
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

[체육복](https://school.programmers.co.kr/learn/courses/30/lessons/42862)

### 답

```js
function solution(n, lost, reserve) {
  const rl = lost.filter((x) => !reserve.includes(x)).sort((a, b) => a - b);
  const rr = reserve.filter((x) => !lost.includes(x)).sort((a, b) => a - b);

  for (let i = 0; i < rr.length; i++) {
    const r = rr[i];
    const index = rl.findIndex((l) => Math.abs(l - r) === 1);
    if (index !== -1) rl.splice(index, 1);
  }

  return n - rl.length;
}
```

---

그리디, dp문제는 풀 때마다 복기용으로 글을 남길까 합니다.

보통 앞의 선택이 다음 선택에 영향을 주면 그리디(현재의 최선의 선택 반복해서 해결)로 풀 수 없다고 합니다.
그래서 이 문제도 앞의 사람이 누구 체육복 빌릴껀지 선택하면 다음 사람의 선택에 영향을 주니까 그리디 아니지 않나? 라고 생각했는데,

일단 오름차순으로 정렬을 해두었을 때
`앞쪽부터 도우면 뒤쪽은 여전히 뒤쪽 학생에게 도움 받을 기회가 있지만 뒤부터 도우면, 앞쪽 애가 도움받을 기회를 잃어버린다.`
즉 따라서 앞을 먼저 구조하는 게 전체적으로 이득: reserve를 오름차순으로 정렬하고 앞쪽부터 lost한 친구들 구조하면 최선의 결과를 얻을 수 있습니다.
