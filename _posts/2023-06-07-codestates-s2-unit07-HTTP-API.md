---
layout: post
title: "[S2-Unit07] HTTP/Network - HTTP 서버 통신과 API"
date: 2023-06-07 14:45:00 +900
lastmod: 2023-06-07 14:45:00 +900
categories: [CODESTATES, Section02]
tags: [CODESTATES, 코드스테이츠, Section02]
use_math: true
---

웹 애플리케이션 아키텍처에서는 클라이언트와 서버가 서로 HTTP라는 프로토콜을 이용해서 서로 대화를 나눈다. HTTP를 이용해 주고받는 메시지를 `HTTP 메시지` 라고 부른다.

# 클라이언트와 서버 간 통신
스타벅스와 같은 커피 전문점에 가서 커피를 주문할 때 카운터로 찾아가거나 앱 또는 키오스크를 이용할 수 있습니다. 이러한 방법 하나하나 전부 프로토콜이며, 같은 일을 하기 위해 다양한 방법이 존재할 수 있다.

## 주요 프로토콜
OSI 7 Layer에서 각각의 프로토콜은 다음과 같은 계층에 속해있다.

**7 Layer: 응용 계층**
- `HTTP` : 웹에서 HTML, JSON 등의 정보를 주고 받는 프로토콜
- `HTTPS` : HTTP에서 보안이 강화된 프로토콜
- `FTP` : 파일 전송 프로토콜
- `SMTP` : 메일을 전송하기 위한 프로토콜
- `SSH` : CLI 환경의 원격 컴퓨터에 접속하기 위한 프로토콜
- `RDP` : Windows 계열의 원격 컴퓨터에 접속하기 위한 프로토콜
- `WebSocket` : 실시간 통신, Push 등을 지원하는 프로토콜

**4 Layer: 전송 계층**
- `TCP` : HTTP, FTP 통신의 등의 근간이 되는 인터넷 프로토콜
- `UDP` : (양방향의 TCP와는 다르게) 단방향으로 작동하는 훨씬 더 단순하고 빠르지만, 신뢰성이 낮은 인터넷 프로토콜

<br>

## API

> `API (Application Programming Interface)` 는 서버가 클라이언트에게 리소스를 잘 활용할 수 있도록 인터페이스를 제공해주는 역할이다.

### API Case Study: 커피 주문

호스트의 주소가 `http://starbucks.com` 이라 가정하였을 때, 요청과 URL 주소로는 다음과 같이 예를 들 수 있다.

| **요청** | **URL 디자인 예제** |
| :---: | :---: |
| 아메리카노 한 잔 주세요 | /coffee/americano |
| 망고 프라푸치노 한 잔 주세요 | /frappuccino/mango |
| 콜드브루 두 잔 주세요 | /coffee/coldbrew?quantity=2/ |
| 아메리카노 두 잔 전부 헤이즐넛 시럽 넣어주세요 | /coffee/americano?quantity=2/&syrup=hazelnet |

서버는 리소스 전달을 위한 메뉴판, 즉 **API 문서**를 작성해야 클라이언트가 이를 활용할 수 있다. 보통 인터넷에 있는 데이터를 요청할 때에는 **HTTP 프로토콜**을 사용하며, **주소(URL, URI)** 를 통해 접근할 수 있다.

### HTTP API 디자인하는 방법

HTTP API 디자인에는 Best Practice가 존재한다.

- `조회(Read)` : GET
- `추가(Create)` : POST
- `갱신(Update)` : PUT 또는 PATCH
- `삭제(Delete)` : DELETE

**예) 사용자 관리 API**

| **요청** | **URL 디자인 예제** | **사용하는 메소드** |
| :---: | :---: | :---: |
| 모든 사용자 조회 | /users | GET |
| 새 사용자 추가 | /users | POST |
| 1번 사용자 정보 갱신 | /users/1 | PUT |
| 1번 사용자 정보 삭제 | /users/1 | DELETE |
| 1번 사용자 정보 조회 | /users/1 | GET |

HTTP 요청 시 메소드를 지정하여 리소스와 관련된 행동(CRUD)을 지정할 수 있다.

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)
