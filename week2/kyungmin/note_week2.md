## 📘 IAM (Identity and Access Management)

### ❗IAM의 개념

AWS IAM은 **AWS 리소스에 대한 접근을 제어할 수 있는 웹 서비스**로 누가(Identity: 사용자, 그룹, 역할) 무엇(Resource)에 대해 어떤 액션(Action)을 할 수 있는 지를 결정한다. 

- IAM은 AWS 계정에 대한 인증(Authentication) 및 권한 부여(Authorization)를 제어하는 데 필요한 인프라를 제공한다.
- 사용자를 생성하고 그룹에 배치하기 때문에 리전별로 따로 설정할 필요 없는 글로벌 서비스이다.

### 🦷IAM의 구성 요소

- 👤사용자 (User)
    - 루트 계정(root account)이 만든 개별 계정으로 계정 생성 시 루트 사용자 1개 자동 생성 된다.
        - AWS 계정에 로그인하는 사람/애플리케이션
        - 실무에서는 루트 대신 IAM 사용자/역할을 만들어 사용
    - 콘솔 로그인: 사용자 이름 + 비밀번호
    - CLI/API 접근: Access Key + Secret Key
    - 권한은 정책(Policy)을 통해 부여해야 한다.
- 👥그룹 (Group)
    - IAM 사용자들을 묶어서 동일한 권한을 부여할 때 사용
    - 그룹 안에는 정책만 부여 가능(직접 리소스는 소유하지 않음)
    - ex) Developers, Admins
- 🎭역할 (Role)
    - IAM 사용자나 AWS 서비스가 일시적으로 빌려 쓰는 권한
    - 비밀번호나 Access Key 없음 → STS(Security Token Service)를 통해 임시 자격 증명 부여
    - 대표 사례
        - EC2가 S3접근 (EC2 Role)
        - Lambda가 Dynamo DB 접근(Lambda Role)
        - Cross-account Access(다른 AWS 계정에서 권한 위임)

<aside>
❓

**루트 사용자(root user)와 IAM 사용자(IAM user) ?**

- 루트 사용자
    - AWS 계정을 처음 생성할 때 자동으로 만들어지는 계정 (이메일 + 비밀번호 = 루트 사용자 자격 증명)
    - 해당 AWS 계정 내 모든 리소스와 결제, 보안 등 모든 작업 가능(슈퍼 관리자)
- IAM 사용자
    - 루트 사용자가 로그인한 후 직접 생성하는 개별 계정

✅ 루트 사용자가 IAM 사용자들을 만들고, 권한을 줄 수 있다. 
IAM 사용자는 다른 IAM 사용자를 직접 만들 수는 없으나, 관리자 권한을 부여받으면 가능

</aside>

### 🪪IAM 정책 (Policy)

