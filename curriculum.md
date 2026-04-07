# AWS Certified Cloud Practitioner 마스터 커리큘럼

---

## 1. 과정 개요 (Course Overview)

**과정 제목**: AWS Certified Cloud Practitioner (CLF-C02) 완전 정복

**과정 설명**:

이 과정은 클라우드 컴퓨팅에 대한 사전 지식이 전혀 없는 학습자가 AWS Certified Cloud Practitioner 자격증을 취득하고, 나아가 AWS 클라우드의 핵심 개념과 서비스를 독립적으로 활용·설명·교육할 수 있는 수준까지 도달하는 것을 목표로 합니다.

AWS Certified Cloud Practitioner(CLF-C02)는 AWS의 입문 수준 자격증으로, 클라우드 개념, AWS 핵심 서비스, 보안 및 규정 준수, 요금 및 결제 모델을 포괄합니다. 이 시험은 IT 직군뿐 아니라 영업, 관리, 재무 등 비기술 직군에서도 클라우드에 대한 기본 소양을 증명하기 위해 널리 활용됩니다.

본 커리큘럼은 시험 합격에 필요한 내용을 넘어, 실무에서 AWS 클라우드를 이해하고 의사결정에 참여할 수 있는 깊이 있는 지식을 체계적으로 다룹니다. 각 Chapter는 선수지식 의존 관계에 따라 배치되어 있어, 순서대로 학습하면 개념적 공백 없이 자연스럽게 이해를 쌓아갈 수 있습니다.

**대상 학습자**:
- 클라우드 컴퓨팅을 처음 접하는 완전 초보자
- AWS 자격증 취득을 목표로 하는 IT/비IT 직군 종사자
- 클라우드 기반 프로젝트에 참여하기 위해 기본 소양이 필요한 관리자, 영업, 기획자
- 클라우드 엔지니어링 커리어를 시작하려는 학생

**전체 예상 학습 시간**: 약 70시간 (※ 시험 합격만을 목표로 하는 경우 약 40~50시간으로 압축 가능. 본 커리큘럼은 실무 활용 수준까지 다루는 "마스터 과정"이므로, 시험 범위를 넘어서는 깊이 있는 내용도 포함합니다.)

**선수 과목/지식**: 없음 (컴퓨터와 인터넷의 기본 사용 능력만 필요)

---

## 2. 학습 로드맵 (Learning Roadmap)

### 전체 구조 한눈에 보기

```
📘 AWS Certified Cloud Practitioner 마스터 커리큘럼
│
├── Part 1: 클라우드 컴퓨팅의 이해 (Ch 1~4)
│   ├── Chapter 1:  클라우드 컴퓨팅의 개념과 이점
│   ├── Chapter 2:  클라우드 서비스 모델과 배포 모델
│   ├── Chapter 3:  AWS 소개와 글로벌 인프라
│   └── Chapter 4:  AWS 계정 설정과 관리 콘솔
│
├── Part 2: AWS 핵심 서비스 (Ch 5~11)
│   ├── Chapter 5:  컴퓨팅 서비스
│   ├── Chapter 6:  스토리지 서비스
│   ├── Chapter 7:  네트워킹과 콘텐츠 전송
│   ├── Chapter 8:  데이터베이스 서비스
│   ├── Chapter 9:  컨테이너와 서버리스 아키텍처
│   ├── Chapter 10: 애플리케이션 통합과 메시징 서비스
│   └── Chapter 11: 분석, AI/ML, 기타 서비스
│
├── Part 3: 보안, 자격 증명, 규정 준수 (Ch 12~16)
│   ├── Chapter 12: 공동 책임 모델과 보안 기초
│   ├── Chapter 13: IAM — 자격 증명 및 접근 관리
│   ├── Chapter 14: 네트워크 보안과 데이터 보호
│   ├── Chapter 15: 보안 서비스와 위협 탐지
│   └── Chapter 16: 규정 준수 프로그램과 거버넌스
│
├── Part 4: 클라우드 관리와 운영 (Ch 17~20)
│   ├── Chapter 17: 관리 및 거버넌스 도구
│   ├── Chapter 18: 모니터링, 로깅, 감사
│   ├── Chapter 19: 배포 자동화와 Infrastructure as Code
│   └── Chapter 20: 마이그레이션과 혁신 서비스
│
└── Part 5: 요금, 지원, 아키텍처 설계 원칙 (Ch 21~24)
    ├── Chapter 21: AWS 요금 모델과 비용 최적화
    ├── Chapter 22: 결제 관리와 비용 분석 도구
    ├── Chapter 23: AWS 지원 플랜과 학습 리소스
    └── Chapter 24: Well-Architected Framework와 시험 전략
```

### Chapter 간 선수지식 의존 관계

```
Chapter 1 → Chapter 2   (클라우드 컴퓨팅 기본 개념 필요)
Chapter 2 → Chapter 3   (서비스 모델(IaaS/PaaS/SaaS) 개념 필요)
Chapter 3 → Chapter 4   (AWS 글로벌 인프라, 리전/AZ 개념 필요)
Chapter 4 → Chapter 5   (AWS 콘솔 탐색, 계정 구조 이해 필요)
Chapter 4 → Chapter 6   (AWS 콘솔 탐색, 계정 구조 이해 필요)
Chapter 4 → Chapter 7   (AWS 콘솔 탐색, 계정 구조 이해 필요)
Chapter 5 → Chapter 8   (EC2 인스턴스, 컴퓨팅 개념 필요)
Chapter 6 → Chapter 8   (스토리지 유형, EBS 개념 필요)
Chapter 7 ⇢ Chapter 8   (VPC 개념 참고 — 선택적 의존, 없어도 학습 가능)
Chapter 5 → Chapter 9   (EC2, Lambda 기본 개념 필요)
Chapter 5 → Chapter 10  (컴퓨팅 서비스 개념 필요)
Chapter 6 → Chapter 11  (S3 기반 데이터 레이크 이해 필요)
Chapter 8 → Chapter 11  (데이터베이스 개념 필요)
Chapter 3 → Chapter 12  (AWS 인프라 구조 이해 필요)
Chapter 12 → Chapter 13 (공동 책임 모델, 보안 기초 필요)
Chapter 7 → Chapter 14  (VPC, 서브넷, 네트워크 구조 필요)
Chapter 13 → Chapter 14 (IAM 정책, 접근 제어 개념 필요)
Chapter 13 → Chapter 15 (IAM, 보안 기초 개념 필요)
Chapter 14 → Chapter 15 (네트워크 보안, 암호화 개념 필요)
Chapter 12 → Chapter 16 (공동 책임 모델 이해 필요)
Chapter 13 → Chapter 16 (IAM 정책 개념, SCP 이해에 필요)
Chapter 4 → Chapter 17  (AWS 콘솔, 계정 구조 이해 필요)
Chapter 13 → Chapter 17 (IAM 기본 이해 필요)
Chapter 17 → Chapter 18 (관리 도구 기초 이해 필요)
Chapter 5 → Chapter 19  (EC2, 인프라 자원 개념 필요)
Chapter 3 → Chapter 20  (AWS 글로벌 인프라, 리전 개념 필요)
Chapter 5 → Chapter 20  (컴퓨팅 서비스 개념 필요)
Chapter 6 → Chapter 20  (스토리지 서비스 개념 필요)
Chapter 3 → Chapter 21  (리전, AZ, 서비스 유형 이해 필요)
Chapter 5 → Chapter 21  (EC2 요금 모델 이해 필요)
Chapter 6 → Chapter 21  (S3 요금 구조 이해 필요)
Chapter 21 → Chapter 22 (요금 모델, 비용 개념 필요)
Chapter 16 → Chapter 22 (AWS Organizations, 통합 결제 개념 필요)
Chapter 4 → Chapter 23  (AWS 계정 구조 이해 필요)
Chapter 12 → Chapter 24 (보안 원칙 이해 필요)
Chapter 21 → Chapter 24 (비용 최적화 개념 필요)
Chapter 18 → Chapter 24 (모니터링 개념 필요)
```

**범례**: `→` 필수 의존 (반드시 먼저 학습), `⇢` 선택적 의존 (참고하면 좋으나 건너뛰어도 무방)

**의존 관계가 없는 독립 시작점**: Chapter 1 (사전 지식 없이 시작 가능)

---

## 3. 상세 커리큘럼 (Detailed Curriculum)

---

## Part 1: 클라우드 컴퓨팅의 이해

> 클라우드 컴퓨팅의 근본 개념부터 AWS의 글로벌 인프라, 계정 설정까지 학습합니다. 이 Part를 마치면 "클라우드가 무엇이고, AWS가 어떤 회사이며, 어떻게 시작하는지"를 명확히 설명할 수 있습니다.

