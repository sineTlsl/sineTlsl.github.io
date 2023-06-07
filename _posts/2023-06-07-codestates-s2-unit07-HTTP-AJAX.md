---
layout: post
title: "[S2-Unit07] HTTP/Network - AJAX"
date: 2023-06-07 15:07:00 +900
lastmod: 2023-06-07 15:07:00 +900
categories: [CODESTATES, Section02]
tags: [CODESTATES, 코드스테이츠, Section02]
use_math: true
---

# AJAX

> `AJAX (Asynchronous JavaScript And XMLHttpRequest)` 는 JavaScript, DOM, Fetch, XMLHttpRequest, HTML 등의 다양한 기술을 사용하는 웹 개발 기법이다.

AJAX의 가장 큰 특징은 웹 페이지에 필요한 부분에 필요한 데이터만 비동기적으로 받아와 화면에 그려낼 수 있는 것이다.

- 웹 페이지의 html에 의해서 유저에게 필요한 페이지가 렌더링된다.
- 그러나 딱 한 부분만큼은 html에 작성된 대로 유저가 사용하는 것이 아니라, 유저의 요구에 따라 반응하여 변화하는 부분이 존재한다.

예를 들어, 구글에서 내가 원하는 키워드를 입력하면 해당 글자에 시작하는 단어들을 서버로부터 받아와 아래에 추천 검색어로 보여주게 된다. 

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/49492af9-63e9-4aa2-914a-69fc252b36da" width="80%" />
</center>

그때 검색창에서는 필요한 데이터만 비동기적으로 받아와 렌더링 되며, 여기에 **AJAX**가 사용된다. 그 외에도 윈티드, 페이스북 메시지나 네이터 포털사이트의 뉴스 탭이 있다.

<br>

## AJAX의 두 가지 핵심 기술
AJAX를 구성하는 핵심 기술은 JavaScript, DOM 그리고 Fetch다.

과거에는 클라이언트에서 요청을 보내면 매번 새로운 페이지로 이동해야 했다. 그러나 `Fetch` 를 사용하면 페이지를 이동하지 않아도 서버로부터 **필요한 데이터**를 받아올 수 있다. 그 이유는 JavaScript에서 DOM을 사용해 조작할 수 있기 때문이다.

- Fetch는 사용자가 현재 페이지에서 작업을 하는 동안 서버와 통신할 수 있도록 한다.
- 브라우저는 Fetch가 서버에 요청을 보내고 응답을 받을 때까지 모든 동작을 멈추는 것이 아니라 계속해서 페이지를 사용할 수 있게 하는 비동기적인 방식을 사용한다.

### XHR과 Fetch
Fetch 이전에는 XHR(XMLHttpRequest)를 사용했다. `XHR` 은 Cross-Site 이슈 등의 불편함이 있었고, 그에 비해 Fetch는 promise 지원 등의 장점을 가지고 있다.

`Fetch` 는 XHR의 단점을 보완한 새로운 Web API이며, XML보다 가볍고 JavaScript와 호환되는 JSON을 사용한다. 따라서 오늘날에는 XHR보다 Fetch를 많이 사용한다.


**XMLHttpRequest 예제**

```jsx
// XMLHttpRequest를 사용
var xhr = new XMLHttpRequest();
xhr.open('get', 'http://52.78.213.9:3000/messages');

xhr.onreadystatechange = function(){
  if(xhr.readyState !== 4) return;
  // readyState 4: 완료

  if(xhr.status === 200) {
    // status 200: 성공
    console.log(xhr.responseText); // 서버로부터 온 응답
  } else {
    console.log('에러: ' + xhr.status); // 요청 도중 에러 발생
  }
}

xhr.send(); // 요청 전송
```

**Fetch 예제**
```jsx
fetch('http://52.78.213.9:3000/messages')
  .then(function(response) {
  	 return response.json();
  })
  .then(function(json) {
	 ...
  });
```
<br>

## AJAX의 장점
### 1. 서버에서 HTML을 완성하여 보내주지 않아도 웹페이지를 만들 수 있다.
이전에는 서버에서 HTML을 완성하여 보내주어야 화면에 렌더링할 수 있었다.

그러나 AJAX를 사용하면 서버에서 완성된 HTML을 보내주지 않아도 필요한 데이터를 비동기적으로 가져와 브라우저에서 화면의 일부만 업데이트하여 렌더링 할 수 있다.

### 2. 표준화된 방법
이전에는 브라우저마다 다른 방식으로 AJAX를 사용했으나, XHR이 표준화되면서부터 브라우저에 상관없이 AJAX를 사용할 수 있게 되었다.

### 3. 유저 중심 애플리케이션 개발
AJAX를 사용하면 필요한 일부분만 렌더링하기 때문에 빠르고 더 많은 상호작용이 가능한 애플리케이션을 만들 수 있다.

### 4. 더 작은 대역폭
`대역폭` : 네트워크 통신 한 번에 보낼 수 있는 데이터의 크기

이전에는 서버로부터 완성된 HTML 파일을 받아와야 했기 때문에 한 번에 보내야 하는 데이터의 크기가 컸다. 그러나 AJAX에서는 필요한 데이터를 텍스트 형태(JSON, XML 등)로 보내면 되기 때문에 비교적 데이터의 크기가 작다.

## AJAX의 단점
### 1. Search Engine Optimization(SEO)에 불리
AJAX 방식의 웹 애플리케이션은 한 번 받은 HTML을 렌더링 한 후, 서버에서 비동기적으로 필요한 데이터를 가져와 그려낸다. 따라서 처음 받는 HTML 파일에는 데이터를 채우기 위한 틀만 작성되어 있는 경우가 많다.

검색 사이트에서는 전 세계 사이트를 돌아다니며 각 사이트의 모든 정보를 긁어와 사용자에게 검색 결과로 보여준다. AJAX 방식의 웹 애플리케이션의 HTML 파일은 뼈대만 있고 데이터는 없기 때문에 사이트의 정보를 긁어가기 어렵다.

### 2. 뒤로가기 버튼 문제
일반적으로 상요자는 뒤로가기 버튼을 누르면 이전 상태로 돌아갈 거라고 생각하지만, AJAX에서는 이전 상태를 기억하지 않기 때문에 사용하자 의도한 대로 동작하지 않는다.

따라서 뒤로가기 등의 기능을 구현하기 위해서는 별도로 History API를 사용해야 한다.

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)
