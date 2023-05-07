---
layout: post
title: 패스트캠퍼스 JavaScript 코딩테스트 131개 예제 & CS지식으로 끝내기 강의 3주차
date: 2023-05-07 17:58:00 +900
lastmod: 2023-05-07 18:00:00 +900
categories: [CHALLENGE, Upskill JS CodingTest]
tags: [패스트캠퍼스, 패캠, fastcampus, 자바, 자바스크립트, 파이썬, 코딩테스트, 패스트캠퍼스후기, 코딩교육, 코딩자격증]
use_math: true
image: 
  path: https://user-images.githubusercontent.com/97720335/233675262-28867749-fd9d-4193-924e-8918d1a85517.png
  width: 700
  alt: UPSKILL JS CodingTest 표지
---

# 🔗 Part2 - 자료 구조 핵심 내용 (주관적)
## 큐(Queue) 란?
**큐**는 먼저 삽입된 데이터가 먼저 추출되는 자료구조다.

- **예시)** 게임 대기 큐는 먼저 대기한 사람이 먼저 게임에 매칭된다.
- `머리(head)` : 남아있는 원소 중 가장 먼저 들어 온 데이터를 가리키는 포인터
- `꼬리(tail)` : 남아있는 원소 중 가장 마지막에 들어 온 데이터를 가리키는 포인터

### 큐 구현하기
```js
class Queue {
  constructor() {
    this.items = {};
    this.headIndex = 0;
    this.tailIndex = 0;
  }
  enqueue(item) {
    this.items[this.tailIndex] = item;
    this.tailIndex++;
  }
  dequeue() {
    const item = this.items[this.headIndex];
    delete this.items[this.headIndex];
    this.headIndex++;

    return item;
  }
  peek() {
    return this.items[this.headIndex];
  }
  getLength() {
    return this.tailIndex - this.headIndex;
  }
}

// 구현된 큐 (Queue) 라이브러리 사용
let queue = new Queue();

// 삽입(5) - 삽입(2) - 삽입(3) - 삽입(7) - 삭제() - 삽입(1) - 삽입(4) - 삭제()
queue.enqueue(5);
queue.enqueue(2);
queue.enqueue(3);
queue.enqueue(7);
queue.dequeue();
queue.enqueue(1);
queue.enqueue(4);
queue.dequeue();

// 먼저 들어온 순서대로 출력
while (queue.getLength() !== 0) {
  console.log(queue.dequeue());
}
```

<br>

## 트리(Tree) 란?
**트리**는 가계도와 같이 **계층적인 구조를 표현**할 때 사용할 수 있는 자료구조다.

- 나무(tree)의 형태를 뒤집은 것과 같이 생겼다.

### 트리 용어 정리
- `Root(루트)` : 트리 구조의 시작점이 되는 노드 (가장 상위에 존재하는 정점)
- `Node(노드)` : 트리 구조를 이루는 모든 개별 데이터 (각 정점)
- `Parent node(부모 노드)` : 두 노드가 상하관계로 연결되어 있을 때 상대적으로 루트에서 가까운 노드
- `Child node(자식 노드)` : 두 노드가 상하관계로 연결되어 있을 때 상대적으로 루크에서 먼 노드
- `Leaf(리프)` : 트리 구조의 끝 지점이고, 자식 노드가 없는 노드 (더 이상 자식이 없는 정점)
- `Level(레벨)` : root로부터 몇 번째의 깊이인지를 표현
- `Degree(차수)` : 한 정점에서 뻗어나가는 간선 수

<br>

## 우선순위 큐(Priority Queue) 란?
**우선순위 큐**는 우선순위에 따라서 데이터를 추출하는 자료구조다.

- 컴퓨터 운영체제, 온라인 게임 매칭 등에서 활용된다.
- 우선순위 큐는 일반적으로 **힙(heap)을 이용해 구현**한다.

## 힙(Heap) 이란?
**힙**은 원소들 중에서 최댓값 혹은 최솟값을 빠르게 찾아내는 자료구조다.

- `최대 힙(max heap)` : 값이 큰 원소부터 추출한다.
- `최소 힙(min heap)` : 값이 작은 원소부터 추출한다.
- 힙은 원소의 삽입과 삭제를 위해 $O(log N)$의 수행 시간을 요구한다.
- 단순한 $N$개의 데이터를 힙에 넣었다가 모두 꺼내는 작업은 정렬과 동일하다.
- 이 경우 시간 복잡도는 $O(N log N)$이다.

### 힙(Heap) 라이브러리
- JavaScript는 기본적으로 우선순위 큐를 라이브러리로 제공하지 않는다.
- 최단 경로 알고리즘 등에서 **힙(heap)**이 필요한 경우 **별도의 라이브러리를 사용**해야 한다.

