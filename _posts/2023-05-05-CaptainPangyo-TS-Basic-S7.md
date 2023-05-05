---
layout: post
title: "[캡틴판교 TS] 섹션 7. 연산자를 이용한 타입 정의"
date: 2023-05-05 11:16:00 +900
lastmod: 2023-05-05 11:16:00 +900
categories: [STUDY, Captain Pangyo - TS Basic]
tags: [captainpangyo, typescript]
image: 
  path: https://user-images.githubusercontent.com/97720335/233822587-60d294e1-867c-4cc0-b352-26899b803685.png
  width: 700
  alt: 타입스크립트 입문 - 기초부터 실전까지 강의 표지
---

# Union Type 이란?
`유니온 타입(Union Type)` 이란 자바스크립트의 OR 연산자 (`||`)와 같이 'A이거나 B다' 라는 의미의 타입이다.

다음 코드 예시처럼 string 타입과 number 타입 둘 다 가능하다.
```ts
function logMessage(value: string | number) {
  console.log(value);
}

logMessage('hello');
logMessage(100);
```

<br>

## Union Type의 장점
타입 가드를 활용할 수 있다.
  - `타입 가드(Type Guard)` : 특정 타입으로 타입의 범위를 좁혀나가는(필터링 하는) 과정

```ts
function logMessage(value: string | number) {
  // 타입 가드
  if (typeof value === 'number') {
    value.toLocaleString();
  } if (typeof value === 'string') {
    value.toString();
  }

  throw new TypeError('value must be string or number');
}
```

<br>

## Union의 특징
유니온 타입으로 인터페이스 두 개 이상을 연결할 때, 공통된 즉, 보장된 속성만 제공한다.

```ts
interface Developer {
  name: string;
  skill: string;
}

interface Person {
  name: string;
  age: number;
}
```

위와 같아 인터페이스를 선언하면 공통으로 작성된 `name` 만 사용할 수 있는 걸 확인할 수 있다.

<div align="center"><img src="https://user-images.githubusercontent.com/97720335/236362903-e1427546-e5d8-4879-96d8-75c13426ff75.png" width="80%" ></div>

<br>

## Intersection Type 이란?
`인터섹션 타입(Intersection Type)` 은 여러 타입을 모두 만족하는 하나의 타입을 의미한다.

위에서 인터페이스로 타입 정의한 `Developer` 와 `Person` 를 `&` 연산자를 이용하여 합친 후 `askSomeone` 함수 타입에 선언할 때 다음과 같이 활용할 수 있다.

```ts
function askSomeone(someone: Developer & Person) {
  someone.name
  someone.skill
  someone.age
}
```

이처럼 `&` 연산자를 이용해 여러 개의 타입 정의를 하나로 합치는 방식을 인터섹션 타입 정의 방식이라고 한다.

<div align="center"><img src="https://user-images.githubusercontent.com/97720335/236363759-8220c4b2-9db5-4185-86ee-9feace89d844.png" width="80%" ></div>

---

## 🧸 Feelings ...
실무에서 사용하는 건 인터섹션 타입보단 유니온 타입을 더 많이 사용하니까 이 부분을 기억하자

<div align="center"><img src="https://user-images.githubusercontent.com/97720335/236364873-00898dab-ef86-42f0-b16b-aa7a8fdddb32.png"></div>

<br>

**Reference**

[[캡틴판교 TS] 타입스크립트 입문 - 기초부터 실전까지](https://www.inflearn.com/course/%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%9E%85%EB%AC%B8) <br>
[타입스크립트 핸드북](https://joshua1988.github.io/ts/)

<br>

> 본 포스팅은 캡틴판교 강사님의 `타입스크립트 입문 - 기초부터 실전까지` 강의를 수강하고 난 후, 본인의 주관적인 견해에 의하여 작성되었습니다.
{: .prompt-info}