# Chapter 23: AWS 지원 플랜과 학습 리소스

> **난이도**: ⭐ | **예상 학습 시간**: 2시간 | **선수 지식**: Chapter 4

---

## 학습 목표 (Learning Objectives)

이 Chapter를 완료하면, 당신은 다음을 할 수 있습니다:

- [ ] AWS의 5가지 지원 플랜(Basic, Developer, Business, Enterprise On-Ramp, Enterprise)의 차이를 비교하고, 조직의 상황에 맞는 플랜을 선택할 수 있다
- [ ] TAM, Concierge Support, IEM의 역할과 어떤 지원 플랜에서 제공되는지를 설명할 수 있다
- [ ] AWS 지원 케이스의 심각도 분류와 플랜별 응답 시간 SLA를 이해할 수 있다
- [ ] AWS의 공식 학습 리소스(Skill Builder, re:Post, Training and Certification)를 활용할 수 있다
- [ ] AWS Marketplace와 Partner Network의 역할을 설명하고 활용 시나리오를 구분할 수 있다

---

## 핵심 질문 (Essential Questions)

1. **AWS에 문제가 생겼을 때, 어떤 도움을 받을 수 있는가?** — 무료 계정과 유료 지원 플랜에서 받을 수 있는 지원의 범위는 얼마나 다를까?
2. **우리 조직에 맞는 지원 플랜은 어떻게 선택하는가?** — 스타트업, 중견기업, 대기업은 각각 어떤 수준의 지원이 필요한가?
3. **AWS를 더 잘 활용하기 위해 어떤 학습 자원과 생태계가 있는가?** — AWS가 제공하는 공식 학습 경로와 파트너 생태계를 어떻게 활용할 수 있는가?

---

## 개념 지도 (Concept Map)

```
[선수: Chapter 4 — AWS 계정, Management Console, 프리 티어]
        │
        ▼
┌──────────────────────────────────────────────────────────┐
│          Chapter 23: AWS 지원 플랜과 학습 리소스            │
│                                                          │
│  [신규: 5가지 지원 플랜] ──→ Basic ~ Enterprise 비교       │
│         │                                                │
│         ▼                                                │
│  [신규: Enterprise 전용 기능] ──→ TAM, Concierge, IEM     │
│         │                                                │
│         ▼                                                │
│  [신규: 지원 케이스 & SLA] ──→ 심각도 분류, 응답 시간       │
│         │                                                │
│         ▼                                                │
│  [신규: 학습 리소스] ──→ Skill Builder, re:Post, Training  │
│         │                                                │
│         ▼                                                │
│  [신규: Marketplace & APN] ──→ 서드파티 솔루션, 파트너      │
└──────────────────────────────────────────────────────────┘
        │
        ▼
[결과: AWS 지원 체계와 학습 생태계를 이해하고 활용할 수 있는 능력]
```

---

## 실습 환경 안내 (Lab Prerequisites)

> 🧪 **실습 환경 안내**
>
> **필요 계정**: AWS 계정 (Free Tier 활성 상태 권장)
> **사용 서비스**: AWS Support Center, AWS Trusted Advisor, AWS Skill Builder, AWS Marketplace, AWS re:Post
> **예상 비용**: Free Tier 범위 내 (이 Chapter의 모든 실습은 무료입니다)
> **사전 준비**: Chapter 4에서 생성한 AWS 계정이 필요합니다. 별도의 리소스 사전 생성은 필요하지 않습니다.
> **리전 설정**: Support Center는 글로벌 서비스로 리전에 무관합니다. 기타 탐색은 ap-northeast-2 (서울) 권장.

> 💬 **참고**: 이 Chapter의 실습은 대부분 AWS 콘솔의 지원 관련 메뉴를 **탐색하고 확인**하는 수준입니다. 리소스를 생성하거나 비용이 발생하는 실습은 없으므로, 실습 후 별도의 리소스 정리가 필요하지 않습니다.

---

## 23.1 AWS 지원 플랜 비교

> 💡 **한 줄 요약**: AWS는 무료(Basic)부터 전담 기술 관리자가 배정되는 Enterprise까지, 5가지 지원 플랜을 제공하며 조직의 규모와 필요에 따라 선택합니다.

### 직관적 이해 (Intuitive Understanding)

새로운 아파트에 입주했다고 상상해 봅시다. 아파트에는 기본적으로 관리 사무소가 있어서 공지사항을 확인하고, 간단한 문의를 할 수 있습니다. 하지만 배관이 터지거나 전기 문제가 생기면 더 전문적인 도움이 필요합니다. 이때 아파트에 따라 제공하는 서비스 수준이 다릅니다:

- **일반 아파트**: 관리 사무소 게시판만 있음 → **Basic** 플랜
- **서비스 아파트**: 이메일로 기술 상담 가능 → **Developer** 플랜
- **프리미엄 아파트**: 24시간 전화 지원 + 전문가 상담 → **Business** 플랜
- **호텔식 레지던스**: 전담 컨시어지 + 빠른 대응 → **Enterprise On-Ramp** 플랜
- **최고급 호텔**: 전담 매니저(버틀러) + 즉각 대응 + 맞춤 서비스 → **Enterprise** 플랜

AWS도 마찬가지입니다. AWS 계정을 만들면 **Basic** 플랜이 무료로 제공되지만, 비즈니스가 성장하고 운영 환경이 복잡해지면 더 높은 수준의 기술 지원이 필요해집니다. AWS는 이러한 다양한 필요를 충족하기 위해 **5가지 지원 플랜**을 제공합니다.

> 🔗 **연결**: Chapter 4에서 AWS 계정을 생성했을 때, 자동으로 Basic 지원 플랜이 적용되었습니다. 이 Section에서는 그 Basic 플랜이 무엇을 포함하는지, 그리고 그 이상의 플랜들이 무엇을 추가로 제공하는지 상세히 비교합니다.

### 핵심 개념 설명 (Core Explanation)

> 📝 **AWS Support Plan (AWS 지원 플랜)**: AWS가 고객에게 제공하는 기술 지원 서비스의 등급입니다. 플랜에 따라 지원 범위, 응답 시간, 접근 가능한 전문 서비스가 달라집니다.

AWS의 5가지 지원 플랜을 하나씩 살펴보겠습니다.

**1) Basic 플랜 (무료)**

모든 AWS 계정에 자동으로 포함되는 무료 플랜입니다. 기술 지원 엔지니어에게 직접 문의하는 것은 불가능하지만, 다음과 같은 기본 지원이 포함됩니다:

- **고객 서비스(Customer Service)**: 계정 및 결제 관련 문의 가능 (24/7)
- **AWS 문서, 백서, 포럼**: 셀프 서비스 학습 자원 이용
- **AWS Trusted Advisor**: 7개의 핵심 검사(Core Checks)만 이용 가능
- **AWS Personal Health Dashboard**: 자신의 계정에 영향을 미치는 AWS 이벤트 확인

**2) Developer 플랜 (월 $29~ 또는 AWS 사용료의 3% 중 큰 금액)**

개인 개발자나 테스트 환경에서 AWS를 사용하는 경우에 적합합니다. Basic 플랜의 모든 기능에 더해:

- **기술 지원 접근**: AWS 지원 엔지니어에게 **이메일**로 기술 문의 가능
- **응답 시간**: 일반 안내 24시간 이내, 시스템 손상 시 12시간 이내
- **문의 가능 인원**: 계정의 **루트 사용자 1명**만 지원 케이스 생성 가능
- **일반 아키텍처 지침**: "이 구조가 적절한가요?"와 같은 일반적인 조언을 받을 수 있음

**3) Business 플랜 (월 $100~ 또는 AWS 사용료의 일정 비율 중 큰 금액)**

프로덕션 워크로드를 운영하는 기업에 적합합니다. Developer 플랜의 모든 기능에 더해:

- **기술 지원 접근**: **전화, 채팅, 이메일** 모두 가능 (24/7)
- **응답 시간**: 프로덕션 시스템 장애 시 **4시간** 이내, 시스템 다운 시 **1시간** 이내
- **문의 가능 인원**: **무제한** — IAM 사용자 누구나 지원 케이스 생성 가능
- **Trusted Advisor**: **전체 검사(Full Checks)** 이용 가능
- **AWS Support API**: 프로그래밍 방식으로 지원 케이스 관리 가능
- **서드파티 소프트웨어 지원**: AWS에서 실행 중인 서드파티 OS, 애플리케이션에 대한 지원

**4) Enterprise On-Ramp 플랜 (월 $5,500~ 또는 AWS 사용료의 일정 비율 중 큰 금액)**

Enterprise 수준의 지원이 필요하지만 전담 TAM까지는 필요하지 않은 조직을 위한 플랜입니다. Business 플랜의 모든 기능에 더해:

- **응답 시간**: 비즈니스 크리티컬 시스템 다운 시 **30분** 이내
- **TAM 풀(Pool) 접근**: 전담 TAM은 아니지만, TAM 풀의 기술 전문가 그룹에 접근 가능
- **Concierge Support Team**: 계정 및 결제 전문 팀의 지원
- **Infrastructure Event Management(IEM)**: 연 1회 무료 제공 (추가 비용으로 더 이용 가능)

**5) Enterprise 플랜 (월 $15,000~ 또는 AWS 사용료의 일정 비율 중 큰 금액)**

미션 크리티컬 워크로드를 운영하는 대규모 조직을 위한 최고 수준의 지원입니다. Enterprise On-Ramp의 모든 기능에 더해:

- **응답 시간**: 비즈니스 크리티컬 시스템 다운 시 **15분** 이내
- **전담 TAM**: 지정된 **Technical Account Manager**가 1:1로 배정
- **Concierge Support Team**: 계정 및 결제 전문 팀의 지원
- **Infrastructure Event Management(IEM)**: 무제한 제공
- **Well-Architected 리뷰**: AWS의 모범 사례 프레임워크에 따른 아키텍처 리뷰

다음 표에서 5가지 플랜의 핵심 차이를 한눈에 비교할 수 있습니다:

| 항목 | Basic | Developer | Business | Enterprise On-Ramp | Enterprise |
|------|-------|-----------|----------|--------------------|------------|
| **월 비용** | 무료 | $29~ | $100~ | $5,500~ | $15,000~ |
| **기술 지원 채널** | 없음 | 이메일 | 전화, 채팅, 이메일 | 전화, 채팅, 이메일 | 전화, 채팅, 이메일 |
| **지원 가능 인원** | - | 루트 1명 | 무제한 | 무제한 | 무제한 |
| **크리티컬 응답 시간** | - | - | 1시간 | 30분 | **15분** |
| **Trusted Advisor** | 7개 핵심 검사 | 7개 핵심 검사 | 전체 검사 | 전체 검사 | 전체 검사 |
| **TAM** | ✗ | ✗ | ✗ | TAM 풀 | **전담 TAM** |
| **Concierge** | ✗ | ✗ | ✗ | ✓ | ✓ |
| **IEM** | ✗ | ✗ | ✗ | 연 1회 | 무제한 |

### 상세 예시 (Detailed Examples)

> 🔍 **예시 23.1.1: 1인 개발자의 지원 플랜 선택**
>
> **상황**: 프리랜서 개발자 민수는 개인 프로젝트로 AWS Lambda와 DynamoDB를 사용하여 간단한 API를 구축하고 있습니다. 가끔 설정 방법을 모를 때 AWS에 질문하고 싶지만, 24시간 전화 지원까지는 필요하지 않습니다.
> **풀이/설명**: 민수에게는 **Developer** 플랜이 적합합니다. 이메일로 기술 질문을 보낼 수 있고, 일반 안내는 24시간 이내에 응답받을 수 있습니다. 월 $29 수준의 비용으로 필요한 기술 상담을 받을 수 있습니다. Basic 플랜은 무료이지만 기술 지원 문의가 불가능하므로, 기술적인 질문이 있을 때 답을 얻기 어렵습니다.
> **핵심 포인트**: 기술 지원이 필요하지만 프로덕션 워크로드가 아닌 경우, Developer 플랜이 비용 대비 적절한 선택입니다.