---

### Chapter 1: 클라우드 컴퓨팅의 개념과 이점

- **학습 목표**:
  - 클라우드 컴퓨팅의 정의를 자신의 말로 설명할 수 있다
  - 온프레미스와 클라우드 환경의 차이를 비교·분석할 수 있다
  - 클라우드 컴퓨팅의 6가지 이점을 구체적 사례와 함께 설명할 수 있다
  - 클라우드 도입이 비즈니스에 미치는 영향을 논의할 수 있다
- **핵심 키워드**: 클라우드 컴퓨팅, 온프레미스, 온디맨드, 종량제, 탄력성, 확장성, 고가용성, CapEx, OpEx
- **도입 개념**: 클라우드 컴퓨팅, 온프레미스, 온디맨드 셀프서비스, 광범위한 네트워크 접근, 리소스 풀링, 신속한 탄력성, 종량제 과금, 자본 지출(CapEx), 운영 지출(OpEx), 확장성, 고가용성
- **선수 지식**: 없음
- **난이도**: ⭐
- **예상 학습 시간**: 2시간
- **Section 목록**:
  - 1.1 전통적 IT 인프라와 그 한계 — 온프레미스 데이터센터의 구조, 비용, 운영 부담
  - 1.2 클라우드 컴퓨팅의 정의 — NIST 정의 기반 5가지 핵심 특성
  - 1.3 클라우드 컴퓨팅의 6가지 이점 — AWS가 제시하는 클라우드의 비즈니스/기술적 이점
  - 1.4 CapEx vs OpEx — 자본 지출에서 운영 지출로의 전환이 갖는 의미
  - 1.5 클라우드 컴퓨팅의 실제 활용 사례 — 스타트업, 대기업, 공공기관의 도입 사례

---

### Chapter 2: 클라우드 서비스 모델과 배포 모델

- **학습 목표**:
  - IaaS, PaaS, SaaS의 차이를 명확히 구분하고 예시를 들 수 있다
  - 퍼블릭, 프라이빗, 하이브리드 클라우드의 특성과 적합한 사용 시나리오를 설명할 수 있다
  - 특정 비즈니스 요구사항에 적합한 서비스 모델과 배포 모델을 추천할 수 있다
  - 클라우드 서비스 모델별 책임 범위의 차이를 이해할 수 있다
- **핵심 키워드**: IaaS, PaaS, SaaS, 퍼블릭 클라우드, 프라이빗 클라우드, 하이브리드 클라우드, 추상화 수준, 관리 책임
- **도입 개념**: IaaS(Infrastructure as a Service), PaaS(Platform as a Service), SaaS(Software as a Service), 퍼블릭 클라우드, 프라이빗 클라우드, 하이브리드 클라우드, 추상화 수준, 서비스 모델별 관리 책임 경계
- **선수 지식**: Chapter 1 (클라우드 컴퓨팅 기본 개념, 온프레미스 vs 클라우드 차이)
- **난이도**: ⭐
- **예상 학습 시간**: 2시간
- **Section 목록**:
  - 2.1 클라우드 서비스 모델 개요 — IaaS, PaaS, SaaS의 정의와 추상화 수준 비교
  - 2.2 IaaS 심화 — 가상 머신, 네트워크, 스토리지를 직접 관리하는 모델
  - 2.3 PaaS 심화 — 인프라 관리 없이 애플리케이션 개발에 집중하는 모델
  - 2.4 SaaS 심화 — 완성된 소프트웨어를 서비스로 이용하는 모델
  - 2.5 클라우드 배포 모델 — 퍼블릭, 프라이빗, 하이브리드 클라우드의 특성과 선택 기준

---

### Chapter 3: AWS 소개와 글로벌 인프라

- **학습 목표**:
  - AWS의 역사와 시장 내 위치를 설명할 수 있다
  - 리전, 가용 영역, 엣지 로케이션의 개념과 관계를 도식화하여 설명할 수 있다
  - 리전 선택 시 고려해야 할 4가지 요소를 열거하고 적용할 수 있다
  - AWS 서비스의 범위와 카테고리를 개괄적으로 파악할 수 있다
- **핵심 키워드**: AWS, 리전, 가용 영역(AZ), 엣지 로케이션, Local Zones, Wavelength, Outposts, 데이터 레지던시, 지연 시간, 서비스 가용성, AWS 글로벌 인프라
- **도입 개념**: AWS(Amazon Web Services), 리전(Region), 가용 영역(Availability Zone), 엣지 로케이션(Edge Location), AWS Local Zones, AWS Wavelength, AWS Outposts, 데이터 레지던시, 리전 선택 기준(규정 준수, 지연 시간, 서비스 가용성, 비용), AWS 서비스 카테고리
- **선수 지식**: Chapter 2 (IaaS/PaaS/SaaS 서비스 모델 이해)
- **난이도**: ⭐
- **예상 학습 시간**: 2.5시간
- **Section 목록**:
  - 3.1 AWS의 역사와 시장 위치 — AWS의 탄생 배경, 성장, 클라우드 시장 점유율
  - 3.2 리전과 가용 영역 — 글로벌 인프라의 핵심 구성 요소와 고가용성 설계
  - 3.3 엣지 로케이션과 글로벌 네트워크 — CDN, 엣지 컴퓨팅, AWS 전용 네트워크
  - 3.4 Local Zones, Wavelength, Outposts — 리전 외부로 AWS를 확장하는 인프라 옵션
  - 3.5 리전 선택 전략 — 규정 준수, 지연 시간, 비용, 서비스 가용성 기반 의사결정
  - 3.6 AWS 서비스 카테고리 개요 — 200개 이상의 서비스를 기능별로 분류하여 조망

---

### Chapter 4: AWS 계정 설정과 관리 콘솔

- **학습 목표**:
  - AWS 계정을 생성하고 기본 보안 설정(MFA)을 적용할 수 있다
  - AWS Management Console의 주요 인터페이스를 탐색할 수 있다
  - AWS CLI와 SDK의 역할과 사용 시나리오를 구분할 수 있다
  - 프리 티어의 범위와 한계를 이해하고 비용 발생을 방지할 수 있다
- **핵심 키워드**: AWS 계정, 루트 사용자, MFA, AWS Management Console, AWS CLI, AWS SDK, 프리 티어, AWS CloudShell
- **도입 개념**: AWS 계정, 루트 사용자, MFA(다중 인증), AWS Management Console, AWS CLI(Command Line Interface), AWS SDK(Software Development Kit), AWS 프리 티어, AWS CloudShell
- **선수 지식**: Chapter 3 (AWS 글로벌 인프라, 리전/AZ 개념)
- **난이도**: ⭐
- **예상 학습 시간**: 2.5시간
- **Section 목록**:
  - 4.1 AWS 계정 생성 — 계정 생성 절차, 루트 사용자의 역할과 보안 위험
  - 4.2 MFA와 초기 보안 설정 — 다중 인증 설정, 루트 사용자 보호 모범 사례
  - 4.3 AWS Management Console 탐색 — 서비스 검색, 리전 전환, 대시보드 활용
  - 4.4 AWS CLI와 CloudShell — 명령줄 인터페이스를 통한 AWS 서비스 접근
  - 4.5 AWS 프리 티어 활용과 비용 관리 — 프리 티어의 3가지 유형, 예기치 않은 비용 방지

---

## Part 2: AWS 핵심 서비스

> AWS의 핵심 서비스군(컴퓨팅, 스토리지, 네트워킹, 데이터베이스 등)을 체계적으로 학습합니다. 각 서비스의 개념, 용도, 차이점을 명확히 이해하여 적절한 서비스를 선택할 수 있는 능력을 기릅니다.

---

### Chapter 5: 컴퓨팅 서비스

- **학습 목표**:
  - EC2 인스턴스의 개념과 인스턴스 유형 패밀리를 분류할 수 있다
  - EC2 구매 옵션(온디맨드, 예약, 스팟 등)의 차이와 적합한 사용 시나리오를 설명할 수 있다
  - AWS Lambda의 서버리스 개념과 이벤트 기반 실행 모델을 설명할 수 있다
  - Elastic Beanstalk, Lightsail 등 추가 컴퓨팅 서비스의 역할을 구분할 수 있다
