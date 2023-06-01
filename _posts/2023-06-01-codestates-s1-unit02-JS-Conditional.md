---
layout: post
title: "[S1-Unit02] JavaScript 기초 - 조건문(Conditional)"
date: 2023-06-01 15:31:00 +900
lastmod: 2023-06-01 17:30:00 +900
categories: [CODESTATES, Section01]
tags: [CODESTATES, 코드스테이츠, Section01]
use_math: true
---

# 조건문(Conditional) 이란?

> `조건문(條件文, Conditional)` 이란 어떤 조건이 주어질 때 어떤 동작을 수행하도록 하는, 즉 조건에 따라 실행이 달라지게 할 때 사용되는 문장이다.
{: .prompt-info} 

## 1. if문
> `if문` 은 주어진 조건식의 참(true) / 거짓(falst) 여부에 따라 실행이 결정된다.
{: .prompt-info} 

참과 거짓을 판단하기 위한 JavaScript의 타입은 불린 타입이라는 것을 알 수 있다. 따라서 조건식은 결과가 불린 타입이 되도록 작성해야 한다.

조건식의 평가 결과가 참일 때 `'hello word'` 를 출력하기 위한 코드는 이와 같다.

```js
if (true) {
  console.log('hello world');
}
```

`if` 뒤에 있는 소괄호에 조건식을 넣으면, 조건식이 참으로 평가된 경우 코드블럭 내부의 코드가 실행된다. 지금은 `true` 를 넣었기 때문에 `console.log('hello world')` 가 실행된다.

조건식을 상황에 맞게 작성하면 특정 상황에만 코드가 실행되도록 할 수 있다. 

<br>

### 동치연산자 (===)

**동치연산자**는 두 피연산자가 동일하면 `true`, 그렇지 않으면 `false` 를 반환한다. `!==` 는 반대로 두 피연산자가 동일하지 않으면 `true` , 동일하면 `false` 를 반환한다.

```js
let name = 'kimcoding';
if (name === 'kimcoding') {
	console.log('중복된 이름입니다.');  // '중복된 이름입니다.'
}
```

```js
let name = 'parkhacker';
if (name !== 'parkhacker') {
	console.log('가입할 수 있는 이름입니다.');  // '가입할 수 있는 이름입니다.'
}
```

### 비교연산자 (> , < , >= , <=)

**비교연산자**는 두 피 연산자의 값의 크기를 비교한다. 수학에서의 부등호 기호의 사용법과 유사하다.

```js
let num = 5;
if (num < 10) {
  num = num + 1;
}
console.log(num);  // 6

if (num > 5) {
	num = num - 5;
}
console.log(num);  // 5
```

### 논리연산자(&&, ||)

논리합(`||`)과 논리곱(`&&`)을 사용하면 복수의 조건을 작성할 수 있다. `||` 은 여러 조건 중 하나만 	`true` 여도 `true` 로 판단된다. `&&` 은 여러 조건 중 하나라도 `false` 이면 `false` 로 판단된다.

```js
let age = 15;
if (age > 13 && age <= 19) {
	console.log('청소년입니다.');  // '청소년입니다.'
}
```

### 부정연산자 (!)

**부정연산자**는 조건을 부정한다. 조건이 `true` 이면 `false`, 조건이 `false` 이면 `true` 로 리턴한다.

```js
let num = 11;
if (!(num === 10)) {
	console.log('변수 num은 10이 아닙니다.');  // '변수 num은 10이 아닙니다.'
}
```

<br>

## 2. else문

if문을 사용하여 조건식이 true일 때만 코드가 실행되도록 할 수 있었다. 조건이 `true` 일 때, 그리고 `false` 일 때 각각 다른 코드가 실행될 수 있도록 **else문**을 사용하면 가능하다.

```js
let num = 5;
if (num % 2 === 0) {
	console.log('짝수입니다.');
} else {
	console.log('홀수입니다.');  // '홀수입니다.'
}
```

else문은 독립적으로 사용할 수 없고, if문 바로 뒤에 작성해야 한다. 여기서 조건을 추가하고 싶르면 **else if문**을 사용한다.

```js
let name = 'kimcoding';
let course = 'seb fe'

if(name === 'kimcoding' && course === 'seb fe') {
	console.log('정보가 일치합니다.')
} else if (name === 'kimcoding' && course !== 'seb fe') {
	console.log('코스를 확인하세요.')  // '코스를 확인하세요.'
} else {
	console.log('일치하지 않는 정보입니다.')
}
```

if문과 else문은 두 번 이상 사용할 수 없지만 else if문은 여러 번 사용이 가능하다.

```js
let age = 15;
if (age < 8) {
  console.log('미취학아동입니다.');
} else if (age >= 8 && age < 14) {
  console.log('초등학생입니다.');
} else if (age >= 14 && age < 17) {
  console.log('중학생입니다.'); // '중학생입니다.'
} else if (age >= 17 && age < 20) {
  console.log('고등학생입니다.');
} else {
  console.log('성인입니다.');
}
```

<br>

## 3. 삼항 조건 연산자

if문과 else문을 삼항 조건 연산자로 바꿔쓸 수 있다.

```js
let num = 5;
num % 2 === 0 ? console.log('짝수') : console.log('홀수');  // '홀수입니다.'
```

**삼항 조건 연산자**는 조건식을 먼저 작성한 후 `?` 를 입력하고, `?` 뒤로 참/거짓일 때 실행할 코드를 각각 입력한다. 참/거짓일 때는 실행할 코드를 `:` 로 구분한다. 위 코드는 아래 코드와 동일하게 동작한다.

```js
let num = 5;
if (num % 2 === 0) {
	console.log('짝수입니다.');
} else {
	console.log('홀수입니다.'); // '홀수입니다.'
}
```

위의 예시처럼 조건에 따라 실행할 코드가 간단하다며느 삼항 조건 연산자를 활용하는 것이 편리할 뿐만 아니라 가독성도 좋다. 그러나 조건에 따라 실행해야 할 내용이 복잡하다면, if문과 else문을 사용하는 것이 좋다.

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)