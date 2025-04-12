---
layout: article
title: 코딩테스트 - softeer - 나무섭지
article_header:
  type: overlay
  theme: dark
  background_color: "#203028"
author: SeoYeonii
categories: coding-test
tags: [coding-test, softeer]
# top: 1
# sidebar: []
---

## 문제

[softeer - 나무섭지](https://softeer.ai/practice/7726)

### 내가 푼 답 - 오답

```js
const readline = require("readline");
const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});
let lineCnt = 0;
let n, m;
const arr = [];
const TYPES = ["N", "D", "G"];
const DIR = [
  [1, 0],
  [0, 1],
  [-1, 0],
  [0, -1],
];
const indexes = [];

const isOkIndex = (i, j) => {
  return i >= 0 && i < n && j >= 0 && j < m;
};

const solve = () => {
  // index 정보들
  const nInfo = indexes.filter((x) => x.type === "N")[0];
  const dInfo = indexes.filter((x) => x.type === "D")[0];
  const [nI, nJ, dI, dJ] = [nInfo.i, nInfo.j, dInfo.i, dInfo.j];
  const gInfo = indexes.filter((x) => x.type === "G");

  const bfs = (type, i, j) => {
    const visited = Array.from({ length: n }, () => new Array(m).fill(false));
    const q = [];
    q.push([i, j, 0]);
    visited[i][j] = true;

    while (q.length > 0) {
      const cur = q.shift();
      const [curI, curJ, curDis] = [...cur];
      if (curI === dI && curJ === dJ) return curDis;
      for (let ii = 0; ii < 4; ii += 1) {
        const [newI, newJ] = [curI + DIR[ii][0], curJ + DIR[ii][1]];
        if (isOkIndex(newI, newJ) && !visited[newI][newJ]) {
          if (type === "N") {
            if (arr[newI][newJ] === "#") continue;
          }
          q.push([newI, newJ, curDis + 1]);
          visited[newI][newJ] = true;
        }
      }
    }
    return -1;
  };

  // 남우가 탈출하는 루트, bfs로 최단거리 구하기
  const nCnt = bfs("N", nI, nJ);

  if (nCnt < 0) {
    console.log("No");
    return;
  }

  // 있거나 없을 수 있는 유령이 탈출하는 루트, 벽 무시, 그냥 d까지 달리기
  for (const g of gInfo) {
    const gCnt = Math.abs(g.i - dI) + Math.abs(g.j - dJ);
    if (gCnt <= nCnt) {
      console.log("No");
      return;
    }
  }
  console.log("Yes");
};

rl.on("line", (line) => {
  if (lineCnt === 0) [n, m] = line.split(" ").map((x) => 1 * x);
  else {
    const temp = line.split("");
    for (const t of TYPES) {
      if (temp.includes(t))
        indexes.push({
          type: t,
          i: lineCnt - 1,
          j: temp.findIndex((x) => x === t),
        });
    }
    arr.push(temp);
  }
  lineCnt += 1;
}).on("close", () => {
  solve();
  process.exit(0);
});
```

---

남우는 벽도 고려해야 하니, dfs를 사용했고,

유령은 벽을 뛰어 넘으니 맨해튼 거리가 가장 가까우므로 바로 맨해튼 거리로 계산했습니다.

(사실 처음엔 둘다 bfs돌렸다가 장황히 시간초과....)