- **핵심 키워드**: EC2, 인스턴스 유형, AMI, 온디맨드, 예약 인스턴스, 스팟 인스턴스, Savings Plans, Lambda, 서버리스, Elastic Beanstalk, Lightsail
- **도입 개념**: EC2(Elastic Compute Cloud), 인스턴스, 인스턴스 유형 패밀리, AMI(Amazon Machine Image), 온디맨드 인스턴스, 예약 인스턴스, 스팟 인스턴스, Savings Plans, 전용 호스트, AWS Lambda, 서버리스 컴퓨팅, 이벤트 기반 실행, Elastic Beanstalk, Amazon Lightsail, AWS Batch, Auto Scaling 기초
- **선수 지식**: Chapter 4 (AWS 콘솔 탐색, 계정 구조, 프리 티어 이해)
- **난이도**: ⭐⭐
- **예상 학습 시간**: 3.5시간
- **Section 목록**:
  - 5.1 Amazon EC2 개요 — 가상 서버의 개념, 인스턴스 생명주기
  - 5.2 EC2 인스턴스 유형과 선택 — 범용, 컴퓨팅 최적화, 메모리 최적화 등 패밀리 분류
  - 5.3 AMI와 인스턴스 시작 — Amazon Machine Image의 개념과 인스턴스 구성
  - 5.4 EC2 구매 옵션 — 온디맨드, 예약, 스팟, Savings Plans, 전용 호스트 비교
  - 5.5 AWS Lambda와 서버리스 컴퓨팅 — 서버 관리 없는 코드 실행, 이벤트 기반 아키텍처
  - 5.6 기타 컴퓨팅 서비스 — Elastic Beanstalk, Lightsail, AWS Batch, Outposts 개요
  - 5.7 Auto Scaling 기초 — 수요에 따른 자동 확장/축소 개념 (→ ELB와의 연동은 Ch 7.6에서 다룸)

---

### Chapter 6: 스토리지 서비스

- **학습 목표**:
  - S3의 객체 스토리지 개념과 스토리지 클래스를 구분할 수 있다
  - EBS, EFS, FSx의 차이점과 적합한 사용 시나리오를 설명할 수 있다
  - S3 버킷 정책과 접근 제어의 기본 원리를 이해할 수 있다
  - 데이터 백업 및 아카이빙 전략에 적합한 스토리지 서비스를 선택할 수 있다
- **핵심 키워드**: S3, 객체 스토리지, 버킷, 스토리지 클래스, S3 Glacier, EBS, EFS, 블록 스토리지, 파일 스토리지, AWS Backup, AWS Storage Gateway
- **도입 개념**: Amazon S3(Simple Storage Service), 객체 스토리지, 버킷, 객체, S3 스토리지 클래스(Standard, IA, One Zone-IA, Glacier, Glacier Deep Archive, Intelligent-Tiering), 블록 스토리지, EBS(Elastic Block Store), EBS 스냅샷, 파일 스토리지, EFS(Elastic File System), Amazon FSx, AWS Backup, AWS Storage Gateway, S3 버전 관리, S3 수명 주기 정책
- **선수 지식**: Chapter 4 (AWS 콘솔 탐색, 계정 구조 이해)
- **난이도**: ⭐⭐
- **예상 학습 시간**: 3.5시간
- **Section 목록**:
  - 6.1 스토리지 유형 비교 — 객체, 블록, 파일 스토리지의 개념과 차이
  - 6.2 Amazon S3 기초 — 버킷, 객체, 키, 무제한 확장성
  - 6.3 S3 스토리지 클래스와 수명 주기 — 비용과 접근 빈도에 따른 클래스 선택 전략
  - 6.4 S3 보안과 접근 제어 — 버킷 정책, ACL, 퍼블릭 접근 차단
  - 6.5 Amazon EBS — EC2에 연결되는 블록 스토리지, 볼륨 유형, 스냅샷
  - 6.6 Amazon EFS와 FSx — 공유 파일 시스템, 관리형 파일 스토리지
  - 6.7 AWS Backup과 데이터 보호 — 중앙 집중식 백업 관리, 백업 정책
  - 6.8 하이브리드 스토리지와 데이터 전송 — Storage Gateway, Snow Family 개요 (→ Snow Family 마이그레이션 관점은 Ch 20.5에서 심화)

---

### Chapter 7: 네트워킹과 콘텐츠 전송

- **학습 목표**:
  - VPC의 구성 요소(서브넷, 라우팅 테이블, 게이트웨이)를 설명할 수 있다
  - 퍼블릭 서브넷과 프라이빗 서브넷의 차이와 설계 의도를 이해할 수 있다
  - Route 53의 DNS 서비스 역할과 라우팅 정책을 설명할 수 있다
  - CloudFront의 CDN 개념과 콘텐츠 전송 최적화 원리를 이해할 수 있다
- **핵심 키워드**: VPC, 서브넷, 인터넷 게이트웨이, NAT 게이트웨이, 라우팅 테이블, VPC Endpoints, PrivateLink, Route 53, CloudFront, Global Accelerator, CDN, Direct Connect, VPN, Elastic Load Balancing
- **도입 개념**: VPC(Virtual Private Cloud), 서브넷, 퍼블릭 서브넷, 프라이빗 서브넷, 인터넷 게이트웨이(IGW), NAT 게이트웨이, 라우팅 테이블, CIDR 블록, 탄력적 IP, VPC Endpoints(Gateway/Interface), AWS PrivateLink, Route 53, DNS, CloudFront, CDN(Content Delivery Network), AWS Global Accelerator, AWS Direct Connect, Site-to-Site VPN, VPC 피어링, Elastic Load Balancing(ELB), Transit Gateway
- **선수 지식**: Chapter 4 (AWS 콘솔 탐색, 계정 구조 이해)
- **난이도**: ⭐⭐⭐
- **예상 학습 시간**: 4시간
- **Section 목록**:
  - 7.1 네트워킹 기초 개념 — IP 주소, CIDR, DNS, HTTP/HTTPS 기본 (※ CCP 수준에서는 개념 이해 중심, CIDR 계산 등 세부사항은 SAA 대비용)
  - 7.2 Amazon VPC 핵심 구성 — VPC 생성, 서브넷, 인터넷 게이트웨이, 라우팅 테이블
  - 7.3 퍼블릭 vs 프라이빗 서브넷 — NAT 게이트웨이, 네트워크 계층 설계
  - 7.4 VPC 연결 옵션 — VPC 피어링, Transit Gateway, VPN, Direct Connect
  - 7.5 VPC Endpoints와 AWS PrivateLink — 프라이빗 네트워크를 통한 AWS 서비스 접근
  - 7.6 Elastic Load Balancing — ALB, NLB를 활용한 트래픽 분산, Auto Scaling과의 연동 (← Ch 5.7 참조)
  - 7.7 Amazon Route 53 — DNS 서비스, 도메인 등록, 라우팅 정책
  - 7.8 Amazon CloudFront와 Global Accelerator — CDN, 글로벌 네트워크 가속화

---

### Chapter 8: 데이터베이스 서비스

- **학습 목표**:
  - 관계형 데이터베이스와 비관계형 데이터베이스의 차이를 설명할 수 있다
  - RDS, Aurora, DynamoDB, ElastiCache 등 AWS 데이터베이스 서비스를 구분할 수 있다
  - 워크로드 특성에 따라 적합한 데이터베이스 서비스를 추천할 수 있다
  - 관리형 데이터베이스의 이점과 자체 관리 대비 장점을 설명할 수 있다
- **핵심 키워드**: RDS, Aurora, DynamoDB, ElastiCache, Redshift, 관계형 DB, 비관계형 DB, 관리형 서비스, Multi-AZ, 읽기 전용 복제본
- **도입 개념**: 관계형 데이터베이스, 비관계형(NoSQL) 데이터베이스, Amazon RDS(Relational Database Service), Amazon Aurora, Aurora Serverless, Multi-AZ 배포, 읽기 전용 복제본(Read Replica), Amazon DynamoDB, 키-값 스토어, Amazon ElastiCache, 인메모리 캐시, Amazon Redshift, 데이터 웨어하우스, Amazon DocumentDB, Amazon Neptune, Amazon QLDB, Amazon DMS(Database Migration Service), AWS SCT(Schema Conversion Tool)
- **선수 지식**: Chapter 5 (EC2 인스턴스, 컴퓨팅 개념), Chapter 6 (스토리지 유형, EBS 개념). ※ Chapter 7 (VPC 개념)은 참고하면 좋으나 필수는 아님
- **난이도**: ⭐⭐
- **예상 학습 시간**: 3시간
- **Section 목록**:
  - 8.1 데이터베이스 기초 개념 — 관계형 vs 비관계형 데이터베이스, SQL vs NoSQL
  - 8.2 Amazon RDS — 관리형 관계형 데이터베이스, 지원 엔진, Multi-AZ, 읽기 전용 복제본
  - 8.3 Amazon Aurora — 클라우드 네이티브 관계형 데이터베이스, RDS와의 차이, Aurora Serverless
  - 8.4 Amazon DynamoDB — 완전 관리형 NoSQL, 키-값 및 문서 모델
  - 8.5 캐싱과 특수 목적 데이터베이스 — ElastiCache, Redshift, Neptune, DocumentDB, QLDB
  - 8.6 데이터베이스 마이그레이션 — AWS DMS를 활용한 데이터베이스 이전, AWS SCT(Schema Conversion Tool)를 통한 스키마 변환

