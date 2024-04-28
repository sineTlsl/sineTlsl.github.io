---
layout: post
title: "[jQuery] jQuery 개념 & 설치"
date: 2024-04-28 15:23:00 +900
lastmod: 2024-04-28 15:27:00 +900
categories: [Skill, jQuery]
tags: [jQuery]
use_math: true
image:
  path: https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/3f95da04-84cd-48d3-9d5a-0d7f48ed89d9
  width: 700
  alt: jQuery 로고
---

처음 자바스크립트를 배울 때는 jQuery로 시작했었는데, 요즘에는 React를 사용하다 보니 jQuery에 대한 기억이 희미하다 .. 🥺

당장 jQuery를 활용할 일이 있어서 기억을 되찾는 겸 복습을 하기 위해 글을 작성하게 되었다.

# jQuery란 무엇인가?

jQuery는 2006년 처음 소개된 자바스크립트 라이브러리로, 과거에는 인기가 가장 많았던 라이브러리지만, 현재는 사용자 유저가 감소하고 있는 추세다.

하지만, 아직도 많은 기업들은 jQuery를 사용하고 있어 단 기간 내에 마이그레이션 하거나 사라지기에는 어려움이 있다. 아직은 jQuery의 미래는 불투명한 것으로 보여지고 지켜봐야될 것 같다.

## 특징

- 버전이나 호환성의 문제를 해결하는 **'크로스 브라우징'**
- 간결하고 직관적인 문법으로 DOM 조작이 편리하다.
- 이벤트 핸들링이 용이하다.
- 단점으로는 바닐라 자바스크립트보다 속도가 느리다.

## 기본 문법

```javascript
$(선택자).액션(); // $(selector).action()
```

`$`는 제이쿼리를 의미하고, 제이쿼리에 선언하거나 접근할 때 사용한다. action에는 원하는 html 요소에 특정 이벤트를 실행할 수 있다.

## 사용 전 셋팅

jQuery 라이브러리를 사용하기 위해서는 [jQuery 공식 웹 사이트](https://jquery.com/)에서 다운로드를 하거나 CDN을 활용할 수 있다.

```html
// 1. 제이쿼리 다운로드
<script src="path/to/jquery-3.7.1.min.js"></script>

// 2. CDN 이용
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
```

또한 `npm`과 `yarn`을 사용하여 다운로드도 가능하다.

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/990e4544-aa30-40e7-9b09-59eb41931123" width="90%" />
</p>

<br><br>

**Reference**

[jQuery 공식 웹페이지](https://jquery.com/)

[jQuery 란, 사용하는 이유부터 특징, 기능까지 모두 알려드립니다.](https://www.elancer.co.kr/blog/view?seq=176)

[웹 개발의 필수, 자바스크립트 라이브러리 Top 5 및 그 이유](https://hileejaeho.cafe24.com/%EC%9B%B9-%EA%B0%9C%EB%B0%9C%EC%9D%98-%ED%95%84%EC%88%98-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC-top-5-%EB%B0%8F-%EA%B7%B8-%EC%9D%B4/)
