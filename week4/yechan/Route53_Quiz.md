### 🧭 1️⃣ Routing Policy — **Latency 기반**

**문제**

> You have an application that's hosted in two different AWS Regions `us-west-1` and `eu-west-2`.  
> You want your users to get the best possible user experience by minimizing the response time.  
> Which Route 53 Routing Policy should you choose?

**선택지**

1. Multi Value
2. Weighted
3. **Latency** ✅
4. Geolocation

**📘 개념 메모**

- **Latency-based Routing** :  
  사용자의 요청을 **가장 지연 시간이 짧은 리전으로 라우팅**.  
  (사용자와 AWS 리전 간의 네트워크 지연을 측정해서 자동 선택)
- 주로 **멀티 리전 배포** 시 사용 (예: us-west-1, eu-west-2)

---

### 🌍 2️⃣ Routing Policy — **Geolocation 기반**

**문제**

> You have a legal requirement that people in any country but France should NOT be able to access your website.  
> Which Routing Policy helps you in achieving this?

**선택지**

1. Latency
2. Simple
3. Multi Value
4. **Geolocation** ✅

**📘 개념 메모**

- **Geolocation Routing** :  
  사용자의 **지리적 위치(국가, 대륙, IP 기반)** 에 따라 트래픽을 보냄
- 특정 지역 사용자만 접근 허용/차단 가능
- 💡 **법적 요구사항(국가 제한)** 에 자주 사용됨

---

### ⚖️ 3️⃣ Routing Policy — **Weighted (가중치 기반)**

**문제**

> You deployed a new Elastic Beanstalk environment and want to direct 5% of traffic there for testing.  
> Which Routing Policy allows this?

**선택지**

1. Simple
2. **Weighted** ✅
3. Latency
4. Failover

**📘 개념 메모**

- **Weighted Routing** :  
  여러 리소스에 **트래픽 비율을 지정** 가능 (예: 95% vs 5%)
- **테스트 배포 / 점진적 트래픽 전환(Blue-Green)** 시 사용

---

### 🌐 4️⃣ Domain Registrar vs DNS Service

**문제**

> You have purchased a domain on GoDaddy and want to use Route 53 as the DNS Service Provider.  
> What should you do?

**선택지**

1. Request a domain transfer
2. Create a Private Hosted Zone and update 3rd party Registrar NS records
3. Create a Public Hosted Zone and update Route 53 NS records
4. **Create a Public Hosted Zone and update the 3rd party Registrar NS records** ✅

**📘 개념 메모**

- **Registrar**: 도메인 “소유/등록” 관리 (GoDaddy 등)
- **DNS Service**: 실제 트래픽 “해석” 담당 (Route 53 등)
- 💡 도메인 소유는 그대로 두고, **네임서버(NS)** 를 Route 53으로 교체하면 됨.

---

### 🕒 5️⃣ CNAME vs Alias — **TTL 문제**

**문제**

> You updated a Route 53 Record's value to a new ELB,  
> but users are still being directed to the old one. Why?

**선택지**

1. Because of the Alias record
2. Because of the CNAME record
3. **Because of the TTL** ✅
4. Because of Route 53 Health Checks

**📘 개념 메모**

- **TTL (Time To Live)** : DNS 레코드가 캐시되는 시간
- 변경 후에도 TTL 동안은 **기존 IP 주소**가 사용될 수 있음
- ⚠️ 테스트 시 TTL을 짧게(예: 60초) 설정하면 빠르게 반영됨

---

### 🔁 6️⃣ CNAME vs Alias — **AWS 리소스 연결**

**문제**

> You purchased `mycoolcompany.com` on Route 53 and want it to point to your ELB (`my-elb-1234.us-west-2.elb.amazonaws.com`).  
> Which record type must you use?

**선택지**

1. CNAME
2. **Alias** ✅

**📘 개념 메모**
| 구분 | 설명 | 예시 |
|------|------|------|
| **CNAME** | 한 도메인을 **다른 호스트 이름으로** 연결 | app.mydomain.com → blog.other.com |
| **Alias** | 도메인을 **AWS 리소스(ELB, S3, CF 등)** 으로 직접 연결 | app.mydomain.com → my-elb.amazonaws.com |

- Alias는 **루트 도메인(@)** 에도 설정 가능 (CNAME은 불가능)

---

### ❤️‍🔥 7️⃣ Route 53 Health Check

**문제**

> Which of the following are NOT valid Route 53 Health Checks?

**선택지**

1. **Health Check that monitor SQS Queue** ✅
2. Health Check that monitors an Endpoint
3. Health Check that monitors other Health Checks
4. Health Check that monitors CloudWatch Alarms

**📘 개념 메모**

- Health Check는 주로 **Endpoint(URL/IP)** 상태를 모니터링함
- SQS Queue는 **모니터링 대상이 아님**
- Route 53 Health Check 유형:
  - Endpoint (HTTP, HTTPS, TCP)
  - CloudWatch Alarm 연동
  - 다른 Health Check 조합 (복합 조건)