> 🔍 **예시 23.1.2: 성장하는 스타트업의 지원 플랜 선택**
>
> **상황**: 전자상거래 스타트업 A사는 AWS에서 웹사이트와 결제 시스템을 운영 중입니다. 최근 사용자가 급증하면서, 서비스 장애가 발생하면 매출에 직접적인 영향이 있습니다. 팀원 5명이 AWS를 사용하며, 장애 시 빠른 응답이 필요합니다.
> **풀이/설명**: A사에는 **Business** 플랜이 적합합니다. 프로덕션 시스템 장애 시 1시간 이내에 응답받을 수 있고, 전화와 채팅으로 24/7 지원을 받을 수 있습니다. 팀원 모두가 지원 케이스를 생성할 수 있어 운영 효율성이 높습니다. 또한 Trusted Advisor 전체 검사를 통해 인프라 최적화 권장 사항도 받을 수 있습니다.
> **핵심 포인트**: 프로덕션 워크로드를 운영하고, 장애 시 비즈니스 영향이 큰 경우 Business 플랜 이상을 고려해야 합니다.

### 미니 실습 (Hands-on Mini Lab)

> 🧪 **Mini Lab 23.1: 현재 지원 플랜 확인하기**
>
> **목표**: 내 AWS 계정에 적용된 지원 플랜을 확인하고, Support Center의 기본 화면을 탐색합니다.
> **예상 소요 시간**: 5분
> **비용**: 무료
>
> **Step 1**: AWS Management Console에 로그인합니다.
> **Step 2**: 상단 검색창에 `Support`를 입력하고, **Support Center**를 클릭합니다.
> **Step 3**: Support Center 메인 화면 왼쪽 메뉴에서 **Account overview** 또는 화면 상단 영역에서 현재 적용된 지원 플랜을 확인합니다. 무료 계정이라면 "Basic" 또는 "Basic Support"로 표시됩니다.
> **Step 4**: 왼쪽 메뉴에서 **Create case**를 클릭해 봅니다. Basic 플랜에서는 "Account and billing support"만 생성할 수 있고, "Technical support" 케이스는 생성할 수 없는 것을 확인합니다. (케이스를 실제로 생성하지 않아도 됩니다.)
> **Step 5**: 왼쪽 메뉴에서 **Trusted Advisor**를 클릭하여 탐색합니다. Basic 플랜에서는 일부 핵심 검사만 이용 가능한 것을 확인할 수 있습니다.
>
> **확인**: Support Center에서 현재 플랜이 "Basic"으로 표시되고, 기술 지원 케이스는 생성할 수 없으며, Trusted Advisor에서 제한된 검사 항목만 확인할 수 있습니다.

### 깊이 있는 이해 (Deep Dive)

> 🔬 **Deep Dive: AWS 지원 플랜 체계 변경 (2025~2027)**
>
> *이 부분은 심화 내용입니다. 처음 학습 시 건너뛰어도 됩니다.*
>
> AWS는 2025년 12월부터 지원 플랜 체계를 개편하고 있습니다. 기존 5단계(Basic, Developer, Business, Enterprise On-Ramp, Enterprise) 중 **Developer**와 **Business** 플랜은 신규 가입이 중단되었으며, 2027년 1월까지 완전히 새로운 체계로 전환될 예정입니다.
>
> **새로운 지원 플랜 체계**:
> - **Basic**: 기존과 동일 (무료)
> - **Business Support+**: 기존 Business 플랜을 대체
> - **Enterprise Support**: 기존 Enterprise On-Ramp와 Enterprise를 통합·개편
> - **Unified Operations**: 대규모 조직을 위한 새로운 최상위 플랜
>
> 단, **AWS Certified Cloud Practitioner(CLF-C02) 시험**은 당분간 **기존 5단계 체계를 기준으로 출제**됩니다. 따라서 시험 준비를 위해서는 본문에서 설명한 5단계 체계를 정확히 이해하는 것이 중요합니다. 향후 시험 범위가 변경되면 AWS 공식 시험 가이드를 통해 안내될 것입니다.

### 흔한 실수와 주의사항 (Common Pitfalls)

> ⚠️ **주의**:
> - **"Basic 플랜에서도 기술 지원을 받을 수 있다"는 오해**: Basic 플랜에서는 **계정 및 결제** 관련 문의만 가능합니다. "EC2 인스턴스가 안 됩니다"와 같은 기술 문의는 Developer 플랜 이상에서만 가능합니다.
> - **Developer 플랜의 문의 인원 제한**: Developer 플랜에서는 **루트 사용자 1명만** 지원 케이스를 생성할 수 있습니다. 팀 단위로 지원이 필요하면 Business 플랜 이상이 필요합니다.
> - **Trusted Advisor 전체 검사는 Business 이상**: Basic과 Developer 플랜에서는 7개의 핵심 검사만 이용 가능합니다. 전체 검사(비용 최적화, 성능, 보안, 내결함성, 서비스 한도 등)는 Business 플랜부터 가능합니다.

### Section 요약 (Section Summary)

- AWS는 Basic(무료), Developer, Business, Enterprise On-Ramp, Enterprise의 5가지 지원 플랜을 제공한다.
- Basic 플랜은 기술 지원이 불가하며, Developer 플랜부터 이메일 기술 지원이 가능하다.
- Business 플랜부터 전화/채팅 24/7 지원과 Trusted Advisor 전체 검사가 제공된다.
- Enterprise On-Ramp는 TAM 풀 접근과 30분 응답 시간을, Enterprise는 전담 TAM과 15분 응답 시간을 제공한다.
- 지원 플랜 선택은 조직의 규모, 워크로드의 중요도, 필요한 응답 속도에 따라 결정한다.

---

## 23.2 Enterprise 전용 기능 — TAM, Concierge, IEM, Well-Architected 리뷰

> 💡 **한 줄 요약**: Enterprise급 지원 플랜에서는 전담 기술 관리자(TAM), 결제 전문 팀(Concierge), 대규모 이벤트 지원(IEM) 등 고급 서비스를 통해 선제적이고 맞춤화된 지원을 받을 수 있습니다.

### 직관적 이해 (Intuitive Understanding)

대형 건물을 관리한다고 생각해 봅시다. 일반 관리 서비스에서는 문제가 생기면 콜센터에 전화하여 순서를 기다려야 합니다. 하지만 프리미엄 관리 서비스를 이용하면:

- **전담 건물 관리인(TAM)**: 여러분의 건물 구조를 속속들이 알고 있는 전담 관리인이 배정됩니다. 문제가 생기기 전에 미리 점검하고, 최적의 관리 방법을 제안합니다.
- **컨시어지(Concierge)**: 관리비 청구서, 계약 갱신, 세금 문제 등을 전담으로 처리해주는 사무 전문가입니다.
- **대규모 이벤트 지원(IEM)**: 건물에서 대형 행사가 열릴 때, 사전에 시설을 점검하고 추가 인력을 배치해주는 서비스입니다.

이처럼 Enterprise급 지원은 단순히 "문제가 생기면 도와주는" 수준을 넘어, **선제적(proactive)으로 관리하고 최적화를 도와주는** 파트너십에 가깝습니다.

### 핵심 개념 설명 (Core Explanation)

#### TAM (Technical Account Manager)

> 📝 **TAM (Technical Account Manager)**: AWS가 고객에게 배정하는 전담 기술 관리자입니다. 고객의 AWS 환경을 깊이 이해하고, 기술적 가이드, 아키텍처 리뷰, 모범 사례 적용을 선제적으로 지원합니다.

TAM은 AWS의 기술 전문가로서, 다음과 같은 역할을 수행합니다:

- **선제적 가이드**: 문제가 발생하기 전에 잠재적 리스크를 파악하고 개선 방안을 제안합니다.
- **아키텍처 리뷰**: 고객의 AWS 인프라가 모범 사례에 부합하는지 정기적으로 검토합니다.
- **이벤트 조율**: 대규모 마이그레이션이나 출시 이벤트 시 AWS 내부 리소스를 조율합니다.
- **기술 전문성**: 고객의 비즈니스와 기술 환경을 이해하고 맞춤형 기술 조언을 제공합니다.

TAM의 제공 방식은 플랜에 따라 다릅니다:
- **Enterprise On-Ramp**: **TAM 풀(Pool)** — 전담 TAM은 없지만, TAM 전문가 그룹에 접근하여 지원을 받을 수 있습니다.
- **Enterprise**: **전담 TAM** — 지정된 1명의 TAM이 여러분의 계정을 전담합니다.

#### AWS Concierge Support Team

> 📝 **AWS Concierge Support Team**: Enterprise On-Ramp 및 Enterprise 플랜 고객에게 제공되는 계정 및 결제 전문 지원 팀입니다. 일반적인 기술 지원과는 별도로, 결제·계정 관련 복잡한 문제를 전담합니다.

Concierge 팀이 도와주는 대표적인 업무:

- 복잡한 **결제 구조**에 대한 상담 및 안내
- AWS 계정 관련 **모범 사례** 조언
- **결제 관련 지원 케이스**의 우선 처리
- 비용 최적화를 위한 **결제 분석 지원**

> 💬 **참고**: Concierge는 *기술* 문제가 아닌 *계정 및 결제* 관련 문제를 전담합니다. 기술적인 문제는 일반 기술 지원 또는 TAM을 통해 해결합니다.

#### Infrastructure Event Management (IEM)

> 📝 **Infrastructure Event Management (IEM)**: 블랙 프라이데이 세일, 신규 서비스 출시 등 **대규모 트래픽이 예상되는 이벤트** 전에, AWS 전문가가 인프라를 사전 점검하고 이벤트 중에도 실시간으로 지원하는 서비스입니다.

IEM은 다음과 같은 단계로 진행됩니다:

1. **사전 준비 단계**: 이벤트 전에 아키텍처를 점검하고, 확장성(Scalability)과 가용성을 검증합니다.
2. **이벤트 실행 단계**: 이벤트 당일 실시간으로 모니터링하고, 문제 발생 시 즉각 대응합니다.
3. **사후 분석 단계**: 이벤트 후 성과를 분석하고 개선 사항을 도출합니다.

IEM의 제공 방식은 플랜에 따라 다릅니다:
- **Business**: 추가 비용을 지불하면 이용 가능
- **Enterprise On-Ramp**: **연 1회** 무료 제공
- **Enterprise**: **무제한** 제공

#### Well-Architected 리뷰

> 📝 **Well-Architected 리뷰**: AWS Well-Architected Framework의 모범 사례를 기준으로, 고객의 워크로드 아키텍처를 점검하고 개선 권장 사항을 제공하는 서비스입니다.

Enterprise 플랜에서는 AWS 솔루션 아키텍트가 직접 고객의 아키텍처를 리뷰하고, 보안·안정성·성능·비용·운영 측면에서 개선 포인트를 제안합니다.

> 💬 **참고**: Well-Architected Framework 자체는 Chapter 24에서 자세히 다룹니다. 여기서는 Enterprise 플랜에서 이 프레임워크에 기반한 전문가 리뷰 서비스를 받을 수 있다는 점만 알아둡니다.

