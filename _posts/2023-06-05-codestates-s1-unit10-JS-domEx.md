---
layout: post
title: "[S1-Unit10] JS/Browser - DOM 동적 실습"
date: 2023-06-05 14:32:00 +900
lastmod: 2023-06-05 14:32:00 +900
categories: [CODESTATES, Section01]
tags: [CODESTATES, 코드스테이츠, Section01]
use_math: true
image: 
  path: https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/10399d33-229e-4eb2-ab78-e7172ba06d32
  width: 866
  alt: DOM 동적 실습
---

`document` 객체에는 많은 속성과 메서드가 존재한다. 모든 속성과 메서드를 외우기에는 어려움이 있어, 제일 자주 사용하는 CRUD(Create, Update and Delete)를 제대로 이해하고 학습하는 것이 중요하다.

# DOM 실습
본격적으로 DOM 실습하기 전, 다음과 같은 `html` 과 `css` 코드를 적용하여 크롬 개발자 도구에서 작업을 진행한다.

```html
<!-- html 코드 -->
<!DOCTYPE html>
<html lang="ko">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <link rel="stylesheet" href="style.css" />
        <title>Document</title>
    </head>
    <body>
        <div id="container">
            <h2>Tweet List</h2>
            <div class="tweet">hello</div>
            <div class="tweet">world</div>
            <div class="tweet">code</div>
            <div class="tweet">states</div>
        </div>
    </body>
</html>
```

```css
/* css 코드 */
@import url("https://fonts.googleapis.com/css?family=Open+Sans&display=swap");

* {
    box-sizing: border-box;
}

body {
    background-color: #f9fafb;
    font-family: "Open Sans", sans-serif;
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    margin: 0;
}

.container {
    background-color: #fff;
    border-radius: 5px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
    width: 400px;
    padding: 30px 40px;
}

h2 {
    text-align: center;
    margin: 0 0 20px;
}

.tweet {
    margin-bottom: 10px;
    padding-bottom: 20px;
    position: relative;
    border: 2px solid #f0f0f0;
    border-radius: 4px;
    display: block;
    width: 100%;
    padding: 10px;
    font-size: 14px;
}
```

<br>

## CREATE
document 객체의 `createElement` 메서드를 이용하여 `<div>` 요소를 생성한다.

```jsx
document.createElement('div');
```

변수`tweetDiv` 를 생성하여 `<div>` 요소를 할당한다.

```jsx
const tweetDiv = document.createElement('div');
```

## APPEND
CREATE에서 만든 `tweetDiv` 변수를 `append` 변수를 사용하여 `<body>` 안에 포함시킨다.

```jsx
document.body.append(tweetDiv);
```

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/d5685808-3aa9-4da4-8a55-672d287780d1" width="80%" />
</center>

위 사진처럼 `<div>` 가 추가된 것을 확인할 수 있다.

## READ
JavaScript에서 값을 조회하기 위해서는 변수의 이름 아니면 배열은 index를 객체는 key를 이용하여 값을 조회할 수 있지만, DOM은 다른 방법을 사용해야 한다.

DOM으로 HTML 엘리먼트의 정보를 조회하기 위해서는 `querySelector` 의 첫 번재 인자로 셀렉터(selector)를 전달하여 확인 가능하다. 셀렉터로는 HTML 요소, id, class 이 세 가지가 가장 많이 사용된다. 참고로 `querySelector` 는 셀렉터를 조회한다는 의미를 가지고 있다.

### querySelector
`querySelector` 에 `.tweet` 을 첫 번째 인자로 넣으면, 클래스 이름이 `tweet` 인 HTML 엘리먼트 중 첫 번째 엘리먼트를 조회할 수 있다.

```jsx
const oneTweet = document.querySelector('.tweet');
```

### querySelectorAll
첫 번재 엘리먼트가 아닌, 여러 개의 요소를 한 번에 가져오기 위해서는 `querySelectorAll` 을 사용한다. 이렇게 조회한 HTML 요소들은 배열처럼 for문을 사용할 수 있다. 하지만, **이 요소들은 배열이 아니다.** 이런 '배열 아닌 배열'을 **유사 배열**, **배열형 객체** 등 다양한 이름으로 부른다. 

정식 명칭은 **Array-like Object**다.

클래스 이름이 `tweet` 인 모든 HTML 요소를 유사 배열로 받아온다.

```jsx
const tweets = document.querySelectorAll('.tweet');
```

`querySelector` 와 `querySelectorAll` 만 알아도 대부분의 요소를 조회할 수 있지만, `get` 으로 시작하는 DOM 조회 메서드를 볼 수도 있다. 이전 버전의 브라우저(인터넷 익스플로러) 호환성을 신경 써야 한다면, 다음과 같은 방식을 사용할 수도 있다. 실제 동작은 동일하다.

```jsx
const getOneTweet = document.getElementById('container');
const queryOneTweet = document.querySelector('#container');
console.log(getOneTweet === queryOneTweet);  // true
```

CREATE에서 생성한 div 요소를 `container` 의 맨 마지막 요소로 `tweetDiv` 를 추가한다.

