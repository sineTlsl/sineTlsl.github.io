---
layout: post
title: "[S1-Unit04] CSS - 박스 모델 (Box Model)"
date: 2023-06-01 17:05:00 +900
lastmod: 2023-06-01 17:30:00 +900
categories: [CODESTATES, Section01]
tags: [CODESTATES, 코드스테이츠, Section01]
use_math: true
---

모든 콘텐츠는 각자의 영역을 가지며, 일반적으로 하나의 콘텐츠로 묶이는 요소들이 하나의 박스가 된다. 박스는 항상 직사각형이고, `너비(width)` 와 `높이(height)` 를 가진다. CSS를 이용해 속성과 값으로 그 크기를 설정한다. 

## block vs. inline, inline-block

박스의 종류는 줄 바꿈이 되는 박스와 줄 바꿈이 없이 옆으로 붙는 박스로 구분할 수 있다. 줄 바꿈이 되는 박스는 `block` 박스라 하고, 줌 바꿈이 일어나지 않으며 크기를 지정할 수 없는 박스는 `inline` 박스라고 부른다. 그리고 이 두 가지 박스 종류의 특징이 섞인, 줄 바꿈이 일어나지 않은 동시에 block 박스의 특징을 가지는 inline-block 박스도 있다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/5435131c-c41c-4989-b7c8-52e7b11d46b2" width="80%" />
</center>

<br>

## 박스를 구성하는 요소
CSS 박스 모델은 다음 그림만 기억하면 된다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/13627782-5cb5-4715-b824-6c5c8e9e9616" width="80%" />
</center>

### border (테두리)
`border` 는 심미적인 용도 외에도, 개발 과정에서도 매우 의미 있게 사용한다. 각 영역이 차지하는 크기를 파악하기 위해, 레이아웃을 만들면서 그 크기를 시각적으로 확인할 수 있도록 만든다. 

다음의 코드를 통해 테두리를 실선으로 확인할 수 있다.
```css
p {
	border: 1px solid red;
}
```

### margin (바깥 여백)
각각의 값은 top, right, bottom, left로 `시계방향` 이다.
```css
p {
	/*
    	margin-top: 10px;
  		margin-right: 20px;
  		margin-bottom: 10px;
  		margin-left: 20px;
    */
	margin: 10px 20px 10px 20px;  /* margin: 10px 20px; */
}
```

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/bcee025c-eac6-47f8-a9c7-469431a0d818" width="80%" />
</center>

### padding (안쪽 여백)

`padding` 은 border를 기준으로 박스 내부의 여백을 지정한다. 값의 순서에 따른 방향은 margin과 동일하다.

```css
p {
	/*
    	padding-top: 10px;
  		padding-right: 20px;
  		padding-bottom: 10px;
  		padding-left: 20px;
    */
	padding: 10px 20px 10px 20px;  /* padding: 10px 20px; */
}
```

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/23198443-a940-40cd-9086-d99dbfaf3f3a" width="80%" />
</center>

### 박스를 벗어나는 콘텐츠 처리
박스의 `height` 속성에 콘텐츠가 차지하는 공간보다 작은 값을 지정한다.
```css
p {
	height: 40px;
}
```

박스 크기보다 콘텐츠 크기가 더 큰 경우에는 콘텐츠가 박스 바깥으로 빠져나온다. 이렇게 콘텐츠가 박스를 뚫고 나가는 경우에는 박스 크기에 맞게 콘텐츠를 더 이상 표시하지 않거나, 혹은 박스 안에 스크롤을 추가하여 콘텐츠를 확인할 수 있게 만든다.

```css
p {
	height: 40px;
    overflow: auto; /* 콘텐츠가 넘치는 경우, 스크롤을 생성한다. */
}
```

<br>

### 박스 크기 측정 기준
박스 크기를 측정하는 기준은 중요하다.

[html 코드]
```html
<div id="container">
  <div id="inner">
    안쪽 box
  </div>
</div>
```

[css 코드]
```css
#container {
  width: 300px;
  padding: 10px;
  background-color: yellow;
  border: 2px solid red;
}

#inner {
  width: 100%;
  height: 200px;
  border: 2px solid green;
  background-color: lightgreen;
  padding: 30px;
}
```

id가 `container` 인 박스의 `width` 속성에 300px을 지정했다. 그러나 개발자 도구로 확인한 해당 요소의 width 값은 324px이다. 

![container 너비](https://velog.velcdn.com/images/tlsl13/post/5f2ce482-6f72-450e-a10b-55fc25f3048d/image.png)

- `#container` 의 너비는 300px이 아니라, **324px**이다. 브라우저는 다음과 같은 계산을 실행한다.
```
  300px (콘텐츠 영역)
+ 10px (padding-left)
+ 10px (padding-right)
+ 2px (border-left)
+ 2px (border-right)
```

- `#inner` 의 100%는 300px이 아니라 364px이다. 브라우저는 다음과 같은 계산을 실행한다.
```
  300px  (300px의 100%)
+ 30px (padding-left)
+ 30px (padding-right)
+ 2px (border-left)
+ 2px (border-right)
```

처음 레이아웃 디자인을 할 때 가장 많이하는 실수는 박스에 적용할 여백을 고려하지 않고 박스의 크기를 디자인하는 경우다. 박스의 크기를 디자인할 때 콘텐츠 영역만 고려하면, 개발 과정에서 처음 생각한 레이아웃을 벗어날 수 있다. 여백을 고려하지 않은 계산 방식은 레이아웃 디자인을 어렵게 만든다.

레이아웃 디자인을 조금 더 쉽게 하는 방법은 여백과 테두리 두께를 포함해서 박스 크기를 계산하게 만드는 것이다. 한 번 적용해보겠다. 	`*` 은 모든 요소를 선택하는 셀렉터이다. 모든 요소를 선택해 `box-sizing` 속성을 추가하고, `border-box` 라는 값을 추가한다.

```css
* {
	box-sizing: border-box;
}
```
이렇게 모든 요소에 `border-box` 를 적용하면, 모든 박스에서 여백과 테두리를 포함한 크기로 계산한다. 일반적으로 `box-sizing` 은 HTML 문서 전체에 적용한다. `box-sizing` 을 일부 요소에만 적용하는 경우, 혼란을 가중시킬 수 있다. **앞으로 레이아웃과 관련된 이야기를 할 때는 border-box 계산법을 기준으로 이야기 한다.**
- `content-box` 는 박스의 크기를 측정하는 기본 값이다. 그러나 대부분의 레이아웃 디자인에서 여백과 테두리를 포함하는 박스 크기 계산법은 `border-box` 를 권장한다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/de65d19f-5dc7-4114-827f-e4f88c74aca4" width="80%" />
</center>

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)