---

### Chapter 9: 컨테이너와 서버리스 아키텍처

- **학습 목표**:
  - 컨테이너의 개념과 가상 머신과의 차이를 설명할 수 있다
  - ECS, EKS, Fargate의 역할과 차이를 구분할 수 있다
  - 서버리스 아키텍처의 구성 요소와 장점을 설명할 수 있다
  - API Gateway와 Lambda를 연동한 서버리스 패턴을 이해할 수 있다
- **핵심 키워드**: 컨테이너, Docker, ECS, EKS, Fargate, ECR, App Runner, API Gateway, Step Functions, 서버리스 아키텍처
- **도입 개념**: 컨테이너, Docker, 컨테이너 이미지, Amazon ECS(Elastic Container Service), Amazon EKS(Elastic Kubernetes Service), AWS Fargate, AWS App Runner, Amazon ECR(Elastic Container Registry), Amazon API Gateway, AWS Step Functions, 서버리스 아키텍처 패턴
- **선수 지식**: Chapter 5 (EC2, Lambda 기본 개념)
- **난이도**: ⭐⭐
- **예상 학습 시간**: 2.5시간
- **Section 목록**:
  - 9.1 컨테이너 기초 — 컨테이너 vs 가상 머신, Docker의 핵심 개념
  - 9.2 Amazon ECS와 ECR — AWS의 컨테이너 오케스트레이션 서비스
  - 9.3 Amazon EKS — Kubernetes 기반 컨테이너 관리
  - 9.4 AWS Fargate와 App Runner — 서버리스 컨테이너 실행 환경, 간소화된 컨테이너 배포
  - 9.5 Amazon API Gateway — RESTful API 생성 및 관리
  - 9.6 AWS Step Functions과 서버리스 아키텍처 — 워크플로 오케스트레이션, 서버리스 패턴 설계

---

### Chapter 10: 애플리케이션 통합과 메시징 서비스

- **학습 목표**:
  - 느슨한 결합(Loose Coupling)의 개념과 중요성을 설명할 수 있다
  - SQS, SNS, EventBridge의 차이와 사용 시나리오를 구분할 수 있다
  - 메시징 기반 아키텍처의 이점(확장성, 내결함성)을 설명할 수 있다
  - 적절한 통합 서비스를 선택하여 시스템 아키텍처를 설계할 수 있다
- **핵심 키워드**: SQS, SNS, EventBridge, 메시지 큐, Pub/Sub, 느슨한 결합, 디커플링, Amazon MQ, Amazon Kinesis, Amazon SES, Amazon Pinpoint
- **도입 개념**: 느슨한 결합(Loose Coupling), 디커플링, Amazon SQS(Simple Queue Service), 메시지 큐, Amazon SNS(Simple Notification Service), Pub/Sub 패턴, 토픽, 구독, Amazon EventBridge, 이벤트 버스, Amazon MQ, Amazon Kinesis, 실시간 데이터 스트리밍, Amazon SES(Simple Email Service), Amazon Pinpoint
- **선수 지식**: Chapter 5 (컴퓨팅 서비스 개념)
- **난이도**: ⭐⭐
- **예상 학습 시간**: 3시간
- **Section 목록**:
  - 10.1 긴밀한 결합 vs 느슨한 결합 — 모놀리식 vs 마이크로서비스, 디커플링의 가치
  - 10.2 Amazon SQS — 메시지 큐, 표준 대기열 vs FIFO 대기열
  - 10.3 Amazon SNS — 알림 서비스, 토픽 기반 Pub/Sub 메시징
  - 10.4 Amazon EventBridge — 이벤트 기반 아키텍처, 이벤트 버스와 규칙
  - 10.5 Amazon Kinesis와 MQ — 실시간 데이터 스트리밍, 레거시 메시지 브로커 호환
  - 10.6 Amazon SES와 Pinpoint — 이메일 전송 서비스, 마케팅 커뮤니케이션 플랫폼

---

### Chapter 11: 분석, AI/ML, 기타 서비스

- **학습 목표**:
  - AWS의 주요 데이터 분석 서비스(Athena, Glue, EMR 등)의 역할을 구분할 수 있다
  - AWS의 AI/ML 서비스 계층(사전 구축, 플랫폼, 프레임워크)을 설명할 수 있다
  - Rekognition, Comprehend, SageMaker AI 등의 활용 사례를 설명할 수 있다
  - AWS의 IoT, 블록체인 등 추가 서비스 카테고리를 인지할 수 있다
- **핵심 키워드**: Athena, Glue, EMR, QuickSight, SageMaker AI, Rekognition, Comprehend, Polly, Transcribe, Translate, Textract, Lex, Kendra, WorkSpaces, AppStream 2.0, Connect, IoT Core
- **도입 개념**: Amazon Athena, AWS Glue, Amazon EMR, Amazon QuickSight, 데이터 레이크, AWS Data Exchange, Amazon SageMaker AI, Amazon Rekognition, Amazon Comprehend, Amazon Polly, Amazon Transcribe, Amazon Translate, Amazon Textract, Amazon Lex, Amazon Kendra, Amazon Bedrock, 파운데이션 모델(FM), 생성형 AI, Amazon Connect, Amazon WorkSpaces, Amazon AppStream 2.0, AWS IoT Core, AWS IoT Greengrass, Amazon Managed Blockchain, Amazon Q, AWS AppSync
- **선수 지식**: Chapter 6 (S3 기반 데이터 레이크 이해), Chapter 8 (데이터베이스 개념)
- **난이도**: ⭐⭐
- **예상 학습 시간**: 3.5시간
- **Section 목록**:
  - 11.1 데이터 분석 서비스 개요 — Athena, Glue, EMR, QuickSight의 역할과 관계
  - 11.2 데이터 레이크와 분석 파이프라인 — S3 기반 데이터 레이크 아키텍처, AWS Data Exchange
  - 11.3 AWS AI/ML 서비스 계층 — 사전 구축 AI, ML 플랫폼, 프레임워크 계층 분류
  - 11.4 주요 AI/ML 서비스 — Rekognition, Comprehend, Polly, Transcribe, Translate, Textract, Lex, SageMaker AI
  - 11.5 Amazon Bedrock과 생성형 AI — 파운데이션 모델 접근, 생성형 AI 서비스의 개념과 활용 (※ Bedrock은 CLF-C02 시험 범위 밖이나 실무 이해를 위해 포함. 시험 대비 시 Amazon Q에 집중)
  - 11.6 최종 사용자 컴퓨팅과 비즈니스 서비스 — WorkSpaces, AppStream 2.0, Amazon Connect 개요
  - 11.7 Amazon Q, IoT, 기타 서비스 — Amazon Q, IoT Core, IoT Greengrass, AWS AppSync(GraphQL API 관리), 블록체인 서비스 개요

---

## Part 3: 보안, 자격 증명, 규정 준수

> AWS 보안의 핵심인 공동 책임 모델부터 IAM, 네트워크 보안, 보안 서비스, 규정 준수까지 체계적으로 학습합니다. 시험 출제 비중이 가장 높은(30%) 영역입니다.

---

### Chapter 12: 공동 책임 모델과 보안 기초

- **학습 목표**:
  - AWS 공동 책임 모델에서 AWS와 고객 각각의 보안 책임 범위를 명확히 구분할 수 있다
  - 서비스 유형(IaaS, PaaS, SaaS)에 따라 책임 경계가 어떻게 달라지는지 설명할 수 있다
  - AWS의 물리적 보안과 인프라 보안 조치를 설명할 수 있다
  - 보안 설계의 기본 원칙(최소 권한, 심층 방어)을 이해할 수 있다
- **핵심 키워드**: 공동 책임 모델, AWS 책임, 고객 책임, 최소 권한 원칙, 심층 방어, 물리적 보안, 인프라 보안
- **도입 개념**: 공동 책임 모델(Shared Responsibility Model), "클라우드의 보안" vs "클라우드에서의 보안", 최소 권한 원칙(Principle of Least Privilege), 심층 방어(Defense in Depth), AWS 물리적 보안, 인프라 보호 계층, 상속된 제어(Inherited Controls), 공유된 제어(Shared Controls)
- **선수 지식**: Chapter 3 (AWS 인프라 구조 이해)
- **난이도**: ⭐⭐
- **예상 학습 시간**: 2.5시간
- **Section 목록**:
  - 12.1 공동 책임 모델 개요 — "클라우드의 보안"과 "클라우드에서의 보안" 구분
  - 12.2 AWS의 보안 책임 — 물리적 인프라, 하이퍼바이저, 관리형 서비스 보안
  - 12.3 고객의 보안 책임 — 데이터, 운영체제, 네트워크 구성, 접근 관리
  - 12.4 서비스별 책임 변화 — EC2 vs RDS vs Lambda에서의 책임 경계 비교
  - 12.5 보안 설계 원칙 — 최소 권한, 심층 방어, 자동화, 추적 가능성

