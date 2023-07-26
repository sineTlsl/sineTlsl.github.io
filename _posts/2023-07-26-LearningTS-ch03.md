---
layout: post
title: "[LearningTS] Chapter 03. 유니언과 리터럴 "
date: 2023-07-26 16:05:00 +900
lastmod: 2023-07-26 16:05:00 +900
categories: [STUDY, Learning TypeScript]
tags: [typescript]
use_math: true
image: 
  path: https://github.com/sineTlsl/sineTlsl/assets/97720335/a367fb26-a4e4-44d1-b2e0-18f617ce2101
  width: 400
  alt: 러닝 타입스크립트 교재
---

# CHAPTER 03. 유니언과 리터럴

```
상수를 제외한 모든 것은 변합니다.
시간이 지나면서 값도 변할 수 있습니다.
```

타입스크립트가 해당 값을 바탕으로 추론을 수행하는 **두 가지 핵심 개념**
- `유니언(union)` : 값에 허용된 타입을 두 개 이상의 가능한 타입으로 확장하는 것
- `내로잉(narrowing)` : 값에 허용된 타입이 하나 이상의 가능한 타입이 되지 않도록 좁히는 것

<br>

## 🌓 유니언 타입
- 유니언 타입은 OR 연산자와 같이 `이거 혹은 저거` 와 같은 타입이다.
- 정확히 어떤 타입인지 모르지만 두 개 이상의 옵션 중 하나라는 것을 알고 있는 경우에 코드를 처리하는 개념이다.
- 가능한 값 또는 구성 요소 사이에 `|(수직선)` 연산자를 사용해 유니언 타입을 나타낼 수 있다.

```ts
let mathematician = Math.random() > 0.5 
  ? undefined
  : "Mark Goldberg";
```

위 함수는 `string | undefined` 타입으로 간주된다.

<br>

### 1. 유니언 타입 선언
- 변수의 초깃값이 있더라도 변수에 명시적 타입 애너테이션을 제공하는 것이 유용할 때 유니언 타입을 사용한다.

**[예제]** <br> 
thinker의 초깃값은 `null`이지만 잠재적으로 `null` 대신 `string`이 될 수 있음을 알려준다.

```ts
let thinker: string | null = null;

if (Math.randon() > 0.5) {
  thinker = "Susanne Langer"; // Ok
}
```

- 명시적으로 `string | undefined` 타입 애너테이션은 타입스크립트가 thinker의 값으로 `string` 타입의 값을 할당할 수 있음을 의미한다.

유니언 타입 선언은 타입 애너테이션으로 타입을 정의하는 모든 곳에서 사용할 수 있다.

> 🌿 유니언 타입 순서는 중요하지 않다.
타입스크립트에서는 `boolean | number` 나  `number | boolean` 모두 똑같이 취급된다.

### 2. 유니언 속성
- 값이 유니언 타입일 때 타입스크립트는 유니언으로 선언한 모든 가능한 타입에 존재하는 멤버 속성에만 접근할 수 있다.
- 유니언 외의 타입에 접근하려고 하면 타입 검사 오류가 발생한다.
- 모든 유니언 타입에 존재하지 않는 속성에 대한 접근을 제한하는 것은 안전 조치에 해당한다.
- 객체에 어떤 속성을 포함한 타입으로 확실하게 알려지지 않은 경우, 타입스크립트는 해당 속성을 사용하려고 시도하는 것이 안전하지 않다고 여긴다. 그런 속성이 존재하지 않을 수도 있기 때문이다.

유니언 타입으로 정의된 여러 타입 중 하나의 타입으로 된 값의 속성을 사용하려면 코드에서 값이 보다 구체적인 타입 중 하나라는 것을 타입스크립트에 알려야 한다. 이 과정을 `내로잉` 이라고 한다.

<br>

## 🌓 내로잉
- 내로잉은 값의 정의, 선언 혹은 이전에 유추된 것보다 더 구체적인 타입임을 코드에서 유추하는 것이다.
- 타입을 좁히는 데 사용할 수 있는 논리적 검사를 `타입 가드` 라고 한다.

### 1. 값 할당을 통한 내로잉
- 변수에 값을 직접 할당하면 타입스크립트는 변수의 타입을 할당된 값의 타입으로 좁힌다.

**[예제 1]** <br>
admiral 변수는 초기에 `number | string`으로 선언했지만 “Grace Hopper” 값이 할당된 이후 타입스크립트는 admiral 변수가 `string` 타입이라는 것을 알게 된다.

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl/assets/97720335/48fb9340-412f-4297-b1f1-8ab6b90c1c7e" width="70%" />
</p>

