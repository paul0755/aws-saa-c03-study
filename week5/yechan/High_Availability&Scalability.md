## 1️⃣ 문제 1  
Application Load Balancer에서 사용자 정의 애플리케이션 기반 쿠키를 만들려고 합니다.  
다음 중 쿠키 이름으로 사용할 수 있는 것은 무엇입니까?  

- ① AWSALBAPP  
- ② APPUSERC  ⭕
- ③ AWSALBTG  
- ④ AWSALB  

---

## 2️⃣ 문제 2  
us-east-1 리전에서 Network Load Balancer가 여러 EC2 인스턴스로 트래픽을 분산하고 있습니다.  
us-east-1b AZ에는 2개의 인스턴스, us-east-1e AZ에는 5개의 인스턴스가 있습니다.  
트래픽은 두 AZ에 동일하게 분배되지만, us-east-1b의 인스턴스 CPU 사용률이 더 높습니다.  
이 문제를 어떻게 해결해야 합니까?  

- ① Cross-Zone Load Balancing 활성화  ⭕
- ② Sticky Sessions 활성화  // 2가지 요청을 수행하는 클라이언트가 요청에 응답하기 위해 백엔드에 동일한 인스턴스를 갖는것.
- ③ ELB Health Check 활성화  
- ④ SSL Termination 활성화  

---

## 3️⃣ 문제 3  
상사가 애플리케이션이 데이터베이스에 보내는 “분당 요청 수”를 기준으로 Auto Scaling Group을 확장하라고 합니다.  
어떻게 해야 합니까?  

- ① CloudWatch 사용자 정의 지표를 생성하고, 이 지표에 대한 알람으로 ASG를 확장한다  ⭕
- ② 불가능하다고 말한다  
- ③ 상세 모니터링(Detailed Monitoring)을 활성화하고 알람으로 ASG를 확장한다  

---

## 4️⃣ 문제 4  
Application Load Balancer와 Network Load Balancer 모두에서  
하나의 리스너에 여러 SSL 인증서를 설정할 수 있게 해주는 기능은 무엇입니까?  

- ① TLS 종료(TLS Termination)  
- ② SNI(Server Name Indication) ⭕  
- ③ SSL 보안 정책(SSL Security Policies)  
- ④ 호스트 헤더(Host Headers)  

---

## 5️⃣ 문제 5  
규제 준수를 위해 최종 사용자에게 고정된 IP 주소를 노출시켜 방화벽 규칙을 안정적으로 유지하고자 합니다.  
어떤 종류의 Elastic Load Balancer를 선택해야 합니까?  

- ① Elastic IP가 연결된 Application Load Balancer  
- ② Network Load Balancer  ⭕
- ③ Classic Load Balancer  

---

## 6️⃣ 문제 6  
Elastic Load Balancer 앞단의 EC2 인스턴스들에서 애플리케이션이 가끔 작동하지 않습니다.  
조사 결과, 일부 EC2 인스턴스가 주기적으로 다운되는 것을 발견했습니다.  
사용자가 다운된 인스턴스에 연결되지 않도록 하려면 어떻게 해야 합니까?  

- ① ELB Health Check 활성화  ⭕
- ② ELB Sticky Session 활성화  
- ③ SSL Termination 활성화  
- ④ Cross-Zone Load Balancing 활성화  

---

## 7️⃣ 문제 7  
Application Load Balancer가 지원하는 프로토콜이 아닌 것은 무엇입니까?  

- ① HTTP  
- ② HTTPS  
- ③ TCP  ⭕
- ④ WebSocket  

---

## 8️⃣ 문제 8  
초당 수백만 건의 요청을 처리해야 하는 고성능·저지연 애플리케이션을 설계하려고 합니다.  
어떤 유형의 Elastic Load Balancer를 선택해야 합니까?  

- ① Application Load Balancer  
- ② Classic Load Balancer  
- ③ Network Load Balancer  ⭕

---

## 9️⃣ 문제 9  
Auto Scaling Group이 EC2 인스턴스의 수를 자동으로 늘리고 줄이는 방식은 무엇이라고 부릅니까?  

- ① 수평 확장(Horizontal Scalability)  ⭕
- ② 수직 확장(Vertical Scalability)  

---

## 🔟 문제 10  
Application Load Balancer와 Auto Scaling Group을 사용하는 애플리케이션에서,  
평균 연결 수를 1000개로 유지하려면 어떤 Scaling Policy를 사용해야 합니까?  

- ① Simple Scaling Policy  
- ② Step Scaling Policy  
- ③ Target Tracking Policy  ⭕
- ④ Scheduled Scaling Policy  

---

## 1️⃣ 문제 11  
현재 HTTP로 서비스 중인 웹사이트를 HTTPS로 전환했습니다.  
ACM 인증서를 ALB에 연결한 후, 사용자가 HTTPS로만 접속하도록 강제하려면 어떻게 해야 합니까?  

