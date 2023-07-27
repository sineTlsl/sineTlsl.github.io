---
layout: post
title: "[LearningTS] Chapter05. 함수"
date: 2023-07-27 16:06:00 +900
lastmod: 2023-07-27 16:06:00 +900
categories: [STUDY, Learning TypeScript]
tags: [typescript]
use_math: true
image: 
  path: https://github.com/sineTlsl/sineTlsl/assets/97720335/a367fb26-a4e4-44d1-b2e0-18f617ce2101
  width: 400
  alt: 러닝 타입스크립트 교재
---

# CHAPTER 05. 함수

```
한쪽 끝에는 함수 인수가 있고 다른 쪽 끝에는 반환 타입이 있습니다.
```

## 🌓 함수 매개변수

**[예제]** <br> 
sing 함수는 song 매개변수를 받아 콘솔에 출력한다.

```ts
function sing(song) {
  console.log(`Singing: ${song}!`);
}
```

- 명시적 타입 정보가 선언되지 않으면 절대 타입을 알 수 없다.
- 타입스크립트가 이를 `any` 타입으로 간주하며 매개변수의 타입은 무엇이든 될 수 있다.
- 변수와 마찬가지로 타입스크립트를 사용하면 타입 애너테이션으로 함수 매개변수의 타입을 선언할 수 있다.

```ts
function sing(song: string) {
  console.log(`Singing: ${song}!`);
}
```

- 코드를 유효한 타입스크립트 구문으로 만들기 위해 함수 매개변수에 적절한 타입 애너테이션을 추가할 필요는 없다.
- 타입스크립트는 타입 오류로 오류를 계속 알리지만, 이미 시작된 자바스크립트는 게속 실행된다.

<br>

### 1. 필수 매개변수

- 자바스크립트에서는 인수의 수와 상관없이 함수를 호출할 수 있다.
- 하지만 타입스크립트는 함수에 선언된 모든 매개변수가 필수라고 가정한다.
- 함수가 잘못된 수의 인수로 호출되면, 타입스크립튼느 타입 오류의 형태로 이의를 제기한다.
- 함수가 너무 적거나 많은 인수로 호출되면 타입스크립트는 인수의 개수를 계산한다.

**[예제]** <br>
```ts
function singTwo(first: string, second: string) {
  console.log(`${first} / ${second}`);
}

singTwo("I will Survie", "Higher Love"); // Ok
```

<p align="center">
  <img src="https://github.com/FE-BookStudy/LearningTS/assets/97720335/c49adb31-6196-4dbe-81c7-d77ad95dd7e4" width="60%" />
  <img src="https://github.com/FE-BookStudy/LearningTS/assets/97720335/82d13c13-597e-48f8-83f5-2addbb399c68" width="60%" />
</p>

- 함수에 필수 매개변수를 제공하도록 강제하면 예상되는 모든 인숫값을 함수 내에 존재하도록 만들어 타입 안정성을 강화하는 데 도움이 된다.
- 모든 인숫값이 존재하는지 확인하지 못하면 이전 singTwo 함수가 undefined 로그로 남기거나 인수를 무시하는 것과 같이 코드에서 예기치 않은 동작이 발생한다.

<br>

### 2. 선택적 매개변수

- 자바스크립트에서 함수 매개변수가 제공되지 않으면 함수 내부의 인숫값을 `undefined`으로 기본 설정이 되지만, 타입스크립트는 인수를 제공하지 못하는 경우, 타입 오류가 발생한다.
- 타입스크립트에서 선택적 객페 타입 속성과 유사하게 타입 애너테이션의 `:` 앞에 `?`를 추가해 매개변수가 선택적이라고 표시한다.
- 함수 호출에 선택적 매개변수를 제공할 필요는 없다.
- 선택적 매개변수에는 항상 `| undefined`가 유니언 타입으로 추가되어 있다.

**[예제 1]** <br> 
- announceSong 함수에서 singer 매개변수는 선택 사항으로 표시된다.
- 타입은 string | undefined이며 함수 호출자가 singer 매개변수를 위한 인수를 제공할 필요가 없다.
- 만일 singer가 제공되면, string 값이거나 undefined일 수 있다.

```ts
function announceSong(song: string, singer?: string) {
  console.log(`Song: ${song}`);

  if (singer) {
    console.log(`Singer: ${singer}`);
  }
}

announceSong('Greensleeves'); // Ok
announceSong('Greensleeves', undefined); // Ok
announceSong('Greensleeves', 'Sia'); // Ok
```

