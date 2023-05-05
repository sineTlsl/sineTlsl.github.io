---
layout: post
title: "[캡틴판교 TS] 섹션 10. 제네릭"
date: 2023-05-06 00:05:00 +900
lastmod: 2023-05-06 00:05:00 +900
categories: [STUDY, Captain Pangyo - TS Basic]
tags: [captainpangyo, typescript]
image: 
  path: https://user-images.githubusercontent.com/97720335/233822587-60d294e1-867c-4cc0-b352-26899b803685.png
  width: 700
  alt: 타입스크립트 입문 - 기초부터 실전까지 강의 표지
---

# 제네릭(Generics) 이란?
`제네릭` 은 C#, Java 등의 언어에서 재사용성이 높은 컴포넌트를 만들 때 자주 활용되는 특징이다.

- 특히, 한 가지 타입보다 여러 가지 타입에서 동작하는 컴포넌트를 생성하는데 사용된다.

**즉, 제네릭이란 타입을 마치 함수의 파라미터처럼 사용하는 것을 의미한다.**

## 제네릭 예시
다음은 제네릭을 사용하기 전 코드다. 현재 타입은 `any` 라고 볼 수 있다.

```ts
function getText(text) {
  return text;
}
```

위 함수는 `text` 라는 매개변수를 받아 `text` 를 반환해준다. `hi`, `10`, `true` 등 어떤 값이 들어가더라도 그대로 반환한다.

```ts
getText('hi'); // 'hi'
getText(10); // 10
getText(true); // true
```

### ‼️ 여기서 제네릭 기본 문법을 적용 시키면?
```ts
function getText<T>(text: T): T {
  return text;
}
```

함수를 호출할 때 다음과 같이 함수 안에서 사용할 타입을 넘겨줄 수 있다.
```ts
getText<string>("hi");
getText<number>(10);
getText<boolean>(true);
```

위 코드 중 `getText<string>('hi')` 를 호출했을 때 제네릭 타입은 `<T>`에서 `<string>` 으로 변환된다.

- 그 이유는 `getText()` 함수를 호출할 때 제네릭(함수에서 사용할 타입) 값으로 `string` 을 넘겼기 때문이다.

`getText` 함수는 아래와 같이 타입을 정의한 것과 같다.
```ts
function getText<string>(test: string): string {
  return text;
}
```

위 함수는 입력 값의 타입이 `string` 이면서 반환 값 타입도 `string` 이어야 한다.

<br>

## 기존 타입 정의 방식과 제네릭의 차이점
기존 타입 정의 방식에는 2가지의 문제점이 있다. 

### 1. 중복 함수 선언
```ts
function logText(text: string) {
  console.log(text);

  return text;
}

function logNumber(num: number) {
  console.log(num);

  return num;
}

logText("Hi");
logNumber(10);
```

동일한 작업을 하는 함수를 여러 개 생성할 경우, 불필요한 반복을 하게 된다.

### 2. 유니온 타입 함수 선언
```ts
function logText(text: string | number) {
  console.log(text); 
  
  return text;
}
logText('a');
logText(10);
```

유니온 타입으로 함수를 선언할 경우에 `string` 과 `number` 속성이 둘 다 뜨기 때문에, 타입을 추론하기 어렵다.

저 위에 있는 코드들을 `제너릭` 으로 바꿔보면 다음과 같다.
```ts
function logText<T>(text: T): T {
  console.log(text);

  return text;
}

logText<number>(10);
logText<string>("hi");
```

<br>

## 제너릭 활용 예제
제네릭을 사용하기 전 코드는 다음과 같다.

```ts
const emails = [
  { value: 'naver.com', selected: true },
  { value: 'gmail.com', selected: false },
  { value: 'hanmail.net', selected: false },
];

const numberOfProducts = [
  { value: 1, selected: true },
  { value: 2, selected: false },
  { value: 3, selected: false },
];

function createDropdownItem(item) {
  const option = document.createElement('option');
  option.value = item.value.toString();
  option.innerText = item.value.toString();
  option.selected = item.selected;
  return option;
}

// NOTE: 이메일 드롭 다운 아이템 추가
emails.forEach(function (email) {
  const item = createDropdownItem(email);
  const selectTag = document.querySelector('#email-dropdown');
  selectTag.appendChild(item);
});
```

제네릭을 사용한 코드다.
```ts
interface DropdownItem<T> {
  value: T;
  selected: boolean;
}

const emails: DropdownItem<string> [] = [
  { value: 'naver.com', selected: true },
  { value: 'gmail.com', selected: false },
  { value: 'hanmail.net', selected: false },
];

const numberOfProducts: DropdownItem<number>[] = [
  { value: 1, selected: true },
  { value: 2, selected: false },
  { value: 3, selected: false },
];

// 제네릭으로 받을 수 있는 타입을 string과 number로 제한한다.
function createDropdownItem<T extends string | number>(item: DropdownItem<T>): HTMLOptionElement {
  const option = document.createElement('option');
  option.value = item.value.toString();
  option.innerText = item.value.toString();
  option.selected = item.selected;

  return option;
}

// NOTE: 이메일 드롭 다운 아이템 추가
emails.forEach(function (email) {
  const item = createDropdownItem<string>(email);
  const selectTag = document.querySelector('#email-dropdown');
  selectTag?.appendChild(item);
});
```

<br>

## 제네릭의 타입 제한
- 반환값에 T를 안해도 T의 타입이 나온다는 것을 알 수 있지만, 써주는 것이 명확하다.
- T 뒤에 []을 넣으면 배열로 들어온다는 것을 알 수 있다.

**[예제 1]**
```ts
function logTextLength<T>(text: T[]): T[] {
  text.forEach(function (text) {
    console.log(text);
  })
  return text;
}
logTextLength<string>(['hi', 'abc']);
```

**[예제 2]**

제네릭의 타입은 항상 lengthType 하위 타입일 것이다.

```ts
function logTextLength<T extends lengthType>(text: T): T {
  text.length;

  return text;
}
logTextLength('a');
logTextLength(10); // 숫자 10은 포함할 수 없다. 이유는 숫자는 length 속성을 사용할 수 없기 때문!
logTextLength({ length: 10 });
```

**[에제 3] keyof**
- `keyof` : 제네릭 타입의 범위를 줄인다.
- ShoppingItem에 있는 key 속성 중 하나만 들어갈 수 있다.

```ts
function getShoppingItemoption<T extends keyof ShoppingItem>(itemOptiion: T): T {
  return itemOptiion;
}
getShoppingItemoption("name")
```

---

## 🧸 Feelings ...
제네릭은 타입스크립트의 필수다!!!!! 다른 자료도 더 찾아보자!!!!

<div align="center"><img src="https://user-images.githubusercontent.com/97720335/236495673-5485ff58-ec77-41bd-acc0-f245ec0e40a0.png"></div>

<br>

**Reference**

[[캡틴판교 TS] 타입스크립트 입문 - 기초부터 실전까지](https://www.inflearn.com/course/%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%9E%85%EB%AC%B8) <br>
[타입스크립트 핸드북](https://joshua1988.github.io/ts/)

<br>

> 본 포스팅은 캡틴판교 강사님의 `타입스크립트 입문 - 기초부터 실전까지` 강의를 수강하고 난 후, 본인의 주관적인 견해에 의하여 작성되었습니다.
{: .prompt-info}