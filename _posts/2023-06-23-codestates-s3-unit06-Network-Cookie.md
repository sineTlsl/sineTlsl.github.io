---
layout: post
title: "[S3-Unit06] Network - Cookie"
date: 2023-06-23 18:03:00 +900
lastmod: 2023-06-23 18:03:00 +900
categories: [CODESTATES, Section03]
tags: [CODESTATES, 코드스테이츠, Section03]
use_math: true
---

# Cookie란?

> `Cookie` 는 서버에서 클라이언트에 영속성있는 데이터를 저장하는 방법이다. 즉, 서버가 웹 브라우저에 정보를 저장하고 불러올 수 있는 수단이다.

### 특징
- 쿠키를 삭제하면 사라지지 않는다.
- 서버는 클라이언트의 쿠키를 이용하여 데이터를 가져올 수 있다.
- 쿠키를 이용하는 것은 단순히 서버에서 클라이언트에 쿠키를 전송하는 것만 의미하지 않고 클라이언트에서 서버로 쿠키를 다시 전송하는 것도 포함된다.
- 해당 도메인에 대해 쿠키가 존재하면, 웹 브라우저는 도메인에게 http 요청 시 쿠키를 함께 전달한다.

> **쿠키를 이용한 상태 유지**
> - 서버는 클라이언트에 인증정보를 담은 쿠키를 전송하고, 클라이언트는 전달받은 쿠키를 서버에 요청과 함께 전송하여 Stateless한 인터넷 연결을 Stateful하게 유지할 수 있다.
>
> - 하지만 기본적으로 쿠키는 오랜 시간 동안 유지될 수 있고, HttpOnly 옵션을 사용하지 않았다면 자바스크립트를 이용해서 쿠키에 접근할 수 있기 때문에 쿠키에 민감한 정보를 담는 것은 위험하다.


### 사용 예
- 장기간 저장해야하는 옵션을 클라이언트에 저장할 때
- 로그인/로그아웃을 위한 인증 정보를 저장할 때
  - 웹 사이트 로그인 시, "아이디와 비밀번호를 저장하시겠습니까?"

<br>

## Cookie Options
> **서버가 클라이언트에 특정한 데이터를 저장할 수 있다.** <br>
> 서버는 쿠키를 이용하여 데이터를 저장하고 그 데이터를 불러와서 사용할 수 있지만, 데이터를 저장한 이후 아무 때나 데이터를 가져올 수는 없다.
>
> 데이터를 저장한 이후 특정 조건이 만족되어야 다시 가져올 수 있기 때문이다.

이러한 조건들은 아래 http 헤더를 사용해 **쿠키 옵션**으로 표현할 수 있다.

```jsx
'Set-Cookie':[
  'cookie=yummy', 
  'Secure=Secure; Secure',
  'HttpOnly=HttpOnly; HttpOnly',
  'Path=Path; Path=/cookie',
  'Doamin=Domain; Domain=codestates.com'
]
```

서버에서 이러한 옵션들을 지정한 다음 서버에서 클라이언트로 쿠키를 처음 전송하게 된다면 헤더에 `Set-Cookie` 라는 프로퍼티로 쿠키를 담아 전송한다. 

이후 클라이언트에서 서버에게 쿠키를 전송해야 한다면 클라이언트는 헤더에 `Cookie` 라는 프로퍼티에 쿠키를 담아 서버에 쿠키를 전송하게 된다.

### Domain

> `Domain` 은 서버의 요청의 세부 경로가 일치하는 경우에만 쿠키를 전송한다.

- Domain은 `www.google.com` 과 같은 서버에 접속할 수 있는 이름이다.
- 쿠키 옵션에서 도메인은 포트 및 서브 도메인 정보, 세부 경로를 포함하지 않으며, 여기서 **서브 도메인**은 `www` 같은 도메인 앞에 추가로 작성되는 부분을 말한다.
- URL이 `http://www.localhost.com:3000/users/login` 이라 하면, 여기에서 Domain은 `localhost.com` 이다.

쿠키 옵션에서 Domain을 지정하면 `naver.com` 에서 받은 쿠키를 `google.com` 에 전송하는 일을 막을 수 있다.
 
