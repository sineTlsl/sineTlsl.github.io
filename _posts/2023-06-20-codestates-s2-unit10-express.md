---
layout: post
title: "[S2-Unit10] NodeJS - Express"
date: 2023-06-20 21:25:00 +900
lastmod: 2023-06-20 21:25:00 +900
categories: [CODESTATES, Section02]
tags: [CODESTATES, 코드스테이츠, Section02]
use_math: true
---

**MERN 스택이란?**

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/33369c18-bfec-4dbb-bbe8-c6627ec29cc8" width="80%" />
</center>

`MERN Stack` 은 JavaScript 생태계에서 인기 있는 프레임워크인 **MongoDB**, **Express**, **React**, **NodeJS** 을 사용하여 서버(백엔드), 웹(프론트)를 모두 만드는 기술을 의미한다.

# Express란?

> `Express` 는 Node.js를 위한 빠르고 개방적인 간결한 웹 프레임워크다.

- **웹 애플리케이션**: Express는 웹 및 모바일 애플리케이션을 위한 일련의 강력한 기능을 제공하는 간결하고 유연한 Node.js 웹 애플리케이션 프레임워크다.

- **API**:자유롭게 활용할 수 있는 수많은 HTTP 유틸리티 메소드 및 미들웨어를 통해 쉽고 빠르게 강력한 API를 작성할 수 있다.

- **성능**: Express는 기본적인 웹 애플리케이션 기능으로 구성된 얇은 계층을 제공하여, 여러분이 알고 있고 선호하는 Node.js 기능을 모호하게 만들지 않는다.

<br>

## Express 간단한 웹 서버 만들기

### 1. Express 설치 

**작업을 할 디렉터리를 생성해준다.**

Node.js가 이미 설치되어 있다고 가정한 상태에서, 애플리케이션을 보관할 디렉토리를 작성하고 그 디렉토리를 작업 디렉토리로 설정한다.

```shell
mkdir express_practice
```

**애플리케이션에 대한 package.json 파일을 작성한다.**

`npm init` 명령을 이용하여 package.json 파일을 작성한다. package.json의 작동 원리에 대한 자세한 정보는 [Specifics of npm’s package.json handling](https://docs.npmjs.com/cli/v9/configuring-npm/package-json) 에서 참조할 수 있다.

```shell
npm init
```

**npm으로 express를 설치한다.**

```shell
npm install express
```

<br>

### 2. 웹 서버 만들기

위에서 생성한 디렉터리에 들어가서 `app.js` 라는 이름의 파일을 생성한 후, app.js에 다음의 코드를 추가한다.

```jsx
const express = require("express");
const app = express();
const port = 3000;

app.get("/", (req, res) => {
  res.send("Hello World!");
});

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`);
});
```

이 앱은 서버를 시작하며 3000번 port에 연결이 되어있다. 앱은 루트 URL(/) 또는 **route**에 대한 요청에 “Hello World!”로 응답한다. 모든 경로에 대해서는 **404 Not Found**로 응답한다.

**브라우저에서 확인**

다음의 명령어를 이용하여 앱을 실행한다. 명령어를 입력한 후, 브라우저에서 [http://localhost:3000/](http://localhost:3000/) 로 확인할 수 있다.

```shell
node app.js
```

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/ff8e60c2-4a9a-45a8-9758-ccfc742f1333" width="80%" />
</center>

## 라우팅: 메서드와 url에 따라 분기(Routing)하기

> `라우팅(Routing)` 은 URI(또는 경로) 및 특정한 HTTP 요청 메소드(GET, POST 등)인 특정 Endpoint에 대한 클라이언트 요청에 애플리케이션이 응답하는 방법을 결정하는 것을 말한다.

각 라우트는 하나 이상의 handler 함수를 가질 수 있으며, 이러한 함수는 라우트가 일치할 때 실행된다.

라우트 정의에는 다음과 같은 구조가 필요하다.

```jsx
app.METHOD(PATH, HANDLER)
```

- app은 express의 인스턴트다.
- METHOD는 HTTP 요청 메소드다.
- PATH는 서버에서의 경로다.
- HANDLER는 라우트가 일치할 때 실행되는 함수다.

메서드와 url(`/lower`, `/upper` 등)로 분기점을 만드는 것도 **라우팅(Routing)**이다. 이 부분을 NodeJS와 Express 코드로 구현하면 다음과 같다.

### NodeJS 코드

추가적인 라이브러리를 사용하지 않고, 순수한 Node.js로 코드를 다음과 같이 작성할 수 있다.

```jsx
// Node.js로 라우팅을 구현한 코드
const requestHandler = (req, res) => {
  if(req.url === '/lower') {
    if (req.method === 'GET') {
      res.end(data)
    } else if (req.method === 'POST') {
      req.on('data', (req, res) => {
        // do something ...
      })
    }
  }
}
```

### Express 코드
반면에 Express는 프레임워크 자체에서 라우터 기능을 제공한다. Express의 라우터를 활용하면 아래와 같이 직관적인 코드를 작성할 수 있다.

```jsx
// Express로 라우팅을 구현한 코드
const router = express.Router()

router.get('/lower', (req, res) => {
  res.send(data);
})

router.post('/lower', (req, res) => {
  // do something
})
```

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)

[Express 공식 문서](https://expressjs.com/ko/)

[[Express 공식 문서] 시작하기 - 설치](https://expressjs.com/ko/starter/installing.html)

[[Express 공식 문서] 시작하기 - Hello word 예제](https://expressjs.com/ko/starter/hello-world.html)

[[Express 공식 문서] 시작하기 - 기본 라우팅](https://expressjs.com/ko/starter/basic-routing.html)