---

### Chapter 13: IAM — 자격 증명 및 접근 관리

- **학습 목표**:
  - IAM 사용자, 그룹, 역할, 정책의 개념과 관계를 설명할 수 있다
  - IAM 정책의 JSON 구조를 읽고 해석할 수 있다
  - IAM 역할의 사용 시나리오(EC2 역할, 교차 계정 접근 등)를 설명할 수 있다
  - IAM 보안 모범 사례를 열거하고 적용할 수 있다
  - IAM Identity Center(SSO)의 개념과 활용을 이해할 수 있다
- **핵심 키워드**: IAM, IAM 사용자, IAM 그룹, IAM 역할, IAM 정책, JSON 정책, ARN, 접근 키, MFA, IAM Identity Center, 자격 증명 연동
- **도입 개념**: IAM(Identity and Access Management), IAM 사용자, IAM 그룹, IAM 역할, IAM 정책, 관리형 정책(AWS/고객), 인라인 정책, JSON 정책 구조(Effect, Action, Resource), ARN(Amazon Resource Name), 접근 키(Access Key), IAM Identity Center(AWS SSO), 자격 증명 연동(Federation), 임시 보안 자격 증명, AWS STS, AWS Resource Access Manager(RAM)
- **선수 지식**: Chapter 12 (공동 책임 모델, 보안 기초, 최소 권한 원칙)
- **난이도**: ⭐⭐⭐
- **예상 학습 시간**: 3.5시간
- **Section 목록**:
  - 13.1 IAM 개요 — 글로벌 서비스, 인증과 인가의 차이
  - 13.2 IAM 사용자와 그룹 — 사용자 생성, 그룹 기반 권한 관리
  - 13.3 IAM 정책 심화 — JSON 정책 구조, Effect/Action/Resource, 정책 평가 로직
  - 13.4 IAM 역할 — 역할의 개념, EC2 역할, 교차 계정 접근, 서비스 연결 역할
  - 13.5 IAM Identity Center — 다중 계정 환경에서의 SSO, 자격 증명 연동
  - 13.6 AWS Resource Access Manager — 계정 간 리소스 공유, RAM의 역할과 활용
  - 13.7 IAM 보안 모범 사례 — 루트 계정 보호, MFA 적용, 접근 키 관리, 정기 감사

---

### Chapter 14: 네트워크 보안과 데이터 보호

- **학습 목표**:
  - 보안 그룹과 네트워크 ACL의 차이를 비교하고 적절히 구성할 수 있다
  - 전송 중 암호화와 저장 시 암호화의 차이를 설명할 수 있다
  - AWS KMS, CloudHSM, ACM의 역할을 구분할 수 있다
  - AWS WAF, Shield의 역할과 DDoS 보호 전략을 설명할 수 있다
- **핵심 키워드**: 보안 그룹, 네트워크 ACL, 상태 유지/비유지 방화벽, KMS, CloudHSM, ACM, SSL/TLS, 암호화, WAF, Shield, AWS Firewall Manager
- **도입 개념**: 보안 그룹(Security Group), 네트워크 ACL(Network Access Control List), 상태 유지 방화벽(Stateful), 상태 비유지 방화벽(Stateless), 인바운드/아웃바운드 규칙, 전송 중 암호화(Encryption in Transit), 저장 시 암호화(Encryption at Rest), AWS KMS(Key Management Service), CMK(Customer Managed Key), CloudHSM, AWS Certificate Manager(ACM), SSL/TLS, AWS WAF(Web Application Firewall), AWS Shield(Standard/Advanced), DDoS 보호, AWS Firewall Manager
- **선수 지식**: Chapter 7 (VPC, 서브넷, 네트워크 구조), Chapter 13 (IAM 정책, 접근 제어 개념)
- **난이도**: ⭐⭐⭐
- **예상 학습 시간**: 3.5시간
- **Section 목록**:
  - 14.1 네트워크 보안 계층 — 보안 그룹과 네트워크 ACL의 비교, 상태 유지 vs 비유지
  - 14.2 보안 그룹 심화 — 인바운드/아웃바운드 규칙, 보안 그룹 참조
  - 14.3 네트워크 ACL 심화 — 서브넷 수준 방화벽, 규칙 번호와 평가 순서
  - 14.4 데이터 암호화 기초 — 전송 중 암호화(SSL/TLS)와 저장 시 암호화
  - 14.5 AWS KMS와 CloudHSM — 키 관리 서비스, 고객 관리 키, 하드웨어 보안 모듈
  - 14.6 AWS WAF와 Shield — 웹 애플리케이션 방화벽, DDoS 보호 전략
  - 14.7 AWS Firewall Manager와 네트워크 방화벽 — 중앙 집중식 방화벽 관리

---

### Chapter 15: 보안 서비스와 위협 탐지

- **학습 목표**:
  - GuardDuty, Inspector, Macie의 역할과 차이를 구분할 수 있다
  - AWS Security Hub를 통한 보안 상태 통합 관리 방법을 설명할 수 있다
  - Detective, Secrets Manager, Systems Manager Parameter Store의 역할을 이해할 수 있다
  - AWS의 보안 서비스를 조합하여 다층 보안 전략을 수립할 수 있다
- **핵심 키워드**: GuardDuty, Inspector, Macie, Security Hub, Detective, Secrets Manager, Parameter Store, 침입 탐지, 취약점 분석
- **도입 개념**: Amazon GuardDuty, 위협 탐지, Amazon Inspector, 취약점 평가, Amazon Macie, 민감 데이터 탐지, AWS Security Hub, 보안 상태 관리, Amazon Detective, 보안 조사, AWS Secrets Manager, AWS Systems Manager Parameter Store, 보안 자동화
- **선수 지식**: Chapter 13 (IAM, 보안 기초 개념), Chapter 14 (네트워크 보안, 암호화 개념)
- **난이도**: ⭐⭐⭐
- **예상 학습 시간**: 3시간
- **Section 목록**:
  - 15.1 Amazon GuardDuty — 지능형 위협 탐지, 이상 행동 분석
  - 15.2 Amazon Inspector — EC2, Lambda, 컨테이너 취약점 자동 평가
  - 15.3 Amazon Macie — S3 데이터에서 민감 정보(PII 등) 자동 탐지
  - 15.4 AWS Security Hub — 보안 발견 사항 통합, 보안 표준 점검
  - 15.5 Amazon Detective와 보안 조사 — 보안 이벤트의 근본 원인 분석
  - 15.6 비밀 정보 관리 — Secrets Manager, Parameter Store를 활용한 자격 증명 관리

---

### Chapter 16: 규정 준수 프로그램과 거버넌스

- **학습 목표**:
  - AWS의 주요 규정 준수 프로그램(SOC, ISO, HIPAA 등)을 열거할 수 있다
  - AWS Config, CloudTrail의 역할과 거버넌스에서의 중요성을 설명할 수 있다
  - AWS Organizations와 SCP를 활용한 다중 계정 거버넌스 전략을 이해할 수 있다
  - 규정 준수와 감사 요구사항에 대응하는 AWS 서비스 조합을 추천할 수 있다
- **핵심 키워드**: 규정 준수, SOC, ISO, HIPAA, GDPR, AWS Config, CloudTrail, AWS Organizations, SCP, Control Tower, AWS Audit Manager, AWS Artifact
- **도입 개념**: 규정 준수(Compliance), SOC 보고서, ISO 27001, HIPAA, GDPR, PCI DSS, AWS Artifact, 규정 준수 보고서, AWS Config, 구성 규칙, AWS CloudTrail, API 활동 로깅, AWS Organizations, 서비스 제어 정책(SCP), AWS Control Tower, 랜딩 존, AWS Audit Manager, 감사 자동화
- **선수 지식**: Chapter 12 (공동 책임 모델 이해), Chapter 13 (IAM 정책, SCP 관련 개념)
- **난이도**: ⭐⭐
- **예상 학습 시간**: 3시간
- **Section 목록**:
  - 16.1 AWS 규정 준수 프로그램과 Artifact — SOC, ISO, HIPAA, GDPR, PCI DSS 등 주요 인증, AWS Artifact를 통한 보고서 접근
  - 16.2 AWS Config — 리소스 구성 기록, 변경 추적, 규정 준수 규칙 평가 (거버넌스 관점 소개)
  - 16.3 AWS CloudTrail 소개 — API 호출 기록의 개념과 감사에서의 역할 (심화는 Ch 18에서)
  - 16.4 AWS Organizations와 SCP — 다중 계정 관리, 서비스 제어 정책, OU 구조
  - 16.5 AWS Control Tower — 자동화된 랜딩 존 설정, 가드레일
  - 16.6 AWS Audit Manager — 감사 증거 자동 수집, 규정 준수 보고

