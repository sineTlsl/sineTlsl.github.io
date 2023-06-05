---
layout: post
title: "[S2-Unit01] JavaScript - 일급 객체와 고차 함수"
date: 2023-06-05 15:07:00 +900
lastmod: 2023-06-05 15:08:00 +900
categories: [CODESTATES, Section02]
tags: [CODESTATES, 코드스테이츠, Section02]
use_math: true
---

고차 함수를 알아보기 전, 일급 객체를 알고 있어야 조금 더 이해가 쉽다.

## 일급 객체(First-class object)란? 
자바스크립트의 대표적인 일급 객체 중 하나가 함수다.

함수는 변수에 할당할 수 있어 배열의 요소나 객체의 속성 값으로 지정할 수 있다. 또 함수를 데이터(`string`, `number`, `boolean`, `array`, `object`) 처럼 다룰 수 있다.

### 일급 객체 특징
- 변수에 할당(assignment) 할 수 있다.
- 다른 함수의 전달인자(argument)로 전달될 수 있다.
- 다른 함수의 결과로서 리턴될 수 있다.

**변수에 함수를 할당하는 예시**

```jsx
const square = function(num) {
  return num * num;
};

// 변수 square에는 함수가 할당되어 있으므로 (일급 객체), 함수 호출 연산자 '()'를 사용할 수 있다.
output = square(7);
console.log(output);  // 49
```
함수는 예시와 같이 변수에 저장된 데이터를 전달 인자로 받거나, 리턴 값으로 사용할 수 있다.

<br>

## 고차 함수(Higher-order function)란?

> `고차 함수(higher order function)` 는 함수를 전달인자(argument)로 받을 수 있고, 함수를 리턴할 수 있는 함수다.

- 고차 함수는 함수와 달리 함수 내부에서 변수에 할당하지 않고, 함수를 바로 이용할 수 있다.
- 어떤 고차 함수에 함수를 전달인자로 전달하고, 고차 함수는 함수 자체를 리턴한다.

위에 동작은 함수에서 변수만 빠졌을 뿐, 동일하게 동작한다.

### 콜백 함수
- `콜백 함수(callback function)` 는 다른 함수의 전달인자(argument)로 전달되는 함수다.
- 어떤 작업이 완료되었을 때, 호출하는 경우가 많아서 답신 전화를 뜻하는 콜백 함수라고 이름이 붙여졌다.
- 콜백 함수를 전달받은 고차 함수(caller)는 함수 내부에서 이 콜백 함수를 호출(invoke)할 수 있다.
- 조건에 따라 콜백 함수의 실행 여부를 결정할 수 있다.
- 아예 호출하지 않을 수도 있고, 여러 번 실행할 수도 있으며, 특정 작업의 완료 후에 호출하는 경우도 있다.

### 커링 함수
- **'함수를 리턴하는 함수'**는 이를 고안해 낸 논리학자 하스켈 커리(Haskell Curry)의 이름을 따 `커링 함수` 라고 한다. 
- 따로 커링 함수라는 용어를 사용하는 경우에는, 고차 함수라는 용어를 **함수를 전달인자로 받는 함수**에만 한정해 사용하기도 한다.
- 정확하게는 고차 함수가 커링 함수를 포함한다.

<br>

### 고차함수 예시
**1. 다른 함수를 인자로 받는 경우**

```jsx
function double(num) {
	return num * 2;
}
function doubleNum(func, num) {
	return func(num);
}

let output = doubleNum(double, 4);
console.log(output);  // 8
```

함수 doubleNum은 **다른 함수를 인자로 받는** 고차 함수다. 

함수 doubleNum은 첫 번째 인자 func에 함수가 들어올 경우, 함수 func는 함수 double의 콜백 함수다. 즉, dobule은 함수 doubleNum의 콜백 함수라는 것이다.

**2. 함수를 리턴하는 경우**

```jsx
function adder(added) {
	return function(num) {
    	return num + added;
    };
}

// adder(5)는 함수이므로 함수 호출 연산자 '()'를 사용할 수 있다.
let output = adder(5)(3);
console.log(output);  // 8

const add3 = adder(3); 
output = add3(2);
console.log(output);  // 5
```

함수 adder는 **다른 함수를 리턴하는** 고차 함수다. 

adder는 인자 한 개를 입력받아서 함수(익명 함수)를 리턴한다. 리턴되는 익명 함수는 인자 한 개를 받아서 added와 더한 값을 리턴한다.

**3. 함수를 인자로 받고, 함수를 리턴하는 경우**

```jsx
function double(num) {
	return num * 2;
}

function doubleAdder(added, func) {
    const doubled = func(added);
    return function (num) {
      	return num + doubled;
    };
}

// doubleAdder(5, double)는 함수이므로 함수 호출 기호 '()'를 사용할 수 있다.
doubleAdder(5, double)(3);  // 13
```

