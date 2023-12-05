---
layout: post
title: "[S2-Unit04] React - React Intro"
date: 2023-06-05 15:42:00 +900
lastmod: 2023-12-05 18:19:00 +900
categories: [CODESTATES, Section02]
tags: [CODESTATES, 코드스테이츠, Section02]
use_math: true
image:
  path: https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/9e0481a2-04fd-4d82-be2b-cc8948e1a3bf
  width: 900
  alt: React
---

## React란?

리액트(React)는 프론트엔드 개발을 위한 JavaScript 오픈소스 라이브러리다.

## React 특징

### 1. 선언형 (Declarative)

React는 한 페이지를 보여주기 위해 HTML, CSS, JS로 나눠서 적기 보다는 하나의 파일에 명시적으로 작성할 수 있게 `JSX` 를 활용한 선언형 프로그래밍을 지향한다.

### 2. 컴포넌트 기반 (Component-Based)

React는 하나의 기능 구현을 위해 여러 종류의 코드를 묶어둔 컴포넌트를 기반으로 개발한다. 컴포넌트로 분리하면 서로 독립적이고 재사용 가능하기 때문에, 기능 자체에 집중하여 개발할 수 있다.

### 3. 범용성 (Learn Once, Write Anywhere)

React는 JavaScript 프로젝트에서 어디에든 유연하게 적용될 수 있다. Facebook에서 관리되어 안정적이고, 가장 유명하며, React Native로 모바일 개발도 가능하다.

## Component (컴포넌트)

> `Component` 는 하나의 기능 구현을 위한 여러 종유의 코드 묶음이며, UI를 구성하는 필수 요소다.

- 컴포넌트를 여러 개 만들고 조합하여 애플리케이션을 만들 수 있다.
- React Application은 컴포넌트들의 관계를 **리 구조** 형상화하여 표현할 수 있다.
- 컴포넌트 기반 개발 웹 애플리케이션에서 각 기능 별로 하나의 컴포넌트를 작성하도록 권장한다.
- 그래서 컴포넌트 간 의존성이 낮아지고 독립적을 작동한다.

<br>

## JSX

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/14bf61dd-b7fd-4c36-9787-c7c57ea2ff27" width="80%" />
</center>

> `JSX` 는 JavaScript가 확장된 문법이지만, 브라우저가 바로 실행할 수 있는 JavaScript 코드가 아니다. 그래서 브라우저가 이해할 수 있는 JavaScript 코드로 변환을 해주어야하는데, 이때 컴파일 해주는 것이 `Babel` 이다.

- 동작은 **SX -> Babel(컴파일) -> JS로 변환 -> 브라우저**로 이루어진다.
- React에서는 DOM과 다르게 CSS, JSX 문법만을 가지고 웹 애플리케이션을 개발할 수 있다.
- 컴포넌트 하나를 구현하기 위해서 필요한 파일이 줄어들었고, 한 눈에 컴포넌트를 확인할 수 있다.
- JSX는 HTTML이 아니다.

즉, **SX를 사용하면 JavaScript 만으로 마크업 형태의 코드를 작성하여 DOM에 배치할 수 있다.**
React에서는 JSX를 이용해서 DOM보다 명시적으로 코드를 작성할 수 있고, JavaScript 문법과 HTML 문법을 동시에 이용해 기능과 구조를 한눈에 확인할 수 있다. 이렇게 구조와 동작에 대한 코드를 한 뭉치로 적은 코드셋을 컴포넌트라고 한다.

### JSX가 없을 경우

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/2ff7bcc2-5d8a-41d6-8d8b-41988c35fba1" width="80%" />
</center>

사진을 보면 왼쪽에는 JSX가 없어도 React 요소를 만들 수 있지만 코드가 복잡한 것을 확인할 수 있다. 반면, 오른쪽에는 JSX를 사용함으로 코드를 이해하기 쉬워진다.

**eact 로 엘리먼트 생성하기 예제 (JSX가 없을때와 있을 때 비교)**

```jsx
import React from "react";

function App() {
  const user = {
    firstName: "React",
    lastName: "JSX Activity"
  };

  function formatName(user) {
    return user.firstName + " " + user.lastName;
  }
  // JSX 없이 활용한 React
  return React.createElement("h1", null, `Hello, ${formatName(user)}!`);

  // JSX 를 활용한 React
  return <h1>Hello, {formatName(user)}!</h1>;
}

export default App;
```

위 `App.js` 에서는 한 개의 JavaScript 파일 안에서 HTML과 JavaScript로 나누어졌던 두 가지 일을 한 번에 처리하고 있다.

HTML과 JavaScript를 한번에 작성하여 하나의 파일에서 웹 애플리케이션의 구조와 동작을 한눈에 파악할 수 있다. JSX는 개발자가 코드만 바라보는게 아니라 구조를 바라보게 돕는다.

