---
layout: post
title: Algorytm - BackTracking
description: BackTracking
image: assets/images/notebook-dev.jpg
---

# 오늘 회고:

오늘 본 모의평가에 나온 알고리즘 기초 작성

# BackTracking: 특정 범위를 지정하여 탐색할때 사용함

## 문제:

> N개의 좌 -> 우는 순서를 위 -> 아래는 점수를 나타낼때,  
> 각 숫자의 순서와 숫자에 따른 점수가 arrData 내에 존재하면,  
> 이때 숫자를 정렬할때 최대 점수의 합을 구하면?

## 순서:

> 1. BackTracking 인자 선언 및 초기화:
>    점수 등의 포인트 / 방문 flag 배열 / 결과값 저장

```
// 3개의 선택을 할까 가장 큰 점수
let N = 3; // 종료지점 계속 변경
let arrData = [[0,0,0, 0], [1,2,3, 4], [4, 5, 6, 7], [7, 8, 9, 10]]; // 점수
let visited = new Array(N + 1);
let max = -1;
let ans = 0;


// 초기화
for(let v = 0; v <= 3 ; v++){
    visited[v] = false;
}

```

> 2. BackTracking 함수 생성: 종료 조건에 리턴 및 결과 저장

```

// Depth
function back (depth, count) {
    <!-- console.log('ans', ans, 'depth', depth, 'count', count, N == depth); -->
    // 종료 조건
    if (N == depth) {
        if(max < count){
            ans = count;
        }
        return;
    }

    // 반복 조건
    for (let i = 1 ; i <= N; i++) {
        <!-- console.log('i', i, 'depth', depth, 'count', count); -->
        let next = i;
        <!-- visited[i] = true; // 현재 방문 지점 마킹 -->

        if (!visited[next]) {
            visited[next] = true;
            count = count + arrData[depth+1][next];
            back(depth + 1, count);
            visited[next] = false;
        }
    }
}

```

> 3. 함수 실행

```

back(0, 0);

console.log('ans', ans);

```

---

- 참고:
  > 교육

---
