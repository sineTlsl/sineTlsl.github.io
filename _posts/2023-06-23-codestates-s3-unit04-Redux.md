---
layout: post
title: "[S3-Unit04] 상태관리 - Redux"
date: 2023-06-23 17:21:00 +900
lastmod: 2023-06-23 17:21:00 +900
categories: [CODESTATES, Section03]
tags: [CODESTATES, 코드스테이츠, Section03]
use_math: true
image: 
  path: https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/a8558799-b32c-4b7d-85fe-ac51385935e3
  width: 1200
  alt: Redux
---

# Redux란?
> `Redux` 는 JavaScript 상태관리 라이브러리다.

`Redux` 는 일관적으로 동작하고, 서로 다른 환경(서버, 클라이언트, 네이티브) 등에서 작동하고, 테스트하기 쉬운 앱으로 작성할 수 있게 도와준다.

`React` 와 `React Native` 와 같은 다른 뷰 라이브러리와 함께 사용할 수 있고, `Redux`는 매우 작지만(의존 라이브러리 포함 2KB), 사용 가능한 **애드온**(프로그램의 기능을 보완하기 위해 추가하는 보조 프로그램)은 매우 많다.

**Redux를 사용하면 전역으로 상태를 관리해주는 저장소를 제공 받을 수 있어, 언제 어디서든 저장소에 접근하여 상태관리(state management)를 편리하고 효율적으로 다룰 수 있게 해준다.**

### Redux는 이럴 때 사용해야 한다.
`Redux` 는 상태를 관리하기에 유용한 도구이지만 현재 상황에 적합한지 따져 보아야 한다.
단지 누군가가 사용하라고 했다는 이유만으로 `Redux` 를 사용해서는 안된다. 시간을 들여서 잠재적인 이점과 그에 따르는 단점을 이해해야 한다.

> **Redux를 사용하기 적합한 상황**
> 1. 계속해서 변화하는 상당한 양의 데이터가 있을 경우
> 2. 상태를 위한 단 하나의 근원이 필요할 경우
> 3. 앱에 중간 또는 큰 규모의 코드베이스가 있고, 많은 사람들이 작업할 경우

<br>

## Redux의 흐름

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/aad114ea-e8dc-4b1e-925f-0a18ccd5040d" width="90%" />
</center>

Redux는 다음과 같은 순서로 상태를 관리한다.

> 1. 상태가 변경되어야 하는 이벤트가 발생하면, 변경될 상태에 대한 정보가 담긴 **Action 객체**가 생성된다.
> 2. 이 Action 객체는 **Dispatch 함수**의 인자로 전달된다.
> 3. Dispatch 함수는 Action 객체를 **Reducer 함수**로 전달해준다.
> 4. Reducer 함수는 Action 객체의 값을 확인하고, 그 값에 따라 **전역 상태 저장소 Store**의 상태를 변경한다.
> 5. 상태가 변경되면, React는 화면을 다시 렌더링한다.

즉, Redux에서는 **Action -> Dispatch -> Reducer -> Store** 순서로 데이터가 단방향으로 흐르게 된다.

<br>

## Store

>`Store` 는 상태과 관리되는 오직 하나뿐인 저장소의 역할을 하고, Redux 앱의 state가 저장되어 있는 공간이다.

다음과 같이 `createStore` 메서드를 활용해 Reducer를 연결해서 Store를 생성할 수 있다.

```jsx
import { createStore } from 'redux';

const store = createStore(rootReducer);
```

```jsx
import React from 'react';
import { createRoot } from 'react-dom/client';
import App from './App';

/* 1. react-redux에서 Provider를 불러와야 한다. */
// Provider는 store를 손쉽게 사용할 수 있게 하는 컴포넌트다.
// 해당 컴포넌트를 불러온 다음에, Store를 사용할 컴포넌트를 감싸준 후,
// Provider 컴포넌트의 props로 store를 설정해주어야 한다.
import { Provider } from 'react-redux';

/* 2. redux에서 createStore를 불러와야 한다. */
import { legacy_createStore as createStore } from 'redux';

const rootElement = document.getElementById('root');
const root = createRoot(rootElement);

const reducer = () => {};

/* 4. 변수 Store에 createStore 메서드를 통해 store를 전달해주어야 한다. */
const store = createStore(reducer);

root.render(
  /* 3. 전역 상태 저장소 Store를 사용하기 위해서는 App 컴포넌트를 Provider로 감싸준 후, 
  		props로 변수 store를 전달해주여야 한다. */
  <Provider store={store}>
    <App />
  </Provider>
);
```

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/27854c35-0f42-48df-a14c-f0c5f3bba71d" width="90%" />
</center>

<br>

## Reducer

