---
layout: post
title: "[S2-Unit09] React - React 데이터 흐름, State 끌어올리기 (Lifting State Up)"
date: 2023-06-13 11:32:00 +900
lastmod: 2023-06-13 11:32:00 +900
categories: [CODESTATES, Section02]
tags: [CODESTATES, 코드스테이츠, Section02]
use_math: true
image: 
  path: https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/9e0481a2-04fd-4d82-be2b-cc8948e1a3bf
  width: 900
  alt: React
---

# React 데이터 흐름
React의 개발 방식의 가장 큰 특징은 페이지 단위가 아닌 컴포넌트 단위로 시작한다는 점이다.

## 단방향 데이터 흐름 (one-way data flow)
React는 데이터가 위에서 아래로 흐르는 단방향 데이터 흐름을 따른다. 

React를 대표하는 설명 중 하나일 정도로 중요하며, 컴포넌트는 `props` 를 통해 전달받은 데이터가 어디서 왔는지 전혀 알지 못한다.

### 예시) Twittler 애플리케이션의 데이터 흐름

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/4c9591d5-c357-48c6-96f4-3189ab1cd7dc" width="80%" />
</center>

트위터 형식의 컴포넌트로 디자인을 하고, 트리 구조로 나타낸 것이다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/2665bd4f-ff46-45a3-9de7-b656ca319036" width="80%" />
</center>

사진에서 보이는 것처럼 데이터를 전달하는 주체는 부모 컴포넌트가 된다. 이는 데이터 흐름이 하향식(top-down)임을 의미한다.

**데이터 정의**

우선 애플리케이션에서 필요한 데이터를 다음과 같이 정의할 수 있다. 이 데이터들은 언제든지 변할 수 있어 상태(state)라고 할 수 있다.

- 전체 트윗 목록
- 사용자가 작성 중인 새로운 트윗 내용

하지만, 모든 데이터를 state로 둘 필요는 없다. 오히려 state는 최소화하는 것이 좋으며, state가 많아질수록 애플리케이션은 복잡해진다.

> **만약 어떠한 데이터를 state로 두어야 하는 지 모르겠으면 다음을 참고한다.** <br>
> 1. 부모로부터 `props` 가 전달되는 지 확인한다. => state x
> 2. 시간이 지나도 변하지 않는지 확인한다.  => state x
> 3. 컴포넌트 안의 다른 state나 props를 가지고 계산이 가능한지 확인한다.  => state o

**state 위치 정하기**

state가 특정 컴포넌트에서만 유의미하다면, 특정 컴포넌트에만 두면 되니까 크게 어렵지 않지만, 만일 하나의 state를 기반으로 두 컴포넌트가 영향을 받는다면 이때에는 공통 소유 컴포넌트를 찾아 그곳에 상태를 위치해야 한다. 

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/e80e5e28-d2e7-4b8d-b4a9-ee9d7a0061fd" width="80%" />
</center>

즉, 두 개의 자식 컴포넌트가 하나의 state에 접근하고자 할 때는 두 자식의 공통 부모 컴포넌트에 state를 위치해야 한다.

### 역방향 데이터 흐름 추가
부모 컴포넌트에서의 state가 하위 컴포넌트에 의해 변하는 것을 발견할 수 있다. `<NewTweetForm>` 컴포넌트에서 버튼을 통한 액션은 부모의 상태를 변화시켜야 한다.

이를 해결할 수 있는 키워드로 바로 "**State 끌어올리기(Lifting state up)**"다. 

State 끌어올리기(Lifting state up)는 상태를 변경시키는 함수(handler)를 하위 컴포넌트에 props로 전달해서 해결할 수 있다.

<br>

## State 끌어올리기 (Lifting State Up)

단방향 데이터 흐름이라는 원칙에 따라, 하위 컴포넌트는 상위 컴포넌트로부터 전달받은 데이터의 형태 혹은 타입이 무엇인지만 알 수 있다.
- 데이터가 state로부터 왔는지, 하드코딩으로 입력한 내용인지 알지 못한다.

그러므로 하위 컴포넌트에서의 어떤 이벤트로 인해 상위 컴포넌트의 상태가 바뀌는 것은 마치 "역방향 데이터 흐름"과 같이 조금 이상하게 들릴 수 있다. React가 제시하는 해결책은 다음과 같다.

> 상위 컴포넌트의 "상태를 변경하는 함수" 그 자체를 하위 컴포넌트로 전달하고, 이 함수를 하위 컴포넌트가 실행한다.

여전히 단방향 데이터 흐름의 원칙에 부합하는 해결 방법으로 이것이 "**상태 끌어올리기**"다.

### Action Item: Twittler 예제 분석하기
React 데이터 흐름 슬라이드에 등장한 Twittler의 소스코드에 State 끌어올리기를 적용한 모습이다.

```jsx
import React, { useState } from "react";
import "./styles.css";

const currentUser = "김코딩";

function Twittler() {
  const [tweets, setTweets] = useState([
    {
      uuid: 1,
      writer: "김코딩",
      date: "2020-10-10",
      content: "안녕 리액트"
    },
    {
      uuid: 2,
      writer: "박해커",
      date: "2020-10-12",
      content: "좋아 코드스테이츠!"
    }
  ]);

  const addNewTweet = (newTweet) => {
    setTweets([...tweets, newTweet]);
  };

  return (
    <div>
      <div>작성자: {currentUser}</div>
      { /* ADD: NewTweetForm에 버튼 클릭 시 props를 내려받는다. */ } 
      <NewTweetForm onButtonClick={addNewTweet} />
      <ul id="tweets">
        {tweets.map((t) => (
          <SingleTweet key={t.uuid} writer={t.writer} date={t.date}>
            {t.content}
          </SingleTweet>
        ))}
      </ul>
    </div>
  );
}

function NewTweetForm({ onButtonClick }) {
  const [newTweetContent, setNewTweetContent] = useState("");

  const onTextChange = (e) => {
    setNewTweetContent(e.target.value);
  };

  const onClickSubmit = () => {
    let newTweet = {
      uuid: Math.floor(Math.random() * 10000),
      writer: currentUser,
      date: new Date().toISOString().substring(0, 10),
      content: newTweetContent
    };
    { /* ADD. newTweet이 addNewTweet에 전달되어야 한다. */ } 
    onButtonClick(newTweet);
  };

  return (
    <div id="writing-area">
      <textarea id="new-tweet-content" onChange={onTextChange}></textarea>
      <button id="submit-new-tweet" onClick={onClickSubmit}>
        새 글 쓰기
      </button>
    </div>
  );
}

function SingleTweet({ writer, date, children }) {
  return (
    <li className="tweet">
      <div className="writer">{writer}</div>
      <div className="date">{date}</div>
      <div>{children}</div>
    </li>
  );
}

export default Twittler;
```


<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)
