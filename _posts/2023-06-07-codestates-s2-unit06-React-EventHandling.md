---
layout: post
title: "[S2-Unit06] React - 이벤트 핸들링 (Event Handling)"
date: 2023-06-07 14:38:00 +900
lastmod: 2023-06-07 14:38:00 +900
categories: [CODESTATES, Section02]
tags: [CODESTATES, 코드스테이츠, Section02]
use_math: true
image: 
  path: https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/9e0481a2-04fd-4d82-be2b-cc8948e1a3bf
  width: 900
  alt: React
---

# 이벤트 핸들링 (Event Handling)

React의 이벤트 처리는 DOM의 이벤트 처리 방식과 유사하지만, 몇 가지의 문법 차이가 있다.

- React에서 이벤트는 소문자 대신 **카멜 케이스(camelCase)** 를 사용한다.
- JSX를 사용하여 문자열이 아닌 함수로 이벤트 처리 함수를 전달한다.

HTML과 React 이벤트 처리 방식은 다음과 같다.

```jsx
// HTML에서 이벤트 처리 방식
<button onclick='handleEvent()'>Event</button>

// React의 이벤트 처리 방식
<button onClick={handleEvent}>Event</button>
```

## onChange

`<input>`, `<textarea>`, `<select>` 와 같은 폼(Form) element는 사용자의 입력값을 제어하는데 사용된다. **React에서는 이러한 변경될 수 있는 값을 일반적으로 컴포넌트와 state로 관리하고 업데이트 한다.**

- `onChange` 이벤트가 발생하면 `e.target.value` 를 통해 이벤트 객체에 담겨있는 input 값을 읽어올 수 있다. 
- `input` 태그에 `value` 와 `onChange` 는 input의 텍스트가 바뀔 때마다 발생하는 이벤트다.
- 이벤트가 발생하면 `handleChange` 함수가 작동하며, 이벤트 객체에 담긴 input 값을 `setState` 를 통해 새로운 state로 갱신한다.

```jsx
function NameForm() {
  const [name, setName] = useState("");
  
  const handleChange = (e) => {
  	setName(e.target.value);
  };
  
  return (
  	<div>
      <input type='text' value={name} onChange={handleChange} />
      <h1>{name}</h1>
    </div>
  ); 
};
```

## onClick

- `onClick` 이벤트는 말 그대로 사용자가 **클릭**이라는 행동을 하였을 때 발생하는 이벤트다.
- 버튼이나 `<a>` 태그를 통한 링크 이동 등과 같이 주로 사용자의 행동에 따라 애플리케이션이 반응해야 할 때 자주 사용하는 이벤트다.

위에 예시에서 `onChange` 버튼을 추가하여 버튼 시 `input` 태그에 입력한 이름이 alert을 통해 알림 창이 팝업되도록 코드를 추가하면 다음과 같이 2가지 방법으로 작성할 수 잇다.

### 1. 함수 정의하기

```jsx
function NameForm() {
  const [name, setName] = useState("");

  const handleChange = (e) => {
    setName(e.target.value);
  };

  return (
    <div className="App">
      <h1>Event handler practice</h1>
      <input type="text" value={name} onChange={handleChange}></input>
      <button onClick={() => alert(name)}>Button</button>
      <h3>{name}</h3>
    </div>
  );
}
```

### 2. 함수 자체를 전달하기

```jsx
function NameForm() {
  const [name, setName] = useState("");

  const handleChange = (e) => {
    setName(e.target.value);
  };

  const handleClick = () => {
    alert(name);
  };
  
  return (
    <div className="App">
      <h1>Event handler practice</h1>
      <input type="text" value={name} onChange={handleChange} />
      <button onClick={handleClick}>Button</button>
      <h3>{name}</h3>
    </div>
  );
}
```

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)
