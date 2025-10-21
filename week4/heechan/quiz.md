## 7. Route 53

**질문 1:**

애플리케이션이 두 개의 AWS 리전(us-west-1, eu-west-2)에 호스팅되어 있습니다. 사용자들이 애플리케이션 서버로부터의 응답 시간을 최소화하여 최상의 사용자 경험을 얻도록 하고 싶습니다. 어떤 Route 53 라우팅 정책(Route 53 Routing Policy)을 선택해야 하나요?

* 멀티 값 (Multi Value)
* 가중치 기반 (Weighted)
* 지연 시간 기반 (Latency) ✅
* 지리 위치 기반 (Geolocation)

---

**질문 2:**

Route 53 레코드 `myapp.mydomain.com`의 값을 새로운 Elastic Load Balancer로 업데이트했는데, 여전히 사용자가 이전 ELB로 리디렉션되는 것처럼 보입니다. 이런 동작의 가능한 원인은 무엇일까요?

* 앨리어스 레코드( Alias record ) 때문
* CNAME 레코드(CNAME record) 때문
* TTL 때문 ✅
* Route 53 상태 확인(Health Checks) 때문

---

**질문 3:**

GoDaddy에서 도메인을 구매했고, Route 53을 DNS 서비스 제공자로 사용하고자 합니다. 이를 위해 무엇을 해야 하나요?

* 도메인 이전(domain transfer) 요청
* 프라이빗 호스티드 존(Private Hosted Zone)을 만들고, 제3자 레지스트라의 NS 레코드를 업데이트
* 퍼블릭 호스티드 존(Public Hosted Zone)을 만들고, Route 53의 NS 레코드를 업데이트
* 퍼블릭 호스티드 존(Public Hosted Zone)을 만들고, 제3자 레지스트라의 NS 레코드를 업데이트 ✅

---

**질문 4:**

새로운 Elastic Beanstalk 환경을 배포했으며, 프로덕션 트래픽의 5%만 이 새로운 환경으로 보내고 싶습니다. 이렇게 하면 CloudWatch 지표를 모니터링하고 새 환경에 버그가 없는지 확인할 수 있습니다. 이를 가능하게 하는 Route 53 라우팅 정책은 무엇인가요?

* 단순(Simple)
* 가중치 기반(Weighted) ✅
* 지연 시간 기반(Latency)
* 장애 조치(Failover)

---

**질문 5:**

다음 중 **유효하지 않은** Route 53 상태 확인(Health Check)은 무엇인가요?

* SQS 큐(SQS Queue)를 모니터링하는 상태 확인 ✅
* 엔드포인트(Endpoint)를 모니터링하는 상태 확인
* 다른 상태 확인을 모니터링하는 상태 확인
* CloudWatch 알람을 모니터링하는 상태 확인

---

**질문 6:**

법적 요구 사항으로 인해, 프랑스를 **제외한** 어떤 국가의 사람들도 귀사의 웹사이트에 접근할 수 없도록 해야 합니다. 이를 달성하는 데 도움이 되는 Route 53 라우팅 정책은 무엇인가요?

* 지연 시간 기반(Latency)
* 단순(Simple)
* 멀티 값(Multi Value)
* 지리 위치 기반(Geolocation) ✅

---

**질문 7:**

Amazon Route 53 레지스트라에서 `mycoolcompany.com` 도메인을 구매했으며, 이 도메인이 Elastic Load Balancer `my-elb-1234567890.us-west-2.elb.amazonaws.com`을 가리키도록 하고 싶습니다. 이때 사용해야 하는 Route 53 레코드 타입은 무엇인가요?

* CNAME
* 앨리어스(Alias) ✅


---


<br>

## 23. VPC 


**질문 1:**

CIDR `10.0.4.0/28`은 무엇에 해당하나요?

* 10.0.4.0 ~ 10.0.4.15 ✅
* 10.0.4.0 ~ 10.0.32.0
* 10.0.4.0 ~ 10.0.4.28
* 10.0.0.0 ~ 10.0.16.0

---

**질문 2:**

VPC 엔드포인트를 사용할 때, **Gateway Endpoint**가 제공되는 AWS 서비스는 어떤 두 가지뿐인가요?

* Amazon S3 & Amazon SQS
* Amazon SQS & DynamoDB
* Amazon S3 & DynamoDB ✅