### 상세 예시 (Detailed Examples)

> 🔍 **예시 23.2.1: TAM이 선제적으로 문제를 방지한 사례**
>
> **상황**: 대형 온라인 쇼핑몰 B사는 Enterprise 플랜을 사용하며, 전담 TAM이 배정되어 있습니다. TAM은 분기별로 B사의 AWS 인프라를 검토합니다. 어느 날 TAM이 B사의 데이터베이스 스토리지가 현재 성장 추세로는 2개월 내에 한도에 도달할 것이라는 점을 발견했습니다.
> **풀이/설명**: TAM은 B사 팀에 사전 알림을 보내고, 스토리지 확장 옵션과 비용 효율적인 데이터 아카이빙 전략을 제안했습니다. B사는 장애가 발생하기 전에 여유 있게 인프라를 조정할 수 있었습니다. 이것이 TAM의 핵심 가치인 **선제적(proactive) 지원**입니다.
> **핵심 포인트**: TAM은 문제가 발생한 후에 대응하는 것이 아니라, 발생하기 전에 예방하는 역할을 합니다.

> 🔍 **예시 23.2.2: IEM을 활용한 대규모 이벤트 준비**
>
> **상황**: 게임 회사 C사가 신작 게임을 출시합니다. 출시 직후 수백만 명의 동시 접속자가 예상되는데, 이전 출시 때 서버 다운으로 큰 손실을 겪은 적이 있습니다. C사는 Enterprise 플랜을 사용 중입니다.
> **풀이/설명**: C사는 IEM을 요청했습니다. AWS 전문가가 출시 2주 전부터 인프라를 점검하여 Auto Scaling 설정을 최적화하고, 데이터베이스 읽기 성능을 보강했습니다. 출시 당일에는 AWS 전문가가 실시간으로 시스템을 모니터링하며, 트래픽 급증에 즉각 대응했습니다. 결과적으로 출시는 성공적으로 진행되었습니다.
> **핵심 포인트**: IEM은 한 번의 대규모 이벤트를 성공적으로 수행하기 위한 AWS의 맞춤 지원 서비스입니다.

### 흔한 실수와 주의사항 (Common Pitfalls)

> ⚠️ **주의**:
> - **"TAM은 모든 Enterprise급 플랜에서 전담으로 배정된다"는 오해**: Enterprise On-Ramp에서는 **TAM 풀**에 접근하는 것이지, 전담 TAM이 배정되는 것이 아닙니다. 전담 TAM은 **Enterprise 플랜에서만** 제공됩니다. 시험에서 이 차이를 묻는 문제가 자주 출제됩니다.
> - **Concierge는 기술 지원이 아님**: Concierge Support Team은 **계정 및 결제** 전문 팀입니다. 기술적인 문제(서버 장애, 설정 오류 등)는 Concierge가 아닌 기술 지원 또는 TAM에게 문의해야 합니다.
> - **IEM은 "항상 제공되는 서비스"가 아님**: IEM은 특정 이벤트를 위해 **사전에 요청**하여 진행하는 서비스입니다. 상시 모니터링 서비스와는 다릅니다.

### Section 요약 (Section Summary)

- **TAM(Technical Account Manager)**은 전담 기술 관리자로, Enterprise 플랜에서 1:1 배정되고 Enterprise On-Ramp에서는 TAM 풀로 접근한다.
- **Concierge Support Team**은 계정 및 결제 전문 팀으로, Enterprise On-Ramp 이상에서 제공된다.
- **IEM(Infrastructure Event Management)**은 대규모 이벤트 전후로 인프라를 점검·지원하는 서비스이다.
- **Well-Architected 리뷰**는 Enterprise 플랜에서 AWS 전문가가 직접 아키텍처를 점검해주는 서비스이다.
- 이들 서비스의 공통점은 **선제적(proactive) 지원**이라는 점이며, 단순 장애 대응을 넘어 최적화와 예방에 초점을 맞춘다.

---

## 23.3 지원 케이스와 응답 시간

> 💡 **한 줄 요약**: AWS 지원 케이스는 심각도에 따라 5단계로 분류되며, 지원 플랜에 따라 응답 시간 SLA가 달라집니다.

### 직관적 이해 (Intuitive Understanding)

병원의 응급실을 생각해 봅시다. 환자가 도착하면 증상의 심각도에 따라 분류(트리아지)됩니다:

- 가벼운 상담 → 일반 외래 → 순서대로 진료
- 골절이나 출혈 → 우선 진료
- 생명이 위험한 상황 → **즉시** 응급 처치

AWS 지원도 마찬가지입니다. 모든 문의가 같은 긴급도를 갖는 것이 아닙니다. "이 서비스는 뭔가요?"라는 일반 질문과 "프로덕션 시스템이 완전히 다운됐습니다!"라는 긴급 상황은 완전히 다른 속도로 대응해야 합니다. 그래서 AWS는 지원 케이스를 **심각도(Severity)** 에 따라 분류하고, 각 심각도에 맞는 **응답 시간 SLA**를 보장합니다.

### 핵심 개념 설명 (Core Explanation)

> 📝 **지원 케이스(Support Case)**: AWS Support Center를 통해 생성하는 기술 문의 또는 계정/결제 문의를 말합니다. 케이스에는 문제 설명, 심각도, 관련 서비스 등의 정보가 포함됩니다.

> 📝 **심각도(Severity)**: 문제가 비즈니스에 미치는 영향의 정도를 나타내는 분류입니다. 심각도가 높을수록 더 빠른 응답이 보장됩니다.

> 📝 **SLA (Service Level Agreement, 서비스 수준 계약)**: 서비스 제공자가 고객에게 보장하는 서비스 품질 수준을 명시한 계약입니다. 여기서는 "이 심각도의 케이스에는 N시간 이내에 첫 번째 응답을 드리겠습니다"라는 약속입니다.

AWS 지원 케이스의 5가지 심각도와 플랜별 응답 시간은 다음과 같습니다:

| 심각도 | 설명 | Developer | Business | Enterprise On-Ramp | Enterprise |
|--------|------|-----------|----------|--------------------|------------|
| **일반 안내** | 일반적인 질문, 기능 요청 | 24시간 (영업시간) | 24시간 | 24시간 | 24시간 |
| **시스템 손상** | 기능이 저하되었으나 대안이 있음 | 12시간 (영업시간) | 12시간 | 12시간 | 12시간 |
| **프로덕션 시스템 손상** | 중요 기능이 심각하게 손상됨 | - | 4시간 | 4시간 | 4시간 |
| **프로덕션 시스템 다운** | 비즈니스에 심각한 영향, 우회 불가 | - | **1시간** | **1시간** | **1시간** |
| **비즈니스 크리티컬 시스템 다운** | 비즈니스가 위험에 처함 | - | - | **30분** | **15분** |

각 심각도를 실제 상황으로 이해해 봅시다:

**1) 일반 안내 (General Guidance)**
- "S3 버킷의 버전 관리를 활성화하는 방법이 궁금합니다."
- "이 아키텍처에 대한 일반적인 조언을 듣고 싶습니다."

**2) 시스템 손상 (System Impaired)**
- "애플리케이션의 일부 기능이 느려졌지만, 다른 경로로 서비스는 가능합니다."
- "개발 환경의 데이터베이스가 간헐적으로 연결이 끊깁니다."

**3) 프로덕션 시스템 손상 (Production System Impaired)**
- "프로덕션 웹 서버의 응답 시간이 10배 느려져서 사용자 경험이 심각하게 저하되고 있습니다."

**4) 프로덕션 시스템 다운 (Production System Down)**
- "프로덕션 데이터베이스에 접속이 불가능하여 모든 사용자가 서비스를 이용할 수 없습니다."

**5) 비즈니스 크리티컬 시스템 다운 (Business-Critical System Down)**
- "핵심 결제 시스템이 완전히 다운되어 매출 손실이 발생하고 있으며, 시간이 지날수록 손실이 급격히 증가합니다."

> 💬 **참고**: "프로덕션 시스템 손상" 이상의 심각도는 **Business 플랜 이상**에서만 선택할 수 있습니다. "비즈니스 크리티컬 시스템 다운"은 **Enterprise On-Ramp 이상**에서만 가능합니다. 이는 해당 심각도의 빠른 응답을 보장하려면 그에 상응하는 지원 플랜이 필요하기 때문입니다.

#### 지원 케이스 생성 방법

AWS Support Center에서 지원 케이스를 생성할 때는 다음 정보를 입력합니다:

1. **케이스 유형**: 계정/결제 문의 또는 기술 문의
2. **서비스**: 문제가 발생한 AWS 서비스 선택
3. **심각도**: 위의 5단계 중 선택 (플랜에 따라 선택 가능 범위가 다름)
4. **문제 설명**: 문제 상황, 영향 범위, 이미 시도한 해결 방법 등
5. **연락 방법**: 이메일, 채팅, 전화 (플랜에 따라 선택 가능 범위가 다름)

### 상세 예시 (Detailed Examples)

> 🔍 **예시 23.3.1: 심각도 선택의 중요성**
>
> **상황**: Business 플랜을 사용하는 D사에서 테스트 환경의 EC2 인스턴스 하나가 응답하지 않습니다. 담당자는 이 문제를 "프로덕션 시스템 다운"으로 케이스를 생성했습니다.
> **풀이/설명**: 테스트 환경의 문제는 실제 비즈니스에 즉각적인 영향을 주지 않으므로, "시스템 손상" 정도가 적절한 심각도입니다. 심각도를 과도하게 높게 설정하면 AWS 지원 팀의 리소스가 비효율적으로 사용되고, 실제 긴급 상황에서의 대응 품질이 저하될 수 있습니다. AWS는 심각도가 부적절하다고 판단하면 조정을 요청할 수 있습니다.
> **핵심 포인트**: 심각도는 실제 비즈니스 영향에 맞게 정확히 선택해야 합니다. "빠른 응답을 받기 위해" 심각도를 높이는 것은 적절하지 않습니다.

> 🔍 **예시 23.3.2: 플랜별 대응 속도 비교**
>
> **상황**: 두 회사가 동일한 프로덕션 장애를 경험했습니다. E사는 Business 플랜, F사는 Enterprise 플랜을 사용합니다. 둘 다 "비즈니스에 심각한 영향이 있는 장애"입니다.
> **풀이/설명**: E사(Business)는 "프로덕션 시스템 다운"으로 케이스를 생성할 수 있고, **1시간** 이내 응답이 보장됩니다. F사(Enterprise)는 "비즈니스 크리티컬 시스템 다운"으로 케이스를 생성할 수 있고, **15분** 이내 응답이 보장됩니다. 또한 F사는 전담 TAM이 즉시 상황을 인지하고 내부 조율을 시작합니다.
> **핵심 포인트**: 비즈니스 크리티컬 워크로드를 운영할 때, 15분 응답과 1시간 응답의 차이는 매우 클 수 있습니다. 이것이 Enterprise 플랜의 비용을 정당화하는 핵심 요소 중 하나입니다.

### 흔한 실수와 주의사항 (Common Pitfalls)

> ⚠️ **주의**:
> - **응답 시간 ≠ 해결 시간**: SLA에서 보장하는 것은 **첫 번째 응답**까지의 시간입니다. 문제가 완전히 해결되는 시간은 문제의 복잡도에 따라 달라집니다.
> - **Developer 플랜의 응답 시간은 "영업시간" 기준**: Developer 플랜의 응답 시간은 영업 시간(business hours) 기준입니다. 금요일 저녁에 케이스를 생성하면 월요일에 응답을 받을 수 있습니다. Business 플랜부터 24/7 지원이 제공됩니다.
> - **시험에서 자주 출제되는 포인트**: CLF-C02 시험에서는 "15분 응답 시간을 제공하는 플랜은?" (Enterprise), "전담 TAM이 제공되는 플랜은?" (Enterprise) 등의 문제가 자주 출제됩니다.

