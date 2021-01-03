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

```
// 열거형 타입: enum 사용
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




```

---------
+ 참고: 실전리액트프로그래밍 / 이재승 지음 / 인사이트


---------