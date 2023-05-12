---
layout: post
title: 패스트캠퍼스 JavaScript 코딩테스트 131개 예제 & CS지식으로 끝내기 강의 4주차
date: 2023-05-12 17:26:00 +900
lastmod: 2023-05-12 17:31:00 +900
categories: [CHALLENGE, Upskill-JS-CodingTest]
tags: [패스트캠퍼스, 패캠, fastcampus, 자바, 자바스크립트, 파이썬, 코딩테스트, 패스트캠퍼스후기, 코딩교육, 코딩자격증]
use_math: true
image: 
  path: https://user-images.githubusercontent.com/97720335/233675262-28867749-fd9d-4193-924e-8918d1a85517.png
  width: 700
  alt: UPSKILL JS CodingTest 표지
---

# 🔗 Part1. Ch03 - 정렬 정리 (1/2) (주관적)
## 선택 정렬 (Selection Sort) 정리

**정렬 알고리즘 중에 기본이 되면서 비효율적인 알고리즘이 `선택 정렬` 이다.**

- 선택 정렬은 비효율적이지만 그 동작 방식이 직관적이기 때문에 외우고 있지 않아도, 필요할 때 떠올려서 구현할 수 있을 정도로 구현 난이도가  다른 정렬 알고리즘에 비해 낮다.
- `‘매번 낮은 것을 선택한다’` 만 기억하면 된다.
- 시간 복잡도는 비효율적이다.

## 버블 정렬 (Bubble Sort) 정리
- 최악의 경우 시간 복잡도 $O(N^2)$을 보장한다.
    - 선택 정렬보다 소요 시간이 더 걸린다.
- 이미 정렬된 배열에 대하여 모든 비교가 필요하므로, 굉장히 비효율적인 정렬 알고리즘 중 하나에 속한다.

## 삽입 정렬 (Insertion Sort) 정리
- 선택 정렬과 버블 정렬보다 빠르다.
- 삽입 정렬은 위치를 변경할 요소의 왼쪽 위치들은 정렬이 되어있어야 한다.
- 삽입 정렬이란 각 원소를 적절한 위치에 **삽입**하는 정렬 기법이다.
- 매 단계에서 현재 처리 중인 원소가 삽입될 위치를 찾기 위해 약 $N$번의 연산이 필요하다.
- 결과적으로 약 N개의 단계를 거친다는 점에서 최악의 경우 $O(N^2)$의 시간 복잡도를 가져 비효율적인 정렬 알고리즘이라고 할 수 있다.

## 병합 정렬(Merge Sort) 정리
- 병합 정렬은 전형적인 분할 정복 알고리즘이다.
- 분할 정복은 일반적으로 재귀 함수를 이용하여 구현한다.
  - 큰 문제를 작은 문제로 “분할하는 방식이 동일한” 경우가 많기 때문

<br>

## JavaScript 정렬 라이브러리
- JavaScript에서는 배열에 포함된 데이터를 정렬하는 `sort()` 함수를 제공한다.
- 최악의 경우 시간 복잡도 $O(N log N)$을 보장한다.

`정수` 에 대한 정렬은 다음과 같이 할 수 있다.
```js
let arr = [1, 8, 5, 9, 21, 3, 7, 2, 15];

arr.sort((a, b) => a - b); // 오름차순
arr.sort((a, b) => b - a); // 내림차순
```

<br>

# 📃 Week 04 Review
이번 주애는 정렬에 관한 강의를 들었다. 정렬에 대한 공부는 처음하는게 아니였지만, 들을 때마다 신선하다. 알고리즘 공부를 할 때마다 제공해주는 `sort()` 함수에 감사함을 느낀다... 

이번 주차는 평일 오전에 하루도 빠짐없이 들을려고 했는데 오늘은 블로그 글로 대체!

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/ac573aab-447c-4fcd-b249-edacc299d279" width="80%" />
</center>

정렬은 예제가 많아서 코드 따라치고, 이해하고 반복이였는데 코드를 치면서 하니까 확실히 더 빨리 머릿속에 들어왔다. 예제 코드가 더 많았으면..!!!!! 

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/b9e62e21-cc61-48f1-9eac-ad3a9d58d607" width="80%" />

  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/316d0327-ad64-4741-94eb-11d698aedae5" width="80%" />
</center>

<br>

<https://fastcampus.co.kr/dev_online_upjscodingtest>

> 본 포스팅은 패스트캠퍼스 환급 챌린지 참여를 위해 작성되었습니다. 
{: .prompt-info}