### Section 요약 (Section Summary)

- 지원 케이스는 5가지 심각도(일반 안내, 시스템 손상, 프로덕션 시스템 손상, 프로덕션 시스템 다운, 비즈니스 크리티컬 시스템 다운)로 분류된다.
- 심각도가 높을수록 더 빠른 응답 시간이 보장되며, 높은 심각도는 상위 플랜에서만 선택할 수 있다.
- SLA의 응답 시간은 "첫 번째 응답"까지의 시간이며, 해결 시간을 보장하는 것은 아니다.
- Developer 플랜은 영업시간 기준, Business 이상은 24/7 기준으로 응답 시간이 적용된다.

---

## 23.4 AWS 학습 리소스

> 💡 **한 줄 요약**: AWS는 Skill Builder, Training and Certification, re:Post, 공식 문서 등 다양한 무료·유료 학습 리소스를 제공하여, 누구나 AWS를 체계적으로 학습할 수 있도록 지원합니다.

### 직관적 이해 (Intuitive Understanding)

새로운 프로그래밍 언어를 배운다고 상상해 봅시다. 어디서부터 시작해야 할까요? 공식 문서를 읽을 수도 있고, 온라인 강좌를 수강할 수도 있고, 커뮤니티 포럼에서 질문할 수도 있습니다. AWS를 배우는 것도 마찬가지입니다. 문제는 AWS에는 200개 이상의 서비스가 있어서, **어디서부터, 어떤 자원을 활용해** 학습할지 아는 것 자체가 중요합니다.

AWS는 이런 학습 여정을 돕기 위해 다양한 공식 리소스를 제공합니다. 이 리소스들은 대부분 **무료**이거나 합리적인 비용으로 이용할 수 있어서, 독학자부터 기업의 대규모 교육까지 폭넓게 활용됩니다.

### 핵심 개념 설명 (Core Explanation)

#### AWS Skill Builder

> 📝 **AWS Skill Builder**: AWS가 운영하는 온라인 학습 플랫폼입니다. 수백 개의 디지털 학습 과정, 학습 경로(Learning Path), 실습 랩을 제공합니다.

AWS Skill Builder의 주요 특징:

- **무료 디지털 과정**: 600개 이상의 무료 온라인 과정을 제공합니다. AWS 기초부터 고급 아키텍처까지 다양한 주제를 다룹니다.
- **학습 경로(Learning Path)**: 역할별(클라우드 실무자, 솔루션 아키텍트, 개발자 등)로 체계적인 학습 경로를 제안합니다.
- **실습 랩(Hands-on Labs)**: 실제 AWS 환경에서 실습할 수 있는 가이드형 랩을 제공합니다. 일부는 무료, 일부는 유료 구독이 필요합니다.
- **시험 준비 과정**: AWS 자격증 시험을 준비하기 위한 전용 과정과 연습 문제를 제공합니다.
- **구독 플랜**: 무료 티어와 유료 구독($29/월 개인, 팀/기업 플랜도 있음)이 있으며, 유료 구독 시 더 많은 실습 랩과 시험 준비 자료에 접근할 수 있습니다.

#### AWS Training and Certification

> 📝 **AWS Training and Certification**: AWS의 공식 교육 및 자격증 프로그램입니다. 강사 주도 교육(Instructor-Led Training), 디지털 교육, 자격증 시험을 포함합니다.

주요 구성 요소:

- **강사 주도 교육(ILT, Instructor-Led Training)**: AWS 공인 강사가 진행하는 교실 또는 가상 교육입니다. 유료이며, 심화 학습에 적합합니다.
- **AWS 자격증(Certification)**: AWS는 역할 기반(Cloud Practitioner, Solutions Architect, Developer 등)과 전문 분야(보안, 데이터 분석, 머신러닝 등)의 자격증을 제공합니다.
  - **Foundational**: AWS Certified Cloud Practitioner (CLF-C02) — 바로 여러분이 준비하고 있는 시험입니다!
  - **Associate**: Solutions Architect, Developer, SysOps Administrator
  - **Professional**: Solutions Architect Professional, DevOps Engineer Professional
  - **Specialty**: Security, Machine Learning, Database 등

#### AWS re:Post

> 📝 **AWS re:Post**: AWS가 운영하는 공식 커뮤니티 Q&A 플랫폼입니다. 기존의 AWS 포럼을 대체하여, AWS 전문가와 커뮤니티 멤버가 질문과 답변을 공유합니다.

AWS re:Post의 특징:

- **무료**: 누구나 질문하고 답변할 수 있습니다.
- **AWS 전문가 참여**: AWS 직원과 AWS Heroes(커뮤니티에서 인정받은 전문가)가 답변에 참여합니다.
- **검증된 답변**: 커뮤니티에서 검증된 답변에 표시가 붙어, 신뢰할 수 있는 정보를 빠르게 찾을 수 있습니다.
- **지식 기반**: 기존 AWS 포럼의 축적된 Q&A가 포함되어 있어, 검색만으로도 많은 문제를 해결할 수 있습니다.

> 💬 **참고**: re:Post는 Stack Overflow와 비슷한 형태이지만, AWS에 특화된 공식 플랫폼이라는 점에서 차별화됩니다.

#### AWS 공식 문서 (Documentation)

AWS의 모든 서비스에는 상세한 공식 문서가 제공됩니다:

- **사용자 가이드(User Guide)**: 서비스의 개념 설명과 사용 방법
- **API 레퍼런스(API Reference)**: 프로그래밍 방식으로 서비스를 사용하기 위한 참조 문서
- **모범 사례(Best Practices)**: 서비스를 효과적으로 사용하기 위한 권장 사항
- **FAQ**: 자주 묻는 질문과 답변

공식 문서는 항상 최신 상태로 유지되며, 무료로 접근할 수 있습니다.

#### AWS 백서 (Whitepapers)

> 📝 **AWS 백서(Whitepapers)**: AWS가 발행하는 기술 문서로, 특정 주제(보안, 아키텍처, 마이그레이션 등)에 대한 심층 가이드를 제공합니다.

대표적인 백서:

- **AWS Well-Architected Framework**: AWS 아키텍처 설계의 모범 사례
- **AWS Overview of Amazon Web Services**: AWS 전체 서비스 개요
- **AWS Pricing Overview**: AWS 요금 체계 상세 설명

백서는 무료로 제공되며, 자격증 시험 준비에도 유용합니다.

### 상세 예시 (Detailed Examples)

> 🔍 **예시 23.4.1: 자격증 준비를 위한 학습 경로 설계**
>
> **상황**: 대학생 지영이는 AWS Certified Cloud Practitioner 시험을 준비하려 합니다. AWS를 처음 접하며, 어떤 리소스를 어떤 순서로 활용해야 할지 모릅니다.
> **풀이/설명**: 지영이에게 추천하는 학습 경로는 다음과 같습니다:
> 1. **AWS Skill Builder**에서 "AWS Cloud Practitioner Essentials" 무료 과정 수강 (약 6시간)
> 2. **AWS 공식 문서**에서 주요 서비스(EC2, S3, IAM 등)의 FAQ 읽기
> 3. **AWS re:Post**에서 다른 학습자들의 시험 관련 질문과 답변 탐색
> 4. **AWS Skill Builder**의 시험 준비 과정(Exam Prep) 수강
> 5. **연습 시험(Practice Exam)** 응시하여 약점 파악
>
> 이 모든 과정은 무료(또는 최소 비용)로 진행할 수 있습니다.
> **핵심 포인트**: AWS의 공식 학습 리소스만으로도 체계적인 자격증 준비가 가능합니다.

> 🔍 **예시 23.4.2: 실무 문제 해결을 위한 리소스 활용**
>
> **상황**: 신입 클라우드 엔지니어 태호가 S3 버킷의 접근 권한 설정에서 문제를 겪고 있습니다. 특정 사용자에게만 읽기 권한을 부여하고 싶은데, 방법을 모릅니다.
> **풀이/설명**: 태호는 다음 순서로 문제를 해결할 수 있습니다:
> 1. **AWS S3 공식 문서**의 "버킷 정책(Bucket Policy)" 섹션 검색
> 2. 문서에서 해결이 안 되면 **AWS re:Post**에서 유사한 질문 검색
> 3. 여전히 해결이 안 되면 re:Post에 구체적인 상황을 설명하며 새 질문 작성
>
> **핵심 포인트**: AWS 공식 문서 → 커뮤니티 검색 → 질문 작성의 순서로 문제를 해결하는 것이 효율적입니다.

### 미니 실습 (Hands-on Mini Lab)

> 🧪 **Mini Lab 23.4: AWS Skill Builder와 re:Post 탐색하기**
>
> **목표**: AWS의 주요 학습 리소스인 Skill Builder와 re:Post에 접속하여 어떤 콘텐츠가 제공되는지 직접 탐색합니다.
> **예상 소요 시간**: 10분
> **비용**: 무료
>
> **Step 1**: 웹 브라우저에서 AWS Skill Builder(skillbuilder.aws)에 접속합니다. AWS 계정 또는 Amazon 계정으로 로그인합니다.
> **Step 2**: 상단 검색창에 "Cloud Practitioner"를 검색합니다. "AWS Cloud Practitioner Essentials" 과정을 찾아 클릭하고, 과정 설명과 목차를 확인합니다. (무료 과정인지 확인합니다.)
> **Step 3**: 좌측 메뉴 또는 카테고리에서 "Learning Plans"를 찾아, "Cloud Practitioner" 관련 학습 경로가 어떤 과정들로 구성되어 있는지 확인합니다.
> **Step 4**: 새 탭에서 AWS re:Post(repost.aws)에 접속합니다.
> **Step 5**: re:Post에서 "S3 bucket policy"와 같은 기술 키워드를 검색하여, 어떤 질문과 답변이 있는지 탐색합니다. 답변에 "Accepted answer" 또는 체크 표시가 있는 항목을 확인합니다.
>
> **확인**: Skill Builder에서 무료 학습 과정 목록을 확인할 수 있고, re:Post에서 기술 Q&A를 검색·탐색할 수 있습니다.

### 흔한 실수와 주의사항 (Common Pitfalls)

> ⚠️ **주의**:
> - **"AWS re:Post"와 "AWS 포럼"을 혼동하지 마세요**: 기존의 AWS Discussion Forums는 re:Post로 통합되었습니다. 시험에서는 **re:Post**가 AWS의 공식 커뮤니티 Q&A 플랫폼이라는 점을 기억하세요.
> - **Skill Builder 무료 vs 유료 구분**: Skill Builder의 디지털 과정 대부분은 무료이지만, 일부 실습 랩과 시험 준비 자료는 유료 구독이 필요합니다. 무료 자원만으로도 기본적인 학습은 충분히 가능합니다.

### Section 요약 (Section Summary)

- **AWS Skill Builder**는 수백 개의 무료 디지털 과정과 학습 경로를 제공하는 온라인 학습 플랫폼이다.
- **AWS Training and Certification**은 강사 주도 교육과 자격증 프로그램을 제공한다.
- **AWS re:Post**는 AWS 공식 커뮤니티 Q&A 플랫폼으로, 기존 포럼을 대체했다.
- **AWS 공식 문서**와 **백서**는 서비스별 상세 가이드와 심층 기술 문서를 무료로 제공한다.
- 효과적인 학습 순서는 공식 문서 → 온라인 과정 → 커뮤니티 활용 → 자격증 도전이다.