```jsx
const container = document.querySelector('#container');
const tweetDiv = document.createElement('div');
container.append(tweetDiv);
```
그럼 다음 사진처럼 `<div>` 요소가 추가된 것을 확인할 수 있다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/1de6f304-1649-4d77-a5a3-5e234a6e3de5" width="80%" />
</center>

<br>

## UPDATE

우선 `oneDiv` 라는 이름의 `<div>` 요소를 생성한 다음,`<div>` 를 업데이트하여 작업을 진행할 수 있다.

```jsx
const oneDiv = document.createElement('div');
oneDiv.textContent = 'dev';  // div 엘리먼트에 문자열 입력
console.log(oneDiv);  // <div>dev</div>
```

CSS 스타일링이 적용될 수 있도록, div 엘리먼트에 `class` 를 추가한다.

```jsx
oneDiv.classList.add('tweet');
console.log(oneDiv);  // <div class="tweet">dev</div>
```

생성한 엘리먼트에 텍스트를 넣고, 클래스를 추가하여 스타일링 적용까지 하였다. 그 다음에는 append를 이용해 container의 자식 요소로 추가한다.

```jsx
const container = document.querySelector('#container');
container.append(oneDiv);
```

새롭게 추가한 엘리먼트는 클래스 `tweet` 의 스타일이 적용된 상태로 출력된다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/49581eea-7aa0-47e1-b248-534c2dac69af" width="80%" />
</center>

<br>

## DELETE
### remove

삭제하려는 요소의 위치를 알고 있을 경우에 사용하는 방법이다. 

id가 container인 요소 아래에`tweetDiv` 를 추가하고, `remove` 로 삭제한다.

```jsx
const container = document.querySelector('#container');
const tweetDiv = document.createElement('div');
container.append(tweetDiv);
tweetDiv.remove();
```

### innerHTML
여러 개의 자식 요소를 지우려할 때, `innerHTML` 을 이용하면, 아주 간단하게 모든 자식 요소를 지울 수 있다. container의 모든 자식 요소를 지우려고 할 때, 다음과 같이 입력한다.

```jsx
document.querySelector('#container').innerHTML = '';
```

`innerHTML` 을 이용하는 방법은 간편하고 편리한 방식이지만, [보안에서 몇 가지 문제점](https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML#security_considerations)을 가지고 있다. 그래서 **다른 메서드를 이용하는 것을 권장한다.** 바로 `removeChild` 메소드다.

### removeChild
`removeChild` 는 자식 요소를 지정해서 삭제하는 메서드다. 모든 자식 요소를 삭제하기 위해, 반복문(while, for, etc.)을 활용할 수 있다.

다음 코드는 자식 요소가 남아있지 않을 때 까지, 첫 번째 자식 요소를 삭제하는 코드다.

```jsx
const container = document.querySelector('#container');
while (container.firstChild) {
	container.removeChild(container.firstChild);
}
```
`container` 의 모든 자식 요소가 지워진 것을 확인할 수 있다.

![removeChild](https://velog.velcdn.com/images/tlsl13/post/fbd26774-84c8-46c3-b456-f5f803bb3297/image.png)

`removeChild` 와 `while` 을 이용해 자식 요소를 삭제하면, 제목에 해당하는 h2 "Tweet List" 까지 삭제된다. 

제목까지 삭제되는 것을 방지하기 위해선 여러 방법이 있다.
- 자식 요소가 담고 있는 문자열을 비교해 "Tweet List"만 남기는 방법
- "Tweet List" 자식 요소 하나만 남을 때까지, 마지막 요소를 제거하는 방법
- 새로운 변수를 생성하고 "Tweet List"를 할당해뒀다가 반복이 끝난 뒤에 새롭게 추가하는 방법
- 클래스 이름이 `tweet` 인 요소만 찾아서 지우는 방법

**1. 자식 요소가 담고 있는 문자열을 비교해 "Tweet List"만 남기는 방법**

```jsx
const container = document.querySelector('#container');
const childrens = container.children;

while (childrens.length > 1) {
  for (let child of childrens) {
    if (child.textContent !== 'Tweet List') {
      container.removeChild(child);
    } 
  }
}
```

**2. "Tweet List" 자식 요소 하나만 남을 때까지, 마지막 요소를 제거하는 방법**

```jsx
const container = document.querySelector('#container');
while (container.children.length > 1) {
	container.removeChild(container.lastChild);
}
```

**3. 새로운 변수를 생성하고 "Tweet List"를 할당해뒀다가 반복이 끝난 뒤에 새롭게 추가하는 방법**

```jsx
const container = document.querySelector('#container');
const tweet = container.children[0];

while (container.firstChild) {
	container.removeChild(container.firstChild);
}

container.append(tweet);
```

**4. 클래스 이름이 tweet인 요소만 찾아서 지우는 방법**

```jsx
const tweets = document.querySelectorAll('.tweet');
tweets.forEach(function(tweet) {
	tweet.remove();
})
/* or
for (let tweet of tweets) {
	tweet.remove()
}
*/
```

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)

[JavaScript가 뭔가요?](https://developer.mozilla.org/ko/docs/Learn/JavaScript/First_steps/What_is_JavaScript)