---
layout: post
title: Algorytm - Index Tree
description: Index Tree
image: assets/images/notebook-dev.jpg
---

# 오늘 회고:

어제 / 오늘 배운 알고리즘을 복습하기 위해 작성해 본다.

# Index Tree: 포화 바이너리 트리 구조, 분할하여 계산할때 사용함

## 순서:

> 1. Tree 초기화:

```
int[] tree = new int[4 * N + 1];
```

> 2. leafNode Size 계산:

```
function findLeafSize(int N) {
    int count = 1;
    while(N > count){
        count *= 2;
    }
    return count - 1; // 처음 시작점을 찾기 위한 값으로 leafnode의 총 갯수 (ex. 3depth의 8이 아닌 7)로 리턴함
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
let ans = 0;

function sum (int a, int b){
    int left = a + leafSize;
    int right = b + leafSize;

    if(a % 2 == 1) ans = ans + tree[left];
    if(b % 2 == 0) ans = ans + tree[right];

    <!-- ... 미완성 -->
}

function update(int a, int b){
    <!-- ... 미완성 -->
}

```

---

- 참고:
  > 교육

---
