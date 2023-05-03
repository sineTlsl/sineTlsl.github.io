---
layout: post
title: "[캡틴판교 TS] 섹션 6. 타입 별칭"
date: 2023-05-03 20:48:00 +900
lastmod: 2023-05-03 20:48:00 +900
categories: [STUDY, Captain Pangyo - TS Basic]
tags: [captainpangyo, typescript]
image: 
  path: https://user-images.githubusercontent.com/97720335/233822587-60d294e1-867c-4cc0-b352-26899b803685.png
  width: 700
  alt: 타입스크립트 입문 - 기초부터 실전까지 강의 표지
---

# 타입 별칭이란?
`타입 별칭` 은 특정 타입이나 인터페이스를 참조할 수 있는 타입 변수를 의미한다.

```ts
// string 타입을 사용할 때
const name: string = 'capt';

// 타입 별칭을 사용할 때
type MyName = string;
const anme: MyName = 'capt';
```

**복잡한 타입 별칭**

간단한 타입 뿐만 아니라 `interface` 레벨의 복잡한 타입에도 별칭을 부여할 수 있다.

```ts
type Developer = {
  name: string;
  skill: string;  
}
```

<br>

## 타입 별칭 예제 코드
타입 별칭은 새로운 타입 값을 하나 생성하는 것이 아니라 정의한 타입에 대해 나중에 쉽게 참고할 수 있게 이름을 부여하는 것과 같다.

```ts
type MyString = string;
var str: MyString = 'hello';

type Todo = { id: string; title: string; done: boolean};

// 위에 있는 타입(Todo) 사용하기
function getTodo (todo: Todo) {
  ...
}
```
타입을 별칭으로 사용하면 좀 더 쉽게 타입을 지정할 수 있고, 코드의 가독성이 올라간다. 

<br>

## type vs interface
**VSCode 상의 프리뷰 상태로 다른 타입과 어떤 차이점이 있는지 확인해볼 수 있다.**

우선 `interface` 로 정의한다면, 다음과 같이 나온다.

```ts
interface Person2 {
  name: string;
  age: number;
}
```

<img src="https://user-images.githubusercontent.com/97720335/235867528-960a8885-2067-4556-b315-25b770007b6a.png" width="40%">


**위에 작성한 코드를 타입 별칭으로 정의한다면?** 

```ts
type Person2 = {
  name: string;
  age: number;
}
```

<img src="https://user-images.githubusercontent.com/97720335/235868187-51c9ea53-a178-4681-9a17-8e41824693f0.png" width="40%">

마우스가 focus가 되면, 각 타입을 확인할 수 있다.

### 가장 큰 차이점
- 타입 별칭과 인터페이스의 가장 큰 차이점은 타입의 확장 가능 / 불가능 여부다.
- `인터페이스` 는 확장이 가능하고, `타입 별칭` 은 확장이 불가능하다.

따라서, `type` 보다는 `interface` 로 선언해서 사용하는 것이 좋다.

<br>

## 추천 문서
- [인터페이스와 타입 별칭의 차이점 (공식 문서)](https://www.typescriptlang.org/docs/handbook/advanced-types.html#interfaces-vs-type-aliases)
- [인터페이스와 타입 별칭의 차이점 (미디엄 글)](https://medium.com/@martin_hotell/interface-vs-type-alias-in-typescript-2-7-2a8f1777af4c)
- [인터페이스와 타입 별칭의 차이점 (스택 오버 플로우 글)](https://stackoverflow.com/questions/41385059/possible-to-extend-types-in-typescript/41385149)

---

## 🧸 Feelings ...
타입 별칭보다는 인터페이스로 선언해서 사용하는 것이 좋다는 것만 기억하자..!

<div align="center"><img src="https://user-images.githubusercontent.com/97720335/235907007-c436a915-eef0-4ded-8be8-3198c4faaa45.png"></div>

<br>

**Reference**

[[캡틴판교 TS] 타입스크립트 입문 - 기초부터 실전까지](https://www.inflearn.com/course/%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%9E%85%EB%AC%B8) <br>
[타입스크립트 핸드북](https://joshua1988.github.io/ts/)

<br>

> 본 포스팅은 캡틴판교 강사님의 `타입스크립트 입문 - 기초부터 실전까지` 강의를 수강하고 난 후, 본인의 주관적인 견해에 의하여 작성되었습니다.
{: .prompt-info}