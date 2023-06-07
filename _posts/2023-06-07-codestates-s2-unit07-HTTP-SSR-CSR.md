---
layout: post
title: "[S2-Unit07] HTTP/Network - SSR, CSR"
date: 2023-06-07 15:17:00 +900
lastmod: 2023-06-07 15:17:00 +900
categories: [CODESTATES, Section02]
tags: [CODESTATES, 코드스테이츠, Section02]
use_math: true
image: 
  path: https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/0dc3c925-6bbe-4709-a801-0e7b9832e205
  width: 900
  alt: SSR vs. CSR
---

## SSR

> `SSR(Server Side Rendering)` 은 웹 페이지를 브라우저에서 렌더링하는 대신에 서버에서 렌더링한다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/d37aa542-6065-4a43-ba81-0bbdd2378394" width="80%" />
</center>

1. 브라우저가 서버의 URI로 `GET` 요청을 보내면 서버는 정해진 웹 페이지 파일을 브라우저로 전송한다.
2. 그리고 서버의 웹 페이지가 브라우저에 도착하면 완전히 렌더링된다.

서버에서 웹 페이지를 보내기 전에 서버에서 완전히 렌더링했기 때문에 Server Side Rendering 이라고 한다. 

**웹 페이지의 내용에 데이터베이스의 데이터가 필요한 경우**

서버는 데이터베이스의 데이터를 불러온 다음, 웹 페이지를 완전히 렌더링 된 페이지로 변환한 후에 브라우저에 응답으로 보낸다. 

**사용자가 브라우저의 다른 경로로 이동하게 되는 경우**

브라우저가 다른 경로를 이동할 때마다 서버는 같은 작업을 다시 수행한다.

## SSR 예시
### 1. 네이버 블로그
네이버 블로그는 2020년에 SSR 방식을 도입했다. 여러가지 이유가 있겠지만 대표적인 이유는 SSR이 검색엔진 최적화(Search Engine Optimization, SEO)에 유리한 이점이 있기 때문이다. 

- 검색엔진에 최대한 노출되는 게 유리
- 다른 웹 사이트에 비해 사용자와 상호작용이 많지 않다.

### 2. The NewYork Times
뉴욕 타임스 홈페이지도 SSR 방식을 사용하고 있다. 

SSR의 대표적인 단점인 많은 사용자가 클릭할 때마다 전체 웹 사이트를 다시 서버에서 받아오기 때문에 발생하는 **서버 과부하 이슈**가 있음에도 불구하고, CSR에 비해 **초기 로딩 속도가 빠르기 때문에** 구독자 신문기사를 빠르게 읽을 수 있는 장점이 있다.

그 뿐만 아니라 해당 신문사의 기사가 검색엔진에 노출되는 것이 중요하기 때문에 SEO에 유리한 SSR을 이용하고 있다.

<br>

## CSR

> `CSR(Client Side Rendering)` 은 일반적으로 SSR의 반대료 여겨지며, SSR이 서버 측에서 페이지를 렌더링한다면, CSR은 클라이언트에서 페이지를 렌더링한다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/107d7e02-b57e-4b09-8dad-adcf827ab961" width="80%" />
</center>

웹 개발에서 사용하는 대표적인 클라이언트는 **웹 브라우저**다.

1. 브라우저의 요청을 서버로 보내면 서버는 웹 페이지를 렌더링하는 대신, 웹 페이지의 골격이 될 단일 페이지(Single Page)를 클라이언트에게 보낸다. (이때 서버는 웹 페이지와 함께 JavaScript 파일을 보낸다. )

2. 클라이언트가 웹 페이지를 받으면, 웹 페이지와 함께 전달된 JavaScript 파일은 브라우저의 웹 페이지를 완전히 렌더링 된 페이지로 바꾼다.

**웹 페이지에 필요한 내용이 데이터베이스에 저장된 데이터인 경우**

브라우저는 데이터베이스에 저장된 데이터를 가져와서 웹 페이지에 렌더링을 해야 한다. 이를 위해 Fetch와 같은 API가 사용된다.

**브라우저가 다른 경로로 이동하는 경우**

CSR에서는 SSR과 다르게 서버가 웹 페이지를 다시 보내지 않는다. 브라우저는 브라우저가 요청한 경로에 따라 페이지를 다시 렌더링한다. 이때 보이는 웹 페이지의 파일은 맨 처음 서버로부터 전달받은 웹 페이지 파일과 동일한 파일이다.

## CSR 예시
### 아고다

