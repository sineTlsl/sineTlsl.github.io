---
layout: post
title: "[S1-Unit06] Calculator 구현 회고"
date: 2023-06-01 17:32:00 +900
lastmod: 2023-06-01 17:32:00 +900
categories: [CODESTATES, Section01]
tags: [CODESTATES, 코드스테이츠, Section01, 회고]
use_math: true
image: 
  path: https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/8ac2c1a4-622c-4040-84cc-dd9345b7780d
  width: 700
  alt: 구현한 계산기 사진
---

# Advanced Challenge & Nightmare Test
> **Step1 - 숫자 버튼을 누르고 화면에 숫자를 입력하기**
- 숫자 버튼을 눌렀을 때, 계산기의 화면에 숫자가 보여야 한다.
- 숫자 버튼을 여러 번 눌렀을 때, 계산기 화면에 숫자가 이어붙여져야(concatenation) 한다.

> **Step2 - 연산자 버튼 동작시키기**
- 연산자 버튼을 눌렀을 때, 계산기 화면에 보이는 숫자를 따로 저장하고 계산할 준비해야 한다.<br>

> **Step3 - Enter 버튼, AC 버튼 동작시키기**
- Enter 버튼을 눌렀을 때, 이전에 저장한 숫자와 계산기 화면에 보이는 숫자를 계산한 결과를 화면에 보여줘야 한다.
- 두 정수의 사칙연산을 수행하는 calculate 함수를 작성한다.
- AC 버튼을 누르면 초기 상태로 돌아갈 수 있어야 한다.
- 미리 작성된 SpecRunner.html 파일을 열고, Requirements을 전부 구현했는지 테스트를 돌려서 확인 한다.

>**Step4 - Nightmare 도전하기**
- 혹시라도 발생할 수 있는 특이한 작동 시 대비하여, 더욱 정교한 계산기를 구현한다.

<br>

## 🪵 와이어프레임 
우선 나는 계산기를 다음과 보이는 사진처럼 뼈대를 잡았다. 제일 크게 계산기 결과 화면과 버튼 화면, 이미지 화면 3개로 구성하게 되었다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/a48b3efb-9226-4c52-aba0-b6cb8ac22446" width="80%" />
</center>

## 👩🏻‍💻 MY CODE
### 1. HTML 코드

계산 결과화면을 다른 분들 `input` 으로 많이 하시는 것 같은데 나는 `div` 가 좀 더 익숙해서 그런지 div로 사용하게 되었다.

```html
<body>
  <div id="wrap">
    <div id="result">
      <div id="result_text">0</div>
    </div>
    <div id="calcBtn_sec">
      <div class="calcBtn">
        <button class="clear double">AC</button>
        <button class="operator">%</button>
        <button class="operator">/</button>
      </div>
      <div class="calcBtn">
        <button class="number">7</button>
        <button class="number">8</button>
        <button class="number">9</button>
        <button class="operator">x</button>
      </div>
      <div class="calcBtn">
        <button class="number">4</button>
        <button class="number">5</button>
        <button class="number">6</button>
        <button class="operator">-</button>
      </div>
      <div class="calcBtn">
        <button class="number">1</button>
        <button class="number">2</button>
        <button class="number">3</button>
        <button class="operator">+</button>
      </div>
      <div class="calcBtn">
        <button class="number double">0</button>
        <button class="decimal">.</button>
        <button class="calculate">=</button>
      </div>
    </div>
    <div class="png_sec">
      <span>We</span>
      <img src="./webare.png">
      <span>Bare</span>
    </div>
  </div>
  <script src="./script.js"></script>
</body>
```

### 2. CSS 코드

나는 심플한 디자인을 좋아하여 깔끔하게 구현하였다. 그러다보니 여러 색을 사용하지 않았고, 밋밋할 수 있는 요소를 그림자 효과를 주어 생동감을 주게되었다.

```css
* {
  box-sizing: border-box;
}

html,
body {
  margin: 0;
  padding: 0;
  font-family: 'Yeon Sung', cursive;
}

body {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-color: #e0e0e0; 
}

img {
  width: 35%;
}

#wrap {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  max-width: 400px;
  width: 100%;
  max-height: 690px;
  height: 100vh;

  border-radius: 30px;
  background: #e0e0e0;
  box-shadow: 15px 15px 15px #bebebe, -15px -15px 15px #bebebe;
}

#result {
  display: flex;
  align-items: flex-end;
  justify-content: flex-end;
  background-color: #eabcb8;
  height: 17%;
  width: 90%;
  padding: 0 20px 10px 0;
  border-radius: 10px 10px 0 0;
  margin-top: 10%;
}

#result_text {
  border: 0;
  width: 90%;
  font-size: 50px;
  text-align: right;
  font-weight: 500;
  text-shadow: 2px 5px 5px rgb(172, 109, 109);
}

#calcBtn_sec {
  background-color: #fff;
  height: 55%;
  width: 90%;
  border-radius: 0 0 10px 10px;

  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  
  padding: 0 0.5rem;
  overflow: hidden auto;
}

#calcBtn_sec .calcBtn {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  margin: 1rem;
  height: 10%;
}


#calcBtn_sec .calcBtn .double {
  width: 24rem;
}

#calcBtn_sec .calcBtn .clear, .number, .operator, .decimal, .calculate {
  font-size: 17px;
  margin: 0.2rem;
  font-weight: 900;
}

button {
  background-color: #eee;
  border: none;
  padding: 1rem;
  font-size: 1rem;
  width: 10rem;
  border-radius: 1rem;
  color: lightcoral;
  box-shadow: 0 0.4rem #dfd9d9;
  cursor: pointer;
  font-family: 'Yeon Sung', cursive;
}

button:hover {
  color: white;
  box-shadow: 0 0.2rem #dfd9d9;
  transform: translateY(0.2rem);
}

button:hover:not(:disabled) {
  background: lightcoral;
  color: white;
  text-shadow: 0 0.1rem #bcb4b4;
}

button:disabled {
  cursor: auto;
  color: grey;
}

.png_sec {
  display: flex;
  justify-content: center;
  align-items: flex-end;
  padding-top: 5%;
}
```
<br>

