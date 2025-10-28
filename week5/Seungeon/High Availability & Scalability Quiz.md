# High Availability & Scalability Quiz

1. 다음 중 **애플리케이션 로드 밸런서가 서로 다른 타겟 그룹으로 트래픽을 라우팅할 수 있는 기준이 아닌 것**은 무엇입니까?
    
    ① 클라이언트의 위치(지리적 위치) ✅
    
    ② 호스트 이름
    
    ③ 요청 URL 경로
    
    ④ 소스 IP 주소 ❌
    
    > 애플리케이션 로드 밸런서(ALB)는 **HTTP/HTTPS 요청의 내용**을 기반으로 라우팅
    > 

---

1. **Elastic Load Balancers**는 애플리케이션에서 사용할 수 있는 ....................... 을(를) 제공합니다.
    
    ① 정적 IPv4 주소
    
    ② 정적 DNS 이름 ✅
    
    ③ 정적 IPv6 주소
    

---

1. **애플리케이션 로드 밸런서**와 **네트워크 로드 밸런서** 모두에서,
    
    **하나의 리스너에 여러 개의 SSL 인증서**를 로드할 수 있게 하는 기능은 무엇입니까?
    
    ① TLS 종료(TLS Termination)
    
    ② 서버 이름 표시(SNI, Server Name Indication) ✅
    
    ③ SSL 보안 정책(SSL Security Policies)
    
    ④ 호스트 헤더(Host Headers)
    

---

1. 당신은 10개의 **EC2 인스턴스** 앞단에 **Elastic Load Balancer**를 두고 웹사이트를 운영하고 있습니다. 사용자들이 웹사이트 내 페이지를 이동할 때마다 **다시 인증**을 요구받는다고 불평하고 있습니다.하지만 당신의 로컬 환경과 **EC2 인스턴스**가 1개뿐인 **Dev 환경**에서는 문제가 없습니다.
    
    그 이유는 무엇일까요?
    
    ① 웹사이트가 여러 EC2 인스턴스에서 호스팅될 때 발생하는 문제이다.
    
    ② EC2 인스턴스가 사용자의 실제 IP 주소를 보지 못하고, 대신 ELB의 IP 주소를 받아 로그아웃시키기 때문이다.
    
    ③ Elastic Load Balancer에서 Sticky Session이 활성화되어 있지 않기 때문이다. ✅
    

---

1. **Auto Scaling Group**에서 EC2 인스턴스의 개수를 자동으로 늘리거나 줄이며 애플리케이션을 실행하는 것을 무엇이라고 합니까?
    
    ① **Horizontal Scalability** ✅
    
    ② **Vertical Scalability**
    

---

1. 당신은 여러 **EC2 인스턴스** 위에 애플리케이션을 호스팅하고, 그 앞단에 **Elastic Load Balancer**를 두었습니다. 일주일 후, 사용자들이 간헐적으로 애플리케이션이 작동하지 않는다고 불평하기 시작했습니다. 조사 결과, 일부 **EC2 인스턴스**가 주기적으로 **crash**하는 것을 발견했습니다.
    
    이럴 때 사용자가 **crash된 인스턴스**에 연결되지 않도록 보호하려면 어떻게 해야 합니까?
    
    ① **ELB Health Checks** 활성화 ✅
    
    ② **ELB Stickiness** 활성화
    
    ③ **SSL Termination** 활성화
    
    ④ **Cross-Zone Load Balancing** 활성화
    

---

1. **EC2 인스턴스**를 **r4.large**에서 **r4.4xlarge**로 확장하는 것을 무엇이라고 합니까?
    
    ① **Horizontal Scalability**
    
    ② **Vertical Scalability** ✅
    

---

1. 당신은 **Application Load Balancer**를 사용하여 **EC2 인스턴스**에서 호스팅 중인 웹사이트로 트래픽을 분산하고 있습니다. 그런데 웹사이트에서 보이는 모든 트래픽의 **IPv4 주소**가 실제 사용자의 IP가 아니라, **Application Load Balancer의 사설 IP 주소들**로만 나타납니다.
    
    웹사이트에 접속한 **클라이언트(사용자)**의 실제 IP 주소를 얻으려면 어떻게 해야 합니까?
    
    ① 웹사이트의 프론트엔드를 수정하여 사용자가 모든 요청마다 자신의 IP를 전송하도록 한다.
    
    ② 웹사이트의 백엔드를 수정하여 클라이언트 IP 주소를 **X-Forwarded-For** 헤더에서 가져오도록 한다. ✅
    
    ③ 웹사이트의 백엔드를 수정하여 클라이언트 IP 주소를 **X-Forwarded-Port** 헤더에서 가져오도록 한다. ❌
    
    ④ 웹사이트의 백엔드를 수정하여 클라이언트 IP 주소를 **X-Forwarded-Proto** 헤더에서 가져오도록 한다.
    
    > ALB는 원래 클라이언트의 IP 주소를 HTTP 헤더에 실어서 같이 보냄 
    ⇒ **X-Forwarded-For**
    > 

