---
layout: post
title: "[S2-Unit10] Web Server - CORS"
date: 2023-06-20 21:21:00 +900
lastmod: 2023-06-20 21:21:00 +900
categories: [CODESTATES, Section02]
tags: [CODESTATES, 코드스테이츠, Section02]
use_math: true
---

CORS에 무엇인지 알아보기 전, CORS가 필요하게 된 배경인 **SOP**에 대해서 먼저 알아본다.

# SOP란?

> `SOP (Same-Origin Policy)` 는 동일 출처 정책을 뜻한다.

한 마디로 '**같은 출처의 리소스만 공유가 가능하다**'라는 정책이다. 여기서 말하는 **출처(Origin)** 는 다음과 같다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/476f7199-475c-4fbe-b90d-cf51f8458203" width="80%" />
</center>

출처는 **프로토콜**, **호스트**, **포트**의 조합으로 구성되어 있다. 이 중 하나라도 다르다면 출처로 보지 않는다. 

> **예시** <br>
> - `https://www.codestates.com` **vs** `http://www.codestates.com`
> => 두 URI는 **프로토콜**이 다르기 때문에 동일 출처가 아니다. (https / http)
>
>
> - `https://urclass.codestates.com` **vs** `https://codestates.com` <br>
> => 두 URI는 **호스트**가 다르기 때문에 동일 출처가 아니다. (urclass.codestates.com / codestates.com)
>
>
> - `http://codestates.com:81` **vs** `http://codestates.com` <br>
> => http 프로토콜의 기본 포트는 80이므로 두 URI는 포트가 달라 동일 출처가 아니다. (:81 / :80)
>
>
> - `https://codestates.com:443` **vs** `https://codestates.com` <br>
> => https 프로토콜의 기본 포트는 443이므로 두 URI는 프로토콜, 호스트, 포트가 모두 같은 **동일 출처**다.

<br>

## SOP 등장 배경
동일 출처 정책은 잠재적으로 해로울 수 있는 문서를 분리함으로써 공격받을 수 있는 경로를 줄여준다. SOP을 통해 해킹 등의 위협에서 보다 더 안전해질 수 있다.


만약 동일 출처 정책이 없는 네이버와 같은 웹 페이지에 로그인해서 서비스를 이용하고 있다고 가정한다. 서비스 이용 중이 아니더라도 로그아웃을 깜빡했거나 자동 로그인 기능으로 인해 브라우저에 로그인 정보가 남아있을 수 있다.

**그 상태에서 우리의 로그인 정보를 노리고 있는 코드가 있는 다른 사이트에 방문하게 된다면?**

- 해커는 우리의 로그인 정보를 이용해서 네이버에서 사용할 수 있는 모든 기능을 이용할 수 있게 된다. 
- 나도 모르는 사이에 내 계정으로 블로그나 카페에 좋지 않은 글을 올리게 될 수도, 수 천 명에게 스팸 메일을 보낼 수도 있다.

> `SOP` 는 애초에 다른 사이트와의 리소스 공유를 제한하기 때문에 로그인 정보가 타 사이트의 코드에 의해서 새어나가는 것을 방지할 수 있다. <br>
> 이러한 `SOP` 는 **모든 브라우저에서 기본적으로 사용하고 있는 정책**이다. 

그렇지만 다른 출처의 리소스를 사용하게 될 상황은 많다. 

- 당장 로컬 환경에서 개발을 할 때에도 클라이언트와 서버를 따로 개발하게 된다면 둘의 출처가 달라지게 된다.
- 개발 중인 웹 사이트에서 네이버 지도 API를 사용하고 싶거나 github 정보를 받아와서 사용하고 싶다면 모두 다른 출처의 리소스를 사용해야 한다. 

하지만 모든 브라우저는 기본적으로 SOP 정책을 사용하고 있다. 이때 다른 출처의 리소스를 받아올 수 있게 하는 것이 **CORS**다.

<br>

## CORS란?

`CORS (Cross-Origin Resource Sharing)` 는 교차 출처 리소스 공유를 뜻한다.

> **교차 출처 리소스 공유**(Cross-Origin Resource Sharing, CORS) <br>
> 추가 HTTP 헤더를 사용하여, 한 출처에서 실행 중인 웹 애플리케이션이 **다른 출처의 선택한 자원에 접근할 수 있는 권한을 부여**하도록 브라우저에 알려주는 체제다.

즉, 브라우저는 SOP에 의해 기본적으로 다른 출처의 리소스 공유를 막지만, CORS를 사용하면 접근 권한을 얻을 수 있게 되는 것이다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/72a322bc-4753-4cd5-a544-89b8700e9c21" width="80%" />
</center>

위 에러를 해석하면 다음과 같다.

> 다른 출처의 리소스를 가져오려고 했지만 **SOP** 때문에 접근이 불가능하다.
**CORS 설정을 통해 서버의 응답 헤더에 ‘Access-Control-Allow-Origin’을 작성하면 접근 권한을 얻을 수 있다.**

이러한 에러는 CORS 때문이 아닌 SOP 때문에 생긴 에러다. CORS는 이러한 에러를 해결해줄 수 있는 방안이다.

<br>

## CORS 동작 방식
CORS의 동작 방식에는 크게 세 가지가 있다.

### 1. 프리플라이트 요청 (Preflight Request)

실제 요청을 보내기 전, OPTIONS 메서드로 사전 요청을 보내 출처 리소스에 접근 권한이 있는지부터 확인하는 것을 프리플라이트 요청이라고 한다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/a24fe736-7ad2-4ed6-bab0-91f8a430457a" width="80%" />
</center>

