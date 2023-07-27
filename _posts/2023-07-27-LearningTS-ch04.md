---
layout: post
title: "[LearningTS] Chapter04. 객체"
date: 2023-07-27 13:21:00 +900
lastmod: 2023-07-27 13:21:00 +900
categories: [STUDY, Learning TypeScript]
tags: [typescript]
use_math: true
image: 
  path: https://github.com/sineTlsl/sineTlsl/assets/97720335/a367fb26-a4e4-44d1-b2e0-18f617ce2101
  width: 400
  alt: 러닝 타입스크립트 교재
---

# CHAPTER 04. 객체

```
객체 리터럴은 각자의 타입이 있는 키와 값의 집합입니다.
```

## 🌓 객체 타입
- `{...}` 구문을 사용해서 객체 리터럴을 생성하면, 타입스크립트는 해당 속성을 기반으로 새로운 객체 타입 또는 타입 형태를 고려한다.
- 해당 각채의 타입은 객체의 값과 동일한 속성명과 원시 타입을 갖는다.
- 값의 속성에 접근하려면 `value.멤버` 또는 `value['멤버']` 구문을 사용한다.

**[예제]** <br> 
- poot 변수의 타입은 number 타입인 born과 string 타입인 name으로 이루어진 두 개의 속성을 갖는 객체다.
- 이 두 개의 속성에 접근하는 것은 허용되지만, 다른 속성 이름으로 접근하려고 하면 해당 이름이 존재하지 않는다는 타입 오류가 발생한다.

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl/assets/97720335/ae9eb13b-7891-4071-b448-15b1ced90b01" width="70%" />
</p>

- 객체 타입은 타입스크립트가 자바스크립트 코드를 이해하는 방법에 대한 핵심 개념이다.
- `null`과 `undefined`를 제외한 모든 값은 그 값에 대한 실제 타입의 멤버 집합을 가지므로 타입 스크립트는 모든 값의 타입을 확인하기 위해 객체 타입을 이해해야 한다.

<br>

### 1. 객체 타입 선언
- 객체 타입은 객체 리터럴과 유사하게 보이지만 필드 값 대신 타입을 사용해 설명한다.
- 타입스크립트가 타입 할당 가능성에 대한 오류 메시지에 표시하는 것과 동일한 구문이다.

**[예제]** <br> 
poetLater 변수는 born: number와 name: string으로 이전과 동일한 타입이다.

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl/assets/97720335/8b356eb4-e980-4a7c-b08b-5d5e1ab7f436" width="70%" />
</p>

### 2. 별칭 객체 타입
- `{born: number, name: string}` 과 같은 객체 타입을 계속 작성하는 것은 번거롭다.
- 각 객체 타입에 타입 별칭을 할당해 사용하는 방법이 더 일반적이다.

**[예제]** <br> 
이전 코드 스니펫은 Poet 타입으로 다시 작성할 수 잇으며, 타입스크립트의 할당 가능성 오류 메시지를 좀 더 직접적으로 읽기 쉽게 만드는 추가 이점이 있다.

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl/assets/97720335/70507dcc-e702-4f78-a250-b49a547e2efd" width="55%" />
</p>

> 🌿 대부분의 타입스크립트 프로젝트는 객체 타입을 설명할 때 `인터페이스 (interface)` 키워드를 사용하는 것을 선호한다.

<br>

## 🌓 구조적 타이핑
- 타입스크립트의 타입 시스템은 **구조적으로 타입화**되어 있다.
- 즉, 타입을 충족하는 모든 값을 해당 타입의 값으로 사용할 수 있다.
- 다시 말하자면 매개변수나 변수가 특정 객체 타입으로 선언되면 타입스크립트에 어떤 객체를 사용하든 해당 속성이 있어야 한다고 말해야 한다.

**[예제]** <br> 
- 별칭 객체 타입인 WithFirstName과 WithLastName은 오직 string 타입의 단일 멤버만 선언한다.
- hasBoth 변수는 명시적으로 선언되지 않았음에도 두 개의 별칭 객체 타입을 모두 가지므로 두 개의 별칭 객체 타입 내에 선언된 변수를 모두 제공할 수 있다.

```ts
type WithFirstName = {
  firstName: string;
}
type WithLirstName = {
  lastName: string;
}

const hasBoth = {
  firstName: "Lucille",
  lastName: "Clifton",
}

// Ok: 'hasBoth'는 string 타입의 'firstName'을 포함함
let withFirstName: WithFirstName = hasBoth;

// Ok: 'hasBoth'는 string 타입의 'lastName'을 포함함
let WithLirstName: WithLirstName = hasBoth;
```

