---
layout: article
title: 코딩테스트 - 가장 큰 수
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

[가장 큰 수](https://school.programmers.co.kr/learn/courses/30/lessons/42746)

### 답

```js
function solution(numbers) {
  const res = numbers
    .map((x) => x.toString())
    .sort((a, b) => (b + a).localeCompare(a + b))
    .join("");

  return res[0] === "0" ? "0" : res;
}
```

---

sorting 할 때 a+b 와 b+a를 문자비교(localeCompare) 해서 비교하면 엄청 쉽다는 것을
생각해내기까지 조금 오래 걸려서 기록했습니다.
