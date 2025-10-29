## 문제 1  
분석 애플리케이션이 현재 주요 프로덕션 RDS 데이터베이스에서 쿼리를 수행하고 있습니다.  
이 쿼리들은 하루 중 언제든 실행되며, RDS의 성능을 저하시켜 사용자 경험에 영향을 줍니다.  
사용자 경험을 개선하기 위해 무엇을 해야 합니까?  

- Setup a Read Replica (읽기 복제본 구성) ⭕ 
- Setup Multi-AZ (다중 AZ 구성)  
- Run the analytics queries at night (야간에 분석 쿼리 실행)

---

## 문제 2  
RDS의 Read Replica와 Multi-AZ 모두에서 복제 방식에 대해 올바른 설명은 무엇입니까?  

- Read Replica는 비동기 복제(Asynchronous), Multi-AZ도 비동기 복제를 사용한다  
- Read Replica는 비동기 복제(Asynchronous), Multi-AZ는 동기 복제(Synchronous)를 사용한다  ⭕
- Read Replica와 Multi-AZ 모두 동기 복제를 사용한다  
- Read Replica는 동기 복제, Multi-AZ는 비동기 복제를 사용한다  

---

## 문제 3  
하나의 Aurora DB 클러스터에 최대 몇 개의 Aurora Read Replica를 생성할 수 있습니까?  

- 5  
- 10  
- 15  ⭕

---

## 문제 4  
RDS 데이터베이스에 Read Replica를 구성했지만,  
사용자들이 게시물을 업데이트한 후 바로 반영되지 않는다고 불평합니다.  
가능한 원인은 무엇입니까?  

- 애플리케이션의 버그  
- Read Replica는 비동기 복제를 사용하므로 “결국적 일관성(Eventual Consistency)”이 발생한다  ⭕
- Multi-AZ를 구성했어야 한다  

---

## 문제 5  
다음 중 IAM 데이터베이스 인증을 지원하지 않는 RDS 데이터베이스는 무엇입니까?  

- Oracle  ⭕
- PostgreSQL  
- MySQL  

---

## 문제 6  
ElastiCache Redis 클러스터에 접근할 때  
IAM 사용자 또는 역할을 통해 접근을 제어하고 보안을 강화하려면 어떻게 해야 합니까?  

- Redis Authentication 사용  
- IAM Authentication 사용  ⭕
- Security Group 사용  

---

## 문제 7  
MySQL 데이터베이스를 사용해야 하며,  
하나의 가용 영역(AZ)에 장애가 발생해도 데이터베이스가 가용해야 합니다.  
어떤 구성을 해야 합니까?  

- Read Replica 생성  
- Encryption 활성화  
- Multi-AZ 활성화  ⭕

---

## 문제 8  
RDS 데이터베이스에서 생성할 수 있는 최대 Read Replica 수는 몇 개입니까?  

- 5  
- 15  ⭕
- 7  

---

## 문제 9  
RDS 데이터베이스가 웹사이트 요청을 감당하기 어렵습니다.  
사용자 대부분은 뉴스를 읽기만 하고, 게시물 업데이트는 드뭅니다.  
이 문제를 해결하기에 적합하지 않은 방법은 무엇입니까?  

- ElastiCache 클러스터 사용  
- RDS Multi-AZ 구성  ⭕
- RDS Read Replica 구성  

---

## 문제 10  
Aurora 데이터베이스의 장기 백업을 저장해야 합니다.  
재해 복구 및 감사 용도로 사용할 예정입니다.  
어떤 방법을 권장합니까?  

- 자동 백업(Automated Backups) 활성화  
- 필요 시 백업(On-Demand Backups) 수행  ⭕
- Aurora Database Cloning 사용  

---

## 문제 11  
RDS PostgreSQL 데이터베이스에 대한 재해 복구 전략을 세워야 합니다.  
리전 장애가 발생해도 다른 리전에서 빠르게 읽기 및 쓰기 트래픽을 처리할 수 있어야 합니다.  
가장 좋은 방법은 무엇입니까?  

- 동일 리전에 Read Replica를 만들고, 메인 DB에서 Multi-AZ 활성화  
- 다른 리전에 Read Replica를 만들고, 그 Read Replica에서 Multi-AZ 활성화  ⭕
- 동일 리전에 Read Replica를 만들고, 그 Read Replica에서 Multi-AZ 활성화  
- 메인 데이터베이스에서 Multi-Region 옵션 활성화  

---

## 문제 12  
온프레미스의 MySQL 데이터베이스를 RDS로 마이그레이션했습니다.  
여러 개발자들이 각자 IAM 사용자로 AWS 계정에 존재합니다.  
각 개발자에게 개별 DB 계정을 만들지 않고 접근 권한을 주려면 어떻게 해야 합니까?  

- IAM 사용자는 기본적으로 RDS에 접근할 수 있다  
- Amazon Cognito 사용  
- IAM Database Authentication 활성화  ⭕

---

