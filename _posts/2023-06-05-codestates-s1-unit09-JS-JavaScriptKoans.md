---
layout: post
title: "[S1-Unit09] JavaScript Koans 회고"
date: 2023-06-05 13:59:00 +900
lastmod: 2023-06-05 13:59:00 +900
categories: [CODESTATES, Section01]
tags: [CODESTATES, 코드스테이츠, Section01, 회고]
use_math: true
image: 
  path: https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/384144ba-7525-4370-8579-eb1875128f58
  width: 901
  alt: JavaScript Koans 회고 사진
---

## 과제 Rule
테스트하는 값과 기대값을 비교하기 위해서 `expect` 함수를 사용하여 진행한다.

> **expect의 사용법**
>
> `expect(테스트하는값).기대하는조건`
`expect(isEven(3)).to.be.true` => 'isEven(3)의 결과값은 참(true)이어야 한다'
`expect(1 + 2).to.equal(3)`  => 'sum(1, 2)의 결과값은 3과 같아야(equal) 한다' 
> 
> '기대하는조건'에 해당하는 함수를 `matcher` 라고 한다.
'참인 것이어야 한다' => `to.be.true`
'3과 같아야 한다' => `to.equal(3)`

`.equal` 은 두 값이 타입까지 엄격하게 같은지 검사(strict equality, ===) 한다.

## 👩🏻‍💻 CODE
### 표현식 (Expressioin) 예제

```jsx
it ('', function {
    expect(1 + '1').to.equal('11');
    expect(123 - '1').to.equal(122);
    expect(1 + true).to.equal(2);
    expect('1' + true).to.equal('1true');
})
```

주어진 표현식의 결과를 예측하여 작성하는 부분이였는데, 놓치고 있었던 부분이 `+` 가 아닌 다른 산술연산자(`**`,`*`, `/`, `%`, `-`) 들은 피연산자를 숫자로 반환한다는 것이였다. 

자주 사용하지 않는 부분이다보니 순간 헷갈리게 되었었고, 예제를 통해 확실하게 짚고 넘어갈 수 있었다.

<br>

### 상수 (const) 예제

```jsx
// Array
it ('', function {
    const arr = [];
    const toBePushed = 42;
    arr.push(toBePushed);
    expect(arr[0]).to.equal(42);
})
```
```jsx
// Object
it ('', function {
    const obj = { x: 1 };
    expect(obj.x).to.equal(1);

    delete obj.x;
    expect(obj.x).to.equal(undefined);
})
```

`const` 로 선언된 변수는 재할당이 금지되지만, 배열과 객체는 새로운 요소(속성) 추가하거나 삭제가 가능하다. 

<br>

### 스코프 (Scope) 예제

```jsx
// 함수 선언문과 함수 표현식의 차이를 확인하는 예제
it ('', function {
    let funcExpressed = 'to be a function';

    expect(typeof funcDeclared).to.equal('function');
    expect(typeof funcExpressed).to.equal('string');  // 현재 'string' 타입의 값이 들어가있다.

    // 함수 선언문 (declaration)
    function funcDeclared() {
      return 'this is a function declaration';
    }

    // 함수 표현식 (expression)
    funcExpressed = function () {
      return 'this is a function expression';
    };

    const funcContainer = { func: funcExpressed };
    expect(funcContainer.func(funcExpressed)).to.equal('this is a function expression');

    funcContainer.func = funcDeclared;
    expect(funcContainer.func()).to.equal('this is a function declaration');
})
```

여기서 `호이스팅(hosting)` 의 개념을 알고 있어야 정확하게 이해를 할 수 있다.

`호이스팅` 은 함수 안에 있는 선언들을 모두 끌어올려서 해당 함수 유효 범위의 최상단에 선언하는 것이다.
- 함수 안에 존재하는 변수나 함수 선언에 대한 정보를 기억하고 있다가 실행시킨다.
- 함수 블록`{}` 안에서만 유효하다.
- `var` 변수 선언과 `함수 선언문` 에서만 호이스팅이 일어난다.

