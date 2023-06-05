---
layout: post
title: "[S1-Unit08] JavaScript - 배열(Array)과 객체(Object)"
date: 2023-06-05 13:25:00 +900
lastmod: 2023-06-05 14:00:00 +900
categories: [CODESTATES, Section01]
tags: [CODESTATES, 코드스테이츠, Section01]
use_math: true
image: 
  path: https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/827b6ec5-bd98-4db9-b505-f28a7487bd22
  alt: 배열(Array)과 객체(Object)
---

# 자바스크립트 배열(Array)

하나의 값을 저장하는 변수는 대량의 데이터를 처리하기엔 불편하다. 그래서 배열(Array) 자료형을 사용하여 하나의 변수에 여러 개의 값을 분리하여 저장할 있어 가독성이 높아지는 장점을 지니고 있다.

```js
let arr = ['apple', 'banana'];
console.log(arr[1]);  // banana
console.log(arr);  // ['apple', 'banana']
```

<br>

## 배열의 특징
- 자바스크립트는, 명시적인 배열 자료형이 없고, 자바스크립트 객체의 일종으로 취급된다. 즉, 특화시킨 **객체형 배열**로 취급된다.
  - typeof로 타입을 확인했을 때, 결과가 객체의 타입과 동일하게 `object` 로 나타난다.
  <center>
    <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/28545431-9653-49b5-bf76-ee368f75e0f6" width="80%" />
  </center>
- 다양한 데이터 타입의 배열 요소다.
-  동적으로 크기 조절도 가능하다. (가변 객체, Mutable)
  - 배열은 크기(length) 프로퍼티가 존재하지만, 객체는 length 프로퍼티가 존재하지 않는다.
-  요소가 순서대로 저장한다.
  - 배열은 순서로써 접근 가능하지만, 객체는 순서없이 키로만 접근된다.


## 배열 생성
1. **[]** 배열 리터럴 이용하는 방법

```let arr = [1, 2, 3, 4, 5];```

2. **new Array** 생성자 함수를 이용하는 방법

```let arr = new Array(1, 2, 3, 4, 5); ```
  - new Array(5); 이면, 길이 5인만큼 빈 배열을 생성

3. ES6부터 도입된 방법
`Array.of()` : 전달된 이수를 요소로 갖는 배열을 생성
`Array.from()` : 유사배열객체 또는 이터러블객체를 인수로 전달받아 배열로 변환시켜 배열 생성

배열 접근은 1이 아닌 0부터 시작하므로`0` 번째 요소 `arr[0]` 로 각 요소에 접근한다.

## 자바스크립트 배열 객체
- 자바스크립트는 배열에 특화된 다양한 메소드와 프로퍼티가 존재한다.
- Array 객체의 메소드들은 [MDN JavaScript](https://developer.mozilla.org/ko/) 에서 확인할 수 있다.
- Array 객체의 프로퍼티는 `length` 가 있으며, 베열 요소의 개수를 의미한다. 

<br>

## 자바스크립트 객체(Object)
> 자바스크립트는 객체 기반 프로그래밍 언어다. 자바스크립트를 구성하는 것의 대부분은 개체라고 볼 수 있다.
{: .prompt-info}

원시형 값을 제외한 나머지 값(함수, 배열, 정규 표현식 등) 모두 객체다.

```js
const obj = {
	name: 'apple',
  	color: 'red',
  	age: 20
};
```

### 객체의 속성(property)와 메소드(method)

`property` : 객체의 상태를 나타내는 값(data)
`method` : property

```js
const obj = {
	name: function(name, color) {
    	return `저의 이름은 ${name}이고, 색상은 ${color} 입니다.`;
    }
}
```
- 자바스크립트의 함수도 객체의 프로퍼티 값으로 사용할 수 있다.
- 객체의 프로퍼티 값이 함수인 경우를 **method**라고 부른다.

### 객체 for문 사용법

- 배열과 객체, 반복문 응용하여 대량의 정보를 다룰 수 있다.
- 객체에서 사용하는 반복은 **for in** 이 있다.
  - ```for (let key in obj)```
- 배열에서는 **for of** 를 사용한다.
  - ```for (let el of arr)```

### 객체의 메소드
- `Object.keys(obj)` : 객체의 속성의 이름(key)을 배열로 반환한다.
- `Object.values(obj)` : 객체의 속성의 값(values)을 배열로 반환한다.

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)

[자바스크립트 Array](http://www.ktword.co.kr/test/view/view.php?m_temp1=2573)

[자바스크립트 Obejct](https://hanamon.kr/javascript-%EA%B0%9D%EC%B2%B4-%EA%B8%B0%EC%B4%88/)