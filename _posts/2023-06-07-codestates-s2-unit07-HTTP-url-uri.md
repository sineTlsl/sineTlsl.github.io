---
layout: post
title: "[S2-Unit07] HTTP/Network - URL/URI, IP/Port, Domain/DNS"
date: 2023-06-07 14:54:00 +900
lastmod: 2023-06-07 14:54:00 +900
categories: [CODESTATES, Section02]
tags: [CODESTATES, 코드스테이츠, Section02]
use_math: true
---

## URL과 URI
브라우저의 주소창에 입력한 URL은 서버가 제공되는 환경에 존재하는 파일의 위치를 나타낸다.

예를 들어 `https://codestates.com:443/` 사이트에 접속하게 되면, codestate.com 주소가 가리키는 서버의 기본 폴더를 뜻한다. CLI 환경에서 폴더와 파일의 위치를 찾아 이동하듯이, 슬래시(`/`)를 이용해 서버의 폴더에 진입하거나 파일을 요청할 수 있다. 

그러나 기본적인 보안의 일환으로 외부에서 직접 접근이 가능한 경우는 거의 없다. 쉽게 이해하기 위해 크롬 브라우저의 다음 url 입력한다.

```
# username: 사용자 이름

# macOS 경우
file://127.0.0.1/Users/username/Desktop/
```

위 URL을 크롬 브라우저에 입력하면 크롬 브라우저를 파일 탐색기로 사용할 수 있다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/87ae26d8-1d5f-499d-952d-2747f4769810" width="80%" />
</center>

**구성 요소**

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/a96769e4-51a2-464e-82d9-a4b6bc270dba" width="80%" />
</center>

- `127.0.0.1` 은 로컬 PC를 나타낸다.
- port는 서버로 진입할 수 있는 통로다.

<br>

### URL

>`URL (Uniform Resource Locator)` 의 줄임말로, 네트워크 상에서 웹 페이지, 이미지, 동영상 등의 파일이 위치한 정보를 나타낸다.

URL은 scheme, hosts, url-path로 구분할 수 있다.

- `scheme` : 통신 방식(프로토콜). 일반적인 웹 브라우저에서 http(s)를 사용
- `hosts` : 웹 서버의 이름이나 도메인, IP를 사용하여 주소를 나타냄
- `url-path` : 웹 서버에서 지정한 루트 디렉토리부터 시작하여 웹 페이지, 이미지, 동영상 등이 위치한 경로와 파일명을 나타냄

### URI

> `URI (Uniform Resource Identifier)` 의 줄임말로, 브라우저의 검색창을 클릭하면 나타나는 주소다.

URI는 scheme, hosts, url-path에 더해 query, fragment를 포함한다.
- `query` : 웹 서버에 보내는 추가적인 질문
  - `http://www.google.com:80/search?q=JavaScript` 를 브라우저의 검색창에 입력하면, 구글에서 JavaScript를 검색한 결과가 나타남
- `fragment` : 일종의 북마크 기능을 수행하여 URL에 fragment(`#`)와 특정 HTML 요소의 id를 전달하면 해당 요소가 있는 곳으로 스크롤을 이동함

URI는 URL을 포함하는 상위 개념이다. 따라서 **'URL은 URI다.'**는 참이고, 'URI는 URL이다.'는 거짓이다.

<br>

## IP와 Port
`IP(Internet Protocol)` 은 인터넷상에서 사용하는 주소체계를 의미한다. 

인터넷에 연결된 모든 PC는 IP 주소 체계를 따라 닷(`.`)으로 구분된 네 덩이의 숫자로 구성된다. 이렇게 네 덩이의 숫자로 구분된 IP 주소체계를 **IPv4**라고 한다. 

### IPv4
> `IPv4` 는 Internet Protocol version 4의 줄임말이며 IP 주소체계의 네 번째 버전이다.

- IPv4는 각 덩어리마다 0~255까지 나타날 수 있다.
- 따라서 2^(32)인 약 43억 개의 IP 주소를 표현할 수 있다.


- `localhost`, `127.0.0.1` : 현재 사용 중인 로컬 PC를 지칭
- `0.0.0.0`, `255.255.255.255` : broadcast address, 로컬 네트워크에 접속된 모든 장치와 소통하는 주소
- 서버에서 접근 가능 IP 주소를 broadcast address 로 지정하면, 모든 기기에서 서버에 접근할 수 있다.

