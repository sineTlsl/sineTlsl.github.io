---
layout: post
title: "[S2-Unit10] My Agora States Server 회고"
date: 2023-06-23 16:10:00 +900
lastmod: 2023-06-23 16:10:00 +900
categories: [CODESTATES, Section02]
tags: [CODESTATES, 코드스테이츠, Section02, 회고]
use_math: true
image: 
  path: https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/651f3db3-3eb7-42df-b737-49210265a0fb
  width: 1200
  alt: My Agora States Server 회고
---

# 과제 Rule
이번 해커톤에서는 Section2에서 학습한 내용을 얼마나 적용 및 응용할 수 있는지 자기 자신의 개발 역량을 스스로 확인한다. 

다음과 같이 과제가 주어졌고, 내가 직접 구현한 것만 체크하였다.

## Bare Minimum Requirement
my-agora-states-server는 기본적인 테스트가 준비되어 있다. 

> **my-agora-states-server** <br>
> - ☑️ `my-agora-states-server/app.js` 
>   - ☑️ 모든 Origin, 경로에 대해 CORS 요청을 허용하게 미들웨어를 적용합니다.
>   - ☑️ POST 요청 등에 포함된 body(payload)를 구조화하기 위한 미들웨어를 적용합니다. 
>   - ☑️ 서버 상태 확인을 위해 `/` 에서 상태 코드 200으로 응답합니다. 
>   - ☑️ `discussionsRouter` 를 이용하여 `/discussions` 경로로 라우팅합니다. 
> - ☑️ `my-agora-states-server/router/discussions.js` 
>   - ☑️ `GET /discussions` 
>   - ☑️ `GET /discussions/:id` 
> - ☑️ `my-agora-states-server/controller/index.js`
>   - ☑️ `discussionsController.findAll`
>   - ☑️ `discussionsController.findById`
>
> **my-agora-states-server 과제 제출 (Pull request)** <br>
> - ☑️ Pull request로 과제 제출
>
> **my-agora-states-server 시작** <br>
> - ☑️ `package.json` 을 참고하여 나만의 아고라 스테이츠 서버를 로컬 환경에서 실행합니다.
>
> **my-agora-states와 연동하기** <br>
> - ☑️ my-agora-states-server가 켜져있는지 확인합니다.
> - ☑️ 로컬 환경에서 실행한 나만의 아고라 스테이츠 서버에서 discussions 데이터를 조회합니다.


## Optional Checklist
react로 리팩토링 작업하는 와중에 css에서 머릿속 과부하가 발생했다 .. 

> 1. **my-agora-states-in-react** <br>
>   - ☑️ create-react-app으로 프로젝트 생성 <br>
    - [ ] 기존에 만든 나만의 아고라 스테이츠를 React로 옮기기 <br>
      - [ ] 디스커션 나열 기능 <br>
    - [ ] 로컬 환경에서 실행한 나만의 아고라 스테이츠 서버에서 discussions 데이터를 조회합니다.

<br>

## 👩🏻‍💻 CODE
다음은 **my-agora-states-server** 과제에서 수행하였던 코드를 중심적으로 소개한다.

### app.js
테스트를 진행하기 전, 경로를 라우팅하고 미들웨어를 적용하는 작업을 진행하는 부분이다. 주석으로 내가 어디 부분을 작성해야하는 지 알려주어서 어려움은 없었다.

```jsx
const express = require("express");
const app = express();

const cors = require("cors");
const morgan = require("morgan");

// morgan 미들웨어가 세팅되어 있습니다.
// HTTP 요청 logger를 편리하게 사용할 수 있는 미들웨어 입니다.
app.use(morgan("tiny"));

// TODO: cors를 적용합니다.
app.use(cors());

// TODO: Express 내장 미들웨어인 express.json()을 적용합니다.
app.use(express.json());

const port = 4000;
const discussionsRouter = require("./router/discussions");

// TODO: app.use()를 활용하여 /discussions 경로로 라우팅합니다.
app.use("/discussions", discussionsRouter);

app.get("/", (req, res) => {
  // 서버 상태 확인을 위해 상태 코드 200과 함께 응답을 보냅니다.
  res.status(200).send("fe-sprint-my-agora-states-server");
});

const server = app.listen(port, () => {
  console.log(`[RUN] My Agora States Server... | http://localhost:${port}`);
});