위 이미지의 흐름과 같이, 브라우저는 서버에 실제 요청을 보내기 전에 프리플라이트 요청을 보내고, 응답 헤더의 `Access-Control-Allow-Origin` 으로 요청을 보낸 출처가 돌아오면 실제 요청을 보내게 된다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/8fed3f68-27d9-4ace-b5b1-11030706d36c" width="80%" />
</center>

만약에 요청을 보낸 출처가 접근 권한이 없다면 브라우저에서 CORS 에러를 띄우게 되고, 실제 요청은 전달되지 않는다. 

> **프리플라이트 요청은 왜 필요할까?** <br>
> - 실제 요청을 보내기 전에 미리 권한 확인을 할 수 있기 때문에, 실제 요청을 처음부터 통째로 보내는 것보다 리소스 측면에서 효율적이다.
> - CORS에 대비가 되어있지 않은 서버를 보호할 수 있다. CORS 이전에 만들어진 서버들은 SOP 요청만 들어오는 상황을 고려하고 만들어졌다. 따라서 다른 출처에서 들어오는 요청에 대한 대비가 되어있지 않다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/37550d51-7308-4ebb-a512-8621784af5e8" width="80%" />
</center>

이런 서버에 바로 요청을 보내면, 응답을 보내기 전에 우선 요청을 처리하게 된다. 브라우저는 응답을 받은 후에야 CORS 권한이 없다는 것을 인지하지만, 브라우저가 에러를 띄운 후에는 이미 요청이 수행된 상태가 된다.

하지만 CORS에 대비가 되어있지 않은 서버라도 프리플라이트 요청을 먼저 보내게 되면, 프리플라이트 요청에서 CORS 에러를 띄우게된다. 예시와 같이 실행되선 안 되는 Cross-Origin 요청이 실행되는 것을 방지할 수 있는 것이다. 

이런 이유로 프리플라이트 요청이 CORS의 기본 사양으로 들어가게 되었다.

### 2. 단순 요청 (Simple Request)
단순 요청은 특정 조건이 만족되면 프리플라이트 요청을 생략하고 요청을 보내는 것을 말한다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/f01f14d5-ab91-4b60-90c4-c685168c797d" width="80%" />
</center>

조건은 다음과 같다. 하지만 이 조건들은 모두 만족시키긴느 어려우므로 우선은 참고만 한다.

>- `GET`, `HEAD`, `POST` 요청 중 하나여야 한다.
>
> - 자동으로 설정되는 헤더 외에, `Accept`, `Accept-Language`, `Content-Language`, `Content-Type` 헤더의 값만 수동으로 설정할 수 있다.
>
> - `Content-Type` 헤더에는 application/x-www-form-urlencoded, multipart/form-data, text/plain 값만 허용된다.

### 3. 인증정보를 포함한 요청 (Credentialed Request)

요청 헤더에 인증 정보를 담아 보내는 요청이다. 출처가 다를 경우에는 별도의 설정을 하지 않으면 쿠키를 보낼 수 없다. 민감한 정보이기 때문이다. 

이 경우에는 **프론트, 서버 양측 모두 CORS 설정이 필요하다.**

- **프론트** 측에서는 요청 헤더에 `withCredentials : true` 를 넣어줘야 한다.
- **서버** 측에서는 응답 헤더에 `Access-Control-Allow-Credentials : true` 를 넣어줘야 한다.
- 서버 측에서 `Access-Control-Allow-Origin` 을 설정할 때, 모든 출처를 허용한다는 뜻의 와일드카드(`*`)로 설정하면 에러가 발생한다. 인증 정보를 다루는 만큼 출처를 정확하게 설정해주어야 한다.

<br>

## CORS 설정 방법

CORS 설정하는 방법에는 Node.js 서버와 Express 서버가 있다.

### 1. Node.js 서버

Node.js로 간단한 HTTP 서버를 만들 경우, 다음과 같이 응답 헤더를 설정해줄 수 있다.

```jsx
const http = require('http');

const server = http.createServer((request, response) => {
// 모든 도메인
  response.setHeader("Access-Control-Allow-Origin", "*");

// 특정 도메인
  response.setHeader("Access-Control-Allow-Origin", "https://codestates.com");

// 인증 정보를 포함한 요청을 받을 경우
  response.setHeader("Access-Control-Allow-Credentials", "true");
})
```

### 2. Express 서버

Express 프레임워크를 사용해서 서버를 만드는 경우에는, cors 미들웨어를 사용해서 보다 더 간단하게 CORS 설정을 해줄 수 있다.

```jsx
const cors = require("cors");
const app = express();

//모든 도메인
app.use(cors());

//특정 도메인
const options = {
  origin: "https://codestates.com", // 접근 권한을 부여하는 도메인
  credentials: true, // 응답 헤더에 Access-Control-Allow-Credentials 추가
  optionsSuccessStatus: 200, // 응답 상태 200으로 설정
};

app.use(cors(options));

//특정 요청
app.get("/example/:id", cors(), function (req, res, next) {
  res.json({ msg: "example" });
});
```

Express로 구현한 서버가 Node.js HTTP 모듈로 작성한 서버와 다른 점은 다음과 같다.
- 미들웨어를 추가할 수 있다.
- [라우터](https://expressjs.com/ko/guide/routing.html)를 제공한다.

이 외 다양한 개발 환경에서도, 헤더의 값을 설정하는 방법만 알면 CORS 설정을 해줄 수 있다.

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)
