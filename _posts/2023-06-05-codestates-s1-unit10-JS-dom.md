---
layout: post
title: "[S1-Unit10] JS/Browser - DOM 개요"
date: 2023-06-05 14:07:00 +900
lastmod: 2023-06-05 14:07:00 +900
categories: [CODESTATES, Section01]
tags: [CODESTATES, 코드스테이츠, Section01]
use_math: true
---

# DOM이란?
`DOM (Document Object Model)` 의 약자로, HTML 요소를 Object(JavaScript Object)처럼 조작할 수 있는 Model이다.

JavaScirpt를 사용할 수 있으면, DOM으로 HTML을 조작할 수 있다. 여러 뛰어난 웹 개발자들이 모여 HTML을 분석하여 HTML의 아주 작은 부분까지 접근할 수 있는 구조를 만들었는데, 이 구조를 `DOM` 이라고 한다.

DOM을 이용하면 HTML로 구성된 웹 페이지를 동적으로 움직이게 만들 수 있다. 

## HTML에 JavaScript 적용
HTML에 JavaScript를 적용하기 위해선 `<script>` 태그를 이용한다.

js 파일에 동작을 원하는 코드를 작성하고, html 파일에 다음과 같이 작성한다.

```html
<script src="myScript.js"></script> 
```

웹 브라우저가 작성된 코드를 해석하는 과정에서 `<script>` 요소를 만나면, 웹 브라우저는 HTML 해석을 잠시 중단한다. HTML 해석을 멈춘 웹 브라우저는 `<script>` 요소를 먼저 실행한다.

**`<script>` 요소는 등장과 함께 실행된다는 사실을 꼭 기억해야한다.**

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/1bfd2926-89b5-489c-b5fe-af459fea2eaf" width="80%" />
</center>

<br>

### 1. `<head>`에 삽입하는 방법

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
    <!-- script 요소 삽입 위치 -->
    <script src="myScript.js"></script>
  </head>
  <body>
    ...
  </body>
</html>
```

- 문서를 초기화하거나 설정하는 가벼운 스크립트가 실행된다.
- 무거운 스크립트가 실행되는 경우, 브라우저 파싱 및 렌더링에 방해가 되어 웹 페이지 로딩이 오래 걸린다.

### 2. `<body>`에 삽입하는 방법

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
  </head>
  <body>
    <!-- script 요소 삽입 위치 -->
    <script src="myScriptFile.js"></script>
  </body>
</html>
```

- 무거운 스크립트가 삽입되기 적절한 위치다.
- 브라우저의 파싱 및 렌더링이 완료된 상태에서 스크립트가 실행되므로, 콘텐츠 및 브라우저를 변경하는 스크립트의 경우 완벽하게 구현할 수 있다.

### 두 방법의 공통점과 차이점
고전적인 방법은 `<script>` 요소를 본문의 맨 마지막 (`</body>` 태그 앞)에 배치하는 것이다.

그러면 모든 HTML을 읽은 후에 스크립트를 불러오게 된다. 이 방법의 문제는 HTML DOM을 모두 불러오기 전에는 스크립트의 로딩과 분석이 완전히 중단된다는 점이다. 그래서 많은 스크립트를 포함하는 대형 사이트에서 성능이 저하될 수 있다.

<br>

## 스크립트 중단 문제 해결
스크립트 중단 문제를 해결할 수 있는 기능에는 `async` 와 `defer` 가 있다.

### async
`async` 특성을 지정하면 스크립트를 가져오는 동안 페이지 로딩을 중단하지 않는다.

그러나 스크립트 다운로드가 끝나면 바로 실행되어, 실행 도중에는 페이지 렌더링이 중단된다. 스크립트의 실행 순서를 보장할 방법은 없다는 문제점이 있어 `async` 는 다른 스크립트에 의존하지 않는 독립 스크립트에 사용하는 것이 적합하다.

```html
<script async src="js/vendor/jquery.js"></script>
<script async src="js/script2.js"></script>
<script async src="js/script3.js"></script>
```
위 코드만으로는 스크립트가 HTML의 순서대로 불러와질 것이라고 확실하게 예측할 수 없다. `jquery.js` 가 정의되지 않았으면, 이 스크립트에 의존하는 `script2.js` 와 `script3` 에서 오류가 발생한다. 

`async` 는 다수의 백그라운드 스크립트를 최대한 빠르게 불러올 때 사용하는 게 좋다.


### defer
`defer` 특성을 지정한 스크립트는 페이지 내에 배치한 순서대로 불러오게 된다.

페이지 콘텐츠를 모두 불러오기 전까지는 실행하지 않으므로, 페이지 요소를 수정하거나 추가하는 등 DOM 작업을 기대하는 스크립트에 유용하다.

```html
<script defer src="js/vendor/jquery.js"></script>
<script defer src="js/script2.js"></script>
<script defer src="js/script3.js"></script>
```
위 코드에서는 `script2.js` 와 `script3` 보다 `jquery.js` 를 먼저 불러올 것이라고 확신할 수 있다. 세 스크립트 모두 페이지 콘텐츠를 모두 불러오기 전엔 실행하지 않으므로, 페이지 요소를 수정해야 하는 등 DOM 조작이 필요하다면 더 유용하다.

### async와 defer 정리
- `async` 와 `defer` 모두, 브라우저가 페이지의 다른 내용(DOM 등등)을 불러오는 동안 스크립트를 별도 스레드에서 불러오게 만든다. => **스크립트를 가져오는 동안 페이지 로딩이 중단되지 않는다.**

- `async` 특성을 지정한 스크립트는 다운로드가 끝나는 즉시 실행한다. 실행은 현재 페이지 렌더링을 중단하며, 실행 순서는 보장되지 않는다.

- `defer` 특성을 지정한 스크립트는 순서를 유지한 채로 가져오며 모든 콘텐츠를 다 불러온 이후에 실행한다.

- 의존성 없는 스크립트를 불러온 즉시 실행하려면 `async` 를 사용하는 것이 적합하다.

- 다른 스크립트에 의존하거나 DOM 로딩이 필요한 스크립트에는 `defer` 를 사용하고, 원하는 순서에 맞춰서 `<script>` 요소를 배치해야 한다.

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)

[JavaScript가 뭔가요?](https://developer.mozilla.org/ko/docs/Learn/JavaScript/First_steps/What_is_JavaScript)