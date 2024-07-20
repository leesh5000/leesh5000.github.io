---
title: Scalability & High Availability
date: 2024-07-20 14:44:00 +09:00
categories: [AWS]
tags: [AWS]
---

> 이 문서는 불특정 다수에게 정보 전달을 목적으로 하는 문서가 아니며, **작성자가 학습한 내용을 정리하고 참고하기 위해 작성한 문서**입니다.
{: .prompt-tip}

## Scalability
---

- 애플리케이션이 조정을 통해 더 많은 부하를 처리할 수 있는 능력

### 수직적 확장(Vertical Scaling)

- 인스턴스의 크기를 늘리는 것
- 분산시스템이 아닌 환경에서 사용하기 좋음 (ex. Database)
- 일반적으로 한계가 존재
- `Scale Up` 이라고도 함
- ex) EC2 인스턴스의 CPU, RAM 업그레이드

### 수평적 확장(Horizontal Scaling)

- 인스턴스의 수를 늘리는 것
- 분산시스템에서 사용
- `Scale Out`, `elasticity` 라고 도 함
- ex) Auto Scaling

## High Availability
---

- 시스템이 정상적으로 작동하는 시간을 최대화하는 능력
- 시스템을 두 개의 물리적 위치가 서로 다른 데이터 센터에 배포하여 고가용성을 확보
- 데이터센터의 손실에서 생존하는 것을 목표로 함

## Elasticity
---

- 시스템을 자유롭게 확장 및 축소할 수 있는 능력
- 일반적으로 `Scailability`의 Scale Out과 같은 의미로 사용