---

## Part 4: 클라우드 관리와 운영

> AWS 리소스를 효율적으로 관리, 모니터링, 배포하는 방법과 온프레미스에서 클라우드로의 마이그레이션 전략을 학습합니다.

---

### Chapter 17: 관리 및 거버넌스 도구

- **학습 목표**:
  - AWS Systems Manager의 주요 기능과 활용 사례를 설명할 수 있다
  - AWS Trusted Advisor의 6가지 점검 카테고리를 열거하고 활용할 수 있다
  - AWS Health Dashboard와 Personal Health Dashboard의 차이를 설명할 수 있다
  - 태그 기반 리소스 관리 전략을 수립할 수 있다
- **핵심 키워드**: Systems Manager, Trusted Advisor, Health Dashboard, 태그, Resource Groups, License Manager, Service Catalog
- **도입 개념**: AWS Systems Manager, Session Manager, Patch Manager, AWS Trusted Advisor, 6가지 점검 카테고리(비용 최적화, 성능, 복원력, 보안, 운영 우수성, 서비스 한도), AWS Health Dashboard, Personal Health Dashboard, 태그(Tag), 태그 기반 관리, Resource Groups, AWS Service Catalog, AWS License Manager
- **선수 지식**: Chapter 4 (AWS 콘솔, 계정 구조 이해), Chapter 13 (IAM 기본 이해)
- **난이도**: ⭐⭐
- **예상 학습 시간**: 2.5시간
- **Section 목록**:
  - 17.1 AWS Systems Manager — 인프라 운영 허브, Session Manager, Patch Manager
  - 17.2 AWS Trusted Advisor — 6가지 카테고리(비용 최적화, 성능, 복원력, 보안, 운영 우수성, 서비스 한도) 모범 사례 점검, 지원 플랜별 차이
  - 17.3 AWS Health Dashboard — 서비스 상태 확인, 개인화된 이벤트 알림
  - 17.4 태그와 리소스 관리 — 태그 전략, Resource Groups, 비용 할당 태그
  - 17.5 Service Catalog와 License Manager — 승인된 제품 관리, 라이선스 추적

---

### Chapter 18: 모니터링, 로깅, 감사

- **학습 목표**:
  - CloudWatch의 지표, 경보, 대시보드, 로그 기능을 활용할 수 있다
  - CloudTrail과 CloudWatch Logs의 차이와 보완 관계를 설명할 수 있다
  - EventBridge를 활용한 이벤트 기반 자동화 시나리오를 설명할 수 있다
  - X-Ray를 통한 분산 시스템 추적의 개념을 이해할 수 있다
- **핵심 키워드**: CloudWatch, CloudWatch Logs, CloudWatch Alarms, CloudTrail, EventBridge, X-Ray, 지표, 경보, 대시보드, 관측 가능성
- **도입 개념**: Amazon CloudWatch, CloudWatch 지표(Metrics), CloudWatch 경보(Alarms), CloudWatch 대시보드, CloudWatch Logs, 로그 그룹, CloudWatch Events/EventBridge 연동, AWS X-Ray, 분산 추적, 관측 가능성(Observability), CloudWatch Insights
- **선수 지식**: Chapter 17 (관리 도구 기초 이해)
- **난이도**: ⭐⭐
- **예상 학습 시간**: 3시간
- **Section 목록**:
  - 18.1 Amazon CloudWatch 지표 — 기본 지표, 사용자 정의 지표, 지표 수집 주기
  - 18.2 CloudWatch 경보와 대시보드 — 경보 생성, SNS 연동, 시각화 대시보드
  - 18.3 CloudWatch Logs — 로그 수집, 로그 그룹, 로그 인사이트 쿼리
  - 18.4 CloudTrail 심화 — 관리 이벤트, 데이터 이벤트, 다중 리전 설정
  - 18.5 AWS X-Ray — 마이크로서비스 분산 추적, 서비스 맵
  - 18.6 관측 가능성 통합 — CloudWatch, CloudTrail, X-Ray의 역할 조합

---

### Chapter 19: 배포 자동화와 Infrastructure as Code

- **학습 목표**:
  - CloudFormation의 IaC 개념과 템플릿 기반 인프라 관리의 이점을 설명할 수 있다
  - CDK, SAM의 역할과 CloudFormation과의 관계를 이해할 수 있다
  - CodeBuild, CodeDeploy, CodePipeline의 CI/CD 파이프라인 역할을 구분할 수 있다
  - 인프라 자동화의 이점(반복 가능성, 일관성, 버전 관리)을 설명할 수 있다
- **핵심 키워드**: CloudFormation, IaC, 스택, 템플릿, CDK, SAM, CodeBuild, CodePipeline, CI/CD, CodeDeploy(참고)
- **도입 개념**: AWS CloudFormation, Infrastructure as Code(IaC), 스택(Stack), 템플릿(Template), AWS CDK(Cloud Development Kit), AWS SAM(Serverless Application Model), AWS CodeBuild, AWS CodePipeline, CI/CD(지속적 통합/지속적 배포), AWS CodeDeploy(시험 범위 밖, 참고용)
- **선수 지식**: Chapter 5 (EC2, 인프라 자원 개념)
- **난이도**: ⭐⭐
- **예상 학습 시간**: 2.5시간
- **Section 목록**:
  - 19.1 Infrastructure as Code 개요 — IaC의 개념, 수동 관리 대비 장점
  - 19.2 AWS CloudFormation — 템플릿 구조, 스택 생성/업데이트/삭제, 드리프트 탐지
  - 19.3 AWS CDK와 SAM — 프로그래밍 언어 기반 IaC, 서버리스 전용 프레임워크
  - 19.4 CI/CD 파이프라인 — CodeBuild의 역할, CodePipeline과의 연동 (※ CodeDeploy는 CLF-C02 시험 범위 밖이나 CI/CD 이해를 위해 개념만 소개)
  - 19.5 AWS CodePipeline — 완전 관리형 CI/CD 오케스트레이션
  - 19.6 추가 개발자 도구 — AWS Amplify(웹/모바일 앱 배포, 시험 범위), AWS Cloud9, CodeArtifact 개요

---

### Chapter 20: 마이그레이션과 혁신 서비스

- **학습 목표**:
  - AWS CAF(Cloud Adoption Framework)의 6가지 관점을 설명할 수 있다
  - 6R 마이그레이션 전략을 구분하고 시나리오에 적용할 수 있다
  - AWS Migration Hub, DMS, MGN 등 마이그레이션 도구의 역할을 구분할 수 있다
  - Snow Family 디바이스의 종류와 사용 시나리오를 설명할 수 있다
- **핵심 키워드**: AWS CAF, 6R 전략, Migration Hub, DMS, MGN(Application Migration Service), Snow Family, Snowball Edge, Snowcone, Application Discovery Service, AWS Transfer Family
- **도입 개념**: AWS Cloud Adoption Framework(CAF), 6가지 관점(비즈니스, 사람, 거버넌스, 플랫폼, 보안, 운영), 6R 마이그레이션 전략(Rehost, Replatform, Refactor, Repurchase, Retain, Retire), AWS Migration Hub, AWS Application Discovery Service, AWS Application Migration Service(AWS MGN), AWS Snow Family(Snowcone, Snowball Edge) ※ Snowmobile은 2024년 폐기됨, AWS DataSync, AWS Transfer Family, AWS Elastic Disaster Recovery(DRS)
- **선수 지식**: Chapter 3 (AWS 글로벌 인프라, 리전 개념), Chapter 5 (컴퓨팅 서비스 개념), Chapter 6 (스토리지 서비스 개념)
- **난이도**: ⭐⭐
- **예상 학습 시간**: 3시간
- **Section 목록**:
  - 20.1 클라우드 도입 프레임워크(CAF) — 6가지 관점, 조직 변화 관리
  - 20.2 6R 마이그레이션 전략 — Rehost, Replatform, Refactor 등 전략 비교
  - 20.3 AWS Migration Hub와 MGN — 마이그레이션 중앙 추적, Application Migration Service를 통한 리호스팅
  - 20.4 데이터 전송 서비스 — DMS, DataSync, Transfer Family
  - 20.5 AWS Snow Family — 대용량 오프라인 데이터 전송, 엣지 컴퓨팅 (← Ch 6.8 스토리지 관점 참조)
  - 20.6 AWS Elastic Disaster Recovery — 클라우드 기반 재해 복구(DR), RPO/RTO 개념
  - 20.7 AWS의 혁신 서비스 — VMware Cloud on AWS, 하이브리드/엣지 컴퓨팅 활용 사례 (← Local Zones, Wavelength, Outposts 개념은 Ch 3.4 참조)

