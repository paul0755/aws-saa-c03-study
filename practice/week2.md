
# 실습 목표

* EC2에 **IAM Role(AmazonS3FullAccess)** 부여
* **t4g.micro (ARM, Ubuntu 22.04)** 인스턴스 생성 + SSH 접속
* vim으로 **Hello World** 파일 생성
* EC2에서 **AWS CLI로 S3 업로드**
* 콘솔에서 업로드 파일 확인

<br>

## 1) IAM Role 생성 (EC2용 + AmazonS3FullAccess)

1. 콘솔 → **IAM** → **Roles** → **Create role**
2. **신뢰할 수 있는 엔터티 유형**: AWS 서비스
   **사용 사례**: **EC2** 선택 → Next
3. **Permissions policies**에서 **AmazonS3FullAccess** 검색 후 체크 → Next
4. **Role name**: `week2-role` → **Create role**
    - 이름, 설명은 원하는 내용을 적어도 된다.


✅ **결과**: EC2 인스턴스에 붙일 수 있는 S3 전체 접근 Role 준비 완료


<br>

## 2) Security Group 생성 (SSH 전용)

1. 콘솔 → **EC2** → **Security Groups** → **Create security group**
2. Name: `sg-ssh-only`, VPC: **default**
3. **Inbound rules**:
   * Type: **SSH** / Port: **22** / Source: **My IP** (권장)
4. **Outbound rules**: All traffic (기본값)
5. **Create security group**

✅ **결과**: SSH만 허용하는 SG 준비 완료

> 보안그룹은 포트 하나당 하나를 만들어주는게 좋다. 예를 들어 SSH 접속, 웹서버용, API 서버용 이렇게 나눠놓으면 서버를 새로 생성할 때마다 매번 보안그룹의 내부를 자세하게 안보고 내가 적은 이름만 보고 바로 적용시킬 수 있다.

<br>

## 3) EC2 인스턴스 생성 (Ubuntu 22.04 ARM, t4g.micro)

1. AWS 콘솔 → **EC2** → **Launch instance**
2. **Name**: `week2-ec2`
3. **AMI**: “**Ubuntu Server 22.04 LTS** (64-bit (Arm))” 선택

   * 반드시 **64-bit (Arm)** 아키텍처를 선택해야 t4g 타입 사용 가능
4. **Instance type**: **t4g.micro**
5. **Key pair**: **Create new key pair** → Name: `study-keypair` → Type: RSA → **.pem** 다운로드

   * (Mac/Linux) `chmod 400 study-keypair.pem` 해둘 것
   * (window) 권한 다 지우고 읽기 권한만 넣어주기
       ```
       icacls.exe myec2.pem /reset
       icacls.exe myec2.pem /grant:r %username%:(R)
       icacls.exe myec2.pem /inheritance:r
       ```

6. **Network settings**:

   * VPC: **default**
   * Subnet: default 
   * **Auto-assign public IP: Enable(자동 할당)**  ← “ip 자동활성화” 조건 충족
   * **Security group**: **Select existing** → `sg-ssh-only`, `default`
       - default는 나중에 내부망 통신에 사용됨
7. Storage: 기본값 사용
8. **Advanced details**는 다음 단계(4번)에서 설정

<br>


## 4) 고급 세부 정보 (IAM 인스턴스 프로파일 연결)

* 같은 생성 화면의 **Advanced details** → **IAM instance profile**:
  `week2-profile` 선택

✅ **결과**: 인스턴스가 부팅되면 자동으로 S3 전체권한 Credentials를 Role 통해 획득


<br>

## 5) S3 버킷 생성 (임시용)

1. 콘솔 → **S3** → **Create bucket**
2. **Bucket name**: 전역 고유값 (예: `study-ahn-hc-20250930`)
3. **AWS Region**: **ap-northeast-2 (Seoul)** (EC2와 동일 권장)
4. Public access: **Block all public access** 유지(기본)
5. **Create bucket**

✅ **결과**: 업로드 대상 버킷 준비 완료

<br>

## 6) EC2 SSH 접속 & vim으로 파일 생성

### 로컬에서 접속

```bash
# Mac/Linux
chmod 400 study-keypair.pem
ssh -i study-keypair.pem ubuntu@<EC2_PUBLIC_IP>

# Windows PowerShell
ssh -i .\study-keypair.pem ubuntu@<EC2_PUBLIC_IP>
```

> 🔵 ssh 접속 관련해서 진행 안되면 각 OS에 맞게 블로그글 찾아보기

### 접속 후(EC2 안에서)

```bash
# 필수 도구 설치 (Ubuntu 22.04)
sudo apt-get update
sudo snap install aws-cli --classic

# 파일 생성 (vim)
vim hello.txt
# (i) 입력모드 → Hello World 입력 → (Esc) → :wq → Enter 로 저장/종료

# 내용 확인
cat hello.txt
```

✅ **결과**: EC2에 `hello.txt` (“Hello World”) 준비

<br>

## 7) AWS CLI로 S3 업로드 (EC2 내부)

Role이 붙었으므로 `aws configure` 없이 바로 동작합니다. (권한/리전 점검 권장)

```bash
aws s3 cp hello.txt s3://<생성한 버킷 이름>/hello.txt
```

✅ **결과**: `s3://<버킷>/hello.txt` 객체로 업로드 완료

<br>

## 8) 콘솔에서 S3 파일 확인

1. 콘솔 → **S3** → 해당 버킷 → `hello.txt` 존재 확인
2. 객체 클릭 → **Open/Download** 버튼으로 내용 확인

✅ **결과**: 콘솔에서 업로드된 파일 확인 완료

<br>

## 실습 후 종료하기

1. ec2 종료
2. 버킷 삭제