구조적 타이핑은 `덕 타이핑(duck typing)` 과 다르며, 덕 타이핑은 '오리처럼 보이고 오리처럼 꽥꽥거리면, 오리일 것이다'라는 문구에서 유래했다.
- 타입스크립트의 타입 검사기에 구조적 타이핑은 정적 시스템이 타입을 검사하는 경우다.
- 덕 타이핑은 런타임에서 사용될 때까지 객체 타입을 검사하지 않는 것을 말한다.

즉, 자바스크립트는 `덕 타입`인 반면 타입스크립트는 `구조적으로 타입화`된다.

<br>

### 1. 사용 검사
- 객체 타입으로 애너테이션된 위치에 값을 제공할 때 타입스크립트는 값을 해당 객체 타입에 할당할 수 있는지 확인한다.
- 할당하는 값에는 객체 타입의 필수 속성이 있어야 한다.
- 객체 타입에 필요한 멤버가 객체가 없다면 타입스크립트는 타입 오류를 발생시킨다.

**[예제 1]** <br> 
- 별칭 객체 타입인 FirstAndLastNames는 first와 last 속성이 모두 있어야 한다.
- 두 가지 속성을 모두 포함한 객체는 FirstAndLastNames 타입으로 선언된 변수에 사용할 수 있지만, 두 가지 속성이 모두 없는 객체는 사용할 수 없다.

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl/assets/97720335/5ee9ad35-be21-465d-a3bb-dd48124b85d0" width="75%" />
</p>

**[예제 2]** <br> 
- TimeRange 타입은 start 속성을 Date 타입으로 예상한다.
- 하지만, 객체의 start 속성이 Date가 아니라 string 타입이므로 타입 오류가 발생한다.

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl/assets/97720335/6451a243-db6f-417e-b0a3-35a1daf6889f" width="80%" />
</p>

<br>

### 2. 초과 속성 검사
- 변수가 객체 타입으로 선언되고, 초깃값에 따라 객체 타입에서 정의된 것보다 많은 필드가 있다면 타입스크립트에서 타입 오류가 발생한다.
- 따라서 변수를 객체 타입으로 선언하는 것은 타입 검사기에 해당 타입에 예상되는 필드만 있는지 확인하는 방법이기도 하다.

**[예제 1]** <br> 
poetMatch 변수는 별칭 객체 타입에 정의된 필드가 Poet에 정확히 있지만, 초과 속성이 있는 extraProperty는 타입 오류를 발생시킨다. 

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl/assets/97720335/5c2d7cf8-035e-47b3-9576-f2a68fa4f456" width="80%" />
</p>

- 초과 속성 검사는 객체 타입으로 선언된 위치에서 생성되는 객체 리터럴에 대해서만 일어난다.
- 기존 객체 리터럴을 제공하면 초과 속성 검사를 우회한다.

**[예제 2]** <br> 
extraPropertyButOk 변수는 초깃값이 구조적으로 Poet과 일치하기 때문에 이전 예제의 Poet 타입처럼 타입 오류가 발생하지 않는다.

```ts
const existingObject = {
  activity: "walking",
  born: 1935,
  name: "Mary Oliver"
}

const extraPropertyButOk: Poet = existingObject; // Ok
```

- 배열 요소, 클래스 필드 및 함수 매개변수가 포함된 객체 타입과 일치할거라 예상되는 위치에서 생성되는, 새로운 객체가 있는 모든 곳에서도 초과 속성 검사가 일어난다.
- 타입스크립트에서 초과 속성을 금지하면 코드를 께끗하게 유지할 수 있고, 예상한 대로 작동하도록 만들 수 있다.
- 객체 타입에 선언되지 않은 초과 속성은 종종 잘못된 입력된 속성 이름이거나 사용되지 않는 코드일 수 있다.

<br>

### 3. 중첩된 객체 타입
- 자바스크립트 객체는 다른 객체의 멤버로 중첩될 수 있으므로 타입스크립트의 객체 타입도 타입 시스템에서 중첩된 객체 타입을 나타낼 수 있어야 한다.
- 이를 구현하는 구문은 이전과 동일하지만 기본 이름 대신에 `{...}` 객체 타입을 사용한다.

**[예제 1]** <br> 
- Poem 타입은 author 속성이 firstName: string과 lastsName: string이 객체로 선언되었다.
- poemMatch 변수는 구조가 Poem과 일치하기 때문에 Poem을 할당할 수 있는 반면, poemMismatch는 author 속성에 firstName과 lastName 대신 name을 포함하므로 할당할 수 없다.