함수 doubleAdder의 인자 func는 함수 doubleAdder의 콜백 함수다. 함수 double은 함수 doubleAdder의 콜백으로 전달되었다.

<br>

### 고차 함수를 사용하는 이유
> **추상화**: 복잡한 어떤 것을 압축해서 핵심만 추출한 상태로 만드는 것

추상화의 결과는 자동차의 시동 버튼, 자료를 정리하는 엑셀, 지하철/버스를 타기 위한 교통 카드 등 우리의 일상생활에서 쉽게 찾아볼 수 있다.

현재 자바스크립트를 비롯한 언어도 추상화의 결과이며, 크롬 개발자 도구의 콘솔 탭에서 코드를 입력할 경우에 크롬의 자바스크립트 해석기(엔진)가 대신 해주는 것도 마찬가지다.

**1. 추상화는 생산성(productivity)의 향상**
- 추상화는 고민거리를 줄여주고, 문제 해결이 더 쉬워지도록 도와준다.

**2. 고차 함수는 함수를 통해 얻은 추상화를 한 단계 더 높인 것**

**함수** 
= ```값을 전달받아 리턴한다``` = ```값에 대한 복잡한 로직은 감추어져 있다``` = ```값 수준에서의 추상화```
- 고차 함수는 이 추상화의 수준을 사고의 추상화 수준으로 끌어올린다.
- 값 수준의 추상화: 단순히 값(value)을 전달받아 처리하는 수준
- 사고의 추상화: 함수(사고의 묶음)를 전달받아 처리하는 수준
- 고차 함수를 통해, 보다 높은 수준(higher order)에서 생각할 수 있다.

**고차 함수** 
= ```함수를 전달받거나 함수를 리턴한다``` = ```사고(함수)에 대한 복잡한 로직은 감추어져 있다``` = ```사고 수준에서의 추상화```

- 추상화의 수준이 높아지는 만큼, 생산성도 높아진다.

<br>

### 사고 수준의 추상화의 예시

```jsx
const data = [
    {
        gender: 'male',
        age: 24,
    },
    {
        gender: 'male',
        age: 25,
    },
    {
      	gender: 'female',
        age: 27,
    },
    {
        gender: 'female',
        age: 22,
    },
    {
        gender: 'male',
        age: 29,
    },
];
```

위와 같이 주어진 데이터를 순차적으로 처리하려고 할 때, 모든 작업을 하나의 함수로 작성할 수 있다.

**남성들의 평균 나이를 구하는 함수 예제**

```jsx
function getAverageAgeOfMaleAtOnce(data) {
    const onlyMales = data.filter(function (d) {
      	return d.gender === 'male';
    });

  	const numOfMales = onlyMales.length;
  	const onlyMaleAges = onlyMales.map(function (d) {
    	return d.age;
  	});
	const sumOfAges = onlyMaleAges.reduce(function (acc, cur) {
    	return acc + cur;
  	}, 0);

  	return sumOfAges / numOfMales;
}
```

위 함수는 배열 메서드를 적절하게 사용하여 순차적으로 작업을 수행한다. 현재는 남성의 평균 나이만 구하는 작업에만 사용할 수 있지만, 여기서 `'male'` 을 매개변수화(parameterization) 하여 남성과 여성의 평균 나이를 구하는 작업을 수행할 수 있다.

한편, `filter`, `map`, `reduce` 등의 배열 메서드는 다른 목적을 위해서 사용될 수 있다. 이러한 추상화는 고차 함수를 통해 보다 더 쉽게 달성할 수 있다.

```jsx
function getOnlyMales(data) {
    return data.filter(function (d) {
      	return d.gender === 'male';
    });
}

function getOnlyAges(data) {
    return data.map(function (d) {
      	return d.age;
    });
}

function getAverage(data) {
    const sum = data.reduce(function (acc, cur) {
      	return acc + cur;
    }, 0);
    return sum / data.length;
}

// 여러 개의 함수를 인자로 전달받아 함수를 리턴하는 고차 함수
function compose(...funcArgs) {
    return function (data) {
        let result = data;
        for (let i = 0; i < funcArgs.length; i++) {
          	result = funcArgs[i](result);
        }
        return result;
    };
}

// 각각의 함수 재사용 가능
const getAverageAgeOfMale = compose(
    getOnlyMales,  // 배열을 입력받아 배열을 리턴하는 함수
    getOnlyAges,  // 배열을 입력받아 배열을 리턴하는 함수
    getAverage  // 배열을 입력받아 `number` 타입을 리턴하는 함수
);

const result = getAverageAgeOfMale(data);
console.log(result);  // 26
```

이와 같이 고차 함수를 통해 사고 수준에서 추상화를 달성할 수 있다. 이러한 작업들은 다른 목적을 위해 재사용될 수 있다.

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)
