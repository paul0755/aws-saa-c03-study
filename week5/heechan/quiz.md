## 1. Scalability & High Availability


**질문 1:**

Elastic Load Balancer(ELB)가 앞단에 있고 여러 대의 EC2 인스턴스에 애플리케이션을 호스팅했습니다. 일주일쯤 지나 사용자들이 가끔 애플리케이션이 동작하지 않는다고 불평합니다. 조사해 보니 일부 EC2 인스턴스가 때때로 크래시합니다. 크래시되는 인스턴스에 사용자가 연결되지 않도록 보호하려면 무엇을 해야 하나요?

* ELB 상태 검사(Health Checks) 활성화 ✅
* ELB 스티키 세션(Stickiness) 활성화
* SSL 종료(Termination) 활성화
* 가용 영역 간 로드 밸런싱(Cross-Zone Load Balancing) 활성화

---

**질문 2:**

EC2 인스턴스를 r4.large에서 r4.4xlarge로 확장하는 것은 ..................... 라고 부릅니다.

* 수평 확장성(Horizontal Scalability)
* 수직 확장성(Vertical Scalability) ✅

---

**질문 3:**

Application Load Balancer 앞단에 Auto Scaling Group(ASG)이 있습니다. ASG가 ALB 상태 검사를 사용하도록 구성했고, 방금 한 EC2 인스턴스가 비정상(unhealthy)으로 보고되었습니다. 이 EC2 인스턴스에 대해 어떤 일이 일어나나요?

* ASG는 인스턴스를 계속 실행시키고 애플리케이션만 재시작한다
* ASG는 EC2 인스턴스를 분리(detach)하지만 계속 실행 상태로 둔다
* ASG는 EC2 인스턴스를 종료(terminate)한다 ✅

---

**질문 4:**

10대의 EC2 인스턴스에서 웹사이트를 운영하고 있고, 앞단에 ELB가 있습니다. 사용자는 페이지를 이동할 때마다 계속 다시 인증하라고 뜬다고 불평합니다. 로컬과 1대 인스턴스인 Dev 환경에서는 문제없이 잘 동작합니다. 가능한 이유는 무엇일까요?

* 여러 EC2 인스턴스에서 호스팅할 때 웹사이트 자체에 문제가 있다
* EC2 인스턴스가 사용자의 IP를 볼 수 없고 ELB의 IP만 받기 때문에 사용자를 로그아웃시킨다
* Elastic Load Balancer에 스티키 세션(Sticky Sessions)이 활성화되어 있지 않다 ✅

---

**질문 5:**

us-east-1 리전에 있는 여러 EC2 인스턴스에 트래픽을 분산하는 Network Load Balancer가 있습니다. us-east-1b AZ에 2대, us-east-1e AZ에 5대의 EC2 인스턴스가 있습니다. 트래픽은 두 AZ에 동일하게 분산되고 있는데, us-east-1b의 인스턴스들에서 CPU 사용률이 더 높습니다. 이 문제를 어떻게 해결하겠습니까?

* 가용 영역 간 로드 밸런싱(Cross-Zone Load Balancing) 활성화 ✅
* 스티키 세션(Sticky Sessions) 활성화
* ELB 상태 검사(Health Checks) 활성화
* SSL 종료(Termination) 활성화

---

**질문 6:**

Application Load Balancer가 지원하는 프로토콜은 다음과 같지만, 다음 중 하나는 **예외**입니다(지원하지 않음):

* HTTP
* HTTPS
* TCP ✅
* WebSocket 

---

**질문 7:**

컴플라이언스 때문에 최종 사용자에게 고정(static) 공인 IP를 노출하여 방화벽 규칙을 안정적으로 승인받고자 합니다. 어떤 유형의 Elastic Load Balancer를 선택하겠습니까?

* Elastic IP를 연결한 Application Load Balancer 
* Network Load Balancer ✅
* Classic Load Balancer

---

**질문 8:**

Application Load Balancer가 호스트명에 따라 3개의 대상 그룹으로 트래픽을 라우팅하도록 구성되어 있습니다: users.example.com, api.external.example.com, checkout.example.com. 이 각각의 호스트명에 대해 HTTPS를 구성하려고 합니다. 이를 위해 ALB를 어떻게 설정해야 하나요?

