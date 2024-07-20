---
title: EC2 Instance Storages
date: 2024-07-16 19:11:00 +09:00
categories: [AWS]
tags: [AWS]
---

> 이 문서는 불특정 다수에게 정보 전달을 목적으로 하는 문서가 아니며, **작성자가 학습한 내용을 정리하고 참고하기 위해 작성한 문서**입니다.
{: .prompt-tip}

## EBS Volume
---

- EC2 인스턴스에 사용하는 `network drive`
  - EC2 <-> EBS는 서로 네트워크로 통신하므로 약간의 latency 존재
- EC2 인스턴스가 중단/종료되어도 데이터는 보존
- AZ에 종속적
  - 다른 AZ로 이동하려면 EBS snapshot을 이용해야 함

### EBS Snapshot

- 특정 시점에 대한 EBS 볼륨의 백업
- AZ나 Region을 넘어 복사 가능
- 스냅샷 생성 시, EC2 인스턴스와 detach 할 필요는 없지만 공식 문서 권장 사항
- EBS Snapshot Archive
  - EBS 스냅샷을 더 저렴하게 보관 가능
  - 하지만, 복원 시 24 - 72시간 까지 소요
- Fast Snapshot Restore
  - EBS 스냅샷을 매우 빠르게 복원 가능
  - 하지만, 가격이 비쌈

### EBS Volume Types

- gp2 / gp3 (SSD) : 범용 스토리지
- io1 / io2 (SSD) : 고성능 스토리지
- st1 (HDD) : 자주 엑세스하는 더 저렴한 스토리지
- sc1 (HDD) : 자주 액세스하지 않는 가장 저렴한 스토리지
- gp2/gp3/io1/io2만 부트 볼륨으로 사용
- io1/io2 스토리지는 스토리지 하나에 여러 EC2 인스턴스를 부착 가능

### EBS Encryption

## EFS
---

- 여러 EC2 인스턴스에 마운트 될 수 있는 관리형 NFS(Network File System)
- 여러 AZ의 EC2 인스턴스들에 부착 가능
- high availability, scalable but expensive
- Only for Linux Based Instance (POSIX)
- EFS-IA 기능을 사용하여 비용 절감 가능

## EC2 Instance Store
---

- EBS보다 고성능 하드웨어 디스크
- EC2 인스턴스가 중단/종료되면 데이터 손실 (ephemeral)
- 장애가 발생할 경우 데이터 손실 위험
