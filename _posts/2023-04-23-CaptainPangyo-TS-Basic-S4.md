---
layout: post
title: "[캡틴판교 TS] 섹션 4. 첫 번째 프로젝트 - 할 일 관리, 애플리케이션"
date: 2023-04-23 20:01:00 +900
lastmod: 2023-04-23 20:01:00 +900
categories: [STUDY, Captain Pangyo - TS Basic]
tags: [captainpangyo, typescript]
image: 
  path: https://user-images.githubusercontent.com/97720335/233822587-60d294e1-867c-4cc0-b352-26899b803685.png
  width: 700
  alt: 타입스크립트 입문 - 기초부터 실전까지 강의 표지
---

# 할 일 관리, 애플리케이션 실습

## Todo 실습 안내
주어진 코드에서 올바르게 타입을 변환할 수 있는 알아보는 시간이다.

**1. `1_todo` 폴더 안에서 `npm install` 을 해서 node_modules를 설치한다.**

<div align="center"><img src="https://user-images.githubusercontent.com/97720335/233835875-0a12acc6-9862-4494-846f-e71ced682e5a.png" width="50%"></div>

**2. `tsconfig.json` 파일 수정**

<div align="center"><img src="https://user-images.githubusercontent.com/97720335/233835955-a15f0652-0bf0-44b0-8611-92ca6e4484b3.png" width="70%"></div>

<br>

## 실습 CODE
```ts
// type TodoType = { id: number, title: string, done: boolean}
interface TodoType {
  id: number;
  title: string;
  done: boolean;
}
let todoItems: TodoType[];

// api
function fetchTodoItems(): TodoType[] {
  const todos = [
    { id: 1, title: '안녕', done: false },
    { id: 2, title: '타입', done: false },
    { id: 3, title: '스크립트', done: false },
  ];
  return todos;
}

// crud methods
function fetchTodos(): object[] {
  const todos = fetchTodoItems();
  return todos;
}

function addTodo(todo: TodoType): void {
  todoItems.push(todo);
}

function deleteTodo(index: number): void {
  todoItems.splice(index, 1);
}

function completeTodo(index: number, todo: TodoType): void {
  todo.done = true;
  todoItems.splice(index, 1, todo);
}

// business logic
function logFirstTodo(): object {
  return todoItems[0];
}

function showCompleted(): object[] {
  return todoItems.filter(item => item.done);
}

// TODO: 아래 함수의 내용을 채워보세요. 아래 함수는 `addTodo()` 함수를 이용하여 2개의 새 할 일을 추가하는 함수입니다.
function addTwoTodoItems(): void {
  // addTodo() 함수를 두 번 호출하여 todoItems에 새 할 일이 2개 추가되어야 합니다.
  addTodo({ id: 4, title: '아이템 4', done: false });
  addTodo({ id: 5, title: '아이템 5', done: false });
}

// NOTE: 유틸 함수
function log(): void {
  console.log(todoItems);
}

todoItems = fetchTodoItems();
addTwoTodoItems();
log();
```

---

## 🧸 Feelings ...
Todo 파일에 있는 함수 타입을 직접 설정하는 시간이었다. 간단한 코드들만 보다가 조금 더 길어진 코드봤다고 당황하는 내 자신 ... 공부를 좀 더 해야겠다...

<div align="center"><img src="https://user-images.githubusercontent.com/97720335/233835994-75d25719-55ea-4b54-8173-4dc2f6ca1e20.png"></div>

<br>

**Reference**

[[캡틴판교 TS] 타입스크립트 입문 - 기초부터 실전까지](https://www.inflearn.com/course/%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%9E%85%EB%AC%B8)

<br>

> 본 포스팅은 캡틴판교 강사님의 `타입스크립트 입문 - 기초부터 실전까지` 강의를 수강하고 난 후, 본인의 주관적인 견해에 의하여 작성되었습니다.
{: .prompt-info}