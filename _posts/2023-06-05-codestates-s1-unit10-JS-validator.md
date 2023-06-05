---
layout: post
title: "[S1-Unit10] 회원가입 validator check 회고"
date: 2023-06-05 14:41:00 +900
lastmod: 2023-06-05 14:41:00 +900
categories: [CODESTATES, Section01]
tags: [CODESTATES, 코드스테이츠, Section01, 회고]
use_math: true
image: 
  path: https://velog.velcdn.com/images/tlsl13/post/03a8f906-3a07-450e-a1bd-0a64e7cec78d/image.gif
  width: 901
  alt: 내가 구현한 회원가입 폼
---

## 과제 Rule
### HTML - 비밀번호 입력 및 비밀번호 입력 창

> 비밀번호 입력 창: `#password` <br>
비밀번호 확인 입력 창: `#password-retype` <br>
시각적 피드백: `.mismatch-messge` <br>

시각적 피드백은 "비밀번호가 일치 않습니다." 메시지를 출력해야 한다.

### JavaScript - 유효성 검사 함수 작성
함수 `isMatch` 가 파일 script.js 에 작성되어야 한다. 이 함수는 문자열 두 개를 입력으로 받고, boolean 타입을 리턴한다. 작성 후 개발자 콘솔에서 `isMatch('암호1', '암호2')` 와 같이 테스트를 진행해야 한다.

### 이벤트 연결과 시각적 피드백 제공
의사코드는 다음과 같다. 다음의 의사코드를 자바스크립트로 작성하면 성공이다.

- [비밀번호 확인] 입력창에서 값을 입력(keyup)하면
- [비밀번호] 값과 [비밀번호 확인] 값이 일치하는지 확인하고,
- 일치하지 않은 경우, 불일치 메시지를 화면에 표시한다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/6d1955f2-6a2d-4191-b0fe-e0cc4536f54a" width="80%" />
</center>

위에 사진처럼 간단한 과제를 수행한 후, 나만의 회원가입 페이지로 새롭게 다시 구현해보았다.

<br>

## 👩🏻‍💻 CODE

```jsx
// Email
let emailInput = document.querySelector('#email');
let emailFailed = document.querySelector('.email-failed');

// Password
let passwordInput = document.querySelector('#password');
let passwordFailed = document.querySelector('.password-message');
let passwordReInput = document.querySelector('#password-retype');
let passwordReFailed = document.querySelector('.password-remessage');

// Name
let nameInput = document.querySelector('#name');
let nameFailed = document.querySelector('.name-message');

// Date of Bir
let dateInput = document.querySelector('#date');
let dateFailed = document.querySelector('.date-message');



// 이메일 확인
emailInput.onkeyup = function () {
  // 이메일 형식: 알파벳+숫자@알파벳+숫자.알파벳+숫자
  let exptext = /^([0-9a-zA-Z_\.-]+)@([0-9a-zA-Z_-]+)(\.[0-9a-zA-Z_-]+){1,2}$/;  
  if (exptext.test(emailInput.value) === true) {
    emailFailed.classList.add('hide');
  } else {
    emailFailed.classList.remove('hide');
    icon.classList.remove('hide');
  }
}

// 비밀번호 확인
passwordInput.onkeyup = function () {
  // 비밀번호 형식: 최소 8자 이상, 알파벳과 숫자 및 특수문자(@$!%*#?&)는 하나 이상 포함
  let exptext = /^(?=.*[A-Za-z])(?=.*\d)(?=.*[@$!%*#?&])[A-Za-z\d@$!%*#?&]{8,}$/;
  if (exptext.test(passwordInput.value) === true) {
    passwordFailed.classList.add('hide');
  } else {
    passwordFailed.classList.remove('hide');
  }
}

// 비밀번호 재확인
passwordReInput.onkeyup = function () {
  if (passwordInput.value === passwordReInput.value) {
    passwordReFailed.classList.add('hide');
  } else {
    passwordReFailed.classList.remove('hide');
  }
}

// 이름 확인
nameInput.onkeyup = function () {
  let exptext = /^[가-힣]{2,4}|[a-zA-Z]{2,10}\s[a-zA-Z]{2,10}$/;;
  if (exptext.test(nameInput.value) === true) {
    nameFailed.classList.add('hide');
  } else {
    nameFailed.classList.remove('hide');
  }
}

// 생년월일(6자리) 입력 확인
dateInput.onkeyup = function () {
  let exptext = /([0-9]{2}(0[1-9]|1[0-2])(0[1-9]|[1,2][0-9]|3[0,1]))/;
  if (exptext.test(dateInput.value) === true) {
    dateFailed.classList.add('hide');
  } else {
    dateFailed.classList.remove('hide');
  }
}
```

<br>

## Feelings ...
튜토리얼 영상을 확실하게 이해하고 넘어가서 그런지, 비밀번호 관련 유효성 검사 기능 구현도 손쉽게 하였다. 2일동안 진행되는 과제였는데 나는 영상시청과 코드 구현까지 40분도 안걸렸다..? 과제 기간이 길어서 시작하기도 전에 살짝 겁을 먹었었는데 오히려 너무 간단해서 웃음이 나왔다. 그래도 나중에 회원가입 및 로그인 기능을 구현하게 되면 유용하게 사용될 것 같은 기능이라 한번 더 복습할 예정이다 😛

## Findings ...
튜토리얼 영상을 시청하기 전에 나는 `div` 를 자바스크립트에서 나타나고 숨기는 코드만 생각을 하였는데, CSS `class` 를 이용해서 `add` 와 `remove` 로 스타일을 손쉽게 조작할 수 있는 것을 이번 과제를 통해서 알게되었다. 

CSS `class` 를 이용해서 간접적으로 바꾸는 것을 권장하는 이유
- 디자인의 디테일한 요소가 자바스크립트 코드에 담기는 것을 방지한다.
- 따로 클래스를 이용하면, 해당 디자인을 디자이너가 쉽게 바꿀 수 있다.
- CSS는 디자인, 자바스크립트는 로직에 집중할 수 있다.

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)