- JSON 문서 형식으로, 사용자, 그룹, 역할이 어떤 작업을 허용/거부할 수 있는 지 정의한다.
    
    ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Effect": "Allow",
                "Action": "ec2:Describe*",
                "Resource": "*",
            }, 
          	{
                "Effect": "Allow",
                "Action": "elasticloadbalancing:Describe*",
                "Resource": "*",
            },
          	{
                "Effect": "Allow",
                "Action": [
                  "cloudwatch:ListMetrics",
                  "cloudwatch:GetMetricStatistics",
                  "cloudwatch:Describe*"
                ],
                "Resource": "*",
            },
        ]
    }
    ```
    
- 구성 요소
    - Version: 정책 언어 버전(거의 항상 “2012-10-17”)
    - Id: 정책을 식별하기 위한 ID(선택)
    - Statement: 필수 요소, 한 개 이상 포함된다.
- Statement 세부 구성
    - Sid(Statement ID): Statement를 구분하는 식별자(선택)
    - Effect: 허용(Allow) 또는 거부(Deny)
    - Principal: 정책이 적용되는 주체(사용자, 역할, 계정)
        - IAM Identity-based Policy에서는 잘 안 쓰이고, 리소스 기반 정책(Resource-based Policy)에서 자주 등장한다.
        - ex) S3 버킷 정책, Lambda 리소스 정책 등에서 “누가 접근 가능한가” 정의할 때 사용
    - Action: 허용/거부할 API 호출 (`S3:GetObject`, `ec2:StartInstance` 등)
    - Resource: 적용되는 리소스 (ARN(Amazon Resource Name) 또는 *)
    - Condition: 조건부 허용/거부
        - aws:SourceIp → 특정 IP에서만 접근
        - aws: MultiFactorAuthPresent → MFA 인증된 사용자만 허용
- 정책 유형
    - AWS Managed Policy: AWS에서 제공 (ex. AmazonS3ReadOnlyAccess)
    - Customer Managed Policy: 사용자가 작성 (재사용 가능)
    - Inline Policy: 특정 사용자/그룹/역할에 종속 (재사용 불가)
- 정책 평가 순서
    1. 기본은 암묵적 거부(Implicit Deny)
    2. 정책에서 허용(Allow) → 허용
    3. 명시적 거부(Explicit Deny) → 무조건 거부
- 권한 부여 방식
    - 정책은 사용자, 그룹, 역할에 붙일 수 있다.
    - 관리 효율성을 위해 사용자 개별보다는 그룹 기반 관리 권장
    - 애플리케이션/서비스(EC2, Lambda)는 Access Ky 대신 IAM Role 사용

### 🔐IAM 보안 및 관리

- IAM Credential Report(Account-level)
    - 계정 내 모든 사용자 자격 증명 상태 요약
    - 모든 IAM 사용자 보안 상태를 CSV로 확인
    - MFA 적용 여부, Access Key 마지막 사용일 등
- IAM Access Analyzer(User-level)
    - 특정 사용자에게 부여된 권한과 마지막 서비스 사용 시간 제공
    - 사용되지 않는 권한을 찾아 최소 권한 원칙 유지 가능
    - S3 버킷, IAM 역할, KMS 키, Lambda 함수 등에서 외부 계정에 공유된 리소스 탐지
- Password Policy
    - 최소 길이 설정
    - 대문자, 소문자, 숫자, 특수문자 요구
    - 비밀번호 재사용 금지
    - 비밀번호 만료 주기 설정 및 새 비밀번호 강제
- MFA(Multi-Factor Authentication)
    - 비밀번호(you know) + 장치(you own) →  2차 인증 장치
    - 루트 계정 및 관리자 계정에 반드시 활성화
    - MFA 방식
        - Virtual MFA(Google Authenticator, Authy 등)
        - U2F Security Key(Yubikey 등)
        - Hardware Key Fob(AWS 파트너 제공)
    - 비밀번호 유출 시에도 계정 보호 가능

### 🌟IAM 권장 사항

- 루트 계정은 MFA 적용 & Access Key 발급 금지
- 루트는 필수 작업 외엔 사용하지 않고 IAM 사용자/역할 활용
- **Least Privilege Principle(최소 권한 원칙)** 적용
- 그룹 기반 권한 관리 권장
- EC2, Lambda 등 서비스는 Access Key 대신 IAM Role 사용
- Access Key는 주기적으로 교체 & 미사용 키는 삭제

## 📗 AWS CLI & SDK

### 🚪AWS 접근 방식

- Management Console: 브라우저 UI (Password + MFA)
- AWS CLI: 명령어 기반 (Access Key 필요)
- AWS SDK: 프로그래밍 언어 기반 라이브러리(Access Key 필요)

### 📋 AWS CLI (Command Line Interface)

- 터미널/명령 프롬프트에서 AWS 서비스를 명령어(Command Line)를 통해 제어할 수 있는 도구
- AWS Management Console(웹 UI) 대신 AWS 공용 API에 직접 액세스 해서  자동화, 스크립트 실행, 빠른 실험에 유용
- 설치 후 `aws configure`로 Access Key / Secret Key, 기본 Region, 출력 형식을 설정
    
    ```bash
    aws configure
    AWS Access Key ID [None]: ****
    AWS Secret Access Key [None]: ****
    Default region name [None]: ap-northeast-2
    Default output format [None]: json
    ```
    
    - 파일 경로
        - ~/.aws/credentials(키 저장)
        - ~/.aws/config(리전, 출력 형식)
- 출력 형식: json, text, table
- Profiles
    - 여러 계정/환경 관리 가능
    - `aws s3 ls -- profile dev`
- STS Assume Role
    - 다른 계정 Role 사용 → `aws sts assume-role`
    - 임시 자격증명(AccessKey, SecretKey, Session Token) 발급

### 📦 AWS SDK

- 특정 언어용 라이브러리 집합
- 지원 언어: JavaScript, Python, Java, Go, Ruby, PHP, .Net, C++ 등
- Mobile SDK/ IoT Device SDK도 제공
- CLI 역시 내부적으로는 Python SDK에 기반

## 📙 Amazon EC2(Elastic Compute Cloud)

### ❗EC2 개념

EC2는 아마존이 제공하는 클라우드 가상 서버이다. AWS의 대표적 IaaS(Infrastructure as a Service)로, 단일 서비스가 아니라 여러 기능이 있다. 

- 가상 머신 임대: EC2 Instance
- 스토리지: EBS, EFS, Instance Store
- 로드 밸런싱: ELB
- 오토 스케일링: ASG

### 🔍 EC2 구성 요소 (Sizing & Configuration)

- 운영체제(OS): Linux, Windows, Mac 등
- CPU: 성능과 코어 개수 선택 가능
- RAM(메모리): 서버가 동시에 처리할 수 있는 작업 크기 결정
- 스토리지(저장소)
    - EBS/EFS → 네트워크 연결된 스토리지
    - Instance Store → 인스턴스에 직접 붙는 하드웨어 디스크
- 네트워크 카드: 인터넷 속도, 퍼블릭 IP 설정 가능
- 보안 설정: 방화벽(Security Group)으로 트래픽 제어
- User Data: 서버가 처음 켜질 때 자동 실행되는 스크립트

### 📜 EC2 User Data

User Data는 서버가 처음 켜질 때 실행되는 자동화 스크립트로 서버 업데이트, 프로그램 설치(ex. 웹 서버 Apache, Nginx), 특정 파일 다운로드 등이 그 예이다. 

- 서버 시작할 때 한 번만 실행된다.
- 항상 루트 권한으로 실행된다.
- 민감 정보(비밀번호, 키 등)는 넣으면 안된다.(암호화 안됨)

### 🙄 EC2 인스턴스 타입

AWS는 용도에 따라 여러 가지 인스턴스를 제공한다.

- 범용(General Purpose, t/m): CPU/메모리 균형 → 웹 서버, 앱 서버에 적합
- 컴퓨팅 최적화(Compute Optimized, c): CPU 위주 → 게임 서버, 배치 작업, 고성능 연산
- 메모리 최적화(Memory Optimized, r/x/z): 메모리 위주 → 데이터베이스, 캐시 서버
- 가속화(Accelerated Computing, p/g/f): GPU/FPGA → 머신러닝, 그래픽 처리
- 스토리지 최적화(Storage Optimized, i/d/h): 디스크 I/O 위주 → 대용량 DB, 로그 처리

네이밍 규칙

ex) `m5.2xlarge`

- m: 클래스 (범용)
- 5: 세대(버전
- 2xlarge: 크기(성능/메모리 크기)

### 🛡️ 보안 그룹(Security Group)

보안 그룹은 서버의 방화벽으로 인스턴스로 들어고 나가는 네트워크를 제어한다.

- 허용(Allow) 규칙만 있음 (Deny 규칙은 없음)
- 인스턴스 여러 대에 재사용 가능
- 기본: 인바운드(들어오는 트래픽) 차단, 아웃바운드(나가는 트래픽) 허용

자주 쓰는 포트 번호

- 22: SSH(리눅스 원격 접속)
- 3389: RDP(윈도우 원격 접속)
- 80: HTTP(웹 사이트)
- 443: HTTPS(보안 웹 사이트)

👉 애플리케이션이 안 열리면? 보안 그룹 문제일 확률이 높다.

👉 Connection refused라면? 보안 그룹은 통과했지만 서버 안의 프로그램이 실행이 안된 것

### 👛 EC2 구매 옵션

- On-Demand(주문형)
    - 필요할 때 바로 켜고 끔
    - 초 단위 과금(가장 비쌈)
    - 단기적이고 불규칙한 사용에 적합
- Reserved Instance(예약형)
    - 1년/3년 약정 → 최대 72% 할인
    - 꾸준히 쓰는 워크로드(ex. DB)에 적합
- Savings Plan
    - 일정 금액/시간을 약정 → RI와 비슷한 할인
    - 인스턴스 크기/OS 변경에 더 유연
- Spot Instance
    - 남는 서버 자원을 싸게 빌림(최대 90% 할인)
    - 언제든 종료될 수 있음 → 중단돼도 괜찮은 작업에만 사용
    - ex) 배치 처리, 데이터 분석, 이미지 처리
- Dedicated Host
    - 물리적 서버 자체를 예약
    - 규제 준수/특수 라이선스 필요할 때
- Dedicated Instance
    - 다른 계정과 하드웨어 공유하지 않음(서버 단위)
- Capacity Reservation
    - 특정 AZ에 서버 용량 확보
    - 할인은 없음 → 꼭 필요한 경우만 사용

호텔에 비유하면

- On-Demand: 즉시 예약, 제일 비쌈
- Reserved: 장기 계약, 싸게 사용
- Spot: 빈 방 경매, 싸지만 언제든 쫓겨남
- Dedicated Host: 호텔 건물 통째로 예약
- Capacity Reservation: 방만 예약해두고 쓸지 안 쓸지는 나중에

### 📍Spot Instances & Fleet

- Spot Instance
    - 현재 가격(spot price)이 내가 설정한 최대 가격 이하일 때만 실행
    - 가격이 오르면 2분 뒤 강제 종료
    - Spot Block: 1~6시간 동안은 강제 종료 안됨
- Spot Fleet
    - Spot Instance 여러 개 + On-Demand Instance 조합
    - 전략적으로 가장 저렴하거나 안정적인 인스턴스를 자동 선택
    - 할당 전략
        - lowestPrice → 제일 싼 곳 부터
        - diversified → 분산 배치
        - capacityOptimized → 안정성 위주
        - priceCapacityOptimized(추천) → 안정성과 가격 모두 고려
    
    👉 Spot Fleet = “자동 경매 대행인”같은 역할