---

## 23.5 AWS Marketplace와 Partner Network

> 💡 **한 줄 요약**: AWS Marketplace는 서드파티 소프트웨어를 손쉽게 구매·배포하는 디지털 스토어이고, AWS Partner Network(APN)는 AWS와 협력하는 기술·컨설팅 파트너의 생태계입니다.

### 직관적 이해 (Intuitive Understanding)

스마트폰을 구입한 후의 상황을 생각해 봅시다. 폰 자체로도 유용하지만, **앱스토어**에서 다양한 앱을 설치하면 훨씬 더 많은 일을 할 수 있습니다. 또한, 폰을 수리하거나 맞춤 설정이 필요할 때는 **공식 서비스 센터나 공인 대리점**을 찾아가죠.

AWS에서도 비슷합니다:
- **AWS Marketplace** = **앱스토어**: 다양한 서드파티 소프트웨어를 AWS 환경에 바로 설치·사용할 수 있는 디지털 카탈로그입니다.
- **AWS Partner Network(APN)** = **공식 파트너 네트워크**: AWS를 기반으로 솔루션을 구축하거나 컨설팅을 제공하는 전문 기업들의 네트워크입니다.

### 핵심 개념 설명 (Core Explanation)

#### AWS Marketplace

> 📝 **AWS Marketplace**: AWS에서 실행되는 서드파티 소프트웨어 및 서비스를 검색, 구매, 배포할 수 있는 디지털 카탈로그입니다.

AWS Marketplace의 주요 특징:

- **다양한 카테고리**: 보안, 네트워킹, 스토리지, 머신러닝, 비즈니스 애플리케이션 등 수천 개의 소프트웨어가 등록되어 있습니다.
- **다양한 제공 형태**:
  - **AMI(Amazon Machine Image)**: EC2에 바로 배포할 수 있는 사전 구성된 서버 이미지
  - **SaaS(Software as a Service)**: 별도 설치 없이 바로 사용하는 구독형 서비스
  - **컨테이너**: 컨테이너 이미지로 배포 가능한 소프트웨어
  - **데이터 제품**: 데이터 세트나 데이터 피드
- **통합 결제**: Marketplace에서 구매한 소프트웨어 비용이 **AWS 청구서에 통합**되어 청구됩니다. 별도의 결제 과정이 필요하지 않습니다.
- **무료 체험**: 많은 소프트웨어가 무료 체험 기간을 제공합니다.
- **계약 유연성**: 시간당, 월별, 연간, BYOL(Bring Your Own License — 기존 라이선스 사용) 등 다양한 요금 모델을 지원합니다.

> 🔗 **연결**: Chapter 4에서 배운 AWS 프리 티어처럼, Marketplace의 많은 소프트웨어도 무료 체험이 가능합니다. 다만, Marketplace 소프트웨어를 실행하기 위한 AWS 인프라 비용(예: EC2 인스턴스 비용)은 별도로 발생할 수 있습니다.

#### AWS Partner Network (APN)

> 📝 **AWS Partner Network (APN)**: AWS를 기반으로 솔루션을 구축하거나 서비스를 제공하는 기업들의 글로벌 파트너 프로그램입니다.

APN에는 두 가지 주요 유형의 파트너가 있습니다:

**1) 기술 파트너 (Technology Partners)**
- AWS에서 실행되거나 AWS와 통합되는 **소프트웨어 솔루션**을 제공하는 기업
- 예: Datadog(모니터링), Splunk(로그 분석), Trend Micro(보안)

**2) 컨설팅 파트너 (Consulting Partners)**
- AWS를 활용한 **설계, 구축, 마이그레이션, 운영**을 도와주는 전문 서비스 기업
- 예: AWS 클라우드 마이그레이션 전문 컨설팅사, 관리형 서비스 제공업체(MSP)

APN 파트너는 역량에 따라 등급이 나뉩니다:
- **Select Tier**: APN 가입 초기 단계
- **Advanced Tier**: 일정 수준의 AWS 역량과 고객 사례를 갖춘 파트너
- **Premier Tier**: 최고 수준의 AWS 전문성과 고객 성공 사례를 갖춘 파트너

### 상세 예시 (Detailed Examples)

> 🔍 **예시 23.5.1: Marketplace를 통한 보안 솔루션 도입**
>
> **상황**: 중소기업 G사는 AWS에서 웹 서비스를 운영 중이며, 침입 탐지 시스템(IDS)이 필요합니다. 하지만 보안 소프트웨어를 직접 설치하고 구성하는 것은 복잡하고 시간이 많이 걸립니다.
> **풀이/설명**: G사는 AWS Marketplace에서 "IDS" 또는 "intrusion detection"을 검색하여 검증된 보안 솔루션을 찾을 수 있습니다. 원하는 솔루션을 선택하면 몇 번의 클릭으로 AWS 환경에 배포됩니다. 비용은 AWS 청구서에 통합되어 별도의 계약이나 결제 과정이 필요하지 않습니다. 무료 체험이 가능한 솔루션을 먼저 테스트해본 후 결정할 수도 있습니다.
> **핵심 포인트**: AWS Marketplace는 서드파티 소프트웨어의 검색·구매·배포를 단순화하고, AWS 결제에 통합하여 관리 부담을 줄여줍니다.

> 🔍 **예시 23.5.2: APN 컨설팅 파트너를 통한 클라우드 마이그레이션**
>
> **상황**: 전통 제조업체 H사는 사내 서버(온프레미스)에서 운영 중인 ERP 시스템을 AWS로 마이그레이션하려 합니다. 하지만 사내에 클라우드 전문 인력이 없어 어디서부터 시작해야 할지 모릅니다.
> **풀이/설명**: H사는 APN의 **컨설팅 파트너**를 활용할 수 있습니다. AWS 파트너 찾기(AWS Partner Finder)에서 "ERP migration" 또는 "manufacturing" 키워드로 전문 파트너를 검색합니다. Advanced 또는 Premier Tier 파트너 중에서 유사한 프로젝트 경험이 있는 기업을 선택하면, 마이그레이션 계획 수립부터 실행, 최적화까지 전문적인 지원을 받을 수 있습니다.
> **핵심 포인트**: 클라우드 전문 인력이 부족한 조직은 APN 컨설팅 파트너를 통해 전문성을 확보할 수 있습니다.

### 미니 실습 (Hands-on Mini Lab)

> 🧪 **Mini Lab 23.5: AWS Marketplace 탐색하기**
>
> **목표**: AWS Marketplace에서 어떤 소프트웨어가 제공되는지 직접 탐색하고, 요금 모델과 배포 옵션을 확인합니다.
> **예상 소요 시간**: 5분
> **비용**: 무료 (탐색만 수행하며, 실제 구매하지 않습니다)
>
> **Step 1**: AWS Management Console에 로그인한 상태에서, 상단 검색창에 `Marketplace`를 입력하고 **AWS Marketplace**를 클릭합니다. (또는 웹 브라우저에서 aws.amazon.com/marketplace에 직접 접속합니다.)
> **Step 2**: Marketplace 홈 화면에서 카테고리를 탐색합니다. "Security", "Machine Learning", "Business Applications" 등의 카테고리를 클릭하여 어떤 소프트웨어가 있는지 둘러봅니다.
> **Step 3**: 검색창에 관심 있는 키워드(예: "WordPress", "monitoring", "firewall")를 입력하여 검색합니다.
> **Step 4**: 검색 결과에서 아무 소프트웨어를 하나 클릭하여 상세 페이지를 확인합니다. **요금 정보(Pricing Information)**, **제공 형태(Delivery Method — AMI, SaaS 등)**, **무료 체험 여부**를 확인합니다.
> **Step 5**: "Free Tier eligible" 또는 "Free trial" 필터를 적용하여 무료로 체험할 수 있는 소프트웨어가 얼마나 있는지 확인합니다.
>
> **확인**: Marketplace에서 다양한 카테고리의 서드파티 소프트웨어를 검색할 수 있고, 각 소프트웨어의 요금 모델과 배포 방식을 확인할 수 있습니다.

### 흔한 실수와 주의사항 (Common Pitfalls)

> ⚠️ **주의**:
> - **Marketplace 소프트웨어 비용 ≠ AWS 인프라 비용**: Marketplace에서 "무료"라고 표시된 소프트웨어도, 이를 실행하기 위한 EC2 인스턴스 등의 **인프라 비용은 별도로 발생**합니다. 항상 총 비용을 확인하세요.
> - **APN의 Technology Partner와 Consulting Partner 구분**: 시험에서 이 둘의 차이를 묻는 문제가 나올 수 있습니다. Technology Partner는 **소프트웨어 솔루션**을, Consulting Partner는 **전문 서비스(설계, 구축, 마이그레이션)**를 제공합니다.

### Section 요약 (Section Summary)

- **AWS Marketplace**는 서드파티 소프트웨어를 AWS 환경에 쉽게 배포·구매할 수 있는 디지털 카탈로그이다.
- Marketplace의 소프트웨어 비용은 AWS 청구서에 통합되어 결제 관리가 편리하다.
- **AWS Partner Network(APN)**은 기술 파트너(소프트웨어)와 컨설팅 파트너(전문 서비스)로 구성된다.
- APN 파트너는 Select, Advanced, Premier Tier로 등급이 나뉘며, 높은 등급일수록 더 많은 AWS 전문성을 갖추고 있다.

---

## Chapter 핵심 요약 (Chapter Summary)

이 Chapter에서는 AWS의 지원 체계와 학습 생태계 전반을 살펴보았습니다.

- **Section 23.1**: AWS는 Basic(무료)부터 Enterprise까지 5가지 지원 플랜을 제공하며, 플랜에 따라 기술 지원 채널, 응답 시간, 접근 가능한 서비스가 달라진다.
- **Section 23.2**: Enterprise급 플랜에서는 TAM(전담 기술 관리자), Concierge(결제 전문 팀), IEM(대규모 이벤트 지원), Well-Architected 리뷰 등 선제적이고 맞춤화된 고급 지원을 받을 수 있다.
- **Section 23.3**: 지원 케이스는 5가지 심각도로 분류되며, 심각도와 지원 플랜에 따라 응답 시간 SLA가 결정된다. SLA는 "첫 번째 응답" 시간을 보장한다.
- **Section 23.4**: AWS Skill Builder, Training and Certification, re:Post, 공식 문서, 백서 등 다양한 무료·유료 학습 리소스를 활용하여 체계적으로 AWS를 학습할 수 있다.
- **Section 23.5**: AWS Marketplace는 서드파티 소프트웨어의 디지털 카탈로그이고, APN은 기술 파트너와 컨설팅 파트너로 구성된 파트너 생태계이다.

---

## 핵심 용어 정리 (Glossary)