---

**질문 3:**

서브넷을 만들려 합니다. 최소 **EC2 인스턴스 28개**를 수용하려면, 서브넷의 최소 크기는 무엇이어야 하나요?

* /28
* /27
* /26 ✅
* /25

---

**질문 4:**

듀얼 스택 모드(IPv4+IPv6)로 실행 중인 VPC에서 EC2 인스턴스 시작이 계속 실패합니다. 조사해 보니 **IPv4 주소가 더 이상 남아 있지 않음**을 발견했습니다. 무엇을 해야 하나요?

* VPC를 IPv6 전용 모드로 변경
* VPC를 IPv4 전용 모드로 변경
* VPC에 추가 IPv4 CIDR을 할당 ✅

---

**질문 5:**

온프레미스와 AWS 클라우드 간 **Site-to-Site VPN**의 처리량을, 단일 IPsec 터널의 최대치(1.25 Gbps)를 넘어 확장하고 싶습니다. 무엇을 사용해야 하나요?

* 두 개의 Virtual Private Gateway 사용
* Direct Connect Gateway 사용
* Transit Gateway 사용 ✅

---

**질문 6:**

VPC에 Internet Gateway를 연결했지만, EC2 인스턴스가 여전히 인터넷에 접근하지 못합니다. **가능한 문제가 아닌 것**은 무엇인가요?

* 라우트 테이블에 항목이 없음
* EC2 인스턴스에 퍼블릭 IP가 없음 
* 보안 그룹이 인바운드 트래픽을 허용하지 않음✅
* NACL이 아웃바운드 트래픽을 허용하지 않음

---

**질문 7:**

보안 그룹(Security Group)은 ................. 수준에서 동작하고, NACL(Network ACL)은 ................. 수준에서 동작합니다.

* EC2 인스턴스, 서브넷 ✅
* 서브넷, EC2 인스턴스

---

**질문 8:**

VPC A, B, C가 있습니다. 세 VPC 사이에 **상호 VPC 피어링**을 구성하고자 합니다. 무엇을 해야 하나요?

* VPC 피어링이 **전이(Transitive) 피어링**을 지원하므로, 2개 연결(A-B, B-C)만 만들면 된다
* 3개의 피어링 연결(A-B, A-C, B-C)을 만든다 ✅

---

**질문 9:**

VPC A와 VPC B 사이에 VPC 피어링을 활성화했고, VPC A의 라우트 테이블을 업데이트했습니다. 그러나 EC2 인스턴스 간 통신이 되지 않습니다. 가능성이 높은 문제는 무엇인가요?

* NACL을 확인
* **VPC B의 라우트 테이블**을 확인 ✅
* EC2 인스턴스에 연결된 보안 그룹을 확인
* DNS 해석(Resolution)이 활성화되었는지 확인

---

**질문 10:**

웹 앱 백엔드는 **프라이빗 서브넷**의 EC2 인스턴스에서 호스팅되고, **퍼블릭 서브넷**의 Application Load Balancer(ALB)가 앞단에 있습니다. 일부 개발자에게 백엔드 EC2에 접근 권한을 주되 인터넷에 노출되지는 않게 하려 합니다. 퍼블릭 서브넷에 배스천 호스트를 만들고, 백엔드 EC2 보안 그룹에 배스천 호스트에서 오는 트래픽을 허용했습니다. 보안을 위해 배스천 호스트 **보안 그룹**을 어떻게 설정하는 것이 가장 좋은가요?

* 회사 **퍼블릭 CIDR**에서 들어오는 **80번 포트**만 허용
* 회사 **퍼블릭 CIDR**에서 들어오는 **22번 포트**만 허용 ✅
* 회사 **프라이빗 CIDR**에서 들어오는 **22번 포트**만 허용
* 회사 **프라이빗 CIDR**에서 들어오는 **80번 포트**만 허용

---

**질문 11:**

VPC 내부의 IP 트래픽 정보를 수집하려면 어떻게 해야 하나요?

* **VPC Flow Logs** 활성화 ✅
* VPC Traffic Mirroring 활성화
* CloudWatch Traffic Logs 활성화

---

**질문 12:**

VPC 내 트래픽을 **3~7계층**에서 보호하고 제어하도록 해주는 AWS 서비스는 무엇인가요?

