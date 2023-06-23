---
layout: post
title: "[S3-Unit02] UI/IX - UI 디자인"
date: 2023-06-23 16:49:00 +900
lastmod: 2023-06-23 16:49:00 +900
categories: [CODESTATES, Section03]
tags: [CODESTATES, 코드스테이츠, Section03]
use_math: true
image: 
  path: https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/e4d44fa4-a4ed-4b1b-84b1-579785269e72
  width: 1200
  alt: UI 디자인
---

UI를 디자인할 때 필요한 개념인 UI 디자인 패턴과 UI 레이아웃 구성법을 알고있어야 한다.

**UI 디자인 패턴**은 화면에 배치할 수 있는 자주 쓰이는 컴포넌트를 말하고, **UI 레이아웃 구성법**은 이 컴포넌트들을 화면에 어떻게 배치할 것인지를 정하는 방법론이다.

## UI 디자인 패턴

>`UI 디자인 패턴` 은 프로그래밍 시 자주 반복되어 나타나는 문제점을 해결하고자, 과거의 다른 사람이 해결한 결과물을 재사용하기 좋은 형태로 만든 패턴을 말한다. 쉽게 말하자면 **UI 컴포넌트** 라고 할 수 있다.

자주 쓰이는 UI 디자인 패턴을 익혀두면 UI를 디자인하기 쉬워지고, 개발자들과 디자이너, PM과의 의사소통이 원할해져 협업 효율이 높아진다.

## 자주 사용되는 UI 요소

### 1. Modal (모달)
Modal은 기존에 있던 화면 위에 오버레이 되는 창을 뜻한다. 

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/7165e737-b487-467a-b29f-463c9155511e" width="90%" />
</center>

- 닫기 버튼, 혹은 모달 범위 밖을 클릭하면 모달이 닫기 전에는 기존 화면과 상호작용할 수 없다.
- 새로운 브라우저 페이지를 여는 팝업창과 구분되는 개념이다.
- 팝업은 브라우저에 의해 강제로 막힐 수 있지만, 모달은 브라우저 설정에 영향을 받지 않아 꼭 보여주고 싶은 내용이 있다면 모달을 사용하는 것이 좋다.

### 2. Toggle (토글)
Toggle은 On/Off를 설정하는 방식처럼 켜고 끌 수 있는 스위치를 의미한다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/51ea821a-72e8-49a6-a8c0-c9eb0a88396d" width="90%" />
</center>

색상, 스위치의 위치 등의 시각적인 효과를 주어 사용자가 직관적으로 파악할 수 있게 해야한다.

<br>

### 3. Tab (탭)
Tab은 콘텐츠를 분리해서 보여주고 싶을 때 사용한다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/49f501e0-d29f-4d2e-a1ca-6eb77519a791" width="90%" />
</center>

<br>

### 4. Tag (태그)
Tag는 콘텐츠를 설명하는 키워드를 사용하여 라벨을 붙이는 역할을 한다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/139542c2-070a-445c-9928-c9af47bcfac6" width="90%" />
</center>

<br>

### 5. Autocomplete (자동완성)
Autocomplete는 사용자가 내용을 입력 중일 때 사용자가 입력하고자 하는 내용과 일치할 가능성이 높은 항목을 보여주는 것을 의미한다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/d3acd9b6-7fc2-493e-9be7-bd3c800fa5fb" width="90%" />
</center>

- 자동 완성 항목 개수를 제한하는 것이 좋다.
- 키보드 방향키나 클릭 등으로 접근할 수 있도록 설정해야 한다.

<br>

### 6. Accordion (아코디언)
Accordion은 접었다 폈다 할 수 있는 컴포넌트로 사용자가 섹션을 펼쳐 컨텐츠를 확인하고, 필요하지 않으면 축소할 수 있는 인터페이스다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/c71e7840-4e4e-47ce-b1c8-11f917364532" width="90%" />
</center>

<br>

### 7. Carousel (캐러셀)
Carousel은 이미지나 카드와 같은 콘텐츠를 회전목마처럼 돌아가면서 콘텐츠를 표시해주는 인터페이스다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/cc8e9e05-508c-4f0f-b4f6-e5bbd778146d" width="90%" />
</center>

<br>

### 8. Pagination (페이지네이션)
Pagination은 한 페이지에 띄우기엔 정보가 너무 많을 경우에, 책처럼 번호를 붙여 페이지를 구분해주는 인터페이스다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/622265cc-a008-4442-8bd8-06c9cf8cef4c" width="90%" />
</center>

<br>

### 9. Infinite Scroll, Continuous Scroll (무한 스크롤)
Infinite Scroll과 Continuous Scroll은 같은 말이며 둘 다 무한으로 스크롤을 내릴 수 있는 것을 의미한다. 

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/d77ec07b-143c-4363-8f0d-3afe4097eab3" width="90%" />
</center>

