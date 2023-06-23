---
layout: post
title: "[S5-Unit02] Git - GitHub Issue, Milestone, Kanban"
date: 2023-06-23 19:18:00 +900
lastmod: 2023-06-23 19:18:00 +900
categories: [CODESTATES, Section05]
tags: [CODESTATES, 코드스테이츠, Section05]
use_math: true
image: 
  path: https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/bffde79d-51f0-43a4-818a-2bc7b1f39a05
  width: 1100
  alt: Git
---

## GitHub Issue란?
GitHub에서는 다음과 [GitHub Issue의 특징](https://docs.github.com/en/issues/tracking-your-work-with-issues/about-issues)을 설명하고 있다.

> **Use GitHub Issues to track ideas, feedback, tasks, or bugs for work on GitHub.** <br>
GitHub Issue를 아이디어 공유, 피드백, 태스크, 버그 관리로 사용하세요. - GitHub

## GitHub Issue 실습
### 1. 이슈 (task card) 생성

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/6725e926-38cd-43fd-a1a8-4a3838cdb661" width="90%" />
</center>

저장소 첫 페이지의 `Issues` 탭을 선택하고 `New Issue`를 클릭한다.

### 2. task 작성
이슈 템플릿의 제목과 본문을 만들고자 하는 태스크 카드에 맞게 수정해준다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/819838a7-5131-4b0c-9be2-d86118d6c1f2" width="90%" />
</center>

제목과 본문을 다 작성했으면, 우측 탭을 이용해 세부 설정을 진행한다.

- `Assigness` : 해당 태스크를 맡은 사람을 지정해주면 된다. assign yourself를 누르시면 자신의 태스크로 만들 수 있다.
- `Labels` : 태스크 카드에 라벨링을 할 수 있다.
- `Projects` : Projects를 지정할 수 있다.
- `Milestone` : 마일스톤을 지정할 수 있다.

**Task Card 작성 완료 후 모습**

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/0cbfd90c-38e3-4257-82a5-cb637dcc0429" width="90%" />
</center>

### 3. task 일정 완료 후 이슈 닫기

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/663b2afb-8ebb-4656-8ddc-5db05c48c0f5" width="90%" />
</center>

<br>

## GitHub Issue 템플릿 카드
이슈 반복 생성을 편하게 할 수 있는 이슈 템플릿 카드 기능이다.

### 1. `settings` 클릭

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/f76d814f-ed32-4592-91f0-3fbd3704a829" width="90%" />
</center>

### 2. `Issues` 의 `Set up templates`를 클릭

> Settings 설정 화면 아래로 조금 내려가면 Feature의 `Issues` 설정을 확인할 수 있다.
템플릿 생성을 위해 `Set up templates` 를 클릭한다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/2e7a3046-0feb-490c-982e-8793e7fdc8eb" width="90%" />
</center>

아래와 같이 템플릿을 만들면 향후 새롭게 이슈를 생성할 때 아래 템플릿을 그대로 사용할 수 있다. 더 자세한 내용은 [GitHub 공식문서](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/configuring-issue-templates-for-your-repository)를 참고한다.

```
### 만들고자 하는 기능이 무엇인가요?
ex) Todo 생성 기능

### 해당 기능을 구현하기 위해 할 일이 무엇인가요?
1. [ ] Job1
2. [ ] Job2
3. [ ] Job3

### 예상 작업 시간
ex) 3h
```

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/af08eae9-80ee-413f-9bb8-0e99eaeecd6a" width="90%" />
</center>

<br>

## GitHub Milestone란?

GitHub에서는 아래와 같이 [GitHub Milestone의 특징](https://docs.github.com/en/issues/using-labels-and-milestones-to-track-work/about-milestones)에 대해서 설명하고 있다.

> **You can use milestones to track progress on groups of issues or pull requests in a repository.** <br>
마일스톤을 이슈, PR 그룹의 진척도를 확인하는데 사용하세요. - GitHub

프로젝트가 커지고 많은 양의 이슈들이 생기게 된다면 이슈로는 관리가 어렵다. 그렇기 때문에 여러 개의 이슈들을 각각의 마일스톤으로 그룹화 하는 작업이 필요하다.

## GitHub Milestone 실습

### 1. GitHub Milestone 생성
1-1. `Issue` 탭을 누르고 `Milestones` 를 클릭한다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/88336904-ffd6-40e2-b16a-0ebb8308f711" width="90%" />
</center>

1-2. `Create a Milestone` 혹은 `New milestone` 을 클릭한다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/6fa18689-43a1-4eef-8ac5-188c71446479" width="90%" />
</center>

### 2. GitHub Milestone 세부 내용 작성
마일스톤의 이름을 `Title`에 작성하고 `Due Date`를 설정한다.
- `Due Date` 는 마일스톤의 마지막 날을 의미한다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/c7b79ab9-78bc-4125-b733-5c53fb4cbadd" width="90%" />
</center>

`Description` 의 해당 마일스톤의 설명을 작성하고, `Create milestone` 을 클릭한다.

### 3. 마일스톤 생성 확인

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/69ef57a8-cb2c-4c39-aaf2-b3b077a32c1f" width="90%" />
</center>

다음과 같이 사진처럼 계획에 알맞은 갯수만큼의 마일스톤과 태스크를 만들어 관리할 수 있다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/a6efe11f-4f75-4092-b578-caf2f34939b6" width="90%" />
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/07b1794e-be91-4588-b20f-06cfe722e6df" width="90%" />
</center>

<br>

## GitHub Project Kanban란?

GitHub에서는 2022년 7월 27일 GitHub Issues를 기반으로 하는 GitHub 프로젝트를 리뉴얼 하였다.

GitHub에서는 아래와 같이 GitHub Project의 특징을 설명하고 있다.

> **Projects is an adaptable, flexible tool for planning and tracking work on GitHub.** <br>
GitHub Project는 작업을 계획하고 트래킹하는데 뛰어난 도구입니다 - GitHub

GitHub 이슈와 마일스톤을 칸반으로 쉽게 관리할 수 있다.

## Kanban 실습
### 1. Project 생성

1-1. `Projects` 탭을 선택하고 `Link a project` -> `New project` 를 클릭한다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/9ca5629f-7400-4849-96a9-5ff5660415f1" width="90%" />
</center>

1-2. `New project` 를 클릭한다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/2bce2e40-92fa-4397-9e0a-dbcb425b9b3a" width="90%" />
</center>

1-3. 탬플릿을 고르는 모달창에서 테이블 또는 모드를 선택한 후 `Create` 버튼을 클릭한다.

### 2. Project 이름 및 접근 설정
2-1. 오른쪽 상단의 버튼을 눌러 `Settins` 를 클릭하고, 프로젝트 이름과 간단한 설명을 다 작성하였으면 `Save` 버튼을 눌러 저장한다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/44ef3393-b48f-4be4-9dc6-6966208bb41e" width="90%" />
</center>

2-2. 프로젝트의 이름이 변경된 것을 확인할 수 있다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/91c32d37-3131-428d-91b3-88dd7b121e7e" width="90%" />
</center>

### 3. Issue 연결하기
3-1. `#` 으로 자신의 리포지토리를 찾는다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/85a3aa62-a1e6-4f7d-bd46-6b01c2c9c695" width="90%" />
</center>


3-2. 리포지토리를 선택하면 이슈나 PR을 선택할 수 있다. 
- `Add multiple items` 버튼을 눌러 모든 item을 추가하거나,
- 이슈가 없을 때는 버튼이 뜨지 않아 개별 item을 추가할 수 있다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/cbd1f6fe-4405-478f-b0cc-86298c0049e1" width="90%" />
</center>

3-3. 리포지토리에 작성한 이슈가 프로젝트의 추가된 것을 확인할 수 있다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/9b4d9a7e-73f3-4457-83d3-7e26890429dd" width="90%" />
</center>

### 4. 프로젝트 설정
4-1. 각 이슈들의 상태를 설정할 수 있다. 기본적으로 `Todo` , `In Progress` , `Done` 세가지 상태가 있다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/5ac7a90b-4ac8-4921-bc27-460ef97bc62a" width="90%" />
</center>

4-2. `Labels`, `PR`, `Reviewers`, `Repository`, `Milestone` 등 새로운 칼럼도 넣을 수 있다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/3d0ed8a5-bb6a-4af4-8ae2-adb0e6b10746" width="90%" />
</center>

4-3. 그룹으로 나눠서 볼 수 있으며, `Assignees`, `Status`, `Milestone`, `Repository` 등으로 나눌 수 있다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/5c8a009a-e009-4cd6-a522-449d3f2395f6" width="90%" />
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/192c28e2-24d6-4127-85e0-75ae88a7f1cb" width="90%" />
</center>

4-4. 칸반보드로도 볼 수 있다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/9ad89447-9fe6-4b36-ac04-2d1a061e846b" width="90%" />
</center>

4-5. 설정이 끝났다면 우측 상단에 있는 `Save changes` 버튼을 클릭하여 저장한다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/46ac0d66-b3e9-4abb-b831-3fc19be8371c" width="90%" />
</center>

### 5. 프로젝트 적용
5-1. `Projects` 탭 목록에 있으면 프로젝트에 적용이 된 것이다. 적용이 안됬을 경우에는 `Link a project` 에서 생성한 프로젝트를 연결해준다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/6fc40bba-0c55-41cf-8eb4-1445a2966575" width="90%" />
</center>

이슈 생성 시 `Projects` 를 Todo List로 지정하면 자동으로 트래킹 된다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/16b2ecc8-6a28-42b9-b14f-0b72853602c2" width="90%" />
</center>

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)
