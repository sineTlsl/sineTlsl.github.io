---
layout: post
title: "[캡틴판교 TS] 섹션 1. 타입스크립트 소개와 배경"
date: 2023-04-23 15:58:00 +900
lastmod: 2023-04-23 15:58:00 +900
categories: [STUDY, Captain Pangyo - TS Basic]
tags: [captainpangyo, typescript]
image: 
  path: https://user-images.githubusercontent.com/97720335/233822587-60d294e1-867c-4cc0-b352-26899b803685.png
  width: 700
  alt: 타입스크립트 입문 - 기초부터 실전까지 강의 표지
---

**TS 공식 문서**: <https://www.typescriptlang.org/>

# 타입스크립트(TypeScript) 란?

<center><img src="https://user-images.githubusercontent.com/97720335/233824397-5a15426a-e55e-41a9-b063-a1f00c995b6e.png"></center>

- 타입스크립트는 자바스크립트에 타입을 부여한 언어다.
- 자바스크립트의 확장된 언어라고 볼 수 있다.
- 타입스크립트는 자바스크립트와 달리 브라우저에서 실행하려면 파일을 한번 변환해주어야 한다.
- 이 변환 과정을 `컴파일(complile)` 이라고 부른다

<br>

# 타입스크립트를 사용해야 하는 이유
아래 2가지 관점에서 자바스크립트 코드의 품질과 개발 생산성을 높일 수 있다.

## 1. 에러의 사전 방지
- 타입스크립트는 에러를 사전에 미리 예방할 수 있다.

**두 코드 모두 두 숫자의 합을 구하는 함수 코드다.**

<center><img src="https://user-images.githubusercontent.com/97720335/233824505-9061c03d-203d-42a3-ad3e-c99fc68af788.png"></center>

첫 번째 사진처럼 `sum` 함수를 이용하여 숫자 10과 20을 더할 경우에는 30이 나오게되지만, 두 번째 사진은 문자열을 더하기 때문에 1020이라는 결과가 나오게 된다. 

<center><img src="https://user-images.githubusercontent.com/97720335/233824557-c67281bf-5cd1-497a-8db0-9abeb57d8a0f.png"></center>

이처럼 타입스크립트는 의도하지 않는 코드의 동작을 예방할 수 있다.

**[VSCode에서 확인할 경우]**

<center><img src="https://user-images.githubusercontent.com/97720335/233824600-713bf70f-e055-4b26-adc9-890ec71bb4ee.png"></center>

## 2. 코드 자동 완성과 가이드
타입스크립트의 또 다른 장점은 코드를 작성할 때 개발 툴의 기능을 최대로 활용할 수 있다는 것이다.
- 코드를 작성할 때 개발 툴의 기능을 최대로 활용할 수 있다.
- `Visual Studio Code` 는 툴의 내부가 타입스크립트로 작성되어 있어 타입스크립트 개발에 최적화 되어 있다.

<br>

# JS를 TS처럼 코딩하는 방법
`JSDOC` 과 `ts-check`으로 자바스크립트에서 타입을 정의할 수 있다.

<center><img src="https://user-images.githubusercontent.com/97720335/233824663-bed9e784-fb57-42fe-925f-390df3665c3c.png"></center>  

하지만, 이 방법은 너무 번거로우므로 타입스크립트를 사용하는 것이 좋다.

---

# 🧸 Feelings ...
타입스크립트를 들어가기 전, 강의 개요 및 VSCode 세팅에 대해 알아보았다. 
이제 타입스크립트를 처음 배우는 입장으로서 앞으로 섹션 끝날 때 마다 블로그에 작성할 계획이다. 

<center><img src="https://user-images.githubusercontent.com/97720335/233823022-cebf4ec8-1d28-428e-b367-732ad6ab534c.png"></center>

<br>

**Reference**

[[캡틴판교 TS] 타입스크립트 입문 - 기초부터 실전까지](https://www.inflearn.com/course/%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%9E%85%EB%AC%B8) <br>
[타입스크립트 핸드북](https://joshua1988.github.io/ts/)

<br>

> 본 포스팅은 캡틴판교 강사님의 `타입스크립트 입문 - 기초부터 실전까지` 강의를 수강하고 난 후, 본인의 주관적인 견해에 의하여 작성되었습니다.
{: .prompt-info}