| 용어 | 정의 | 관련 Section |
|------|------|-------------|
| AWS Support Plan | AWS가 고객에게 제공하는 기술 지원 서비스의 등급 체계 | 23.1 |
| Basic 플랜 | 모든 AWS 계정에 무료로 포함되는 기본 지원 플랜 (기술 지원 불가) | 23.1 |
| Developer 플랜 | 이메일 기술 지원을 제공하는 유료 플랜 (월 $29~) | 23.1 |
| Business 플랜 | 24/7 전화/채팅/이메일 지원을 제공하는 유료 플랜 (월 $100~) | 23.1 |
| Enterprise On-Ramp 플랜 | TAM 풀 접근과 30분 응답 시간을 제공하는 플랜 (월 $5,500~) | 23.1 |
| Enterprise 플랜 | 전담 TAM과 15분 응답 시간을 제공하는 최상위 플랜 (월 $15,000~) | 23.1 |
| TAM (Technical Account Manager) | 고객에게 배정되는 전담 기술 관리자 | 23.2 |
| AWS Concierge Support Team | 계정 및 결제 전문 지원 팀 | 23.2 |
| IEM (Infrastructure Event Management) | 대규모 이벤트 전후로 인프라를 점검·지원하는 서비스 | 23.2 |
| Well-Architected 리뷰 | AWS 모범 사례 프레임워크 기반의 아키텍처 점검 서비스 | 23.2 |
| 지원 케이스 (Support Case) | AWS Support Center를 통해 생성하는 기술/결제 문의 | 23.3 |
| 심각도 (Severity) | 문제가 비즈니스에 미치는 영향의 정도를 나타내는 분류 | 23.3 |
| SLA (Service Level Agreement) | 서비스 제공자가 보장하는 서비스 품질 수준 계약 | 23.3 |
| AWS Skill Builder | AWS 공식 온라인 학습 플랫폼 | 23.4 |
| AWS Training and Certification | AWS 공식 교육 및 자격증 프로그램 | 23.4 |
| AWS re:Post | AWS 공식 커뮤니티 Q&A 플랫폼 | 23.4 |
| AWS 백서 (Whitepapers) | AWS가 발행하는 심층 기술 문서 | 23.4 |
| AWS Marketplace | 서드파티 소프트웨어를 검색·구매·배포하는 디지털 카탈로그 | 23.5 |
| APN (AWS Partner Network) | AWS 기반 솔루션/서비스를 제공하는 파트너 기업들의 네트워크 | 23.5 |
| Technology Partner | APN에서 소프트웨어 솔루션을 제공하는 파트너 유형 | 23.5 |
| Consulting Partner | APN에서 전문 서비스(설계, 구축, 마이그레이션)를 제공하는 파트너 유형 | 23.5 |

---

## 개념 연결 맵 (Connection Map)

- **이전 Chapter와의 연결**:
  - **Chapter 4 (AWS 계정 설정과 관리 콘솔)**: Chapter 4에서 생성한 AWS 계정에는 Basic 지원 플랜이 자동 적용됩니다. 이 Chapter에서는 그 Basic 플랜을 포함한 전체 지원 체계를 학습했습니다.
  - **Chapter 21~22 (요금 모델과 결제 관리)**: Concierge Support Team의 역할을 이해하려면, Chapter 21~22에서 배운 AWS 요금 구조와 결제 관리 도구의 맥락이 도움이 됩니다.

- **다음 Chapter로의 연결**:
  - **Chapter 24 (Well-Architected Framework와 시험 전략)**: 이 Chapter에서 맛보기로 언급한 Well-Architected 리뷰의 기반이 되는 Well-Architected Framework를 Chapter 24에서 상세히 학습합니다. 또한, 이 Chapter에서 배운 학습 리소스 활용법이 Chapter 24의 시험 전략과 자연스럽게 연결됩니다.

---

## 자기 점검 질문 (Self-Check Questions)

**1.** Basic 지원 플랜에서 AWS 기술 지원 엔지니어에게 기술 문의를 할 수 있다. (O/X)

<details>
<summary>정답</summary>

**X** — Basic 플랜에서는 계정 및 결제 관련 문의만 가능합니다. 기술 지원은 Developer 플랜부터 이용할 수 있습니다.
</details>

**2.** Developer 플랜에서 지원 케이스를 생성할 수 있는 사용자 수는?

<details>
<summary>정답</summary>

**루트 사용자 1명만** 지원 케이스를 생성할 수 있습니다. 무제한 사용자가 케이스를 생성하려면 Business 플랜 이상이 필요합니다.
</details>

**3.** 전담 TAM(Technical Account Manager)이 배정되는 지원 플랜은?

<details>
<summary>정답</summary>

**Enterprise 플랜**입니다. Enterprise On-Ramp에서는 전담 TAM이 아닌 TAM 풀(Pool)에 접근할 수 있습니다.
</details>

**4.** Trusted Advisor의 전체 검사(Full Checks)를 이용할 수 있는 최소 지원 플랜은?

<details>
<summary>정답</summary>

**Business 플랜**입니다. Basic과 Developer 플랜에서는 7개의 핵심 검사(Core Checks)만 이용할 수 있습니다.
</details>

**5.** 비즈니스 크리티컬 시스템이 다운되었을 때, Enterprise 플랜에서 보장하는 최초 응답 시간은?

<details>
<summary>정답</summary>

**15분** 이내입니다. Enterprise On-Ramp는 30분 이내입니다.
</details>

**6.** AWS re:Post는 어떤 역할을 하는 서비스인가?

<details>
<summary>정답</summary>

AWS re:Post는 AWS 공식 **커뮤니티 Q&A 플랫폼**입니다. 기존의 AWS Discussion Forums를 대체하며, AWS 전문가와 커뮤니티 멤버가 질문과 답변을 공유합니다.
</details>

**7.** AWS Marketplace에서 구매한 소프트웨어의 비용은 어떻게 청구되는가?

<details>
<summary>정답</summary>

**AWS 청구서에 통합**되어 청구됩니다. 별도의 결제 과정이 필요하지 않으며, AWS 인프라 비용과 함께 하나의 청구서로 관리할 수 있습니다.
</details>

---

## 🧪 통합 실습: AWS 지원 및 학습 생태계 종합 탐색

> **시나리오**: 당신은 스타트업에 합류한 첫 번째 클라우드 엔지니어입니다. CTO가 "우리 회사에 적합한 AWS 지원 플랜을 조사하고, 팀원들이 AWS를 학습할 수 있는 리소스를 정리해달라"고 요청했습니다. 이 실습에서는 AWS의 지원 체계와 학습 리소스를 직접 탐색하여, CTO에게 보고할 정보를 수집합니다.

### 실습 개요

| 항목 | 내용 |
|------|------|
| **목표** | AWS Support Center, Trusted Advisor, Skill Builder, Marketplace를 직접 탐색하고 각각의 역할을 체험한다 |
| **사용 서비스** | AWS Support Center, AWS Trusted Advisor, AWS Skill Builder, AWS Marketplace, AWS re:Post |
| **활용 개념** | Section 23.1 지원 플랜, Section 23.3 지원 케이스, Section 23.4 학습 리소스, Section 23.5 Marketplace |
| **선수 실습** | Chapter 4에서 생성한 AWS 계정 |
| **예상 소요 시간** | 20분 |
| **비용** | 무료 (탐색만 수행) |

### 아키텍처 다이어그램

이 실습은 인프라를 구축하는 것이 아니라, AWS의 지원·학습 생태계를 탐색하는 실습입니다.

```
[AWS Management Console]
        │
        ├──→ [Support Center] ──→ 지원 플랜 확인, 케이스 생성 화면 탐색
        │
        ├──→ [Trusted Advisor] ──→ 핵심 검사 결과 확인
        │
        ├──→ [Marketplace] ──→ 소프트웨어 카탈로그 탐색
        │
        └──→ [외부 사이트]
                ├──→ [Skill Builder] ──→ 학습 과정 탐색
                └──→ [re:Post] ──→ 커뮤니티 Q&A 탐색
```

### 실습 단계

> **Phase 1: Support Center 탐색** (활용 개념: Section 23.1, 23.3)
>
> **Step 1**: AWS Management Console에 로그인합니다.
> **Step 2**: 상단 검색창에 `Support`를 입력하고 **Support Center**를 클릭합니다.
> **Step 3**: 현재 적용된 지원 플랜을 확인합니다 (Basic으로 표시될 것입니다).
> **Step 4**: 왼쪽 메뉴에서 **Create case**를 클릭합니다. "Account and billing support"와 "Technical support" 두 가지 유형이 있는 것을 확인합니다. Basic 플랜에서는 Technical support를 선택할 수 없거나, 선택 후 업그레이드 안내가 표시됩니다.
> **Step 5**: "Account and billing support"를 클릭하여, 케이스 생성 양식에 어떤 정보(서비스, 카테고리, 심각도, 설명 등)를 입력해야 하는지 확인합니다. (**실제 케이스를 제출하지는 않습니다.**)
>
> **✅ 체크포인트**: 현재 플랜이 Basic임을 확인했고, 기술 지원 케이스는 생성할 수 없으며, 계정/결제 케이스의 생성 양식을 확인했습니다.

> **Phase 2: Trusted Advisor 탐색** (활용 개념: Section 23.1)
>
> **Step 1**: Support Center 왼쪽 메뉴에서 **Trusted Advisor**를 클릭하거나, 상단 검색창에서 `Trusted Advisor`를 검색하여 접속합니다.
> **Step 2**: Trusted Advisor 대시보드에서 표시되는 검사 카테고리(비용 최적화, 성능, 보안, 내결함성, 서비스 한도)를 확인합니다.
> **Step 3**: Basic 플랜에서 이용 가능한 핵심 검사 항목을 확인합니다. 일부 검사 옆에 자물쇠 아이콘이나 "Upgrade" 표시가 있을 수 있는데, 이는 Business 이상의 플랜에서만 이용 가능한 검사입니다.
> **Step 4**: 이용 가능한 검사 중 하나를 클릭하여, 어떤 권장 사항이 표시되는지 확인합니다.
>
> **✅ 체크포인트**: Trusted Advisor에서 Basic 플랜으로 확인할 수 있는 검사 항목과 제한된 항목을 구분할 수 있습니다.

> **Phase 3: 학습 리소스 탐색** (활용 개념: Section 23.4)
>
> **Step 1**: 새 브라우저 탭에서 AWS Skill Builder(skillbuilder.aws)에 접속하고 로그인합니다.
> **Step 2**: "Cloud Practitioner"로 검색하여 관련 무료 과정을 2~3개 확인합니다. 과정의 예상 소요 시간과 내용을 메모합니다.
> **Step 3**: 또 다른 탭에서 AWS re:Post(repost.aws)에 접속합니다.
> **Step 4**: re:Post에서 본인이 관심 있는 AWS 서비스(예: "EC2", "Lambda", "S3")를 검색하여 Q&A를 탐색합니다.
>
> **✅ 체크포인트**: Skill Builder에서 Cloud Practitioner 관련 무료 과정을 찾았고, re:Post에서 기술 Q&A를 검색할 수 있습니다.

> **Phase 4: Marketplace 탐색** (활용 개념: Section 23.5)
>
> **Step 1**: AWS Management Console로 돌아가서, 상단 검색창에 `Marketplace`를 입력하고 **AWS Marketplace**를 클릭합니다.
> **Step 2**: "Security" 카테고리를 탐색하여 어떤 보안 솔루션이 있는지 확인합니다.
> **Step 3**: 하나의 소프트웨어를 클릭하여 상세 페이지에서 **요금 모델**(시간당, 월별, 무료 체험 등)과 **제공 형태**(AMI, SaaS 등)를 확인합니다.
>
> **✅ 체크포인트**: Marketplace에서 소프트웨어를 검색하고, 요금 모델과 배포 방식을 확인할 수 있습니다.

### 최종 확인

모든 Phase를 완료하면, 다음 정보를 직접 확인한 것입니다:
- 현재 AWS 계정의 지원 플랜(Basic)과 그 제한 사항
- Trusted Advisor에서 Basic 플랜으로 확인할 수 있는 검사 항목
- AWS Skill Builder와 re:Post의 학습 리소스
- AWS Marketplace의 소프트웨어 카탈로그와 요금 체계