module.exports.app = app;
module.exports.server = server;
```

### router/discussions.js

모든 디스커션 목록을 조회하는 라우터와 디스커션 하나를 조회는 라우터를 작성해주는 부분이다.

```jsx
// TODO: discussions 라우터를 완성합니다.
const { discussionsController } = require("../controller");
const { findAll, findById } = discussionsController;
const express = require("express");
const router = express.Router();

// TODO: 모든 discussions 목록을 조회하는 라우터를 작성합니다.
router.get("/", findAll);

// TODO: :id에 맞는 discussion을 조회하는 라우터를 작성합니다.
router.get("/:id", findById);

module.exports = router;
```

### controller/index.js

- `findAll` : 모든 디스커션 목록 조회
- `findById` : 하나의 디스커션 조회

```jsx
const { agoraStatesDiscussions } = require("../repository/discussions");
const discussionsData = agoraStatesDiscussions;

const discussionsController = {
  findAll: (req, res) => {
    // TODO: 모든 discussions 목록을 응답합니다.
    res.status(200).json(discussionsData);
  },

  findById: (req, res) => {
    // TODO: 요청으로 들어온 id와 일치하는 discussion을 응답합니다.
    const { id } = req.params;

    let filterdData = discussionsData.filter((discussion) => {
      return Number(id) === discussion.id;
    });

    let result = Object.assign({}, filterdData[0]);

    if (result.id) {
      res.status(200).json(result);
    } else {
      res.status(404).json("NOT FOUND!");
    }
  },
};

module.exports = {
  discussionsController,
};
```

다음과 같이 서버 쪽 작업이 끝났다면 터미널에서 `npm start` 를 입력한 후, 섹션 1때 작업했던 나만의 아코라 스테이츠(클라이언트)를 수정해야 한다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/7f6ba2a5-4be6-42d2-91a9-86ad59a4cfc5" width="80%" />
</center>

### My Agora States - script.js 
기존에 작성한 스크립트 밑에 부분에 있던 `render(ul)` 를 삭제하고, 비동기에서 실행시켜주었다. 다음에 코드만 추가하면 된다.

```jsx
fetch(`http://localhost:4000/discussions`)
  .then((res) => res.json())
  .then((json) => {
    json.map((data) => {
      agoraStatesDiscussions = json;

      const ul = document.querySelector("ul.discussions__container");
      render(ul);
    });
  });
```

`fetch` 에서 사용한 주소를 Postman을 통해 실행한다면 다음과 같이 정보를 확인할 수 있다. 

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/593ea0a5-18bd-4dce-a061-fdd537ad3050" width="80%" />
</center>

<br>

## Feelings ...

비동기로 불러오는 과정에서 함수를 사용하여 불러오는 방법을 생각하지 않고 많은 고민을 하다보니 어려움이 있었고, 작성한 코드가 가독성이 좀 떨어지는 것 같아서 아쉬움이 남았다. 그러다 보니 React로 리팩토링하기엔 시간이 부족했고 React에 대해 개념이 부족한 난 React에서 CSS 수정하는 부분에서 막혀버렸다 ..😢 

> _앞으로는 React 공부만 더 할거다... 진심...!!_

## Findings ...
이번 과제를 통해 부족했었던 개념을 확실하게 짚고 넘어갈 수 있었다.

1. `express.json` 와 `express.json({ strict: false })`
> **express.json({ strict: true })**
> 기본(default). 베열과 객체의 데이터(참조자료형)만 받을 수 있다.
>
> **express.json({ strict: false })**
> 참조자료형 외에 데이터를 받을 수 있다.

2. `module.exports = {}` 이 문법은 다른 파일에서 사용하기 위해 모듈의 형태로 내보내는 것을 의미한다.

3. **morgan 모듈**
>
> - morgan은 요청과 응답에 대한 정보를 콘솔에 기록한다.
> - morgan에 연결 후 포트에 접속하면 기존 로그 외에 추가적인 로그를 볼 수 있다. 

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)