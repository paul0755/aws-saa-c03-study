# 🧠 AWS 로드밸런서 & 오토스케일링 핵심 개념 정리

---

## 🔹 Elastic Load Balancer (ELB)

### 종류
- **Application Load Balancer (ALB)**  
  - HTTP, HTTPS, WebSocket 지원  
  - **7계층 (L7)** 로드 밸런서  
  - 요청 기반 라우팅 가능 (호스트/경로 기반)
  - Target Group에 EC2, IP, Lambda 등록 가능  

- **Network Load Balancer (NLB)**  
  - TCP, UDP, TLS 지원  
  - **4계층 (L4)** 로드 밸런서  
  - 초고속·저지연 처리에 적합  
  - **정적 IP 또는 Elastic IP** 할당 가능  

- **Classic Load Balancer (CLB)**  
  - 구형, ALB와 NLB의 이전 세대  
  - HTTP/HTTPS/TCP 지원  
  - 새 프로젝트에서는 사용 권장 X  

---

## 🔹 주요 기능 및 개념

### ✅ Cross-Zone Load Balancing  
- 모든 가용 영역(AZ)의 인스턴스에 트래픽을 균등하게 분산  
- 활성화하지 않으면 AZ 단위로 균등 분배됨 (AZ 내 인스턴스 수는 고려 X)

### ✅ Sticky Session (세션 고정)
- 동일한 사용자가 항상 같은 인스턴스로 라우팅되게 함  
- 로그인 세션, 장바구니 유지 등에 필요  
- **ALB 쿠키 기반 세션** (`APPUSERC` 같은 커스텀 쿠키 이름 사용 가능)  

### ✅ Health Check  
- 인스턴스 상태를 주기적으로 확인  
- 비정상 인스턴스는 자동으로 트래픽 라우팅에서 제외  

### ✅ SSL/TLS Termination  
- HTTPS 트래픽을 로드밸런서에서 복호화(Decryption) 처리  
- 이후 백엔드에는 HTTP로 전달 가능 (성능 효율 ↑)  

### ✅ SNI (Server Name Indication)
- 하나의 리스너에 여러 SSL 인증서 적용 가능  
- 다중 도메인 HTTPS 지원 (`api.example.com`, `users.example.com` 등)

### ✅ HTTP → HTTPS Redirect
- ALB 리스너 규칙(Rules)을 이용해 HTTP 트래픽을 HTTPS로 자동 리디렉션  

### ✅ X-Forwarded-For
- ALB 뒤의 서버가 실제 클라이언트 IP를 확인할 수 있게 해주는 HTTP 헤더  
- `X-Forwarded-For`, `X-Forwarded-Port`, `X-Forwarded-Proto` 존재  

---

## 🔹 Auto Scaling Group (ASG)

### ✅ 기본 개념
- EC2 인스턴스를 자동으로 **증가(Scale Out)** / **감소(Scale In)**  
- **Desired Capacity**, **Min**, **Max** 크기로 동작  

### ✅ 확장(Scalability) 유형
- **수평 확장(Horizontal)** : 인스턴스 개수를 늘리거나 줄이는 방식  
- **수직 확장(Vertical)** : 인스턴스의 스펙(CPU, 메모리 등)을 업그레이드  

### ✅ Scaling Policy 유형
- **Simple Scaling** : 하나의 CloudWatch 알람에 단순 증감 설정  
- **Step Scaling** : 임계값 구간별로 단계적 증감  
- **Target Tracking Scaling** : 지표(Target)를 일정 수준으로 유지 (예: 평균 CPU 60%)  
- **Scheduled Scaling** : 시간 기반으로 인스턴스 수 조절  

---

## 🔹 CloudWatch & Metrics

- **CloudWatch Metric** : 지표 (예: CPUUtilization, RequestCount 등)
- **Custom Metric** : 사용자가 직접 생성하는 지표 (예: DB 요청 수)
- **CloudWatch Alarm** : 특정 Metric 기준에 따라 ASG 조정 트리거  

---

## 🔹 기타 개념

### ✅ DNS vs IP
- ALB는 **고정 DNS 이름**만 제공 (`my-alb-1234.elb.amazonaws.com`)
- NLB는 **고정 IP (Elastic IP)** 제공 가능  

### ✅ 로드밸런서별 지원 프로토콜
| 로드밸런서 | 지원 계층 | 지원 프로토콜 |
|-------------|------------|----------------|
| ALB | L7 | HTTP, HTTPS, WebSocket |
| NLB | L4 | TCP, UDP, TLS |
| CLB | L4/L7 | TCP, HTTP, HTTPS |

### ✅ Target Group에 등록 가능한 대상
- EC2 인스턴스  
- IP 주소 (Private IP)  
- Lambda 함수  
❌ Network Load Balancer는 Target Group 대상이 될 수 없음  

---

## 🔹 ALB 트래픽 라우팅 조건

| 조건 | 설명 |
|------|------|
| Host-based routing | 도메인 이름 기반 (`api.example.com`) |
| Path-based routing | URL 경로 기반 (`/users`, `/checkout`) |
| Query string / Header routing | HTTP 헤더나 파라미터 기반 |
| ❌ Client location-based routing | ALB는 지원하지 않음 (Route 53 사용 필요) |

---

## 🔹 Health Check와 Auto Scaling 연동
- ASG가 **ALB의 Health Check 결과**를 모니터링  
- 인스턴스가 **Unhealthy**로 표시되면 ASG가 자동으로 **Terminate → 새 인스턴스 생성**

---

## 🔹 요약 키포인트
- ALB → 애플리케이션 계층, HTTP/HTTPS 라우팅 중심  
- NLB → 네트워크 계층, 초고속·정적 IP 지원  
- Sticky Session → 로그인 유지, 세션 일관성  
- SNI → 여러 인증서 한 리스너에 적용  
- Cross-Zone LB → AZ 간 균등 트래픽 분산  
- Target Tracking Policy → 평균 지표 유지 자동 스케일링  
- `X-Forwarded-For` → 실제 클라이언트 IP 확인  

---