```ts
type Poem = {
  author: {
      firstName: string;
      lastName: string;
  };
  name: string;
};

// Ok
const poemMatch: Poem = {
  author: {
      firstName: "Sylvia",
      lastName: "Plath",
  },
  name: "Lady Lazarus", 
}
```

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl/assets/97720335/7d054eba-ddaf-4f0f-a7e6-5fb3d4aac9ef" width="90%" />
</p>

**[예제 2]** <br> 
- Poem 타입을 작성할 때 author 속성의 형태를 자체 별칭 객체 타입으로 추출하는 방법도 있다.
- 중첩된 타입을 자체 타입으로 별칭으로 추출하면 타입스크립트의 타입 오류 메시지에 더 많은 정보를 담을 수 있다.
- 이 경우에는 `{ firstName: string, lastName: string; }` 대신 author를 사용할 수 있다.

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl/assets/97720335/6da49ee3-1c08-4672-8272-f7d5d196563b" width="80%" />
</p>

> 🌿 이처럼 중첩된 객체를 고유한 타입 이름으로 바꿔서 사용하면 코드와 오류 메시지가 더 읽기 쉬워진다.

<br>

### 4. 선택적 속성
- 모든 객체에 타입 속성이 필요한 것은 아니다.
- 이때 타입의 속성 애너테이션에서 `:` 앞에 `?`를 추가하면 선택적 속성임을 나타낼 수 있다.
- 필수로 선언된 속성과 `| undefined`는 그 값이 `undefined` 일지라도 반드시 존재해야 한다. 

**[예제 1]** <br> 
- Book 타입은 pages 속성만 필요하고 author 속성은 선택적으로 허용한다.
- 객체가 pages 속성을 제공하기만 하면 author 속성은 제공하거나 생략할 수 있다.

```ts
type Book = {
  author?: string;
  pages: number;
};

// Ok
const ok: Book = {
  author: "Rita Dove",
  pages: 80,
};
```

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl/assets/97720335/14c00d45-d67f-44e4-84e4-6549832baecc" width="80%" />
</p>

**[예제 2]** <br> 
- Writers 타입의 editor 속성은 `?`를 사용해 선언했으므로 변수를 선언할 때 생략이 가능하다..
- author 속성은 `?`가 없으므로 값이 `undefined`여도 반드시 존재해야 한다.

```ts
type Writers = {
  author: string | undefined;
  editor?: string;
};

// Ok: author는 undefined으로 제공됨
const hasRequired: Writers = {
  author: undefined,
}
```

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl/assets/97720335/77678efe-120a-4e4c-a7a0-68f7a13bf2c2" width="70%" />
</p>

<br>

## 🌓 객체 타입 유니언
- 타입스크립트 코드에서는 속성이 조금 다른, 하나 이상의 서로 다른 객체 타입이 될 수 있는 타입을 설명할 수 있어야 한다.
- 또한 속성값을 기반으로 해당 객체 타입 간에 타입을 좁혀야할 수도 있다.

### 1. 유추된 객체 타입 유니언
- 변수에 여러 객체 타입 중 하나가 될 수 있는 초깃값이 주어지면 타입스크립트는 해당 타입을 객체 타입 유니언으로 유추한다.
- 유니언 타입은 가능한 각 객체 타입을 구성하고 있는 요소를 모두 가질 수 있다.
- 객체 타입에 정의된 각각의 가능한 속성은 비록 초깃값이 없는 선택적(`?`) 타입이지만 각 객체 타입의 구성 요소로 주어진다.

**[예제]** <br> 
poem 값은 항상 string 타입인 name 속성을 가지며, pages와 rhymes는 있을 수도 있고, 없을 수도 있다.

```ts
const poem = Math.random() > 0.5
  ? { name: 'The Double Image', pages: 7 }
  : { name: 'Her Kind', rhymes: true };

poem.name; // string
poem.pages; // number | undefined
poem.rhymes; // boolean | undefined
```

<br>

### 2. 명시된 객체 타입 유니언
- 객체 타입의 조합을 명시하면 객체 타입을 더 명확히 정의할 수 있다.
- 코드를 조금 더 작성해야 하지만 객체 타입을 더 많이 제어할 수 있다는 이점이 있다.
- 특히 값의 타입이 객체 타입으로 구성된 유니언이라면 타입스크립트의 타입 시스템은 이런 모든 유니언 타입에 존재하는 속성에 대한 접근만 허용한다.

