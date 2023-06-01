---
layout: post
title: "[S1-Unit03] HTML - 기본 구조와 문법"
date: 2023-06-01 16:34:00 +900
lastmod: 2023-06-01 16:34:00 +900
categories: [CODESTATES]
tags: [CODESTATES, 코드스테이츠, Section01]
use_math: true
---

# HTML이란?
> `HTML (Hyper Text Markup Language)` 은 웹 페이지의 틀을 만드는 마크업 언어다.
{: .prompt-info} 

## How to use HTML?
- HTML은 태그(tag)들의 집합
- `Tag` : 부등호(<>)로 묶인 HTML의 기본 구성 요소

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Page title</title>
  </head>
  <body>
    <h1>Hello world!</h1>
    <div>Contents here
      <span>Here too!</span>
    </div>
  </body>
</html>
```

태그 내부에 내용이 없다면, (`<tag></tag>` 와 같이 표현되는 경우) `<tag />` 와 같이 표현 가능

```html
<img src="codestates-logo.png"></img>

<img src="codestates-logo.png" />
```

<br>

## Most used tags in HTML
- `<div>` : Divison
- `<span>` : Span
- `<img>` : Image
- `<a>` : Link
- `<ul>&<li>` : Unoredred List & List Item
- `<input>` : Input (Text, Radio, Checkbox)
- `<textarea>` : Multi-line Text Input
- `<button>` : Button

### div VS span

`div` 태그는 한 줄을 차지하고, `span` 태그는 컨텐츠 크기만큼 공간을 차지한다.

```html
<div>div 태그는 한 줄을 차지한다.</div>
<div>division 2</div>
<span>span 태그는 컨텐츠 크기만큼 공간을 차지한다.</span>
<span>span 2</span>
<span>span 3</span>
<div>division 3</div>
```

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/ae871b3d-fe4f-4484-87e4-97e0bf1798f9" width="80%" />
</center>

### img: 이미지 삽입

```html
<img src="/라푼젤.jpeg" />
```

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/1733b9f2-ec70-49bf-a45a-83c7c1df78dd" width="80%" />
</center>

### a: 링크 삽입

```html
<a href="https://codestates.com" target="_blank">코드스테이츠</a>
```

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/479145d9-7684-4816-8e7f-54aacaa5a64a" width="80%" />
</center>

### ul, li: 목록 입력

```html
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
  <li>
    Item 3 3 has nested list
    <ul>
      <li>Item 3-1</li>
    </ul>
  </li>
</ul>
```

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/46ed3d53-629b-4055-8793-86924542adae" width="80%" />
</center>


### input, textarea: 다양한 입력 폼

```html
<input type="text" placeholder="type-here" />
<div>
  <input type="radio" name="choice" value="a" /> a
  <input type="radio" name="choice" value="b" /> b
</div>
<textarea></textarea>
<div>
  <input type="checkbox" checked /> checked
  <input type="checkbox" /> unchecked
</div>
```

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/ef418b80-8dec-4ef6-9e1c-458ef4fbbbf1" width="80%" />
</center>

### button: 버튼

```html
<button>Submit</button>
```

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/ad480542-362a-4e72-8acb-ed5b17660aff" width="80%" />
</center>

<br>

## 아이디, 비밀번호 입력 창 예제 (뼈대만)

```html
<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>아이디, 비밀번호 입력 창 만들기</title>
  </head>
  <body>
    <input type="text" placeholder="ID" />
    <input type="password" placeholder="password" />
    <button>Login</button>
    <label> <input type="checkbox" />Keep Login </label>
  </body>
</html>
```

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/a99ba46d-70df-4a56-a17f-94c79b1bfdaa" width="80%" />
</center>

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)