* HTTP → HTTPS 리다이렉트 규칙 사용
* 보안 그룹의 SSL 인증서 사용 
* 서버 이름 표시(SNI, Server Name Indication) 사용 ✅

---

**질문 9:**

Application Load Balancer의 대상 그룹(Target Group)에 등록될 수 있는 대상은 다음과 같지만, 다음 중 하나는 **예외**입니다:

* EC2 인스턴스 
* Network Load Balancer ✅
* 프라이빗 IP 주소
* Lambda 함수

---

**질문 10:**

Application Load Balancer를 사용해 EC2 인스턴스에 호스팅된 웹사이트로 트래픽을 분산하고 있습니다. 그런데 웹사이트에서는 들어오는 트래픽의 IP가 모두 사설 IPv4 주소로 보이며, 이는 실제로 ALB의 IP들입니다. 접속한 클라이언트의 실제 IP 주소를 얻으려면 어떻게 해야 하나요?

* 프런트엔드를 수정하여 사용자가 매 요청마다 자신의 IP를 보내도록 한다
* 백엔드를 수정하여 `X-Forwarded-For` 헤더에서 클라이언트 IP를 가져온다 ✅
* 백엔드를 수정하여 `X-Forwarded-Port` 헤더에서 클라이언트 IP를 가져온다
* 백엔드를 수정하여 `X-Forwarded-Proto` 헤더에서 클라이언트 IP를 가져온다

---

**질문 11:**

Application Load Balancer와 Network Load Balancer 모두에서 하나의 리스너에 여러 SSL 인증서를 로드할 수 있게 해주는 기능은 무엇인가요?

* TLS 종료(Termination) 
* 서버 이름 표시(SNI) ✅
* SSL 보안 정책(SSL Security Policies)
* 호스트 헤더(Host Headers)

---

**질문 12:**

오토 스케일링 그룹에서 EC2 인스턴스 수를 늘렸다 줄였다 하며 애플리케이션을 실행하는 것은 ..................... 라고 부릅니다.

* 수평 확장성(Horizontal Scalability) ✅
* 수직 확장성(Vertical Scalability)

---

**질문 13:**

오토 스케일링 그룹에서 EC2 인스턴스 3대를 원하는 용량(desired)과 최대 용량(maximum) 모두 3으로 설정했습니다. 또한 CPU 사용률이 60%에 도달하면 ASG가 확장되도록 CloudWatch 알람을 만들었습니다. 갑자기 트래픽이 급증하여 현재 CPU 사용률이 80%입니다. 어떤 일이 일어날까요?

* 아무 일도 일어나지 않는다 ✅
* 원하는 용량은 4로 올라가고 최대 용량은 3으로 유지된다
* 원하는 용량은 4로, 최대 용량도 4로 올라간다

---

**질문 14:**

Application Load Balancer와 오토 스케일링 그룹으로 애플리케이션이 배포되어 있습니다. 현재는 수동으로 ASG를 조절하고 있는데, EC2 인스턴스당 평균 연결 수가 약 1000이 되도록 유지하는 스케일링 정책을 정의하고 싶습니다. 어떤 스케일링 정책을 사용해야 하나요?

* 단순(Simple) 스케일링 정책
* 단계(Step) 스케일링 정책
* 타깃 추적(Target Tracking) 정책 ✅
* 예약(Scheduled) 스케일링 정책

---

**질문 15:**

ASG와 Network Load Balancer가 있습니다. ASG의 애플리케이션은 HTTP 프로토콜을 지원하며 로드 밸런서 상태 검사와 연동되어 있습니다. 현재 TCP 상태 검사를 사용 중인데, HTTP 상태 검사로 마이그레이션하고 싶습니다. 어떻게 하시겠습니까?

* Application Load Balancer로 마이그레이션한다 
* 상태 검사를 HTTP로 마이그레이션한다 ✅

---

**질문 16:**

Application Load Balancer에서 사용자 정의 애플리케이션 기반 쿠키를 만들고자 합니다. 다음 중 쿠키 이름으로 사용할 수 있는 것은 무엇인가요?

* `AWSALBAPP`
* `APPUSERC` ✅
* `AWSALBTG`
* `AWSALB`

---

**질문 17:**

Application Load Balancer는 다음 기준에 따라 서로 다른 대상 그룹으로 트래픽을 라우팅할 수 있습니다. 다음 중 하나는 **예외**입니다:

* 클라이언트의 위치(지리적 위치) ✅
* 호스트명(Hostname)
* 요청 URL 경로(Path)
* 소스 IP 주소

---

**질문 18:**

EC2 인스턴스의 오토 스케일링 그룹 앞단에 Application Load Balancer가 있고, 현재 웹사이트는 HTTP로 서비스되고 있습니다. HTTPS로 사용하도록 구성하라는 업무를 받았습니다. ACM에 인증서를 생성하여 ALB에 연결했습니다. 사용자가 HTTP 대신 HTTPS로 접속하도록 강제하려면 무엇을 할 수 있나요?

* 모든 고객에게 HTTP 대신 HTTPS를 사용하라고 이메일을 보낸다
* Application Load Balancer에서 HTTP를 HTTPS로 리다이렉트하도록 구성한다 ✅
* DNS 레코드를 구성해 HTTP를 HTTPS로 리다이렉트한다

---

**질문 19:**

상사가 데이터베이스에 대한 애플리케이션의 분당 요청 수를 기준으로 오토 스케일링 그룹을 확장하라고 요청했습니다. 어떻게 해야 하나요?

* CloudWatch 사용자 정의 지표를 생성하고, 이 지표에 대한 CloudWatch 알람을 만들어 ASG를 스케일링한다 ✅
* 공손히 불가능하다고 말한다
* 상세 모니터링(Detailed Monitoring)을 활성화하고, 이를 기반으로 CloudWatch 알람을 만들어 ASG를 스케일링한다

---

**질문 20:**

수백만 RPS(초당 요청)를 처리해야 하는 고성능·저지연 애플리케이션 아키텍처를 설계해야 합니다. 어떤 유형의 Elastic Load Balancer를 선택하겠습니까?

* Application Load Balancer
* Classic Load Balancer
* Network Load Balancer ✅

---

**질문 21:**

Elastic Load Balancer가 제공하는 것은 ....................... 입니다.

* 애플리케이션에서 사용할 수 있는 고정 IPv4
* 애플리케이션에서 사용할 수 있는 고정 DNS 이름 ✅
* 애플리케이션에서 사용할 수 있는 고정 IPv6

---

## 2. RDS



**질문 1:**

암호화되지 않은(un-encrypted) RDS DB 인스턴스가 있고 Read Replica를 만들고 싶습니다. RDS Read Replica를 **암호화된** 상태로 구성할 수 있나요?

* 아니요 ✅
* 예 

---

**질문 2:**

프로덕션에서 실행 중인 애플리케이션이 데이터베이스로 Aurora 클러스터를 사용하고 있습니다. 개발팀은 축소된 규모로 애플리케이션을 한 버전 더 돌리되, 필요할 때만 무거운 작업을 수행하고자 합니다. 대부분의 시간에는 애플리케이션이 사용되지 않을 것입니다. CIO는 비용을 최소화하면서 이를 달성하도록 요청했습니다. 무엇을 제안하시겠습니까?

* Aurora Global Database 사용
* RDS 데이터베이스 사용
* Aurora Serverless 사용 ✅
* EC2 위에 Aurora를 올리고, 밤에는 EC2 인스턴스를 종료하는 스크립트를 작성 

---

**질문 3:**

RDS 데이터베이스에 Read Replica를 설정했지만, 사용자가 소셜 미디어 게시물을 업데이트한 직후 자신의 업데이트가 바로 보이지 않는다고 불평합니다. 가능한 원인은 무엇일까요?

* 애플리케이션에 버그가 있다
* Read Replica는 비동기 복제를 사용하므로, 사용자는 결국적 일관성(Eventual Consistency)만 보게 될 수 있다 ✅
* 대신 Multi-AZ를 설정했어야 한다

---

**질문 4:**

웹사이트 요청을 처리하기에 RDS 데이터베이스가 버겁습니다. 천만 단위의 사용자 대부분은 뉴스를 **읽기만** 하고, 뉴스 게시 빈도는 높지 않습니다. 이 문제에 **적합하지 않은** 솔루션은 무엇일까요?

* ElastiCache 클러스터
* RDS Multi-AZ ✅
* RDS Read Replica

---

**질문 5:**

암호화되지 않은 RDS DB 인스턴스를 어떻게 암호화하나요?