- 이러한 선택적 매개변수는 항상 암묵적으로 undefined가 될 수 있다.
- 이전 코드에서 singer눈 string | undefined 타입으로 시작한 후에 if 문에 따라 string 타입으로 좁혀진다.
- 선택적 매개변수는 `| undefined`를 포함하는 유니언 타입 매개변수와는 다르며, `?`으로 표시된 선택적 매개변수가 아닌 매개변수는 값이 명시적으로 `undefined`일지라도 항상 제공되어야 한다.

**[예제 2]** <br> 
- announceSongBy 함수의 singer 매개변수는 명시적으로 제공되어야 한다.
- singer는 string 값이거나 undefined가 될 수 있다.

```ts
function announceSongBy(song: string, singer: string | undefined) {
  /*...*/
}

announceSongBy('Greensleeves', undefined); // Ok
announceSongBy('Chandelier', 'Sia'); // Ok
```

<p align="center">
  <img src="https://github.com/FE-BookStudy/LearningTS/assets/97720335/74943004-2659-4814-b6c9-aac9c2c43c1b" width="65%" />
</p>

- 함수에서 사용되는 모든 선택적 매개변수는 **마지막 매개변수**여야 한다.
- 필수 매개변수 전에 선택적 매개변수를 위치시키면 다음과 같이 타입스크립트 구문 오류가 발생한다.

<p align="center">
  <img src="https://github.com/FE-BookStudy/LearningTS/assets/97720335/f198d1cf-c24e-44d7-a2af-11a2431e4c57" width="70%" />
</p>

<br>

### 3. 기본 매개변수

- 자바스크립트에서 선택적 매개변수를 선언할 때 =와 같이 값이 포함된 기본값을 제공할 수 있다.
- 즉, 선택적 매개변수에는 기본적으로 값이 제공되기 때문에 해당 타입스크립트 타입에는 암묵적으로 함수 내부에 `| undefined` 유니언 타입이 추가된다.
- 타입스크립트는 함수의 매개변수에 대해 인수를 누락하거나 `undefined` 인수를 사용해서 호출하는 것을 여전히 허용한다.
- 타입스크립트의 타입 추론은 초기 변숫값과 마찬가지로 기본 함수 매개변수에 대해서도 유사하게 작동한다.
- 매개변수에 기본값이 있고 타입 애너테이션이 없는 경우, 타입스크립트는 해당 기본값을 기반으로 매개변수 타입을 유추한다.

**[예제]** <br> 
rateSong 함수에서 rating은 number 타입으로 유추되지만, 함수를 호출하는 코드에서는 선택적 number | undefined가 된다.

```ts
function rateSong(song: string, rating = 0) {
  console.log(`${song} gets ${rating}/5 stars!`);
}

rateSong('Photograph');
rateSong('Set Fire to Rain', 5);
rateSong('Set Fire to the Rain', undefined);
```

<p align="center">
  <img src="https://github.com/FE-BookStudy/LearningTS/assets/97720335/52d53239-5408-4eeb-96b3-471bfb7e8192" width="80%" />
</p>

<br>

### 4. 나머지 매개변수
- 자바스크립트의 일부 함수는 임의의 수의 인수로 호출할 수 있도록 만들어진다.
- `...` 스프레드 연산자는 함수 선언의 마지막 매개변수에 위치하고, 해당 매개변수에서 시작해 함수에 전달된 '나머지(rest)' 인수가 모두 단일 배열에 저장되어야 함을 나타낸다.
- 타입스크립트는 이러한 나머지 매개변수의 타입을 일반 매개변수와 유사하게 선언할 수 있다.
- 단 인수 배열을 나타내기 위해 끝에 `[]` 구문이 추가된다는 점만 다르다.

**[예제]** <br> 
singAllTheSongs는 songs 나머지 매개변수에 대해 0개 이상의 string 타입 인수를 사용할 수 있다.

```ts
function singAllTheSongs(singer: string, ...songs: string[]) {
  for (const song of songs) {
    console.log(`${song}, by ${singer}`);
  }
}

singAllTheSongs('Alicia Keys'); // Ok
singAllTheSongs('lady Gaga', 'Bad Romance', 'Just Dance', 'Poker Face'); // Ok
```

