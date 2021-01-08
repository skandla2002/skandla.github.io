---
layout: post
title: Algorytm - BackTracking, DFS, BFS
description: BackTracking, DFS, BFS
image: assets/images/notebook-dev.jpg
---

# 오늘 회고:

오늘 본 모의평가에 나온 알고리즘 기초 작성

# BackTracking: 특정 범위를 지정하여 탐색할때 사용함

## 순서:

> 1. Tree 초기화:

```
let N = 4; // 종료지점 계속 변경
let visited = new Array(N + 1);
let ans = 0;
back();

// Depth
function back (depth) {
    // 종료 조건
    if (N == depth) {
        return Count++;
    }

    // 반복 조건
    for (let i = 1 + depth ; i <= N; i++) {
        if (!visited[i]) {
            visited[i] = true;
            Count++;
            back(depth + 1, count++);
        }
    }
}
```

> 2. leafNode Size 계산:

```
function findLeafSize(int N) {
    int count = 1;
    while(N > count){
        count *= 2;
    }
    return count - 1;
}
```

> 3. indexTree 채우기

```
int leafSize = findLeafSize(N);

BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
StringTokenizer st = new StringTokenizer(br.readLine());

// ...

st = new StringTokenizer(br.readLine());
for(int i = leafSize + 1 ; i <= leafSize + N ; i++){
    tree[i] = Integer.parseInt(st.nextToken());
}

function makeIndexTree (){
    for(int i = leafSize ; i > 0 ; i--){
        tree[i] = tree[i * 2] + tree[i * 2 + 1];
    }
}

```

> 4. 조건에 따른 함수 생성: sum, update(swap)

```
function sum (int a, int b){
    int left = tree[a];
    int right = tree[b];


}

function update(int a, int b){

}

```

---

- 참고:
  > 교육

---
