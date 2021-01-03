---
layout: post
title: TypeScript - 2
description: TypeScript, 생산성
image: assets/images/pic01.jpg
---

# 오늘의 느낌:   
 현재 사용중인 React.js를 좀더 견고하게 만들어주는 TypeScript에 대해   
 이야기만 듣고 실제 사용해보지 않았었다.   
 이에 대해 알아보기 위해 정리를 시작한다.

## 생산성이 높은 이유   
- 정적 타입 언어의 코드는 타입으로 서로 연결 되어 있음
    1. 연관된 코드 간의 이동이 쉬움
    2. 리팩터링 쉬움
    3. 단축키 한번이면 IDE가 필요한 임포트 코드를 자동으로 넣어줌
    4. 함수 이름과 괄호 입력시 매개변수 종류와 반환값의 타입을 확인
    5. 객체 이름과 점을 입력시 속성값 목록 확인
    6. 철자 틀리거나 타입 오류시 IDE가 즉시 알려줌

## 실습 가능한 URL  

> http://typescriptlang.org/play


# 타입 스크립트의 여러가지 타입   

```
const width: number = 123;
const isBag: boolean = false;
const message: string = 'hello';
const arrVal1: number[] = [1, 2, 3];
const arrVal2: Array<number> = [1, 2, 3];
const data: [string, number] = [message, width]; // 튜플(tuple)타입 정의

let v1: undefined = undefined;
let v2: null = null;
let v3: number | undefined = undefined; // 다른 타입과 유니온으로 자주 사용됨
v3 = 3;

let n1: 10 | 20 | 30;
n1 = 10;
n1 = 15; // error 발생
let s1: 'sing' | 'again';
s1 = 'music'; // error 발생

let val: any; // 기존에 자바스크립트 코드로 작성된 프로젝트를 타입스크립트로 포팅 하는 경우 사용
val = 123;
val = '123';
val = () => { console.log('123'); };

// void: 아무값 반환 없이 종료 되는 것
function f1(): void {
    console.log('hello');
}
// never: 항상 예외 발생해서 비정상적 종료되거나, 무한 루프때문에 종료 되지 않는 함수의 반환 되는 것
function f2(): never {
    throw new Error('new error');
}
function f3(): never {
    while(true){
        console.log('hello');
    }
}

let obj: object;
obj = { name: 'abc' };
console.log(obj.prop1); // 타입 에러, 속성정보 없을때 타입 정의하기 위해서는 인터페이스를 사용

// 교차타입 &, 유니온 타입 |
let v1: (1 | 2 | 3) & ( 2 | 3);
v1 = 3;
v1 = 1; // error

// type 키워드로 타입에 별칭 주기
type Width = number | string;
let width: Width;
width = 100;
width = '100px';

```

---------
+ 참고: 실전리액트프로그래밍 / 이재승 지음 / 인사이트


---------