* AWS 콘솔에서 해당 RDS DB 인스턴스를 선택하고, Actions → KMS로 암호화(Encrypt)
* AWS 콘솔에서 DB 인스턴스를 중지한 뒤 바로 암호화
* 암호화되지 않은 DB 인스턴스의 스냅샷을 생성하고, 그 스냅샷을 **복사**하면서 “암호화 활성화”를 체크한 다음, 암호화된 스냅샷에서 DB 인스턴스를 복원 ✅

---

**질문 6:**

RDS 데이터베이스에 연결된 EC2 인스턴스가 100대 있습니다. 데이터베이스 유지보수 시 애플리케이션의 재연결 로직이 부실해 모든 앱이 RDS에 재연결하는 데 시간이 오래 걸립니다. 어떻게 개선하시겠습니까?

* 모든 애플리케이션을 고친다
* Multi-AZ를 비활성화한다
* Multi-AZ를 활성화한다
* RDS Proxy를 사용한다 ✅

---

**질문 7:**

분석용 애플리케이션이 현재 프로덕션 RDS 데이터베이스를 대상으로 쿼리를 수행하고 있습니다. 이 쿼리들은 하루 중 아무 때나 실행되어 RDS를 느리게 만들어 사용자 경험에 영향을 줍니다. 어떻게 개선하시겠습니까?

* Read Replica를 구성한다✅
* Multi-AZ를 구성한다 
* 분석 쿼리를 야간에만 실행한다

---

**질문 8:**

Amazon RDS가 지원하는 데이터베이스는 다음과 같지만, **다음 중 하나는 제외**입니다:

* MongoDB ✅
* MySQL
* MariaDB
* Microsoft SQL Server

---

**질문 9:**

개발팀이 프로덕션 Aurora 데이터베이스에 대해 읽기 및 쓰기 테스트를 수행하려 합니다. 가능한 한 빨리 프로덕션 데이터에 접근해야 한다고 합니다. 무엇을 권고하시겠습니까?

* 개발팀을 위해 Aurora Read Replica를 생성
* 프로덕션 데이터베이스에서 직접 테스트 수행
* DB 스냅샷을 생성하고 새 데이터베이스로 복원
* Aurora 클로닝 기능 사용 ✅

---

**질문 10:**

사용자가 IAM ID(예: 사용자, 역할)로 ElastiCache Redis 클러스터에 접근할 수 있도록 하여 보안을 강화하려면 어떻게 해야 하나요?

* Redis 인증(Requirepass 등) 사용
* IAM 인증 사용 ✅
* 보안 그룹 사용

---

**질문 11:**

게임 회사의 솔루션스 아키텍트로 일하고 있습니다. 게임의 요구사항은 플레이어 점수를 기준으로 실시간 랭킹을 만드는 것입니다. 고가용성과 효과적인 구현이 필요합니다. 무엇을 사용하시겠습니까?

* RDS for MySQL 사용
* Amazon Aurora 사용
* ElastiCache for Memcached 사용
* ElastiCache for Redis – Sorted Set 사용 ✅

---

**질문 12:**

하나의 Aurora DB 클러스터에서 가질 수 있는 Aurora Read Replica의 최대 수는 얼마인가요?

* 5
* 10
* 15 ✅

---

**질문 13:**

RDS PostgreSQL 데이터베이스에 대한 재해 복구 전략을 세우고자 합니다. 리전 장애 시 다른 AWS 리전에서 읽기/쓰기 워크로드를 빠르게 처리할 수 있어야 합니다. DR 데이터베이스는 고가용해야 합니다. 무엇을 추천하시겠습니까?

* 같은 리전에 Read Replica를 만들고, 메인 DB에는 Multi-AZ를 활성화 
* **다른 리전**에 Read Replica를 만들고, 그 Read Replica에 Multi-AZ를 활성화 ✅
* 같은 리전에 Read Replica를 만들고, 그 Read Replica에 Multi-AZ를 활성화
* 메인 데이터베이스에 Multi-Region 옵션을 활성화

---

**질문 14:**

RDS(Aurora 제외)의 기능 중 **SQL 연결 문자열을 변경할 필요가 없는** 것은 무엇인가요?

* Multi-AZ ✅
* Read Replica

---

**질문 15:**

