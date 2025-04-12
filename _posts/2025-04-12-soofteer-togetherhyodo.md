---
layout: article
title: 코딩테스트 - softeer - 함께하는 효도
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

[softeer - 함께하는 효도](https://softeer.ai/practice/7727)

### 내가 푼 답 - 오답

```js
const readline = require("readline");
const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});
let lineNo = 0;
const dir = [
  [-1, 0],
  [0, 1],
  [1, 0],
  [0, -1],
];
let n, m;
const arr = [];
const fArr = [];

const isOk = (i, j) => {
  return i >= 1 && i <= n && j >= 1 && j <= n;
};

const solve = () => {
  const searchRoute = (curFIndex) => {
    const result = [];
    const findARoute = () => {
      const visited = Array.from({ length: n + 1 }, () =>
        new Array(n + 1).fill(false)
      );
      const s = [];
      const curFI = fArr[curFIndex][0];
      const curFJ = fArr[curFIndex][1];
      s.push({ i: curFI, j: curFJ, time: 0, num: arr[curFI][curFJ] });
      visited[curFI][curFJ] = true;

      const dfs = (curI, curJ, curTime) => {
        if (curTime === 3) {
          result.push([
            { i: curFI, j: curFJ, time: 0, num: arr[curFI][curFJ] },
            ...s.slice(0),
          ]);
          return;
        }
        for (let i = 0; i < 4; i += 1) {
          const [newI, newJ] = [curI + dir[i][0], curJ + dir[i][1]];
          if (isOk(newI, newJ) && !visited[newI][newJ]) {
            visited[newI][newJ] = true;
            s.push({
              i: newI,
              j: newJ,
              time: curTime + 1,
              num: arr[newI][newJ],
            });
            dfs(newI, newJ, curTime + 1);
            visited[newI][newJ] = false;
            s.pop();
          }
        }
      };
      while (s.length > 0) {
        const { i, j, time } = s.pop();
        dfs(i, j, time);
      }
    };
    findARoute();
    return result;
  };
  // 1. 가능한 루트 dfs로 다 탐색
  const allRoute = [];
  for (let i = 0; i < fArr.length; i += 1) {
    allRoute.push(searchRoute(i));
  }

  // 2. 그 경로들로 dfs로 전부 탐색
  let foundedR = [];
  const visitedTime = Array.from({ length: 4 }, () =>
    Array.from({ length: n + 1 }, () => new Array(n + 1).fill(false))
  );
  const visitedFruit = Array.from({ length: n + 1 }, () =>
    new Array(n + 1).fill(false)
  );
  const s = [];
  const dfs = (fIndex) => {
    if (fIndex === m) {
      foundedR.push(s.slice(0));
      return;
    }

    const routes = allRoute[fIndex];
    // 여기서 for돌면서 하나 고르고.
    for (const r of routes) {
      // 그 루트 돌면서 체쿠.
      // 그 시간에 없는지
      // 그 과일에 없는지
      if (
        r.every(
          (x) => !visitedTime[x.time][x.i][x.j] && !visitedFruit[x.i][x.j]
        )
      ) {
        // 없으면 방문 체크 후 push
        r.forEach((x) => {
          visitedTime[x.time][x.i][x.j] = true;
          visitedFruit[x.i][x.j] = true;
        });
        s.push(r);
        // dfs
        dfs(fIndex + 1);
        // 방문 해제 후 pop
        r.forEach((x) => {
          visitedTime[x.time][x.i][x.j] = false;
          visitedFruit[x.i][x.j] = false;
        });
        s.pop();
      }
    }
  };
  dfs(0);

  let max = 0;
  for (const fR of foundedR) {
    max = Math.max(
      max,
      fR.reduce((a, b) => a + b.reduce((aa, bb) => aa + bb.num, 0), 0)
    );
  }

  console.log(max);
};

rl.on("line", (line) => {
  if (lineNo === 0) {
    [n, m] = line.split(" ").map((x) => 1 * x);
    arr.push(new Array(n + 1).fill(-1));
  } else if (lineNo <= n) arr.push([-1, ...line.split(" ").map((x) => 1 * x)]);
  else fArr.push(line.split(" ").map((x) => 1 * x));
  lineNo += 1;
}).on("close", () => {
  solve();
  process.exit(0);
});
```

---

dfs를 2번 사용하는 구조를 썼습니다.

1. 우선 모든 친구들이 3초간 이동할 수 있는 경로 구하기
2. 그 경로들 중, 같은 시간에, 같은 위치에 안겹치는

마지막 케이스만 오류가 나서... 찝찝한 형태로 일단은 마무리 했습니다.
다른 분이 논리적인 이유로 마지막 케이스 이상하다고 올려주셔서 <br />
일단 다른 문제도 풀어봐야 하므로 넘어가지만...<br />
이 문제는 다시 한 번 봐야 할 것 같습니다.

++ 추가!!!

```js
const readline = require("readline");
const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});
let lineNo = 0;
const dir = [
  [-1, 0],
  [0, 1],
  [1, 0],
  [0, -1],
];
let n, m;
const arr = [];
const fArr = [];

const isOk = (i, j) => {
  return i >= 1 && i <= n && j >= 1 && j <= n;
};

const solve = () => {
  const searchRoute = (curFIndex) => {
    const result = [];
    const findARoute = () => {
      const visited = Array.from({ length: n + 1 }, () =>
        new Array(n + 1).fill(false)
      );
      const s = [];
      const curFI = fArr[curFIndex][0];
      const curFJ = fArr[curFIndex][1];
      s.push({ i: curFI, j: curFJ, time: 0, num: arr[curFI][curFJ] });
      visited[curFI][curFJ] = true;

      const dfs = (curI, curJ, curTime) => {
        if (curTime === 3) {
          result.push([
            { i: curFI, j: curFJ, time: 0, num: arr[curFI][curFJ] },
            ...s.slice(0),
          ]);
          return;
        }
        for (let i = 0; i < 4; i += 1) {
          const [newI, newJ] = [curI + dir[i][0], curJ + dir[i][1]];
          if (isOk(newI, newJ) && !visited[newI][newJ]) {
            visited[newI][newJ] = true;
            s.push({
              i: newI,
              j: newJ,
              time: curTime + 1,
              num: arr[newI][newJ],
            });
            dfs(newI, newJ, curTime + 1);
            visited[newI][newJ] = false;
            s.pop();
          }
        }
      };
      while (s.length > 0) {
        const { i, j, time } = s.pop();
        dfs(i, j, time);
      }
    };
    findARoute();
    return result;
  };
  // 1. 가능한 루트 dfs로 다 탐색
  const allRoute = [];
  for (let i = 0; i < fArr.length; i += 1) {
    allRoute.push(searchRoute(i));
  }

  // 2. 그 경로들로 dfs로 전부 탐색
  let foundedR = [];
  const visitedTime = Array.from({ length: 4 }, () =>
    Array.from({ length: n + 1 }, () => new Array(n + 1).fill(false))
  );
  const visitedFruit = Array.from({ length: n + 1 }, () =>
    new Array(n + 1).fill(0)
  );
  const s = [];
  const dfs = (fIndex) => {
    if (fIndex === m) {
      foundedR.push(s.slice(0));
      return;
    }

    const routes = allRoute[fIndex];
    // 여기서 for돌면서 하나 고르고.
    for (const r of routes) {
      // 그 루트 돌면서 체쿠.
      // 그 시간에 없는지
      // 그 과일에 없는지
      // if (r.every((x) => !visitedTime[x.time][x.i][x.j] && !visitedFruit[x.i][x.j])) {
      if (r.every((x) => !visitedTime[x.time][x.i][x.j])) {
        // + 남이 따간 곳 방문하면 num 0으로 바꾸는 로직 추가
        const processedR = r.map((x) => {
          if (visitedFruit[x.i][x.j] > 0) return { ...x, num: 0 };
          else return x;
        });
        // 없으면 방문 체크 후 push
        r.forEach((x) => {
          visitedTime[x.time][x.i][x.j] = true;
          visitedFruit[x.i][x.j] += 1;
        });
        // s.push(r);
        s.push(processedR);
        // dfs
        dfs(fIndex + 1);
        // 방문 해제 후 pop
        r.forEach((x) => {
          visitedTime[x.time][x.i][x.j] = false;
          visitedFruit[x.i][x.j] -= 1;
        });
        s.pop();
      }
    }
  };
  dfs(0);

  let max = 0;
  for (const fR of foundedR) {
    max = Math.max(
      max,
      fR.reduce((a, b) => a + b.reduce((aa, bb) => aa + bb.num, 0), 0)
    );
  }

  console.log(max);
};

rl.on("line", (line) => {
  if (lineNo === 0) {
    [n, m] = line.split(" ").map((x) => 1 * x);
    arr.push(new Array(n + 1).fill(-1));
  } else if (lineNo <= n) arr.push([-1, ...line.split(" ").map((x) => 1 * x)]);
  else fArr.push(line.split(" ").map((x) => 1 * x));
  lineNo += 1;
}).on("close", () => {
  solve();
  process.exit(0);
});
```

남이 방문한 곳을 방문할 수는 있는데 이를 처리 안해서 문제였습니다!!!