<br>

### 10. GNB (Global Navigation Bar), LNB (Local Navigation Bar)
`GNB(Global Navigation Bar)` 는 어느 페이지에 들어가든 사용할 수 있는 최상위 메뉴를 의미하고, `LNB(Local Navigation Bar)` 는 GNB에 종속되는 서브 메뉴 혹은 특정 페이지에서만 볼 수 있는 메뉴를 뜻한다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/a7dd80bf-7b52-4b34-99e4-e7a6008cc843" width="90%" />
</center>

위 예시에서는 탭 형식으로 최상단에 위치한 메뉴가 GNB, 마우스를 올렸을 때 드롭다운 형식으로 내려오는 서브 메뉴가 LNB다.

- GNB는 어느 페이지에 있든 바로바로 사용할 수 있도록 항상 동일한 위치에 있어야 한다.
- GNB가 있다 없다 한다거나 위치가 자꾸 변하면 사용자 경험에 악영향을 줄 수 있다.

<br>

## UI 레이아웃
> `레이아웃` 은 테스트와 이미지 정보, 기능적 요소 등 여러 가지 구성 요소를 시각적, 기능적 계획에 맞춰 특정한 공간에 효과적으로 배치하는 것을 의미한다.

- 정보를 효율적으로 명확하게 제공하기 위한 위함이다.
- 레이아웃의 기본조건인 주목성, 가독성, 명쾌성, 조형성, 창조성을 만족해야한다.

UI 레이아웃을 구성하는 방법인 그리드 시스템을 사용할 수 있다.

## 그리드 시스템 (Grid System)
`그리드(grid)` 는 수직, 수평으로 분할된 격자무늬를 뜻하며, 말 그대로 화면을 격자로 나눈 다음 그 격자에 맞춰 콘텐츠를 배치하는 방법이다.

웹 디자인 분야에서는 화면을 세로로 몇 개의 영역으로 나눌 것인가에 초점을 맞춘 **컬럼 그리드 시스템(Column Grid System)**을 사용하며, Column, Gutter, Margin라는 세 가지 요소로 구성된다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/c29c1bed-81d0-4224-81be-3ff8cb2d9044" width="90%" />
</center>

### 1. Column
Column은 콘텐츠가 위치하게 될 세로로 나누어진 영역이다. 

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/318e6917-e07a-4b9e-bfd2-2602c6cf8594" width="90%" />
</center>

- 컬럼 개수를 임의로 나눌 수도 있지만, 표준적으로 휴대폰에서 4개, 태블릿에서 8개, PC에서는 12개의 컬럼으로 나눈다.
- 이미지 속 화면 크기의 구분선을 `break point` 라고 하며, 내가 만들고자 하는 UI가 어디에 속하는 지 파악하고 컬럼 개수를 지정해야 한다.

- 기기 마다 화면의 크기가 조금씩 다르고 브라우저의 크기를 사용자 마음대로 조정할 수 있어, Column은 상대 단위를 사용하여 콘텐츠가 창 크기에 맞춰서 크기가 변하도록 설정하는 것이 좋다.

### 2. Gutter
Gutter는 Column 사이의 공간으로, 콘텐츠를 구분하는데 도움을 준다. 

Gutter의 간격이 좁을수록 콘텐츠들이 연관성 있어 보이고, 넓을수록 각 콘텐츠가 독립적인 느낌을 줄 수 있어 이 간격을 잘 정해야한다. 주의할 점은 **Gutter는 아무리 넓어도 컬럼 너비보다는 작게 설정해야한다**는 것이다.

### 3. Margin
Margin은 화면 양쪽의 여백을 의미한다.

너비를 `px` 같은 절대 단위를 사용해서 고정 값으로 사용해도 되지만, `vw`, `%` 같은 상대 단위를 사용하여 유동성을 주는 것이 좋다.

<br>

## 컬럼 그리드 시스템 예시
**네이버** 

네이버에서도 컬럼 그리드 시스템을 사용한다. 화면이 12개의 컬럼으로 나누어져 있고 컬럼에 맞춰서 콘텐츠가 배열되어 있음을 알 수 있다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/f43ac117-d8e1-48d7-ab02-578fad925124" width="90%" />
</center>

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)

[ui-patterns.com](https://ui-patterns.com/patterns)

[UI 디자이너를 위한 32가지 사용자 인터페이스 요소](https://careerfoundry.com/en/blog/ui-design/ui-element-glossary/)

[m2.material.io](https://m2.material.io/design/layout/responsive-layout-grid.html#columns-gutters-and-margins)