온프레미스의 MySQL 데이터베이스를 RDS로 마이그레이션했습니다. 많은 애플리케이션과 개발자가 데이터베이스에 접근합니다. 각 개발자는 회사 AWS 계정에 IAM 사용자가 있습니다. 각 개발자마다 DB 계정을 따로 만들지 않고 RDS MySQL DB 인스턴스에 접근 권한을 주는 적절한 방법은 무엇인가요?

* 기본적으로 IAM 사용자는 RDS 데이터베이스에 접근할 수 있다
* Amazon Cognito 사용
* IAM Database Authentication 활성화 ✅

---

**질문 16:**

다음 중 **IAM Database Authentication**을 지원하지 않는 RDS 데이터베이스 기술은 무엇인가요?

* Oracle ✅
* PostgreSQL
* MySQL 

---

**질문 17:**

새 솔루션에서 MySQL 데이터베이스가 필요하며, 하나의 가용 영역에 장애가 발생해도 사용 가능해야 합니다. 무엇을 사용하시겠습니까?

* Read Replica 생성
* 암호화 활성화
* Multi-AZ 활성화 ✅

---

**질문 18:**

RDS 데이터베이스에서 Read Replica는 최대 ............ 개까지 가질 수 있습니다.

* 5
* 15 ✅
* 7

---

**질문 19:**

회사에는 프로덕션 Node.js 애플리케이션이 있고, 데이터베이스로 RDS MySQL 5.6을 사용합니다. 새 Java 애플리케이션이 매시간 정기적으로 대규모 분석 작업을 수행해 대시보드를 만들 예정입니다. 메인 애플리케이션에 대한 방해를 최소화하기 위한 가장 비용 효율적인 방안은 무엇인가요?

* RDS 데이터베이스에 Multi-AZ를 활성화하고, 스탠바이 DB에서 분석 작업 실행
* 다른 AZ에 Read Replica를 만들고, 그 Replica 데이터베이스에서 분석 작업 실행 ✅
* 다른 AZ에 Read Replica를 만들고, **소스** 데이터베이스에서 분석 작업 실행

---

**질문 20:**

애플리케이션은 Auto Scaling Group이 관리하는 EC2 플릿에서 실행되고, Application Load Balancer 뒤에 있습니다. 사용자가 자꾸 다시 로그인해야 합니다. ALB에서 스티키 세션을 활성화하면 일부 EC2 인스턴스에 과부하가 갈까 우려되어 사용하지 않으려 합니다. 무엇을 해야 합니까?

* ALB 대신 EC2 위에 직접 커스텀 로드 밸런서를 사용
* 세션 데이터를 RDS에 저장
* 세션 데이터를 ElastiCache에 저장 ✅
* 세션 데이터를 공유 EBS 볼륨에 저장

---

**질문 21:**

Amazon Aurora는 다음 **둘 다**를 지원합니다.

* MySQL과 MariaDB
* MySQL과 PostgreSQL ✅
* Oracle과 MariaDB
* Oracle과 MS SQL Server

---

**질문 22:**

주 리전에 재해가 발생했을 때 다른 AWS 리전에서도 데이터베이스 복제본을 사용할 수 있도록 하고 싶습니다. 이를 쉽게 구현하려면 어떤 데이터베이스를 추천하나요?

* RDS Read Replica
* RDS Multi-AZ
* Aurora Read Replica
* Aurora Global Database ✅

---

**질문 23:**

AWS에서 Oracle 데이터베이스를 완전히 커스터마이즈해서 사용하고 싶고, 동시에 AWS 서비스의 이점을 활용하고자 합니다. 무엇을 추천하시겠습니까?

* RDS for Oracle
* RDS Custom for Oracle  
* EC2에 Oracle 배포 

---

**질문 24:**

재해 복구 및 감사 목적을 위해 Aurora 데이터베이스의 장기 백업을 저장해야 합니다. 무엇을 추천하시겠습니까?

* 자동 백업(Automated Backups) 활성화
* 온디맨드 백업 수행 ✅
* Aurora 데이터베이스 클로닝 사용

---

**질문 25:**

RDS Read Replica와 Multi-AZ의 복제에 관한 다음 설명 중 **참**인 것은 무엇인가요?

* Read Replica는 비동기 복제, Multi-AZ는 비동기 복제
* Read Replica는 비동기 복제, Multi-AZ는 동기 복제 ✅
* Read Replica는 동기 복제, Multi-AZ는 동기 복제
* Read Replica는 동기 복제, Multi-AZ는 비동기 복제