---

## Part 5: 요금, 지원, 아키텍처 설계 원칙

> AWS의 요금 구조, 비용 관리 도구, 지원 체계를 이해하고, Well-Architected Framework를 통해 클라우드 아키텍처 설계 원칙을 학습합니다. 마지막으로 시험 전략까지 다룹니다.

---

### Chapter 21: AWS 요금 모델과 비용 최적화

- **학습 목표**:
  - AWS의 3가지 기본 요금 원칙(사용한 만큼, 예약 할인, 볼륨 할인)을 설명할 수 있다
  - EC2, S3, Lambda, 데이터 전송의 요금 구조를 이해할 수 있다
  - 비용 최적화의 핵심 전략(적정 크기, 예약, 스팟 활용 등)을 수립할 수 있다
  - AWS 프리 티어의 3가지 유형(상시 무료, 12개월 무료, 시험판)을 구분할 수 있다
- **핵심 키워드**: 종량제, 예약 할인, 볼륨 할인, 데이터 전송 비용, 프리 티어, 적정 크기 조정, Savings Plans, Compute Optimizer
- **도입 개념**: AWS 요금 3원칙(종량제, 예약 할인, 볼륨 할인), EC2 요금 구조, S3 요금 구조(스토리지, 요청, 데이터 전송), Lambda 요금(요청 수, 실행 시간), 데이터 전송 요금(인바운드 무료, 아웃바운드 과금), 프리 티어 3유형, 적정 크기 조정(Right-sizing), AWS Compute Optimizer, 총 소유 비용(TCO)
- **선수 지식**: Chapter 3 (리전, AZ, 서비스 유형 이해), Chapter 5 (EC2 구매 옵션 이해), Chapter 6 (S3 스토리지 클래스 이해)
- **난이도**: ⭐⭐
- **예상 학습 시간**: 3시간
- **Section 목록**:
  - 21.1 AWS 요금의 기본 원칙 — 종량제, 예약 할인, 볼륨 할인, 무료 티어
  - 21.2 주요 서비스별 요금 구조 — EC2, S3, Lambda, RDS, 데이터 전송 요금 분석
  - 21.3 데이터 전송 비용 이해 — 인바운드/아웃바운드, 리전 간, AZ 간 비용
  - 21.4 비용 최적화 전략 — 적정 크기 조정, 예약, 스팟, Savings Plans 활용
  - 21.5 AWS Compute Optimizer와 TCO — 자동 추천, 온프레미스 대비 비용 비교

---

### Chapter 22: 결제 관리와 비용 분석 도구

- **학습 목표**:
  - AWS Billing Console의 주요 기능을 활용할 수 있다
  - AWS Cost Explorer를 사용하여 비용 추세를 분석할 수 있다
  - AWS Budgets를 설정하여 예산 초과 알림을 받을 수 있다
  - 통합 결제(Consolidated Billing)의 이점을 설명할 수 있다
  - AWS Cost and Usage Report의 역할을 이해할 수 있다
- **핵심 키워드**: Billing Console, Cost Explorer, AWS Budgets, 통합 결제, Cost and Usage Report, 비용 할당 태그, AWS Pricing Calculator
- **도입 개념**: AWS Billing and Cost Management Console, AWS Cost Explorer, AWS Budgets, 예산 알림, 통합 결제(Consolidated Billing), 볼륨 할인 공유, AWS Cost and Usage Report(CUR), 비용 할당 태그(Cost Allocation Tags), AWS Pricing Calculator, AWS Cost Anomaly Detection
- **선수 지식**: Chapter 21 (요금 모델, 비용 개념), Chapter 16 (AWS Organizations, 다중 계정 관리)
- **난이도**: ⭐⭐
- **예상 학습 시간**: 2.5시간
- **Section 목록**:
  - 22.1 AWS Billing Console 개요 — 청구서 확인, 결제 수단 관리, 세금 설정
  - 22.2 AWS Cost Explorer — 비용 시각화, 필터링, 예측, 추세 분석
  - 22.3 AWS Budgets — 예산 생성, 알림 설정, 작업 자동화
  - 22.4 통합 결제와 Organizations — 볼륨 할인 공유, 결제 계정 구조
  - 22.5 Cost and Usage Report — 상세 비용 데이터, S3 내보내기
  - 22.6 AWS Pricing Calculator와 Cost Anomaly Detection — 비용 추정, 이상 비용 탐지

---

### Chapter 23: AWS 지원 플랜과 학습 리소스

- **학습 목표**:
  - AWS의 5가지 지원 플랜(Basic, Developer, Business, Enterprise On-Ramp, Enterprise)의 차이를 비교할 수 있다
  - TAM, Concierge Support, IEM의 역할을 설명할 수 있다
  - AWS 지원 케이스 심각도와 응답 시간을 이해할 수 있다
  - AWS의 공식 학습 리소스와 커뮤니티를 활용할 수 있다
- **핵심 키워드**: 지원 플랜, Basic, Developer, Business, Enterprise, TAM, Concierge, IEM, AWS re:Post, AWS Training, AWS Skill Builder
- **도입 개념**: AWS 지원 플랜(Basic, Developer, Business, Enterprise On-Ramp, Enterprise), TAM(Technical Account Manager), AWS Concierge Support, Infrastructure Event Management(IEM), 지원 케이스 심각도, 응답 시간 SLA, AWS re:Post, AWS Training and Certification, AWS Skill Builder, AWS Partner Network(APN), AWS Marketplace
- **선수 지식**: Chapter 4 (AWS 계정 구조 이해)
- **난이도**: ⭐
- **예상 학습 시간**: 2시간
- **Section 목록**:
  - 23.1 AWS 지원 플랜 비교 — 기존 5단계(Basic, Developer, Business, Enterprise On-Ramp, Enterprise) 상세 비교 + 신규 체계(Basic, Business Support+, Enterprise Support, Unified Operations) 안내 (※ 2025.12부터 Developer/Business 신규 가입 중단, 2027.1 완전 전환 예정. CLF-C02 시험은 당분간 기존 5단계 기준 출제)
  - 23.2 Enterprise 전용 기능 — TAM, Concierge, IEM, Well-Architected 리뷰
  - 23.3 지원 케이스와 응답 시간 — 심각도 분류, 플랜별 응답 시간 SLA
  - 23.4 AWS 학습 리소스 — Skill Builder, Training, re:Post, 공식 문서 활용법
  - 23.5 AWS Marketplace와 Partner Network — 서드파티 솔루션, 파트너 생태계

---

### Chapter 24: Well-Architected Framework와 시험 전략

- **학습 목표**:
  - Well-Architected Framework의 6가지 핵심 원칙(필러)을 설명할 수 있다
  - 각 필러의 설계 원칙과 주요 모범 사례를 열거할 수 있다
  - 시험 영역별 출제 비중과 핵심 토픽을 파악할 수 있다
  - 시험 문제 유형을 분석하고 효과적인 풀이 전략을 적용할 수 있다
  - 실전 모의고사를 통해 약점을 파악하고 보완할 수 있다
- **핵심 키워드**: Well-Architected Framework, 운영 우수성, 보안, 안정성, 성능 효율성, 비용 최적화, 지속 가능성, CLF-C02, 시험 전략, 모의고사
- **도입 개념**: AWS Well-Architected Framework, 운영 우수성(Operational Excellence), 보안(Security), 안정성(Reliability), 성능 효율성(Performance Efficiency), 비용 최적화(Cost Optimization), 지속 가능성(Sustainability), Well-Architected Tool, CLF-C02 시험 구조, 시험 영역(Domain), 시험 전략
- **선수 지식**: Chapter 12 (보안 원칙 이해), Chapter 21 (비용 최적화 개념), Chapter 18 (모니터링 개념)
- **난이도**: ⭐⭐⭐
- **예상 학습 시간**: 3.5시간
- **Section 목록**:
  - 24.1 Well-Architected Framework 개요 — 6가지 필러, 설계 원칙의 전체 조망
  - 24.2 운영 우수성과 안정성 — 코드형 운영, 장애 예측, 복구 전략
  - 24.3 보안과 성능 효율성 — 심층 방어, 적절한 리소스 유형 선택
  - 24.4 비용 최적화와 지속 가능성 — 낭비 제거, 환경 영향 최소화
  - 24.5 CLF-C02 시험 구조 분석 — 4개 영역, 출제 비중, 문제 유형
  - 24.6 시험 풀이 전략 — 소거법, 키워드 분석, 시간 관리
  - 24.7 최종 복습과 모의고사 — 핵심 요약, 자주 출제되는 서비스, 실전 연습

