---
title: Amazon RDS
date: 2024-07-29 19:11:00 +09:00
categories: [AWS]
tags: [AWS]
---

## Overview
---

- Amazon RDS(Relational Database Service)는 AWS 관리형 서비스로 관계형 데이터베이스를 쉽게 설정, 운영 및 확장할 수 있도록 지원하는 서비스
- PostgreSQL, MySQL, MariaDB, Oracle, SQL Server, Aurora 등 다양한 데이터베이스 엔진을 지원

## Advantage over using RDS vs Deploying Database on EC2 
---

- RDS is a managed service
  - Automated backups, OS patching, monitoring, scaling, and replication
  - No need to worry about the underlying infrastructure
  - Monitoring dashboards
  - Read replicas for read performance
  - Multi-AZ for DR(Disaster Recovery) (High Availability)
  - Scaling capability (vertical and horizontal)
- you can't SSH into the RDS instances

## RDS Storage Auto Scaling
---

- RDS 스토리지가 부족할 경우 자동으로 스토리지를 확장할 수 있는 기능
- 최대 스토리지 Threshold 설정하여 자동으로 확장할 수 있음
- `unpredictable workloads`에 유용

## RDS Read Replicas for read scalability
---

- `Read Replicas`는 Master DB의 복제본으로, 읽기 작업을 분산시키기 위해 사용
- ASYNC Replication으로 이루어지며, Master DB에 영향을 주지 않음 ([eventual consistency](https://ko.wikipedia.org/wiki/%EA%B6%81%EA%B7%B9%EC%A0%81_%EC%9D%BC%EA%B4%80%EC%84%B1))
  - 복제본을 Master로 승격할 수 있음
- 일반적으로, AWS의 네트워크 비용은 AZ를 이동할 때 발생
  - 다만, Managed Service 들은 이 관례에 맞지 않음
  - `RDS read replica`의 경우도 마찬가지로 같은 리전에 대해서는 비용이 발생하지 않음

## RDS Multi-AZ (Disaster Recovery)
---

- SYNC Replication
  - 마스터 DB에 변화가 생길 경우, 즉시 stand-by DB에 반영
- 전체 AZ, 혹은 네트워크가 실패할 경우를 위한 방지책
- 자동으로 stand-by가 master로 승격





