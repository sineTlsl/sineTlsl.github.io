---
layout: post
title: "[Error] GitBlog Ruby failed with exit code 5 해결"
date: 2024-02-09 16:13:00 +900
lastmod: 2024-02-09 16:13:00 +900
categories: [GitBlog]
tags: [GitBlog, Blog, Error]
use_math: true
---

## 🔺 에러 발생 원인은?

블로그 빌드 과정에서 다음과 같이 에러가 발생했다.

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/dd705e60-743d-46dc-b936-dc1f2e21e8ed" width="90%" />
</p>

> The process '/opt/hostedtoolcache/Ruby/3.3.0/x64/bin/bundle' failed with exit code 5
> {: .prompt-warning}

## ❓ 그럼 어떻게 해결해야할까?

해결은 간단하다. `pages-deploy.yml` 파일을 찾아서 다음과 같이 버전을 변경해주면 된다.

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/2b6c4336-5176-4297-b568-34d415a5c342" width="50%" />
</p>

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/407c4cf6-2867-4169-ad52-1b04267797c0" width="90%" />
</p>

기존에는 ruby-version이 `3`으로 지정되어있는 걸 확인할 수 있다.

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/bd96e965-6a11-4299-8ed6-a66b5dcc730b" width="90%" />
</p>

이 부분을 `3.2`로 변경해주고 push까지 완료하면 빌드 과정에서 아무런 문제도 발생하지 않고 해결이 된다!

~~그 전의 나는 3.3.0으로 루비 업데이트 해보았지만 안되서 3.2로 다시 변경한건 안비밀 ... 삽질의 흔적들... 마지막엔 드디어 완료~~

<p align="center">
  <img src="https://github.com/sineTlsl/sineTlsl.github.io/assets/97720335/5558f8ac-681c-49c6-8b08-3f29dd75bb44" width="90%" />
</p>

<br><br>

**Reference**

[Build error at Setup Ruby, failed with exit code 5](https://talk.jekyllrb.com/t/build-error-at-setup-ruby-need-help/8791/2)
