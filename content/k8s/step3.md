---
title: "쿠버네티스의 기본 오브젝트"
date: 2020-01-08T23:18:01+09:00
categories: ["cloud-native"]
tags: ["k8s"]
---

## 1. k8s의 기본 오브젝트


### 1.1 Pod

파드는 쿠버네티스의 기본 작업 단위로 스케줄링이 될 단일 컨테이너나 컨테이너의 그룹을 지정한다. 하나의 파드안에 있는 컨테이너 그룹들은 localhost 통신이 가능하다.

### 1.2 Deployment

디폴로이먼트는 파드를 선언적으로 관리하는 고수준 쿠버네티스 리소스다. 배포, 스케줄링, 업데이트 작업을 수행하며 필요한다면 파드를 재시작한다.

### 1.3 레플리카셋
디폴로이먼트는 직접 파드를 관리하지 않는다. 파드 관리는 레플리카셋 오브젝트가 수행한다. 파드가 사용자에 의해서 저앻진 스펙보다 너무 적거나 많은 파드가 존재하면, 레플리카셋 컨트롤러는 **이런 상태를 바로 잡기 위해 일부 파드를 실행하거나 중지한다.**

디폴로이먼트는 이런 레플리카셋을 관리한다. 디폴로이먼트를 업데이트하면 새로운 레플리카셋, 새로운 파드가 시작된다. 이전의 레플리카셋과 파드는 종료된다.

### 1.4 스케줄러

1. 디폴로이먼트가 새로운 레플리카셋을 필요하다고 판단하면, 쿠버네티스 데이터베이스에 파드 리소스를 직접 생성한다.
2. 동시에 이 파드는 **스케줄러 수신함**과 같은 대기열에 추가된다.

이때, **스케줄러의 역할**이 나온다.
1. 아직 대기열에서 스케줄링되지 않은 파드를 찾아 배치하고 실행할 노드를 찾는다.
2. 이때 적절한 노드를 찾기 위해 *파드 리소스*을 포함한 *몇 가지 사항을(추후설명)* 기준으로 삼는다.
3. 스케줄링이 완료되면 노드에 돌고 있는 kubelet에게 실제로 컨테이너를 실행하라고 요청한다.


참고
* (feat. 엔지니어 줄리아 에번스가 작성한 [쿠버네티스 스케줄러 작동원리 참고])
* https://thenewstack.io/implementing-advanced-scheduling-techniques-with-kubernetes/


### 1.5 서비스

생성한 파드를 어떻게 찾아가야 할까? 파드가 배포될 때마다 IP 주소(쿠버네티스에서 할당된)를 찾고 애플리케이션의 포트 번호를 연결하면 된다. **그러나 파드는 컨트롤러에 의해서 재시작 될 수 있고 IP 주소도 계속 바뀐다.** 그렇기에 이런 방법은 좋지 못하다.

실망하기에는 이르다. 이런 문제를 해결할 쿠버네티스에서 훌륭한 오브젝트가 있다. **서비스 리소스는 파드에 자동으로 라우팅되는 영구적인 IP주소와 DNS 주소를 제공한다.**

서비스에는 *selector* 항목이 있다. selector는 서비스에 라우팅할 파드를 알려준다.

## 2. 리소스 매니페스트

kubectl run 명령어로 디폴로이먼트 하는 것은 한정적이다. **k8s는 근본적으로 선언형 시스템이다.** 현재 상태에서 의도한 상태로 계속해서 조정해나가는 시스템이다.

쿠버네티스의 오브젝트, 즉 *리소스*는 **모두 내부 데이터베이스에 기록된다.**


매니페스트란 **리소스에 대한 의도한 상태의 스펙을 의미한다.** 이러한 리소스의 상태를 정의해놓은 매니페스트를 쿠버네티스에게 전달하여 오브젝트를 생성한다.


## 3. 쿠버네티스 패키지 매니저:헬름

헬름은 명령줄 도구로 직접 만들거나 다른 사람에 의해서 만들어진 *차트*라는 패키지를 생성할 수 있고 이 패키지를 통해 애플리케이션 실행에 필요한 리소스, 의존성, 구성 가능한 변수를 지정할 수 있다.

    헬름은 APT나 YUM과 같은 바이너리 소프트웨어 패키지와는 달리 실제로 컨테이너 이미지자체를 포함하지 않는다. 쿠버네티스가 지정한 위치에 바이너리 컨테이너 이미지를 다운로드 할 뿐이다. 헬름은 YAML 매니페스트를 둘러싼 Wrapper에 불과하다.