---
layout: post
title: "[캡틴판교 TS] 섹션 0. 강의 오리엔테이션"
date: 2023-04-23 15:20:00 +900
lastmod: 2023-04-23 15:23:00 +900
categories: [STUDY, Captain Pangyo-TS Basic]
tags: [captainpangyo, typescript]
image: 
  path: https://user-images.githubusercontent.com/97720335/233822587-60d294e1-867c-4cc0-b352-26899b803685.png
  width: 700
  alt: 타입스크립트 입문 - 기초부터 실전까지 강의 표지
---

자바스크립트로 제작된 COVID-19 세계 현황판을 타입스크립트로 변환해보면서 타입스크립트의 개념과 기초를 배워보는 강좌다.

# 📌 강의 오리엔테이션
## 강의 특징
- 실습 & 코딩 중심 강의 - 3개의 실습 프로젝트
- 개념 설명은 짧고 간단하게 실습은 자세하게
- 수업 & 학습 자료를 웹 문서로 제공 - [타입스크립트 핸드북](https://joshua1988.github.io/ts/)

## 교과 과정
구현되어 있는 자바스크립트를 타입스크립트로 변환하기 위해 필요한 개념들을 하나 하나 간단히 설명하고 실습한 뒤 실제 프로젝트에 적용해보는 순서로 진행된다.
- 전반부는 개념 설명 및 실습 + 후반부는 프로젝트에 코드 적용

## 강의 대상
- 자바스크립트의 기본 문법을 알고 있는 웹 개발자
  - 최신 문법(ES6)은 몰라도 된다.
- 자바스크립트로 좀 더 단단한 웹 애플리케이션을 만들고 싶은 웹 개발자
- 타입스크립트로 되어 있는 프로젝트에서 퍼블리싱을 해야 하는 퍼블리셔

## 개발 환경

-   [Chrome](https://www.google.com/intl/ko/chrome/)
-   [Visual Studio Code](https://code.visualstudio.com/)
-   [Node.js LTS 버전(v10.x 이상)](https://nodejs.org/ko/)
-   [Git](https://git-scm.com/downloads)

수업에서는 VSCode를 기준으로 설명한다.

<br>

## 수업 소스 리포지토리 클론 및 VSCode로 폴더 열기
강의 리포지토리 주소: [learn-typescript](https://github.com/joshua1988/learn-typescript)


### 1. git clone

```shell
git clone https://github.com/joshua1988/learn-typescript.git
```

### 2. VSCode로 폴더 열기

<center><img src="https://user-images.githubusercontent.com/97720335/233822798-5cd3f79e-db75-4c51-8995-17cc86988f20.png"></center>

## VSCode 플러그인 설치 및 구성, 플러그인 목록 안내
- 색 테마: [Night Owl](https://marketplace.visualstudio.com/items?itemName=sdras.night-owl)
- 파일 아이콘 테마: [Material Icon Theme](https://marketplace.visualstudio.com/items?itemName=PKief.material-icon-theme)
- 문법 검사: ESLint, [TSLint](https://marketplace.visualstudio.com/items?itemName=eg2.tslint)
- 실습 환경 보조: [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer)
-   기타: [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode), [Project Manager](https://marketplace.visualstudio.com/items?itemName=alefragnani.project-manager), [Auto Close Tag](https://marketplace.visualstudio.com/items?itemName=formulahendry.auto-close-tag), [GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens), [Atom Keymap](https://marketplace.visualstudio.com/items?itemName=ms-vscode.atom-keybindings), [Jetbrains IDE Keymap](https://marketplace.visualstudio.com/items?itemName=isudox.vscode-jetbrains-keybindings) 등

---

## 🧸 Feelings ...
타입스크립트를 들어가기 전, 강의 개요 및 VSCode 세팅에 대해 알아보았다. 
이제 타입스크립트를 처음 배우는 입장으로서 앞으로 섹션 끝날 때 마다 블로그에 작성할 계획이다. 

<center><img src="https://user-images.githubusercontent.com/97720335/233823022-cebf4ec8-1d28-428e-b367-732ad6ab534c.png"></center>

<br>

<https://www.inflearn.com/course/%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%9E%85%EB%AC%B8>

> 본 포스팅은 캡틴판교 강사님의 `타입스크립트 입문 - 기초부터 실전까지` 강의를 수강하고 난 후, 본인의 주관적인 견해에 의하여 작성되었습니다.
{: .prompt-info}