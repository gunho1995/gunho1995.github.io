---
layout: post
title: "맥과 윈도우에서 블로그 포스팅 시 에러"
subtitle: "CRLF error"
categories: ETC
tags: 
comments: true
---



나는 맥 OS와 윈도우 OS 모두 사용하여 포스팅을 한다.

이 때 포스트 작성 후, add 작업을 거칠 때 항상 에러 메시지가 나타난다.


---
Warning : CRLF will be replaced by LF in some/file.file.
The file will have its original line endings in your work directory
---

각 OS에서 문장의 끝을 나타낼 때 사용하는 기호가 다르기 때문에 발생하는 에러이다.

맥 OS에서는 LF (Line Feed), 윈도우 OS에서는 CR(Carriage Return)으로 이루어지기 때문인데,
이를 해결하기 위해서 git 에서 자동 변환해주는 core.autocrlf 기능을 적용하면 된다.

적용하는 방법은 매우 간단하다


윈도우에서 작업하는 경우:

---
git config --global core.autocrlf true
---

맥에서 작업하는 경우:

---
git config --global core.autocrlf true input
---

을 적용해주면 된다.
