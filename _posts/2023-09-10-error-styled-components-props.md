---
layout: post
title: "[Error] styled-components 라이브러리 사용 시, 실제 DOM으로 속성이 전달되는 에러 발생"
date: 2023-09-10 20:10:00 +900
lastmod: 2023-09-10 20:10:00 +900
categories: [Error, React]
tags: [Error, React, styled-components]
use_math: true
---

# Warning: Received `true` for a non-boolean attribute
## 에러 발생 원인은?
styled-components 라이브러리를 사용하던 중, 폼 유효성 검사를 반환해서 `boolean` 값으로 넘어가 props로 속성을 전달해주는데, 이때 에러가 발생하였다.

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/be121807-000e-4a35-b32b-0a56c8799f6d" width="100%" />
</p>

> react-dom.development.js:86 Warning: Received `true` for a non-boolean attribute `active`. <br>
If you want to write it to the DOM, pass a string instead: active="true" or active={value.toString()}.
{: .prompt-warning}


이 에러가 발생하는 이유는 React가 isValid라는 prop을 DOM 요소의 표준 속성으로 인식하지 못하기 때문이다. 그렇기 때문에 현재 실제 DOM 전달이 되고, 에러를 반환하는 것이였다.

<br>

## 에러 처리 전 코드는?

기존의 코드는 다음과 같다. 

```ts
{contentTabs.map((tab, idx) => (
  <ContentTabItems key={idx} active={currentTabMode === idx} onClick={() => handlerTabClick(idx)}>
    {tab.title}
  </ContentTabItems>
))}

// =============== 콘텐츠 Vlog or Blog 탭 ===============
const ContentTabItems = styled.li<{ active: boolean }>`
  ${({ theme }) => theme.common.flexCenterRow};
  cursor: pointer;
  font-weight: ${({ active }) => (active ? 600 : 500)};
  letter-spacing: 0.5px;
  font-size: 17px;
  height: 45px;
  color: ${({ active }) => (active ? 'var(--black-hunt)' : 'var(--gray-dark)')};
  position: relative;
`;
```

`active` 속성에서 문제가 발생하는 것이다.

<br>

## 그럼 어떻게 해결해야할까?
내가 에러를 해결한 방법은 `transient props ($)`을 사용하는 것이였다.

[styled-components 공식사이트](https://styled-components.com/docs/faqs#why-am-i-getting-html-attribute-warnings)에 자세하게 나와있다. 나는 한참 삽질하다가 공식문서에서 찾은거지만... 공식문서를 잘 보자..!!!

### transient props ($)
- `$` 는 styled-components의 v5.1.0부터 도입된 `transient props`의 일부다.
- styled-components에서 컴포넌트에 전달된 모든 props는 DOM 요소에도 전달되는데, DOM에서 지원하지 않는 prop를 받는 경우 React는 내가 위에서 발생한 에러처럼 발생시킨다.
- 이때, styled-components는 `transient props`라는 개념을 도입한 것이다.
- `transient props`는 styled-components로 전달되지만 실제 DOM 요소에는 전달되지 않는 props다.
- `transient props`는 `$` 접두사를 사용하여 정의한다.

내가 수정한 코드는 다음과 같다. 수정 전 코드를 비교하면 `$`를 사용유무만 다르지 코드는 동일하다.

```ts
{contentTabs.map((tab, idx) => (
  <ContentTabItems key={idx} $active={currentTabMode === idx} onClick={() => handlerTabClick(idx)}>
    {tab.title}
  </ContentTabItems>
))}

// =============== 콘텐츠 Vlog or Blog 탭 ===============
const ContentTabItems = styled.li<{ $active: boolean }>`
  ${({ theme }) => theme.common.flexCenterRow};
  cursor: pointer;
  letter-spacing: 0.5px;
  font-size: 17px;
  height: 45px;
  font-weight: ${({ $active }) => ($active ? 600 : 500)};
  color: ${({ $active }) => ($active ? 'var(--black-hunt)' : 'var(--gray-dark)')};
  position: relative;
`;
```

위의 코드에서, $active prop은 ContentTabItems 컴포넌트에만 전달되고 실제 DOM 요소에는 전달되지 않고, 이렇게하면 React 경고를 피할 수 있다.