---

## 4. 학습 가이드 (Study Guide)

### 권장 학습 순서

본 커리큘럼은 선수지식 의존성에 따라 설계되어 있으므로, **Chapter 1부터 순서대로 학습하는 것을 권장**합니다. 단, 다음과 같은 병렬 학습도 가능합니다:

- Chapter 5, 6, 7은 서로 독립적이므로 동시 학습 가능
- Chapter 12는 Chapter 3 이후 언제든 시작 가능 (Part 2와 병행 가능)
- Chapter 16은 Chapter 12, 13 이후 Chapter 14, 15와 독립적으로 학습 가능 (규정 준수는 보안 서비스 심화 없이도 진행 가능)
- Chapter 20은 Chapter 3, 5, 6 이후 Part 3과 독립적으로 학습 가능
- Chapter 23은 Chapter 4 이후 언제든 학습 가능 (지원 플랜 이해)

### CLF-C02 시험 도메인별 출제 비중과 커리큘럼 매핑

시험 영역에 맞춰 학습 시간을 전략적으로 배분하세요. 특히 **보안(30%)**과 **클라우드 기술(34%)**이 전체의 64%를 차지합니다.

| 시험 도메인 | 출제 비중 | 해당 Chapter | 학습 시간 |
|-------------|-----------|-------------|-----------|
| Domain 1: 클라우드 개념 | 24% | Ch 1~4, Ch 24 | ~12.5h |
| Domain 2: 보안 및 규정 준수 | **30%** | Ch 12~16 | ~15.5h |
| Domain 3: 클라우드 기술 및 서비스 | **34%** | Ch 5~11, Ch 17~20 | ~34h |
| Domain 4: 결제, 요금, 지원 | 12% | Ch 21~23 | ~8h |

> 💡 **시험 합격이 급한 경우**: Domain 2(보안)와 Domain 3(기술/서비스)에 집중하고, 각 Chapter에서 ★ 표시된 핵심 키워드를 우선 학습하세요.

### 학습 전략

| 전략 | 설명 |
|------|------|
| **능동적 학습** | 각 Chapter의 개념을 자신의 말로 요약하고, AWS 콘솔에서 직접 확인 |
| **반복 복습** | 새 Chapter 시작 전 이전 Chapter의 핵심 키워드를 3분간 회상 |
| **실습 병행** | AWS 프리 티어를 활용하여 핵심 서비스를 직접 사용해보기 |
| **시험 연습** | 각 Part 완료 후 해당 영역의 연습 문제 풀기 |
| **시각화** | 서비스 간 관계, 아키텍처를 직접 다이어그램으로 그려보기 |

### 특별히 어려운 Chapter에 대한 학습 팁

| Chapter | 난이도 | 학습 팁 |
|---------|--------|---------|
| Ch 7: 네트워킹 | ⭐⭐⭐ | VPC를 실제로 생성해보며 서브넷, 라우팅 테이블, 게이트웨이 관계를 체화. 네트워크 기초(IP, CIDR)가 부족하면 Section 7.1에 충분한 시간 투자 |
| Ch 13: IAM | ⭐⭐⭐ | JSON 정책을 직접 작성하고 IAM Policy Simulator로 테스트. 사용자/그룹/역할의 차이를 표로 정리 |
| Ch 14: 네트워크 보안 | ⭐⭐⭐ | 보안 그룹 vs NACL 비교표를 직접 만들어 암기. 암호화 개념은 일상생활 비유(자물쇠, 열쇠)로 이해 |
| Ch 15: 보안 서비스 | ⭐⭐⭐ | GuardDuty/Inspector/Macie를 "무엇을 탐지하는가"로 구분하여 정리. Security Hub는 통합 대시보드로 이해 |
| Ch 18: 모니터링 | ⭐⭐ | CloudWatch(성능 모니터링) vs CloudTrail(API 감사)의 차이를 명확히 구분. "누가 무엇을 했는가 = CloudTrail, 얼마나 잘 동작하는가 = CloudWatch" |
| Ch 24: WAF & 시험 전략 | ⭐⭐⭐ | 6가지 필러를 먼저 암기한 후, 각 필러의 핵심 키워드 3개씩 연결. 모의고사는 최소 3회 실시 |

### 추천 참고 자료

| 자료 | 설명 |
|------|------|
| **AWS Skill Builder** | AWS 공식 무료 학습 플랫폼, CLF-C02 전용 코스 제공 |
| **AWS 공식 문서** | 각 서비스의 최신 기능과 요금 확인 |
| **AWS 공식 시험 가이드** | CLF-C02 시험 영역, 출제 비중, 샘플 문제 |
| **AWS Well-Architected Labs** | 실습 중심의 아키텍처 학습 |
| **Tutorials Dojo 연습 문제** | 실전에 가까운 모의고사 문제집 |

---

## 5. 요약

| 항목 | 내용 |
|------|------|
| **과정명** | AWS Certified Cloud Practitioner (CLF-C02) 완전 정복 |
| **총 Part 수** | 5개 |
| **총 Chapter 수** | 24개 |
| **총 Section 수** | 147개 |
| **총 예상 학습 시간** | 약 70시간 |
| **난이도 분포** | ⭐: 5개 / ⭐⭐: 14개 / ⭐⭐⭐: 5개 |

### Chapter별 학습 시간 요약

| Part | Chapter | 제목 | 난이도 | 시간 |
|------|---------|------|--------|------|
| 1 | Ch 1 | 클라우드 컴퓨팅의 개념과 이점 | ⭐ | 2h |
| 1 | Ch 2 | 클라우드 서비스 모델과 배포 모델 | ⭐ | 2h |
| 1 | Ch 3 | AWS 소개와 글로벌 인프라 | ⭐ | 2.5h |
| 1 | Ch 4 | AWS 계정 설정과 관리 콘솔 | ⭐ | 2.5h |
| 2 | Ch 5 | 컴퓨팅 서비스 | ⭐⭐ | 3.5h |
| 2 | Ch 6 | 스토리지 서비스 | ⭐⭐ | 3.5h |
| 2 | Ch 7 | 네트워킹과 콘텐츠 전송 | ⭐⭐⭐ | 4h |
| 2 | Ch 8 | 데이터베이스 서비스 | ⭐⭐ | 3h |
| 2 | Ch 9 | 컨테이너와 서버리스 아키텍처 | ⭐⭐ | 2.5h |
| 2 | Ch 10 | 애플리케이션 통합과 메시징 서비스 | ⭐⭐ | 3h |
| 2 | Ch 11 | 분석, AI/ML, 기타 서비스 | ⭐⭐ | 3.5h |
| 3 | Ch 12 | 공동 책임 모델과 보안 기초 | ⭐⭐ | 2.5h |
| 3 | Ch 13 | IAM — 자격 증명 및 접근 관리 | ⭐⭐⭐ | 3.5h |
| 3 | Ch 14 | 네트워크 보안과 데이터 보호 | ⭐⭐⭐ | 3.5h |
| 3 | Ch 15 | 보안 서비스와 위협 탐지 | ⭐⭐⭐ | 3h |
| 3 | Ch 16 | 규정 준수 프로그램과 거버넌스 | ⭐⭐ | 3h |
| 4 | Ch 17 | 관리 및 거버넌스 도구 | ⭐⭐ | 2.5h |
| 4 | Ch 18 | 모니터링, 로깅, 감사 | ⭐⭐ | 3h |
| 4 | Ch 19 | 배포 자동화와 Infrastructure as Code | ⭐⭐ | 2.5h |
| 4 | Ch 20 | 마이그레이션과 혁신 서비스 | ⭐⭐ | 3h |
| 5 | Ch 21 | AWS 요금 모델과 비용 최적화 | ⭐⭐ | 3h |
| 5 | Ch 22 | 결제 관리와 비용 분석 도구 | ⭐⭐ | 2.5h |
| 5 | Ch 23 | AWS 지원 플랜과 학습 리소스 | ⭐ | 2h |
| 5 | Ch 24 | Well-Architected Framework와 시험 전략 | ⭐⭐⭐ | 3.5h |
| | | **합계** | | **70h** |
