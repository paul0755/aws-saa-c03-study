# RDS, Aurora, & ElastiCache Quiz

1. 하나의 **Aurora DB Cluster**에서 가질 수 있는 **Aurora Read Replica**의 최대 개수는 얼마입니까?
    
    ① 5
    
    ② 10
    
    ③ 15 ✅
    

---

1. 회사의 프로덕션 **Node.js** 애플리케이션이 **RDS MySQL 5.6**을 데이터베이스로 사용하고 있습니다. 새로운 **Java** 애플리케이션이 정기적으로 무거운 분석 작업을 수행하여 대시보드를 생성할 예정입니다. 메인 애플리케이션의 중단을 최소화하면서 **비용 효율적인 방법**은 무엇입니까?
    
    ① **RDS Multi-AZ**를 활성화하고, 대기(standby) 데이터베이스에서 분석 작업을 수행한다. ❌
    
    ② **다른 AZ에 Read Replica를 생성**하고, 복제본 데이터베이스에서 분석 작업을 수행한다. ✅
    
    ③ **다른 AZ에 Read Replica를 생성**하고, 원본(source) 데이터베이스에서 분석 작업을 수행한다.
    
    > **Read Replica는 분석, 리포팅, 백업, 오프로드 작업을 위한 정석적인 해결책**
    > 

---

1. 온프레미스의 **MySQL 데이터베이스**를 **RDS**로 마이그레이션했습니다. 많은 애플리케이션과 개발자가 데이터베이스에 접근해야 하며, 각 개발자는 회사의 **AWS 계정에 IAM 사용자**로 존재합니다. 각 사용자별 DB 계정을 만들지 않고 **RDS MySQL DB 인스턴스** 접근 권한을 부여하는 적절한 방법은 무엇입니까?
    
    ① 기본적으로 IAM 사용자는 RDS 데이터베이스에 접근할 수 있다.
    
    ② **Amazon Cognito**를 사용한다.
    
    ③ **IAM Database Authentication**을 활성화한다. ✅
    

---

1. 프로덕션 환경의 애플리케이션이 **Aurora Cluster**를 데이터베이스로 사용 중입니다. 개발팀은 축소된 규모의 애플리케이션을 테스트 환경에서 실행하고, 필요 시 무거운 워크로드를 수행하고자 합니다. 대부분의 시간에는 애플리케이션이 사용되지 않습니다.
    
    **비용을 최소화**하면서 이를 달성할 방법은 무엇입니까?
    
    ① **Aurora Global Database**를 사용한다.
    
    ② **RDS 데이터베이스**를 사용한다.
    
    ③ **Aurora Serverless**를 사용한다. ✅
    
    ④ **Aurora를 EC2에서 실행**하고, 밤에는 EC2 인스턴스를 종료하는 스크립트를 작성한다.
    

---

1. 다음 중 **IAM Database Authentication**을 지원하지 않는 **RDS 데이터베이스 기술**은 무엇입니까?
    
    ① Oracle ✅
    
    ② PostgreSQL
    
    ③ MySQL
    

---

1. 하나의 **RDS 데이터베이스**에서 가질 수 있는 최대 **Read Replica** 수는 얼마입니까?
    
    ① 5
    
    ② 15 ✅
    
    ③ 7
    

---

1. **Amazon RDS**가 지원하는 데이터베이스 중, 다음 중 **지원하지 않는 것**은 무엇입니까?
    
    ① MongoDB ✅
    
    ② MySQL
    
    ③ MariaDB
    
    ④ Microsoft SQL Server
    

---

1. **RDS Read Replica**와 **Multi-AZ** 모두에 대한 복제 방식 중 올바른 설명은 무엇입니까?
    
    ① Read Replica는 **비동기 복제**, Multi-AZ는 **비동기 복제**를 사용한다.
    
    ② Read Replica는 **비동기 복제**, Multi-AZ는 **동기 복제**를 사용한다. ✅
    
    ③ Read Replica는 **동기 복제**, Multi-AZ는 **동기 복제**를 사용한다.
    
    ④ Read Replica는 **동기 복제**, Multi-AZ는 **비동기 복제**를 사용한다.
    

---

1. 암호화되지 않은 **RDS DB 인스턴스**에서 **Read Replica**를 생성하려고 합니다.
    
    이때 **Read Replica를 암호화**할 수 있습니까?
    
    ① No ✅
    
    ② Yes ❌
    
    > Read Replica는 원본 DB의 스냅샷을 기반으로 생성되므로,
    > 
    > 
    > **원본 DB가 암호화되어 있지 않으면 Replica도 암호화되지 않은 상태로 생성**
    > 

---