그래서 함수 선언문은 맨 위로 끌어올리기 때문에 타입이 `function` 이고, **함수 표현문은 끌어 올려지지 않기 때문에 변수의 스코프 규칙을 그대로 따른다.**

```jsx
// lexical scope 예제
it ('', function {
    let message = 'Outer';

    function getMessage() {
      return message;
    }

    function shadowGlobal() {
      let message = 'Inner';
      return message;
    }

    function shadowGlobal2(message) {
      return message;
    }

    function shadowParameter(message) {
      message = 'Do not use parameters like this!';
      return message;
    }

    expect(getMessage()).to.equal('Outer');
    expect(shadowGlobal()).to.equal('Inner');
    expect(shadowGlobal2('Parameter')).to.equal('Parameter');
    expect(shadowParameter('Parameter')).to.equal('Do not use parameters like this!');
    expect(message).to.equal('Outer');
})
```

```jsx
// 클로저(closure) 예제
it ('', function {
    function increaseBy(increaseByAmount) {
      return function (numberToIncrease) {
        return numberToIncrease + increaseByAmount;
      };
    }

    const increaseBy3 = increaseBy(3);
    const increaseBy5 = increaseBy(5);

    expect(increaseBy3(10)).to.equal(13);  // increaseBy(3)(10)
    expect(increaseBy5(10)).to.equal(15);  // increaseBy(5)(10)
    expect(increaseBy(8)(6) + increaseBy(5)(9)).to.equal(28);
})
```

스코프와 클로저의 규칙을 잘 이해하고 있는지 확인하는 문제였다. 이 부분은 간단한 문제라 손쉽게 넘어갔다.

```jsx
// lexical scope와 closure 예제
it ('', function {
    let age = 27;
    let name = 'jin';
    let height = 179;

    function outerFn() {
      let age = 24;
      name = 'jimin';
      let height = 178;

      function innerFn() {
        age = 26;
        let name = 'suga';
        return height;
      }

      innerFn();

      expect(age).to.equal(26);
      expect(name).to.equal('jimin');  // 새로 선언한 name은 메모리에 저장이 되지 않는다.

      return innerFn;
    }

    const innerFn = outerFn();

    expect(age).to.equal(27);
    expect(name).to.equal('jimin');
    expect(innerFn()).to.equal(178);  // 외부 변수인 height의 값을 리턴받는다.
});
```

이 문제에서 시간이 제일 오래 걸렸었다. 메모리 상에 남아있는 값과 현재 함수를 요청해서 리턴되는 값의 차이를 이해하고, 다시보니 쉬운 문제였다 .. 

<br>

### 화살표 함수 (Arrow Function) 예제

```jsx
// 기본적인 함수 로직
/* const add = function (x, y) {
      return x + y
    }

    expect(add(5, 8)).to.eql(13) */

// 화살표 함수
it ('', function {
    const add = (x, y) => {
      return x + y
    }
    expect(add(10, 20)).to.eql(30)

    // 리턴을 생략할 수 있습니다
    const subtract = (x, y) => x - y
    expect(subtract(10, 20)).to.eql(-10)

    // 필요에 따라 소괄호를 붙일 수도 있습니다
    const multiply = (x, y) => (x * y)
    expect(multiply(10, 20)).to.eql(200)

    // 파라미터가 하나일 경우 소괄호 생략이 가능합니다
    const divideBy10 = x => x / 10
    expect(divideBy10(100)).to.eql(10)
})
```

기본적인 함수에서 `function` 키워드를 생략하고 화살표(`=>`)를 붙여 사용할 수 있다.

