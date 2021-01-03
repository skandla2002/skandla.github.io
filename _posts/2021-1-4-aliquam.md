---
layout: post
title: TypeScript - 3
description: TypeScript, 생산성
image: assets/images/pic01.jpg
---

# 오늘의 느낌:   
 처음 opensource 에 대해 파악하고 PR 하고 싶은 프로젝트를 발견하여 소스 분석 중이다.
 해당 프로젝트가 TypeScript를 기반으로 하고 있어, 지금 공부한 것을 바탕으로 진행 하고 싶다.


# 타입 스크립트의 여러가지 타입 - 2   

## 열거형 타입: enum 사용   

```
enum Fruit {
    Apple,
    Banana,
    Melon
}
const v1: Fruit = Fruit.Apple; // Apple을 값으로 사용
const v2: Fruit.Apple | Fruit.Banana = Fruit.Banana; // Apple을 타입으로 사용

enum Fruit {
    Apple,
    Banana = 5,
    Melon
}
console.log(Melon); // 6, 명시적으로 1씩 증가함

// 열거형은 컴파일 후에도 관련 코드가 남아서 객체를 사용 할 수 있음
console.log(Fruit.Banana); // 5
console.log(Fruit['Banana']); // 5
console.log(Fruit[5]); // 'Banana'

// 열거형 타입 원소에 문자열 할당(단방향 맵핑, 이름 같은경우 충돌 이슈)
enum Lang {
    Korean = 'ko',
    English = 'en',
    Chinese = 'zh',
    Japanese = 'ja'
}

// 열거형 타입을 위한 유틸리티 함수: 테스크 코드 작성에 유리함
// - 원소 갯수 확인
function getEnumLen(enumObj: any) {
    const keys = Object.keys(enumObj);
    return keys.reduce((acc, key) => (typeof enumObj[key] === 'string' ? acc + 1 : acc))
}

// - 열거형 타입에 존재하는 값인지 검사
function isValidEnumVal(enumObj: any, val: number | string) {
    if (typeof value === 'number') {
        return !!enumObj[val];
    } else {
        return (
            Object.keys(enumObj)
                .filter(key => isNaN(number(key)))
                .find(key => enumObj[key] === val) != null
        )
    }
}

// 상수 열거형 타입: 컴파일 결과에 열거형 타입 객체 남기지 않을 수 있음
// 단, 열거형 타입을 상수로 정의하면 열거형 타입의 객체 사용 불가
const enum Fruit {
    Apple,
    Banana,
    Melon
}
const fruit: Fruit = Fruit.Apple;

const enum Lang {
    Korean = 'ko',
    English = 'en',
    Chinese = 'zh',
    Japanese = 'ja'
}
```

## 함수 타입: 매개변수 타입과 반환 타입  

```
function getInfoText(name: string, age: number): string {
    const nameText = name.substr(0, 10);
    const ageText = age >= 35 ? 'senior' : 'junior';
    return `name: ${nameText}, age: ${ageText}`;
}
const v1: string = getInfoText('andy', 35);
const v2: string = getInfoText('andy', '35'); // error
const v3: number = getInfoText('andy', 35); // error

// 변수를 함수 타입으로 정의하기
const getinfoText: (name: string, age: number) => string = function(name, age) {
    ...
};

// 선택 매개변수: 반드시 입력하지 않아도 되는 변수
function getInfoText(name: string, age: number, lang?: string): string {
    const nameText = name.substr(0, 10);
    const ageText = age >= 35 ? 'senior' : 'junior';
    const langText = lang ? lang.substr(0, 10) : '';
    return `name: ${nameText}, age: ${ageText}, lang: ${langText}`;
}
// 선택 매개변수 오른쪽에 필수 매개변수를 정의한 코드: 컴파일 에러 발생
function getInfoText(name: string, lang?: string, age: number): string {
    ...
}
=> 오류없이 구현하려면 undefined 이용
function getInfoText(
    name: string,
    lang: string | undefined,
    age: number
): string {
    // ...
}

// 매개변수의 기본값 정의하기
function getInfoText (
    name: string,
    age: number = 15, // 기본값 15
    lang = 'korean' // 기본값 'korean'
): string {
    // ...
}

// 나머지 매개변수: 배열로 정의 할 수 있음
function getInfoText(name: string, ...rest: string[]): string {
    //...
}

// this 타입: 미정의시 기본 this는 any 타입, this는 첫번째 매개변수가 된다.
function getParam(index: number): string{
    const params = this.splt(','); // 오타지만 any type으로 컴파일 에러 발생하지 않는다.
    if ( index < 0 || param.length <= index) {
        return '';
    }
    return this.split(',')[index];
}

function getParam(this: string, index: number): string {
    const params = this.splt(','); // error
}

// 원시 타입에 메서드 추가하기: interface 이용함
interface String {
    getParam(this: string, index: number): string;
}
String.prototype.getParam = getParam;

console.log('as, 12, test'.getParam(1)); // 'as'

// 함수 오버로드
// ex) 두 매개변수가 모두 문자열이면 문자열 리턴, 숫자면 숫자 리턴, 두개가 다른 타입 입력하면 안됨

// 1) 함수 오버로드 없는 경우 - 오류
function add(x: number | string, y: number | string): number | string {
    if (typeof x === 'number' && typeof y === 'number') {
        return x + y;
    } else {
        const result = Number(x) + Number(y);
        return result.toString();
    }
}
const v: number = add(1, 2); // 매개변수 숫자, 반환도 숫자인데 타입 에러
console.log(add(1, '2')); // 타입이 다른데 에러 없음

// 2) 함수 오버로드 사용
function add(x: number, y: number): number;
function add(x: string, y: string): string;
function add(x: number | string, y:number | string): number | string {
    // ...
}
const v: number = add(1, 2); // 정상
console.log(add(1, '2')); // 타입 에러

// 명명된 매개변수: 이름 정의 > 타입 정의
function getInfoText({
    name,
    age = 15,
    lang
}: {
    name: string;
    age?: number;
    lang: string;
}): string {
    const nameText = name.substr(0, 10);
    ocnst ageText = age >= 35 ? 'senior' : 'junior';
    return `name: ${nameText}, age: ${ageText}, lang: ${langText}`;
}
=> 인터페이스 이용
interface Param {
    name: string;
    age?: number;
    lang?: string;
}
function getInfoText({ name, age = 15, lang }: Param): string {
    // ...
}

```

---------
+ 참고: 실전리액트프로그래밍 / 이재승 지음 / 인사이트


---------