---

1. 한 애플리케이션이 **Application Load Balancer**와 **Auto Scaling Group**으로 배포되어 있습니다. 현재는 ASG를 수동으로 스케일링하고 있지만, 이제는 **EC2 인스턴스들에 대한 평균 연결 수가 약 1000 정도가 되도록** 자동으로 유지하고 싶습니다.
    
    이때 어떤 **Scaling Policy**를 사용해야 합니까?
    
    ① Simple Scaling Policy
    
    ② Step Scaling Policy ❌
    
    ③ Target Tracking Policy ✅
    
    ④ Scheduled Scaling Policy
    
    > 평균, 목표 ⇒ Target Tracking Policy
    > 

---

1. 규제 준수를 위해 최종 사용자에게 **고정(static)된 IP 주소**를 노출하고자 합니다.
이로써 사용자들이 방화벽 규칙을 안정적으로 설정하고 규제 기관의 승인을 받을 수 있도록 하려 합니다.
이 경우 어떤 유형의 **Elastic Load Balancer**를 선택해야 합니까?
    
    ① Application Load Balancer에 Elastic IP를 연결한다.
    
    ② Network Load Balancer ✅
    
    ③ Classic Load Balancer
    

---

1. 당신은 **Network Load Balancer**를 사용하여 **us-east-1** 리전에 있는 여러 **EC2 인스턴스**로 트래픽을 분산하고 있습니다.
현재 **us-east-1b AZ**에 2대, **us-east-1e AZ**에 5대의 인스턴스가 있습니다.
조사 결과, **두 AZ 간 트래픽이 균등하게 분배되지만**, **us-east-1b**의 인스턴스에서 **CPU 사용률이 더 높습니다.**
이 문제를 해결하려면 어떻게 해야 합니까?
    
    ① Cross-Zone Load Balancing 활성화 ✅
    
    ② Sticky Sessions 활성화
    
    ③ ELB Health Checks 활성화
    
    ④ SSL Termination 활성화
    

---

1. 당신은 한 회사의 **Solutions Architect**로서,**초당 수백만 건의 요청을 처리하는 고성능·저지연 애플리케이션**을 설계해야 합니다.
이때 어떤 유형의 **Elastic Load Balancer**를 선택해야 합니까?
    
    ① Application Load Balancer
    
    ② Classic Load Balancer
    
    ③ Network Load Balancer ✅
    

---

1. 당신은 **Application Load Balancer**를 사용하여 다음 세 개의 **Hostname** 기반으로 트래픽을 라우팅하고 있습니다:
    - users.example.com
    - api.external.example.com
    - checkout.example.com
    
    이 세 호스트 이름 각각에 대해 **HTTPS 연결**을 설정하려면 어떻게 구성해야 합니까?
    
    ① HTTP → HTTPS 리디렉션 규칙을 사용한다.
    
    ② 보안 그룹 SSL 인증서를 사용한다.
    
    ③ Server Name Indication (SNI)을 사용한다. ✅
    

---

1. 당신은 **Application Load Balancer**에서 **애플리케이션 기반 커스텀 쿠키**를 생성하려고 합니다.
다음 중 어떤 값을 **쿠키 이름**으로 사용할 수 있습니까?
    
    ① AWSALBAPP ❌
    
    ② APPUSERC ✅
    
    ③ AWSALBTG
    
    ④ AWSALB
    
    > `AWSALB`, `AWSALBTG`, `AWSALBAPP` → ALB가 자체적으로 사용하는 예약 쿠키 이름
    > 
    > 
    > `APPUSERC` → 사용자 정의 형태의 일반 이름
    > 

---

