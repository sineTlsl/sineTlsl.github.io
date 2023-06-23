---
layout: post
title: "[S3-Unit03] React - styled-components"
date: 2023-06-23 17:12:00 +900
lastmod: 2023-06-23 17:12:00 +900
categories: [CODESTATES, Section03]
tags: [CODESTATES, 코드스테이츠, Section03]
use_math: true
---

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/610cda28-a6b2-4304-b42d-4c8dba5c3c52" width="50%" />
</center>

styled-components를 공부하기 전에, CDD의 개념을 알고 넘어가는 것이 좋다. 

> **CDD (Component Driven Development)** <br>
`CDD` 는 부품 단위로 UI 컴포넌트를 만들어 나가는 개발을 진행하는 것을 말한다.

즉, CDD는 재사용 할 수 있는 UI 컴포넌트를 미리 디자인하고 개발하는 것을 의미한다. 이 CDD를 할 수 있는 방법 중 대표적인 React 라이브러리 **styled-components**가 있다.

<br>

## styled-components란?

> `styled-components` 는 CSS in JS 라는 개념이 대두되면서 나온 라이브러리다.

기본적으로 CSS를 코드를 다룰 때, class 이름을 고민하거나 CSS 파일에서 내가 원하는 부분을 찾는 경우가 힘든 경우가 한 번쯤 있었을 것이다.

이러한 문제점인 CSS를 컴포넌트화 시킴으로써 해결해주고, 현재 CSS in JS 라이브러리 중에서 가장 인기 있는 라이브러리다.

## styled-components 설치하기

### 1. library install

설치하는 방법은 간단하다. 내가 이 라이브러리를 사용할 곳에서 다음과 같은 명령어를 입력하기만 하면 된다.

```shell
# npm install
npm install styled-components

# yarn install
yarn add styled-components
```

### 2. package setting

공식 홈페이지에서는 package.json에 다음 코드를 추가하도록 권장하고 있다. 이렇게 설정할 경우, 여러 버전의 스타일 구성 요소가 설치되어 여러 버전이 설치되어 발생하는 문제점을 줄여준다.

```jsx
{
  "resolutions": {
    "styled-components": "^5"
  }
}
```

### 3. library import

마지막으로는 styled-components를 사용할 파일에 불러오기만 하면 된다.

```jsx
import styled from "styled-components"
```

vscode에서 다음과 같은 `vscode-styled-components` 플러그인을 제공한다. 가독성과.. 수많은 이유로 현재까지도 유용하게 잘 사용하고 있다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/9c835e84-dd42-4400-8c46-ea687f4013da" width="90%" />
</center>

<br>

## styled-components 문법

### 1. 컴포넌트 생성하기

ES6의 [Templete Literals](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Template_literals) 문법을 사용하므로 백틱(`)을 꼭 붙여야한다.

```jsx
const 컴포넌트이름 = styled.태그종류`
	css속성 1: 속성값;
	css속성 2: 속성값;
`;

// 예시
const InputButton = styled.div`
	background-color: gray;
	display: flex;
`;
```

### 2. 컴포넌트 재활용해서 새로운 컴포넌트 생성하기

이미 만들어진 컴포넌트를 재활용해서 다음과 같이 컴포넌트를 생성할 수 있다. 컴포넌트를 선언하고 `styled()` 에 재활용할 컴포넌트를 전달해준 다음, 추가하고 싶은 스타일 속성을 작성하면 된다.

```jsx
const 컴포넌트이름 = styled.(재활용할 컴포넌트)`
	추가할 css속성 1: 속성값;
	추가할 css속성 2: 속성값;
`;

// 예시
const InputColorButton = styled.(InputButton)`
	color: #fff;
`;
```

### 3. props 활용하기

styled-component로 만든 컴포넌트도 React 컴포넌트처럼 props를 내려줄 수 있다. 내려준 props 값에 따라서 컴포넌트를 렌더링하는 것도 가능하다.

```jsx
const 컴포넌트이름 = styled.태그종류`
	css속성: ${(props) => 함수 코드}
`;
```

**[예제 1]**

다음은 삼항연산자를 활용하여 `<Button1>` 컴포넌트에 `skyblue` 라는 props가 있는지 확인하고, 있으면 배경색으로 `skyblue` 를, 없을 경우 `white` 를 지정해주는 코드다.

```jsx
const Button1 = styled.button`
	background: ${(props) => (props.skyblue ? "skyblue" : "white")};
`;

export default function App () {
  return (
    <>
      <GlobalStyle />
      <Button1>Button1</Button1>
      <Button1 skyblue>Button1</Button1>
    </>
  );
}
```

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/04706c35-92b6-4a53-ba75-c2d2a63b1a09" width="90%" />
</center>

**[예제 2]**

다음 예제도 삼항연산자를 사용하고 있지만 `<Button1>` 과 `<Button2>` 컴포넌트에 `props.color` 가 없다면 `white` 를 `props.color` 가 있다면 그대로 값을 가져와서 스타일 속성 값으로 리턴해주는 코드다.

```jsx
const Button1 = styled.button`
  background: ${(props) => (props.color ? props.color : "white")};
`;
// 위와 같은 방식.
const Button2 = styled.button`
  background: ${(props) => props.color || "white"};
`;

export default function App() {
  return (
    <>
      <GlobalStyle />
      <Button1>Button1</Button1>
      <Button1 color="orange">Button1</Button1>
      <Button1 color="tomato">Button1</Button1>
      <br />
      <Button2>Button2</Button2>
      <Button2 color="pink">Button2</Button2>
      <Button2 color="turquoise">Button2</Button2>
    </>
  );
}
```

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/c5428055-f263-4ce7-b139-550559601504" width="90%" />
</center>

### 4. 전역 스타일 설정하기

스타일을 컴포넌트로 생성할 수 있지만, 전역에 스타일을 저장하여 사용할 수도 있다.

전역 스타일을 설정하기 위해선 `createGlobalStyle` 함수를 불러와야 한다.

```jsx
import { createGlobalStyle } from "styled-components";
```

그 다음 이 함수를 사용하여 CSS 파일에서 작성하듯 설정해주고 싶은 스타일을 작성한다.

```jsx
const GlobalStyle = createGlobalStyle`
	button {
		padding : 5px;
    margin : 2px;
    border-radius : 5px;
	}
`;
```

이렇게 만들어진 `<GlobalStyle>` 컴포넌트를 최상위 컴포넌트에서 사용해주면 전역에 `<GlobalStyle>` 컴포넌트의 스타일이 적용된다.

```jsx
function App() {
	return (
		<>
			<GlobalStyle />
			<Button>전역 스타일 적용하기</Button>
		</>
	);
}
```

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)

[styled-components 공식 홈페이지](https://styled-components.com/)