```jsx
// 화살표 함수를 이용하여 클로저를 표현하는 예제
it ('', function {
    const adder = x => {
      return y => {
        return x + y
      }
    }

    expect(adder(50)(10)).to.eql(60)

    const subtractor = x => y => {
      return x - y
    }

    expect(subtractor(50)(10)).to.eql(40)

    const htmlMaker = tag => textContent => `<${tag}>${textContent}</${tag}>`
    expect(htmlMaker('div')('code states')).to.eql('<div>code states</div>')

    const liMaker = htmlMaker('li')
    expect(liMaker('1st item')).to.eql('<li>1st item</li>')
    expect(liMaker('2nd item')).to.eql('<li>2nd item</li>')
})
```

<br>

### 원시 자료형과 참조 자료형 예제

```jsx
// 원시 자료형을 변수에 할당하는 예제
it ('', function {
    let overTwenty = true;
  	let allowedToDrink = overTwenty;

    overTwenty = false;
    expect(overTwenty).to.equal(false);
    expect(allowedToDrink).to.equal(true);
})
```

```jsx
// 원시 자료형 또는 원시 자료형의 데이터를 함수의 전달인자로 전달하는 예제
it ('', function {
    let currentYear = 2020;
    function afterTenYears(year) {
      year = year + 10;
    }
    afterTenYears(currentYear);
    expect(currentYear).to.equal(2020);
    function afterTenYears2(currentYear) {
      currentYear = currentYear + 10;
      return currentYear;
    }
    let after10 = afterTenYears2(currentYear);
    expect(currentYear).to.equal(2020);
    expect(after10).to.equal(2030);
})
```

`원시 자료형` 은 값 자체의 복사가 일어난다. 함수도 변수와 똑같이 데이터를 할당한다.
원시자료형은 6가지의 데이터(string, number, bigint, boolean, undefined, symbol, (null))를 말한다.

```jsx
it ('', function {
    const person = {
      son: {
        age: 9,
      },
    };

    const boy = person.son;
    boy.age = 20;
    expect(person.son.age).to.equal(20);
    expect(person.son === boy).to.equal(true);  // 주소가 동일
    expect(person.son === { age: 9 }).to.equal(false); 
    expect(person.son === { age: 20 }).to.equal(false);
})
```

`참조 자료형` 은 원시 자료형이 아닌 모든 것은 참조 자료형이다. 배열과 객체, 함수가 대표적이다.

```jsx
const nums1 = [1, 2, 3];
const nums2 = [1, 2, 3];
expect(nums1 === nums2).to.equal(false);
```

위에 코드처럼 배열 nums1과 배열 num2에는 동일한 데이터 [1, 2, 3]이 들어있는 게 분명해 보이는데, 이 둘은 같지가 않다. 사실 변수 num1와 num2는 배열이 아니고, 참조 타입의 변수에는 (데이터에 대한) 주소만이 저장된다는 것을 잊으면 안된다. 

<br>

### 배열 (Array) 예제

```jsx
it ('', function {
    // Array 메소드인 slice 예제
    const arr = ['peanut', 'butter', 'and', 'jelly'];

    expect(arr.slice(1)).to.deep.equal(['butter', 'and', 'jelly']);
    expect(arr.slice(0, 1)).to.deep.equal(['peanut']);
    expect(arr.slice(0, 2)).to.deep.equal(['peanut', 'butter']);
    expect(arr.slice(2, 2)).to.deep.equal([]);
    expect(arr.slice(2, 20)).to.deep.equal(['and', 'jelly']);
    expect(arr.slice(3, 0)).to.deep.equal([]);
    expect(arr.slice(3, 100)).to.deep.equal(['jelly']);
})
```

`arr.slice` 는 arr의 값을 복사하여 새로운 배열을 리턴한다. 또 `.slice(0)` 은 배열의 전체를 복사한다는 것을 잊으면 안된다 !!

<br>

### 객체 (Object) 예제