터미널에서 `nslookup codestates.com` 을 입력하면 코드스테이츠의 IPv4 주소를 확인할 수 있다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/a225328b-c602-4a6c-8c29-3f45decf5f8c" width="80%" />
</center>

### IPv6 등장

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/830f460e-c0c7-44e9-9d74-4f0fe375e53c" width="80%" />
</center>

과거에는 인터넷 보급률이 낮아 IPv4 버전으로만 네트워크에 연결된 PC에 주소를 할당하는 일이 가능했다. 

그러나 개인 PC의 보급으로 전 세계의 누구나 PC를 이용하여 인터넷에 접속하게 되고, 각종 서비스를 위해 서버를 생산하면서 IPv4로 할당할 수 있는 PC가 한계를 넘어서게 되었다.

늘어나는 기기를 감당할 수 없어 그 대안으로 등장하게 된 것이 `IPv6(IP version 6)` 이다. IPv6는 표기법을 달리 책정하여 2^(128)개의 IP 주소를 표현할 수 있다.

### PORT
PORT는 `127.0.0.1` 뒤에 `:숫자` 와 같이 표현된다. `:` 뒤에 숫자는 IP 주소가 가리키는 PC에 접속할 수 있는 통로(채널)를 의미한다. 

이미 사용 중인 포트는 중복해서 사용할 수 없고, 만약 다른 프로그램에서 3000번 포트가 사용 중이라면 다른 포트 번호(3001)로 실행된다.

포트 번호는 0~65535까지 사용할 수 있다. 그 중에서 0~1024번 까지의 포트 번호는 주요 통을 위한 규약에 따라 이미 정해져 있다. 다음은 반드시 알아야 할 **포트 번호**다.
- `22` : SSH
- `80` : HTTP
- `443` : HTTPS

이미 정해진 포트라도 필요에 따라 자유롭게 사용이 가능하다. HTTP(:80), HTTPS(:443)과 같이 잘 알려진 포트의 경우, `https://codestates.com:443` 이 아닌 `https://codestates.com` 처럼 포트 번호를 URI에 생략할 수 있지만, 그 외의 잘 알려지지 않은 포트(리액트의 기본 3000과 같은 임시 포트)는 반드시 포트 번호를 포함해야 한다.

<br>

## Domain과 DNS
### Domaoin Name

웹 브라우저를 통해 특정 사이트에 진입 할 때, IP 주소를 대신하여 사용하는 주소가 존재한다. 만약 IP 주소가 지번 또는 도로명 주소라면, 도메인 이름은 해당 주소에 위치한 상호로 볼 수 있다.

도메인 이름을 이용하면, 한눈에 파악하기 힘든 IP 주소를 보다 간단하게 나타낼 수 있다.

위에서 터미널로 `nslookup` 으로 살펴본 주소를 한번 더 보자면, **IP 주소**는 3.34.153.168 이고, **도메인 이름**은 codestates.com이다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/c87703a7-2d0a-41b9-8d35-268d3c9b6a3f" width="80%" />
</center>

주소 창에 IP 주소(3.34.153.168)를 입력하면, codestates.com으로 이동할 수 있다.

### DNS
> `DNS(Domain Name System)` 는 도메인 이름을 입력하여 해당 사이트로 이동하기 위해서 해당 도메인 이름과 매칭된 IP 주소를 확인하는 작업을 수행하는 시스템이다.

<center>
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/199a961e-34f3-4cea-abbf-c0774ac1a3f7" width="80%" />
</center>

- DNS는 호스트의 도메인 이름을 IP 주소로 변환하거나 반대의 경우를 수행할 수 있도록 개발된 데이터베이스 시스템이다.
- 브라우저 검색창에 `naver.com` 을 입력한다면, 이 요청은 DNS에서 IP 주소(ex.125.209.222.142)를 찾는다.
- IP 주소에 해당하는 웹 서버로 요청을 전달하여 클라이언트와 서버가 통신할 수 있도록 한다.

<br>

**Reference**

[CODESTATES (SEB_FE_43)](https://www.codestates.com/)
