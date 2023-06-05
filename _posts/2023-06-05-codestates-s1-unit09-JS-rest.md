---
layout: post
title: "[S1-Unit09] JavaScript - Spread/Rest 문법 (구조 분해 할당)"
date: 2023-06-05 13:48:00 +900
lastmod: 2023-06-05 14:00:00 +900
categories: [CODESTATES, Section01]
tags: [CODESTATES, 코드스테이츠, Section01]
use_math: true
---

Spread와 Rest는 ES6에서 도입되었으며 서로 완전히 다른 문법이지만 비슷한 부분이 있다.

## Spread 문법
주로 배열을 풀어서 `인자` 로 전달하거나, 배열을 풀어서 `각각의 요소` 로 넣을 때에 사용한다.

```jsx
function sum(x, y, z) {
	return x + y + z;
} 

const numbers = [1, 2, 3];
sum(...numbers);  // 6
```

## Rest 문법
파라미터를 `배열의 형태` 로 받아서 사용할 수 있다. 파라미터 개수가 가변적일 때 유용하다.

```jsx
// 예제 1
function sum(...theArgs) {
	return theArgs.reduce((previous, current) => {
    	return previous + current;
    })
}

sum(1, 2, 3);  // 6
sum(1, 2, 3, 4);  // 10
```

## 배열에서 사용하기
spread 문법은 배열에서 사용하기 적합하다.

### 1. 배열 합치기

```jsx
let parts = ['shoulders', 'knees'];
let lyrics = ['head', ...parts, 'and', 'toes'];  

// lyrics = ['head', 'shoulders', 'knees', 'and', 'toes']
```
```jsx
let arr1 = [0, 1, 2];
let arr2 = [3, 4, 5];
arr1 = [...arr1, ...arr2];  

// arr1 = [0, 1, 2, 3, 4, 5]
```

### 2. 배열 복사
```jsx
let arr = [1, 2, 3];
let arr2 = [...arr]; // arr.slice() 와 유사
arr2.push(4);

// arr = [1, 2, 3];
// arr2 = [1, 2, 3, 4];
```

spread 문법은 기존 배열을 변경하지 않으므로 arr2를 수정한다고, arr이 바뀌지 않는다.

## 객체에서 사용하기

```jsx
let obj1 = { foo: 'bar', x: 42 };
let obj2 = { foo: 'baz', y: 13 };

let clonedObj = { ...obj1 };  // clonedObj = { foo: 'bar', x: 42 }
let mergedObj = { ...obj1, ...obj2 };  // mergedObj = { foo: 'baz', x: 42, y: 13 }
```
객체의 기존에 있던 `key` 와 이름이 동일하면, 데이터를 덮어씌운다.

## 함수에서 나머지 파라미터 받아오기

```jsx
function myFun(a, b, ...manyMoreArgs) {
  console.log("a", a);  // a one
  console.log("b", b);  // b two
  console.log("manyMoreArgs", manyMoreArgs);  // manyMoreArgs ["three", "four", "five", "six"]
}

myFun("one", "two", "three", "four", "five", "six");
```

<br>

## 구조 분해 할당
`구조 분해 할당` 은 spread 문법을 이용하여 값을 해체한 후, 개별 값을 변수에 새로 할당하는 과정을 말한다.

### 분해 후 새 변수에 할당
**배열**

```jsx
const [a, b, ...rest] = [10, 20, 30, 40, 50];

// a = 10
// b = 20
// rest = [30, 40, 50]
```
**객체**

```jsx
const {a, b, ...rest} = {a: 10, b: 20, c: 30, d: 40};

// a = 10
// b = 20
// rest = {c: 30, d: 40} 
```

객체에서 구조 분해 할당을 사용하는 경우, 선언(`const`, `let`, `var`)과 함께 사용하지 않으면 에러가 발생할 수 있다.

### 유용한 예제) 함수에서 객체 분해

```jsx
function whois({displayName: displayName, fullName: {firstName: name}}){
  console.log(displayName + " is " + name);
}

let user = {
  id: 42,
  displayName: "jdoe",
  fullName: {
      firstName: "John",
      lastName: "Doe"
  }
};

whois(user);  // jdoe is John
```

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)