```jsx
// Object를 함수의 전달인자로 활용하는 예제
it ('', function {
    const obj = {
      mastermind: 'Joker',
      henchwoman: 'Harley',
      relations: ['Anarky', 'Duela Dent', 'Lucy'],
      twins: {
        'Jared Leto': 'Suicide Squad',
        'Joaquin Phoenix': 'Joker',
        'Heath Ledger': 'The Dark Knight',
        'Jack Nicholson': 'Tim Burton Batman',
      },
    };

    function passedByReference(refObj) {
      refObj.henchwoman = 'Adam West';
    }
    passedByReference(obj);
    expect(obj.henchwoman).to.equal('Adam West');

    const assignedObj = obj;
    assignedObj['relations'] = [1, 2, 3];
    expect(obj['relations']).to.deep.equal([1, 2, 3]);

    const copiedObj = Object.assign({}, obj);
    copiedObj.mastermind = 'James Wood';
    expect(obj.mastermind).to.equal('Joker');

    obj.henchwoman = 'Harley';
    expect(copiedObj.henchwoman).to.equal('Adam West');

    delete obj.twins['Jared Leto'];
    expect('Jared Leto' in copiedObj.twins).to.equal(false);
})
```

다른 부분은 괜찮았는데 마지막 코드는 왜 이렇게 답이 나오지?? 라는 생각을 들게하였다.
`Object.asign` 을 통한 복사는 참조 변수의 주소만 복사하기 때문이라고 하였는데, 이해가 잘 되지 않아서 이 얕은 복사와 깊은 복사에 관련되어 더 많은 학습이 필요할 것 같다.

<br>

### Spread 구문 예제

```jsx
// Spread 예제
it ('', function {
    const spread = [];
    const arr = [0, ...spread, 1];
    expect(arr).to.deep.equal([0, 1]);

	const arr1 = [0, 1, 2];
    const arr2 = [3, 4, 5];
    const concatenated = [...arr1, ...arr2];  // arr1.concat(arr2);
    expect(concatenated).to.deep.equal([0, 1, 2, 3, 4, 5]);
})
```

빈 배열에 전개 구문을 사용할 경우에는 아무런 값이 출력되지 않는다.

```jsx
// Rest Parameter를 활용하는 예제
it ('', function {
    function sum(...nums) {
      let sum = 0;
      for (let i = 0; i < nums.length; i++) {
        sum = sum + nums[i];
      }
      return sum;
    }
    expect(sum(1, 2, 3)).to.equal(6);
    expect(sum(1, 2, 3, 4)).to.equal(10);
})
```
`Rest Parameter` 는 전달인자의 수가 정해져 있지 않는 경우에 유용하게 사용할 수 있다.

```jsx
// Rest Parameter를 활용하는 예제 2
it ('', function {
    function getAllParams(required1, required2, ...args) {
          return [required1, required2, args];
        }
        expect(getAllParams(123)).to.deep.equal([123, undefined, []]);

        function makePizza(dough, name, ...toppings) {
          const order = `You ordered ${name} pizza with ${dough} dough and ${toppings.length} extra toppings!`;
          return order;
        }

        expect(makePizza('original')).to.equal('You ordered undefined pizza with original dough and 0 extra toppings!');
        expect(makePizza('thin', 'pepperoni')).to.equal('You ordered pepperoni pizza with thin dough and 0 extra toppings!');
        expect(makePizza('napoli', 'meat', 'extra cheese', 'onion', 'bacon')).to.equal('You ordered meat pizza with napoli dough and 3 extra toppings!');
})
```

`Rest Parameter` 는 전달인자의 일부만 사용할 수도 있다. 또 항상 배열인 것을 잊으면 안된다!!

### 구조 분해 할당(Destructing Assignment) 예제

**Array**
```jsx
// Array을 분해하는 예제
it ('', function {
    const array = ['code', 'states', 'im', 'course'];

    const [first, second] = array;
    expect(first).to.eql('code');
    expect(second).to.eql('states');

    const result = [];
    function foo([first, second]) {
      result.push(second);  // 'states'
      result.push(first);  // 'code'
    }

    foo(array);
    expect(result).to.eql(['states', 'code']);
})
```

