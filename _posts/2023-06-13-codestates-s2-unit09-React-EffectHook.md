---
layout: post
title: "[S2-Unit09] React - Effect Hook"
date: 2023-06-13 11:52:00 +900
lastmod: 2023-06-13 11:52:00 +900
categories: [CODESTATES, Section02]
tags: [CODESTATES, 코드스테이츠, Section02]
use_math: true
image: 
  path: https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/9e0481a2-04fd-4d82-be2b-cc8948e1a3bf
  width: 900
  alt: React
---

# Effect Hook이란?

> React 컴포넌트 내에서 특정 부분에 변화가 생긴 뒤에 (혹은 렌더링 이후에) 지정한 효과(콜백함수)를 실행한다. 특정 동작이 발생하면 자동으로 특정 행동을 하도록 하는 것을 `Hook` 이라고 보면 된다.

## Side Effect (부수 효과)
함수 내에서 어떤 구현이 함수 외부에 영향을 끼치는 경우 해당 함수는 `Side Effect` 가 있다고 이야기한다.

React에서는 컴포넌트 내에서 fetch를 사용해 API 정보를 가져오거나 이벤트를 활용해 DOM 직접 조작할 때 Side Effect가 발생했다고 말한다.

**전역 변수 foo를 bar 함수가 수정하는 예제**

```jsx
let foo = 'hello';

const bar = () => {
	foo = 'world';
}

bar();  // 여기서 Side Effect 발생
```

### Pure Function (순수 함수)
순수 함수란, 오직 함수의 입력만이 함수의 결과에 영향을 주는 함수를 의미한다.

- 함수의 입력이 아닌 다른 값이 함수의 결과에 영향을 미치는 경우, 순수 함수라고 부를 수 없다.
- 순수 함수는 입력으로 전달된 값을 수정하지 않는다.

```jsx
const upper = (str) => {
	return str.toUpperCase();  // toUpperCase 메소드는 원본을 수정하지 않는다.
}

upper('hello');
```
순수 함수에는 네트워크 요청과 같은 Side Effect가 없다.

순수 함수의 특징 중 하나는 어떠한 전달 인자가 주어질 경우, 항상 똑같은 값이 리턴됨을 보장한다. 그래서 예측 가능한 함수이기도 하다.

### React의 함수 컴포넌트

다음 예시에는 그 어떤 Side Effect도 없으며, 순수 함수로 작동한다.

```jsx
function SingleTweet({ writer, body, createdAt }) {
  return <div>
    <div>{writer}</div>
    <div>{createdAt}</div>
    <div>{body}</div>
  </div>
}
```

이 예시와는 다르게 보통 React 애플리케이션을 작성할 때는 AJAX 요청이 필요하거나 LocalStorage 또는 타이머와 같은 React와 상관없는 API를 사용하는 경우가 발생할 수 있다. 이는 React의 입장에서는 전부 `Side Effect` 다.

**React는 Side Effect를 다루기 위한 Hook인 Effect Hook을 제공한다.**

> **React 컴포넌트에서의 Side Effect** <br>
> - 타이머 사용 (setTimeout)
> - 데이터 가져오기 (fetch API, localStorage)

### Hook을 쓸 때 주의할 점

**1. 최상위에서만 Hook을 호출한다.**

반복문, 조건문 혹은 중첩된 함수 내에서 Hook을 호출하면 안된다. 대신 early return이 실행되기 전에 항상 React 함수의 최상위(at the top level)에서 Hook을 호출해야 한다.

**2. React 함수 내에서 Hook을 호출한다.**

Hook을 일반적인 JavaScript 함수에서 호출하면 안된다. 대신에 다음과 같이 호출할 수 있다.
- React 함수 컴포넌트에서 Hook을 호출한다.
- Custom Hook에서 Hook을 호출한다.

<br>

## useEffect
`useEffect`는 컴포넌트 내에서 Side effect를 실행할 수 있게 하는 Hook이다.

이 컴포넌트에서 실행하는 Side effect는 **브라우저 API를 이용하여, 타이틀을 변경하는 것**이다.

### 첫 번째 인자 - 함수(Function)
> `useEffect(함수)`
> 
> `useEffect` 의 첫 번째 인자는 **함수**다. 해당 함수 내에서 Side effect를 실행하면 된다. 이 함수는 다음과 같은 조건에서 실행된다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/b3cb9a1b-2c24-4fe4-9e03-14c2758279eb" width="80%" />
</center>

- 컴포넌트 생성 후 처음 화면에 렌더링(표시)
- 컴포넌트에 새로운 props가 전달되며 렌더링
- 컴포넌트에 상태(state)가 바뀌며 렌더링

이와 같이 매번 새롭게 컴포넌트가 **렌더링** 될 때 Effect Hook이 실행된다.

### 두 번째 인자 - 배열(Array)

> `useEffect(함수, [종속성1, 종속성2, ...])`
>
> `useEffect` 의 두 번째 인자는 **배열**이다. 이 배열은 조건을 담고 있으며, 여기서 말하는 조건은 boolean 형태의 표현식이 아닌, **어떤 값의 변경이 일어날 때**를 의미한다.

따라서 해당 배열엔 **어떤 값의 목록**이 들어간다. 이 배열을 특별히 **종속성 배열**이라고 부른다. 

배열 내의 종속성1 또는 종속성2의 값이 변할 때, 첫 번째 인자의 함수가 실행된다.