<p align="center">
  <img src="https://github.com/FE-BookStudy/LearningTS/assets/97720335/7f010b83-419a-415c-a70d-db78a5cc4a2e" width="80%" />
</p>

<br>

## 🌓 반환 타입
- 타입스크립트는 지각적이다.
- 함수가 반환할 수 있는 가능한 모든 값을 이해하면 함수가 반환하는 타입을 알 수 있다.

**[예제 1]** <br> 
```ts
// 타입: (songs: string[]) => number
function singSongs(songs: string[]) {
  for (const song of songs) {
    console.log(`${song}`);
  }

  return songs.length;
}
```

함수에 다른 값을 가진 여러 개의 반환값을 포함하고 있다면 타입스크립트는 반환 타입을 가능한 모든 반환 타입의 조합으로 유추한다.

**[예제 2]** <br>
- getSongAt 함수는 string | undefined를 반환하는 것으로 유추된다.
- 두 가지 가능한 반환값이 각각 string과 undefined이기 때문이다.

```ts
// 타입: (songs: string[], index: number) => string | undefined
function getSongAt(songs: string[], index: number) {
  return index < songs.length 
    ? songs[index] 
    : undefined;
}
```

<br>

### 명시적 반환 타입
변수와 마찬가지로 타입 애너테이션을 사용해 함수의 반환 타입을 명시적으로 선언하지 않는 좋지만, 함수에서 반환 타입을 명시적으로 선언하는 방식이 매우 유용할 때가 종종 있다.
- 가능한 반환값이 많은 함수가 항상 동일한 타입의 값을 반환하도록 강제한다.
- 타입스크립트는 재귀 함수의 반환 타입을 통해 유추하는 것을 거부한다.
- 수백 개 이상의 타입스크립트 파일이 있는 매우 큰 프로젝트에서 타입스크립트 타입 검사 속도를 높일 수 있다.

함수 선언 반환 타입 에너테이션은 매개변수 목록이 끝나는 `)` 다음에 배치되며, 함수 선언의 경우는 `{` 앞에 배치된다.

```ts
function singSongRecursive(songs: string[], count = 0): number {
  return songs.length ? singSongRecursive(songs.slice(1), count + 1) : count;
}
```

화살표 함수의 경우 `=>` 앞에 배치된다.

```ts
const singSongRecursive = (songs: string[], count = 0): number => {
  return songs.length ? singSongRecursive(songs.slice(1), count + 1) : count;
};
```

함수의 반환문이 함수의 반환 타입으로 할당할 수 없는 값을 반환하는 경우 타입스크립트는 할당 가능서 오류를 표시한다.

**[예제]** <br> 
getSongRecordingDate 함수는 Date | undefiend를 반환하도록 명시적으로 선언되었지만, 반환문 중 하나가 string을 반환하도록 잘못 제공하고 있다.

<p align="center">
  <img src="https://github.com/FE-BookStudy/LearningTS/assets/97720335/ad63a651-4ae8-4625-a79b-436cc51f02c6" width="60%" />
</p>

<br>

## 🌓 함수 타입
- 자바스크립트에서는 함수의 값으로 전달할 수 있다.
- 즉, 함수를 가지기 위한 매개변수 또는 변수의 타입을 선언하는 방법이 필요하다.
- 함수 타입 구문은 화살표 함수와 유사하지만 함수 본문 대신 타입이 있다.

**[예제 1]** <br> 
nothingInGiveString 변수 타입은 매개변수가 없고 string 타입을 반환하는 함수다.

```ts
let nothingInGiveString: () => string;
```

**[예제 2]** <br> 
inputAndOutput 변수 타입은 string[] 매개변수와 count 선택적 매개변수 및 number 값을 반환하는 함수임을 설명한다.

```ts
let inputAndOutput: (songs: string[], count?: number) => number;
```

함수 타입은 콜백 매개변수(함수로 호출되는 매개변수)를 설명하는 데 자주 사용된다.

**[예제 3]** <br>
- runOnSongs 함수는 getSongAt 매개변수의 타입을 index: number를 받고 string을 반환하는 함수로 선언했다.
- getSongAt을 전달하면 해당 타입과 일치하지만, logSong은 매개변수로 number 대신 string을 사용하므로 반환값을 가져오는 데 실패한다.

