---
layout: post
title: "[캡틴판교 TS] 섹션 12. 타입 추론"
date: 2023-05-06 15:45:00 +900
lastmod: 2023-05-07 01:01:00 +900
categories: [STUDY, Captain Pangyo - TS Basic]
tags: [captainpangyo, typescript]
image: 
  path: https://user-images.githubusercontent.com/97720335/233822587-60d294e1-867c-4cc0-b352-26899b803685.png
  width: 700
  alt: 타입스크립트 입문 - 기초부터 실전까지 강의 표지
---

# 타입 추론(Type Inference) 이란?
`타입 추론` 은 타입스크립트가 코드를 해석해 나가는 동작을 의미한다.

## 타입 추론의 기본
```ts
let a = "abc";
```
위에 `a` 는 `string` 으로 간주된다. 이렇게 변수를 선언하거나 초기화할 때 타입이 추론된다. <br>
이외에도 변수, 속성, 인자의 기본 값, 함수의 반환 값 등을 설정할 대 타입 추론이 일어난다.

## 가장 적절한 타입 (Best Common Type)
타입은 보통 몇 개의 표현식(코드)을 바탕으로 타입을 추론한다. <br>
이 표현식을 이용하여 가장 근접한 타입을 추론하게 되는데, 이 가장 근접한 타입을 **[Best Common Type](https://www.typescriptlang.org/docs/handbook/type-inference.html)** 이라고 한다.

```ts
let arr = [1, "a", true];
```

이 배열은 `number`, `string`, `boolean` 으로 구분되는데, Best Common Type 알고리즘으로 다른 타입글과 가장 잘 호환되는 타입을 선정한다.

### 추가적인 공부
- [문맥을 이용한 타입 추론 방식](https://joshua1988.github.io/ts/guide/type-inference.html#%EA%B0%80%EC%9E%A5-%EC%A0%81%EC%A0%88%ED%95%9C-%ED%83%80%EC%9E%85-best-common-type)

<br>

## Typescript Language Server
VSCode에는 타입스크립트를 지원하는 Language Server가 탑재되어 있다.

- [VSCode 타입스크립트 소개 문서](https://code.visualstudio.com/docs/languages/typescript#_code-suggestions)
- [VSCode Language Server Extension 가이드](https://code.visualstudio.com/api/language-extensions/language-server-extension-guide)
- [Language Server 소개 사이트](https://langserver.org/)
- [Language Server Protocol 개요](https://learn.microsoft.com/ko-kr/visualstudio/extensibility/language-server-protocol?view=vs-2019)

---

## 🧸 Feelings ...
Language Server가 돌아가고 있다는 것만 알고있자 

<div align="center"><img src="https://user-images.githubusercontent.com/97720335/236607833-c3b67bbc-bddf-4520-b951-aab057019510.png"></div>

<br>

**Reference**

[[캡틴판교 TS] 타입스크립트 입문 - 기초부터 실전까지](https://www.inflearn.com/course/%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%9E%85%EB%AC%B8) <br>
[타입스크립트 핸드북](https://joshua1988.github.io/ts/)

<br>

> 본 포스팅은 캡틴판교 강사님의 `타입스크립트 입문 - 기초부터 실전까지` 강의를 수강하고 난 후, 본인의 주관적인 견해에 의하여 작성되었습니다.
{: .prompt-info}