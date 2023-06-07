---
layout: post
title: "[S2-Unit05] React - SPA"
date: 2023-06-07 14:26:00 +900
lastmod: 2023-06-07 14:32:00 +900
categories: [CODESTATES, Section02]
tags: [CODESTATES, 코드스테이츠, Section02]
use_math: true
image: 
  path: https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/9e0481a2-04fd-4d82-be2b-cc8948e1a3bf
  width: 900
  alt: React
---

SPA가 등장하기 전까지는 웹 사이트에서는 웹 사이트 내의 다른 페이지로 이동하면 매번 HTML 파일로 된 페이지 전체를 불러와야했다. 

웹 사이트가 보다 복잡해지고 애플리케이션의 형태를 가지게 되면서 사용자와 서비스 사이에 더 많은 상호작용이 일어나게 되었지만, 중복되는 요소들을 매번 불러오는 것은 서버와의 불필요한 트래픽을 발생시켰다.

사용자 입장에서는 매번 모든 페이지를 불러옴에 따라 더 느린 반응성을 갖게 되었고, 이는 애플리케이션과 같은 사용자 경험을 제공하기 어렵게 만들었다.

**HTML 문서 전체가 아닌, 업데이트에 필요한 데이터만 서버에서 전달받아 이 데이터를 JavaScript가 동적으로 HTML 요소를 생성해서 화면에 보여주는 개발 방식을 이용한 웹 애플리케이션이 보편화 되었고, 이것이 SPA다.**

<br>

# SPA란?

> `SPA (Single Page Application)` 이란 서버로부터 완전한 페이지를 불러오지 않고 페이지 갱신에 필요한 데이터로만 받아 그 정보를 기준으로 현재의 페이지를 업데이트함으로써 사용자와 소통하는 웹 어플리케이션이나 웹 사이트다.

SPA의 대표적인 서비스로 Youtube와 Facebook, Gmail, Airbnb, Netflix 등 다양하게 있다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/a83bd738-02fa-445b-a26e-fe456d3ad5af" width="80%" />
</center>

## SPA 장단점
### 장점
- 전체 페이지가 아니라 필요한 부분의 데이터만 받아서 화면을 업데이트 하면되기 때문에 사용자와의 상호 작용에 빠르게 반응한다.
- 서버에서는 요청 받은 데이터만 넘겨주면 되기 때문에 서버 과부화 문제가 현저하게 줄어든다.
- 전체 페이지를 렌더링하지 않아 더 나은 유저경험을 제공한다.

### 단점
- JavaScript 파일의 크기가 크다.
- 파일의 크기가 커 기다리는 시간으로 인해 첫 화면 로딩 시간이 길어진다.
- 검색 엔진 최적화(SEO)가 좋지 않다.

<br>

## SPA & Routing
SPA는 하나의 페이지를 가지고 있지만 사실 한 종류의 화면만 사용하지 않는다. 

예를 들어, Twittler와 같은 SPA를 만들 때 메인 트윗 모음 페이지, 알림 페이지, 마이 트윗 페이지 등의 여러 화면이 필요하다. 또한 이 화면에 따라 **주소도 달라진다.**

> `라우팅(Routing)` 은 이렇게 **다른 주소에 따라 다른 뷰를 보여주는 과정으로 "경로에 따라 변경한다."라는 의미**를 가지고 있다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/9cd7e274-156e-40b8-a7b1-23633e92c285" width="80%" />
</center>

React 자체에는 이 라우팅(Routing) 기능이 내장되어 있지 않다. React SPA에서는 이 기능을 위해 `React Router` 라는 라이브러리를 주로 사용한다.

### React Router 주요 컴포넌트
React Router의 주요 컴포넌트는 크게 3가지로 구분할수 있다.

- **라우터** : BrowserRouter
- **경로 매칭** : Routes, Route
- **경로 변경** : Link

### 1. BrowserRouter