```ts
const songs = ['Juice', 'Shake It Off', "What's Up"];

function runOnSongs(getSongAt: (index: number) => string) {
  for (let i = 0; i < songs.length; i++) {
    console.log(getSongAt(i));
  }
}

function getSongAt(index: number) {
  return `${songs[index]}`;
}
runOnSongs(getSongAt); // Ok

function logSong(song: string) {
  return `${song}`;
}
```

runOnSongs(logSong)에 대한 오류 메시지는 할당 가능성 오류의 예로 몇 가지 상세한 단계까지 제공한다.

<p align="center">
  <img src="https://github.com/FE-BookStudy/LearningTS/assets/97720335/be91a717-e434-4d78-85ee-36aacd57bdf0" width="90%" />
</p>

**두 함수를 서로 할당할 수 없다는 오류를 출력할 때 타입스크립트는 일반적으로 세 가지 상세한 단계를 제공한다.**

1. 첫 번째 들여쓰기 단계는 두 함수 타입을 출력한다.
2. 다음 들여쓰기 단계는 일치하지 않는 부분을 지정한다.
3. 마지막 들여쓰기 단계는 일치하지 않는 부분에 대한 정확한 할당 가능성 오류를 출력한다.

**이전 코드 스니핏에서 단계별로 제공하는 내용은 다음과 같다.**

1. logSong: (song: string) => string은 getSongAt: (index: number) => string에 할당되도록 제공된 타입이다.
2. logSong의 song 매개변수는 getSongAt의 index의 매개변수로 할당된다.
3. song의 string 타입은 index의 number 타입에 할당할 수 없다.

<br>

### 1. 함수 타입 괄호
- 함수 타입은 다른 타입이 사용되는 모든 곳에 배치할 수 있다.
- 여기에는 유니언 타입도 포함된다.
- 유니언 타입의 애너테이션에서 함수 반환 위치를 나타내거나 유니언 타입을 감싸는 부분을 표시할 때 괄호를 사용한다.

```ts
// 타입은 string | undefined 유니언을 반환하는 함수
let returnStringOrUndefined: () => string | undefined;

// 타입은 undefined나 string을 반환하는 함수
let maybeReturnString: (() => string) | undefined;
```

### 2. 매개변수 타입 추론
- 매개변수로 사용되는 인라인 함수를 포함하여 작성한 모든 함수에 대해 매개변수를 선언해야 한다면 번거로울 것이다.
- 다행히도 타입스크립트는 선언된 타입의 위치에 제공된 함수의 매개변수 타입을 유추할 수 있다.

**[예제 1]** <br> 
singer 변수는 string 타입의 매개변수를 갖는 함수로 알려져 있으므로 나중에 singer가 할당되는 함수 내의 song 매개변수는 string으로 예측된다.

```ts
let singer: (song: string) => string;

singer = function(song) {
  // song: string의 타입
  return `Singer: ${song.toUpperCase()}!`; // Ok
}
```

함수를 매개변수로 갖는 함수에 인수로 전달된 함수는 해당 매개변수 타입도 잘 유추할 수 있다.

**[예제 2]** <br>
song과 index 매개변수 타입스크립트에 따라 각각 string과 number로 유추된다.

```ts
const songs = ['Call Me', 'Jolene', 'The Chain'];

// song: string
// index: number
song.forEach((song, index) => {
  console.log(`${song} is at index ${index}`);
});
```

<br>

### 3. 함수 타입 별칭
- 함수 타입에서도 동일하게 타입 별칭을 사용할 수 있다.

**[예제 1]**<br>
- StringToNumber 타입은 strng 타입을 받고 Number 타입을 반환하는 함수의 별칭을 지정한다.
- 별칭은 이후 변수 타입을 설명하는 데 사용한다.

```ts
type StringToNumber = (input: string) => number;

let stringToNumber: StringToNumber;

stringToNumber = (input) => input.length;
```

<p align="center">
  <img src="https://github.com/FE-BookStudy/LearningTS/assets/97720335/d802cf4e-48d4-4806-aabb-3b9fc08fc732" width="80%" />
</p>

**[예제 2]**<br>
- 비슷하게 함수 매개변수도 함수 타입을 참조하는 별칭을 입력할 수 있다.
- useNumberToString 함수는 함수 타입 별칭인 NumberToString의 단일 매개변수를 갖는다.