```jsx
// rest/spread 문법을 배열에 적용하는 예제
it ('', function {
    const array = ['code', 'states', 'im', 'course'];
    const [start, ...rest] = array;  
    expect(start).to.eql('code');
    expect(rest).to.eql(['states', 'im', 'course']);
})
```
`rest` 문법을 이용한 간단한 문제였다.

주의해야 할 점은 **할당하기 전 왼쪽에 rest 문법 이후에 쉼표가 올 수 없다**는 것이다.
```const [first, ...middle, last] = array;```

위 코드는 잘못된 예시를 보여준다.

#### Object

```jsx
// 객체를 분해
it ('', function {
    const student = { name: '박해커', major: '물리학과' }

    const { name } = student
    expect(name).to.eql('박해커')
})
```
`{ name }` 으로 객체를 접근하여 값을 가져오는 것을 잘 알고있는지 넘어가는 부분이었다.

#### rest/spread

```jsx
// rest/spread 문법을 객체에 적용하는 예제
it ('', function {
    const student = { name: '최초보', major: '물리학과' }
    const { name, ...args } = student  // student = {name: '최초보', major: '물리학과'}

    expect(name).to.eql('최초보')
    expect(args).to.eql({major: '물리학과'})
})
```

```jsx
// rest/spread 문법을 객체에 적용하는 예제 2
it ('', function {
    const student = { name: '최초보', major: '물리학과', lesson: '양자역학', grade: 'B+' }

    function getSummary({ name, lesson: course, grade }) {
      return `${name}님은 ${grade}의 성적으로 ${course}을 수강했습니다`
    }

    expect(getSummary(student)).to.eql('최초보님은 B+의 성적으로 양자역학을 수강했습니다')
})
```

```jsx
// rest/spread 문법을 객체에 적용하는 예제 3
it ('', function {
    const user = {
      name: '김코딩',
      company: {
        name: 'Code States',
        department: 'Development',
        role: {
          name: 'Software Engineer'
        }
      },
      age: 35
    }

    const changedUser = {
      ...user,
      name: '박해커',
      age: 20
    }

    const overwriteChanges = {
      name: '박해커',
      age: 20,
      ...user
    }

    const changedDepartment = {
      ...user,
      company: {
        ...user.company,
        department: 'Marketing'
      }
    }

    expect(changedUser).to.eql({name: '박해커', company: 
          {name: 'Code States', department: 'Development', role: {name: 'Software Engineer'}}, age: 20})

    expect(overwriteChanges).to.eql({name: '김코딩', company: 
          {name: 'Code States', department: 'Development', role: {name: 'Software Engineer'}}, age: 35})

    expect(changedDepartment).to.eql({name: '김코딩', company: 
          {name: 'Code States', department: 'Marketing', role: {name: 'Software Engineer'}}, age: 35})
})
```

아무래도 실무에서 `rest` 와 `spread` 문법을 주로 사용하다보니, 여러 번 활용하는 문제가 반복되어 출제된 것 같다.

<br>

## Feelings ...
그동안 배웠던 문법들을 복습하는 과제였다. 그러다보니 주로 간단한 문제와 그에 알맞는 값을 유추하는 것이라 어려운 문제는 아니였다. 그래서 쉽게 풀 수 있는 문제였는데 중간중간 헷갈리는 문제가 몇 개 있었다. 그럴 때 `console` 을 이용하여, 문제를 해결해나갈 수 있었다.

## Findings ...
과제를 통해서 새롭게 알게된 부분이 `rest` 문법에서** 할당하기 전 왼쪽에 rest 문법 이후에 쉼표가 올 수 없다**는 것이였다. 

```jsx
let arr = ['one', 'two', 'three', 'four', 'five'];
```

우선 배열을 선언하고, 이 배열을 값으로 할당하기 위해서 `const [a, ...b] = arr` 으로 작성할 수는 있지만, `const [a, ...b, c] = arr` 이렇게 작성할 수는 없다.

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)