이 정보를 바탕으로 "우리 스타트업에는 어떤 지원 플랜이 적합한가?", "팀원 학습에 어떤 리소스를 활용할 것인가?"에 대한 보고서를 작성할 수 있습니다.

### 🧹 리소스 정리 (Clean-up)

> 이 실습에서는 AWS 리소스를 생성하지 않았으므로, **별도의 정리가 필요하지 않습니다.** 지원 케이스도 실제로 제출하지 않았으므로 삭제할 항목이 없습니다.

### 트러블슈팅 (Troubleshooting)

> **Q: Support Center에서 "Create case" 버튼이 보이지 않습니다.**
> A: AWS 계정에 로그인된 상태인지 확인하세요. IAM 사용자로 로그인한 경우, Support 관련 IAM 권한이 없을 수 있습니다. 루트 사용자로 로그인하면 확인할 수 있습니다.

> **Q: Trusted Advisor에 아무 검사 결과도 표시되지 않습니다.**
> A: 계정을 생성한 지 얼마 되지 않거나, AWS 서비스를 거의 사용하지 않은 경우 검사 결과가 제한적일 수 있습니다. 이는 정상이며, 서비스 사용이 늘어나면 더 많은 권장 사항이 표시됩니다.

> **Q: Skill Builder에 로그인이 안 됩니다.**
> A: Skill Builder는 AWS Management Console 계정과 별도의 로그인을 사용할 수 있습니다. "Sign In" 후 "Amazon" 계정 또는 "AWS Builder ID"로 로그인을 시도해 보세요. 새 계정을 생성해야 할 수도 있습니다.

---

## 문제 풀이 (Problem Set)

### Practice (연습 문제) — 기본 개념 확인

> **Practice 23.1**: 다음 중 모든 AWS 계정에 무료로 포함되는 지원 플랜은?
> A) Developer
> B) Basic
> C) Business
> D) Enterprise On-Ramp
>
> <details>
> <summary>정답 및 해설</summary>
>
> **정답**: B) Basic
> **해설**: Basic 플랜은 모든 AWS 계정에 자동으로 포함되는 무료 플랜입니다. 고객 서비스(계정/결제 문의), AWS 문서, Trusted Advisor 핵심 검사, Personal Health Dashboard에 접근할 수 있습니다.
> </details>

> **Practice 23.2**: Basic 지원 플랜에서 할 수 **없는** 것은?
> A) AWS 공식 문서 열람
> B) 결제 관련 문의
> C) 기술 지원 엔지니어에게 이메일 기술 문의
> D) Personal Health Dashboard 확인
>
> <details>
> <summary>정답 및 해설</summary>
>
> **정답**: C) 기술 지원 엔지니어에게 이메일 기술 문의
> **해설**: 이메일 기술 문의는 Developer 플랜부터 가능합니다. Basic 플랜에서는 기술 지원 엔지니어에게 직접 문의할 수 없고, 계정/결제 관련 문의만 가능합니다.
> </details>

> **Practice 23.3**: Trusted Advisor의 전체 검사(Full Checks)를 이용할 수 있는 최소 지원 플랜은?
> A) Basic
> B) Developer
> C) Business
> D) Enterprise On-Ramp
>
> <details>
> <summary>정답 및 해설</summary>
>
> **정답**: C) Business
> **해설**: Basic과 Developer 플랜에서는 7개의 핵심 검사(Core Checks)만 이용 가능합니다. Business 플랜부터 비용 최적화, 보안, 성능, 내결함성, 서비스 한도 등 전체 검사에 접근할 수 있습니다.
> </details>

> **Practice 23.4**: TAM(Technical Account Manager)이 고객에게 **전담으로** 배정되는 지원 플랜은?
> A) Business
> B) Enterprise On-Ramp
> C) Enterprise
> D) Business와 Enterprise 모두
>
> <details>
> <summary>정답 및 해설</summary>
>
> **정답**: C) Enterprise
> **해설**: 전담 TAM은 Enterprise 플랜에서만 배정됩니다. Enterprise On-Ramp에서는 TAM 풀(Pool)에 접근할 수 있지만, 전담 TAM은 아닙니다.
> </details>

> **Practice 23.5**: AWS의 공식 커뮤니티 Q&A 플랫폼은 무엇인가?
> A) AWS Forums
> B) AWS re:Post
> C) AWS Support Center
> D) AWS Skill Builder
>
> <details>
> <summary>정답 및 해설</summary>
>
> **정답**: B) AWS re:Post
> **해설**: AWS re:Post는 기존의 AWS Discussion Forums를 대체한 공식 커뮤니티 Q&A 플랫폼입니다. AWS 전문가와 커뮤니티 멤버가 질문과 답변을 공유합니다.
> </details>

> **Practice 23.6**: AWS Marketplace에서 구매한 소프트웨어의 비용은 어떻게 청구되는가?
> A) 소프트웨어 벤더에게 별도 결제
> B) AWS 청구서에 통합하여 청구
> C) AWS 크레딧으로만 결제 가능
> D) 무료로만 제공
>
> <details>
> <summary>정답 및 해설</summary>
>
> **정답**: B) AWS 청구서에 통합하여 청구
> **해설**: AWS Marketplace에서 구매한 소프트웨어 비용은 AWS 인프라 비용과 함께 하나의 AWS 청구서로 통합 청구됩니다. 별도의 결제 과정이 필요하지 않아 관리가 편리합니다.
> </details>

> **Practice 23.7**: 비즈니스 크리티컬 시스템이 완전히 다운되었을 때, Enterprise 플랜에서 보장하는 첫 응답 시간은?
> A) 1시간
> B) 30분
> C) 15분
> D) 5분
>
> <details>
> <summary>정답 및 해설</summary>
>
> **정답**: C) 15분
> **해설**: Enterprise 플랜에서 "비즈니스 크리티컬 시스템 다운" 심각도의 케이스에는 15분 이내에 첫 번째 응답이 보장됩니다. Enterprise On-Ramp에서는 30분입니다.
> </details>

---

### Exercise (응용 문제) — 개념 적용 및 통합

> **Exercise 23.1**: 다음 세 회사에 각각 어떤 지원 플랜을 추천하시겠습니까? 이유를 포함하여 설명하세요.
>
> - **회사 A**: 대학생 3명이 졸업 프로젝트로 AWS를 사용. 월 사용료 $50 이하.
> - **회사 B**: 직원 50명의 전자상거래 회사. AWS에서 프로덕션 웹사이트를 운영하며, 장애 시 매출 손실이 큼.
> - **회사 C**: 글로벌 금융 기업. AWS에서 핵심 거래 시스템을 운영하며, 분 단위의 장애도 수억 원의 손실로 이어짐.
>
> <details>
> <summary>모범 답안</summary>
>
> **접근 방법**: 각 회사의 워크로드 중요도, 필요한 응답 속도, 예산, 팀 규모를 고려합니다.
>
> **풀이 과정**:
>
> - **회사 A → Basic 또는 Developer 플랜**
>   - 졸업 프로젝트이므로 프로덕션 워크로드가 아닙니다. 기술적인 질문이 있으면 AWS 공식 문서, Skill Builder, re:Post를 활용할 수 있습니다.
>   - 가끔 기술 문의가 필요하면 Developer 플랜($29/월)을 고려할 수 있지만, 무료 리소스만으로도 충분히 해결 가능한 수준이라면 Basic 플랜(무료)이 적절합니다.
>
> - **회사 B → Business 플랜**
>   - 프로덕션 웹사이트를 운영하고, 장애 시 매출 손실이 있으므로 빠른 응답이 필요합니다.
>   - 직원 50명이 AWS를 사용하므로, 무제한 사용자가 지원 케이스를 생성할 수 있는 Business 플랜이 적합합니다.
>   - 24/7 전화/채팅 지원, 프로덕션 시스템 다운 시 1시간 응답, Trusted Advisor 전체 검사 등이 필요합니다.
>
> - **회사 C → Enterprise 플랜**
>   - 핵심 거래 시스템으로 분 단위 장애가 수억 원의 손실이므로, 15분 응답 시간이 보장되는 Enterprise 플랜이 필수적입니다.
>   - 전담 TAM이 선제적으로 인프라를 관리하고, IEM으로 대규모 이벤트(결산일, 프로모션 등)에 대비할 수 있습니다.
>   - Well-Architected 리뷰를 통해 아키텍처를 지속적으로 최적화할 수 있습니다.
>
> **보충 설명**: 지원 플랜 선택의 핵심은 "장애가 발생했을 때 비즈니스에 미치는 영향"과 "그 영향을 줄이기 위해 지불할 의향이 있는 비용"의 균형입니다. 월 $15,000의 Enterprise 비용이 크게 느껴질 수 있지만, 1시간 장애로 수억 원이 날아가는 상황에서는 합리적인 투자입니다.
> </details>

> **Exercise 23.2**: AWS Concierge Support Team과 TAM의 역할 차이를 설명하고, 각각 어떤 상황에서 도움을 요청해야 하는지 구체적인 시나리오를 들어 설명하세요.
>
> <details>
> <summary>모범 답안</summary>
>
> **접근 방법**: 두 서비스의 전문 분야(기술 vs 결제)를 구분하고, 실제 상황에 대입합니다.
>
> **풀이 과정**:
>
> | 구분 | TAM | Concierge Support Team |
> |------|-----|----------------------|
> | **전문 분야** | 기술(아키텍처, 운영, 최적화) | 계정 및 결제 |
> | **역할** | 선제적 기술 관리, 아키텍처 리뷰, 이벤트 조율 | 결제 구조 상담, 계정 모범 사례 안내 |
> | **제공 플랜** | Enterprise On-Ramp(풀), Enterprise(전담) | Enterprise On-Ramp, Enterprise |
>
> **TAM에게 도움을 요청하는 시나리오**:
> - "다음 달에 신규 서비스를 출시하는데, 현재 아키텍처가 예상 트래픽을 감당할 수 있을까요?"
> - "EC2 인스턴스 유형을 변경하려는데, 성능과 비용 면에서 최적의 선택은 무엇인가요?"
>
> **Concierge에게 도움을 요청하는 시나리오**:
> - "이번 달 청구서에서 예상보다 높은 금액이 나왔는데, 원인을 분석해주실 수 있나요?"
> - "AWS Organizations에서 여러 계정의 통합 결제를 구성하고 싶은데, 모범 사례를 안내해주세요."
>
> **보충 설명**: 간단히 기억하는 방법은 "기술적인 문제 → TAM", "돈과 계정 문제 → Concierge"입니다.
> </details>