```ts
type NumberToString = (input: number) => string;

function useNumberToString(numberToString: NumberToString) {
  console.log(`The string is: ${numberToString(1234)}`);
}

useNumberToString((input) => `${input}! Hooray!`); // Ok
```

<p align="center">
  <img src="https://github.com/FE-BookStudy/LearningTS/assets/97720335/b723d916-bbeb-4b32-9055-aa7283264445" width="80%" />
</p>

타입 별칭은 특히 함수 타입에 유용하며, 타입 별칭을 이용하면 반복적으로 작성하는 매개변수와 반환 타입을 갖는 코드 공간을 많이 절약할 수 있다.

<br>

## 🌓 그 외 반환 타입

### 1. void 반환 타입
- 일부 함수는 어떤 값도 반환하지 않는다.
- 예를 들면 return 문이 없는 함수이거나 값을 반환하지 않는 return 문을 가진 함수일 경우다.
- 타입스크립트는 `void` 키워드를 사용해 반환 값이 없는 함수의 반환 타입을 확인할 수 있다.

**[예제 1]**<br>
logSong 함수는 void를 반환하도록 선언되었으므로 값 반환을 허용하지 않는다.

<p align="center">
  <img src="https://github.com/FE-BookStudy/LearningTS/assets/97720335/9084b11f-3b72-410b-8c61-f1d8aeb03e78" width="60%" />
</p>

- 함수 타입 선언 시 void 반환 타입은 매우 유용하다.
- 함수 타입을 선언할 때 void를 사용하면 함수에서 반환되는 모든 값은 무시된다.

**[예제 2]**<br>
songLogger 변수는 song: string을 받고, 그 값을 반환하지 않는 함수다.

```ts
let songLogger: (song: string) => void;

songLogger = (song) => {
  console.log(song);
};

songLogger('Heart of Glass'); // Ok
```

- 자바스크립트 함수는 실젯값이 반환되지 않으면 기본이 모두 undefined를 반환하지만 void는 undefined와 동일하지 않는다.
- `void`는 함수의 반환 타입이 무시된다는 것을 의미하고, `undefined`는 반환되는 리터럴 값이다.

**[예제 3]**<br>
undefined를 포함하는 대신 void 타입의 값을 할당하려고 하면 오류가 발생한다. 

```ts
function returnsVoid() {
  return;
}

let lazyValue: string | undefined;
```

<p align="center">
  <img src="https://github.com/FE-BookStudy/LearningTS/assets/97720335/48540815-dac7-47d3-9cf1-8cfbd03901af" width="70%" />
</p>

- undefiend와 void를 구분해서 사용하면 매우 유용하다.
- 특히 void를 반환하도록 선언된 타입 위치에 전달된 함수가 반한된 모든 값을 무시하도록 설정할 때 유용하다.
- 배열의 내장 forEach 메서드는 void를 반환하는 콜백을 받는다.
- forEach에 제공되는 함수는 원하는 모든 값을 반환할 수 있다.

**[예제 4]**<br>
saveRecords 함수의 records.push(record)는 number(배열의 `.push`에서 반환된 값)를 반환하지만, 여전히 newRecords.forEach에 전달된 화살표 함수에 대한 반환값이 허용된다.

```ts
const records: string[] = [];

function saveRecords(newRecords: string[]) {
  newRecords.forEach((record) => records.push(record));
}

saveRecords(['21', 'Come On Over', 'The Bodyguard']);
```

- void 타입은 자바스크립트가 아닌 함수의 반환 타입을 선언하는 데 사용하는 타입스크립트 키워드다.
- **void 타입은 함수의 반환값이 자체적으로 반환될 수 있는 값도 아니고, 사용하기 위한 것도 아니라는 표시를 기억해야 한다.**

<br>

### 2. never 반환 타입
- 일부 함수는 값을 반환하지 않을 뿐만 아니라 반환할 생각도 전혀 없다.
- never 반환 함수는 (의도적으로) 항상 오류를 발생시키거나 무한 루프를 실행하는 함수다.
- 함수가 절대 반환하지 않도록 의도하려면 명시적 `: never` 타입 애너테이션을 추가해 해당 함수를 호출한 후 모든 코드가 실행되지 않음을 나타낸다.

**[예제]**<br>
fail 함수는 오류만 발생시키므로 param의 타입을 string으로 좁혀서 타입스크립트의 제어 흐름 분석을 도와준다.

