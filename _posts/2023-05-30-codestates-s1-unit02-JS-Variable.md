---
layout: post
title: "[S1-Unit02] JavaScript 기초 - 변수(Variable)"
date: 2023-05-30 22:15:00 +900
lastmod: 2023-05-30 22:15:00 +900
categories: [CODESTATES]
tags: [CODESTATES, 코드스테이츠, Section01]
use_math: true
image: 
  path: https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/e18393d7-0bb8-439a-a30d-842ba1fff12f
  width: 700
  alt: 코드스테이츠 합격 사진
---

# 변수(Variable) 란?

> `변수(Variable)` 는 하나의 값을 저장할 수 있는 저장공간이다.
{: .prompt-info} 

## 1. 변수의 개요

사전에 **커피**란 `끓여서 마실 수 있도록 볶아 놓은 커피나무 열매의 씨앗, 또는 그것을 빻은 분말 상태의 물질로 그 씨를 끓이거나 분말을 뜨거운 물에 타서 만든 짙은 갈색 음료` 를 의미한다.

하지만 이 커피를 말할 때마다 이 정의를 모두 말하는 사람은 없다. **커피**라는 이름으로 부르기로 약속이 되어 있기 때문이다. 그래서 카페에서 커피를 주문할 때, '커피 열매의 씨앗을 볶은 뒤 갈아서 물에 타서 만든 짙은 갈색 음료를 주세요.'라고 하지 않아도 된다. '커피 주세요.'라고 말해도 커뮤니케이션이 가능하다.

이처럼 모든 사물에는 이름이 있다. JavaScript에서도 데이터를 편하게 다루기 위해 데이터에 이름을 붙일 수 있다. 그 이름을 바로 **변수** 라고 부른다.

<br>

## 2. 변수의 선언과 할당

변수를 선언할 때는 `let` 키워드를 기본적으로 사용한다. `let` 키워드 뒤에 선언하고자 하는 변수명을 입력한다.

```js
let name;
```

선언된 변수에 값을 할당할 때에는 할당 연산자(`=`)를 사용한다.
```js
name = 'kimcoing';
```

변수의 선언과 값의 할당을 동시에 할 수도 있다.
```js
let name = 'kimcoing';
```

변수에는 JavaScript에서 사용이 가능한 모든 타입의 값을 할당할 수 있다.
```js
let string = '원주율';
let number = 3.141592;
let boolean = true;
let array = [1, 'two', false];
let object = {name: 'kimcoding', age: 25, course: 'SEB FE'};
let empty = null;
let notDefined = undefined;
```

### 아무것도 할당하지 않은 변수

아무것도 할당되지 않은 변수는 `undefined` 가 자동으로 할당된다. 이는 **초기화**라는 JavaScript의 독특한 특징이다.

```js
let variable;
console.log(variable);  // undefined
```

### 값의 재할당

`let` 키워드로 선언한 변수에 새로운 값을 할당할 수 있다. 이를 **재할당**이라고 한다. 재할당에도 할당연산자(`=`)를 사용한다.

```js
let name = 'kimcoding';
console.log(name);  // 'kimcoding'
name = 'parkhacker';
console.log(name);  // 'parkhacker'
```

### 재할당이 불가능한 변수(상수)

`let` 키워드가 아닌 `const` 키워드를 사용하면 재할당이 금지된다.

```js
const name = 'kimcoding';
console.log(name);  // 'kimcoding'
name = 'parkhacker';  // Uncaught TypeError: Assignment to constant variable.
```

### var 키워드

`var` 키워드는 `let` 키워드와 `const` 키워드가 등장하기 이전에 사용하던 변수 선원 키워드이다. `var` 키워드에는 여러 단점이 존재하고, 이를 보완하기 위해 `let` 키워드와 `const` 키워드가 등장하였다. 따라서 `var` 키워드는 사용을 되도록 지양하고, `let` 키워드와 `const` 를 사용할 것을 권장한다. 

재할당이 필요한 변수에는 `let` 키워드를, 재할당이 불필요하거나 변경되는 것을 방지해야 하는 변수는 `const` 키워드를 사용해야 한다.

```js
var name = 'kimcoding'; // var키워드가 가지고 있는 단점으로 인해 사용을 지양하는 것이 좋다.
```

