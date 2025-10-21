# 🧠 AWS VPC & Networking Quiz 정리 (for VSCode Practice)


### Question 1  
**How can you capture information about IP traffic inside your VPCs?**  
✅ **Enable VPC Flow Logs**  
(→ VPC 내부 트래픽을 CloudWatch Logs나 S3로 캡처하는 기능)

---

### Question 2  
**Provide Internet access to EC2 instances in private subnets (IPv4) with least admin effort.**  
✅ **NAT Gateway**  
(→ 자동 확장, 관리 불필요, 고가용성 제공)

---

### Question 3  
**Using a Direct Connect connection, you can access both public and private AWS resources.**  
✅ **True**  
(→ 퍼블릭 AWS 서비스 + VPC 내 프라이빗 리소스 모두 가능)

---

### Question 4  
**Major components of AWS Site-to-Site VPN connection?**  
✅ **Virtual Private Gateway and Customer Gateway**

---

### Question 5  
**Best bastion host Security Group configuration?**  
✅ **Allow traffic only on port 22 from the company’s public CIDR**  
(→ SSH만 허용, 내부 CIDR 아님)

---

### Question 6  
**Gateway Endpoint available for which services?**  
✅ **Amazon S3 & DynamoDB**

---

### Question 7  
**Allow only ALB to access backend EC2 instances on port 80.**  
✅ **Add Inbound Rule with port 80 and ALB's Security Group as the source**

---

### Question 8  
**What does CIDR 10.0.4.0/28 correspond to?**  
✅ **10.0.4.0 to 10.0.4.15**

---

### Question 9  
**Backup for Direct Connect (cost-effective & secure)?**  
✅ **Setup a Site-to-Site VPN connection as a backup**

---

### Question 10  
**500 Mbps Direct Connect connection type?**  
✅ **Hosted Connection**  
(→ Dedicated는 1/10/100 Gbps 고정)

---

### Question 11  
**No IPv4 addresses left in VPC (dual-stack mode). What to do?**  
✅ **Add an additional IPv4 CIDR to your VPC**

---

### Question 12  
**Subnet for at least 28 EC2 instances → 최소 크기?**  
✅ **/27**  
(/27은 32 IP - 5 = 27 usable)

---

### Question 13  
**Private, consistent connection (no internet)?**  
✅ **AWS Direct Connect**

---

### Question 14  
**EC2 has no internet access after attaching IGW → NOT a possible issue?**  
✅ **Security Group does not allow traffic in**  
(→ Outbound 트래픽 문제 아님)

---

### Question 15  
**VPC Peering enabled but EC2 cannot communicate → likely issue?**  
✅ **Check the Route Tables in VPC B**

---

### Question 16  
**VPC CIDR acceptable if on-prem 10.0.0.0/8 & 192.168.0.0/16?**  
✅ **172.16.0.0/12**  
(→ 중복 피해야 함, RFC1918 범위 중 미사용 대역 선택)

---

### Question 17  
**Security Group vs NACL level?**  
✅ **Security Group → EC2 instance level**  
✅ **NACL → Subnet level**

---

### Question 18  
**Scale Site-to-Site VPN throughput beyond 1.25 Gbps?**  
✅ **Use Transit Gateway**  
(→ 여러 터널 병렬 연결 가능)

---

### Question 19  
**Protect/control VPC traffic (Layer 3~7)?**  
✅ **AWS Network Firewall**

---

### Question 20  
**Reserved IPs in 10.0.0.0/24 subnet → EXCEPT**  
✅ **10.0.0.4**  
(→ 0,1,2,3,255 예약됨)

---

### Question 21  
**Direct Connect → Access another VPC in different region**  
✅ **Use a Direct Connect Gateway**

---

### Question 22  
**VPC Peering among 3 VPCs (A,B,C)**  
✅ **Establish 3 Peering Connections (A-B, A-C, B-C)**  
(→ VPC Peering은 transitive 지원 안 함)

---

### Question 23  
**Backup connection over Internet between on-prem sites**  
✅ **AWS VPN CloudHub**

---

# ❌틀린문제 해설

