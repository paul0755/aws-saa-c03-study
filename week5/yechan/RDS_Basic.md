# 🧠 AWS RDS / Aurora / ElastiCache 핵심 개념 정리

---

## 🔹 Amazon RDS (Relational Database Service)

### ✅ 개요
- 완전관리형 관계형 데이터베이스 서비스  
- AWS에서 DB 설치, 백업, 패치, 복제, 장애 복구 자동화  
- 지원 엔진: **MySQL, PostgreSQL, MariaDB, Oracle, Microsoft SQL Server**

---

## 🔹 RDS Read Replica (읽기 복제본)

- **비동기(Asynchronous) 복제**를 사용  
- 주로 읽기 트래픽 분산용 (쓰기 불가)  
- 최대 5개(일반 RDS) / 15개(Aurora)까지 생성 가능  
- 복제 지연(Lag)이 발생할 수 있음 → “Eventual Consistency”  
- 주 DB 부하를 줄이기 위해 분석/리포트 쿼리 실행에 적합  
- **DR(재해 복구)** 용도로 Cross-Region Read Replica 가능  

> ⚠️ 쓰기 작업 후 바로 반영되지 않는 이유 = 비동기 복제 지연 때문  

---

## 🔹 RDS Multi-AZ (다중 가용 영역 구성)

- **동기(Synchronous) 복제** 사용  
- 한 AZ에 Primary, 다른 AZ에 Standby 구성  
- Primary 장애 시 자동 Failover  
- 고가용성(High Availability) 보장  
- **읽기 트래픽 분산 X**, standby는 대기용  

> 💡 Multi-AZ는 성능 향상용이 아닌 가용성(Availability) 보장을 위한 구성이다.

---

## 🔹 Amazon Aurora

- AWS가 직접 개발한 **클라우드 전용 고성능 RDB 엔진**  
- MySQL / PostgreSQL 호환  
- **저장소 자동 확장 (최대 128TB)**  
- **복제본 최대 15개 (Aurora Replicas)**  
- **Cluster Volume**: 자동 복제 6개 복제본(3개 AZ에 분산 저장)  
- **Failover** 시 읽기 복제본이 자동으로 Primary 승격  

### 🌀 Aurora Global Database
- 다중 리전에 걸쳐 읽기 복제본 구성 가능  
- 재해 복구 시 다른 리전으로 빠른 Failover 지원  

### 🌙 Aurora Serverless
- **자동으로 스케일 인/아웃**되는 서버리스 버전  
- 사용량이 적을 때 자동 중지 → 비용 절감  
- 개발/테스트 환경, 간헐적 워크로드에 적합  

---

## 🔹 IAM Database Authentication

- IAM 사용자/역할로 DB에 로그인 가능  
- DB 사용자 자격 증명(비밀번호) 대신 **임시 토큰 기반 인증**  
- **MySQL, PostgreSQL** 지원  
- Oracle, SQL Server는 지원하지 않음  

---

## 🔹 RDS Proxy

- 애플리케이션과 DB 사이의 **연결 풀(Connection Pool)** 역할  
- DB 연결 수를 효율적으로 관리하여 성능 향상  
- DB 재시작, 장애 조치 시 빠른 연결 복구 지원  
- Multi-AZ 환경에서 연결 지연 문제를 완화  

> 💡 다수의 EC2 인스턴스가 동시에 RDS를 재연결해야 할 때 유용  

---

## 🔹 RDS Encryption (암호화)

- KMS(Key Management Service)를 이용하여 데이터 암호화  
- 이미 생성된 **비암호화 DB → 직접 암호화 불가**
- 방법:  
  1. 스냅샷 생성  
  2. 스냅샷 복사 시 “Enable Encryption” 선택  
  3. 암호화된 스냅샷으로 새 인스턴스 복원  

> ⚠️ 암호화되지 않은 DB 인스턴스에서 **암호화된 Read Replica**는 직접 생성 불가  

