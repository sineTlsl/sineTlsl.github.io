---
layout: post
title: "[S2-Unit03] JavaScript - 비동기(callback, promise, async/await)"
date: 2023-06-05 15:20:00 +900
lastmod: 2023-06-05 15:20:00 +900
categories: [CODESTATES, Section02]
tags: [CODESTATES, 코드스테이츠, Section02]
use_math: true
image: 
  path: https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/355a29f6-282e-4cb5-88ff-cc8bd1445a7d
  width: 850
  alt: 동기와 비동기 차이
---

다들 동기와 비동기라는 단어는 한 번쯤 들어봤을거라고 생각한다.

비동기를 들어가기 전에 간단하게 동기를 설명하자면, 자바스크립트의 `동기(synchronous)` 처리는 **특정 코드의 실행이 완료될 때까지 기다리고 난 후에 다음 코드를 수행하는 것**을 의미한다. 

# 비동기(Asynchronous)란?

> 자바스크립트의 `비동기(Asynchronous)` 처리는 **특정 코드의 실행이 완료될 때 까지 기다지리 않고, 다음 코드를 수행하는 것**을 의미한다.

자바스크립트는 싱글 스레드 기반으로 동작하는 언어다. 따라서 동기적으로 작동하게 되지만, 자바스크립트가 작동하는 환경(런타임)에서 비동기 처리를 도와주므로 특별한 작업 없이 비동기 처리가 가능하다.

## ⏲ 타이머 API
비동기를 경험하게 되는 첫 번째는 타이머 관련 API이다. 해당 API는 브라우저에서 제공하는 Web API이며, 비동기로 작동하도록 구성되어 있다. 

### setTimeout
setTimeout(callback, millisecond)는 일정 시간 후에 함수를 실행한다.

- `parameter` : 실행할 콜백 함수, 콜백 함수 실행 전 기다려야 할 시간 (밀리초)
- `return 값` : 임의의 타이머 ID


```jsx
setTimeout(function () {
	console.log('1초 후 실행');
}, 1000);
// 123
```

### clearTimeout
clearTimeout(timerId)는 setTimeout 타이머를 종료한다.

- `parameter` : 타이머 ID
- `return 값` : 없음

```jsx
const timer = clearTimeout(function () {
	console.log('10초 후 실행');
}, 10000);

clearTimeout(timer);
// setTimeout이 종료됨
```

### setInterval
setInterval(callback, millisecond)는 일정 시간의 간격을 가지고 함수를 반복적으로 실행한다.

- `parameter` : 실행할 콜백 함수, 반복적으로 함수를 실행시키기 위한 시간 간격 (밀리초)
- `return 값` : 임의의 타이머 ID

```jsx
setInterval(function () {
	console.log('1초마다 실행'):
}, 1000);
// 345
```

### clearInterval
clearInterval(timerId)는 setInterval 타이머를 종료한다.

- `parameter` : 타이머 ID
- `return 값` : 없음

```jsx
const timer = setInterval(function () {
	console.log('1초마다 실행');
}, 1000);
  
clearInterval(timer);
// setInterval이 종료됨
```

지금까지 비동기인 타이머 API에 대해 알아보았다. 타이머 API는 비동기로 작동하므로, 동기화할 수 있게 해주어야 하는데 다음과 같은 3가지 방법으로 활용할 수 있다.

<br>

## 1. Callback
비동기로 작동하는 코드를 제어할 수 있는 첫 번째 방법은 `Callback` 을 활용하는 것이다.

```jsx
const printString = (string, callback) => {
  setTimeout(function () {
    console.log(string);
    callback();
  }, Math.floor(Math.random() * 100) + 1);
};

const printAll = () => {
  printString('A', () => {
    printString('B', () => {
      printString('C', () => {});
    });
  });
};

printAll();
// A
// B
// C
```

callback 함수를 통해 비동기 코드의 순서를 제어할 수 있지만, 코드가 길어지고 복잡해질 수록 가독성이 낮아지는 `Callback Hell` 이 발생하는 단점이 있다.

## 2. Promise
Callback Hell을 방지하면서 비동기로 작동하는 코드를 제어할 수 있는 두 번째 방법은 `Promise` 를 활용하는 것이다.

### new Promise
- Promise는 class이기 때문에 `new` 키워드를 통해 Promise 객체를 생성한다.
- Promise는 비동기 처리를 수행하는 콜백 함수를 전달받는데, 이 콜백 함수는 `resolve` , `reject` 를 인수로 전달 받는다.

### Promise 객체의 내부 프로퍼티
new Promise가 반환하는 Promise 객체는 `state`, `result` 내부 프로퍼티를 갖는다.

- **state**: 기본 상태는 pendin(대기) 다. 비동기 처리를 수행할 콜백 함수가 정상적으로 작동했다면, fulfilled(이행) 로 변경이 되고, 에러가 발생했다면 rejected(거부)가 된다.

- **result** : 처음은 undefined이다. 비동기 처리를 수행할 콜백 함수가 성공적으로 작동하여 resolve(value)가 호출되면 value로, 에러가 발생하여 reject(error)가 호출되면 error로 변환다.

