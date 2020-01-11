---
title: "gRPC"
date: 2020-01-11T21:44:15+09:00
categories: ["network"]
tags: ["protocol"]
---

# gRPC

## 1. 정의
gRPC(google remote procedure call)는 구글이 최초로 개발한 오픈 소스 원격 프로시저 호출 시스템이다.

## 2. 특징
* RPC framework
* Protocal을 정의 해놓고 쓰는 IDL(Interface Definition Language)이다.
* 구조화된 객체를 직렬화하기 위하여 **Protocal Buffers**를 사용한다.
* HTTP/2 기반으로 만들어져서 **양방향 스트리밍 데이터 처리**가 가능하다.
