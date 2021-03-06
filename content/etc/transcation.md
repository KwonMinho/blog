---
title: "Transcation"
date: 2020-01-02T00:35:31+09:00
categories: ["etc"]
tags: ["term"]
---
# 트랜잭션

## 1. 정의
    DB 상태를 변화시키기 위한 하나의 논리적 기능을 수행하기 위한 작업의 단위 또는 한꺼번에 모두 수행되어야할 일련의 연산

## 2. 특징
    1. 트랜잭션은 DB 시스템에서 병행 제어 및 회복 작업 시 처리되는 작업의 논리적 단위이다.
    2. 사용자 요청에 시스템이 응답하기 위한 상태 변환 과정의 작업단위이다.
    3. 하나의 트랜잭션은 Commit or Rollback 된다.

## 3. 성질
*Atomicity:* 트랜잭션 연산은 모두 반영되거나 반영되지 않아야 한다. 연산에 하나라도 오류가 있으면
트랜잭션은 전부 취소되어야 한다.\
*Consistency:* 트랜잭션의 작업이 성공적으로 완료하면 언제나 일관성 있는 DB 상태로 변환한다. \
*Isolation:* 둘 이상의 트랜잭션이 동시에 병행 실행되는 경우 어느 하나의 트랜잭션 실행중에 다른 트랜잭션 연산이 끼어들 수 없다. \
*Durablility:* 성공적으로 완료된 트랜잭션의 결과는 시스템이 고장나더라도 영구적으로 반영되어야 한다.

## 4. commit, rollback 연산
*commit:* 하나의 트랜잭션이 성공적으로 끝났다는 걸 알려주는 연산이다. 이 연산을 사용하면 트랜잭션이 로그에 저장된다. \
*rollback:* 하나의 트랜잭션처리가 비정상적으로 종료되어 트랜잭션의 원자성이 깨진경우, 트랜잭션을 다시 시작하거나 트랜잭션의 부분적으로 연산된 결과를 취소시킨다.