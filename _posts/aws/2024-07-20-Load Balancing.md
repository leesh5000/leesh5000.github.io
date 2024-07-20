---
title: Load Balancing
date: 2024-07-20 14:43:00 +09:00
categories: [AWS]
tags: [AWS]
---

> 이 문서는 불특정 다수에게 정보 전달을 목적으로 하는 문서가 아니며, **작성자가 학습한 내용을 정리하고 참고하기 위해 작성한 문서**입니다.
{: .prompt-tip}

## Load Balancing
---

**로드 밸런싱**은 여러 서버에 들어오는 트래픽을 분산시켜 서버의 부하를 분산시키는 기술

## Why use a Load Balancer?
---

- 애플리케이션을 단일 진입점으로 노출 시킬 수 있음 (ex. DNS)
- public traffic, private traffic을 분리 시킬 수 있음
- 애플리케이션의 부하를 분산 처리 할 수 있음

## Elastic Load Balancer
---

- AWS에서 제공하는 관리형(managed) 로드 밸런서 서비스
- AWS가 업데이트, 유지 보수, 어떠한 경우에도 동작하는 것을 보장
- AWS의 많은 서비스와 통합 가능 (ex. Auto Scailing Group, AWS Certificate Manager, Route 53, CloudWatch, etc)

### Health Checks

- 로드 밸런서가 인스턴스에 트래픽을 보내기 전에 인스턴스의 상태를 확인하는 기능
- 로드 밸런서가 해당 인스턴스에 트래픽을 보내도 되는지 확인 가능

## Types of Load Balancers
---

### Classic Load Balancer

- 1세대 로드밸런서
- 현재 AWS 사용하지 않는 것을 권장

### Application Load Balancer

- 2세대 로드밸런서
- 7계층(Application Layer)에서 동작
- HTTP, HTTPS, WebSocket 프로토콜 지원
- URL 기반 라우팅 지원
- Host-based routing 지원
- Query String, Headers routing 지원
- Microservice, 컨테이너 기반 애플리케이션에 가장 적합
- Target Group이 될 수 있는 것
  - EC Instances (Auto Scaling Group) - HTTP
  - Lambda Function - HTTP
  - Private IP Address - HTTP
  - ALB
  - ECS tasks

### Network Load Balancer

- 2세대 로드밸런서
- 4계층(Transport Layer)에서 동작
- ALB에 비해 성능이 더 좋음
  - 초당 수백만 건 요청 처리 가능
  - ~100ms 지연시간
- AZ 하나 마다 static IP를 가짐
- TCP, TLS(Secure TCP), UDP 프로토콜 지원
- Target Group이 될 수 있는 것
  - EC2 Instances (Auto Scaling Group) - TCP
  - Private IP Address - TCP
  - ALB

### Gateway Load Balancer

- 가장 최신의 로드밸런서
- 3계층(Network Layer)에서 동작
- IP 프로토콜 지원