아고다뿐만 아니라 많은 예약 사이트들은 CSR을 사용하고 있다. SSR에서는 서버에서 렌더링을 해야하기 때문에 상호작용(interaction)이 많아질수록 서버에 부담이 많다. 반면, CSR에서는 서버가 클라이언트에 필요하 데이터만 넘겨주기 때문에 부담이 적다. 

그리고 SPA(Single Page Application)를 기반으로 화면의 일부만 받아온 데이터로 변경해 주기 때문에 빠른 렌더링으로 User Experience(사용자 경험)에 유리하다.

최근까지 html이 빈 페이지이기 때문에 검색엔진 최적화(SEO)를 하기에는 SSR에 비해 불리하다는 특징이 있었으나, 구글에서 이러한 부분을 보완하기 위해 삽입된 자바스크립트 코드를 분석, 실행시켜 크롤링을 하고있다.

**그러나 검색엔진 최적화가 꼭 필요한 서비스라면 조금 더 최적화에 유리한 SSR을 사용하는 것을 권장하고 있다.**

<br>

## SSR과 CSR 차이점
SSR과 CSR의 주요 차이점은 **페이지가 렌더링되는 위치**다.

`SSR` 은 서버에서 페이지를 렌더링하고, `CSR` 은 브라우저(클라이언트)에서 페이지를 렌더링한다. CSR은 사용자가 다른 경로를 요청할 때마다 페이지를 새로고침 하지 않고, 동적으로 라우팅을 관리한다.

### SSR 사용
- SEO가 우선순위인 경우, 일반적으로 SSR을 사용한다.
- 웹 페이지의 첫 화면 렌더링이 빠르게 필요한 경우, 단일 파일의 용량이 작은 SSR이 적합하다.
- 웹 페이지가 사용자와 상호작용이 적은 경우, SSR을 활용할 수 있다.

### CSR 사용
- SEO가 우선순위가 아닌 경우, CSR을 이용할 수 있다.
- 사이트에 풍부한 상호 작용이 있는 경우, CSR은 빠른 라우팅으로 강력한 사용자 경험을 제공한다.
- 웹 애플리케이션을 제작하는 경우, CSR을 이용해 더 나은 사용자 경험(빠른 동적 렌더링 등)을 제공할 수 있다.

## SSR과 CSR 코드
### SSR 코드 예시

```jsx
const express = require("express");
const app = express();

const infoArr = [
  "csr과 차이점이 느껴지나요?",
  "ssr이란?",
  "HTML은 어디서 조작될까요?",
  "Server Side Rendering",
  "검색엔진 최적화(Search Engine, Optimization)에 상대적으로 유리하다.",
  "초기로딩 속도가 빠르다.",
  "TTV(Time To View)와 TTI(Time To Interact)의 시간 공백이 있을 수 있다."
];

app.get("/", (req, res) => {
  res.send(
    "<html><body><h1>" +
      infoArr[Math.floor(Math.random() * infoArr.length)] +
      "</h1><h1>SSR</h1>" +
      "<h2>Server Side Rendering이란 무엇인가?</h2>" +
      "</body></html>"
  );
});

app.listen(8080);
```

**실행 결과**

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/1b61ff04-ab8d-4d99-b6e8-f8461fa6a408" width="80%" />
</center>

### CSR 코드 예시

```jsx
const express = require("express");
const app = express();
const port = process.env.PORT || 5000;

const infoArr = [
  "ssr과 차이점이 느껴지나요?",
  "csr이란?",
  "SPA를 기반으로",
  "화면의 일부만 바꿔주는 것",
  "HTML은 어디서 조작될까요?",
  "Client Side Rendering",
  "AJAX를 통해서 서버로부터 필요한 데이터만 받습니다."
];
app.get(`/`, (req, res) =>
  res.send(infoArr[Math.floor(Math.random() * infoArr.length)])
);
app.get(`/csr`, (req, res) =>
  res.send(infoArr[Math.floor(Math.random() * infoArr.length)])
);

app.listen(port, () =>
  console.log(`Example app listening at http://localhost:${port}`)
);
```

**실행 결과**

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/a92720e3-8d6c-4f1f-8a67-c79274775291" width="80%" />
</center>

## 정리
- SEO가 가장 우선 순위인 경우, SSR을 사용할 수 있다.
- CSR에서 서버는 주로 API 응답을 담당한다.
- 동적 상호작용이 많은 웹 애플리케이션에는 CSR이 더 적합하다.
- 경로가 변경될 때마다 새로운 정적파일을 요청하는 것은 SSR의 특징이다.


<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)