## ✅ Question 5
**문제:**  
A web app backend in private subnets, bastion host in public subnet.  
개발자들이 백엔드 EC2에 접근해야 하지만, 외부 노출은 금지됨.  
→ Bastion Host SG 설정 중 가장 안전한 방법은?

**정답:**  
✅ **Allow traffic only on port 22 from the company’s public CIDR**

**📘 개념 키워드:**  
- Bastion Host (점프 서버)  
- Security Group (Ingress/Egress)  
- SSH (Port 22)  
- Public CIDR vs Private CIDR

**🔍 상세 설명:**  
Bastion Host는 내부망(Private Subnet)에 접근하기 위한 **보안 게이트웨이(중간 SSH 서버)** 역할을 함.  
따라서 보안그룹에서 외부 접근을 제한해야 함.  
- SSH 접속 포트는 **22번 포트**  
- 접근 가능한 IP 대역은 회사의 **공인 IP(CIDR)** 로 제한  
- HTTP(80)나 사설망 CIDR은 보안상 부적절

**🧾 해설 요약:**  
> Bastion Host는 **회사 외부에서 SSH로 접속하는 유일한 창구**이므로  
> **22번 포트만 허용 + 회사 공인 IP로만 제한**해야 함.

---

## ✅ Question 7
**문제:**  
ALB가 퍼블릭 서브넷에 있고, EC2(백엔드)는 프라이빗 서브넷에 있음.  
오직 ALB만 EC2의 80포트에 접근해야 함. 어떻게 SG 설정?

**정답:**  
✅ **Add an Inbound Rule with port 80 and ALB's Security Group as the source**

**📘 개념 키워드:**  
- ALB (Application Load Balancer)  
- Security Group 간 참조  
- Inbound Rule  
- VPC Internal Traffic

**🔍 상세 설명:**  
ALB는 클라이언트 요청을 받아 백엔드 인스턴스로 전달함.  
이때 인스턴스가 오직 ALB를 통해서만 접근되도록 제한하려면,  
**백엔드 EC2 SG의 Inbound source를 ALB의 SG ID로 지정**해야 함.  
→ IP대역(0.0.0.0/0)이나 VPC CIDR로 설정 시 불필요하게 노출됨.

**🧾 해설 요약:**  
> 백엔드 EC2는 ALB의 요청만 받도록 설정해야 함.  
> 따라서 **Source = ALB의 SG** 로 설정해 내부에서만 접근 가능하게 만든다.

---

## ✅ Question 9
**문제:**  
Direct Connect가 설정된 상태에서, 백업용으로 가장 저렴하고 안전한 연결은?

**정답:**  
✅ **Setup a Site-to-Site VPN connection as a backup**

**📘 개념 키워드:**  
- AWS Direct Connect (전용선)  
- Site-to-Site VPN (IPSec 터널)  
- Hybrid Connectivity  
- Backup Link (Failover)

**🔍 상세 설명:**  
Direct Connect는 전용선을 이용해 안정적이지만 비용이 높고, 장애 시 대비 필요함.  
이때 인터넷 기반 **Site-to-Site VPN**을 백업으로 구성하면,  
전용선이 다운돼도 트래픽이 자동으로 암호화된 터널을 통해 전달 가능.  
비용도 저렴하고 설정도 간단함.

**🧾 해설 요약:**  
> Direct Connect 장애 대비용으로 **Site-to-Site VPN**을 백업으로 두는 게  
> 가장 **비용 효율적이고 보안적인 대안**이다.

---

## ✅ Question 13
**문제:**  
인터넷을 거치지 않고, **일관적이고 프라이빗한 전용 연결**을 구성하려면?

**정답:**  
✅ **AWS Direct Connect**

**📘 개념 키워드:**  
- AWS Direct Connect  
- Private Connection  
- Dedicated Line  
- On-prem ↔ VPC

**🔍 상세 설명:**  
Direct Connect는 **고정적이고 전용선 기반의 프라이빗 연결**을 제공함.  
인터넷을 거치지 않아 지연(latency)이 적고 안정적.  
VPN은 인터넷을 경유하므로 지연과 불안정성이 존재함.  
대규모 기업 환경에서 주로 사용됨.

**🧾 해설 요약:**  
> 인터넷을 사용하지 않고, **일정하고 안전한 네트워크 연결**을 원한다면  
> **Direct Connect**가 정답이다.