> `Reducer` 는 Dispatch에게서 전달받은 Action 객체의 `type` 값에 따라서 상태를 변경시키는 함수다.

```jsx
import React from 'react';
import { createRoot } from 'react-dom/client';
import App from './App';
import { Provider } from 'react-redux';
import { legacy_createStore as createStore } from 'redux';

const rootElement = document.getElementById('root');
const root = createRoot(rootElement);

const count = 1;

// Reducer를 생성할 때에는 초기 상태를 인자로 요구한다.
const counterReducer = (state = count, action) => {
  // Action 객체의 type 값에 따라 분기하는 switch 조건문
  switch (action.type) {
    //action === 'INCREASE'일 경우
    case 'INCREASE':
      return state + 1;

    // action === 'DECREASE'일 경우
    case 'DECREASE':
      return state - 1;

    // action === 'SET_NUMBER'일 경우
    case 'SET_NUMBER':
      return action.payload;

    // 해당 되는 경우가 없을 땐 기존 상태를 그대로 리턴
    default:
      return state;
  }
};
const store = createStore(counterReducer);

root.render(
  <Provider store={store}>
    <App />
  </Provider>
);
```

**이때,  Reducer는 순수함수여야 한다.** 외부 요인으로 인해 거대한 값이 아닌 엉뚱한 값으로 상태가 변경되는 일이 없어야 한다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/203a0d1e-3a64-47af-a9d9-997a312bedcf" width="90%" />
</center>


위와 한 개의 Reducer가 아닌 여러개를 사용할 경우, Redux의 `combineReducers` 메서드를 사용해서 하나의 Reducer로 합쳐줄 수 있다.

```jsx
import { combineReducers } from 'redux';

const rootReducer = combineReducers({
  counterReducer,
  anyReducer,
  ...
});
```

<br>

## Action
> `Action` 은 말 그대로 어떤 액션을 취할 것인지 정의해 놓은 **객체**로, 다음과 같은 형식으로 구성된다.

```jsx
// payload가 필요 없는 경우
{ type: 'INCREASE' }

// payload가 필요한 경우
{ type: 'SET_NUMBER', payload: 5 }
```

여기서 `type` 은 필수로 지정해주어야 한다. 해당 Action 객체가 어떤 동작을 하는지 명시해주는 역할을 하며, 대문자와 Snake Case로 작성한다. 또한, 필요에 따라 `payload` 를 작성해 구체적인 값을 전달한다.

Action을 직접 작성하기보다는 Action 객체를 생성하는 함수를 사용하는 경우가 많다. 이러한 함수를 **액션 생성자(Action Creator)** 라고 한다.
```jsx
// payload가 필요 없는 경우
const increase = () => {
  return {
    type: 'INCREASE'
  }
}

// payload가 필요한 경우
const setNumber = (num) => {
  return {
    type: 'SET_NUMBER',
    payload: num
  }
}
```

기존에 구현했던 코드에 Action Creator 함수를 추가하고, 다른 파일에서도 사용할 수 있도록 export를 붙여주었다.
```jsx
import React from 'react';
import { createRoot } from 'react-dom/client';
import App from './App';
import { Provider } from 'react-redux';
import { legacy_createStore as createStore } from 'redux';

const rootElement = document.getElementById('root');
const root = createRoot(rootElement);

// Action Creator
export const increase = () => {
  return {
    type: 'INCREASE',
  };
};
export const decrease = () => {
  return {
    type: 'DECREASE',
  };
};

const count = 1;
const counterReducer = (state = count, action) => {
  switch (action.type) {
    case 'INCREASE':
      return state + 1;
    case 'DECREASE':
      return state - 1;
    case 'SET_NUMBER':
      return action.payload;
    default:
      return state;
  }
};
const store = createStore(counterReducer);

root.render(
  <Provider store={store}>
    <App />
  </Provider>
);
```

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/28a5c16f-cf71-48bc-a979-4c4bacd77f99" width="90%" />
</center>

<br>

## Dispatch

> `Dispatch` 는 Reducer로 Action을 전달해주는 함수이며, Dispatch의 전달인자로 Action 객체가 전달된다.

```jsx
// Action 객체를 직접 작성하는 경우
dispatch( { type: 'INCREASE' } );
dispatch( { type: 'SET_NUMBER', payload: 5 } );

// 액션 생성자(Action Creator)를 사용하는 경우
dispatch( increase() );
dispatch( setNumber(5) );
```
Action 객체를 전달받은 Dispatch 함수는 Reducer를 호출한다.

지금까지 Store, Reducer, Action, Dispatch의 개념들로 코드를 구성하였다. 이 구성한 코드에서 Redux를 연결시켜주어야 하는데, 이때 이용하는 것이 **Redux Hooks** 다.

