---
layout: post
title: "Git Commit Message Convention"
date: 2023-04-24 13:56:00 +900
lastmod: 2023-04-24 13:56:00 +900
categories: [GIT]
tags: [git]
image: 
  path: https://user-images.githubusercontent.com/97720335/233878034-e4b9bad7-48ad-4eeb-aa97-c4249c60edef.png
  width: 700
  alt: GIT
---

# Git Commit Message Convention

## 1. Commit 메시지 구조
커밋 메시지는 크게 `제목`, `본문`, `꼬리말` 세 가지 파트로 나누고, 각 파트는 **빈줄**을 두어서 구분한다.

```
type(옵션): Subject // 제목
body(옵션) // 본문
footer(옵션) // 꼬리말
```
> - `type` : 어떤 의도로 커밋을 했는지 type에 명시한다.
> - `subject` : 최대 50글자가 넘지않아야하며, 마침표는 찍지 않는다. 영문으로 표기할 경우, 동사를 가장 앞에 두고 첫 글자는 대문자로 표기한다.
> - `body` : 긴 설명이 필요한 경우에 작성한다. 무엇을 왜 하였는지 작성하는 부분으로 최대 75자를 넘기지 않아야 한다.
> - `footer` : issue tracker ID를 명시하고 싶은 경우에 작성한다.

<br>

## 2. Commit Type

타입은 태그와 제목으로 구성된다.

`태그 : 제목` **의 형태이며,** `:` **뒤에만 space가 있음에 유의한다.**

Tag | Title
-- | --
feat | 새로운 기능 추가
fix | 버그 수정
docs | 문서 수정
design | CSS 등 사용자 UI 디자인 변경
style | 코드 포맷 변경, 세미 콜록 누락, 코드 수정이 없는 경우
refactor | 코드 리팩토링
test | 테스트 추가, 테스트 리팩토링 추가 (프로덕션 코드 변경 x)
chore | 빌드 테스트 업데이트, 패키지 매니저를 설정(프로덕션 코드 변경 x)
comment | 필요한 주석 추가 및 변경
rename | 파일 혹은 폴더명을 수정하거나 옮기는 작업만인 경우
remove | 파일을 삭제하는 작업만 수행한 경우
!BREAKING CHANGE | 커다란 API 변경
!HOTFIX | 급하게 치명적인 버그를 고쳐야하는 경우

<br><br>

**Reference**

[[협업] 협업을 위한 git 커밋컨벤션 설정하기](https://overcome-the-limits.tistory.com/entry/%ED%98%91%EC%97%85-%ED%98%91%EC%97%85%EC%9D%84-%EC%9C%84%ED%95%9C-%EA%B8%B0%EB%B3%B8%EC%A0%81%EC%9D%B8-git-%EC%BB%A4%EB%B0%8B%EC%BB%A8%EB%B2%A4%EC%85%98-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0)

<br>