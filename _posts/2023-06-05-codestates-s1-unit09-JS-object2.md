---
layout: post
title: "[S1-Unit09] JavaScript - 원시 자료형과 참조 자료형"
date: 2023-06-05 13:32:00 +900
lastmod: 2023-06-05 14:00:00 +900
categories: [CODESTATES, Section01]
tags: [CODESTATES, 코드스테이츠, Section01]
use_math: true
---

## 원시 자료형(Primitive data type)

JavaScript에서는 원시 타입의 데이터는 객체가 아니면서 method를 가지는 6가지의 데이터 타입이 존재한다.
> `string`, `number`, `bigint`, `boolean`, `undefined`, `symbol` , (null)

이 중에서 자주 사용하는 4 (+1) 가지의 원시 자료형은 다음과 같다.
> `string`, `number`, `boolean`, `undefined`, (null)

원시 자료형은 단 하나의 정보(데이터)를 담고 있다.

과거에는 데이터 저장소(메모리)의 용량이 제한되어 변수 하나에 데이터 용량이 제한된 하나의 원시 자료형 밖에 담을 수 없었다. 그래서 이와 같은 자료형을 `원시 자료형` 이라 부른다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/772bfd92-2619-47c2-b427-625d5d277076" width="80%" />
</center>

```js
let x = 2;
let y = x;
y = 3;
```

원시 자료형을 할당하는 경우, 그 값 자체를 변수에 할당한다. 즉, 그 값을 복사하여 변수에다가 저장한다.

```let y = x;```
변수 x를 변수 y에 할당하는 경우, 변수 x의 값은 원시 자료형이기 때문에 x의 값이었던 2를 y에 복사하여 할당된다.

```y = 3;```
y에 3이 할당되어도, x의 값은 변하지 않는다. x의 값을 y로 복사한 다음 할당하였기 때문에 변수 x에 영향을 미치지 않는다.

<br>

## 참조 자료형(Reference data type)

JavaScript에서 원시 자료형이 아닌 모든 것은 참조 자료형이다. 배열(`[]`)과 객체(`{}`), 함수(`function(){}`)가 대표적이다.

참조 자료형의 데이터는 원시 자료형과 달리 특별한 데이터 보관함에 저장된다.

이 데이터가 위치한 곳(메모리 상 주소)을 가리키는 주소가 변수에 저장된다. 즉, 변수에는 특별한 데이터 보관함을 찾아갈 수 있는 주소가 담겨있고, 이 주소를 따라가보면 특별한 데이터 보관함을 찾을 수 있는데 이 특별한 데이터 보관함에서는 자기가 원하는대로 사이즈를 동적으로 조절 가능하다.

이처럼 데이터는 별도로 관리되고, 우리가 직접 다루는 변수는 주소가 저장되기 때문에 `참조 자료형` 이라고 하며, 이런 특별한 데이터 보관함을 `heap` 이라고도 부른다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/f1b777de-9df0-4c3b-be32-addafe51da1c" width="80%" />
</center>

```js
let x = { foo: 3 };
let y = x;
y.foo = 2;
```

참조 자료형이 변수에 할당되는 경우는, **변수에 데이터가 저장되는 곳의 주소가 할당**이 된다.

```let y = x;```
변수 x를 변수 y에 할당하는 경우, 변수 x의 값은 참조 자료형이기 때문에 x의 값(foo: 3}의 주소를 y에 할당한다. 

이 상태는 변수 x와 변수 y에 모두 같은 { foo : 3 } 이라는 객체의 주소를 바라보고 있다.

```let y.foo = 2;```
y.foo = 2, 값이 3이었던 y.foo에 2를 할당했다. 현재는 같은 주소를 바라보고 있는 y.foo가 2로 변경이 되었으니, 같은 곳을 바라보고 있었던 x.foo도 2가 되어야 한다.

## 원시 자료형과 참조 자료형의 특징
- 원시 자료형이 할당될 때에는 변수에 값(value) 자체가 담기고, 참조 자료형이 할당될 때에는 보관함의 주소(reference)가 담긴다.
- 참조 자료형은 기존된 고정된 크기의 보관함이 아니라, 동적의 크기가 변하는 특별한 보관함을 사용할 수 있다.

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)