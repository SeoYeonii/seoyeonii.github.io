---
layout: article
title: 코딩테스트 - 여행 경로
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

[여행 경로](https://school.programmers.co.kr/learn/courses/30/lessons/43164?language=javascript)

### 답

```js
function solution(tickets) {
  const dirMap = {};
  const ticMap = {};
  const keys = Array.from(new Set(tickets.flat()));
  keys.forEach((x) => (dirMap[x] = []));
  tickets.forEach(([a, b]) => {
    dirMap[a].push(b);

    const key = `${a} ${b}`;
    if (key in ticMap) ticMap[key].cnt += 1;
    else ticMap[key] = { cnt: 1, vCnt: 0 };
  });
  keys.forEach((x) => dirMap[x].sort((a, b) => a.localeCompare(b)));

  const allUsed = () => {
    return Object.keys(ticMap).every((x) => {
      return ticMap[x].cnt === ticMap[x].vCnt;
    });
  };
  const canGo = (target) => {
    return dirMap[target]?.some((x) => {
      return ticMap[`${target} ${x}`].cnt > ticMap[`${target} ${x}`].vCnt;
    });
  };

  const route = ["ICN"];
  const dfs = (target) => {
    // 더 이상 갈 티켓 없고 끝나지도 않았으면 취소
    if (!allUsed() && !canGo(target)) return false;
    // 다 방문했으면 끝.
    if (allUsed()) return true;

    for (const x of dirMap[target]) {
      if (ticMap[`${target} ${x}`].cnt > ticMap[`${target} ${x}`].vCnt) {
        ticMap[`${target} ${x}`].vCnt += 1;
        route.push(x);

        const res = dfs(x);
        if (res) return true;

        // 실패했으면 루트에서 빼기
        ticMap[`${target} ${x}`].vCnt -= 1;
        route.pop();
      }
    }
    return false;
  };
  dfs("ICN");

  return route;
}
```

---

dfs를 어떻게 사용해야하는지는 항상 잘 생각해봐야하는것 같습니다.
