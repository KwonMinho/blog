---
title: "OAuth2"
date: 2020-01-14T22:31:23+09:00
categories: ["auth"]
tags: ["OAuth2","etc"]
---
## OAuth. 왜 등장했을까?

보통 앱을 개발하다보면 앱 기능에 대형 플랫폼인 구글, 페이스북, 네이버, 카카오 등에서 제공하는 기능을 내포해야할 때가 있다. 이러한 제 3자의 플랫폼 서비스를 이용하기 위한 간단한 방법으로는 우리의 앱을 사용하는 클라이언트의 플랫폼 아이디와 비밀번호를 우리 앱에다가 저장해놓고 서비스를 이용하는 것이다.

이 방법에는 크게 3가지 문제가 있다. \
1. 클라이언트 입장에서 다른 앱을 사용하기 위해서 자신한테 중요한 플랫폼 아이디와 비밀번호를 맡겨야한다는 점이 불안할 것이다.
2. 개발 앱측에서도 클라이언트의 중요한 플랫폼 아이디와 비밀번호를 관리하는 비용과 부담은 말로 표현할 수 없을 정도로 크다.
3. 타 플랫폼 입장에서도 관리할 수 없는 리스크가 생긴다는 점이다.


**그래서 우리에게 필요한 것은 OAuth**

## 개념
OAuto의 주체는 크게 3가지로 구분된다.
* Client (타 플랫폼의 제한된 기능을 사용하는 주체: MyApp)
* Resource Owner (MyApp user)
* Resource Server (Other Platform)

Client가 Resource Server에 있는 자원을 사용하고 싶을 때 \
Resource Owner의 ID/Password를 사용하는 것이 아니라 \
제한된 리소스 사용을 허락하는 Access Token을 발급하는 기술이 OAuto 핵심개념이다.



## 과정

*Register 과정* \
Client하고 Resource Server간에 Access Token를 발행하기 위한 약속이 필요하다. 약속에 필요한 준비물은 크게 3가지이다.

* Client ID
* Client Screct
* Authorization Redirect URLs


![title](https://kwonminho.github.io/etc/auth.png)

1. Owner는 Client한테 요청한다.
2. Client는 Resource Server와 미리 합의한 정보를 바탕으로 리소스 서버에게 Redirect를 보낸다. (resouce server url?client_id&scope=a,b,c...)
3. Resource Server는 Owner한테 리소스 권한이 있는지 인증을 요구한다.
4. Owner가 인증을 통과했으면 Resource Server의 DB에 새로운 User 정보를 발급한다.
5. Resource Server는 요청 헤더에 Client의 콜백 주소를 담아 Owner한테 보낸다.
6. Owner가 눈치채지 못하게 Client(MyApp) 영역으로 넘어간다.
7. 이때 Resource Server가 보낸 요청헤더에는 Code 값이 들어있다. Code의 값을 Client가 다시 Resource Server한테 보낸다. (이 절차를 통해 완벽히 세 주체의 신뢰성이 확립)
8. Resource Server는 Access Token을 Client한테 보낸다.
9. Client는 Access Token을 자신의 DB에 보관한다.