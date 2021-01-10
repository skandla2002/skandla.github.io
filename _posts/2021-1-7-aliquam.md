---
layout: post
title: PWA in ReactJS
description: ReactJS, PWA
image: assets/images/notebook-dev.jpg
---

# 오늘 회고:

TF 참여로 인해 미리 공부해 둬야 할 것이 생겼다.
PWA에 대해 이론만 알고 실젝 샘플도 만들어 본 적이 없어 최초 생성 해본다.

# PWS in ReactJS 샘플 만들기

## 생성한 Repo: https://github.com/skandla2002/pwa_sample.git

## 순서

1. CRA로 템플릿 생성한다.

   > - create-react-app pwa-temp --template cra-template-pwa
   > - 위 내용으로 실행해야 PWA 설정 가능 하다.(serviceWorkerRegistration.js

2. 기본 React App 생성한다.

   > - react-router-dom 도 설치하고 경로에 따른 컴포넌트를 2개 이상 생성한다.
   > - 정상 기동 여부 확인한다.: yarn start

3. ServiceWorker를 등록한다.

   > - worker.js를 생성하여 index.html내에 직접 등록 한다.
   > - index.js 내의 serviceWorker.register(); 부분 입력한다.

4. 네트워크 환경을 offline로 변경 후 기동 화면 확인한다.

   > - index.html 내에 reactjs 등이 로드 되지 않아도 되는 테그 영역을 추가 한다.(Loading 시점 등)
   > - 정상적으로 offline 화면 나오는지 확인 한다.

5. 웹 서버 에 올리고 다운로드도 가능한지 확인한다.
   > - 외부 웹에 적용 후 테스트는 미진행

---

- 참고:
  > https://donggyu9410.medium.com/%EB%A6%AC%EC%95%A1%ED%8A%B8%EB%A1%9C-%EB%A7%8C%EB%93%A0-%ED%8E%98%EC%9D%B4%EC%A7%80-progressive-web-app-%EC%9C%BC%EB%A1%9C-%EB%A7%8C%EB%93%A4%EA%B8%B0-b97e7c330fd8 > https://blog.logrocket.com/setting-up-a-pwa-with-service-workers-and-create-react-app/

---