1. 100개의 **EC2 인스턴스**가 **RDS 데이터베이스**에 연결되어 있습니다.
데이터베이스 유지보수 중, 애플리케이션들이 RDS에 다시 연결하는 데 오랜 시간이 걸립니다.
이 문제를 해결하려면 어떻게 해야 합니까?
    
    ① 모든 애플리케이션 코드를 수정한다.
    
    ② **Multi-AZ**를 비활성화한다.
    
    ③ **Multi-AZ**를 활성화한다.
    
    ④ **RDS Proxy**를 사용한다. ✅
    

---

1. 우리의 **RDS 데이터베이스**는 웹사이트 요청을 감당하기 어렵습니다.
사용자는 대부분 뉴스를 읽기만 하고, 게시 빈도는 낮습니다.
다음 중 이 문제에 **적합하지 않은 해결책**은 무엇입니까?
    
    ① **ElastiCache Cluster** ❌
    
    ② **RDS Multi-AZ** ✅
    
    ③ **RDS Read Replicas**
    
    > Multi-AZ는 **장애 복구(HA)** 목적이지, **성능 확장(Scaling)** 용이 아님
    > 

---

1. 당신의 애플리케이션은 **Auto Scaling Group**으로 관리되는 **EC2 인스턴스**에서 실행되고 있으며, 그 앞단에는 **Application Load Balancer**가 있습니다. 사용자들이 계속 다시 로그인해야 하는 문제가 발생하고 있고,**Sticky Session**을 활성화하면 일부 인스턴스에 부하가 집중될까 걱정됩니다. 이 문제를 해결하려면 어떻게 해야 합니까?
    
    ① ALB 대신 **사용자 정의 Load Balancer**를 EC2에서 직접 운영한다.
    
    ② **RDS**에 세션 데이터를 저장한다.
    
    ③ **ElastiCache**에 세션 데이터를 저장한다. ✅
    
    ④ 공유 **EBS 볼륨**에 세션 데이터를 저장한다.
    

---

1. 개발팀이 프로덕션 **Aurora 데이터베이스**의 데이터를 기반으로**읽기·쓰기 테스트**를 수행하고자 합니다. 프로덕션 데이터 접근이 필요한 상황에서 어떤 방법이 가장 적절합니까?
    
    ① **Aurora Read Replica**를 생성한다.
    
    ② **프로덕션 데이터베이스에서 직접 테스트**를 수행한다.
    
    ③ **DB Snapshot을 생성**하고 새로운 DB로 복원한다.
    
    ④ **Aurora Cloning** 기능을 사용한다. ✅
    

---

1. **Aurora 데이터베이스**의 **장기 백업**을 보관하여**재해 복구(DR)** 및 **감사(audit)** 목적에 사용하려고 합니다.
가장 적절한 방법은 무엇입니까?
    
    ① **Automated Backups**을 활성화한다.
    
    ② **On-Demand Backups**을 수행한다. ✅
    
    ③ **Aurora Database Cloning**을 사용한다.
    

---

1. 다음 중 **SQL 연결 문자열을 변경하지 않고도 사용할 수 있는RDS 기능**(Aurora 제외)은 무엇입니까?
    
    ① **Multi-AZ** ✅
    
    ② **Read Replicas** ❌
    
    > Multi-AZ는 장애 조치 시에도 동일한 엔드포인트를 유지하므로
    > 
    > 
    > SQL 연결 문자열을 바꿀 필요가 없음
    > 

---

1. **RDS PostgreSQL** 데이터베이스의 **재해 복구 전략(DR)**을 구성하려고 합니다. 한 리전에 장애가 발생하더라도 다른 리전에서 읽기 및 쓰기 작업이 가능한**고가용성 데이터베이스**를 확보해야 합니다. 이 경우 어떤 구성을 권장합니까?
    
    ① 동일 리전에 **Read Replica**를 생성하고, 메인 DB에 **Multi-AZ**를 활성화한다. ❌
    
    ② **다른 리전에 Read Replica**를 생성하고, 그 복제본에 **Multi-AZ**를 활성화한다. ✅
    
    ③ 동일 리전에 **Read Replica**를 생성하고, 그 복제본에 **Multi-AZ**를 활성화한다.
    
    ④ 메인 데이터베이스에서 **Multi-Region 옵션**을 활성화한다.
    
    > **크로스 리전(Read Replica in another region)** 을 통해 다른 리전에 복제본
    해당 복제본에도 **Multi-AZ**를 활성화하면 
    해당 리전 내에서도 장애 발생 시 자동 Failover가 가능
    > 

---

1. 새 솔루션 설계 시 **MySQL 데이터베이스**가**AZ 장애에도 가용성을 유지**해야 합니다.
이 경우 어떤 구성을 사용해야 합니까?
    
    ① **Read Replicas** 생성
    
    ② **Encryption** 활성화
    
    ③ **Multi-AZ** 활성화 ✅
    

