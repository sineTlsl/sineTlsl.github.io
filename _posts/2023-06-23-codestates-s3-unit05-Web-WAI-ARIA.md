---
layout: post
title: "[S3-Unit05] Web - WAI-ARIA"
date: 2023-06-23 17:43:00 +900
lastmod: 2023-06-23 17:43:00 +900
categories: [CODESTATES, Section03]
tags: [CODESTATES, 코드스테이츠, Section03]
use_math: true
---

# WAI-ARIA란?

> `WAI-ARIA(Web Accessibility Initiative – Accessible Rich Internet Applications)` 는 웹 페이지, 특히 동적 콘텐츠, 그리고 AJAX, HTML, JavaScript 및 관련 기술로 개발된 사용자 인터페이스 구성 요소의 접근성을 증가시키는 방법에 대해 규정한 W3C가 출판한 기술 사양이다.

WAI-ARIA는 WAI와 ARIA를 합친 단어다.

- **WAI (Web Accessibility Initiative)** : 웹 표준을 정하는 W3C에서 웹 접근성을 담당하는 기관
- **ARIA (Accessible Rich Internet Applications)** : 장애가 있는 사람들이 웹 콘텐츠와 웹 응용 프로그램에 더 쉽게 액세스할 수 있도록 하는, 즉 웹 접근성을 갖추기 위한 기술
  - **RIA (Rich Internet Applications)** : 따로 프로그램을 설치하지 않아도 웹 브라우저를 통해 사용할 수 있는 편리성 + 프로그램을 직접 설치해서 사용하는 것처럼 빠른 반응의 사용자 인터페이스를 동시에 가지는 웹 애플리케이션. (SPA를 의미하는 경우가 많음)

<br>

## WAI-ARIA의 필요성

HTML 요소에 의미를 부여한 시맨틱 요소를 사용하는 것만으로도 웹 접근성을 향상시킬 수 있다. WAI-ARIA는 이러한 **HTML 요소에 추가적으로 의미를 부여**할 수 있게 해준다.

1. 시맨틱 요소만으로 의미를 충분히 부여할 수 없는 상황에 WAI-ARIA를 사용하면 HTML 요소에 추가적인 의미를 부여하여 더 원활하게 페이지를 탐색할 수 있게 도와준다.

2. SPA처럼 AJAX를 사용하는 상황, 즉 새로고침 없이 페이지의 내용이 바뀌는 상황에서도 변경된 영역에대한 정보를 전달해줄 수 있어 동적인 콘텐츠에서도 웹 접근성을 향상시킬 수 있다.

<br>

## WAI-ARIA 사용법

WAI-ARIA는 HTML 태그 내부에 속성(attribute)을 추가함으로써 의미를 부여해줄 수 있다. 속성은 크게 세 가지로 분류되어 있다.

> - **역할(role)** : HTML 요소의 역할을 정의하는 속성
> - **상태(state)** : 요소의 현재 상태를 나타내는 속성
> - **속성(property)** : 요소의 특징을 정의하는 속성

### 1. 역할(Role)

HTML의 요소 종류와 역할이 서로 맞지 않을 때, 어떤 역할을 하는 요소인지 명시해줄 때 사용할 수 있는 속성이다. 

**ex 1)** 버튼으로 사용되는 요소를 만들었는데 `<div>` 요소를 사용했다면, 이 요소가 버튼 역할을 하고 있음을 다음과 같이 표시해줄수 있다.

```jsx
<div role="button">div이지만 button으로 사용되는 요소</div>
```
> **[주의할 점]**
> - HTML 요소로 충분히 파악할 수 있는 내용을 WAI-ARIA로 또 설명해줄 필요는 없다.
> - 시맨틱 요소 본연의 의미를 임의로 바꾸지 않아야 한다.
> ```jsx
> // WAI-ARIA의 잘못된 사용 예시
> <button role="button">button인 요소</button>
>
> // WAI-ARIA의 잘못된 사용 예시
> <h1 role="button">h1인 요소</h1>
> ```

**ex 2)** Tab 컴포넌트의 요소들이 어떤 기능하는 지 표시해줄 수 있다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/6f97a600-498e-4b35-9803-aa1882eb39de" width="90%" />
</center>

```jsx
// 1. 컴포넌트 구조를 간소화한 모습
<div>
  <li>Tab1</li>
  <li>Tab2</li>
  <li>Tab3</li>
</div>

<div>Tab menu ONE</div>
<div>Tab menu TWO</div>
<div>Tab menu THREE</div>
```
```jsx
// 2. 위에 코드를 WAI-ARIA를 사용해서 이 구조가 탭의 역할 표시
<div role="tabList">
  <li role="tab">Tab1</li>
  <li role="tab">Tab2</li>
  <li role="tab">Tab3</li>
</div>

<div role="tabpanel">Tab menu ONE</div>
<div role="tabpanel">Tab menu TWO</div>
<div role="tabpanel">Tab menu THREE</div>
```

### 2. 상태(State)
Tab 컴포넌트 예시에서 `role` 속성을 추가하여 해당 요소의 역할을 명시하였다. 여기서 어떤 탭이 선택 되었는지 확인할 수 있는 방법으로는 `aria-selected` 가 있다.

- **aria-selected**: 여러 개의 선택 가능한 요소 중에서 선택 상태인 요소를 표시

```jsx
<div role="tabList">
  <li role="tab" aria-selected="true">Tab1</li>
  <li role="tab" aria-selected="false">Tab2</li>
  <li role="tab" aria-selected="false">Tab3</li>
</div>

<div role="tabpanel">Tab menu ONE</div>
<div role="tabpanel">Tab menu TWO</div>
<div role="tabpanel">Tab menu THREE</div>
```
3개의 탭 중에서 첫 번째 탭이 선택된 상태임을 알 수 있다. 

이 외에도 아코디언 UI가 펼쳐진 상태인지 표시해주는 `aria-expanded`, 요소가 숨김 상태인지를 표시하는 `aria-hidden` 등의 속성이 있다.

### 3. 속성(Property)
- **aria-label**: 요소에 라벨을 붙여지는 기능

이미지만 들어 있는 버튼의 경우 HTML 요소의 구조만으로 어떤 역할을 하는 버튼인지 파악하기 어렵다.

```jsx
// default
<button> <img src="X.png" /> </button>
<button> <img src="돋보기.png" /> </button>

// aria-label 사용
<button aria-label="닫기"/> <img src="X.png" /> </button>
<button aria-label="검색"/> <img src="돋보기.png" /> </button>
```

- **aria-live**: 해당 요소가 실시간으로 내용을 갱신하는 영역인지 표시. 
> 브라우징 도중에 내용을 띄우는 `alert`, `modal`, `dialog` 와 같은 역할을 하는 요소이거나, AJAX 기술을 사용하여 실시간으로 내용을 갱신하는 영역에 사용하는 속성이다.
>
> 속성값으로는 `polite`, `assertive`, `off(default)` 가 있다.

이 외에도 다양한 WAI-ARIA 속성들이 존재하지만, 양이 방대하여 당장은 `role`, `aria-label` 정도만 사용해도 HTML에 추가적인 의미를 부여할 수 있기 때문에 웹 접근성을 어느정도 향상시킬 수 있다.

핵심은 **웹 접근성을 확보할 때 가장 중요한 것은 시맨틱한 HTML을 작성하는 것이다.**

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)
