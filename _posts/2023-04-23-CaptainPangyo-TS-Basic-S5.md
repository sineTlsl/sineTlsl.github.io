---
layout: post
title: "[캡틴판교 TS] 섹션 5. 인터페이스"
date: 2023-04-23 20:01:00 +900
lastmod: 2023-04-23 20:01:00 +900
categories: [STUDY, Captain Pangyo - TS Basic]
tags: [captainpangyo, typescript]
image: 
  path: https://user-images.githubusercontent.com/97720335/233822587-60d294e1-867c-4cc0-b352-26899b803685.png
  width: 700
  alt: 타입스크립트 입문 - 기초부터 실전까지 강의 표지
---

# 인터페이스(Interface) 란?
- `인터페이스` 는 상호 간에 정의한 약속 혹은 규칙을 의미한다.
- 타입스크립트에서의 인터페이스는 보통 다음과 같은 범주의 대해 약속을 정의할 수 있다.
  - 객체의 스펙(속성과 속성의 타입)
  - 함수의 파라미터
  - 함수의 스펙(파라미터, 반환 타입 등)
  - 배열의 객체를 접근하는 방식
  - 클래스

<br>

## ✔︎ 인터페이스 예시
```ts
interface User {
  age: number;
  name: string;
}
```

### 1. 변수에 인터페이스 활용

```ts
let seho: User = {
  age: 33,
  name: '세호'
}
```

### 2. 함수에 인터페이스 활용

```ts
function getUser(user: User) {
  console.log(user);
}
const capt = {
  name: '캡틴',
  age: 100
}

getUser(capt);
```

### 3. 함수의 스펙(구조)에 인터페이스를 활용

```ts
interface sumFunction {
  (a: number, b: number): number;
}

let sum: sumFunction;
sum = function(a: number, b: number): number {
  return a + b;
}
```

### 4. 인덱싱

특정 인덱스의 타입을 문자열로 정의할 수 있다.

```ts
interface StringArray {
  [index: number]: string;
}

let arr: StringArray = ['a', 'b', 'c'];
arr[0]; // 'a'
```

### 5. 딕셔너리 패턴

```ts
interface StringRegexDictionary {
  [key: string]: RegExp;
}

let obj: StringRegexDictionary = {
  cssFile: /\.css$/, // css 확장자 파일 모두 해당
  jsFile: /\.js$/, // js 확장자 파일 모두 해당
}

// 정규표현식이 할당 되어야하는데 일반 문자열이 들어와서 error 발생  
obj['cssFile'] = 'a'; 

Object.keys(obj).forEach(function(value) {});
```

### 6. 인터페이스 확장
다음과 같이 중복되는 속성은 상속을 받을 수 있다.

```ts
interface Person {
  name: string;
  age: number;
}
interface Developer extends Person {
  language: string;
}

let captain: Developer = {
  language: 'ts',
  age: 100,
  name: '캡틴'
}
```

---

## 🧸 Feelings ...
이번 시간에는 인터페이스와 관련되어서 알아보았다. <br>
상속받는 개념은 객체지향 언어에서 사용했던 부분이라 별 어려움 없이 금방 넘어갈 수 있었다.

<div align="center"><img src="https://user-images.githubusercontent.com/97720335/233843331-f4a18165-a20f-4f05-afb5-05ca66cb0b2b.png"></div>

<br>

**Reference**

[[캡틴판교 TS] 타입스크립트 입문 - 기초부터 실전까지](https://www.inflearn.com/course/%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%9E%85%EB%AC%B8)

<br>

> 본 포스팅은 캡틴판교 강사님의 `타입스크립트 입문 - 기초부터 실전까지` 강의를 수강하고 난 후, 본인의 주관적인 견해에 의하여 작성되었습니다.
{: .prompt-info}