- ① 고객에게 HTTPS 주소를 이메일로 공지한다  
- ② ALB에서 HTTP → HTTPS 리디렉션을 설정한다   ⭕
- ③ DNS 레코드에서 HTTP를 HTTPS로 리디렉션한다  

---


## 2️⃣ 문제 12  
Elastic Load Balancer는 애플리케이션에서 사용할 수 있는 어떤 종류의 주소를 제공합니다?  

- ① 고정 IPv4 주소  
- ② 고정 DNS 이름  ⭕
- ③ 고정 IPv6 주소  

---

## 3️⃣ 문제 13  
ASG와 Network Load Balancer를 사용 중입니다.  
현재 TCP Health Check를 사용 중인데, HTTP Health Check로 바꾸고 싶습니다.  
무엇을 해야 합니까?  

- ① Application Load Balancer로 마이그레이션한다  
- ② Health Check 방식을 HTTP로 변경한다  ⭕

---

## 4️⃣ 문제 14  
Application Load Balancer가 다음 세 호스트 이름에 따라 트래픽을 분기하고 있습니다:  
`users.example.com`, `api.external.example.com`, `checkout.example.com`  
각 호스트 이름에 대해 HTTPS를 설정하려면 어떻게 해야 합니까?  

- ① HTTP → HTTPS 리디렉션 규칙 사용  
- ② 보안 그룹 SSL 인증서 사용  
- ③ SNI(Server Name Indication) 사용   ⭕

---

## 5️⃣ 문제 15  
ALB 뒤의 EC2 인스턴스에서 웹사이트 트래픽을 분석하니,  
클라이언트 IP가 아닌 ALB의 사설 IP 주소만 보입니다.  
사용자의 실제 IP를 확인하려면 어떻게 해야 합니까?  

- ① 프런트엔드에서 사용자의 IP를 요청에 직접 포함시킨다  
- ② 백엔드에서 `X-Forwarded-For` 헤더를 사용해 클라이언트 IP를 가져온다  ⭕
- ③ 백엔드에서 `X-Forwarded-Port` 헤더를 사용한다  
- ④ 백엔드에서 `X-Forwarded-Proto` 헤더를 사용한다  

---

## 6️⃣ 문제 16  
10개의 EC2 인스턴스에 웹사이트를 배포했고, ELB로 트래픽을 분산하고 있습니다.  
사용자들이 페이지를 이동할 때마다 재로그인을 요구받는 문제가 발생합니다.  
개발 환경(인스턴스 1개)에서는 잘 동작합니다.  
이 문제의 원인은 무엇입니까?  

- ① 웹사이트 코드 자체 문제  
- ② EC2 인스턴스가 ELB의 IP만 보아서 사용자 IP를 인식하지 못함 
- ③ ELB의 Sticky Session이 비활성화되어 있음  ⭕

---

## 7️⃣ 문제 17  
Application Load Balancer가 트래픽을 Target Group으로 라우팅할 때 사용할 수 없는 기준은 무엇입니까?  

- ① 클라이언트 위치(지리적 위치) ⭕ 
- ② 호스트 이름  
- ③ 요청 URL 경로  
- ④ 소스 IP 주소  

---

## 8️⃣ 문제 18  
Application Load Balancer의 Target Group에 등록할 수 없는 대상은 무엇입니까?  

- ① EC2 인스턴스  
- ② Network Load Balancer  ⭕
- ③ 사설 IP 주소  
- ④ Lambda 함수  

---

## 9️⃣ 문제 19  
EC2 인스턴스를 r4.large에서 r4.4xlarge로 변경하는 것은 어떤 확장 방식입니까?  

- ① 수평 확장(Horizontal Scalability)  
- ② 수직 확장(Vertical Scalability)⭕  

---

## 0️⃣ 문제 20  
Auto Scaling Group이 Application Load Balancer의 Health Check를 사용 중입니다.  
EC2 인스턴스 하나가 비정상으로 판정되면 어떻게 됩니까?  

- ① ASG가 인스턴스를 유지하고 애플리케이션만 재시작한다  
- ② ASG가 인스턴스를 분리(detach)하고 그대로 둔다  
- ③ ASG가 인스턴스를 종료(terminate)한다 ⭕ 

---

## 1️⃣ 문제 21  
Auto Scaling Group의 Desired와 Max 용량이 3으로 설정되어 있습니다.  
CPU 사용률이 80%로 올라가며 Scale-out 조건(60%)을 초과했습니다.  
이때 어떤 일이 발생합니까?  

- ① 아무 일도 일어나지 않는다  ⭕
- ② Desired 용량이 4로 증가하고, Max는 3으로 유지된다  
- ③ Desired 용량이 4로 증가하고, Max도 4로 함께 증가한다  

---
