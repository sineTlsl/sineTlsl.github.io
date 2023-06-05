---
layout: post
title: "[S1-Unit10] JS/Browser - 이벤트 객체 (Event Object)"
date: 2023-06-05 14:45:00 +900
lastmod: 2023-06-05 14:45:00 +900
categories: [CODESTATES, Section01]
tags: [CODESTATES, 코드스테이츠, Section01]
use_math: true
image: 
  path: https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/cafc9464-5f16-4221-ac5f-8060a7374a10
  width: 850
  alt: 이벤트 객체 (Event Object)
---

# 이벤트 객체란?

> `이벤트 객체 (Event Object)` 는 DOM 관련된 이벤트가 발생되면 발생하는 관련 정보를 저장하는 객체다.

이벤트 객체는 사용자 입력(`onclick`, `onkeyup`, `onscroll` 등)을 트리거로 발생한 이벤트 정보를 담은 객체다.

## 이벤트 종류

**Mouse Event**
- `click` : 마우스 버튼을 클릭할 때 (터치스크린이 있는 장치에선 탭 했을 때)
- `mouseover` : 마우스 커서를 요소에서 오버 했을 때 
- `mouseout` : 마우스 커서를 요소에서 아웃 했을 때 
- `mousedown` : 요소에 마우스를 눌렀을 때
- `mouseup` : 요소에 마우스를 떼었을 때
- `mousemove` : 요소에 마우스를 움직였을 때
- `contextmenu` : context menu(마우스 오른쪽 버튼을 눌렀을 때 나오는 메뉴)가 나오기 전에 이벤트 발생

**Keyboard Event**
- `keydown` : 사용자가 키보드를 처음 눌렀을 때 (키가 눌린 동안은 계속해서 발생)
- `keyup` : 사용자가 키보드 버튼을 누르거나 뗄 때
- `keypress` : 사용자가 눌렀던 키의 문자가 입력되었을 때 (키 눌렀거나/누르고 있는중이라 페이지에 문자 입력 되고있음)

**Focus Event**
- `focus` : 요소가 포커스를 얻었을 때
- `blur` : 요소가 포커스를 잃었을 때

**Form Event**
- `input` : input/textarea 요소 값이 변경될 때 
- `submit` : 사용자가 `<form>` 을 제출할 때
- `change` : 선택 상자, 체크박스, 라디오 버튼의 상태가 변경되었을 때

**Document Event**
- `DOMContentLoaded` : HTML이 전부 로드 및 처리되어 DOM 생성이 완료되었을 때 발생한다.

<br>

## 이벤트 핸들러
### 1. 이벤트 핸들러 프로퍼티

```jsx
문서객체선택.on이벤트타입명 = function (이벤트객체매개변수) {
	...
}
```

- 이벤트 핸들러 프로퍼티의 키 = on + 이벤트 타입
- 이벤트 타깃.on + 이벤트 타입 = 이벤트 핸들러

이벤트 핸들러 프로퍼티 방식은 이벤트 핸들러 Attribute 방식의 HTML과 자바스크립트가 뒤섞이는 문제를 해결할 수 있다. 하지만, 이벤트 핸들러 프로퍼티에 **하나의 이벤트 핸들러만 바인딩할 수 있다는 단점**이 있다.

### 2. addEventListener

```jsx
문서객체선택.addEventListener('이벤트타입', function (이벤트객체매개변수) {
	...
});
```
- 이벤트 타킷.addEventListener('이벤트 타입', 이벤트 핸들러)

이벤트 핸들러 프로퍼티 방식과는 달리 on 접두사를 붙이지 않는다. 또 동일한 HTML 요소에 발생한 동일한 이벤트에 대해 **하나 이상의 이벤트 핸들러를 등록**할 수 있다.

### 이벤트 핸들러 프로퍼티와 addEventListener 비교
`onclick` 과 같은 이벤트 핸들러 프로퍼티 방식은 하나의 콜백만 지정할 수 있지만, `addEventListener` 를 사용할 경우에 여러 개의 이벤트 리스너를 추가할 수 있다. 

만약 `onclick` 이벤트 핸들러를 두 번 이상 사용한다면, 기존 이벤트 핸들러를 덮어쓰기 때문에 가장 아래에 추가한 핸들러만 제대로 작동한다. 

반면, `addEventListener` 는 기존 이벤트 핸들러를 덮어 쓰지 않고 얼마든지 계속해서 핸들러를 추가해도 모든 핸들러가 정상적으로 작동한다.

#### 그러면 onclick은 왜 쓰는건지 궁금할 수 있는데,
`onclick` 은 초기 DOM Level-0에서 제공하던 기능이고, 그 이후 버전인 Level-2에서 추가된 것이 `addEventListener` 이다.

**addEventListener는 IE8 이하에서는 작동을 하지 않는다.** 그래서 구형 브라우저 지원이 필요하면 `onclick` 을 사용하거나 다른 방법을 찾아야 한다.

<br>

## 실습
화면에 아메리카노와 카페라떼 두 개의 버튼이 있다고 가정할 때, 각각의 버튼을 클릭할 때마다 이벤트가 발생하여 `console` 에 문자열을 출력해주는 실습을 진행한다.

```html
<!-- button 구성 -->
<body>
    <button>아메리카노</button>
    <button>카페라떼</button>
</body>
```

```jsx
let menus = document.querySelectorAll('button');

let btnAmericano = menus[0];
let btnCaffelatte = menus[1];

function handleClick(event) {
	let currentMenu = event.target.textContent;
    console.log(currentMenu + "를 클릭하셨습니다."):
}

btnAmericano.onclick = handleClick;
btnCaffelatte.onclick = handleClick;
```

`let menus = document.querySelectorAll('button');` 으로 버튼을 요소를 다 가져오고, `btnAmericano` 와 `btnCaffelatte` 에 각각 할당해준다. 

그 다음은 두 버튼의 이벤트 핸들러가 동일한 `handleClick` 함수에서 동작을 할 수 있는 코드다. 이렇게 함수를 작성하면 중복을 줄여주고, 여러 번 재사용할 수 있다.

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)

[[Javascript] 자바스크립트 이벤트 - 이벤트 등록](https://min-kyung.tistory.com/25)

[[JS] onclick과 addEventListener 비교](https://jess2.github.io/2018/05/15/JavaScript/JS-onclick%EA%B3%BC-addEventListener-%EB%B9%84%EA%B5%90/)

[Javascript Event](http://milooy.github.io/TIL/JavaScript/event.html#%E1%84%8B%E1%85%B5%E1%84%87%E1%85%A6%E1%86%AB%E1%84%90%E1%85%B3-%E1%84%8C%E1%85%A9%E1%86%BC%E1%84%85%E1%85%B2)