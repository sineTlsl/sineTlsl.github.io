---
layout: post
title: "[S2-Unit06] React - Props, State"
date: 2023-06-07 14:26:00 +900
lastmod: 2023-06-07 14:26:00 +900
categories: [CODESTATES, Section02]
tags: [CODESTATES, 코드스테이츠, Section02]
use_math: true
image: 
  path: https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/9e0481a2-04fd-4d82-be2b-cc8948e1a3bf
  width: 900
  alt: React
---

# State, Props
`State` 와 `Props` 는 **'데이터가 변하는가? 변하지 않는가?'**로 쉽게 구분할 수 있다. 

예를 들어, 일반적인 사람의 데이터가 있다고 가정하자
- 이름
- 나이
- 성별
- 거주지
- 결혼 여부

여기서 이름과 성별을 변하지 않는 데이터다. 나머지의 정보들은 당장 내일이라도 바뀔 수 있다. 이렇게 변하지 않는 데이터는 `Props` , 변하는 데이터는 `State` 로 구분할 수 있다.

## Props란?
- 컴포넌트의 속성(property)을 의미한다.
- 부모 컴포넌트(상위 컴포넌트)로부터 전달받은 값이다.
- 객체 형태다.
- 외부로부터 전달받아 변하지 않는 읽기 전용(read-only) 객체다.

읽기 전용 객체가 아니라면 props를 전달받은 하위 컴포넌트 내에서 props를 직접 수정 시 props를 전달한 상위 컴포넌트의 값에 영향을 미칠 수 있게 된다. 

즉, 개발자가 위도하지 않은 부작용(side effect)이 발생하게 되고 이는 React의 단방향, 하향식 데이터 흐름 원칙에 위배된다.

<br>

## Props를 사용하는 방법

1. 하위 컴포넌트에 전달하고자 하는 값(data)과 속성을 정의한다.
2. props를 이용하여 정의된 값과 속성을 전달한다.
3. 전달받은 props를 렌더링한다.

props를 사용하기 전, 우선 `<Parent>` 와 `<Child>` 라는 컴포넌트를 선언하고,`<Parent>` 컴포 넌트 안에 `<Child>` 컴포넌트를 작성한다.

```jsx
function Parent() {
  return (
    <div className='parent'>
      <h1>I'm the parent</h1>
      <Child />
    </div>
  );
};

function Child() {
	return (
  		<div className='child'></div>  
    );
};
```

### 1. 하위 컴포넌트에 전달하고자 하는 값(data)과 속성을 정의한다.

`<a>` 요소의 href 속성에 `"www.codestates.com"` 라는 값을 정의한다.

```jsx
<a href='www.codestates.com'>Click me to visit Code States</a>
```

React에서 속성 및 값을 할당하는 방법도 이와 유사하다. 다만 전달하고자 하는 값을 `중괄호({})` 를 이용하여 감싸준다.

```jsx
<Child attribute={value} />
```

위 방법을 이용하여 `text` 라는 속성을 선언하고, 이 속성에 `"I'm the eldest child"` 라는 문자열을 `<Child>` 컴포넌트에서 받아 온다. 

```jsx
<Child text={"I'm the eldest child"} />
```

### 2. props를 이용하여 정의된 값과 속성을 전달한다.

함수에 인자를 전달하듯이 React 컴포넌트에 props를 전달하면 되고, 이 props가 필요한 모든 데이터를 가지고 오게 된다.

```jsx
function Child(props) {
  return (
    <div className='child'></div>
  );
};
```

### 3. 전달받은 props를 렌더링한다.

props를 렌더링하려면 JSX 안에 직접 불러서 사용하면 된다. props는 객체이므로 이 객체의 `{ key : value }` 는 `<Parent>` 컴포넌트에서 정의한 `{ attribute : value }` 의 형태를 띄게 된다.

**[props를 전달하는 방법 1]**

객체의 value에 접근할 때 dot notation을 사용하는 것과 동일하게 props의 value 또한 dot notation으로 접근할 수 있다. 

아래와 같이 `props.text` 를 JSX에 중괄호와 함께 작성하면 잘 작동한다.

```jsx
function Parent() {
  return (
    <div className="parent">
      <h1>I'm the parent</h1>
      <Child text={"I'm the eldest child"} />
      <Child />
    </div>
  );
};

function Child(props) {
  return (
    <div className="child">
      <p>{props.text}</p>
    </div>
  );
}
```

