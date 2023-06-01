---
layout: post
title: "[S1-Unit04] CSS"
date: 2023-06-01 16:37:00 +900
lastmod: 2023-06-01 17:30:00 +900
categories: [CODESTATES, Section01]
tags: [CODESTATES, 코드스테이츠, Section01]
use_math: true
---

# CSS란?
> `CSS (Cascading Style Sheets)` 는 웹 페이지 스타일 및 레이아웃을 정의하는 스타일시트 언어다.
{: .prompt-info} 

단순한 정보를 전달을 하기 위한 사이트라면 [왼쪽](http://www.csszengarden.com/1/)도 괜찮지만, 좀 더 편안한 분위기, 정돈된 레이아웃, 문단 간격을 조정한 [오른쪽](http://www.csszengarden.com/214/)이 조금 더 보기 좋고, 가독성이 좋아보인다. 이 두 사이트는 똑같은 HTML 파일을 사용하지만, 전달력의 차이가 발생한다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/2cde71a3-ce6b-44ca-a277-465704f726e1" width="80%" />
</center>

이처럼 `CSS` 는 웹 사이트 사용자가 HTML 문서에 작성된 콘텐츠를 잘 이해할 수 있도록 돕는 역할을 한다. 개발자는 이 CSS를 활용하여 웹 애플리케이션에 접근할 수 있는 `사용자 인터페이스 (User Interface)` 부터 만들게 된다.

<br>

## 사용자 인터페이스 (UI: User Interface)
`인터페이스 (Interface)` 는 컴퓨터와 교류하기 위한 연결고리다. 버튼도 없고, 마우스도 없던 시대의 개발자는 자신이 만든 애플리케이션과 소통하기 위해 CLI를 사용했다. 키보드로 작성한 비밀 암호같은 코드를 적어서 엔터를 눌러야만 애플리케이션을 작동시킬 수 있었다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/5a3116da-39bb-4030-8388-75365a7aebaf" width="80%" />
</center>

현재는 트위터로 메시지를 보내려면 메시지를 키보드 인터페이스로 톡톡톡 입력하고, 마우스로 버튼 모양의 인터페이스를 누른다. 잘 만들어진 인터페이스 덕분에 사용자가 쉽게 사용할 수 있습니다. 인터페이스 앞에 "사용자"를 붙여 `사용자 인터페이스(UI)` 라고 부른다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/0b3e6479-5663-4426-98b5-dcead7c3d27c" width="80%" />
</center>

<br>

## 기본 셀렉터
### 전체 셀렉터

전체 셀렉터는 문서의 모든 요소를 선택한다.
```css
* { }
```

### 태그 셀렉터
태그 셀렉터는 같은 태그명을 가진 모든 요소를 선택한다. 복수로도 선택이 가능하다.
```css
h1 { }
div { }

section, h1 { }
```

### ID 셀렉터
ID 셀렉터는 `#id` 로 입력하여 선택한다.
```css
#only { }
```

### class 셀렉터
class 셀렉터는 `.class` 로 입력하여 선택한다. 같은 class를 가진 모든 요소를 선택한다.
```css
.widget { }
.center { }
```

### attribute 셀렉터
attribute 셀렉터는 같은 속성을 가진 요소를 선택한다. (모두 암기할 필요는 없다.)
```css
a[href] { }
p[id="only"] { }
p[class~="out"] { }
p[class|="out"] { }
section[id^="sect"] { }
div[class$="2"] { }
div[class*="w"] { }
```

<br>

## 자식 / 후손 / 형제 셀렉터
### 자식 셀렉터
자식 셀렉터는 첫 번째로 입력한 요소의 바로 아래 자식인 요소를 선택한다. 아래 예시의 경우 `<header>` 요소 바로 아래에 있는 두 개의 `<p>` 요소는 선택되지만, `<span>` 요소의 자식인 `<p>` 요소는 선택되지 않는다. (마찬가지로 후손 셀렉터와의 차이를 반드시 알고 있어야 한다.)

```css
header > p { }
```

예시)
```html
<header>
	<p> <!-- 선택 -->
		<span>
			<p></p>
		</span>
	</p>
	<p> <!-- 선택 -->
		<span>
			<p></p>
		</span>
	</p>
</header>
```

### 후손 셀렉터
후손 셀렉터는 첫 번재로 입력한 요소의 후손을 선택한다. 아래 예시의 경우 `<header>` 요소의 자식인 `<p>` 요소 뿐만 아니라, `<header>` 요소의 자식의 자식이 있는 `<p>` 요소까지 모두 선택된다. (자식 셀렉터와의 차이점을 반드시 알고 있어야 한다.)

```css
header p { }
```

예시)
```html
<header>
	<p><!-- 선택 -->
		<span>
			<p><!-- !!선택!! -->
			</p>
		</span>
	</p>
	<p><!-- 선택 -->
		<span>
			<p><!-- !!선택!! -->
			</p>
		</span>
	</p>
</header>
```

### 형제 셀렉터
형제 셀렉터는 같은 부모 요소를 공유하면서, 첫 번째 입력한 요소 뒤에 오는 두 번째 입력한 요소를 모두 선택해야 한다. 아래 예시의 경우 `<section>` 요소 뒤에 있는 세 개의 `<p>` 요소를 모두 선택한다.
```css
section ~ p { }
```

예시)
```html
<header>
	<section></section>
	<p></p> <!-- 선택 -->
	<p></p> <!-- 선택 -->
	<p></p> <!-- 선택 -->
</header>
```

### 인접 형제 셀렉터
인접 형제 셀렉터는 같은 부모 요소를 공유하면서, 첫 번째 입력한 요소 바로 뒤에 오는 두 번재 입력한 요소를 선택한다. 예시의 경우 `<section>` 요소 뒤에 있는 세 개의 `<p>` 요소 중 첫 번째 `<p>` 요소를 선택한다.
```css
section + p { }
```

예시)
```html
<header>
	<section></section>
	<p></p> <!-- 선택 -->
	<p></p> 
	<p></p> 
</header>
```

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)