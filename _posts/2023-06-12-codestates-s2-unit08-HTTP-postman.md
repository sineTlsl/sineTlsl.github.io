---
layout: post
title: "[S2-Unit08] HTTP/Network - HTTP API 테스트 도구 POSTMAN"
date: 2023-06-12 19:19:00 +900
lastmod: 2023-06-12 19:19:00 +900
categories: [CODESTATES, Section02]
tags: [CODESTATES, 코드스테이츠, Section02]
use_math: true
image: 
  path: https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/e07a08b9-2c25-4492-8f89-03126623b763
  width: 850
  alt: POSTMAN
---

# HTTP API 테스트 도구란?
웹 개발에서 사용하는 대표적인 클라이언트는 브라우저다.

> **root-endpoint**: 서버의 기본 주소 <br>
**path**: 세부 경로

브라우저는 서버에 HTTP 요청을 보낼 수 있는 훌륭한 도구이지만, 주로 웹 페이지를 받아오는 `GET` 요청에 사용한다. 브라우저의 주소창에 URL을 입력하면, 해당 URL의 root-endpoint로 `GET` 요청을 보낸다.

테스트를 위해 `GET` 요청이 아닌 다른 요청을 보내려면, 개발자 도구의 콘솔 창에서 Web API `fetch` 를 사용해야한다.

테스트를 위해 매번 코드를 작성하는 것은 번거로운 작업이다. 그 대신에 HTTP 요청을 테스트할 수 있는 다양한 API 테스트 도구들을 사용하여 클라이언트 입장에서 서버 API를 테스트하거나 API를 만드는 과정에서 유용하게 작업할 수 있다.

**HTTP API 테스트 도구 (CLI)**