**[예제]** <br> 
- 앞서 본 poem 변수는 pages 또는 rhymes와 함께 필수 속성인 name을 항상 갖는 유니언 타입으로 명시적으로 작성되었다.
- 속성 name에 접근하는 것은 name 속성이 항상 존재하기 때문에 허용되지만 pages와 rhymes는 항상 존재한다는 보장이 없다.

```ts
type PoemWithPages = {
  name: string;
  pages: number;
};
type PoemWithRhymes = {
  name: string;
  rhymes: boolean;
};

type Poem = PoemWithPages | PoemWithRhymes;

const poem: Poem = Math.random() > 0.5
  ? { name: 'The Double Image', pages: 7 }
  : { name: 'Her Kind', rhymes: true };
```

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl/assets/97720335/8a173df6-5eee-461e-9898-013bdcd329e2" width="70%" />
  <img src="https://github.com/sineTlsl/sineTlsl/assets/97720335/14a8e69d-4a64-4a6f-9dcd-58297d49c8cf" width="70%" />
</p>

- 잠재적으로 존재하지 않는 객체의 멤버에 대한 접근을 제한하면 코드의 안전을 지킬 수 있다.
- 값이 여러 타입 중 하나일 경우, 모든 타입에 존재하지 않는 속성이 객체 존재할 거라 보장할 수 없다.
- 리터럴 타입이나 원시 타입 모두, 혹은 둘 중 하나로 이루어진 유니언 타입에서 모든 타입에 존재하지 않는 속성에 접근하기 위해 타입을 좁여야 하는 것처럼 객체 타입 유니언도 타입을 좁혀야 한다.

<br>

### 3. 객체 타입 내로잉
- 타입 검사기가 유니언 타입 값에 특정 속성이 포함된 경우에만 코드 영역을 실행할 수 있음을 알게 되면, 값의 타입을 해당 속성을 포함하는 구성 요소로만 좁힌다.
- 즉, 코드에서 객체의 형태를 확인하고 타입 내로잉이 객체에 적용된다.

**[예제]** <br>
- 명시적으로 입력된 poem 예제를 계속 살펴보면, poem의 pages가 타입스크립트의 타입 가드 역할을 해 PoemWithPages임을 나타내는지 확인한다.
- 만일 Poem이 PoemWithPage가 아니라면 PoemWithRhymes이어야 한다.

```ts
if ("pages" in poem) {
  poem.pages; // Ok: poem은 PoemWithPages로 좁혀짐
} else {
  poem.rhymes; // Ok: poem은 PoemWithPages로 좁혀짐
}
```

- 타입스크립트는 `if (poem.pages)` 와 같은 형식으로 참 여부를 확인하는 것을 허용하지 않는다.
- 존재하지 않는 객체의 속성에 접근하려고 시도하면 타입 가드처럼 작동하는 방식으로 사용되더라도 타입 오류로 간주된다.

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl/assets/97720335/eb68c9bc-f13c-4e97-b899-f69d6dd939b6" width="70%" />
</p>

<br>

### 4. 판별된 유니언
- 자바스크립트와 타입스크립트에서 유니언 타입으로 된 객체의 또 다른 인기가 있는 형태는 객체의 속성이 객체의 형태를 나타내도록 하는 것이다.
- 이러한 타입 형태를 `판별된 유니언`이라 부르고, 객체의 타입을 가리키는 속성이 `판별값`이다.
- 타입스크립트는 코드에서 판별 속성을 사용해 타입 내로잉을 수행한다.

**[예제]** <br>
- Poem 타입은 PoemWithPages 탸입 또는 PoemWithRhymes 타입 둘 다 될 수 있는 객체를 설명하고 type 속성으로 어느 타입인지를 나타낸다.
- 만일 poem.type이 pages이면, 타입스크립트는 poem을 PoemWithPages로 유추한다.
- 타입 내로잉 없이는 값에 존재하는 속성을 보장할 수 없다.

```ts
type PoemWithPages = {
  name: string;
  pages: number;
  type: 'pages';
};
type PoemWithRhymes = {
  name: string;
  rhymes: boolean;
  type: 'rhymes';
};

type Poem = PoemWithPages | PoemWithRhymes;

const poem: Poem = Math.random() > 0.5
  ? { name: 'The Double Image', pages: 7, type: 'pages' }
  : { name: 'Her Kind', rhymes: true, type: 'rhymes' };

if (poem.type === 'pages') {
  console.log(`It's got pages: ${poem.pages}`); // Ok
} else {
  console.log(`It's rhymes: ${poem.rhymes}`);
}

