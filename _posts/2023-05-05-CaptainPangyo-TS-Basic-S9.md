---
layout: post
title: "[캡틴판교 TS] 섹션 9. 클래스"
date: 2023-05-05 14:54:00 +900
lastmod: 2023-05-05 14:54:00 +900
categories: [STUDY, Captain Pangyo - TS Basic]
tags: [captainpangyo, typescript]
image: 
  path: https://user-images.githubusercontent.com/97720335/233822587-60d294e1-867c-4cc0-b352-26899b803685.png
  width: 700
  alt: 타입스크립트 입문 - 기초부터 실전까지 강의 표지
---

# 클래스(Class) 란?
ES6에서 새롭게 도입되었다. 

## 프토로타입과 클래스 관계
다음과 같이 `method` 와 `class` 로 선언한 부분은 동일한 내용이다.

```js
// method
function Person(name, age) {
  this.name = name;
  this.age = age;
}
let capt = new Person("캡틴", 100);
```

```js
class Person {
  // 클래스 로직
  constructor(name, age) {
    console.log("생성 되었습니다");
    this.name = name;
    this.age = age;
  }
}

let seho = new Person("세호", 30); // 생성 되었습니다
console.log(seho); // Person { name: '세호', age: 30 }
```

<br>

# TypeScript Class
## readonly
클래스 속성에서 `readonly` 키워드를 사용하면 값을 변경할 수는 없고, 읽을 수만 있다.
```ts
class Developer {
    readonly name: string;
    constructor(theName: string) {
        this.name = theName;
    }
}

let john = new Developer("John");
john.name = "John"; // error! name is readonly.
```

이처럼 `readonly` 를 사용하면 `constructor()` 함수에 초기 값 설정 로직을 넣어줘야 하므로 다음과 같이 인자에 `readonly` 키워드를 추가해서 코드를 줄일 수 있다.

```ts
class Developer {
  readonly name: string;
  constructor(readonly name: string) {
  }
}
```

<br>

## Accessor
타입스크립트는 객체의 특정 속성의 접근과 할당에 대해 제어할 수 있다.

```ts
class Developer {
  name: string;
}

const josh = new Developer();
josh.name = 'Josh Bolton';
```

여기서 만약 `name` 속성에 제약 사항을 추가하고 싶다면 아래와 같이 `get` 과 `set` 을 활용한다.

```ts
class Developer {
  private name: string;
  
  get name(): string {
    return this.name;
  }

  set name(newValue: string) {
    if (newValue && newValue.length > 5) {
      throw new Error('이름이 너무 깁니다');
    }
    this.name = newValue;
  }
}
const josh = new Developer();
josh.name = 'Josh Bolton'; // Error
josh.name = 'Josh';
```

`get` 만 선언하고 `set` 을 선언하지 않는 경우에는 자동으로 `readonly` 로 인식된다.

<br>

## Abstract Class
추상 클래스(Abstract Class)는 인터페이스와 비슷한 역할을 하면서도 조금 다른 특징을 갖고 있다.
- 추상 클래스는 특정 클래스의 상속 대상이 되는 클래스이며 좀 더 상위 레벨에서 속성, 메서드의 모양을 정의한다.

```ts
abstract class Developer {
  abstract coding(): void; // 'abstract'가 붙으면 상속 받은 클래스에서 무조건 구현해야 함
  drink(): void {
    console.log('drink sth');
  }
}

class FrontEndDeveloper extends Developer {
  coding(): void {
    // Developer 클래스를 상속 받은 클래스에서 무조건 정의해야 하는 메서드
    console.log('develop web');
  }
  design(): void {
    console.log('design web');
  }
}
const dev = new Developer(); // error: cannot create an instance of an abstract class
const josh = new FrontEndDeveloper();
josh.coding(); // develop web
josh.drink(); // drink sth
josh.design(); // design web
```

---

## 🧸 Feelings ...
클래스는 최상위에 타입을 정의하고 변수에도 타입을 지정해야 한다! 총 2번!! 기억하기

<div align="center"><img src="https://user-images.githubusercontent.com/97720335/236386023-4ef3f64b-9ec6-4a5c-a523-498333f58277.png"></div>

<br>

**Reference**

[[캡틴판교 TS] 타입스크립트 입문 - 기초부터 실전까지](https://www.inflearn.com/course/%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%9E%85%EB%AC%B8) <br>
[타입스크립트 핸드북](https://joshua1988.github.io/ts/)

<br>

> 본 포스팅은 캡틴판교 강사님의 `타입스크립트 입문 - 기초부터 실전까지` 강의를 수강하고 난 후, 본인의 주관적인 견해에 의하여 작성되었습니다.
{: .prompt-info}