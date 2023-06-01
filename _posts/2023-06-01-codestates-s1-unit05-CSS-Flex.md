---
layout: post
title: "[S1-Unit05] CSS - Flex"
date: 2023-06-01 17:20:00 +900
lastmod: 2023-06-01 17:20:00 +900
categories: [CODESTATES]
tags: [CODESTATES, 코드스테이츠, Section01]
use_math: true
---

# Flex(Flexible)
> `Flex(Flexible)` 는 "잘 구부러지는, 유연한" 이라는 뜻이다.
{: .prompt-info} 

Flexbox로 레이아웃을 구성한다는 것은, 박스를 유연하게 늘리거나 줄여 레이아웃을 잡는 방법이다.


## 1. display: flex 분석하기

`display: flex` 는 부모 박스 요소에 적용해, **자식** 박스의 방향과 크기를 결정하는 레이아웃 구성 방법이다.

우선 HTML로 3개의 `<div>` 요소를 자식으로 가진 `<main>` 요소를 작성한다.

```html
<main>
  <div>box1</div>
  <div>box2</div>
  <div>box3</div>
</main>
```

그리고 각 요소들이 눈에 잘 보이도록 CSS로 `<main>` 요소에는 빨간색 점선, `<div>` 요소들에는 초록색 실선으로 테두리를 설정해주고, 전체적으로 `margin` 과 `padding` 도 10픽셀씩 준다.

```css
main {
  border: 1px dotted red;
}

div {
  border: 1px solid green;
}

* {
  margin: 10px;
  padding: 10px;
}
```

그러면 다음과 같은 화면이 나오는 것을 확인할 수 있다. 이처럼 `<div>` 요소들은 별다른 설정을 해주지 않으면 위쪽에서부터 세로로 정렬되며, 가로로 넓게 공간을 차지하는 것을 확인할 수 있다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/b831bf70-02bc-4bbf-875b-c1ea2de1d11c" width="80%" />
</center>

이 상태에서 `<main>` 요소에 `display: flex` 속성을 적용하면, `<div>` 요소들이 왼쪽부터 가로로 정렬된 것과 내용만큼의 공간을 차지하는 것을 확인할 수 있다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/7b9a9907-d315-440c-9018-f4c2a04dccec" width="80%" />
</center>

이처럼 Flexbox 속성들을 활용하면 요소의 **정렬**, 요소가 **차지하는 공간**을 설정할 수 있다.

<br>

## 2. 부모 요소에 적용해야하는 Flexbox 속성들
### flex-direction: 정렬 축 정하기
`flex-direction` 속성은 부모 요소에 설정해주는 속성으로, 자식 요소들을 정렬할 정렬 축을 정한다. 아무 설정도 해주지 않으면 **기본적으로 가로 정렬**을 한다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/1f03130d-2704-4ae0-8944-52a0403edf19" width="80%" />
</center>

### flex-wrap: 줄 바꿈 설정하기
`flex-wrap` 속성은 하위 요소들의 크기가 상위 요소의 크기를 넘으면 자동 줄 바꿈을 할 것인지 정한다. 설정해주지 않으면 **줄 바꿈을 하지 않는다.**

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/f646d78d-947d-44ea-93e5-9cf313e29a90" width="80%" />
</center>

### justify-content: 축 수평 방향 정렬
`justify-content` 속성은 자식 요소들을 축의 수평 방향으로 어떻게 정렬할 것인지 정한다. 요소들이 가로로 정렬되어 있다면 가로 방향으로 어떻게 정렬할 것인지, 세로로 정렬되어 있다면 세로 방향으론 어떻게 정렬할 것인지 정하는 속성이다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/e23c57a3-116b-4a04-bfdd-677712d5b67f" width="80%" />
</center>

주요 속성값으로는 `flex-start`, `flex-end`, `center`, `space-between`, `space-around` 이 있습니다. 각 속성값의 특성이 잘 드러날 수 있도록 자식 요소의 크기를 동일하게 설정해놓았다.

`flex-direction: row` **인 경우**

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/87b2ed66-63b0-4b0c-b3d3-e1bac3fde3cf" width="80%" />
</center>

`flex-direction: column` **인 경우**

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/00788396-bdad-4e38-8af0-d10125a880b1" width="80%" />
</center>

<br>

