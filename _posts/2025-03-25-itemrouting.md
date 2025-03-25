---
layout: article
title: 코딩테스트 - 아이템 줍기
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

[아이템 줍기](https://school.programmers.co.kr/learn/courses/30/lessons/87694)

### 답

```js
// 방향 위 오른 아래 왼
const dir = [
  [-1, 0],
  [0, 1],
  [1, 0],
  [0, -1],
];

const isOk = (x, y) => {
  return x >= 0 && x < 102 && y >= 0 && y < 102;
};

function solution(rectangle, characterX, characterY, itemX, itemY) {
  // 갈 수 있는 길 먼저 찾고
  // 1이상 50 이하인 자연수 좌표값이니까 51 * 51 크기 map으로. -1 채워넣자 => * 2
  const map = Array.from({ length: 102 }).map((x) => new Array(102).fill(-1));
  // rectangle for 문 돌면서
  // 변인경우 1로, 내부이면 0으로 (덮어씌움.) 근데 0인 곳엔 1로 못 넣게
  rectangle.forEach(([x1, y1, x2, y2]) => {
    x1 *= 2;
    y1 *= 2;
    x2 *= 2;
    y2 *= 2;
    for (let i = x1; i <= x2; i += 1) {
      for (let j = y1; j <= y2; j += 1) {
        if (i === x1 || i === x2 || j === y1 || j === y2) {
          if (map[i][j] !== 0) map[i][j] = 1;
        } else {
          map[i][j] = 0;
        }
      }
    }
  });

  const cntMap = Array.from({ length: 102 }).map((x) =>
    new Array(102).fill(-1)
  );
  const q = [[characterX * 2, characterY * 2]];
  cntMap[characterX * 2][characterY * 2] = 0;
  // 길 위에서 아이템 루팅 (bfs)
  while (q.length > 0) {
    const [curX, curY] = q.shift();
    if (curX === itemX * 2 && curY === itemY * 2) break;
    for (let i = 0; i < 4; i += 1) {
      const [newX, newY] = [curX + dir[i][0], curY + dir[i][1]];
      if (
        isOk(newX, newY) &&
        map[newX][newY] === 1 &&
        cntMap[newX][newY] === -1
      ) {
        cntMap[newX][newY] = cntMap[curX][curY] + 1;
        q.push([newX, newY]);
      }
    }
  }

  return cntMap[itemX * 2][itemY * 2] / 2;
}
```

---

오늘도 최단거리 문제 룰루~ 풀고 있었는데...
음.. 이 문제는 원래 2배로 스케일링해서 좌표간 이동 명확하게 표시해야하는 문제인데
문제에서 `즉, 위 그림처럼 서로 다른 두 직사각형이 꼭짓점에서 만나거나, 변이 겹치는 경우 등은 없습니다.`라고 명시를 했습니다.
그래서 스케일링 없이 그냥 풀었더니, 틀리는 케이스가 있다고 나왔습니다.
사각형을 여러 개 겹치면서 1배 좌표계에 표시할때 경로가 모호해지는 경우가 생길 것을 생각을 못했습니다.
ㅠㅠ 다시 한번 잘 생각해서 풀어야겠습니다.

```js
// 방향 위 오른 아래 왼
const dir = [
  [-1, 0],
  [0, 1],
  [1, 0],
  [0, -1],
];

const isOk = (x, y) => {
  return x >= 0 && x < 51 && y >= 0 && y < 51;
};

function solution(rectangle, characterX, characterY, itemX, itemY) {
  // 갈 수 있는 길 먼저 찾고
  // 1이상 50 이하인 자연수 좌표값이니까 51 * 51 크기 map으로. -1 채워넣자
  const map = Array.from({ length: 51 }).map((x) => new Array(51).fill(-1));
  // rectangle for 문 돌면서
  // 변인경우 1로, 내부이면 0으로 (덮어씌움.) 근데 0인 곳엔 1로 못 넣게,
  for (const r of rectangle) {
    const w = r[2] - r[0] + 1;
    const h = r[3] - r[1] + 1;
    for (let i = r[0]; i <= r[2]; i += 1) {
      for (let j = r[1]; j <= r[3]; j += 1) {
        const mapStatus = map[i][j];
        if (
          (i === r[0] || i === r[2] || j === r[1] || j === r[3]) &&
          (mapStatus === -1 || mapStatus === 1)
        )
          map[i][j] = 1;
        else map[i][j] = 0;
      }
    }
  }

  const cntMap = Array.from({ length: 51 }).map((x) => new Array(51).fill(-1));
  const q = [[characterX, characterY]];
  cntMap[characterX][characterY] = 0;
  // 길 위에서 아이템 루팅 (bfs)
  while (q.length > 0) {
    const [curX, curY] = q.shift();
    // if(curX === itemX && curY === itemY) break;
    for (let i = 0; i < 4; i += 1) {
      const [newX, newY] = [curX + dir[i][0], curY + dir[i][1]];
      if (
        isOk(newX, newY) &&
        map[newX][newY] === 1 &&
        cntMap[newX][newY] === -1
      ) {
        cntMap[newX][newY] = cntMap[curX][curY] + 1;
        q.push([newX, newY]);
      }
    }
  }
  return cntMap[itemX][itemY];
}
```