<br>

### JSX 규칙

**1. 하나의 element 안에 모든 엘리먼트가 포함된다.**

> JSX에서 여러 element를 작성하는 경우, 최상위에서 opening tag와 closing tag로 감싸주어야 한다.

**2. 엘리먼트 클래스 사용 시, className 으로 표기한다.**

> 만약 class로 작성하게 된다면, React에서는 이를 html 클래스 속성 대신 자바스크립트 클래스로 받아들이기 때문에 주의해야 한다.

**3. JavaScript 표현식 사용 시, 괄호({})를 이용한다.**

> 중괄호를 사용하지 않으면 일반 텍스트로 인식한다.

**4. 사용자 정의 컴포넌트는 대문자로 시작한다.**

> 대문자로 작성된 JSX 컴포넌트를 `사용자 정의 컴포넌트` 라고 한다. 만약, 소문자로 시작하게 되면 일반적인 HTML element로 인식을 하게 된다.

**5. 조건부 렌더링은 if문이 아닌 삼항연산자를 이용해야 한다.**

> 만약, else의 값을 주고 싶지 않으면 `null` 값을 준다.

```jsx
1 + 1 === 2 ? <p>정답</p> : null;
```

**6. React에서 여러 개의 HTML element를 표시할 때는 `map()` 함수를 사용한다.**

> map 함수를 사용할 때는 반드시 **key' JSX 속성** 넣어주어야 한다. React에서 `map` 메서드 사용 시, key 속성을 넣지 않으면 아래와 같이 리스트의 각 항목에 key를 넣어야 한다는 경고가 표시된다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/b0e5f150-2173-4512-9381-6ffd637450bd" width="80%" />
</center>

> **key 속성값은 가능하면 데이터에서 제공하는 id를 할당해야 한다.**<br><br> key 속성값은 id와 마찬가지로 변하지 않고, 예상 가능하며, 유일해야 하기 때문이다. 정 고유한 id가 없는 경우에만 배열 인덱스를 넣어서 해결할 수 있다. 배열 인덱스는 최후의 수단(as a last resort)으로만 사용한다.

**map을 이용한 React 반복 예제**

```jsx
const posts = [
  { id: 1, title: "Hello World", content: "Welcome to learning React" },
  { id: 2, title: "Installation", content: "You can install React from npm" }
];

export default function App() {
  // 한 포스트의 정보를 담은 객체 post를 매개변수로 받고
  // obj를 JSX 표현식으로 바꿔 리턴해주는 함수 postToJSX
  const postToJSX = (post) => {
    return (
      <div key={post.id}>
        <h3>{post.title}</h3>
        <p>{post.content}</p>
      </div>
    );
  };

  return (
    <div className="App">
      <h1>Hello JSX</h1>
      {posts.map(postToJSX)}
    </div>
  );
}
```

<br>

## Create React App

> `Create React App` 은 리액트 SPA를 쉽고 빠르게 개발할 수 있도록 만들어진 툴 체인이다.

### React 툴 체인 특징

- 많은 파일과 컴포넌트 스케일링
- 서드 파티 npm 라이브러리 사용
- 일반적인 실수를 조기에 발견
- CSS와 JS를 실시간으로 편집
- 프로덕션 코드 최적화

개발 환경을 설정하고, 최신 JavaScript를 사용하게 해주며, 좋은 개발 경험과 프로적션 앱 최적화를 해준다. 현재는 Node 14.0.0 혹은 상위 버전 npm 5.6 혹은 상위 버전이 필요하다.

### React 프로젝트 생성

새로운 React 프로젝트를 만들기 위해서는 다음과 같이 명령어를 터미널에 입력해야 한다. ( `my-app` 은 임의로 지정한 프로젝트명)

밑에 두 개의 방법 중 하나를 선택하여 프로젝트를 생성할 수 있다.

```shell
// 첫 번째 프로젝트 생성 방법
npx create-react-app my-app
```

`@latest` 를 사용하면 항상 **최신버전**을 설치한다.

```shell
// 두 번째 프로젝트 생성 방법
npx create-react-app@latest my-app
```

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/f9cb25b1-9ffc-46e4-b276-ae9b8cbf33af" width="80%" />
</center>

설치를 진행하고 나면 다음과 같이 터미널에 출력되는데 밑에 명령어로 새로 만들어진 프로젝트로 이동하여 그 프로젝트를 실행시켜준다.

```shell
cd my-app
npm start
```

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/409eddbf-55ee-48ac-aed6-67819ae4dc66" width="80%" />
</center>

React 프로젝트가 정상적으로 생성되고 실행될 경우에는 3000 port가 연결된 브라우저가 자동으로 켜진다.

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)