poem.type; // 타입: 'pages' | 'rhymes'
```

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl/assets/97720335/460cfbce-6548-4f70-8b21-ad93dfb70849" width="70%" />
</p>

<br>

## 🌓 교차 타입
- 타입스크립트 유니언 타입은 둘 이상의 다른 타입 중 하나의 타입이 될 수 있음을 나타낸다.
- 자바스크립트의 런타임 `|` 연산자가 `&` 연산자에 대응하는 역할을 하는 것처럼, 타입스크립트에서도 `& 교차타입 (intersection type)`을 사용해 여러 타입을 동시에 나타낸다.
- 교차 타입은 일반적으로 여러 기존 객체 타입을 별칭 객체 타입으로 결합해 새로운 타입을 생성한다.

**[예제 1]** <br>
Artwork와 Writing 타입은 genre, name, pages 속성을 결합해 WrittenArt 타입을 형성하는 데 사용된다.

```ts
type Artwork = {
  genre: string;
  name: string;
};
type Writing = {
  pages: number;
  name: string;
}

type WrittenArt = Artwork & Writing;

// 다음과 같음
// {
//    genre: string;
//    name: string;
//    pages: number;
// }
```

교차 타입은 유니언 타입과 결합할 수 있으며, 이는 하나의 타입으로 판별된 유니언 타입을 설명하는 데 유용하다.

**[예제 2]** <br>
ShortPoem 타입은 항상 author 속성을 가지며 하나의 type 속성으로 판별된 유니언 타입이다.

```ts
type ShortPoem = { author: string } & (
  | { kigo: string; type: 'haiku' }
  | { meter: number; type: 'villanelle' }
);

// Ok
const morningGlory: ShortPoem = {
  author: 'Fukuda Chiyo-ni',
  kigo: 'Morning Glory',
  type: 'haiku',
};
```

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl/assets/97720335/33144fb5-dbb5-4d82-94f3-3ddc637c418f" width="100%" />
</p>

<br>

### 1. 교차 타입의 위험성
- 교차 타입은 유용한 개념이지만, 우리가 스스로 타입스크립트 컴파일러를 혼동시키는 방식으로 사용되기 쉽다.
- 교차 타입을 사용할 때는 가능한 한 코드를 간결하게 유지해야 한다.

### 1.1 긴 할당 가능성 오류
- 유니언 타입과 결합하는 것처럼 복잡한 교차 타입을 만들게 되면 할당 가능성 오류 메시지는 읽기 어려워진다.
- 다시 말해 복잡하면 복잡할수록 타입 검사기의 메시지도 이해하기 더 어려워진다.
- 이 현상은 타입스크립트의 타입 시스템, 그리고 타입을 지정하는 프로그래밍 언어에서 공통적으로 관측된다.

**[예제]** <br>
이전 코드 스니펫의 ShortPoem의 경우 타입스크립트가 해당 이름을 출력하도록 타입을 일련의 별칭으로 된 객체 타입으로 분할하면 읽기가 훨씬 쉬워진다.

```ts
type ShortPoemBase = { author: string };
type Haiku = ShortPoemBase & { kigo: string; type: "haiku" };
type Villanelle = ShortPoemBase & { meter: number; type: "villanelle" };
type ShortPoem = Haiku | Villanelle;
```

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl/assets/97720335/7e720a5b-a89b-4583-8a6d-7408849e3e70" width="100%" />
</p>


### 1.2. never
- 교차 타입은 잘못 사용하기 쉽고 불가능한 타입을 생성한다.
- 원시 타입의 값은 동시에 여러 타입이 될 수 없기 때문에 교차 타입의 구성 요소로 함께 결합할 수 없다.
- 두 개의 원시 타입을 함께 시도하면 `never` 키워드로 표시되는 `never` 타입이 된다.

```ts
type NotPossible = number & string; // 타입: never
```

- never 키워드와 never 타입은 프로그래밍 언어에서 bottom 타입 또는 empty 타입을 뜻한다.
- bottom 타입은 값을 가질 수 없고 참조할 수 없는 변수 타입이므로 bottom 타입에 그 어떠한 타입도 제공할 수 없다.

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl/assets/97720335/8b49f8f8-a496-4d83-b590-6383ad8bf7fc" width="60%" />
  <img src="https://github.com/sineTlsl/sineTlsl/assets/97720335/9434c2ed-aa8a-4378-982c-1ab9c167e9ce" width="60%" />
</p>

- 대부분의 타입스크립트 프로젝트는 `never` 타입을 거의 사용하지 않지만 코드에서 불가능한 상태를 나타내기 위해 가끔 등장한다.
- 하지만 대부분 교차 타입을 잘못 사용해 발생한 실수일 가능성이 높다.

<br>

**Reference**

러닝 타입스크립트 (Learning TypeScript)
