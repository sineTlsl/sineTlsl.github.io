---
layout: post
title: 패스트캠퍼스 JavaScript 코딩테스트 131개 예제 & CS지식으로 끝내기 강의 1주차
date: 2023-04-22 13:05:00 +900
categories: [CHALLENGE, Upskill JS CodingTest]
tags: [패스트캠퍼스, 패캠, fastcampus, 자바, 자바스크립트, 파이썬, 코딩테스트, 패스트캠퍼스후기, 코딩교육, 코딩자격증]
image: 
  path: https://user-images.githubusercontent.com/97720335/233675262-28867749-fd9d-4193-924e-8918d1a85517.png
  width: 700
  alt: UPSKILL JS CodingTest 표지
---

# 📬 본격적으로 강의를 들어가기 전 ...
알고리즘이 비교적 약한 편이라, 알고리즘 공부를 어디서부터 어떻게 시작해야 할지 막막해서 손을 못 대고 있었는데 주변에서 동빈나 강사님의 알고리즘을 추천해 줘서 이번 기회에 듣게 되었다 😛 <br>

항상 *알고리즘 공부해야지* 라고 생각만 하고 알고리즘 공부를 제대로 하지 않았었는데, 나한테 코딩 테스트와 같은 문제를 줬을 때 어떤 식으로 문제를 해결해나가야 하는지 많은 고민과 효율적이지 못한 방식으로 문제를 풀어나가는 것 같았다. <br>

동빈나 강사님의 알고리즘 강의를 듣게 된 이후로 데일리 루틴으로 알고리즘 문제 풀기를 넣게 되었다. 뭐든지 꾸준하게 하면 늘 수밖에 없으니까 당장 급하게 하는 것보다 정확하게 짚고 넘어가는 걸 중점으로 두고 학습할 예정이다.

# 🔗 Part1 - Ch01 핵심 내용 (주관적)
## 1. 코딩 테스트 알아보기
- 코딩 테스트는 온라인과 오프라인으로 분류된다.
- 자신만의 소스코드를 관리하는 것이 중요하다.
- `구현`, `DFS/BFS(탐색)`, `탐욕 알고리즘` 유형이 출제 빈도가 높은 편이다.

## 2. 요구사항에 따라 적절한 알고리즘 설계하기
- 제일 먼저 확인해야 하는 내용은 **시간 제한(수행 시간 요구사항)**이다.

### e.g. 시간 제한이 1초인 문제를 만났을 때
- 의 범위가 500인 경우: 시간복잡도가 $O(N^3)$ 인 알고리즘을 설계하면 문제를 풀 수 있다.
- $N$의 범위가 2,000인 경우: 시간복잡도가 $O(N^2)$ 인 알고리즘을 설계하면 문제를 풀 수 있다.
- $N$의 범위가 100,000인 경우: 시간복잡도가 $O(NlogN)$ 인 알고리즘을 설계하면 문제를 풀 수 있다.
- $N$의 범위가 10,000,000인 경우: 시간복잡도가 $O(N)$ 인 알고리즘을 설계하면 문제를 풀 수 있다.

## 3. JavaScript 기본 출력
알고리즘 문제를 풀 때, 표준 출력을 `console.log()` 를 이용한다.

```js
console.log("Hello World!");
```

### ❓ 만약 문제를 풀 때 출력 과정만으로 시간 초과를 받을 경우에는?
여러 출력 결과를 한 줄에 하나씩 출력할 때 매번 `console.log()` 를 실행하지 않고, 하나의 문자열에 결과를 저장해서 한 꺼번에 출력하는 것이 대게 더 빠르게 수행된다.

```js
let result = "";

for (let i = 0; i <= 100; i++) {
  result += i + "\n";
}
console.log(result);
```

## 4. JavaScript 기본 입력 - `fs 모듈`
- 입력이 `txt` 파일 형태로 주어지는 경우, 파일 시스템 모듈을 사용한다.

**e.g.** `/dev/stdin/` 적힌 텍스트를 읽어오는 경우 다음과 같이 입력한다.

```js
let fs = require('fs');
let input = fs.readFileSync('/dev/stdin').toString().split('\n');
```

## 5. JavaScript 기본 입력 - `readline 모듈`
한 줄씩 입력을 받아서 처이하려 정답을 출력할 때는 `readline` 모듈을 사용할 수 있다.

```js
const rl = require("readline").createInterface({
  input: process.stdin,
  output: process.stdout,
});

let input = [];
rl.on("line", function (line) {
  // 콘솔 입력 창에서 줄바꿈(enter)를 입력할 때마다 호출
  input.push(line);
}).on("close", function () {
  // 콘솔 입력 창에서 Ctrl + C 혹은 Ctrl + D를 입력하면 호출 (입력의 종료)
  console.log(input);
  process.exit();
});
```

# 📃 Week 01 Review
<center><img src="https://user-images.githubusercontent.com/97720335/233762912-4c107493-5be9-4c66-a1c8-f11cb70ebfd6.png" width="80%" /></center>

<center><img src="https://user-images.githubusercontent.com/97720335/233764292-3cffe322-277a-43a0-ae0a-ca29680ba03e.JPG" width="80%" /></center>

코딩 테스트가 무엇인 지, 문제 풀이를 위한 JavaScript 핵심 문법은 무엇인 지 알아보는 시간이었다. JavaScript의 기본적인 `조건문`, `반복문`, `배열`, `문자열` 부분은 강의만 듣고 바로 문제를 풀어보았고, 하나하나 문제를 해결 해나갈 때마다 뿌듯했다. 앞으로 더 기대가 되는 알고리즘!! 🔥

<center><img src="https://user-images.githubusercontent.com/97720335/233764572-5775ce6c-9f20-47e6-be70-948c3e93c105.png">
</center>

밑에 링크는 내가 생성한 깃 리포지토리다.
 
[[My Repository] Daily Algorithmic Problem Solving Repository](https://github.com/sineTlsl/Algorithm)

<br>

<https://fastcampus.co.kr/dev_online_upjscodingtest>

> 본 포스팅은 패스트캠퍼스 환급 챌린지 참여를 위해 작성되었습니다. 
{: .prompt-info}