### Path

> `Path` 는 서버의 요청의 세부경로가 일치하는 경우에만 쿠키를 전송한다.

- Path는 세부 경로로써 서버가 라우팅할 때 사용하는 경로를 의미한다.
- 요청해야 하는 URL이 `http://www.localhost.com:3000/users/login` 인 경우에 여기서 Path는 `/users/login` 이 된다. 이를 명시하지 않을 경우 기본적으로 `/` 로 설정된다.
- Path 옵션의 특징은 설정된 경로를 포함하는 하위 경로로 요청을 하더라도 쿠키를 서버에 전송할 수 있다.

Path가 `/users` 로 설정되어 있고, 요청하는 세부 경로가 `/users/~~~` 인 경우라면 쿠키 전송이 가능하다. 하지만 `/post/~~~` 로 전송되는 요청은 Path 옵션을 만족하기 못했기 때문에 서버로 쿠키를 전송할 수 없다.


### MaxAge or Expires
> `MaxAge or Expires` 는 쿠키의 유효기간을 설정한다. 쿠키가 영원히 남아있을 땐, 보안 측면에서 문제가 생길 수 있어 유효기간을 설정하는 것이 중요하다.

- <span style="color: #E65E5E">`MaxAge` </span>: 쿠키가 유효한 시간을 초 단위로 설정하는 옵션이다. (=시한부 옵션)
- <span style="color: #E65E5E">`Expires` </span> : MaxAge와 비슷하지만 언제까지 쿠키가 유효한지 심판의 날을 지정할 수 있다. 이때 옵션의 값은 클라이언트의 시간을 기준으로 하며, 이후 지정된 시간과 날짜를 초과하게 되면 쿠키는 자동으로 파괴된다.

쿠키는 위 옵션의 여부에 따라 `세션 쿠키(Session Cookie)` 와 `영속성 쿠키(Persistent Cookie)` 로 나눠진다.

### Secure

> `Secure` 는 HTTPS 프로토콜에서만 쿠키 전송 여부를 결정한다. 해당 옵션이 `true` 로 설정되어 있고, HTTPS를 이용하는 경우에만 쿠키를 전송할 수 있다.

- `Secure` 옵션이 없을 경우에는 프로토콜에 상관 없이 `http://www.sieun.com` 또는 `https://www.sieun.com` 에 모두 쿠키를 전송할 수 있다.
- 단, `도메인이 localhost` 인 경우에는 HTTPS가 아니여도 쿠키 전송이 가능하다. 

### HttpOnly

> `HttpOnly` 는 스크립트의 쿠키 접근 가능 여부를 결정한다. 해당 옵션이 `true` 로 설정된 경우, 자바스크립트로 쿠키에 접근이 불가능하다.

- 옵션을 명시하지 않는 경우에는 기본적으로 `false` 로 지정된다.
- 옵션이 `false` 인 경우 `document.cookie` 를 이용하여 자바스크립트에 쿠키로 접근할 수 있으므로 쿠키가 탈취될 위험이 있다.

### SameSite

> `SameSite` 는 Cross-Origin 요청을 받은 경우, 요청에서 사용한 메소드(e.g. `GET`, `POST`, `PUT`, `PATCH` …)와 해당 옵션의 조합을 기준으로 서버의 쿠키 전송 여부를 결정하게 된다.

- `Lax` : Cross-Origin 요청이라면 GET 메소드에 대해서만 쿠키를 전송할 수 있다.
- `Stric` : 단어 그대로 가장 엄격한 옵션으로, Cross-Origin이 아닌 same-site 인 경우에만 쿠키를 전송 할 수 있다.
- `None` : Cross-Origin에 대해 가장 관대한 옵션으로 항상 쿠키를 보내줄 수 있지만, 쿠키 옵션 중 Secure 옵션이 필요하다.

`same-site` 는 요청을 보낸 Origin과 서버의 도메인, 프로토콜, 포트가 같은 경우를 말하며, 이 중 하나라도 다르다면 Cross-Origin으로 구분된다.


<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)