- `curl` (리눅스 환경 내장)
- [wuzz](https://github.com/asciimoo/wuzz)

**HTTP API 테스트 도구 (GUI)**

- [Postman](https://www.postman.com/)
- [Insomia](https://insomnia.rest/)

여러 개의 API 테스트 도구 중 가장 편리한 Postman을 사용하여 진행하고자 한다.

<br>

## POSTMAN이란?
> `Postman` 은 API 개발을 보다 빠르고 쉽게 구현 할 수 있도록 도와주며, 개발된 API를 테스트하여 문서화 또는 공유 할 수 있도록 도와 주는 플랫폼이다.

- Postman은 모든 API 개발자를 위해 다양한 기능을 제공한다.
- 변수 및 환경, request 설명, 테스트 및 사전 요청에 필요한 스크립트 작성 등 Postman은 현재 워크 플로우를 더 효율적으로 만들 수 있도록 고안되었다.

## POSTMAN 시작하기

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/7bdfe59a-22ef-4b1d-b8d7-9b009e28830c" width="80%" />
</center>

**1. 가입 및 설치**

Postman에 회원가입을 한 후, 프로그램을 설치한다.

**2. 환경 설정**

Postman을 설치 후 Workspaces에서 My Workspace를 클릭한 후 `+` 를 눌러 테스팅을 시작한다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/06cbab93-695b-4099-95ad-67b50fabec70" width="80%" />
</center>

**3. 테스팅 시작**

Postman을 사용할 준비가 끝나 Postman을 활용하여 HTTP 요청을 한다.

<br>

## POSTMAN 사용하기

먼저, 이미 만들어져 있는 API 서버가 주어지는 경우에 HTTP로 소통하기 위해서는 API 서버의 endpoint URL로 주어져야 한다.

**예시) 다음과 같은 API 문서가 있을 때**

URL: http://3.36.72.17:3000/

### GET 요청하기

1. HTTP 메서드 중 `GET` 메서드를 선택한다.
2. URL 입력 창에서 URL과 Endpoint를 입력한다.
3. HTTP 요청 버튼을 클릭하여 요청을 보낸다.
4. HTTP 요청시 설정할 수 있는 각종 옵션을 추가한다.
  - 추가적인 parameter나 요청 본문(body)을 추가할 수 있다.
  - API 문서에서 확인할 수 있듯이, `roomname` 이라는 파라미터를 사용할 수 있다. 필수는 아니지만, 파라미터를 사용하려면 Params 탭의 `KEY`, `VALUE` 에 각각 `roomname` 과 필요한 값을 입력한다.
5. 요청을 보낸 후 응답을 확인할 수 있다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/5b085f37-b468-4bbd-95dd-50afb57a411a" width="80%" />
</center>

### 메시지 조회

> **Request** <br>
> sineTlsl이 작성한 모든 메시지를 조회한다.

```
GET /sineTlsl/messages
```

> **Response** <br>
> JSON 형식으로 응답을 받는다.

```json
[
  {
  	"username": "미나리",
    "text": "안녕하세요",
    "roomname": "시은"
  },
  // 더 많은 메시지들 ....
]
```

### POST 요청하기
GET 요청은 브라우저로도 충분히 테스트할 수 있다. `POST` 요청은 GET 요청과 다르게 **본문(body)**을 포함하는 경우 많다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/04faa58f-cd55-49f5-a0d4-f0c2fcdbf3dd" width="80%" />
</center>

1. HTTP 메서드 중 `POST` 메서드를 선택한다.
2. URL 입력 창에서 URL과 Endpoint를 입력한다.
3. **본문의 형식 선택**
  - JSON 형식으로 보낼 때는 `raw` 를 선택한다.
  - 보낼 형식에 맞게 정확한 타입을 선택한다.
    - JSON 형식으로 보낼 때에는, `JSON` 을 선택한다.
    - 이 과정은 HTTP 요청 헤더에 다음과 같이 작성하는 것과 동일하다.
      ```
      Content-Type: application/json
      ```
      
4. 본문 내용은 앞서 JSON을 선택했으므로, 유효한 JSON을 적어주어야 한다.
5. 요청을 보낸 후 응답을 확인할 수 있다.

### 메시지 추가
> **Request** <br>
> sineTlsl이 새로운 메시지를 추가한다.
>
```
POST /sineTlsl/messages
```
> **Response** <br>
JSON 형식으로 응답을 받는다.
```json
{
  "id": 3
}
```
id는 숫자 형식이며, 새로 생성된 메시지의 고유한 ID 값이다.

### 응답 살펴보기

> **상황 1. 요청이 끝지 않을 경우** <br>
일반적으로 서버가 요청에 대한 응답을 하지 않는 경우, 요청이 끝나지 않는다. 이것은 서버의 문제다. 만약 직접 서버를 만드는 중이라면, 응답 처리를 했는지 확인해야 한다.
>
> **상황 2. 기대했던 응답이 오지 않는 경우** <br>
결과에 아무것도 나오지 않거나, 기대했던 값이 나오지 않을 때는 HTTP 응답 코드를 확인해야한다.
> <center>
>  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/ab99d111-ba4d-4724-b4fa-254a060c7af6" width="80%" />
> </center>
> 위 그림의 우측 상단에 HTTP 응답 코드가 표시된다. `400 Bad Request` 라고 되어 있다면, 잘못된 요청을 한 경우일 것이다.

<br>

## HTML & JavaScript에서 확인하기

위에서 `POST` 를 사용해서 메시지를 추가한 데이터들을 `fetch` 를 활용하여 확인할 수 있다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/91765e33-11af-4953-9588-8b34df285533" width="80%" />
</center>

**[html]**

```html
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>OpenAPI 예제</title>
    <link rel="stylesheet" href="./style.css" />
  </head>
  <body>
    <div id="container">
      <h2>GET /{githubID}/messages 가져오기</h2>
      <button class="dataBtn" onclick="dataZero()">데이터 출력</button>
    </div>
    <script src="./script.js"></script>
  </body>
```

**[JavaScript]**

```jsx
const container = document.getElementById("container");

let githubID = "sineTlsl";
let url = `http://3.36.72.17:3000/${githubID}/messages`;

const dataZero = () => {
  fetch(url)
    .then((res) => res.json())
    .then((json) => {
      const datas = json;
      datas.map((data) => {
        const name = document.createElement("div");
        const text = document.createElement("div");
        const roomname = document.createElement("div");

        const box = document.createElement("div");
        box.className = "box";

        name.textContent = data.username;
        text.textContent = data.text;
        roomname.textContent = data.roomname;

        box.append(name, text, roomname);
        container.append(box);
        console.log(data);
      });
    });
};

```

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)