---

## 🔹 RDS Backup

- **Automated Backups (자동 백업)**  
  - 매일 백업 수행  
  - 지정된 보존 기간(최대 35일) 내에서 복원 가능  

- **Manual Snapshot (수동 백업)**  
  - 사용자가 직접 생성  
  - 영구 저장 가능 (삭제 전까지 유지)  

> 💡 재해 복구(Disaster Recovery) 목적이라면 자동 백업보다 스냅샷 보관이 안정적  

---

## 🔹 ElastiCache (In-memory Caching)

- Redis / Memcached 엔진 지원  
- 데이터베이스 부하 감소 및 응답 시간 단축  

### Redis vs Memcached
| 구분 | Redis | Memcached |
|------|--------|------------|
| 구조 | Key-Value + 자료구조 지원 (List, Set 등) | 단순 Key-Value |
| 지속성 | 스냅샷 저장 가능 | 비영속 |
| 복제 | Master/Replica 지원 | 단일 노드 중심 |
| 세션관리 | 가능 | 제한적 |
| 사용예시 | 실시간 랭킹, 세션저장, 캐시 | 단순 캐시 |

### Redis Sorted Set
- 실시간 **랭킹 시스템(Leaderboard)** 구현에 사용  
- 각 사용자 점수를 기준으로 자동 정렬  

---

## 🔹 RDS Proxy + Auto Scaling + ALB 연계 개념

- ALB 뒤의 EC2 인스턴스들이 DB에 직접 연결 시,  
  연결이 너무 많아지면 DB 세션 과부하 발생  
- RDS Proxy를 두면 **연결 재활용 및 풀링** 가능  
- 세션 관리는 ElastiCache (Redis 등)에 저장하여 로그인 유지  

> ⚙️ Sticky Session 없이도 사용자 세션 유지 가능  

---

## 🔹 DB 확장성 (Scalability)

| 유형 | 설명 | 예시 |
|------|------|------|
| 수직 확장 (Vertical Scaling) | 인스턴스 스펙 업그레이드 | r4.large → r4.4xlarge |
| 수평 확장 (Horizontal Scaling) | 인스턴스 수를 늘려 부하 분산 | Read Replica 추가 |

---

## 🔹 일관성 모델 (Consistency)

| 용어 | 설명 |
|------|------|
| **Strong Consistency** | 쓰기 후 즉시 읽기 일관성 보장 |
| **Eventual Consistency** | 일정 시간 후 일관성 수렴 (Read Replica에서 발생 가능) |

---

## 🔹 DR(Disaster Recovery) 전략 요약

| 목적 | 구성 |
|------|------|
| **AZ 장애 복구** | Multi-AZ |
| **Region 장애 복구** | Cross-Region Read Replica or Aurora Global DB |
| **장기 백업 보존** | Snapshot 복사 및 S3 저장 |

---

## 🔹 개발 / 테스트 환경용 저비용 구성

- **Aurora Serverless** : 필요 시 자동 실행, 유휴 시 자동 중지  
- **스냅샷 복원** : 프로덕션 데이터 복제 후 독립된 테스트 환경 구축  
- **Aurora Cloning** : 빠른 복제본 생성, 대용량 데이터 테스트에 효율적  

---

## 🔹 정리 키포인트

- Read Replica → 비동기 복제, 읽기 부하 분산  
- Multi-AZ → 동기 복제, 장애 조치용 (읽기 X)  
- Aurora → 고가용성, 고성능, 자동 확장형 DB  
- IAM DB Auth → MySQL/PostgreSQL만 지원  
- RDS Proxy → 연결 풀링으로 성능 안정화  
- Redis Sorted Set → 실시간 순위 구현  
- Aurora Serverless → 유휴 시간 비용 절감형 DB  
- Multi-Region Read Replica → 리전 단위 DR 구성  

---
