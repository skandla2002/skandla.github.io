---
layout: post
title: 2021년 새롭게 공부할것 정리하기(1. Markdown)
description: MarkDown 정의, 문법
image: assets/images/pic01.jpg
---

+ 2021년 마크다운 문법으로 글 작성 하려고 마크다운 문법에 대해 기초적인 내용을 정리 해 본다.

# 정의
- 텍스트 기반의 마크업 언어.
- 깃헙의 README.md로 인해 유명해짐

# 장단점
## 장점
 ```
 1. 간결
 2. 별도 도구 불필요
 3. 텍스트 저장으로 용량 적음
 4. 텍스트 파일로 버전관리시스템으로 변경 이력 관리 가능
 5. 지원하는 플랫폼 다양
 ```
## 단점
 ```
 1. 표준 없음
 2. 도구따라 변환 방식/생성물 다름
 3. 모든 HTML 마크업을 대신하지 못함
 ```

# 문법
## 헤더
+ 큰제목: 문서 제목
```
 H1
 ======
```
+ 작은 제목: 문서 부제목
```
 H2
 -----
```
+ 글머리: 1~6까지 지원
```
# H1
## H2
### H3
#### H4
##### H5
###### H6
```

## BlockQuote
이메일에서 사용하는 > 블럭 인용 문자 사용
```
> first
>     > second
>     >     > third
```
> first
>     > second
>     >     > third

## 목록
+ 순서있는 목록(번호)
순서 있는 목록은 숫자와 점을 사용
```
1. first
2. second
3. third
```
1. first
2. second
3. third

+ 순서 없는 목록(글머리 기호: *, +, -)

```
* first
    + second
        - third
```

* first
    + second
        - third

## 코드
4개의 공백 또는 하나의 탭으로 들여쓰기를 만나면 변환되기 시작하여 들여쓰지 않은 행을 만날때 까지 변환이 계속 된다.
+ 들여쓰기
```
normal paragraph:
    code block
end code block
```
normal paragraph:
    code block
end code block

+ 코드 블럭
: 2가지 방식 사용함

1. ```<pre><code>{code}</code></pre>``` 이용
<pre><code>
    class List {
        constructor(props){
            super(props);
        }
    }
</code></pre>

2. 코드블럭코드(```)를 이용하는 방법 
```
class List {
    constructor(props){
        super(props);
    }
}
```

## 수평선: <hr/>
```
* * *
***
*****
- - -
______________
```
- - -

## 링크
+ 참조 링크

```
[link keyword][id]
[id]: URL "Title Area"

// code
Link: [Google][googleLink]
[googleLink]: https://google.com "Go Google!!!"
```

Link: [Google][googleLink]
[googleLink]: https://google.com "Go Google!!!"

+ 외부 링크

```
사용문법: [Title](link)

//code
구글연결: [Google](https://google.com, "google link")
```

구글연결: [Google](https://google.com, "google link")

+ 자동연결

```
일반적인 URL 혹은 이메일 주소 링크

// code
* 외부링크: <http://google.com/>
* 이메일 링크: <skandla2002@gmail.com>
```

* 외부링크: <http://google.com/>
* 이메일 링크: <skandla2002@gmail.com>

## 강조

```
*text*
_text_
**text**
__text__
~~text~~
```

*text*   
_text_   
**text**   
__text__   
~~text~~   

## 이미지

```
![Alt text](../assets/images/pic04.jpg)
![Alt text](../assets/images/pic04.jpg, "Title Text: Wolf")
```

![Alt text](../assets/images/pic04.jpg)
![Alt text](../assets/images/pic04.jpg, "Title Text: Wolf")

+ 사이즈 조절: ```<im width="" height=""></img>```

```
<img src="../assets/images/pic04.jpg" width="400px" height="250px" title="px 크기 설정" alt="wolf">
<br/>
<img src="../assets/images/pic04.jpg" width="40%" height="30%" title="px 크기 설정" alt="wolf">
```

<img src="../assets/images/pic04.jpg" width="400px" height="250px" title="px 크기 설정" alt="wolf">
<br/>
<img src="../assets/images/pic04.jpg" width="40%" height="30%" title="px 크기 설정" alt="wolf">

## 줄바꿈
3칸이상 띄어쓰기('   ')

```
줄바꿈을 위해서는 이렇게 한다.   
바뀐줄
```

줄바꿈을 위해서는 이렇게 한다.   
바뀐줄

# MarkDown Editor:
1. 기본은 VS code에서 사용
2. 개발시에는 [tui editor](https://github.com/nhn/tui.editor)를 사용 한다.


---------
+ 참고: https://gist.github.com/ihoneymon/652be052a0727ad59601



---------