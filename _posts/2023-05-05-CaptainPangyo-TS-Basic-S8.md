---
layout: post
title: "[캡틴판교 TS] 섹션 8. 이넘"
date: 2023-05-05 13:43:00 +900
lastmod: 2023-05-05 13:44:00 +900
categories: [STUDY, Captain Pangyo - TS Basic]
tags: [captainpangyo, typescript]
image: 
  path: https://user-images.githubusercontent.com/97720335/233822587-60d294e1-867c-4cc0-b352-26899b803685.png
  width: 700
  alt: 타입스크립트 입문 - 기초부터 실전까지 강의 표지
---

# 이넘(Enums) 이란?
`이넘(Enums)` 은 특정 값들의 집합을 의미하는 자료형이다.

예를 들어, 다음과 같은 목록이 이넘이 될 수 있다.
```
나이키
아디다스
뉴발란스
```

타입스크립트에서는 `숫자형 이넘` 과 `문자형 이넘` 을 지원한다.

<br>

## 숫자형 이넘
타입스크립트에서 숫자형 이넘은 아래와 같이 선언한다.

```ts
enum Shoes {
  Nike = 1,
  Adidas
}
```
초기 값을 지정할 경우 초기 값부터 차례로 1씩 증가한다.
```
Nike - 1
Adidas - 2
```

초기 값을 주지 않을 경우 0부터 차례로 1씩 증가한다.
```ts
enum Shoes {
  Nike,
  Adidas
}

let myShoes = Shoes.Nike;
console.log(myShoes); // 0
```

<br>

## 문자형 이넘
문자형 이넘은 숫자형 이넘과 개념적으로 비슷하지만, 런타임에서 차이가 있다.

우선 **문자형 이넘은 이넘 값 전부 다 특정 문자 또는 다른 이넘 값으로 초기화를 해줘야 한다.**

```ts
enum Shoes {
  Nike = '나이키',
  Adidas = '아디다스'
}

let myShoes = Shoes.Nike;
console.log(myShoes); // '나이키'
```

또한, 문자형 이넘에는 숫자형 이넘과는 다르게 `auto-incrementing` 이 없다.

<br>

## 이넘 활용사례

문자열이 들어와서 값을 비교하는 형식이 아닌 이넘의 속성으로 비교한다.

```ts
enum Answer {
  Yes = 'Y',
  No = 'N',
}

function askQuestion(answer: Answer) {
  if (answer === Answer.Yes) {
    console.log('정답입니다');
  }
  if (answer === Answer.No) {
    console.log('오답입니다')
  }
}
askQuestion(Answer.Yes);
askQuestion('Y'); // Error
```

문자열을 넣으면 에러 발생 !

---

## 🧸 Feelings ...
이넘은 다른 프로그래밍 언어를 사용해본 사람들이란 어렵지 않고 익숙할 거라고 말씀해주셨다. 그래서 그런지 나 또한 어려운 부분은 아니었다. 

<div align="center"><img src="https://user-images.githubusercontent.com/97720335/236379010-fbf7d76d-dbff-4a47-bd97-01466bcef6cb.png"></div>

<br>

**Reference**

[[캡틴판교 TS] 타입스크립트 입문 - 기초부터 실전까지](https://www.inflearn.com/course/%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%9E%85%EB%AC%B8) <br>
[타입스크립트 핸드북](https://joshua1988.github.io/ts/)

<br>

> 본 포스팅은 캡틴판교 강사님의 `타입스크립트 입문 - 기초부터 실전까지` 강의를 수강하고 난 후, 본인의 주관적인 견해에 의하여 작성되었습니다.
{: .prompt-info}