---

## ✅ Question 15
**문제:**  
VPC Peering이 설정됐고, VPC A 라우팅 테이블만 업데이트 했는데 통신 불가. 왜일까?

**정답:**  
✅ **Check the Route Tables in VPC B**

**📘 개념 키워드:**  
- VPC Peering  
- Route Table  
- Bi-directional Routing  
- Transitive Peering 제한

**🔍 상세 설명:**  
VPC Peering은 **양방향 라우팅** 설정이 필요함.  
즉, A → B, B → A 각각의 라우팅 테이블이 업데이트되어야 통신 가능.  
한쪽만 설정하면 **패킷이 반대편에서 되돌아오지 못함**.  
또한 VPC Peering은 전이적(Transitive) 라우팅을 지원하지 않음.

**🧾 해설 요약:**  
> Peering은 **양방향 라우팅**이 필수.  
> 한쪽만 설정하면 통신이 일방통행되어 실패한다.

---

## ✅ Question 16
**문제:**  
온프레미스 네트워크가 `10.0.0.0/8`, `192.168.0.0/16`일 때,  
AWS VPC와 나중에 연결할 것을 고려하면 어떤 CIDR이 적절할까?

**정답:**  
✅ **172.16.0.0/12**

**📘 개념 키워드:**  
- RFC 1918 (사설 IP 주소 대역)  
- CIDR Overlap 방지  
- Hybrid Connectivity (On-prem + VPC)

**🔍 상세 설명:**  
사설 IP 주소는 RFC1918 기준으로 3개 대역 존재:
- 10.0.0.0/8  
- 172.16.0.0/12  
- 192.168.0.0/16  

이미 온프레미스에서 10.x.x.x 와 192.x.x.x 대역을 사용 중이라면,  
**겹치지 않는 172.16.0.0/12** 범위를 사용하는 것이 최선.  
CIDR이 겹치면 라우팅 충돌로 통신 불가.

**🧾 해설 요약:**  
> 온프레와 중복되지 않는 **172.16.0.0/12** 대역을 사용해야  
> 추후 하이브리드 연결 시 IP 충돌이 발생하지 않는다.

---

## ✅ Question 20
**문제:**  
Subnet CIDR `10.0.0.0/24`에서 AWS가 예약한 IP 5개 중  
**예약되지 않은 IP**는 무엇인가?

**정답:**  
✅ **10.0.0.4**

**📘 개념 키워드:**  
- Subnet Reserved IP  
- AWS Networking Rules  
- CIDR /24

**🔍 상세 설명:**  
AWS는 각 Subnet에서 5개 IP를 예약함:  
| IP | 설명 |
|----|------|
| `.0` | Network address |
| `.1` | VPC Router |
| `.2` | DNS / AWS 내부용 |
| `.3` | Future use (AWS 예약) |
| `.255` | Broadcast address |

따라서 `.4` 부터가 사용 가능한 첫 IP.

**🧾 해설 요약:**  
> AWS는 각 Subnet의 **처음 4개 + 마지막 1개 IP**를 예약한다.  
> 따라서 `.4` 부터 사용 가능하다.

---

## ✅ Question 21
**문제:**  
Direct Connect로 회사 데이터센터 ↔ VPC A 연결되어 있음.  
이제 다른 리전의 VPC B에도 접근해야 함. 어떻게 해야 할까?

**정답:**  
✅ **Use a Direct Connect Gateway**

**📘 개념 키워드:**  
- AWS Direct Connect Gateway  
- Multi-Region Connectivity  
- Private Virtual Interface (VIF)

**🔍 상세 설명:**  
기본 Direct Connect는 한 리전 내 VPC만 연결 가능.  
여러 리전의 VPC를 동시에 연결하려면,  
**Direct Connect Gateway (DXGW)** 를 통해  
각 리전의 VPC와 연결할 수 있음.  
이렇게 하면 **하나의 전용선으로 여러 리전** 접근 가능.

**🧾 해설 요약:**  
> 여러 리전의 VPC에 연결하려면 **Direct Connect Gateway** 사용.  
> DXGW는 리전 간 프라이빗 연결을 가능하게 한다.

---
