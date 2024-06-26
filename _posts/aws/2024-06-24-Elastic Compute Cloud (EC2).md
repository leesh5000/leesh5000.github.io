---
title: Elastic Compute Cloud (EC2)
date: 2024-06-24 22:40:00 +09:00
categories: [AWS]
tags: [AWS]
---

## EC2
---

- EC2는 AWS의 가장 대중적인 IaaS 서비스
- 유저가 필요할 때 사용 가능 (On-Demand)

## EC2 설정 옵션
- - -

- Operating System (OS) : Linux, Windows, Mac
- Computing Power & Core (CPU)
- Memory (RAM)
- Storage
    - network-attached storage (EBS, EFS)
    - hardware (Instance Store)
- Network Card
    - Public IP, Elastic IP
- Firewall rules
    - Security Group
- Bootstrap script
    - EC2 UserData

## EC2 User Data
***

- EC2 인스턴스가 시작될 때 실행되는 스크립트
- 사용 사례
    - 업데이트 설치, 소프트웨어 설치 등
- User Data 는 루트 계정으로 실행되므로 모든 명령어는 `sudo` 로 실행 됨

## EC2 Instance Types
-------------------------

- EC2 인스턴스는 아래와 같은 이름 규칙이 있음
    - `ex) m5.2xlarge`
        - m : 인스턴스 패밀리
        - 5 : 세대
        - 2xlarge : 같은 인스턴스 패밀리 사이에서의 사이즈

### EC2 인스턴스 패밀리

#### General Purpose

- m 패밀리, t 패밀리
- Use cases : 웹 서버, 코드 리포지토리, CI/CD 등 다양한 워크로드에 사용하기 좋음

#### Compute Optimized

- c 패밀리
- Use cases : 배치 프로세싱, 고성능 웹서버, 머신러닝, 멀티미디어, 게임 서버 등에 적합

#### Memory Optimized

- r 패밀리, x1 패밀리 등
- 메모리 상에서 많은 데이터를 처리하는 워크로드에 적합
- Use cases : 데이터베이스, 분석, 캐싱, 대규모 분산 메모리 캐시, 대규모의 비정형 데이터를 처리하는 실시간 애플리케이션 등에 적합

#### Storage Optimized

- i 패밀리, d2 패밀리 등
- 로컬 스토리지에서 많은 양의 데이터에 I/O하는 워크로드에 적합
- Use cases : RDB/NoSQL DB, 데이터 웨어하우스, Elasticsearch, 분산 파일 시스템 등에 적합

- 인스턴스 유형별 비교는 https://instances.vantage.sh/ 를 참고

## Security Group
---

- EC2 인스턴스에 대한 인바운드 및 아웃바운드 트래픽을 제어하는 `방화벽`
- 보안 그룹은 `allow(허용)` 규칙만 포함
- 보안 그룹은 IP 주소, 다른 보안 그룹을 참조할 수 있음
- 보안 그룹은 아래 사항들을 제어할 수 있음
    - 인바운드 트래픽
    - 아웃바운드 트래픽
    - 트래픽 소스
    - 트래픽 대상
    - 트래픽 포트
    - 트래픽 프로토콜
    - ...
- 보안 그룹은 여러 인스턴스들에 설정 가능
- 보안 그룹은 Region/VPC 에 종속 -> 다른 Region/VPC 간에 보안 그룹을 공유할 수 없음
- 보안 그룹은 EC2에서 실행하는 것이 아닌 EC2 외부에서 설정되는 것
- `Best Practice`: SSH 접근을 위한 별도의 보안 그룹을 분리할 것을 권장
- `타임 아웃으로 애플리케이션에 접근할 수 없으면 보안 그룹의 문제일 가능성이 높음`
- `보안 그룹간의 참조로 방화벽을 구성하면, IP를 알지 않아도 되기 때문에 유지보수가 용이함`

## Well-Known Ports
---

- 22 : SSH (Secure Shell) - login to a Linux instance
- 22 : SFTC (Secure File Transfer Protocol) - upload files to a file server
- 21 : FTP (File Transfer Protocol) - upload files to a file server
- 80 : HTTP - access a web server
- 443 : HTTPS - access a secure web server
- 3389 : RDP (Remote Desktop Protocol) - login to a Windows instance

## EC2 Instances Purchase Options (Resort case)
---

### On-Demand

- 필요한 만큼의 컴퓨팅 리소스를 사용하고, 시간 단위로 지불
- 가장 비용이 비싸다.
- 사용 사례: 단기적이고 중단이 없는 워크로드, 애플리케이션의 거동을 예측할 수 없는 경우
- ex) 내가 필요할 때 전체 가격을 지불하고 리조트 예약

### Reserved

- 1년 또는 3년 동안 특정한 인스턴스를 예약
- On-Demand에 비해 최대 72% 할인 제공
- 사용 사례: 사용량이 일정한 애플리케이션
- ex) 미리 계획을 짜고, 1년 내지 3년 사용 예약을 함 (기간이 길수록 많은 할인을 받음)

### Savings Plans

- 1년 또는 3년 동안 일정 사용량을 약정 구매
- 사용량이 넘어가면, On-Demand 가격으로 지불
- 사용 사례: 장기적인 워크로드
- ex) 리조트에 일정 기간 동안 머물 것을 약정 구매

### Spot Instances

- AWS의 미사용 컴퓨팅 리소스를 저렴하게 사용
- 가장 할인 폭이 큼
- 지정한 가격보다 인스턴스 가격이 높아지면, 인스턴스가 종료됨
- 사용 사례: 인스턴스 종료에 회복력이 있는 워크로드에 적합 (ex. Batch Job, 데이터 분석, 이미지 처리, 분산 처리 워크로드 등)
- ex) 리조트에서 빈 객실을 처리하기 위해 마지막 파격 할인을 제공

### Dedicated Hosts

- 전체 물리 서버를 예약, 인스턴스 배치를 제어 가능
- 전용 호스트를 사용하여 인스턴스를 실행
- 사용 사례: 법규 준수 요건이 있는 사례나 소프트웨어 라이선스 문제가 있는 경우
- ex) 리조트 건물 전체를 예약

### Dedicated Instances

- 다른 AWS 유저들과 하드웨어를 공유하지 않음
- 사용 사례: 소프트웨어 라이선스 문제, 하드웨어의 물리적 위치를 제어해야 하는 경우

### Capacity Reservations

- 원하는 기간동안 특정한 AZ에 용량 예약하고 필요할 때마다 사용 가능
- 사용 사례: 예측 가능한 워크로드
- ex) 리조트를 예약을 해두고 사용할 지 안할지는 마음대로 결정

```tip
- On-Demand, Reserved, Savings Plans는 인스턴스를 예약하는 방법
```

```
- Spot Instances, Dedicated Hosts, Dedicated Instances, Capacity Reservations는 인스턴스를 예약하지 않는 방법
```

`tip
`

- hihi~~hi~~
- hihihi<mark>hi</mark>

EC2는

: AWS 서비스이다

> HELLO

>tip HELLO

> An example showing the `tip` type prompt.
{: .prompt-tip }
