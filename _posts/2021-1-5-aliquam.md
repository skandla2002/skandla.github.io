---
layout: post
title: TypeScript - 4
description: TypeScript, 생산성, 인터페이스
# image: assets/images/pic01.jpg
---

# 오늘의 느낌:   
 처음 opensource 에 대해 파악하고 PR 하고 싶은 프로젝트를 발견하여 소스 분석 중이다.
 해당 프로젝트가 TypeScript를 기반으로 하고 있어, 지금 공부한 것을 바탕으로 진행 하고 싶다.


# 인터페이스   
- 자바에서는 클래스를 구현하기 전에 필요한 메서드 정의하는 역할
- 타입스크립트는 다양한 것들을 정의함

1. 객체타입 정의   

```
// 객체타입 정의하기
interface Person {
    name: string;
    age: number;
}

const p1: Person = {name: 'andy', age: 35};
const p2: Person = {name: 'andy', age: '35'}; // error

// 선택 속성
interface Person {
    name: string;
    age?: number;
}

// 유니온 정의시 필수적으로 age가 함께 정의 되어야 함
interface Person {
    name: string;
    age: number | undefined;
}

// 읽기 전용 속성
interface Person {
    readonly name: string;
    age?: number;
}
const p1: Person = {
    name: 'mike'
};
p1.name = 'jone'; // error

// 정의되지 않은 속성값에 대한 처리
interface Person {
    readonly name: string;
    age?: number;
}
const p1: Person = {
    name: 'mike',
    birthday: '1997-01-01' // error
};

const p2 = {
    name: 'mike',
    birthday: '1997-01-01'
}
const p3: Person = p2; // p3가 p2를 포함하는 더 큰 타입이므로 error 발생하지 않음

```

2. 인터페이스로 정의하는 인덱스 타입
- 속성 이름을 구체적으로 정의하지 않고 값의 타입만 정의하는 것(인덱스 타입)

```
// 인덱스 타입
interface Person {
    readonly name: string;
    age: number;
    [key: string]: string | number;
}
const p1: Person = {
    name: 'mike',
    birthday: '1997-01-01', // error 발생하지 않음
    age: '25' // error
}

// 여러개의 인덱스를 정의하는 경우
interface YearPricemap {
    [year: number]: A; 
    [year: string]: B; // B는 A조건을 만족해야함
}

interface YearPriceMap {
    [year: number]: number;
    [year: string]: string | number;
}
const yearMap: YearPricemap = {};
yearMap[1998] = 1000;
yearMap[1998] = 'abc'; // error
yearMap['2000'] = 1000;
yearMap['2000'] = 'abc';

```

3. 그밖에 할 수 있는 것   

```
// 인터페이스로 함수 타입 정의
interface GetInfoText {
    (name: string, age: number): string; // 인터페이스로 함수 정의시에는 속성이름 없이 정의함
}
const getInfoText; GetInfoText = function(name, age) {
    const nameText = name.substr(0, 10);
    const ageText = age >= 35 ? 'senior' : 'junior';
    return `name: ${nameText}, age: ${ageText}`;
}

// 인터페이스 함수타입인 경우 추가 속성 입력 가능
interface GetInfoText {
    (name: string, age: number): string;
    totalCall: number; // 추가 속성 입력 가능
}
const getInfoText: GetInfoText = function (name, age) {
    getInfoText.totalCall += 1;
    console.log(`totalCall: ${getInfoText.totalCall}`);
};
getInfoText.totalCall = 0;

// 인터페이스로 클래스 구현하기
interface Person {
    name: string;
    age: number;
    isYoungerThan(age: number): boolean;
}
class SomePerson implements Person {
    name: string;
    age: number;
    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }
    isYoungerThan(age: number) {
        return this.age < age;
    }
}

// 인터페이스 확장하기
interface person {
    name: string;
    age: number;
}
interface Korean extends Person {
    isLiveInSeoul: boolean;
}
/*
interface Korean {
    name: string;
    age: number;
    isLiveInSeoul: boolean;
}
*/

// 여러개의 인터페이스 확장
interface Programer {
    favoritprograminglanguage: string;
}
interface Korean extends Person, Programmer {
    isLiveInSeoul: boolean;
}

// 인터페이스 합치기 - 교차타입 이용하여 하나로 합침

interface Person {
    name: string;
    age: number;
}

interface Product {
    name: string;
    price: number;
}

type PP = Person & Product;
const PP: PP = {
    name: 'a',
    age: 23,
    price: 1000
}

```

---------
+ 참고: 실전리액트프로그래밍 / 이재승 지음 / 인사이트


---------