`<BrowserRouter>` 컴포넌트는 웹 애플리케이션에서 HTML5의 [History API](https://developer.mozilla.org/ko/docs/Web/API/History_API)를 사용해 페이지를 새로고침하지 않고도 주소를 변경할 수 있게 해준다. 또한 `<BrowserRouter>` 가 상위에 작성되어 있어야 React Router의 컴포넌트들을 사용할 수 있다.

아래와 같이 ReactDOM의 렌더 단계인 `index.js` 에서도 활용할 수도 있다.

```jsx
// index.js (React Version 18 기준)
import React from 'react';
import ReactDOM from 'react-dom';
import { BrowserRouter } from 'react-router-dom';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </React.StrictMode>
);    
```

```jsx
// index.js (React Version 17 기준)
import React from 'react';
import ReactDOM from 'react-dom';
import { BrowserRouter } from 'react-router-dom';

ReactDOM.render(
  <BrowserRouter>
    <App/>
  </BrowserRouter>, document.querySelector('#root')
);
```

### 2. Routes, Route
경로를 매칭해주는 역할을 하는 컴포넌트다.

- `<Routes>` 컴포넌트는 여러 `<Route>` 컴포넌트를 감싸서 그중 경로가 일치하는 단 하나의 라우터만 렌더링을 시켜주는 역할을 한다
- `<Route>` 컴포넌트는 `path` 속성을 지정하여 해당 `path` 에서 어떤 컴포넌트를 보여줄지 지정한다.

### 3. Link
사용자들 원하는 경로로 이동시켜 주는 역할이다.

- 페이지 전환을 통해 페이지를 새로 불러오지 않고 애플리케이션을 그대로 유지하여 HTML5 History API를 이용해 페이지의 주소만 변경 해준다.

- ReactDOM으로 렌더를 시키게되면 `<Link>` 컴포넌트는 `<a>` 요소로 바뀌는 모습을 볼 수 있다.
- `<a>` 요소를 사용하지 않고, `<Link>` 를 사용하는 이유는 `<a>` 요소는 페이지를 전환하는 과정에서 페이지를 불러오기 때문에 다시 처음부터 렌더링을 시킨다. 즉, 새로고침 현상이 발생한다.

하지만 `<Link>` 컴포넌트는 **페이지를 방지하는 기능**이 내장되어 있기 때문에 SPA를 구현할 수 있다.

### React Router 사용 환경 세팅

1. react-router 라이브러리 설치

```shell
npm install react-router-dom@v6.7.0
```

2. react-router 라이브러리 불러오기
```jsx
import { BrowserRouter, Routes, Route, Link } from 'react-router-dom';
```

라이브러리 설치와 불러옴으로 간단하게 사용할 수 있다.

<br>

## React Router 실습

```jsx
import logo from "./logo.svg";
import "./App.css";
import { BrowserRouter, Routes, Route, Link } from "react-router-dom";

const Home = () => {
  return <h1>Home</h1>;
};
const MyPage = () => {
  return <h1>My Page</h1>;
};
const Dashboard = () => {
  return <h1>Dashboard</h1>;
};

function App() {
  return (
    <BrowserRouter>
      <div className="App">
        <nav>
          <ul>
            <li>
              <Link to="/">Home</Link>
            </li>
            <li>
              <Link to="/mypage">My Page</Link>
            </li>
            <li>
              <Link to="/dashboard">Dashboard</Link>
            </li>
          </ul>
        </nav>
        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/mypage" element={<MyPage />} />
          <Route path="/dashboard" element={<Dashboard />} />
        </Routes>
      </div>
    </BrowserRouter>
  );
}

export default App;
```

만약 사용자가 지정된 주소인 '/', '/mypage', '/dashboard' 이외의 주소로 접근하게 되면 의도한 화면이 보이지 않을 수 있다, 이럴 때 사용하는 속성이 `path=*` 이다. 

지정되지 않은 주소롤 접근할 시에는 이 속성이 설정되어 있는 컴포넌트를 보여주게 된다.

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)