- 변수에 유니언 타입 애너테이션이 명시되고 초깃값이 주어질 때 값 할당 내로잉이 작동된다.
- 타입스크립트는 변수가 나중에 유니언 타입으로 선언된 타입 중 하나의 값을 받을 수 있지만, 처음에는 초기에 할당된 값의 타입으로 시작한다는 것을 이해한다.

**[예제 2]** <br>
inventor는 `number | string` 타입으로 선언되었지만 초깃값으로 문자열이 할당되었기 때문에 타입스크립트는 즉시 `string` 타입으로 바로 좁혀졌다는 것을 알고있다.

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl/assets/97720335/b8ee4788-2c2b-49da-97b3-1da624dd1d21" width="70%" />
</p>

<br>

### 2. 조건 검사를 통한 내로잉
- 일반적으로 타입스크립트에서는 변수가 알려진 값과 같은지 확인하는 if 문을 통해 변수의 값을 좁히는 방법을 사용한다.
- 타입스크립트는 if 문 내에서 변수가 알려진 값과 동일한 타입인지 확인한다.

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl/assets/97720335/3195d1e1-b8d4-47d0-801d-1743c29c2dc2" width="70%" />
</p>

- 조건부 로직으로 내로잉할 때, 타입스크립트 타입 검사 로직은 훌륭한 자바스크립트 코딩 패턴을 미러링에 구현한다.
- 만약 변수가 여러 타입 중 하나라면, 일반적으로 필요한 타입과 관련된 검사를 원할 것이다.

### 3. typeof 검사를 통한 내로잉
- 타입스크립트는 직접 값을 확인해 타입을 좁히기도 하지만, `typeof` 연산자를 사용할 수도 있다.

**[예제]** <br>
scientist 예제와 유사하게 다음 if 문에서 typeof researcher가 `string`인지 확인해 타입스크립트에 researcher의 타입이 `string`임을 나타낸다.

```ts
let researcher = Math.random() > 0.5 
  ? "Rosalind Franklin"
  : 51;

  if (typeof researcher === "string") {
    researcher.toUpperCase(); // Ok: string
  }
```

`!`을 사용한 논리적 부정과 else 문도 잘 작동한다.
```ts
if (!(typeof researcher === "string")) {
  researcher.toFixed(); // Ok: string
} else {
  researcher.toUpperCase(); // Ok: string
}
```

이러한 코드 스니펫은 타입 내로잉에서도 지원되는 `삼항 연산자`를 이용해 다시 작성할 수 있다.
```ts
!(typeof researcher === "string")
  ? researcher.toFixed(); // Ok: string
  : researcher.toUpperCase(); // Ok: string
```

<br>

## 🌓 리터럴 타입
- 리터럴 타입은 좀 더 구체적인 버전의 원시의 타입이다.

다음 philosopher는 string 타입이다.

```ts
const philosopher = "Hypatia";
```

- philosopher는 단지 string 타입이 아닌 “Hypatia”라는 특별한 값이다.
- 따라서 변수 philosopher의 타입은 기술적으로 더 구체적인 “Hypatia” 이다.
- 이것이 바로 **리터럴 타입**의 개념이며, 원시 타입 값 중 어떤 것이 아닌 **특정 원시값**으로 알려진 타입이다.
- 원시 타입 `string` 은 존재할 수 있는 모든 가능한 문자열의  집합을 나타낸다.
- 하지만 리터럴 타입인 “Hypatia”는 하나의 문자열만 나타낸다.

변수를 `const` 로 선언하고 직접 리터럴 값을 할당하면 타입스크립트는 해당 변수를 할당된 리터럴 값으로 유추한다.
- 초기 리터럴 값이 할당된 const 변수 위에 마우스를 가져가면 일반적인 원시 타입 대신 해당 리터럴이 표시된다.

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl/assets/97720335/d3113e60-b1d6-42a4-8499-fc41208fd3f9" width="40%" />
</p>

- 각 원시 타입은 해당 타입이 가질 수 있는 가능한 모든 리터럴 값의 전체 조합으로 생각할 수 있다.
- **즉, 원시 타입은 해당 타입의 가능한 모든 리터럴의 값의 집합이다.**

boolean, null, undfiend 타입 외에 number, string과 같은 모든 원시 타입에는 무한한 수의 리터럴 타입이 있다. 일반적인 타입스크립트 코드에서 발견할 수 있는 타입은 다음과 같다.

- `boolean` : true | false
- `null과 undefined` : 둘 다 자기 자신, 즉 오직 하나의 리터럴 값만 가짐
- `number` : 0 | 1 | 2 … | 0.1 | 0.2 | …
- `string` : “” | “a” | “c” | … | “aa” | “ab” | “ac” | …


유니언 타입 애너테이션은 리터럴과 원시 타입을 섞어서 사용할 수 있다.

