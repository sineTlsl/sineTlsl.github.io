---
layout: post
title: 패스트캠퍼스 JavaScript 코딩테스트 131개 예제 & CS지식으로 끝내기 강의 2주차
date: 2023-04-30 17:30:00 +900
lastmod: 2023-04-30 17:30:00 +900
categories: [CHALLENGE, Upskill JS CodingTest]
tags: [패스트캠퍼스, 패캠, fastcampus, 자바, 자바스크립트, 파이썬, 코딩테스트, 패스트캠퍼스후기, 코딩교육, 코딩자격증]
use_math: true
image: 
  path: https://user-images.githubusercontent.com/97720335/233675262-28867749-fd9d-4193-924e-8918d1a85517.png
  width: 700
  alt: UPSKILL JS CodingTest 표지
---

# 🔗 Part2 - 자료 구조 핵심 내용 (주관적)
## 자료구조란?
- 자료구조는 다수의 **자료(data)** 를 담기 위한 구조다.
- 데이터의 수가 많아질수록 효율적인 자료구조가 필요하다.
- 데이터를 효과적으로 저장하고, 처리하는 방법에 대해 이해할 필요가 있다.
  - 자료구조를 제대로 이해하지 못하면 불필요하게 메모리와 계산을 낭비할 여지가 있다.
- `구현`, `DFS/BFS(탐색)`, `탐욕 알고리즘` 유형이 출제 빈도가 높은 편이다.

<br>

## 자료구조의 종류
자료구조의 종류는 `선형 구조(linear data structure)` 와 `비선형 구조(non-linear data structure)` 로 분리된다. 

### 선형 구조
> `선형 자료구조` 는 하나의 데이터 뒤에 다른 데이터가 하나 존재하는 자료구조다.

- 배열(array)
- 연결 리스트(linked list)
- 스택(stack)
- 큐(queue)

### 비선형 구조
> `비선형 자료구조` 는 하나의 데이터 뒤에 다른 데이터가 여러 개 올 수 있는 자료구조다.

- 트리(tree)
- 그래프(graph)

<br>

# 📃 Week 02 Review
이번 주는 스택 부분까지 공부를 하였다. 내가 이해한 부분은 다음과 같다고 생각하여 그림을 그려보았다.

<center><img src="https://user-images.githubusercontent.com/97720335/235344906-ac8e1083-016a-43a1-a882-4ba978ca27b5.jpeg" width="80%" /></center>

자료구조 공부를 진행하면서, 배열은 원래 자주 사용했던 부분이어서 따로 문제를 풀어보진 않았고 스택 문제를 풀어보았다.

<https://www.acmicpc.net/problem/10828>

<center><img src="https://user-images.githubusercontent.com/97720335/235342110-eba5d4fc-56bb-4f59-8d8c-9b6b94b6d061.png" width="80%" /></center>

```js
let fs = require("fs");
let input = fs.readFileSync('./dev/stdin').toString().trim().split("\n");
const [n, ...arr] = input;

console.log(solution(n, arr));

function solution (n, arr) {
  let stack = [];
  let result = [];

  arr.forEach(el => {
    const cmd = el.split(' ')[0];
    if (cmd === 'push') {
      const item = el.split(' ')[1];
      stack.push(item)
    } else if (cmd === 'pop') {
      if (stack.length === 0) { result.push(-1); } 
      else {
        result.push(stack[stack.length - 1]);
        stack.pop();
      }
    } else if (cmd === 'size') {
      result.push(stack.length);
    } else if (cmd === 'empty') {
      stack.length === 0 ? result.push(1) : result.push(0);   
    } else if (cmd === 'top') {
      stack.length === 0 ? result.push(-1) : result.push(stack[stack.length - 1]);
    }
  });

  return result.join('\n');
}
```
문제를 풀었는데, 가독성이 좀 떨어지나..? 생각도하게 되었는데 나중에 다른 식으로 풀어보고싶다.

<center><img src="https://user-images.githubusercontent.com/97720335/235344836-abdfd866-e497-4732-b0b7-8a5cf279b9c7.png" width="80%" /></center>

<br>

<https://fastcampus.co.kr/dev_online_upjscodingtest>

> 본 포스팅은 패스트캠퍼스 환급 챌린지 참여를 위해 작성되었습니다. 
{: .prompt-info}