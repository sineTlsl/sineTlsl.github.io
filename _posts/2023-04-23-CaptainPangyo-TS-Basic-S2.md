---
layout: post
title: "[캡틴판교 TS] 섹션 2. 타입스크립트 시작하기"
date: 2023-04-23 16:20:00 +900
lastmod: 2023-04-23 16:20:00 +900
categories: [STUDY, Captain Pangyo - TS Basic]
tags: [captainpangyo, typescript]
image: 
  path: https://user-images.githubusercontent.com/97720335/233822587-60d294e1-867c-4cc0-b352-26899b803685.png
  width: 700
  alt: 타입스크립트 입문 - 기초부터 실전까지 강의 표지
---

## 타입스크립트 프로젝트 시작하는 방법
### 1. `ts` 파일을 생성한다.

```ts
// index.ts
function sum(a: number, b: number) {
  return a + b;
}

sum(10, 20);
```

### 2. 타입스크립트를 글로벌로 설치한다.

```shell
npm i typescript -g
```

### 3. `ts` 파일을 `js` 파일로 컴파일한다.
- `tsc` 명령어: 타입스크립트를 자바스크립트로 변환할 때 사용한다.
- 터미널에 `tsc index.ts` 입력할 경우, js 파일 자동으로 생성된다.

<div align="center"><img src="https://user-images.githubusercontent.com/97720335/233825303-6fd055e7-b2e6-40cb-9903-a95d2cf66fd0.png" width="90%"></div>

## 타입스크립트 설정 파일 (tsconfig.json)
- 타입스크립트 설정 파일은 타입스크립트를 자바스크립트로 변환할 때의 설정을 정의해놓는 파일이다.
- 프로젝트에서 `tsc` 명령어를 치면 타입스크립트 설정 파일에 정의된 내용을 기준으로 컴파일을 진행한다.

### tsconfig.json 파일 속성
tsconfig.json 파일 생성해서 컴파일을 부가 옵션(`compilerOptions`)을 지정한다. 즉, 프로젝트를 타입스크립트로 변환할 때 타입스크립트가 이 프로젝트를 어떻게 이해할 지 정해주는 것이다.
- `allowJs` : 타입스크립트 컴파일 작업을 진행할 때 자바스크립트 파일도 포함될 수 있는지를 설정해주는 속성이다.
- `checkJs` : 타입스크립트의 검사 기능을 자바스크립트에 허용하는 속성이다.
- `noImplicitAny` : any라는 타입이 의도치않게 발생할 경우 에러를 띄워주는 속성이다.

<br>

## 추천 사이트
### 1. [바벨 사이트](https://babeljs.io/)
자바스크립트의 최신 문법을 최대한 많은 브라우저에서 허용할 수 있도록 변환해주는 사이트

### 2. [타입스크립트 플레이그라운드](https://www.typescriptlang.org/play?#code/MYewdgzgLgBAhgJygS2jAvDARAQQK4Dme0cMAynAG5wECmWA3AFCiQgA2tAdOyAQBQBveElSwAvgEogA)
타입스크립트 공식문서에 있는 플레이그라운드다. 간단하게 코드를 작성하고 확인할 수 있다. 
- `tsc` 명령어를 입력한 것과 같다.

---

## 🧸 Feelings ...
타입스크립트 파일 설정하는 방법을 보았는데, `tsconfigs.json` 에 들어가는 속성들이 많아서 개인적으로 정리해야할 것 같다.

<div align="center"><img src="https://user-images.githubusercontent.com/97720335/233825430-a7784885-b297-416e-b58a-d8d0cf55cfae.png"></div>

<br>

**Reference**

[[캡틴판교 TS] 타입스크립트 입문 - 기초부터 실전까지](https://www.inflearn.com/course/%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%9E%85%EB%AC%B8) <br>
[타입스크립트 핸드북](https://joshua1988.github.io/ts/)

<br>

> 본 포스팅은 캡틴판교 강사님의 `타입스크립트 입문 - 기초부터 실전까지` 강의를 수강하고 난 후, 본인의 주관적인 견해에 의하여 작성되었습니다.
{: .prompt-info}