**[예제]** <br>
lifespan은 number 타입이거나 선언된 “ongoing” 혹은 “uncertain” 값 중 하나로 나타낼 수 있다.

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl/assets/97720335/44d79f54-789a-4842-a2d8-fa0f34707c61" width="80%" />
</p>

<br>

### 리터럴 할당 가능성
- number와 string과 같은 서로 다른 원시 타입이 서로 할당되지 못하는 것처럼 0과 1처럼 동일한 원시 타입일지라도 서로 다른 리터럴 타입은 서로 할당할 수 없다.

**[예제]** <br>
specificallyAda는 리터럴 타입 “Ada” 로 선언했으므로 값에 “Ada”을 할당할 수 있지만, “Byron” 이나 string 타입 값은 할당할 수 없다.

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl/assets/97720335/9db701be-b9ef-4640-a1f8-68bd2cc9ba10" width="60%" />
  <img src="https://github.com/sineTlsl/sineTlsl/assets/97720335/cb7a2b1b-b5b9-4829-9311-f10b1ebf7090" width="60%" />
</p>

- 그러나 리터럴 타입은 그 값이 해당하는 원시에 할당할 수 있다.
- 모든 특정 리터럴 문자열은 여전히 string 타입이기 때문이다.

다음 타입 `:)`의 값 `:)` 는 앞서 string 타입으로 간주된 someString 변수에 할당한다.
```ts
someString = ":)";
```

<br>

## 🌓 엄격한 null 검사
- 리터럴로 좁혀진 유니언의 힘은 타입스크립트에서 `엄격한 null 검사` 라 부르는 타입 시스템 영역인 **‘잠재적으로 정의되지 않은 undefined 값’** 으로 작업할 때 특히 두드러진다.
- 타입스크립트는 두려운 **‘십억 달러의 실수’** 를 바로잡기 위해 엄격한 null 검사를 이용하며 이는 최신 프로그래밍 언어의 큰 변화 중 하나다.

### 1. 십억 달러의 실수
- ‘십억 달러의 실수’는 다른 타입이 필요한 위치에서 null 값을 사용하도록 허용하는 많은 타입 시스템을 가리키는 업계 용어다.
- 엄격한 null 검사가 없는 언어에서는 다음 예제 코드처럼 string 타입 변수에 null을 할당하는 것이 허용된다.
  ```ts
  const firstName: string = null;
  ```

타입스크립트의 가장 유용한 옵션 중 하나인 strictNullChecks는 엄격한 null 검사를 활성화할지 여부를 결정한다.
- 간략하게 설명하면, strictNullChecks를 비활성화하면 코드의 모든 타입에 `| null | undefined` 를 추가해야 모든 변수가 null 또는 undefined를 할당할 수 있다.
- strictNullChecks 옵션을 false로 설정하면 다음 코드의 타입은 완벽히 안전하다고 간주되지만 틀린 부분이다.

nameMaybe 변수가 `.toLowerCase`에 접근할 때 `undefined`가 되는 것은 잘못된 것이다.
- 엄격한 null 검사가 활성화되면, 타입스크립트는 다음 코드에서 발생하게 될 잠재적인 충돌을 확인한다.

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl/assets/97720335/59b7bc82-0590-4562-8af5-e8f1024ef22b" width="50%" />
</p>

- 엄격한 null 검사가 활성화해야만, 코드가 `null` 또는 `undefined` 값으로 인한 오류로부터 안전한지 여부를 쉽게 파악할 수 있다.
- 타입스크립트의 모범 사례는 일반적으로 엄격한 `null` 검사를 활성화하는 것이다.
- 그렇게 해야만 충돌을 방지하고 십억 달러의 실수를 제거할 수 있다.

<br>

### 2. 참 검사를 통한 내로잉
- 자바스크립트에서 `false`, `0`, `-0`, `0n`, `""`, `null`, `undefined`, `NaN` 처럼 `falsy`로 정의된 값을 제외한 모든 값은 모두 참이다.
- 타입스크립트는 잠재적인 값 중 truthy로 확인된 일부에 한해서만 변수의 타입을 좁힐 수 있다.

**[예제]** <br>
geneticist는 `string | undefined` 타입이며, `undefined`는 falsy이므로 타입스크립트는 if 문의 코드 블록에서는 geneticist가 string 타입이 되어야 한다고 추론할 수 있다

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl/assets/97720335/4f34c35c-47ab-432f-b549-8271f0af4efe" width="50%" />
</p>

논리 연산자는 `&&` 와 `?` 는 참 여부를 검사하는 일도 잘 수행한다. 
- 하지만 참 여부 확인 외에 다른 기능은 제공하지 않는다.
- `string | undefined` 값에 대해 알고 있는 것이 falsy라면, 그것이 빈 문자열인지 undefined인지 알 수 없다.

```ts
geneticist && geneticist.toUpperCase(); // OK: string | undefined
geneticist?.toUpperCase(); // Ok: string | undefined
```