> **Exercise 23.3**: 다음 상황에서 각각 적절한 지원 케이스 심각도를 선택하고 그 이유를 설명하세요.
>
> - **상황 1**: 개발 환경에서 사용 중인 Lambda 함수의 콜드 스타트 시간이 평소보다 느려진 것 같습니다.
> - **상황 2**: 프로덕션 웹 애플리케이션의 로그인 기능이 간헐적으로 실패하며, 일부 고객이 불편을 겪고 있습니다.
> - **상황 3**: 프로덕션 데이터베이스에 완전히 접속이 불가능하여 모든 서비스가 중단되었고, 우회 방법이 없습니다.
>
> <details>
> <summary>모범 답안</summary>
>
> **접근 방법**: 각 상황의 비즈니스 영향도와 우회 가능 여부를 기준으로 심각도를 판단합니다.
>
> **풀이 과정**:
>
> - **상황 1 → "시스템 손상" (System Impaired)**
>   - 개발 환경의 문제이므로 비즈니스에 즉각적인 영향이 없습니다.
>   - 기능이 완전히 중단된 것이 아니라 성능이 저하된 상태입니다.
>   - "일반 안내"보다는 긴급하지만, 프로덕션 영향은 없으므로 "시스템 손상"이 적절합니다.
>
> - **상황 2 → "프로덕션 시스템 손상" (Production System Impaired)**
>   - 프로덕션 환경이며 고객에게 영향이 있지만, "간헐적" 실패이므로 완전 중단은 아닙니다.
>   - 일부 고객은 정상적으로 로그인할 수 있으므로 우회가 부분적으로 가능합니다.
>   - Business 플랜 이상에서 선택 가능하며, 4시간 이내 응답이 보장됩니다.
>
> - **상황 3 → "프로덕션 시스템 다운" (Production System Down) 또는 "비즈니스 크리티컬 시스템 다운"**
>   - 전체 서비스가 중단되었고 우회 방법이 없으므로, 최소한 "프로덕션 시스템 다운"입니다.
>   - 비즈니스에 심각한 재정적 영향이 있다면 "비즈니스 크리티컬 시스템 다운"을 선택합니다 (Enterprise On-Ramp 이상).
>   - Business 플랜이면 1시간, Enterprise On-Ramp이면 30분, Enterprise이면 15분 이내 응답이 보장됩니다.
>
> **보충 설명**: 심각도 선택의 핵심은 "실제 비즈니스 영향"입니다. 개발 환경의 문제를 과도하게 높은 심각도로 신고하는 것은 부적절하며, 반대로 프로덕션 완전 중단을 낮은 심각도로 신고하면 대응이 늦어질 수 있습니다.
> </details>

---

### Problem (심화 문제) — 깊이 있는 사고와 창의적 문제 해결

> **Problem 23.1**: 당신은 빠르게 성장 중인 SaaS 기업의 클라우드 아키텍트입니다. 현재 Business 플랜을 사용 중이며, 다음 분기에 Enterprise 플랜으로 업그레이드할지 검토하라는 요청을 받았습니다.
>
> 다음 조건을 고려하여, (1) 업그레이드 여부에 대한 의견과 (2) 의사결정 기준을 제시하세요:
> - 월 AWS 사용료: 약 $200,000
> - 서비스: 글로벌 전자상거래 플랫폼 (24/7 운영)
> - 연간 대규모 프로모션 이벤트: 3회 (블랙 프라이데이, 연말 세일 등)
> - 최근 6개월간 프로덕션 장애: 2건 (각각 복구에 3시간, 5시간 소요)
> - 사내 AWS 전문 인력: 3명
>
> <details>
> <summary>풀이 가이드</summary>
>
> **핵심 아이디어**: 지원 플랜 업그레이드의 비용-편익 분석은 "지원 비용" vs "장애로 인한 손실 방지 가치 + 운영 효율화 가치"의 비교입니다.
>
> **풀이 전략**:
>
> **1) 비용 분석**
> - Enterprise 플랜 최소 비용: $15,000/월
> - 실제 비용은 AWS 사용료($200,000)의 일정 비율과 최소 금액 중 큰 값이 적용되므로, 실제로는 $15,000보다 높을 수 있습니다. (구체적인 비율은 AWS에 직접 확인이 필요합니다.)
> - 연간 추가 비용: 대략 $180,000~$240,000 수준으로 추정됩니다.
>
> **2) 편익 분석**
> - **장애 복구 시간 단축**: Enterprise의 15분 응답(vs Business의 1시간) + 전담 TAM의 사전 대응으로 장애 복구 시간을 크게 줄일 수 있습니다. 최근 6개월간 8시간의 장애가 있었고, 이 기간의 매출 손실을 계산하면 Enterprise 비용을 상쇄할 수 있는지 판단할 수 있습니다.
> - **IEM 활용**: 연 3회 대규모 이벤트에 IEM을 무제한 활용할 수 있습니다. 이벤트 중 장애 예방 효과는 매출 보호에 직접적으로 기여합니다.
> - **TAM의 선제적 관리**: 3명의 AWS 전문 인력으로 $200,000 규모의 인프라를 관리하는 것은 쉽지 않습니다. 전담 TAM이 아키텍처 최적화와 비용 절감을 도와줌으로써 팀의 부담을 줄이고, 잠재적인 비용 절감도 기대할 수 있습니다.
>
> **3) 의사결정 기준**
> - 프로덕션 장애 시 시간당 매출 손실이 Enterprise 추가 비용의 연간 총액을 넘기는가?
> - 대규모 이벤트의 매출 규모가 IEM 활용 가치를 정당화하는가?
> - 사내 인력 3명의 역량으로 현재 인프라를 안정적으로 관리할 수 있는가, 아니면 TAM의 지원이 필요한가?
>
> **결론**: 월 $200,000 규모의 글로벌 24/7 전자상거래 플랫폼이라면, Enterprise 플랜 업그레이드를 **강력히 권장**합니다. 연 3회의 대규모 이벤트에서의 IEM 활용, 전담 TAM의 선제적 관리, 15분 응답 시간은 이 규모의 비즈니스에서 충분히 비용을 정당화합니다.
>
> **확장 생각**: 더 나아가, Enterprise 플랜의 비용을 단순히 "지원 비용"이 아니라 "보험"으로 바라보는 관점도 있습니다. 장애가 발생하지 않으면 낭비처럼 보일 수 있지만, TAM의 선제적 관리가 장애 자체를 예방하는 효과가 있으므로, "장애가 적었기 때문에 불필요했다"가 아니라 "지원이 있었기 때문에 장애가 적었다"일 수 있습니다.
> </details>

> **Problem 23.2**: 당신은 500명 규모의 IT 기업에서 AWS 교육 프로그램을 설계하는 담당자입니다. 팀의 구성은 다음과 같습니다:
>
> - 경영진 (10명): AWS 비용과 전략적 의미만 이해하면 됨
> - 프로젝트 매니저 (30명): AWS 서비스의 기본 개념과 제약을 이해해야 함
> - 개발자 (200명): 실제로 AWS 서비스를 사용하여 애플리케이션을 구축함
> - 인프라 엔지니어 (50명): AWS 인프라 설계, 배포, 운영을 담당함
> - 신입사원 (50명, 연간): AWS 경험 없음, 역할은 배정 후 결정
>
> AWS의 공식 학습 리소스(Skill Builder, Training and Certification 등)를 활용하여, 각 그룹에 적합한 학습 경로를 설계하세요. 자격증 취득 권장 여부도 포함하세요.
>
> <details>
> <summary>풀이 가이드</summary>
>
> **핵심 아이디어**: 효과적인 교육 프로그램은 역할별 필요 깊이(depth)에 맞춰 차별화되어야 합니다. 모든 사람에게 같은 수준의 교육을 제공하는 것은 비효율적입니다.
>
> **풀이 전략**:
>
> **1) 경영진 (10명)**
> - **학습 경로**: AWS Skill Builder의 "AWS Cloud for Business Leaders" 또는 유사한 비기술 임원 과정 (2~4시간)
> - **핵심 내용**: 클라우드의 비즈니스 가치, TCO(총 소유 비용) 절감, AWS 요금 모델 개요
> - **자격증**: Cloud Practitioner를 선택적으로 권장 (필수는 아님)
> - **이유**: 경영진에게는 기술 깊이보다 전략적 의사결정에 필요한 개념 이해가 중요합니다.
>
> **2) 프로젝트 매니저 (30명)**
> - **학습 경로**: Skill Builder의 "AWS Cloud Practitioner Essentials" (6시간) + 주요 서비스 개요 과정
> - **핵심 내용**: AWS 주요 서비스의 역할과 제약, 아키텍처 기본 개념, 비용 추정 방법
> - **자격증**: **AWS Certified Cloud Practitioner** 권장
> - **이유**: PM은 기술팀과 소통할 때 AWS 서비스의 가능성과 제약을 이해해야 프로젝트를 효과적으로 관리할 수 있습니다.
>
> **3) 개발자 (200명)**
> - **학습 경로**: Skill Builder의 "Developing on AWS" 학습 경로 + 실습 랩 (Skill Builder 구독 활용)
> - **핵심 내용**: SDK 사용법, Lambda, API Gateway, DynamoDB, S3 등 개발에 직접 관련된 서비스
> - **자격증**: **AWS Certified Developer - Associate** 권장
> - **이유**: 개발자는 실제로 코드를 작성하고 서비스를 사용하므로, 이론보다 실습 중심의 학습이 효과적입니다. Skill Builder 유료 구독의 실습 랩을 적극 활용합니다.
>
> **4) 인프라 엔지니어 (50명)**
> - **학습 경로**: Skill Builder의 "Architecting on AWS" 학습 경로 + AWS 강사 주도 교육(ILT) 수강 권장
> - **핵심 내용**: VPC, EC2, RDS, IAM, CloudFormation, 모니터링, 보안 등 인프라 전반
> - **자격증**: **AWS Certified Solutions Architect - Associate** → 이후 Professional 레벨 권장
> - **이유**: 인프라 엔지니어는 가장 깊은 수준의 이해가 필요합니다. 강사 주도 교육은 비용이 들지만, 실시간 질의응답과 심화 학습이 가능합니다.
>
> **5) 신입사원 (50명/연)**
> - **학습 경로**: 입사 후 2주 이내에 Skill Builder의 "AWS Cloud Practitioner Essentials" 이수 → 역할 배정 후 해당 그룹의 학습 경로 진행
> - **자격증**: 입사 3개월 이내 **Cloud Practitioner** 취득을 필수로 설정
> - **보충**: re:Post를 "질문하기 전에 먼저 검색하는 습관"의 도구로 안내합니다.
>
> **확장 생각**: 이 교육 프로그램의 효과를 극대화하려면, 자격증 취득에 대한 인센티브(시험 비용 지원, 보상금 등)를 제공하고, 분기별로 학습 진행 상황을 추적하는 것이 좋습니다. Skill Builder의 팀 구독 플랜을 활용하면 전사적으로 학습 현황을 관리할 수 있습니다.
> </details>

---

## 다음 단계 안내 (What's Next)

축하합니다! Chapter 23에서 AWS의 지원 플랜과 학습 생태계를 모두 학습했습니다.

다음 **Chapter 24: Well-Architected Framework와 시험 전략**에서는 AWS가 제안하는 아키텍처 설계의 모범 사례 프레임워크를 학습하고, 지금까지 배운 모든 내용을 종합하여 AWS Certified Cloud Practitioner(CLF-C02) 시험을 준비하는 전략을 다룹니다. 이 Chapter에서 배운 지원 플랜 지식과 학습 리소스 활용법이 시험 준비에 직접적으로 도움이 될 것입니다.

---

## 추가 학습 자원 (Further Resources)

- **AWS Support Plans 공식 페이지**: AWS 지원 플랜의 최신 요금과 기능 비교를 확인할 수 있습니다.
- **AWS Skill Builder** (skillbuilder.aws): 무료 및 유료 학습 과정, 실습 랩, 시험 준비 자료를 제공합니다.
- **AWS re:Post** (repost.aws): AWS 공식 커뮤니티 Q&A 플랫폼입니다.
- **AWS Training and Certification 공식 페이지**: 강사 주도 교육 일정, 자격증 시험 등록 등을 확인할 수 있습니다.
- **AWS Well-Architected Framework 백서**: Chapter 24의 선행 학습 자료로 추천합니다.
- **AWS Marketplace** (aws.amazon.com/marketplace): 서드파티 소프트웨어 카탈로그를 탐색할 수 있습니다.