### align-items: 축 수직 방향 정렬
`align-items` 속성은 자식 요소들을 축의 수직 방향으로 어떻게 정렬할 것인지 정한다. 요소들이 가로로 정렬되어 있다면 세로 방향으로 어떻게 정렬할 것인지, 세로로 정렬되어 있다면 가로 방향으론 어떻게 정렬할 것인지 정하는 속성이다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/e8c95de1-fd59-4861-92b7-e96bf0a4bb3e" width="80%" />
</center>

주요 속성값으로는 `stretch`, `flex-start`, `flex-end`, `center`, `baseline` 이 있다. 이번에는 각 속성값의 특징이 명확하게 드러날 수 있도록 자식 요소의 글씨 크기를 각각 다르게 설정해놓았다.

`flex-direction: row` **인 경우**

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/9e95889e-2471-4fb5-b1a6-9c834372e38d" width="80%" />
</center>

`flex-direction: column` **인 경우**

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/88c271bf-aef7-4227-a6df-64587fe2d243" width="80%" />
</center>

<br>

## 3. 자식 요소에 적용해야 하는 Flexbox 속성
`flex` 속성에는 세 가지 값을 지정해줄 수 있다. 각 값이 의미하는 것은 다음과 같다.

```css
flex:   <grow(팽창 지수)>    <shrink(수축 지수)>    <basis(기본 크기)>
```

`grow(팽창 지수)` 는 요소의 크기가 늘어나야 할 때 얼마나 늘어날 것인지,`shrink(수축 지수)`는 요소의 크기가 줄어들어야 할 때 얼마나 줄어들 것인지, `basis(기본 크기)` 는 늘어나고 줄어드는 것과 상관없이 요소의 기본 크기는 얼마인지를 의미한다.

자식 요소에 `flex` 속성을 따라 설정해주지 않으면 다음과 같은 **기본값**이 적용되며, 왼쪽에서부터 오른쪽으로 콘텐츠의 크기만큼 배치된다.

```css
flex: 0 1 auto;  /* flex: grow shrink basis */
```

꼭 `flex` 속성 안에 세 가지 값을 한 번에 설정해줄 필요 없이, 다음과 가티 각 값을 따로 지정해줄 수 있다.

```css
flex-grow: 0;
flex-shrink: 1;
flex-basis: auto;
```

### grow
`grow(팽창 지수)` 는 요소의 크기가 늘어나야 할 때 **얼마나 늘어날 것인지**를 의미한다고 했다. 

```html
<main>
  <div id="box1" class="box">box1</div>
  <div id="box2" class="box">box2</div>
  <div id="box3" class="box">box3</div>
</main>
```

### shrink
`shrink(수축 지수)` 는 grow와 반대로, 설정한 비율만큼 박스 크기가 작아진다. 비율이 클수록 더 많이 줄어든다. 그러나 `flex-grow` 속성과 `flex-shrink` 속성을 함께 사용하는 일을 추천하지 않는다. 

비율로 레이아웃을 지정할 경우 `flex-grow` 속성 또는 `flex: <grow> 1 auto` 와 같이 `grow` 속성에 변화를 주는 방식을 권장한다. `flex-shrink` 속성은 `width` 나 `flex-basis` 속성에 따른 비율이므로 실제 크기를 에측하기가 어렵기 때문이다. 

`flex-grow` **속성으로 비율을 변경하는 경우,** `flex-shrink` **속성은 기본값인 1로 두어도 무방하다.**

### basis
`basis(기본 크기)` 는 자식 박스가 `flex-grow` 나 `flex-shrink` 에 의해 늘어나거나 줄어들기 전에 가지는 기본 크기다. `flex-grow` 가 0일 때, `basis` 크기를 지정하면 그 크기는 유지된다.

`grow` 는 0 : 1 : 1로 설정하고, box1에 `flex-basis: 50px` 로 설정했을 때, box1의 크기는 늘어나거나 줄어들지 않고 50px을 유지하는 것을 확인할 수 있다.

<br>

## 참고
- `width` 와 `flex-basis` 를 동시에 적용하는 경우, `flex-basis` 가 우선된다.
- 콘텐츠가 많아 자식 박스가 넘치는 경우, `width` 가 정확한 크기를 보장하지 않는다.
- (`flex-basis` 를 사용하지 않는다면) 콘텐츠가 많아 자식 박스가 넘치는 경우를 대비해 `width` 대신 `max-width` 를 사용할 수 있다.

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)