다음 코드에서는 biologist는 `false | string` 타입이고, if 문에서는 `string`으로 좁힐 수 있지만, else 문에서는 biologist가 빈 문자열인 경우에는 여전히 `string`이 될 수 있음을 알 수 있다.

```ts
let biologist = Math.random() > 0.5 && "Racher Carson";

if (biologist) {
  biologist; // 타입: string
} else {
  biologist; // 타입: fale | string
}
```

<br>

### 3. 초깃값이 없는 변수
- 자바스크립트에서 초깃값이 없는 변수는 기본적으로 undefined가 된다.
- 이는 타입 시스템에서 극단적인 경우를 나타내기도 한다.

값이 할당되기 전에 속성 중 하나에 접근하려는 것처럼 해당 변수를 사용하려고 시도하면 다음과 같은 오류 메시지가 나타난다.

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl/assets/97720335/b8d66385-c726-4483-84e4-b63dcb0fb0e6" width="60%" />
</p>

- 변수 타입에 `undefined`가 포함되어 있는 경우에는 오류가 보고되지 않는다.
- 변수 타입에 `| undefined` 를 추가하면, `undefined` 는 유효한 타입이기 때문에 사용 전에는 정의할 필요가 없음을 타입스크립트에 나타낸다.

이전 코드에서 mathematician의 타입이 `string | undefined` 이면 어떤 오류도 발생하지 않는다.

```ts
let mathematician: string | undefined;

mathematician?.length;

mathematician = "Mark Goldberg";
mathematician.length;
```

<br>

## 🌓 타입 별칭
다음 각 변수는 5개의 가능한 타입 중 하나가 될 수 있다.

```ts
let rawDataFirst: boolean | number | string | null | undefined;
let rawDataSecond: boolean | number | string | null | undefined;
let rawDataThird: boolean | number | string | null | undefined;
```

타입스크립트에서는 재사용하는 타입에 더 쉬운 이름을 할당하는 `타입 별칭` 이 있다.
- 타입 별칭은 `type 새로운 이름 = 타입` 형태를 갖는다.
- 편의상 타입 별칭은 파스칼 케이스로 이름을 지정한다.
  ```ts
  type MyName = ...;
  ```
- 타입 별칭은 타입 시스템의 ‘복사해서 붙여넣기’처럼 작동한다.
- 타입스크립트가 타입 별칭을 발견하면 해당 별칭이 참조하는 실제 타입을 입력한 것처럼 작동한다.

유니언 타입을 타입 별칭을 사용해 다음과 같이 작성할 수 있다.

```ts
type RawData = boolean | number | string | null | undefined;

let rawDataFirst: RawData;
let rawDataSecond: RawData;
let rawDataThird: RawData;
```

이러한 타입 별칭은 타입이 복잡해질 때마다 사용할 수 있는 편리한 기능이다.

<br>

### 1. 타입 별칭은 자바스크립트가 아니다.
- 타입 별칭은 타입 에너테이션처럼 자바스크립트로 컴파일되지 않는다.
- 순전히 타입스크립트 타입 시스템에만 존재한다.

따라서 앞서 다룬 코드도 다음 자바스크립트로 컴파일된다.

```js
let rawDataFirst;
let rawDataSecond;
let rawDataThird;
```

타입 별칭은 순전히 타입 시스템에만 존재하므로 런타임 코드에서는 참조할 수 없다.
- 타입스크립트는 런타임에 존재하지 않는 항목에 접근하려고 하면 타입 오류로 알려준다.

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl/assets/97720335/5be8daad-f5a7-4769-910a-20975715cf6f" width="80%" />
</p>

타입 별칭은 순전히 ‘개발 시’에만 존재한다.

### 2. 타입 별칭 결합
- 타입 별칭은 다른 타입 별칭을 참조할 수 있다.
- 유니언 타입인 타입 별칭 내에 또 다른 유니언 타입인 타입 별칭을 포함하고 있다면 다른 타입 별칭을 참조하는 것이 유용하다.

IdMaybe 타입은 undefined와 null, 그리고 Id 내의 타입을 포함한 유니언 타입이다.

```ts
type Id = number | string;

// IdMaybe 타입은 다음과 같음: number | string | undefined | null;
type IdMaybe = Id | undefined | null;
```

- 사용 순서대로 타입 별칭을 선언할 필요는 없다.
- 파일 내에서 타입 별칭을 먼저 선언하고 참조할 타입 별칭을 나중에 선언해도 된다.

따라서 이전 코드와 다르게 IdMaybe가 Id 앞에 오도록 작성할 수 있다.

```ts
type IdMaybe = Id | undefined | null; // Ok
type Id = number | string;
```

<br>

**Reference**

러닝 타입스크립트 (Learning TypeScript)
