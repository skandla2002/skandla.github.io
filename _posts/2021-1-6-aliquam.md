---
layout: post
title: TypeScript - 5
description: TypeScript, 생산성, 타입 호환성
image: assets/images/notebook-dev.jpg
---

# 오늘 회고:

알고리즘 문제 풀이 중 너무 해결 되지 않는 알고리즘이 있어, 결국 22:00 포기.  
이후 씻고 TypeScript 정리를 하게 되었다.  
js 알고리즘을 하나 더 추가로 공부하고 자야지.

# 타입 스크립트 - 타입 호환성

- 어떤 타입을 다른 타입으로 취급해도 되는지 판단하는 것
- 타입 A가 타입 B에 할당 가능 하다 = 타입 A 가 타입 B의 서브타입(subtype) 이다.

1. 숫자와 문자열의 타입 호환성

```
function func1(a: number, b: number | string) {
    const v1: number | string = a;
    const v2: number = b; // error
}
function func2(a: 1| 2) {
    const v1: 1 | 3 = a; // error
    const v2: 1 | 2 | 3 = a;
}
```

2. 인터페이스의 타입 호환성

- 값 자체의 타입 보다 값이 가진 내부 구조에 기반해서 타입 호환성 검사함(덕 타이핑, 구조적 타이핑)
- A가 B로 할당 가능해야 할때 조건: B의 필수조건이 A에 존재 / 같은 속성 이름에 대해 A 속성이 B의 속성에 할당 가능

```
interface Person {
    name: string;
    age: number;
}
interface Product {
    name: string;
    age: number;
}
const person: Person = { name: 'mike', age: 23 };
const product: Product = person; // 이름 달라고 내부 구조 같아 할당 가능

// 선택 속성의 영향: 선택속성이 일반 속성보다 범위가 크므로 할당에 영향을 줌
interface Person {
    name: string;
    age?: number;
}
const person: Person = {
    name: 'mike'
}
const product: Product = person; // error person이 더 큰 범위로 할당안됨

// 선택속성이 있으면 더 큰범위임
interface Person {
    name: string;
    age: number;
}
interface Product {
    name: string;
    age?: number
}
const person: Person = {
    name:'mike'
}
const product:Product = person; // 할당 가능

// 추가 속성과 유니온 타입 영향
- 추가 속성: 집합은 작아짐
- 유니온 타입: 집합은 커짐
interface Person {
    name: string;
    age: number;
    gender: string;
}
interface Product {
    name: string;
    age: number | string;
}
const product: Product = {
    name: 'andy',
    age: 35
}
const person:Person = product;
```

3. 함수의 타입 호환성

- A가 B로 할당 가능 조건: 호출하는 시점에 문제가 없어야 할당 가능
  > A의 매개변수 개수가 B의 매개변수 개수보다 적어야 함  
  > 같은 위치의 매개변수에 대해 B의 매개변수가 A의 매개변수로 할당 가능해야 함
  > A의 반환값은 B의 반환값으로 할당 가능

```
type F1 = (a: number, b: string) => number;
type F2 = (a: number) => number;
type F3 = (a: number) => number | string;
let f1: F1 = (a, b) => 1;
let f2: F2 = a => 1;
let f3: F3 = a => 1;
f1 = f2;
f2 = f1; // error, f1이 매개변수 더 많음
f2 = f3; // error, f3이 리턴값 범위 더 넓음

// 배열의 map 메서드를 통해 살펴보는 함수의 타입 호환성
function addOne(value: number) {
    return value + 1;
}
const result = [1, 2, 3].map<number>(addOne); // 반환 가능, 제네릭 number로 매개변수 함수의 반환 타입
// (value: number, index: number, array: number[]) => number // map 함수의 매개변수와 타입으로 addOne 보다 매개변수가 더 많아 정상 할당 가능함
// 매개변수는 3개까지만 가능함(4개는 map 함수에서 전달하지 않음)
// addOne 함수의 매개변수 타입이 1 | 2 | 3이면 문제됨(map 메서드는 다른 숫자 전달 가능하기 때문)
// addOne 함수의 반환 타입이 number | string 이면 문제됨(map 메서드는 숫자 배열을 반환 하기 때문)
// => 함수의 타입 호환성은 호출하는 쪽에서 생각하면 좋다.
```

---

- 참고: 실전리액트프로그래밍 / 이재승 지음 / 인사이트

---