하지만, 직접 접근할 수 없고 `.then`, `.catch`, `.finally` 의 메서드를 사용해야 접근이 가능하다.

- **then** : 콜백 함수(executor)에 작성했던 코드들이 정상적으로 처리가 되었다면 resolve 함수를 호출하고, `.then` 메서드로 접근할 수 있다.

- **catch** : 콜백 함수(executor)에 작성했던 코드들이 에러가 발생할 경우에는 reject 함수를 호출하고 `.catch` 메서드로 접근할 수 있다.
- **finally** : 콜백 함수(executor)에 작성했던 코드들의 정상 처리 여부와 상관없이 `.finally` 메서드로 접근할 수 있다.

<br>

### Promise chaining
Promise chaining가 필요하는 경우는 비동기 작업을 순차적으로 진행해야 하는 경우다.

Promise chaining이 가능한 이유는 `.then`, `.catch`, `.finally` 의 메서드들은 Promise를 반환하기 때문이다. 따라서 `.then` 을 통해 연결할 수 있고, 에러가 발생할 경우 `.catch` 로 처리하면 된다.

```jsx
let promise = new Promise(function(resolve, reject) {
	resolve('성공');
	...
});

promise
  .then((value) => {
    console.log(value);
    return '성공';
  })
  .then((value) => {
    console.log(value);
    return '성공';
  })
  .then((value) => {
    console.log(value);
    return '성공';
  })
  .catch((error) => {
    console.log(error);
    return '실패';
  })
  .finally(() => {
    console.log('성공이든 실패든 작동!');
  });
```

### Promise.all()
`Promise.all()` 은 여러 개의 비동기 작업을 동시에 처리하고 싶을 때 사용한다.

인자로는 배열을 받고, 해당 배열에 있는 모든 Promise에서 콜백 함수 내 작성했던 코드들이 정상적으로 처리가 되었다면 결과를 배열에 저장해 새로운 Promise를 반환 해준다.

다음 코드는 **Promise chaining**을 사용했을 경우다. 코드들이 순차적으로 동작되기 때문에 총 6초의 시간이 걸리게 된다. 또 같은 코드가 중복되는 현상도 발생된다.

```jsx
// Promise chaining
const promiseOne = () => new Promise((resolve, reject) => setTimeout(() => resolve('1초'), 1000));
const promiseTwo = () => new Promise((resolve, reject) => setTimeout(() => resolve('2초'), 2000));
const promiseThree = () => new Promise((resolve, reject) => setTimeout(() => resolve('3초'), 3000));

const result = [];
promiseOne().then(value => {
	result.push(value);
    return promiseTwo();
}).then(value => {
    result.push(value);
    return promiseThree();
}).then(value => {
   	result.push(value);
   	console.log(result);  
	 // ['1초', '2초', '3초']
});
```

이러한 문제들을 `Promise.all()` 을 통해 해결할 수 있다. 비동기 작업들을 동시에 처리하여 3초 안에 모든 작업이 종료된다.

```jsx
// Promise.all()
const promiseOne = () => new Promise((resolve, reject) => setTimeout(() => resolve('1초'), 1000));
const promiseTwo = () => new Promise((resolve, reject) => setTimeout(() => resolve('2초'), 2000));
const promiseThree = () => new Promise((resolve, reject) => setTimeout(() => resolve('3초'), 3000));

Promise.all([promiseOne(), promiseTwo(), promiseThree()])
	.then(value => console.log(value))
	// ['1초', '2초', '3초']
	.catch(err => console.log(err));
```

`Promise.all` 은 인자로 받는 배열에 있는 Promise 중 하나라도 에러가 발생하게 되면 나머지 Promise의 state와 상관없이 종료된다.

또한, Promise를 통해 비동기 코드의 순서를 제어할 수 있지만, Callback 함수와 같이 코드가 길어질 수록 복잡해지고 가독성이 낮아지는 `Promise Hell` 이 발생하는 단점이 있다.

<br>

## 3. Async/Await
자바스크립트에서는 ES8에서 `async/await` 키워드를 제공하였다. 이를 통해 복잡한 Promise 코드를 간결하게 작성할 수 있다.

- 함수 앞에 `async` 키워드를 사용하고, async 함수 내에서만 `await` 키워드를 사용한다.
- 이렇게 작성된 코드는 await 키워드가 작성된 코드가 동작하고 나서 다음 순서의 코드가 동작한다.

**async/await 키워드**는 다음과 같이 작성할 수 있다.

```jsx
// 함수 선언식
async function funcDeclarations() {
	await 작성하고자 하는 코드
	...
}

// 함수 표현식
const funcExpression = async function () {
	await 작성하고자 하는 코드
	...
}

// 화살표 함수
const ArrowFunc = async () => {
	await 작성하고자 하는 코드
	...
}
```

화살표 함수를 사용해서 다음과 같이 간단한 예제를 구현할 수 있다.

```jsx
const printString = (string) => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve();
      console.log(string);
    }, Math.floor(Math.random() * 100) + 1);
  });
};

const printAll = async () => {
  await printString('A');
  await printString('B');
  await printString('C');
};

printAll();
```

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)