```ts
function fail(message: string): never {
  throw new Error(`Invariat failure: ${message}.`);
}

function workWithUnsageParam(param: unknown) {
  if (typeof param !== 'string') {
    fail(`param should be a string, not ${typeof param}`);
  }

  // 여기에서 param의 타입은 string으로 알려진다.
  param.toUpperCase();
}
```

> 🌿 `never`는 `void`와 다르다. **void**는 아무것도 반환하지 않는 함수를 위한 것이고, **never**는 절대 반환하지 않는 함수를 위한 것이다.

<br>

## 🌓 함수 오버로드
- 일부 자바스크립트 함수는 선택적 매개변수와 나머지 매개변수만으로 표현할 수 없는 매우 다른 매개변수들로 호출될 수 있다.
- 이러한 함수는 `오버로드 시그니처`라고 불리는 타입스크립트 구문으로 설명할 수 있다.
- 즉, 하나의 최종 `구현 시그니처`와 그 함수의 본문 앞에 서로 다른 버전의 함수 이름, 매개변수, 반환 타입을 여러 번 선언한다.
- 오버로드된 함수 호출에 대해 구문 오류를 생성할지 여부를 결정할 때 타입스크립트는 함수의 오버로드 시그니처만 확인한다.
- 구현 시그니처는 함수의 내부 로직에서만 사용된다.

**[예제]**<br>
- createDate 함수는 1개의 timestamp 매개변수 또는 3개의 매개변수(month, day, year)를 사용해 호출한다.
- 허용된 수의 인수를 사용해 호출할 수 있지만 2개의 인수를 사용해 호출하면 2개의 인수를 허용하는 오버로드 시그니처가 없기 때문에 타입 오류가 발생한다.
- 예제의 처음 두 줄은 오버로드 시그니처이고 세 번째 줄은 구현 시그니처 코드다.

```ts
// ============== 오버로드 시그니처 ==============
function createDate(timestamp: number): Date;
function createDate(month: number, day: number, year: number): Date;

// ============== 구현 시그니처 ==============
function createDate(monthOrTimeStamp: number, day?: number, year?: number) {
  return day === undefined || year === undefined
    ? new Date(monthOrTimeStamp)
    : new Date(year, monthOrTimeStamp, day);
}

createDate(554356800); // Ok
createDate(7, 27, 1987); // Ok
```

<p align="center">
  <img src="https://github.com/FE-BookStudy/LearningTS/assets/97720335/77f344ae-a3f7-4ae6-b035-b09d87599bae" width="80%" />
</p>

- 타입스크립트를 컴파일해 자바스크립트로 출력하면 다른 타입 시스템 구문처럼 오버로드 시그니처도 지워진다.

이전 코드 스니펫의 함수는 다음 자바스크립트처럼 컴파일 된다.

```js
function createDate(monthOrTimeStamp, day, year) {
  return day === undefined || year === undefined
    ? new Date(monthOrTimeStamp)
    : new Date(year, monthOrTimeStamp, day);
}
```

> 🌿 함수 오버로드는 복잡하고 설명하기 어려운 함수 타입에 사용하는 최후의 수단이다. 함수를 단순하게 유지하고 가능하면 함수 오버로드를 사용하지 않는 것이 좋다.

<br>

### 호출 시그니처 호환성

- 오버로드된 함수의 구현에서 사용되는 구현 시그니처는 매개 변수 타입과 반환 타입에 사용하는 것과 동일하다.
- 따라서 함수의 오버로드 시그니처에 있는 반환 타입과 각 매개변수는 구현 시그니처에 있는 동일한 인덱스의 매개변수에 할당할 수 있어야 한다.
- 즉, 구현 시그니처는 모든 오버로드 시그니처와 호환되어야 한다.

**[예제]**<br>
- format 함수의 구현 시그니처는 첫 번째 매개변수를 string으로 선언한다.
- 처음 두 개의 오버로드 시그니처는 string 타입과 호환되지만, 세 번째 오버로드 시그니처의 () => string 타입과는 호환되지 않는다.

<p align="center">
  <img src="https://github.com/FE-BookStudy/LearningTS/assets/97720335/3c916648-0a25-4bd6-8fcd-9ccd2c8fef3e" width="80%" />
</p>

<br>

**Reference**

러닝 타입스크립트 (Learning TypeScript)
