---
layout: post
title: "[Nextjs] 렌더링 CSR vs. SSG vs. ISR vs. SSR 이해하기"
date: 2024-02-09 15:27:00 +900
lastmod: 2024-02-09 15:27:00 +900
categories: [Skill, Nextjs]
tags: [Nextjs, 렌더링, CSR, SSG, ISR, SSR]
use_math: true
image:
  path: https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/7329aa1e-80fa-4c8d-a2cb-47d91f8aed7a
  width: 700
  alt: CSR vs. SSG vs. ISR vs. SSR
---

# 🆚 Rendering CSR vs. SSG vs. ISR vs. SSR

Next.js는 다양한 렌더링 방식을 지원한다. 각 페이지마다 원하는 렌더링하는 방식을 채택하여 사용할 수 있고, 혼합해서 사용할 수 있다.

## 🕊️ CSR (Client Side Rendering)

> 브라우저에 표기할 모든 코드들을 클라이언트 측에서 다 다운을 받아 서버가 아닌 클라이언트에서 처리되는 방식이다.

### 장점

- 처음 로딩한 후에는 다른 페이지를 load하는 속도가 빠르다.
- 서버의 부하가 작다.
- 동적인 콘텐츠와 상호작용이 많은 페이지에 적합하다.

### 단점

- 검색 엔진 최적화(SEO) 부적합하다.
- 페이지 로딩 시간(TTV)이 길다.
- 보안에 취약하다.
- CDN (Content Delivery Network)에 캐시가 안된다.

<br>

## 🍋 SSG (Static Site Generation)

> 처음 빌드할 때, 클라이언트에서 작성한 코드를 서버에서 실행하여 CDN에서 정적 HTML로 제공되는 방식이다.

### 장점

- 서버에서 미리 만들어놓은 html을 받아오기 때문에, 페이지 로딩 시간(TTV)이 빠르다.
- 검색 엔진 최적화(SEO)가 좋다.
- 클라이언트에서 불필요한 코드를 보내지 않으므로 보안이 좋다.
- HTML 파일만 주고받으면 되니까 CDN에 캐시가 된다.

### 단점

- 처음에 한번에만 렌더링이 이루어지기 때문에 데이터가 정적이다.

<br>

## 🐓 ISR (Incremental Static Regeneration)

> SSG와 동일한 원리지만, 주기적으로 다시 시작되는 방식이다.

### 장점

- 서버에서 미리 만들어놓은 html을 받아오기 때문에, 페이지 로딩 시간(TTV)이 빠르다.
- 검색 엔진 최적화(SEO)가 좋다.
- 클라이언트에서 불필요한 코드를 보내지 않으므로 보안이 좋다.
- HTML 파일만 주고받으면 되니까 CDN에 캐시가 된다.
- 데이터가 주기적으로 업데이트된다.

### 단점

- 주기적이긴 하지만, 바로 반영이 되지 않기 때문에 실시간 데이터가 아니다.

<br>

## 🐁 SSR (Server Side Rendering)

> 미리 렌더링을 하는 방식이 아닌, 클라이언트가 서버에 요청할 때 서버에서 렌더링 처리하여 클라이언트에 결과를 응답해주는 방식이다.

### 장점

- 서버에서 미리 만들어놓은 html을 받아오기 때문에, 페이지 로딩 시간(TTV)이 빠르다.
- 검색 엔진 최적화(SEO)가 좋다.
- 클라이언트에서 불필요한 코드를 보내지 않으므로 보안이 좋다.
- 실시간 데이터가 반영된다.

### 단점

- 서버에서 렌더링을 하고 클라이언트에 보내주기 때문에 SSG와 ISR보다 비교적 느릴 수 있다.
- 매 요청마다 웹 페이지를 만들기 때문에 서버의 과부화가 걸릴 수 있다.

<br>

## 🐤 요약

- CSR은 클라이언트에서 렌더링이 이루어진다.
- SSG, ISR, SSR은 서버에서 렌더링이 이루어진다.