### 단 한 번만 실행되는 Effect 함수
> **1. 빈 배열 넣기** <br>
> `useEffect(함수, [])`
>
> 빈 배열을 useEffect의 두 번재 인자로 사용하면, 이때는 컴포넌트가 처음 생성될 때만 effect 함수가 실행된다. 대표적으로 사용하는 경우는 처음 단 한 번, 외부 API를 통해 리소스를 받아오고 더 이상 API 호출이 필요하지 않을 때 사용할 수 있다.
>
> **2. 아무것도 넣지 않기 (default 형태)** <br>
> `useEffect(함수)`
>
> 기본 형태의 useEffect는 컴포넌트가 처음 생성되거나 props가 업데이트되거나, 상태(state)가 업데이트될 때 effect 함수가 실행된다.

<br>

## Data Fetching: 필터링 예제 다시 보기
목록 내 필터링을 구현하기 위해서는 다음과 같은 두 가지 접근이 있을 수 있다.

1. **컴포넌트 내에서 필터링**: 전체 목록 데이터를 불러오고, 목록을 검색어로 filter 하는 방법
2. **컴포넌트 외부에서 필터링**: 컴포넌트 외부로 API 요청을 할 때, 필터링 한 결과를 받아오는 방법 (보통, 서버에 매번 검색어와 함께 요청하는 경우가 이에 해당한다.)

### 1. 컴포넌트 내에서 필터링

처음 단 한 번, 외부 API로부터 명언 목록을 받아오고, filter 함수를 이용한다.

```jsx
import { useEffect, useState } from "react";
import "./styles.css";
import { getProverbs } from "./storageUtil";

export default function App() {
  const [proverbs, setProverbs] = useState([]);
  const [filter, setFilter] = useState("");

  useEffect(() => {
    console.log("언제 effect 함수가 불릴까요?");
    const result = getProverbs();
    setProverbs(result);
  }, []);

  const handleChange = (e) => {
    setFilter(e.target.value);
  };

  return (
    <div className="App">
      필터
      <input type="text" value={filter} onChange={handleChange} />
      <ul>
        {proverbs
          .filter((prvb) => {
            return prvb.toLowerCase().includes(filter.toLowerCase());
          })
          .map((prvb, i) => (
            <Proverb saying={prvb} key={i} />
          ))}
      </ul>
    </div>
  );
}

function Proverb({ saying }) {
  return <li>{saying}</li>;
}
```

### 2. 컴포넌트 외부에서 필터링

검색어가 바뀔 때마다, 외부 API를 호출한다.

```jsx
import { useEffect, useState } from "react";
import "./styles.css";
import { getProverbs } from "./storageUtil";

export default function App() {
  const [proverbs, setProverbs] = useState([]);
  const [filter, setFilter] = useState("");
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log("언제 effect 함수가 불릴까요?");
    const result = getProverbs(filter);
    setProverbs(result);
  }, [filter]);

  const handleChange = (e) => {
    setFilter(e.target.value);
  };

  const handleCounterClick = () => {
    setCount(count + 1);
  };

  return (
    <div className="App">
      필터
      <input type="text" value={filter} onChange={handleChange} />
      <ul>
        {proverbs.map((prvb, i) => (
          <Proverb saying={prvb} key={i} />
        ))}
      </ul>
      <button onClick={handleCounterClick}>카운터 값: {count}</button>
    </div>
  );
}

function Proverb({ saying }) {
  return <li>{saying}</li>;
}
```

### 두 방식의 차이점

현재는 `LocalStorage API` 를 이용해 외부 API를 직접 구현했지만, 이는 서버 요청으로 대체할 수 있다. 다음은 HTTP를 이용한 서버 요청을 가정할 때, 두 방식의 차이점을 설명하고 있다.

**컴포넌트 내부에서 처리**

- **장점**: HTTP 요청의 빈도를 줄일 수 있다.
- **단점**: 브라우저(클라이언트)의 메모리 상에 많은 데이터를 갖게 되므로, 클라이언트의 부담이 늘어난다.

**컴포넌트 외부에서 처리**

- **장점**: 클라이언트가 필터링 구현을 생각하지 않아도 된다.
- **단점**: 빈번한 HTTP 요청이 일어나게 되며, 서버가 필터링을 처리하므로 서버가 부담을 가져간다.

<br>

### AJAX 요청
임의로 구현한 `LocalStorage API` 대신, fetch API를 써서, 서버에 요청하면 다음과 같다. 명언을 제공하는 API의 엔드포인트는 `http://서버주소/proverbs` 라고 가정한다.

```jsx
useEffect(() => {
  fetch(`http://서버주소/proverbs?q=${filter}`)
  	.then(resp => resp.json())
  	.then(result => {
    	setProverbs(result);
  	})
}, [filter]);
```

### AJAX 요청이 느릴 경우
모든 네트워크 요청이 항상 즉각적인 응답을 가져다주는 것은 아니다. 외부 API 접속이 느릴 경우를 고려하여, 로딩 화면(loading indicator)의 구현은 필수적이다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/4afdd324-d524-42da-b113-9d97ac81f940" width="80%" />
</center>

기본적으로 Loading 화면에도 상태 처리는 필요하다. 

```jsx
const [isLoading, setIsLoading] = useState(true);

// 생략, LoadingIndicator 컴포넌트는 별도로 구현했음을 가정한다.
return {isLoading ? <LoadingIndicator /> : <div>로딩 완료 화면</div>}
```

fetch 요청의 전후로 `setIsLoading` 을 설정해 주어 보다 나은 UX를 구현할 수 있다.

```jsx
useEffect(() => {
	setIsLoading(true);
  	fetch(`http://서버주소/proverbs?q=${filter}`)
  		.then(resp => resp.json())
  		.then(result => {
    		setProverbs(result);
      		setIsLoading(false);
    	})
}, [filter]);
```

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)