### 네이밍 규칙
변수명은 다음과 같은 네이밍 규칙을 준수해야 한다.

- 식별자는 특수문자를 제외한 문자, 숫자, 언더스코어(`_`), 달러 기호(`$`)를 포함할 수 있다.
```js
let name, $head, _score;  // 사용 가능한 변수명
```

- 단, 식별자는 특수문자를 제외한 문자, 숫자, 언더스토어(`_`), 달러 기호(`$`)로 시작해야 한다. **숫자로 시작하는 것은 허용하지 않는다.**
```js
let 1st;  // 사용할 수 없는 변수명
```

- 예약어는 식별자로 사용할 수 없다.
  - **예약어**: 프로그래밍 언어에서 사용되고 있거나 사용될 예정인 단어
    ex) let, const, false, typeof 등
  ```js
  let true;  // 사용할 수 없는 변수명
  ```

- 그외 규칙들
  - 변수명은 변수의 존재 목적을 이애할 수 있도록 의미를 명확히 표현해야 한다.
  ```js
  // 변수의 존재 목적을 이해할 수 없는 변수명
  let x = 100;
  let y = 5;

  // 변수의 존재 목적을 명확히 알 수 있는 변수명
  let name = 'kimcoding';
  let age = 25;
  ```

### 네이밍 컨벤션
하나 이상의 영어단어를 사용하여 식별자를 만들 경우, 네이밍 컨벤션을 잘 지키면 가독성을 높일 수 있다. JavaScript에서는 일반적으로 **카멜 케이스(CamelCase)**를 사용한다. `카멜 케이스` 는 낙타의 등모양에서 유래된 이름으로써, 첫 단어의 첫 문자는 소문자로, 그 이후에 연결되는 단어의 첫 문자는 대문자로 작성하는 방법이다.

```js
// 🐪카멜 케이스(camelCase)
let firstName = 'coding'; 
let lastName = 'kim';

// 그밖에 네이밍 컨벤션
let first_name;   // 🐍스네이크 케이스(snake_case) : 단어와 단어 사이에 언더스코어(_)를 사용
let FirstName;   // 📐파스칼 케이스(PascalCase) : 단어의 시작을 대문자로 작성
```

<br>

## 3. 변수를 활용한 연산

변수에 숫자 타입의 값이 할당되어 있는 경우 숫자 타입에 사용 가능한 모든 연산이 가능하다.

```js
let number = 10;
console.log(number + 2);  // 12
console.log(number - 5);  // 5
console.log(number * 3);  // 30
console.log(number / 2);  // 5
console.log(number % 3);  // 1
console.log(number);  // 10
```

그러나 각각의 연산은 독립적으로 이뤄질 뿐, number는 그대로 10이 할당되어 있다. 연산의 결과를 변수에 반영하려면 **재할당**을 해야한다.

```js
let number = 10;
number = number + 2;
console.log(number);  // 12

number = number * 3;
console.log(number);  // 36
```

변수끼리의 연산도 가능하다. 

### 템플릿 리터럴 (Template Literal)

백틱을 사용하는 방법을 **템플릿 러터럴**이라고 한다. `템플릿 리터럴` 은 큰 따옴표, 작은 따옴표를 사용한 표기 방법과는 다른 기능을 가지고 있다. 특히, **문자열 내부에 변수 삽입할 수 있는 기능**은 매우 유용하게 사용되므로 반드시 알아두어야 한다.

템플릿 리터럴 내부에 `${}` 를 사용하여 변수를 삽입할 수 있다. 이때, 문자열이 할당되지 않은 변수도 문자열로 취급된다.

```js
let course = 'SEB FE';
let cohort = 99;
let name = 'kimcoding';

console.log(`${course} ${cohort} ${name}`);  // 'SEB FE 43 kimcoding'
```

단어와 단어 사이에 공백을 삽입하기 위해 `‘ ‘` 를 사용하는 것보다 템플릿 리터럴을 사용하는 것이 가독성 측면에서 훨씬 우수하다.

```js
let course = 'SEB FE';
let cohort = 43;
let name = 'kimcoding';

console.log(course + ' ' + cohort + ' ' + name); // 'SEB FE 43 kimcoding'
```
<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)