### <span style="color: #535353">3. JavaScript 코드</span>
```javascript
const calculator = document.querySelector('#wrap'); 
const buttons = calculator.querySelector('#calcBtn_sec');
const display = document.querySelector('#result_text'); 

// 두 정수의 사칙연산을 수행하는 calculate 함수
function calculate(n1, operator, n2) {
  let result = 0;

  if (operator === '+') {
    result = Number(n1) + Number(n2);
  } else if (operator === "-") {
    result = Number(n1) - Number(n2);
  } else if (operator === "x") {
    result = Number(n1) * Number(n2);
  } else if (operator === "/") {
    result = Number(n1) / Number(n2);
  } else if (operator === "%") {
    result = Number(n1) % Number(n2);
  }
  result = result.toString();

  // 계산 결과의 값이 현재 계산기 크기보다 커지지 않도록 글자수 조정
  return result.length > 7 ? Number(result).toPrecision(8) : result;
}

let firstNum, operatorForAdvanced, previousKey, previousNum;

buttons.addEventListener('click', function (event) {
  const target = event.target; 
  const action = target.classList[0];
  const buttonContent = target.textContent; 

  if (target.matches('button')) {
    // 숫자 버튼을 누르고 화면에 입력하기
    if (action === 'number') {
      if (display.textContent === '0') {
        display.textContent = buttonContent;
      } else {
        if (display.textContent !== firstNum) {
          display.textContent += buttonContent;
        } else {
          display.textContent = buttonContent;
        }
      }
      previousKey = 'number';
    }

    // 연산자 버튼 동작시키기
    if (action === 'operator') {
      if (firstNum && operatorForAdvanced && previousKey !== 'operator' && previousKey !== 'calculate') {
        display.textContent = calculate(firstNum, operatorForAdvanced, display.textContent);
      }
      firstNum = display.textContent; 
      operatorForAdvanced = buttonContent;

      previousKey = 'operator';
    }
    
    // 소수점 버튼 동작시키기
    if (action === 'decimal') {
      if (!display.textContent.includes('.')) {
        if (previousKey !== 'operator') {
          display.textContent += buttonContent;
        } else {
          display.textContent = '0.'; 
        }
      }
      previousKey = 'decimal';
    }

    // AC 버튼 동작시키기
    if (action === 'clear') {
      firstNum = '';
      operatorForAdvanced = '';
      display.textContent = '0';

      previousKey = 'clear';
    }

    // Enter 버튼 동작시키기
    if (action === 'calculate') {
      previousNum = display.textContent;
      if (operatorForAdvanced === undefined || operatorForAdvanced === '') {
        display.textContent = previousNum;
      } else {
        if (previousKey === 'calculate') {
          display.textContent = calculate(previousNum, operatorForAdvanced, firstNum);
        } else {
          display.textContent = calculate(firstNum, operatorForAdvanced, display.textContent);
        }
      }
      previousKey = 'calculate';
    }
  }
});
```

<br>

## Feelings ...
틀이 있었는데 그 틀을 깨면서 엉터리 코드를 작성하였다.. ㅎㅎ 나중에 주어진 변수로만 사용할려다보니까 갑자기 머리가 아프기 시작했고.. 어쩌다.. 어쩌다 정신놓고 하다보니 완성하게 되었다. 원래 코드는 조금 더 복잡하고 기능이 부족한 느낌이였는데, 이번에 과제를 하면서 내가 놓쳤던 부분의 정교한 계산까지 할 수 있는 기능을 구현하여 더 깔끔한 코드로 탄생하였다 🐥 기존 CSS는 저게 아니었는데 좀 더 심플하게 수정해봤다. 사진은 내가 제일 좋아하는 위베어 이미지로 ..!!

## Findings ...
코드를 구성하기 전에 과제에서 기본적으로 주어진 틀인 `textContent` 를 처음으로 사용하게 되었다.
```js
const buttonContent = target.textContent; // 클릭된 HTML 엘리먼트의 텍스트 정보를 가져옵니다.
```

`innerText` 를 지금까지 사용하였던 나는 `textContent` 가 생소하였다. 그러다 둘의 차이점을 찾아보게 되었고 새로 알게된 내용은 다음과 같다.

### innerText와 textContent 차이점
| innerText | textContent |
| :---: | :---: |
| **사람이 읽을 수 있는 요소**만 처리 | `<script>` 와 `<style>` 요소를 포함한 모든 요소의 콘텐츠를 가져옴 |
| 스타일링을 고려하며 **숨겨진** 요소의 텍스트는 반환하지 않음 | 노드의 모든 요소를 반환 |

- 또한, `innerText` 의 CSS 고려로 인해, `innerText` 값을 읽으면 최신 계산값을 반영하기 위해 [리플로우](https://developer.mozilla.org/ko/docs/Glossary/Reflow)가 발생한다. (리플로우 계산은 비싸므로 가능하면 피해야 한다.)
- Internet Explorer 기준, innerText를 수정하면 요소의 모든 자식 노드를 제거하고, 모든 자손 텍스트 노드를 영구히 파괴한다. 이로 인해, 해당 텍스트 노드를 이후에 다른 노드는 물론 같은 노드에 삽입하는 것도 불가능하다.