---

1. **분석 애플리케이션**이 현재 **프로덕션 RDS 데이터베이스**에 직접 쿼리를 수행합니다.
이로 인해 DB 부하가 높아져 사용자 경험이 저하되고 있습니다.
사용자 경험을 개선하려면 어떻게 해야 합니까?
    
    ① **Read Replica**를 설정한다. ✅
    
    ② **Multi-AZ**를 설정한다. ❌
    
    ③ 분석 쿼리를 **야간에만 실행**한다.
    
    > Read Replica는 원본 DB로부터 데이터를 **비동기 복제**하여, 
    읽기 전용 쿼리를 **별도의 인스턴스에서 실행**
    > 

---

1. AWS에서 **Oracle Database**를 완전히 커스터마이징할 수 있으면서
AWS 서비스의 이점을 함께 누리고 싶습니다.
이 경우 어떤 서비스를 사용해야 합니까?
    
    ① **RDS for Oracle** ❌
    
    ② **RDS Custom for Oracle** ✅
    
    ③ **Oracle on EC2**
    
    > **AWS 관리형 서비스의 편의성과 EC2 수준의 커스터마이징 자유도**를 모두 제공
    RDS for Oracle ⇒ 커스터마이징 자유도는 거의 없음
    > 

---

1. 암호화되지 않은 **RDS DB 인스턴스**를 암호화하려면 어떻게 해야 합니까?
    
    ① AWS Console에서 바로 "Encrypt using KMS" 옵션을 선택한다. ❌
    
    ② RDS 인스턴스를 정지시킨 후 Console에서 암호화한다.
    
    ③ **스냅샷을 생성한 뒤, 복사 시 "Enable encryption"을 체크**하고 암호화된 스냅샷으로부터 복원한다. ✅
    
    > 콘솔에서 “Encrypt using KMS” 같은 옵션으로 바로 암호화하는 기능은 제공되지 않음
    이미 실행 중인 **비암호화 RDS 인스턴스는 직접 암호화로 전환할 수 없음**
    > 

---

1. **Amazon Aurora**는 다음 두 가지 데이터베이스 엔진을 지원합니다:
    
    ① **MySQL** 및 **MariaDB**
    
    ② **MySQL** 및 **PostgreSQL** ✅
    
    ③ **Oracle** 및 **MariaDB**
    
    ④ **Oracle** 및 **MS SQL Server**
    

---

1. 게임 회사의 **Solutions Architect**로 근무 중입니다. 게임에서 플레이어의 점수를 **실시간으로 순위화**해야 하는 요구사항이 있습니다. 가용성이 높고 효율적인 솔루션으로 **리더보드(leaderboard)**를 구현하려면 무엇을 사용해야 합니까?
    
    ① **RDS for MySQL**
    
    ② **Amazon Aurora**
    
    ③ **ElastiCache for Memcached**
    
    ④ **ElastiCache for Redis – Sorted Sets** ✅
    

---

1. **RDS 데이터베이스**에 **Read Replica**를 설정했지만,
사용자들이 게시글을 수정한 후 바로 업데이트된 내용을 확인하지 못하고 있습니다.
이 현상의 가능한 원인은 무엇입니까?
    
    ① 애플리케이션에 버그가 있다.
    
    ② **Read Replica는 비동기 복제**를 사용하므로, **일관성이 지연(최종적 일관성)** 될 수 있다. ✅
    
    ③ **Multi-AZ** 구성을 사용했어야 한다.
    

---

1. 주 리전에 장애가 발생했을 때, 다른 AWS 리전에서 즉시 사용할 수 있는 **데이터베이스 복제본**을 확보하려고 합니다. 이 경우 구현이 가장 쉬운 데이터베이스는 무엇입니까?
    
    ① **RDS Read Replicas**
    
    ② **RDS Multi-AZ**
    
    ③ **Aurora Read Replicas** ❌
    
    ④ **Aurora Global Database** ✅
    
    > Aurora Global Database는 리전 간 실시간 복제 및 빠른 승격 기능을 통해
    > 
    > 
    > “재해 복구 + 고가용성”을 가장 쉽게 구현할 수 있음
    > 

---

1. **ElastiCache for Redis Cluster**의 보안을 강화하고,
사용자가 **IAM Identity(예: User, Role)** 를 사용하여 접근할 수 있도록 하려면
어떤 방법을 사용해야 합니까?
    
    ① **Redis Authentication** 사용
    
    ② **IAM Authentication** 사용 ✅
    
    ③ **Security Groups** 사용
    

---