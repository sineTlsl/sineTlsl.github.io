---
layout: post
title: "[S1-Unit09] JavaScript - 스코프(Scope)"
date: 2023-06-05 13:43:00 +900
lastmod: 2023-06-05 13:43:00 +900
categories: [CODESTATES, Section01]
tags: [CODESTATES, 코드스테이츠, Section01, 회고]
use_math: true
---

**스코프의 정의**
>`스코프(Scope)` 는 변수 접근 규칙에 따른 유효 범위를 뜻한다.

## 스코프의 규칙
- 안쪽 스코프에서 바깥쪽 스코프로는 접근할 수 있지만, 반대로는 불가능하다.
- 스코프는 중첩이 가능하다.
  <center>
    <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/23e91c9b-868b-412a-bde3-e8f6471a5fe1" width="80%" />
  </center>
- 가장 바깥의 스코프는 `전역 스코프 (Global scope)` 라고 부른다. 
  - 전역의 반대말은 지역(local)으로 전역이 아닌 다른 스코프는 전부 `지역 스코프(Local scope)` 이다.
- 지역 변수는 전역 변수보다 더 높은 순위를 가진다.
  ```js
  let name = '김코딩';  // 전역 변수

  function showName() {
      let name = '박해커';  // 지역 변수
  }
  ```

<br>

## 스코프의 종류
### 블록 스코프 (block scope)
`블록 스코프` 는 중괄호 기준으로 범위가 구분된다.

```js
// 예제 1
if (true) {
	console.log('I am in the block');
}

// 예제 2
for (let i = 0; i < 10; i++) {
  	// 변수 i는 중괄호 안에서만 사용할 수 있다.
	console.log(i);
}

// 예제 3
{
	console.log('It works');
}
```

### 함수 스코프 (function scope)

function 키워드가 등장하는 함수 선언식 및 함수 표현식은 `함수 스코프` 를 만든다.

```js
function getName (user) {
	return user.name;
}

let getAge = function (user) {
	return user.age;
}
```

### 화살표 함수 유의할 점

```js
let getAge = user => {
	return user.age;
}
```

같은 함수여도, 화살표 함수를 사용하면 `블록 스코프` 로 취급된다.

```js
let getAge = function (user) {
	return user.age;
}
```

function 키워드를 사용하면 `함수 스코프` 이며, 이 부분은 화살표 함수와 일반 함수의 가장 큰 차이점이다.

<br>

## var, let, const 키워드

### var 키워드 vs. let 키워드
- `var` 키워드는 블록 스코프를 무시하고, **함수 스코프**만 따른다. (이전 방식)
  - 모든 블록 스코프를 무시하는 건 아니며, 화살표 함수의 블록 스코프는 무시하지 않는다.
- 블록 단위로 스코프를 구분했을 때, 훨씬 더 예측 가능한 코드를 작성할 수 있으므로 `let` 키워드 사용이 권장된다.
- var를 사용하지 않는다 해도, 함수 스코프는 `let` 으로 선언된 변수의 접근 범위를 제한한다.
- var 키워드는 재선언을 해도 아무런 에러가 나지 않지만, **let 키워드는 재선언을 방지한다.**

### const 키워드
- let 키워드와 동일하게, 블록 스코프를 따른다.
- 값의 변경을 최소화하여 보다 안전한 프로그램을 만들 수 있다. 값을 새롭게 할당할 일이 없다면, `const` 사용이 권장된다.
- 값을 재할당하는 경우, `TypeError` 를 낸다.

### 키워드 비교
| | let | var | const |
| :---: | :---: | :---: | :---: |
| &emsp;유효 범위&emsp; | 블록 스코프 및 함수 스코프 | 블록 스코프 및 함수 스코프 | 함수 스코프 |
| 값 재할당 | 가능 | 불가능 | 가능 |
| 재선언 | 불가능 | 불가능 | 가능 |

<br>

## 변수 선언에서 주의할 점

### window 객체
var로 선언된 전역 변수 및 전역 함수는 window 객체에 속하게 된다.
- 브라우저에는 `window` 라는 객체가 존재한다.
  - 브라우저 창을 대표하는 객체
  - 그러나, 브라우저 창과 관계없이 전역 항목도 담고 있음
    
- var로 선언된 전역 변수와 전역 함수가 window 객체에 속함
  ```js
  var myName = '김코딩';
  console.log(window.myName);  // 김코딩

  function foo() {
    console.log('bar');
  }

  console.log(foo === window.foo);  // true
  ```

### 1. 전역 변수는 최소화해야 한다.
`전역 변수` 는 어디서든 접근 가능한 변수다.
- 편리한 대신, 다른 함수 혹은 로직에 의해 의도되지 않은 변경이 발생할 수 있다.
  => 부수 효과 (side effect) 발생

### 2. let, const를 주로 사용해야 한다.
- var는 블록 스코프를 무시하며, 재선언을 해도 에러가 나지 않는다고 앞에서 말한 것처럼 동일한 이름의 변수를 재선언 하는 것은 버그를 유발한다.
- 전역 변수를 var로 선언하는 경우, window 기능을 덮어씌워서 내장 기능을 사용할 수 없게 만들 수 있다.

### 3. 선언 없는 변수 할당을 금지한다.
선언 키워드(ver, let, const) 없이 변수를 할당하면 안된다. 선언 없이 변수를 할당하면, 해당 변수는 `var` 로 선언한 전역 변수처럼 취급된다.
```js
function showAge() {
    age = 90;
    console.log(age);  // 90
}
showAge();
console.log(age);  // 90
console.log(window.age);  // 90
```

실수를 방지하기 위해 `Strict Mode` 를 사용할 수 있다. `Strict Mode` 는 브라우저가 보다 엄격하게 작동하도록 만들어 준다. "선언 없는 변수 할당"의 경우도 Strict Mode는 에러로 판단한다.

Strict Mode를 적용하려면, js 파일 상단에 `'use strict'` 라고 입력하면 된다.
```js
'use strict';

function showAge() {
    age = 90;  // 여기서 error 발생
    console.log(age);  // 90
}
showAge();
```

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)