<br>

## Redux Hooks
Redux Hooks는 React-Redux에서 Redux를 사용할 때 활용할 수 있는 Hooks 메서드를 제공한다. 여기서 사용하는 메서드는 `useSelector()`, `useDispatch()` 두 가지가 있다.

### useDispatch()
> `useDispatch()` 는 Action 객체를 Reducer로 전달해 주는 Dispatch 함수를 반환하는 메서드다.

```jsx
import React from 'react';
import './style.css';

// 1. react-redux에서 useDispatch를 불러와야 한다.
import { useDispatch } from 'react-redux';

// 2 . Action Creater 함수 increase, decrease를 불러와야 한다.
import { increase, decrease } from './index.js';

export default function App() {
  // 3. useDispatch의 실행 값를 변수에 저장해서 dispatch 함수를 사용한다.
  const dispatch = useDispatch();
  console.log(dispatch); // 콘솔로 확인

  const plusNum = () => {
    // 4. action 객체를 Reducer 함수로 전달한다.
    dispatch(increase());
  };

  const minusNum = () => {
    // 5. action 객체를 Reducer 함수로 전달한다.
    dispatch(decrease());
  };

  return (
    <div className="container">
      <h1>{`Count: ${1}`}</h1>
      <div>
        <button className="plusBtn" onClick={plusNum}>
          +
        </button>
        <button className="minusBtn" onClick={minusNum}>
          -
        </button>
      </div>
    </div>
  );
}
```

### useSelector()

> `useSelector()` 는 컴포넌트와 state를 연결하여 Redux의 state에 접근할 수 있게 해주는 메서드다.

```jsx
// Redux Hooks 메서드는 'redux'가 아니라 'react-redux'에서 불러온다.
import { useSelector } from 'react-redux'
const counter = useSelector(state => state)

console.log(counter) // 1
```

`useDispatch()` 메서드를 작성한 코드에 `useSelector()` 메서드 부분도 추가해준다.

```jsx
import React from 'react';
import './style.css';

// 1. react-redux에서 useSelector 불러와야 한다.
import { useDispatch, useSelector } from 'react-redux';
import { increase, decrease } from './index.js';

export default function App() {
  const dispatch = useDispatch();
  // 2. useSelector의 콜백 함수의 인자에 Store에 저장된 모든 state가 담긴다.
  // 그대로 return을 하게 되면 Store에 저장된 모든 state를 사용할 수 있다.
  const state = useSelector((state) => state);

  // 3. 변수 state를 콘솔로 확인한다.
  // Store에 저장된 기존 state 값인 1이 찍히는 것을 확인할 수 있다.
  console.log(state);

  const plusNum = () => {
    dispatch(increase());
  };

  const minusNum = () => {
    dispatch(decrease());
  };

  return (
    <div className="container">
      <h1>{`Count: ${state}`}</h1>
      <div>
        <button className="plusBtn" onClick={plusNum}>
          +
        </button>
        <button className="minusBtn" onClick={minusNum}>
          -
        </button>
      </div>
    </div>
  );
}
```

Redux 설정을 다하고 작동해본 결과는 다음과 같다. 

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/1a053a92-d2de-42af-a2b7-083ea38af294" width="90%" />
</center>

<br>

## Redux의 세 가지 원칙

Redux에는 세 가지 원칙이 있다.

### 1. Single source of truth

동일한 데이터는 항상 같은 곳에서 가지고 와야 한다는 의미다. 즉, Redux에는 데이터를 저장하는 **Store** 라는 단 하나뿐인 공간이 있음과 연결이 되는 원칙이다.

### 2. State is read-only

상태는 읽기 전용이라는 뜻으로, React에서 상태갱신함수로만 상태를 변경할 수 있었던 것처럼, Redux의 상태도 직접 변경할 수 없음을 의미한다. 즉, **Action** 객체가 있어야만 상태를 변경할 수 있음과 연결되는 원칙이다.

### 3. Changes are made with pure functions

변경은 순수함수로만 가능하다는 뜻으로, 상태가 엉뚱한 값으로 변경되는 일이 없도록 순수함수로 작성되어야하는 **Reducer** 와 연결되는 원칙이다.

<br>

## Redux install

### 1. 리덕스 설치

```shell
npm i --save redux react-redux
```

### 2. 리덕스 Toolkit 설치
redux toolkit 라이브러리는 redux의 개선 버전으로 볼 수 있으며, 기존 리덕스 문법에서 조금 더 쉬워진다.

```shell
npm install @reduxjs/toolkit react-redux
```

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)

[Redux 공식문서](https://redux.js.org/)

[React-Redux 공식문서](https://react-redux.js.org/)