---
layout: post
title: "[S1-Unit11] My Agora States 회고"
date: 2023-06-05 14:51:00 +900
lastmod: 2023-06-05 14:51:00 +900
categories: [CODESTATES, Section01]
tags: [CODESTATES, 코드스테이츠, Section01, 회고]
use_math: true
image: 
  path: https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/4a9b0bfc-3996-470e-878c-b79711a29a8c
  width: 600
  alt: My Agora States 회고
---

## 과제 Rule
다음과 같이 과제가 주어졌고, 내가 직접 구현한 것만 체크하였다.

### Bare Minimum Requirement
> - 디스커션 나열 기능 <br>
    - ☑️ `script.js`를 수정하여 `agoraStatesDiscussions` 배열의 데이터를 나열할 수 있게 구현합니다.
> - ☑️ CSS <br>
    - ☑️ 아고라 스테이츠 질문 리스트가 중앙으로 와야 합니다. <br>
    - ☑️ `style.css`를 수정하여 멋지고 아름답게 나만의 아고라 스테이츠를 꾸밉니다. <br>
    - ☑️ [colorhunt](https://colorhunt.co/palettes/popular), [dribbble](https://dribbble.com/)에서 적절한 색 조합, 디자인을 참고합니다. <br>
> - ☑️ 디스커션 추가 기능 <br>
    - ☑️ `script.js`를 수정하여 디스커션 추가 기능을 구현합니다. <br>
    - ☑️ `section.form__container` 요소에 새로운 아고라 스테이츠 질문을 추가할 수 있는 입력 폼을 제작합니다. 형식은 자유입니다. <br>
    - ☑️ 아이디, 본문을 입력하고 버튼을 누르면 실제 화면에 디스커션이 추가되어야 합니다. <br>
    - ☑️ `agoraStatesDiscussions` 배열에 추가한 데이터가 실제 쌓여야 합니다. <br>
> - ☑️ Github Page 배포 <br>
    - ☑️ Github Page 배포 기능을 이용하여 누구나 볼 수 있게 배포합니다.
> - ☑️ 코드스테이츠 fe-sprint-my-agora-states 리포지토리로 Pull Request <br>
    - ☑️ 나만의 아고라 스테이츠를 코드스테이츠 깃허브에 Pull request합니다. <br>
    - ☑️ 주어진 Pull request 형식에 따라주세요.

### Advanced Challenge
> - ☑️ 현지 시간 적용 <br>
    - ☑️ 샘플 시간을 잘 변형하여, 현지 시간에 맞게 표현합니다. (ex. 오전 10:02:17)
> - [ ] 페이지네이션 기능 <br>
    - ☑️ 페이지네이션에 대해서 스스로 학습합니다. <br>
    - [ ] 한 페이지에 10개씩 디스커션이 보여야 합니다. <br>
    - [ ] 다음 페이지로 넘어갈 수 있어야 합니다. <br>
    - [ ] 이전 페이지로 돌아올 수 있어야 합니다. <br>
    - [ ] 다음 페이지가 없거나, 이전 페이지가 없는 경우 페이지를 유지해야 합니다.
> - ☑️ 디스커션 유지 기능 <br>
    - ☑️ LocalStorage에 대해서 스스로 학습하고, 새롭게 추가하는 Discussion이 페이지를 새로고침해도 유지되도록 제작합니다.

<br>

## 👩🏻‍💻 CODE

```jsx
// convertToDiscussion은 아고라 스테이츠 데이터를 DOM으로 바꿔준다.
const convertToDiscussion = (obj) => {
  const li = document.createElement("li"); // li 요소 생성
  li.className = "discussion__container"; // 클래스 이름 지정

  const avatarWrapper = document.createElement("div");
  avatarWrapper.className = "discussion__avatar--wrapper";
  const discussionContent = document.createElement("div");
  discussionContent.className = "discussion__content";
  const discussionAnswered = document.createElement("div");
  discussionAnswered.className = "discussion__answered";

  // Img
  const avatarImg = document.createElement('img');
  avatarImg.className = 'discussion__avatar--image';
  avatarImg.src = obj.avatarUrl ? obj.avatarUrl : './webare.png';  // 이미지 경로가 없을 경우에는 기본 이미지로 
  avatarImg.alt = 'avatar of ' + obj.author;
  avatarWrapper.append(avatarImg);
  
  // Title
  const discussionTitle = document.createElement('h4');
  discussionTitle.className = 'discussion__title';
  const discussionA = document.createElement('a');
  discussionA.href = obj.url;
  discussionA.textContent = obj.title;
  discussionTitle.append(discussionA);
  
  // 작성한 사람 정보
  const discussionInform = document.createElement('div');
  discussionInform.className = 'discussion__information';
  discussionInform.textContent = `${obj.author} / ${new Date(obj.createdAt).toLocaleTimeString('ko-kr')}`;
  
  discussionContent.append(discussionTitle, discussionInform);

  // answer 확인
  const discussionAnswer = document.createElement('p');
  obj.answer !== null ? discussionAnswer.textContent = '♥' : discussionAnswer.textContent = '♡';
  discussionAnswered.append(discussionAnswer);
  li.append(avatarWrapper, discussionContent, discussionAnswered);
  return li;
};

// agoraStatesDiscussions 배열의 모든 데이터를 화면에 렌더링하는 함수
const render = (element) => {
  for (let i = 0; i < agoraStatesDiscussions.length; i += 1) {
    element.append(convertToDiscussion(agoraStatesDiscussions[i]));
  }
  return;
};

// localStorage 함수
const renderlocalStorage = (element) => {
  const objLocalData = JSON.parse(localStorage.getItem('agoraDatas'));
  if (objLocalData) {
    for (let i = 0; i < objLocalData.length; i++) {
      element.prepend(convertToDiscussion(objLocalData[i]));
    }
    // renderPagination(); // 확인중
  }
  return;
}

// ul 요소에 agoraStatesDiscussions 배열의 모든 데이터를 화면에 렌더링한다.
const ul = document.querySelector("ul.discussions__container");
render(ul);
renderlocalStorage(ul);

// Form 데이터 삽입
const formInput = document.querySelector('.form');
const formNameInput = document.querySelector('#name');
const formTitleInput = document.querySelector('#title')
const formQuestionInput = document.querySelector('#story');

formInput.addEventListener('submit', (event) => {
  event.preventDefault();

  const newObj = {
    id: "D_kwDOHOApLM4APjJim",
    createdAt: new Date().toISOString(),
    title: formTitleInput.value,
    url: "https://github.com/codestates-seb/agora-states-fe/discussions/45",
    author: formNameInput.value,
    answer: null,
    bodyHTML: formQuestionInput.value,
    avatarUrl: null
  }

  window.localStorage.clear();
  let objData = [];
  if (localStorage.length > 0) {
    let bjLocalData = JSON.parse(localStorage.getItem('agoraDatas'));
    for (let i = 0; i < bjLocalData.length; i++) {
      objData.push(bjLocalData[i]);
    }
  }
  objData.push(newObj);
  localStorage.setItem('agoraDatas', JSON.stringify(objData));

  agoraStatesDiscussions.unshift(newObj);  
  ul.prepend(convertToDiscussion(newObj));

  formInput.reset();
})
```

<br>

## Feelings ...
그 전까지는 주어진 틀 안에서 맞는지 틀렸는지 확인하는 식으로 수행하였는데, 이번에는 처음부터 내가 구현할려니까 너무 힘들었다 😭 구현하는 속도가 너무 느려서 기능을 전부 다 구현하지 못했지만.. 그래도 열심히 했다 ㅠㅠㅠ 시작하기 전부터 .. 헉 막막하다 이런생각도 들었지만 그래도 반 넘게 구현해서 다행이라고 생각한다..

**[처음 배포한 나의 깃허브 프로젝트]**
https://sinetlsl.github.io/fe-sprint-my-agora-states/  

## Findings ...
- [Window.localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage) 에서 자주 사용하는 메서드는 `setItem(key, value)`, `getItem(key)`, `removeItem(key)`, `clear()` 가 있다.
   - **JSON.parse()** : JSON 문자열 -> JavaScript 값으로 변환
   - **JSON.stringify()** : JavaScript 값 -> JSON 문자열로 변환

- addEventListener에서 submit을 사용할 경우, `event.preventDefault()` 를 적용해주면 브라우저 기본 동작인 새로고침이 되는 현상 방지한다.

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)