**[props를 전달하는 방법 2]**

`<Parent>` 컴포넌트에서 여는 태그와 닫는 태그 사이에 value를 넣어 전달하는 방법이 있다. 이 경우 `props.children` 을 이용하면 해당 value에 접근하여 사용할 수 있다. 

```jsx
function Parent() {
  return (
    <div className='parent'>
      <h1>I'm the parent</h1>
      <Child>I'm the eldest Child</Child>
    </div>
  );
};

function Child(props) {
  return (
    <div className='child'>
      <p>{props.children}</p>
    </div>
  );
};
```

<br>

## State란?

`State` 는 컴포넌트 내부에서 변할 수 있는 값이다.

예를 들어, 쇼핑몰의 장바구니를 들 수 있다. 장바구니에서는 체크박스로 현재 구매할 것과 구매하지 않을 것으로 사용자가 자유롭게 클릭할 수 있다. 체크 여부에 따라 가격 변동이 되고, 사용자 화면 또한 금액이 변경 된다.

이처럼 **컴포넌트 내에서 변할 수 있는 값, 즉 상태는 React state로 다뤄야 한다.**

## useState

> React에서는 state를 다루는 방법 중 하나로 `useState` 라는 특별한 함수를 제공한다.

### 1. useState 불러오기

제일 먼저 다른 라이브러리 사용 방법과 동일하게 useState를 이용하기 위해서는 import를 해주어야 한다.

```jsx
import { useState } from 'react';
```

### 2. useState 호출하기

이후 `useState` 를 컴포넌트 안에서 호출해준다.

- useState를 호출하다는 것은 "state" 라는 변수를 선언하는 것과 같아 아무 이름으로 지어도 된다. 
- 일반적인 변수는 함수가 끝날 때 사라지지만, state의 변수는 React에 의해 함수가 끝나도 사라지지 않는다.
- useState를 호출하면 **배열**을 반환한다.

배열의 0번째 요소는 **현재 state 변수**이고, 1번째 요소는 **이 변수를 갱신할 수 있는 함**수다. `useState` 의 인자로 넘겨주는 값은 **state의 초깃값**이다.

```jsx
const [state 저장 변수, state 갱신 함수] = useState(상태 초기 값);
```

```jsx
function CheckboxExample() {
  const [isChecked, setIsChecked] = useState(false);
}
```

- `isChecked` : state를 저장하는 변수
- `setIsChecked` : state `isChecked` 를 변경하는 함수
- `useState` : state hook
- `false` : state 초깃값

이 state 변수에 저장된 값을 사용하려면 JSX element 안에 직접 불러서 사용하면 된다. 여기서는 `isChecked` 가 boolean 값을 가지기 때문에 `true` or `false` 여부에 따라 다른 결과가 보이도록 삼항연산자를 사용한다.

```jsx
<span>{isChecked ? "Checked!!" : "Unchecked"}</span>
```

### 3. state 갱신하기

위 예제에서 state를 갱신하려면 state 변수를 갱신할 수 있는 함수인 `setIsChecked` 를 호출한다.

사용자가 체크박스 값을 변경하면 `onChange` 이벤트가 이벤트 핸들러 함수인 `handleChecked` 를 호출하고,  이 함수가 `setIsChecked` 를 호출한다. `setIsChecked` 가 호출되면 호출된 결과에 따라 `isChecked` 변수가 갱신되며, React는 새로운 `isChecked` 변수를 `CheckboxExample` 컴포넌트에 담겨 해당 컴포넌트를 다시 렌더링 한다.

```jsx
function CheckboxExample() {
  const [isChecked, setIsChecked] = useState(false);
  
  const handleChecked = (event) => {
  	setIsChecked(event.target.checked);
  };
  
  return (
  	<div className='App'>
      <input type='checkbox' checked={isChecked} onChange={handleChecked} />
      <span>{isChecked ? "Checked!!" : "Unchecked"}</span>
    </div>
  );
};
```

### state Hook 사용 시 주의점
- React 컴포넌트는 state가 변경되면 새롭게 호출되고, 리덴더링 된다.
- React state는 상태 변경 함수 호출로 변경해야 한다.
  - 강제로 변경을 시도하면, 리렌더링이 되지 않거나 state가 제대로 변경되지 않는다.

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)
