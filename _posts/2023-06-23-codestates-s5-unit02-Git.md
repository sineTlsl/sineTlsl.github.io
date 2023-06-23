---
layout: post
title: "[S5-Unit02] Git - GitHub Repository 들어가야할 파일 및 기능"
date: 2023-06-23 18:44:00 +900
lastmod: 2023-06-23 18:44:00 +900
categories: [CODESTATES, Section05]
tags: [CODESTATES, 코드스테이츠, Section05]
use_math: true
image: 
  path: https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/bffde79d-51f0-43a4-818a-2bc7b1f39a05
  width: 1100
  alt: Git
---

## GitHub Repository에 들어가야 할 파일
### README.md

- GitHub는 개발자의 SNS라고 불릴 정도로 다양한 종류의 오픈소스 프로젝트가 공유되어 있다.
- 오픈소스 프로젝트에 들어가면, 가장 먼저 확인할 수 있는 정보다.
- 기본적인 마크다운 사용법을 잘 숙지하고 있으면 간단한 소개 페이지처럼 제작할 수 있다.
- README.md 파일을 적는 양식은 따로 존재하지 않지만, 대체로 어떻게 하면 해당 오픈소스를 활용할 수 있는지에 대한 정보가 작성되어 있다.

### gitignore
- gitignore dotfile은 git으로 관리하지 않는 파일 모음이다.
- 여기에는 개인이 따로 관리해야 하는 중요한 secret token이나, 다른 동료와 공유할 필요가 없는 설정 파일, 그 외 공유할 필요 없는 파일을 기록하면 git이 이를 파악하지 않고, push 할 때도 GitHub Repository에 push되지 않는다.

### LICENSE
- 해당 코드의 라이센스를 표기한다.
- GitHub에 public하게 공개된 리포지토리도 라이센스에 따라서 사용을 할 수도 있고, 하지 못 할 수도 있으니 사용할 때 라이센스를 잘 보고 사용해야 한다.
- 회사에서 코드는 private으로 관리하고, 외부에 공개하지 않아 라이센스를 따로 표기하지 않기도 한다.
- but, 모종의 이유로 회사에서 작성하는 코드가 public으로 공개된다면, LICENSE를 명확하게 표기해야 한다.

<br>

## 프로젝트 관리에 활용할 수 있는 GitHub 기능
### Issue
- GitHub Issue는 말 그대로 프로젝트에 새로운 기능을 제안하거나, 버그를 찾아 제보하는 등 프로젝트의 이슈를 의미한다.

### Milestone
- GitHub Milestone 이정표 역할을 하며, 태스크 카드(lssue)를 그룹화하는 데 사용한다.
- GitHub Milestone에 연결된 태스크 카드(Issue)가 종료되면 GitHub Milestone마다 진행 상황이 업데이트되는 것을 볼 수 있다.
- 이 GitHub Milestone 기능을 통해 연관된 이슈의 추적과 진행 상황을 한눈에 파악할 수 있는 장점이 있다.

### Pull Request
- Pull Request는 내가 작업한 내용을 중요 Git branch에 합칠 수 있는지 확인하는 요청이다.
- GitHub에서는 Pull Request에서 커밋한 코드를 따로 선택하여 해당 부분에 코멘트를 달 수 있다.
- 현장에서도 Pull Request를 보고 코멘트를 남기면서 코드 리뷰를 진행하기 때문에 Pull Request 과정에 익숙해지는 것이 중요하다.

### Project
- GitHub Project는 GitHub 내에서 업무 관리를 해줄 수 있게 돕는 새로운 기능이다.

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)
