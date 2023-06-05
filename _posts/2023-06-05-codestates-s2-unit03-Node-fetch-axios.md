---
layout: post
title: "[S2-Unit03] JavaScript - Fetch와 Axios"
date: 2023-06-05 15:28:00 +900
lastmod: 2023-06-05 15:28:00 +900
categories: [CODESTATES, Section02]
tags: [CODESTATES, 코드스테이츠, Section02]
use_math: true
---

비동기 요청의 가장 대표적인 사례는 단연 **네트워크 요청**이다. 

네트워크를 통해 이루어진 요청은 그 형태가 다양하다. 그 중에서 URL로 요청하는 경우가 제일 많고, URL로 요청하는 것을 가능하게 해주는 API가 `Fetch` 와 `Axios` 이다.

본문에 들어가기 전, 자주 사용되는 용어들이 있어 간단히 정리하고 넘어가도록 한다.

> - **GET 요청**은 일반적으로 정보를 요청하기 위해 사용되는 메서드다.
> - **POST 요청**은 서버에게 데이터를 보내기 위해 사용되는 메서드다.
> - **Promise**는 Callback Hell을 방지하면서 비동기로 작동하는 코드를 제어한다.
> - **Async/Await**는 자바스크립트에서는 ES8에서 이 키워드를 제공하였고, Promise Hell을 방지하면서 비동기로 작동하는 코드를 제어한다.

## Fetch
**Fetch**는 자바스크립트를 사용하면 필요할 때 네트워크 요청을 보내고 새로운 정보를 받아오는 일을 수행한다.

- `url` : 접근하고자 하는 URL
- `options` : 선택 매개변수, method나 header 등을 지정할 수 있음

```jsx
let promise = fetch(url, [options])
```

options에 매개변수를 넘기지 않으면 요청은 `GET` 메서드로 진행되어, `url` 로부터 콘텐츠가 다운로드 된다.

### GET 요청
Fetch API를 각각 **GET 메서드**로  `promise` 와 `async/await` 구현한 코드다. 결과는 같다.

```jsx
// Promise ver
// methid의 'GET' 을 넘기지 않아도 'GET' 메서드로 진행된다.
fetch('https://koreanjson.com/users/1', { method: 'GET' })
  .then((response) => response.json())
  .then((json) => console.log(json))
  .catch((error) => console.log(error));

// Async / Await ver
async function request() {
  const response = await fetch('https://koreanjson.com/users/1', {
    method: 'GET',
  });
  const data = await response.json();
  console.log(data);
}

request();
```

크롬 브라우저에서 개발자 도구의 콘솔에 다음과 같이 입력할 경우, 다음 사진과 같이 출력된다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/853224d6-d0fd-4d76-afce-85d3aa776df1" width="80%" />
</center>

### POST 요청
Fetch API를 각각 **POST 메서드**로  `promise` 와 `async/await` 구현한 코드다. 결과는 같다.

```jsx
// Promise ver
fetch('https://koreanjson.com/users', {
  method: 'POST',
  headers: {
    // JSON의 형식으로 데이터를 보내준다고 서버에게 알려주는 역할입니다.
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({ nickName: 'ApeachIcetea', age: 20 }),
})
  .then((response) => response.json())
  .then((json) => console.log(json))
  .catch((error) => console.log(error));

// Async / Await ver
async function request() {
  const response = await fetch('https://koreanjson.com/users', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify({ nickName: 'ApeachIcetea', age: 20 }),
  });
  const data = await response.json();
  console.log(data);
}

request();
```

위 코드에 결과는 다음과 같이 나온다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/e8e1910f-7686-4cbf-a164-ab56d8e78459" width="80%" />
</center>

<br>

## Axios
**Axios**는 fetch API와 비슷한 역할을 하는 라이브러리다. 

**Axios**는 브라우저, Node.js를 위한 Promise API를 활용하는 HTTP 비동기 라이브러리로, fetch API보다 사용이 간편하면서 추가적인 기능들이 포함되어 있다.

### 특징
- 브라우저를 위해 XMLHttpRequests 생성
- node.js를 위해 http 요청 생성
- Promise API를 지원
- 요청 및 응답 인터셉트
- 요청 및 응답 데이터 변환
- 요청 취소
- JSON 데이터 자동 변환
- XSRF를 막기위한 클라이언트 사이드 지원

### 설치
Axios는 써드파티 라이브러리이기 때문에 npm으로 설치 후 사용할 수 있다.

```shell
npm install axios
```

### GET 요청

- `url` : URL 주소 (필수)
- `[,config]` : 요청 시 사용할 수 있는 옵션들

```jsx
axios.get(url,[,config])
```

axios를 각각 **GET 메서드**로  `promise` 와 `async/await` 구현한 코드다. 결과는 같다.

```jsx
// axios를 사용하기 위해서는 설치한 axios를 불러와야 한다.
import axios from 'axios';

axios
  .get('https://koreanjson.com/users/1')
  .then((response) => {
    console.log(response);
    const { data } = response;
    console.log(data);
  })
  .catch((error) => console.log(error));

// Async / Await ver
async function request() {
  const response = await axios.get('https://koreanjson.com/users/1');
  const { data } = response;
  console.log(data);
}

request();
```

### POST 요청

- `url` : URL 주소 (필수)
- `[, data[, config]]` : 요청 시 보낼 데이터를 설정. 옵션의 경우 필수는 아니지만 상황에 따라 설정해주어야 함

```jsx
axios.post("url"[, data[, config]])
```

axios를 각각 **POST 메서드**로  `promise` 와 `async/await` 구현한 코드다. 결과는 같다.

```jsx
// axios를 사용하기 위해서는 설치한 axios를 불러와야 한다.
import axios from 'axios';

// Promise ver
axios
  .post('https://koreanjson.com/users', { nickName: 'ApeachIcetea', age: '20' })
  .then((response) => {
    const { data } = response;
    console.log(data);
  })
  .catch((error) => console.log(error));

// Async / Await ver
async function request() {
  const response = await axios.post('https://koreanjson.com/users', {
    name: 'ApeachIcetea',
    age: '20',
  });
  const { data } = response;
  console.log(data);
}

request();
```

## Fetch와 Axios 차이점

**Fetch**
- 빌트인 API라 별도의 설치가 필요 없다.
- `.json()` 메서드를 사용해야 한다.

**Axios**
- 써드파티 라이브러리로 설치가 필요하다.
- 자동으로 JSON 데이터 형식으로 변환된다.

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)