* **AWS Network Firewall** ✅
* Amazon GuardDuty
* Amazon Inspector
* AWS Shield

---

**질문 13:**

미국 전역에 여러 온프레미스 사이트가 있고, 이를 사설 회선으로 연결해 왔지만 최근 불안정합니다. 장애 시 **공용 인터넷**을 통해 사이트들을 연결할 **백업 회선**을 만들고 싶습니다. 무엇을 권장하나요?

* VPC 피어링
* **AWS VPN CloudHub** ✅
* Direct Connect
* AWS PrivateLink

---

**질문 14:**

AWS는 VPC에서 새 서브넷을 만들 때마다 **IP 5개**를 예약합니다. CIDR `10.0.0.0/24`로 서브넷을 만들면, 다음 중 **예약되지 않는(=예외)** 주소는 무엇인가요?

* 10.0.0.1
* 10.0.0.2
* 10.0.0.3
* 10.0.0.4 ✅

---

**질문 15:**

사내 네트워크가 `10.0.0.0/8`, 위성 오피스가 `192.168.0.0/16`입니다. 나중에 이 네트워크들과 연결할 계획이라면, AWS VPC에 사용할 수 있는 **겹치지 않는 CIDR**은 무엇인가요?

* 172.16.0.0/12
* 172.16.0.0/16 ✅
* 10.0.16.0/16
* 192.168.4.0/18

---

**질문 16:**

회사 데이터센터와 **VPC A** 사이에 Direct Connect를 설정했습니다. **다른 리전**의 **VPC B**에도 데이터센터에서 접근해야 합니다. 무엇을 해야 하나요?

* VPC 피어링 활성화
* Customer Gateway 사용
* **Direct Connect Gateway 사용** ✅
* NAT Gateway 설정

---

질문 17:

데이터센터와 AWS 간 500 Mbps Direct Connect 연결이 필요합니다. 어떤 유형을 선택하나요?

전용(Dedicated)

호스티드(Hosted) ✅

---

질문 18:

회사에서 데이터센터와 AWS 간 Direct Connect를 설정했습니다. 비용 효율적이며 보안적인 백업 연결이 필요합니다(Direct Connect 장애 대비). 무엇을 권장하나요?

같은 리전에 Direct Connect를 하나 더 설정

다른 리전에 Direct Connect를 하나 더 설정

Site-to-Site VPN을 백업으로 구성✅

---

질문 19:

온프레미스 데이터센터와 AWS 클라우드 사이에 전용, 일관적이며 인터넷을 통과하지 않는 사설 연결이 필요합니다. 어떤 서비스를 사용해야 하나요?

Site-to-Site VPN

AWS PrivateLink

AWS Direct Connect ✅

Amazon EventBridge

---

질문 20:

오토 스케일링 그룹의 EC2 인스턴스들 위에 ALB로 노출되는 웹 앱이 있습니다. 둘 다 192.168.0.0/18 CIDR의 VPC에 있습니다. EC2 보안 그룹을 어떻게 설정해야 ALB만 포트 80으로 접근 가능하게 할 수 있나요?

인바운드 규칙에 포트 80, 소스 0.0.0.0/0 추가

인바운드 규칙에 포트 80, 소스 192.168.0.0/18 추가

인바운드 규칙에 포트 80, 소스에 ALB의 보안 그룹 지정 ✅

ALB에 SSL 인증서를 로드


---

질문 21:

Direct Connect 연결을 통해 공용과 사설 AWS 리소스 모두에 접근할 수 있다.

참(True) ✅

거짓(False)

---


질문 22:

온프레미스 데이터센터와 AWS VPC 사이에 Site-to-Site VPN을 설정할 때 구성해야 하는 두 가지 주요 구성요소는 무엇인가요?

Customer Gateway와 NAT Gateway

Internet Gateway와 Customer Gateway

Virtual Private Gateway와 Internet Gateway

Virtual Private Gateway와 Customer Gateway ✅
 

---

질문 23:

프라이빗 서브넷의 EC2 인스턴스(IPv4)에 인터넷 액세스를 제공하면서, 운영 부담이 가장 적고 자동으로 확장되는 해법이 필요합니다. 무엇을 사용해야 하나요?

Source/Destination Check를 끈 NAT 인스턴스

Egress Only Internet Gateway

NAT Gateway ✅