[Heap 라이브러리](https://github.com/ndb796/priorityqueuejs)
- index.js 소스 코드를 가져온 뒤에 다음과 같이 사용할 수 있다.

```js
// 최대힙(Max Heap)
let pq = new PriorityQueue(function (a, b) {
  return a.cash - b.cash;
});

pq.enq({ cash: 250, name: "Doohyun Kim" });
pq.enq({ cash: 300, name: "Gildong Hond" });
pq.enq({ cash: 159, name: "Minchul Han" });
console.log(pq.size()); // 3
console.log(pq.deq()); // { cash: 300, name: 'Gildong Hond' }
console.log(pq.peek()); // { cash: 250, name: 'Doohyun Kim' }
console.log(pq.size()); // 2
```

<br>

## 그래프(Graph) 란?
**그래프**는 사물을 정점(vertex)과 간선(edge)으로 나타내기 위한 도구다.

그래프는 **두 가지 방식**으로 구현할 수 있다.
1. `인접 행렬(adjacency matrix)` : 2차원 배열을 사용하는 방식
2. `인접 리스트(adjacency list)` : 연결 리스트를 이용하는 방식

최단 경로 알고리즘을 구현할 때는 각각 근처의 노드와 연결되어 있는 경우가 많으므로, 간선 개수가 적어 **인접 리스트**가 유리하다.

<br>

# 📃 Week 03 Review
이번 주는 자료 구조 관련 강의를 다 들었다. 핵심적인 부분이 너무 많은 것 같아서 하나씩 적다보니까 내용이 좀 방대해졌다.. <br>
강의 들으면서 필기를 하면 오히려 집중이 잘되어서 밑에있는 사진처럼 공부를 하는 편이다.

<center><img src="https://user-images.githubusercontent.com/97720335/236672676-75e187a3-4c70-4b56-ab17-1a5bb1eeedbf.png" width="80%" /></center>

자료구조 강의를 다 듣고, 어떤 문제를 풀어볼까 고민하다가 큐 문제를 풀게되었다. 다른 자료구조 알고리즘은 난이도가 조금 높은 것 같아서 차근차근 공부하면서 풀어봐야할 것 같다.

<https://www.acmicpc.net/problem/10845>

<center>
  <img src="https://user-images.githubusercontent.com/97720335/236673196-2d8c45ee-ac0d-494d-a46c-d3b2a39720b1.png" width="80%" />
  <img src="https://user-images.githubusercontent.com/97720335/236672280-4e46c832-a02a-4ffe-93c5-cd15c9ce1bf9.png" width="80%" />
</center>

```js
const fs = require("fs");
const file = process.platform === "linux" ? "/dev/stdin" : "./input.txt";
const input = fs.readFileSync(file).toString().split("\n");

class Queue {
  constructor() {
    this.queue = {};
    this.headIndex = 0;
    this.tailIndex = 0;
  }
  push(queue) {
    this.queue[this.tailIndex] = queue;
    this.tailIndex++;

    return queue;
  }
  pop() {
    const current = this.queue[this.headIndex];

    if (this.size() === 0) {
      return -1;
    } else {
      delete this.queue[this.headIndex];
      this.headIndex++;

      return current;
    }
  }
  size() {
    return this.tailIndex - this.headIndex;
  }
  empty() {
    if (this.size() === 0) {
      return 1;
    } else {
      return 0;
    }
  }
  front() {
    if (this.size() === 0) {
      return -1;
    } else {
      return this.queue[this.headIndex];
    }
  }
  back() {
    if (this.size() === 0) {
      return -1;
    } else {
      return this.queue[this.tailIndex - 1];
    }
  }
}

const [N, ...arr] = input;

let queue = new Queue();
let result = [];

for (let i = 0; i < N; i++) {
  let [cmd, item] = arr[i].split(" ");

  switch (cmd) {
    case "back":
      result.push(queue.back());
      break;
    case "pop":
      result.push(queue.pop());
      break;
    case "size":
      result.push(queue.size());
      break;
    case "empty":
      result.push(queue.empty());
      break;
    case "front":
      result.push(queue.front());
      break;
    default:
      queue.push(item);
      break;
  }
}

console.log(result.join("\n"));
```

스택 문제와 큐 문제 거의 비슷한 문제였는데 큐는 class로 만들어서 하다보니까 좀 많이 어려웠는데 풀고나니까 너무 뿌듯했다... 하루에 한 문제씩 진짜 문제풀기!! 지켜보자

<br>

<https://fastcampus.co.kr/dev_online_upjscodingtest>

> 본 포스팅은 패스트캠퍼스 환급 챌린지 참여를 위해 작성되었습니다. 
{: .prompt-info}