## 문제 13  
주 리전에서 재해가 발생하더라도 다른 AWS 리전에 데이터베이스 복제본이 존재하도록 하고 싶습니다.  
이를 쉽게 구현할 수 있는 데이터베이스는 무엇입니까?  

- RDS Read Replica  
- RDS Multi-AZ  
- Aurora Read Replica  
- Aurora Global Database  ⭕

---

## 문제 14  
Amazon RDS에서 지원하지 않는 데이터베이스는 무엇입니까?  

- MongoDB  ⭕
- MySQL  
- MariaDB  
- Microsoft SQL Server  

---

## 문제 15  
Amazon Aurora는 어떤 데이터베이스 엔진을 지원합니까?  

- MySQL과 MariaDB  
- MySQL과 PostgreSQL  ⭕
- Oracle과 MariaDB  
- Oracle과 MS SQL Server  

---

## 문제 16  
100개의 EC2 인스턴스가 RDS에 연결되어 있습니다.  
RDS 유지보수 중 애플리케이션이 재연결에 매우 오랜 시간이 걸립니다.  
이 문제를 개선하려면 어떻게 해야 합니까?  

- 모든 애플리케이션 코드를 수정한다  
- Multi-AZ를 비활성화한다  
- Multi-AZ를 활성화한다  
- RDS Proxy를 사용한다  ⭕

---

## 문제 17  
프로덕션 Node.js 애플리케이션이 RDS MySQL 5.6을 사용 중입니다.  
새로운 Java 애플리케이션이 정기적으로 분석 쿼리를 수행해야 합니다.  
비용 효율적이며 기존 서비스에 지장을 주지 않으려면 어떻게 해야 합니까?  

- Multi-AZ를 활성화하고 스탠바이 DB에서 분석 실행  
- 다른 AZ에 Read Replica를 생성하고 분석 쿼리를 그 Replica에서 실행  ⭕
- 다른 AZ에 Read Replica를 생성하고 분석 쿼리를 소스 DB에서 실행  

---

## 문제 18  
암호화되지 않은 RDS 인스턴스를 암호화하려면 어떻게 해야 합니까?  

- 콘솔에서 "Encrypt using KMS" 옵션으로 직접 암호화  
- 콘솔에서 인스턴스를 중지한 후 암호화  
- 스냅샷을 생성하고, 복사 시 "Enable Encryption"을 체크한 후 복원  ⭕

---

## 문제 19  
SQL 연결 문자열을 변경하지 않아도 되는 RDS(※ Aurora 제외) 기능은 무엇입니까?  

- Multi-AZ  ⭕
- Read Replica  

---

## 문제 20  
게임 회사에서 실시간 점수 기반 랭킹 보드를 구현해야 합니다.  
효율적이고 고가용성의 솔루션을 설계하려면 어떤 서비스를 사용해야 합니까?  

- RDS for MySQL  
- Amazon Aurora  
- ElastiCache for Memcached  
- ElastiCache for Redis (Sorted Sets)⭕  

---

## 문제 21  
AWS에서 Oracle 데이터베이스를 완전히 커스터마이징하여 사용하고자 합니다.  
AWS 서비스의 장점도 함께 활용하려면 어떤 방식을 추천합니까?  

- RDS for Oracle  
- RDS Custom for Oracle  ⭕
- EC2에 Oracle 직접 배포  

---

## 문제 22  
암호화되지 않은 RDS DB 인스턴스에서 Read Replica를 생성하려 합니다.  
이때 Read Replica를 암호화할 수 있습니까?  

- No  ⭕
- Yes  

---

## 문제 23  
프로덕션 환경에서 Aurora 클러스터를 사용하는 애플리케이션이 있습니다.  
개발팀은 낮은 비용으로 축소된 환경에서  
필요할 때만 무거운 작업을 수행하고 싶어 합니다.  
비용 절감에 적합한 방법은 무엇입니까?  

- Aurora Global Database 사용  
- RDS 데이터베이스 사용  
- Aurora Serverless 사용  ⭕
- EC2에 Aurora를 배포하고 야간에 EC2를 중지하는 스크립트 작성  

---

## 문제 24  
개발팀이 프로덕션 Aurora 데이터베이스의 데이터를 활용하여  
읽기/쓰기 테스트를 수행하고자 합니다.  
어떻게 해야 합니까?  

- Aurora Read Replica를 생성하여 테스트  
- 프로덕션 데이터베이스에서 직접 테스트  
- DB 스냅샷 생성 후 복원하여 새 DB에서 테스트  
- Aurora Cloning 기능 사용  ⭕

---

## 문제 25  
Auto Scaling Group과 ALB 뒤에서 동작하는 웹 애플리케이션에서  
사용자가 계속 로그인 상태를 잃습니다.  
Sticky Session을 활성화하고 싶지 않습니다.  
어떻게 해야 합니까?  

- EC2에 직접 커스텀 로드밸런서를 구축한다  
- 세션 데이터를 RDS에 저장한다  
- 세션 데이터를 ElastiCache에 저장한다  ⭕
- 세션 데이터를 공유 EBS 볼륨에 저장한다  