1. 당신은 **Auto Scaling Group**에서 관리되는 여러 **EC2 인스턴스** 위에 애플리케이션을 호스팅하고 있습니다. 해당 ASG의 **desired capacity**(희망 용량)와 **maximum capacity**(최대 용량)를 모두 3으로 설정했습니다. 또한, **CPU Utilization**이 60%에 도달하면 스케일 아웃하도록 설정된 **CloudWatch Alarm**을 만들어 두었습니다. 애플리케이션이 갑자기 많은 트래픽을 받아 현재 **CPU Utilization이 80%**까지 상승했습니다.
이때 어떤 일이 발생합니까?
    
    ① 아무 일도 일어나지 않는다. ✅
    
    ② desired capacity가 4로 증가하고, maximum capacity는 3으로 유지된다. ❌
    
    ③ desired capacity가 4로 증가하고, maximum capacity도 4로 유지된다.
    
    > Auto Scaling Group은 `desired capacity`를 조정할 때 **`maximum capacity`를 절대 초과할 수 없음**
    > 

---

1. **Application Load Balancer**의 **Target Group**에 등록할 수 있는 대상 중, 다음 중 **해당되지 않는 것**은 무엇입니까?
    
    ① EC2 Instances
    
    ② Network Load Balancer ✅
    
    ③ Private IP Addresses
    
    ④ Lambda Functions
    

---

1. 당신은 **ASG(Auto Scaling Group)** 와 **Network Load Balancer**를 사용 중입니다.
ASG에서 실행 중인 애플리케이션은 **HTTP 프로토콜**을 지원하며, 현재 **Load Balancer Health Check**와 연동되어 있습니다. 지금은 **TCP Health Check**를 사용 중인데, 이를 **HTTP Health Check**로 바꾸고자 합니다.
어떻게 해야 합니까?
    
    ① Application Load Balancer로 마이그레이션한다. ❌
    
    ② Health Check를 HTTP로 마이그레이션한다. ✅ 
    
    > NLB는 아예 HTTP Health Check 기능이 없음
    > 

---

1. 상사는 당신에게 **Auto Scaling Group**이 **데이터베이스에 보내는 요청 수(분당 요청 수)**에 따라 스케일링되도록 구성하라고 요청했습니다.
이 요구사항을 충족하려면 어떻게 해야 합니까?
    
    ① CloudWatch **custom metric**을 생성하고, 그 지표에 대한 **CloudWatch Alarm**을 만들어 ASG를 스케일링한다. ✅
    
    ② 정중하게 그것은 불가능하다고 말한다.
    
    ③ **Detailed Monitoring**을 활성화하고, 해당 지표에 대해 **CloudWatch Alarm**을 만들어 ASG를 스케일링한다.
    

---

1. 당신은 **EC2 인스턴스**에서 호스팅된 웹사이트를 **Auto Scaling Group**과 **Application Load Balancer**로 구성했습니다.
현재 웹사이트는 **HTTP**로 서비스되고 있으며, 이를 **HTTPS**로 전환하라는 요청을 받았습니다.
이미 **ACM(AWS Certificate Manager)** 에서 인증서를 발급받아 **Application Load Balancer**에 연결했습니다.
사용자들이 HTTP 대신 HTTPS로만 접속하도록 강제하려면 어떻게 해야 합니까?
    
    ① 모든 고객에게 이메일을 보내 HTTP 대신 HTTPS를 사용하도록 안내한다.
    
    ② **Application Load Balancer**를 구성하여 HTTP를 HTTPS로 리디렉션하도록 설정한다. ✅
    
    ③ **DNS 레코드**를 구성하여 HTTP를 HTTPS로 리디렉션하도록 설정한다.
    

---

1. 당신은 **Application Load Balancer** 앞단에 있는 **Auto Scaling Group**을 운영 중입니다.
ASG는 **ALB Health Check**를 사용하도록 설정해 두었고, 그 결과 한 **EC2 인스턴스**가 방금 **unhealthy(비정상)** 로 표시되었습니다.
이 EC2 인스턴스에는 어떤 일이 발생합니까?
    
    ① ASG는 인스턴스를 계속 실행시키고, 애플리케이션만 재시작한다. ❌
    
    ② ASG는 EC2 인스턴스를 분리(detach)하지만, 인스턴스 자체는 계속 실행 상태로 둔다.
    
    ③ ASG는 EC2 인스턴스를 종료(terminate)한다. ✅
    
    > 지금은 ASG가 **ALB Health Check 결과를 신뢰하도록 설정
    ⇒ ALB가 “이 인스턴스는 unhealthy다”라고 판단하면, 
    ⇒ ASG도 그 인스턴스를 비정상으로 간주**
    > 

---

1. **Application Load Balancer**가 지원하는 프로토콜 중, 다음 중 **해당되지 않는 것**은 무엇입니까?
    
    ① HTTP
    
    ② HTTPS
    
    ③ TCP ✅
    
    ④ WebSocket
    

---