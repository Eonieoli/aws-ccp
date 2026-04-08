# Chapter 19: 배포 자동화와 Infrastructure as Code

> **난이도**: ⭐⭐ | **예상 학습 시간**: 2.5시간 | **선수 지식**: Chapter 5

---

## 학습 목표 (Learning Objectives)

이 Chapter를 완료하면, 당신은 다음을 할 수 있습니다:

- [ ] Infrastructure as Code(IaC)의 개념과 수동 인프라 관리 대비 이점을 설명할 수 있다
- [ ] AWS CloudFormation의 템플릿 구조와 스택 생명주기(생성/업데이트/삭제)를 이해하고 콘솔에서 실습할 수 있다
- [ ] AWS CDK와 SAM의 역할과 CloudFormation과의 관계를 구분할 수 있다
- [ ] CI/CD 파이프라인의 개념과 CodeBuild, CodePipeline의 역할을 설명할 수 있다
- [ ] 인프라 자동화가 가져오는 반복 가능성, 일관성, 버전 관리의 이점을 실제 시나리오에 적용하여 설명할 수 있다

---

## 핵심 질문 (Essential Questions)

1. **왜 AWS 콘솔에서 클릭으로 만든 인프라를 "코드"로 다시 작성해야 할까?** — 수동으로 만들면 빠르고 간편한데, 굳이 코드로 관리하는 것이 어떤 가치를 가질까?
2. **코드를 수정할 때마다 사람이 직접 서버에 배포해야 한다면, 어떤 문제가 생길까?** — 배포 과정을 자동화하면 어떤 실수를 방지하고, 어떤 속도를 얻을 수 있을까?
3. **인프라도 코드처럼 "버전 관리"하고 "롤백"할 수 있다면?** — 어제의 인프라 상태로 되돌리거나, 똑같은 환경을 10개 만드는 일이 가능할까?

---

## 개념 지도 (Concept Map)

```
[선수: EC2, 인프라 리소스 개념, AMI, 보안 그룹]                    ← Chapter 5
        │
        ▼
┌──────────────────── 배포 자동화와 IaC ────────────────────┐
│                                                            │
│  [신규: IaC 개념] ──→ [신규: CloudFormation]               │
│   (코드로 인프라      (템플릿, 스택, 드리프트 감지)          │
│    관리하는 패러다임)                                       │
│        │                     │                             │
│        ▼                     ▼                             │
│  [신규: CDK]           [신규: SAM]                         │
│  (프로그래밍 언어로     (서버리스 전용                       │
│   IaC 작성)             IaC 프레임워크)                     │
│                                                            │
│  ─────────────────────────────────────────                 │
│                                                            │
│  [신규: CI/CD 개념] ──→ [신규: CodeBuild]                  │
│   (지속적 통합/배포)     (빌드 & 테스트)                    │
│        │                     │                             │
│        ▼                     ▼                             │
│  [신규: CodePipeline] ← 오케스트레이션                     │
│  (파이프라인 관리)                                         │
│        │                                                   │
│        ▼                                                   │
│  [신규: 추가 도구] ── Amplify, Cloud9, CodeArtifact        │
└────────────────────────────────────────────────────────────┘
        │
        ▼
[이후: Ch 24 Well-Architected Framework — 운영 우수성 원칙]
```

---

## 실습 환경 안내 (Lab Prerequisites)

> 🧪 **실습 환경 안내**
>
> **필요 계정**: AWS 계정 (Free Tier 활성 상태 권장)
> **사용 서비스**: CloudFormation, S3 (CloudFormation 실습용), CodePipeline (콘솔 탐색)
> **예상 비용**: Free Tier 범위 내 (CloudFormation 자체는 무료, 생성되는 리소스에 대해서만 과금)
> **사전 준비**: 특별한 사전 준비 불필요 (Chapter 5의 EC2 개념 이해 필요)
> **리전 설정**: ap-northeast-2 (서울)
>
> 💬 **참고**: CloudFormation 서비스 자체는 무료입니다. 비용은 CloudFormation이 *생성하는 리소스*(예: EC2, S3)에 대해서만 발생합니다. 본 Chapter의 실습은 S3 버킷 생성 등 Free Tier 범위 내에서 진행합니다.

---

## 19.1 Infrastructure as Code 개요

> 💡 **한 줄 요약**: 인프라를 사람의 클릭이 아닌 코드 파일로 정의하여, 반복 가능하고 일관된 환경을 자동으로 만드는 방법론입니다.

### 직관적 이해 (Intuitive Understanding)

여러분이 레고 블록으로 멋진 성을 만들었다고 상상해 보세요. 그런데 친구가 "나도 똑같은 성을 만들고 싶어!"라고 합니다. 어떻게 해야 할까요?

**방법 1 — 수동**: "먼저 빨간 블록을 여기 놓고, 그 위에 파란 블록을 이렇게 놓고…" 하나하나 말로 설명합니다. 시간도 오래 걸리고, 설명을 빠뜨리면 다른 모양이 됩니다.

**방법 2 — 설명서(코드)**: 레고 조립 설명서를 줍니다. 누구든 이 설명서만 따라하면 **언제나 똑같은 성**이 완성됩니다. 10개든 100개든 동일한 결과를 보장합니다.

AWS 인프라 관리도 마찬가지입니다. 지금까지 우리는 AWS 콘솔에서 마우스로 클릭하며 리소스를 만들었습니다. EC2 인스턴스를 하나 만드는 것은 괜찮지만, **동일한 환경을 여러 번 만들어야 하거나**, **누가 무엇을 어떻게 변경했는지 추적**해야 한다면 어떨까요?

> 🔗 **연결**: Chapter 5에서 EC2 인스턴스를 콘솔에서 직접 시작하고 종료하는 실습을 했습니다. 그때 인스턴스 유형을 선택하고, 보안 그룹을 설정하고, 키 페어를 지정하는 과정을 기억하시나요? 이 모든 설정을 "코드 파일"에 미리 적어두면, 클릭 한 번 없이도 동일한 인스턴스를 자동으로 생성할 수 있습니다.

이것이 바로 **Infrastructure as Code(IaC)** — "코드로서의 인프라" 개념이 탄생한 배경입니다.

### 핵심 개념 설명 (Core Explanation)

> 📝 **Infrastructure as Code (IaC)**: 서버, 네트워크, 데이터베이스 등 IT 인프라를 수동 조작이 아닌 **코드 파일(텍스트)로 정의하고 관리**하는 방법론입니다. 이 코드 파일을 실행하면 정의된 대로 인프라가 자동으로 생성, 수정, 삭제됩니다.

#### 수동 관리 vs IaC

| 비교 항목 | 수동 관리 (콘솔 클릭) | IaC (코드) |
|-----------|----------------------|------------|
| **재현성** | 사람마다 결과가 다를 수 있음 | 항상 동일한 결과 보장 |
| **속도** | 리소스가 많을수록 시간 증가 | 수백 개 리소스도 한 번에 생성 |
| **추적성** | 누가 무엇을 변경했는지 알기 어려움 | Git 등 버전 관리 시스템으로 변경 이력 추적 |
| **일관성** | 개발/스테이징/운영 환경이 미묘하게 다를 수 있음 | 모든 환경이 동일한 코드에서 생성되므로 일관적 |
| **롤백** | 이전 상태로 돌리기 어려움 | 이전 버전의 코드를 다시 실행하면 됨 |
| **문서화** | 별도 문서 작성 필요 | 코드 자체가 인프라 문서 역할 |

#### IaC의 핵심 이점 4가지

1. **반복 가능성(Repeatability)**: 같은 코드를 실행하면 언제나 같은 결과. 개발 환경, 테스트 환경, 운영 환경을 동일하게 구성할 수 있습니다.

2. **일관성(Consistency)**: "내 컴퓨터에서는 되는데 서버에서는 안 돼요"라는 문제를 방지합니다. 환경 간 차이(Configuration Drift)를 원천적으로 막습니다.

3. **버전 관리(Version Control)**: 인프라 코드를 Git 같은 버전 관리 시스템에 저장하면, 언제 누가 어떤 변경을 했는지 추적할 수 있고, 문제가 생기면 이전 버전으로 되돌릴 수 있습니다.

4. **자동화(Automation)**: 사람이 수십 개의 리소스를 하나하나 만들 필요 없이, 코드 한 번 실행으로 전체 인프라를 구축합니다. 실수(Human Error)를 줄이고 속도를 높입니다.

### 상세 예시 (Detailed Examples)

> 🔍 **예시 19.1.1: 요리 레시피와 IaC**
>
> **상황**: 유명 셰프가 운영하는 레스토랑 체인에서 모든 지점이 동일한 맛의 파스타를 만들어야 합니다.
> **비유**: 셰프가 각 지점 요리사에게 전화로 "소금을 적당히 넣고, 면을 알맞게 삶아"라고 말하면(수동 관리), 지점마다 맛이 다릅니다. 하지만 **정확한 레시피 문서**(물 2L, 소금 15g, 면 200g, 8분 삶기)를 주면(IaC), 어떤 요리사가 만들어도 동일한 맛이 보장됩니다.
> **핵심 포인트**: IaC는 인프라 구축의 "레시피"입니다. 누가, 언제 실행해도 동일한 인프라가 만들어집니다.

> 🔍 **예시 19.1.2: 개발팀의 환경 구축 문제**
>
> **상황**: 5명의 개발자가 각자 AWS 콘솔에서 개발 환경을 만듭니다. A 개발자는 t2.micro 인스턴스를 사용하고, B 개발자는 t3.small을 사용합니다. C 개발자는 보안 그룹에서 포트 22만 열었지만, D 개발자는 모든 포트를 열어둡니다.
> **문제**: 운영 환경에 배포하니 "내 환경에서는 잘 되었는데…"라는 문제가 발생합니다.
> **IaC 해결**: 하나의 코드 파일에 "t3.micro, 보안 그룹은 포트 22와 80만 허용"이라고 정의해두면, 모든 개발자가 동일한 환경에서 작업합니다. 운영 환경도 같은 코드로 만들기 때문에 환경 차이로 인한 문제가 사라집니다.
> **핵심 포인트**: IaC는 환경 간 일관성을 보장하여 "내 환경에서는 됐는데" 문제를 방지합니다.

### 흔한 실수와 주의사항 (Common Pitfalls)

> ⚠️ **주의**: "IaC를 사용하면 AWS 콘솔이 필요 없다"는 오해
>
> IaC는 인프라를 *정의하고 생성*하는 도구이지, AWS 콘솔을 완전히 대체하는 것이 아닙니다. 모니터링, 디버깅, 일회성 확인 작업 등에서는 여전히 콘솔이 유용합니다. 다만, **인프라의 생성과 변경**은 IaC를 통해 관리하는 것이 모범 사례입니다.

### Section 요약 (Section Summary)

- **IaC**는 인프라를 코드 파일로 정의하여 자동으로 생성·관리하는 방법론이다
- 수동 관리 대비 **반복 가능성, 일관성, 버전 관리, 자동화** 4가지 핵심 이점을 제공한다
- IaC를 사용하면 동일한 환경을 여러 번 만들거나, 변경 이력을 추적하거나, 이전 상태로 롤백하는 것이 가능하다
- AWS 콘솔을 대체하는 것이 아니라, 인프라의 생성과 변경을 체계적으로 관리하는 도구이다

---

## 19.2 AWS CloudFormation

> 💡 **한 줄 요약**: AWS의 대표적인 IaC 서비스로, JSON 또는 YAML 형식의 템플릿 파일을 작성하면 AWS가 알아서 리소스를 생성·관리해줍니다.

### 직관적 이해 (Intuitive Understanding)

건축에 비유하면, **CloudFormation 템플릿**은 **건축 설계도**에 해당합니다. 설계도에 "1층에 거실, 2층에 침실 3개, 주차장 1개"라고 적으면, 건설 회사(AWS)가 설계도를 보고 집을 지어줍니다. 설계도를 수정하면 리모델링도 해주고, 설계도를 폐기하면 집도 철거해줍니다.

이 건축 설계도가 바로 **템플릿(Template)**, 설계도를 기반으로 실제 지어진 집이 **스택(Stack)**입니다.

CloudFormation이 탄생한 배경은 간단합니다. AWS 리소스가 점점 많아지면서(EC2, VPC, S3, IAM 등), 이들을 하나하나 수동으로 만들고 연결하는 것이 복잡해졌습니다. "이 모든 리소스를 한 번에 정의하고, 한 번에 만들고, 한 번에 삭제할 수는 없을까?"라는 필요에서 CloudFormation이 만들어졌습니다.

### 핵심 개념 설명 (Core Explanation)

> 📝 **AWS CloudFormation**: AWS 리소스를 **템플릿(코드 파일)**으로 정의하고, 이를 기반으로 리소스를 자동으로 생성·업데이트·삭제하는 AWS의 IaC 서비스입니다. CloudFormation 서비스 자체는 **무료**이며, 생성된 리소스에 대해서만 비용이 발생합니다.

> 📝 **템플릿(Template)**: CloudFormation에서 인프라를 정의하는 **JSON 또는 YAML 형식의 텍스트 파일**입니다. 어떤 리소스를 어떤 설정으로 만들지 기술합니다.

> 📝 **스택(Stack)**: 하나의 템플릿을 실행하여 실제로 생성된 **AWS 리소스의 모음**입니다. 스택 단위로 리소스를 생성, 업데이트, 삭제할 수 있습니다.

#### 템플릿의 기본 구조

CloudFormation 템플릿은 YAML 또는 JSON으로 작성합니다. 아래는 S3 버킷을 하나 만드는 가장 간단한 YAML 템플릿 예시입니다:

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Description: 'My first CloudFormation template - S3 bucket'

Resources:
  MyFirstBucket:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: my-cfn-study-bucket-2026
```

각 부분의 의미를 살펴보겠습니다:

| 항목 | 설명 |
|------|------|
| `AWSTemplateFormatVersion` | 템플릿 형식 버전 (현재 `2010-09-09`가 유일한 값) |
| `Description` | 이 템플릿이 무엇을 하는지 설명하는 텍스트 |
| `Resources` | **(필수)** 생성할 AWS 리소스를 정의하는 섹션 |
| `MyFirstBucket` | 리소스의 논리적 이름 (템플릿 내에서 참조할 때 사용) |
| `Type` | 리소스 유형 (`AWS::서비스명::리소스유형` 형식) |
| `Properties` | 해당 리소스의 설정값 |

> 💬 **참고**: 템플릿에는 이 외에도 `Parameters`(입력 매개변수), `Outputs`(출력값), `Mappings`(매핑), `Conditions`(조건) 등의 섹션이 있지만, CLF-C02 시험에서는 `Resources` 섹션이 필수라는 점과 템플릿의 기본 개념만 이해하면 충분합니다.

#### 스택의 생명주기

CloudFormation 스택은 세 가지 핵심 동작이 있습니다:

```
[템플릿 작성] → [스택 생성(Create)] → 리소스가 AWS에 만들어짐
                      │
                [템플릿 수정] → [스택 업데이트(Update)] → 변경된 부분만 적용
                      │
                [스택 삭제(Delete)] → 스택에 속한 모든 리소스가 함께 삭제됨
```

1. **스택 생성(Create Stack)**: 템플릿을 CloudFormation에 제출하면, 정의된 리소스가 자동으로 생성됩니다. 리소스 간 의존성이 있으면 CloudFormation이 자동으로 올바른 순서로 생성합니다.

2. **스택 업데이트(Update Stack)**: 템플릿을 수정하고 다시 제출하면, CloudFormation이 현재 상태와 비교하여 **변경된 부분만** 적용합니다. 변경되지 않은 리소스는 그대로 유지됩니다.

3. **스택 삭제(Delete Stack)**: 스택을 삭제하면 **해당 스택으로 생성된 모든 리소스가 함께 삭제**됩니다. 이것이 CloudFormation의 큰 장점 중 하나입니다 — 수십 개의 리소스를 하나하나 찾아 삭제할 필요 없이, 스택 하나만 삭제하면 깔끔하게 정리됩니다.

#### 드리프트 감지 (Drift Detection)

> 📝 **드리프트(Drift)**: CloudFormation으로 만든 리소스를 누군가가 **콘솔에서 수동으로 변경**하여, 템플릿에 정의된 상태와 실제 리소스의 상태가 **달라진 것**을 말합니다.

예를 들어, CloudFormation으로 보안 그룹을 만들 때 "포트 80만 허용"으로 정의했는데, 누군가 콘솔에서 수동으로 포트 22를 추가로 열면 드리프트가 발생합니다. CloudFormation의 **드리프트 감지** 기능을 사용하면 이런 차이를 발견하고 경고할 수 있습니다.

이것은 IaC의 핵심 가치인 **일관성**을 유지하는 데 중요한 기능입니다.

### 상세 예시 (Detailed Examples)

> 🔍 **예시 19.2.1: 가장 간단한 CloudFormation — S3 버킷 생성**
>
> **상황**: 프로젝트용 S3 버킷을 CloudFormation으로 만들고 싶습니다.
> **템플릿**:
> ```yaml
> AWSTemplateFormatVersion: '2010-09-09'
> Description: 'Simple S3 bucket for project files'
>
> Resources:
>   ProjectBucket:
>     Type: AWS::S3::Bucket
>     Properties:
>       BucketName: my-project-bucket-2026
>       VersioningConfiguration:
>         Status: Enabled
> ```
> **설명**: 이 템플릿은 버전 관리가 활성화된 S3 버킷을 하나 생성합니다. `ProjectBucket`은 이 리소스의 논리적 이름이고, `Type`은 S3 버킷임을 나타내며, `Properties`에서 버킷 이름과 버전 관리 설정을 정의합니다.
> **핵심 포인트**: 템플릿에서 `Resources` 섹션은 반드시 포함해야 하는 유일한 필수 섹션입니다.

> 🔍 **예시 19.2.2: 여러 리소스를 포함하는 CloudFormation 템플릿**
>
> **상황**: EC2 인스턴스와 보안 그룹을 함께 만들고 싶습니다.
> **템플릿 (개념적)**:
> ```yaml
> AWSTemplateFormatVersion: '2010-09-09'
> Description: 'EC2 instance with security group'
>
> Resources:
>   WebServerSecurityGroup:
>     Type: AWS::EC2::SecurityGroup
>     Properties:
>       GroupDescription: Allow HTTP access
>       SecurityGroupIngress:
>         - IpProtocol: tcp
>           FromPort: 80
>           ToPort: 80
>           CidrIp: 0.0.0.0/0
>
>   WebServer:
>     Type: AWS::EC2::Instance
>     Properties:
>       InstanceType: t2.micro
>       ImageId: ami-0abcdef1234567890
>       SecurityGroupIds:
>         - !Ref WebServerSecurityGroup
> ```
> **설명**: 하나의 템플릿에 보안 그룹과 EC2 인스턴스를 함께 정의했습니다. `!Ref`는 같은 템플릿 내의 다른 리소스를 참조하는 문법으로, EC2 인스턴스가 위에서 정의한 보안 그룹을 사용하도록 연결합니다. CloudFormation은 자동으로 보안 그룹을 먼저 만든 뒤 EC2 인스턴스를 생성합니다.
> **핵심 포인트**: 하나의 템플릿에서 여러 리소스를 정의하고, 리소스 간 관계를 `!Ref`로 연결할 수 있습니다. CloudFormation이 의존성 순서를 자동으로 처리합니다.

### 미니 실습 (Hands-on Mini Lab)

> 🧪 **Mini Lab 19.2: CloudFormation으로 S3 버킷 생성하기**
>
> **목표**: CloudFormation 콘솔에서 템플릿을 사용해 S3 버킷을 생성하고, 스택의 생명주기(생성→확인→삭제)를 직접 체험합니다.
> **예상 소요 시간**: 10분
> **비용**: Free Tier 범위 내
>
> **사전 준비**: 아래 YAML 내용을 로컬 컴퓨터에 `my-first-template.yaml` 파일로 저장합니다:
>
> ```yaml
> AWSTemplateFormatVersion: '2010-09-09'
> Description: 'My first CloudFormation template'
>
> Resources:
>   MyStudyBucket:
>     Type: AWS::S3::Bucket
> ```
>
> 💬 **참고**: `BucketName`을 지정하지 않으면 CloudFormation이 자동으로 고유한 이름을 생성합니다. 이렇게 하면 이름 충돌을 피할 수 있어 실습에 편리합니다.
>
> **Step 1**: AWS 콘솔에 로그인한 뒤, 상단 검색창에 `CloudFormation`을 입력하고 서비스를 클릭합니다.
>
> **Step 2**: CloudFormation 대시보드에서 **[스택 생성(Create stack)]** 버튼을 클릭합니다. "기존 리소스 사용(With existing resources)" 옵션이 아닌, **[새 리소스 사용(With new resources (standard))]** 을 선택합니다.
>
> **Step 3**: "템플릿 지정(Specify template)" 단계에서:
> - **템플릿 소스**: "템플릿 파일 업로드(Upload a template file)"를 선택합니다.
> - **파일 선택**: 앞서 저장한 `my-first-template.yaml` 파일을 업로드합니다.
> - **[다음(Next)]** 을 클릭합니다.
>
> **Step 4**: "스택 세부 정보 지정(Specify stack details)" 단계에서:
> - **스택 이름**: `my-first-stack` 을 입력합니다.
> - **[다음(Next)]** 을 클릭합니다.
>
> **Step 5**: "스택 옵션 구성(Configure stack options)" 단계에서는 기본값 그대로 두고 **[다음(Next)]** 을 클릭합니다.
>
> **Step 6**: "검토(Review)" 단계에서 내용을 확인한 뒤 **[제출(Submit)]** 을 클릭합니다.
>
> **확인**:
> - 스택 목록에서 `my-first-stack`의 상태가 `CREATE_IN_PROGRESS` → `CREATE_COMPLETE`로 변경됩니다.
> - **[리소스(Resources)]** 탭을 클릭하면 `MyStudyBucket` (유형: `AWS::S3::Bucket`)이 표시됩니다.
> - 물리적 ID 링크를 클릭하면 실제 생성된 S3 버킷으로 이동합니다.
>
> **드리프트 감지 체험 (선택 사항)**:
> - S3 콘솔로 이동하여 방금 만든 버킷의 속성을 수동으로 변경해봅니다 (예: 버전 관리 활성화).
> - CloudFormation으로 돌아와서 스택을 선택하고 **[스택 작업(Stack actions)] → [드리프트 감지(Detect drift)]** 를 클릭합니다.
> - 잠시 후 드리프트 상태가 `DRIFTED`로 표시되면, 템플릿과 실제 상태의 차이를 확인할 수 있습니다.
>
> **🧹 정리**:
> - CloudFormation 콘솔에서 `my-first-stack`을 선택하고 **[삭제(Delete)]** 를 클릭합니다.
> - 스택이 삭제되면 S3 버킷도 자동으로 함께 삭제됩니다.
> - 💬 **참고**: 만약 버킷에 파일을 넣었다면, 버킷이 비어있지 않아 삭제가 실패할 수 있습니다. 이 경우 S3 콘솔에서 버킷의 내용을 먼저 비운(Empty) 뒤 스택을 다시 삭제하세요.

### 깊이 있는 이해 (Deep Dive)

> 🔬 **Deep Dive: CloudFormation의 내부 동작 원리**
>
> *이 부분은 심화 내용입니다. 처음 학습 시 건너뛰어도 됩니다.*
>
> CloudFormation이 스택을 생성할 때 내부적으로 어떤 일이 일어나는지 살펴보겠습니다:
>
> 1. **템플릿 검증**: CloudFormation이 템플릿의 문법(JSON/YAML)과 리소스 유형이 올바른지 확인합니다.
> 2. **의존성 그래프 생성**: 리소스 간의 참조(`!Ref`) 관계를 분석하여, 어떤 순서로 생성해야 하는지 결정합니다.
> 3. **리소스 생성**: 의존성 순서에 따라 리소스를 생성합니다. 독립적인 리소스는 **병렬로** 동시에 생성하여 속도를 높입니다.
> 4. **롤백**: 생성 도중 하나라도 실패하면, 이미 만든 리소스를 모두 삭제하고 원래 상태로 되돌립니다. 이를 통해 "절반만 만들어진" 불완전한 상태를 방지합니다.
>
> 스택을 **업데이트**할 때는, CloudFormation이 **변경 세트(Change Set)**를 생성하여 "어떤 리소스가 추가/수정/삭제될지"를 미리 보여줍니다. 이를 통해 예상치 못한 변경을 사전에 확인할 수 있습니다.

### 흔한 실수와 주의사항 (Common Pitfalls)

> ⚠️ **주의**: 스택 삭제 시 모든 리소스가 삭제됨
>
> CloudFormation 스택을 삭제하면 스택에 포함된 **모든** AWS 리소스가 함께 삭제됩니다. 이것은 정리할 때는 편리하지만, 운영 중인 리소스가 포함된 스택을 실수로 삭제하면 큰 문제가 됩니다. 운영 환경에서는 스택 삭제 방지(Termination Protection) 기능을 활성화하는 것이 좋습니다.

> ⚠️ **주의**: CloudFormation 템플릿의 `Resources` 섹션은 유일한 필수 섹션
>
> 시험에서 "CloudFormation 템플릿에서 반드시 포함해야 하는 섹션은?"이라는 문제가 나올 수 있습니다. 정답은 `Resources`입니다. `Description`, `Parameters`, `Outputs` 등은 모두 선택 사항입니다.

### Section 요약 (Section Summary)

- **CloudFormation**은 AWS의 IaC 서비스로, **템플릿**(YAML/JSON)을 작성하면 **스택**(리소스 모음)을 자동 생성한다
- 스택은 **생성, 업데이트, 삭제** 세 가지 핵심 동작이 있으며, 삭제 시 모든 리소스가 함께 삭제된다
- **드리프트 감지**로 수동 변경을 탐지하여 템플릿과 실제 상태의 일관성을 유지할 수 있다
- 템플릿에서 `Resources`는 유일한 필수 섹션이다
- CloudFormation 서비스 자체는 무료이며, 생성된 리소스에 대해서만 비용이 발생한다

---

## 19.3 AWS CDK와 SAM

> 💡 **한 줄 요약**: CDK는 프로그래밍 언어로, SAM은 서버리스에 특화된 간결한 문법으로 CloudFormation 템플릿을 더 쉽게 작성하는 도구입니다.

### 직관적 이해 (Intuitive Understanding)

CloudFormation 템플릿은 강력하지만, 복잡한 인프라를 정의하다 보면 YAML 파일이 수백~수천 줄에 달할 수 있습니다. 마치 건축 설계도를 작성할 때, 모든 벽돌의 위치를 일일이 좌표로 적는 것과 같습니다.

이런 불편함을 해결하기 위해 AWS는 두 가지 도구를 제공합니다:

- **CDK(Cloud Development Kit)**: "설계도를 좌표 대신 **프로그래밍 언어**로 작성하자!" — Python, TypeScript, Java 등 익숙한 프로그래밍 언어로 인프라를 정의할 수 있습니다.
- **SAM(Serverless Application Model)**: "서버리스 애플리케이션에 특화된 **간결한 설계도 형식**을 만들자!" — Lambda, API Gateway 등 서버리스 리소스를 더 적은 코드로 정의할 수 있습니다.

중요한 점은, **CDK와 SAM 모두 최종적으로 CloudFormation 템플릿을 생성**한다는 것입니다. 즉, CloudFormation이 "엔진"이고, CDK와 SAM은 그 엔진을 더 편하게 다루는 "도구"입니다.

```
[CDK 코드 (Python/TypeScript)]  ──(변환)──→  [CloudFormation 템플릿]  ──→  [AWS 리소스]
[SAM 템플릿 (간결한 YAML)]      ──(변환)──→  [CloudFormation 템플릿]  ──→  [AWS 리소스]
```

### 핵심 개념 설명 (Core Explanation)

#### AWS CDK (Cloud Development Kit)

> 📝 **AWS CDK (Cloud Development Kit)**: Python, TypeScript, Java, C#, Go 등 **일반 프로그래밍 언어**를 사용하여 AWS 인프라를 정의하는 오픈소스 프레임워크입니다. 작성된 코드는 **CloudFormation 템플릿으로 변환(synthesize)**되어 배포됩니다.

CDK의 장점은 프로그래밍 언어의 기능을 그대로 활용할 수 있다는 점입니다:

- **반복문**: 10개의 비슷한 리소스를 for문 하나로 생성
- **조건문**: 환경(개발/운영)에 따라 다른 설정 적용
- **재사용**: 공통 패턴을 함수나 클래스로 만들어 여러 프로젝트에서 재사용
- **자동완성**: IDE에서 코드 자동완성과 타입 검사 가능

CDK 코드가 어떻게 생겼는지 간단히 살펴보겠습니다 (Python 예시):

```python
from aws_cdk import Stack, aws_s3 as s3
from constructs import Construct

class MyStack(Stack):
    def __init__(self, scope: Construct, id: str):
        super().__init__(scope, id)

        # S3 버킷 생성 — 단 2줄로 완료
        s3.Bucket(self, "MyBucket",
                  versioned=True)
```

이 Python 코드가 실행되면, CloudFormation YAML 템플릿이 자동으로 생성되고, 이 템플릿이 CloudFormation을 통해 실제 S3 버킷을 만듭니다.

#### AWS SAM (Serverless Application Model)

> 📝 **AWS SAM (Serverless Application Model)**: **서버리스 애플리케이션** 구축에 특화된 오픈소스 프레임워크입니다. CloudFormation의 확장 문법을 사용하여 Lambda 함수, API Gateway, DynamoDB 테이블 등을 **더 적은 코드**로 정의할 수 있습니다.

> 🔗 **연결**: Chapter 5에서 Lambda의 서버리스 실행 모델을 배웠습니다. SAM은 이러한 서버리스 리소스를 정의하고 배포하는 데 특화된 도구입니다.

SAM 템플릿은 CloudFormation 템플릿과 비슷하지만, 서버리스 리소스를 더 간결하게 작성할 수 있습니다:

```yaml
# SAM 템플릿 예시
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31    # ← SAM임을 나타내는 표시

Resources:
  HelloFunction:
    Type: AWS::Serverless::Function      # ← SAM 전용 리소스 유형
    Properties:
      Handler: index.handler
      Runtime: python3.12
      Events:
        Api:
          Type: Api
          Properties:
            Path: /hello
            Method: get
```

이 짧은 코드만으로 Lambda 함수, API Gateway, 필요한 IAM 역할이 **모두 자동으로 생성**됩니다. 같은 것을 순수 CloudFormation으로 작성하면 3~4배 더 많은 코드가 필요합니다.

#### CDK vs SAM vs CloudFormation 비교

| 비교 항목 | CloudFormation | CDK | SAM |
|-----------|---------------|-----|-----|
| **작성 방식** | YAML/JSON | 프로그래밍 언어 | YAML (간결한 확장 문법) |
| **대상** | 모든 AWS 리소스 | 모든 AWS 리소스 | 서버리스 리소스에 특화 |
| **학습 곡선** | 중간 (YAML 문법) | 프로그래밍 경험 필요 | 낮음 (간결한 YAML) |
| **최종 결과** | 직접 실행 | CloudFormation 템플릿으로 변환 | CloudFormation 템플릿으로 변환 |
| **핵심 강점** | AWS 네이티브, 가장 세밀한 제어 | 프로그래밍 언어의 모든 기능 활용 | 서버리스 앱을 빠르게 구축 |

### 상세 예시 (Detailed Examples)

> 🔍 **예시 19.3.1: 같은 인프라를 세 가지 방식으로 정의하기**
>
> **상황**: S3 버킷 하나를 만들고 싶습니다.
>
> **CloudFormation (YAML)**:
> ```yaml
> Resources:
>   MyBucket:
>     Type: AWS::S3::Bucket
>     Properties:
>       VersioningConfiguration:
>         Status: Enabled
> ```
>
> **CDK (Python)**:
> ```python
> s3.Bucket(self, "MyBucket", versioned=True)
> ```
>
> **SAM**: (S3 버킷은 서버리스 특화 리소스가 아니므로, CloudFormation과 동일한 문법을 사용)
>
> **핵심 포인트**: 세 가지 모두 동일한 결과를 만들지만, CDK가 가장 간결합니다. 단, CDK와 SAM 모두 내부적으로는 CloudFormation 템플릿을 생성합니다.

> 🔍 **예시 19.3.2: SAM이 빛나는 순간 — 서버리스 API**
>
> **상황**: HTTP 요청을 받아 처리하는 Lambda 함수와 API를 만들고 싶습니다.
> **SAM 템플릿**: 위의 SAM 예시(약 12줄)로 Lambda + API Gateway + IAM Role이 모두 생성됩니다.
> **CloudFormation으로 같은 것을 만들면**: Lambda 함수 정의, IAM 역할 정의, API Gateway REST API 정의, API Gateway 메서드 정의, Lambda 권한 설정 등 **약 50~70줄**이 필요합니다.
> **핵심 포인트**: SAM은 서버리스 애플리케이션에서 반복적으로 필요한 설정을 자동으로 처리해주어 코드량을 대폭 줄여줍니다.

### 흔한 실수와 주의사항 (Common Pitfalls)

> ⚠️ **주의**: "CDK/SAM은 CloudFormation과 별개의 서비스"라는 오해
>
> CDK와 SAM은 CloudFormation을 **대체하는** 것이 아니라 CloudFormation **위에서 동작하는** 도구입니다. 최종적으로 모두 CloudFormation 템플릿이 생성되고, CloudFormation 엔진이 실제 리소스를 만듭니다. 시험에서 "CDK/SAM과 CloudFormation의 관계"를 묻는 문제가 나올 수 있습니다.

> ⚠️ **주의**: CLF-C02 시험에서의 출제 범위
>
> CLF-C02 시험에서는 CDK와 SAM의 **역할과 CloudFormation과의 관계**를 이해하는 수준이면 충분합니다. CDK 코드를 직접 작성하거나 SAM 템플릿의 세부 문법을 알 필요는 없습니다.

### Section 요약 (Section Summary)

- **AWS CDK**는 Python, TypeScript 등 프로그래밍 언어로 인프라를 정의하는 도구이다
- **AWS SAM**은 서버리스 애플리케이션에 특화된 간결한 IaC 프레임워크이다
- CDK와 SAM 모두 최종적으로 **CloudFormation 템플릿을 생성**하여 배포한다
- CloudFormation이 "엔진"이고, CDK와 SAM은 그 엔진을 더 편하게 사용하는 "도구"이다

---

## 19.4 CI/CD 파이프라인

> 💡 **한 줄 요약**: 코드 변경이 발생하면 자동으로 빌드, 테스트, 배포까지 수행하는 자동화된 워크플로를 CI/CD 파이프라인이라 합니다.

### 직관적 이해 (Intuitive Understanding)

자동차 공장의 조립 라인을 떠올려 보세요. 부품이 컨베이어 벨트에 올라가면:

1. **첫 번째 스테이션**: 부품을 조립합니다 → **빌드(Build)**
2. **두 번째 스테이션**: 조립된 차가 제대로 동작하는지 검사합니다 → **테스트(Test)**
3. **세 번째 스테이션**: 검사를 통과한 차를 고객에게 출하합니다 → **배포(Deploy)**

이 모든 과정이 자동화된 컨베이어 벨트 위에서 흘러가듯 진행됩니다. 부품(코드)을 올려놓기만 하면, 완성된 자동차(서비스)가 자동으로 나오는 것이죠.

소프트웨어 개발에서도 똑같은 자동화가 필요합니다. 개발자가 코드를 수정할 때마다 사람이 직접 빌드하고, 테스트하고, 서버에 올리는 것은 느리고 실수가 생기기 쉽습니다. 이 과정을 자동화한 것이 바로 **CI/CD 파이프라인**입니다.

### 핵심 개념 설명 (Core Explanation)

> 📝 **CI (Continuous Integration, 지속적 통합)**: 개발자들이 코드 변경사항을 **자주**(하루에도 여러 번) 중앙 저장소에 통합하고, 통합할 때마다 **자동으로 빌드와 테스트**를 실행하는 개발 관행입니다.

> 📝 **CD (Continuous Deployment/Delivery, 지속적 배포/전달)**: CI를 통과한 코드를 **자동으로 운영 환경에 배포**(Deployment)하거나, 배포 직전 단계까지 자동으로 준비(Delivery)하는 관행입니다.

#### CI/CD 파이프라인의 단계

```
[코드 커밋] → [소스(Source)] → [빌드(Build)] → [테스트(Test)] → [배포(Deploy)]
                  │                  │                │               │
             코드 변경 감지      코드 컴파일       자동 테스트      서버에 반영
             (GitHub 등)       패키지 생성        품질 검증        사용자 접근 가능
```

1. **소스(Source)**: 개발자가 코드를 저장소(GitHub, CodeCommit 등)에 푸시하면 파이프라인이 시작됩니다.
2. **빌드(Build)**: 소스 코드를 컴파일하고, 필요한 패키지를 설치하며, 실행 가능한 형태로 만듭니다.
3. **테스트(Test)**: 자동화된 테스트를 실행하여 코드 품질을 검증합니다.
4. **배포(Deploy)**: 테스트를 통과한 코드를 실제 서버(운영 환경)에 배포합니다.

#### AWS의 CI/CD 도구: CodeBuild

> 📝 **AWS CodeBuild**: 소스 코드를 **컴파일**하고, **테스트**를 실행하고, 배포 가능한 **패키지를 생성**하는 완전 관리형 빌드 서비스입니다.

CodeBuild의 핵심 특징:

- **완전 관리형**: 빌드 서버를 직접 설치하거나 관리할 필요 없음
- **종량제 과금**: 빌드를 실행한 시간만큼만 비용 지불 (빌드하지 않으면 비용 없음)
- **확장 가능**: 여러 빌드를 동시에 병렬로 실행 가능
- `buildspec.yml` 파일에 빌드 명령을 정의

일상적 비유로 설명하면, CodeBuild는 **"자동 요리 기계"**와 같습니다. 레시피(buildspec.yml)를 넣고 재료(소스 코드)를 넣으면, 자동으로 조리(빌드)하고 맛 테스트(테스트)를 해서 완성된 요리(배포 패키지)를 내놓습니다.

#### AWS CodeDeploy (참고)

> 📝 **AWS CodeDeploy**: 빌드된 애플리케이션을 EC2, Lambda, ECS 등 다양한 컴퓨팅 환경에 **자동으로 배포**하는 서비스입니다.

> 💬 **참고**: CodeDeploy는 CLF-C02 시험 범위에 포함되지 않지만, CI/CD 파이프라인의 "배포(Deploy)" 단계를 담당하는 서비스로서 전체적인 흐름을 이해하는 데 도움이 됩니다. 여기서는 역할만 간단히 소개합니다.

CodeDeploy의 역할을 한 문장으로 요약하면: CodeBuild가 만든 패키지를 **실제 서버에 안전하게 설치하는 배달 서비스**입니다.

### 상세 예시 (Detailed Examples)

> 🔍 **예시 19.4.1: CI/CD 없는 배포 vs CI/CD 있는 배포**
>
> **상황**: 웹 애플리케이션의 버그를 수정하고 운영 서버에 배포해야 합니다.
>
> **CI/CD 없이 (수동)**:
> 1. 개발자가 코드를 수정합니다.
> 2. 로컬에서 빌드합니다. ("내 컴퓨터에서는 되네!")
> 3. 빌드된 파일을 USB나 이메일로 전달합니다.
> 4. 운영 담당자가 서버에 접속해서 파일을 교체합니다.
> 5. 문제가 생기면 이전 파일을 찾아서 다시 교체합니다.
> → 시간: 1~2시간, 실수 가능성 높음
>
> **CI/CD 파이프라인 (자동)**:
> 1. 개발자가 코드를 수정하고 Git에 푸시합니다.
> 2. 파이프라인이 자동으로: 빌드 → 테스트 → 배포를 수행합니다.
> 3. 문제가 생기면 이전 버전으로 자동 롤백합니다.
> → 시간: 10~20분, 실수 최소화
>
> **핵심 포인트**: CI/CD는 배포 속도를 높이고, 사람의 실수를 줄이며, 문제 발생 시 빠른 롤백을 가능하게 합니다.

> 🔍 **예시 19.4.2: CodeBuild의 동작 흐름**
>
> **상황**: Python 웹 애플리케이션을 빌드하고 테스트합니다.
> **buildspec.yml 예시 (개념적)**:
> ```yaml
> version: 0.2
> phases:
>   install:
>     commands:
>       - pip install -r requirements.txt    # 의존성 설치
>   build:
>     commands:
>       - python -m pytest tests/            # 테스트 실행
>       - zip -r app.zip .                   # 배포 패키지 생성
> artifacts:
>   files:
>     - app.zip                               # 결과물
> ```
> **흐름**: CodeBuild가 이 파일을 읽고 → 의존성 설치 → 테스트 실행 → 패키지 생성을 자동으로 수행합니다.
> **핵심 포인트**: `buildspec.yml`은 CodeBuild에게 "무엇을 어떤 순서로 실행할지" 알려주는 레시피 파일입니다.

### 흔한 실수와 주의사항 (Common Pitfalls)

> ⚠️ **주의**: CI와 CD를 혼동하지 마세요
>
> - **CI(지속적 통합)**: 코드 통합 + 자동 빌드/테스트 — "코드가 잘 합쳐지고, 문제없이 동작하는가?"
> - **CD(지속적 배포/전달)**: 자동 배포 — "테스트를 통과한 코드를 실제 서비스에 반영"
> - CI는 "품질 검증"에 초점, CD는 "전달 자동화"에 초점입니다.

### Section 요약 (Section Summary)

- **CI/CD 파이프라인**은 코드 변경을 자동으로 빌드, 테스트, 배포하는 자동화 워크플로이다
- **CI(지속적 통합)**는 코드 통합 시 자동 빌드/테스트, **CD(지속적 배포)**는 운영 환경 자동 배포이다
- **AWS CodeBuild**는 빌드와 테스트를 수행하는 완전 관리형 서비스이다
- **AWS CodeDeploy**는 배포를 담당하지만 CLF-C02 시험 범위 밖이므로 개념만 이해한다
- CI/CD는 배포 속도 향상, 실수 감소, 빠른 롤백이라는 핵심 이점을 제공한다

---

## 19.5 AWS CodePipeline

> 💡 **한 줄 요약**: 소스 → 빌드 → 테스트 → 배포의 전체 CI/CD 과정을 하나의 파이프라인으로 자동 연결하는 오케스트레이션 서비스입니다.

### 직관적 이해 (Intuitive Understanding)

앞서 CI/CD 파이프라인을 자동차 공장의 조립 라인에 비유했습니다. 그 비유를 이어가면, **CodePipeline**은 조립 라인의 **컨베이어 벨트 자체**에 해당합니다.

각 스테이션(CodeBuild, CodeDeploy 등)은 각자의 작업을 수행하지만, 이것들을 **어떤 순서로 연결하고, 한 단계가 끝나면 다음 단계로 자동 전달**하는 역할은 컨베이어 벨트(CodePipeline)가 합니다.

CodeBuild가 "빌드하는 기계"라면, CodePipeline은 "기계들을 연결하는 컨베이어 벨트"입니다.

### 핵심 개념 설명 (Core Explanation)

> 📝 **AWS CodePipeline**: CI/CD 파이프라인의 각 단계(소스, 빌드, 테스트, 배포)를 **자동으로 연결하고 오케스트레이션**하는 완전 관리형 서비스입니다. 코드 변경이 감지되면 정의된 순서대로 각 단계를 자동 실행합니다.

> 📝 **오케스트레이션(Orchestration)**: 여러 도구와 서비스를 정해진 순서와 규칙에 따라 **자동으로 조율하고 관리**하는 것을 말합니다. 오케스트라의 지휘자가 각 악기 파트의 연주 순서와 타이밍을 조율하는 것과 같습니다.

#### CodePipeline의 구조

```
┌─────────────────────── CodePipeline ───────────────────────┐
│                                                             │
│  [Stage 1: Source]  →  [Stage 2: Build]  →  [Stage 3: Deploy]  │
│   (GitHub 등에서       (CodeBuild로        (S3, EC2,           │
│    코드 가져오기)        빌드 & 테스트)       Lambda 등에 배포)   │
│                                                             │
└─────────────────────────────────────────────────────────────┘
         ▲
   코드 변경 시
   자동 시작!
```

CodePipeline의 핵심 개념:

- **스테이지(Stage)**: 파이프라인의 각 단계 (Source, Build, Deploy 등)
- **액션(Action)**: 각 스테이지에서 수행되는 구체적 작업 (예: CodeBuild 실행, S3에 배포)
- **전환(Transition)**: 한 스테이지가 성공하면 다음 스테이지로 자동 이동

#### CodePipeline이 연결하는 도구들

| 파이프라인 단계 | AWS 서비스 | 역할 |
|----------------|-----------|------|
| **소스(Source)** | CodeCommit, GitHub, S3 | 코드 변경 감지 및 가져오기 |
| **빌드(Build)** | CodeBuild | 코드 빌드 및 테스트 |
| **배포(Deploy)** | CodeDeploy, S3, CloudFormation, ECS 등 | 빌드 결과물 배포 |

CodePipeline 자체는 빌드를 하거나 배포를 하지 않습니다. 각 단계에서 사용할 도구를 지정하면, CodePipeline이 그 도구들을 **올바른 순서로 자동 실행**합니다.

### 상세 예시 (Detailed Examples)

> 🔍 **예시 19.5.1: 웹 애플리케이션의 전형적인 CI/CD 파이프라인**
>
> **상황**: GitHub에 있는 웹 애플리케이션 코드가 변경되면 자동으로 빌드, 테스트, 배포하고 싶습니다.
> **CodePipeline 설정**:
> ```
> Stage 1 — Source: GitHub 리포지토리 연결
>   → 코드가 푸시되면 자동 시작
>
> Stage 2 — Build: CodeBuild 프로젝트 연결
>   → 빌드 및 테스트 실행
>   → 테스트 실패 시 파이프라인 중단 & 알림
>
> Stage 3 — Deploy: S3에 정적 웹사이트 배포
>   → 빌드 결과물을 S3 버킷에 업로드
> ```
> **결과**: 개발자가 GitHub에 코드를 푸시하기만 하면, 빌드 → 테스트 → 배포가 자동으로 진행됩니다. 어떤 단계에서든 실패하면 파이프라인이 중단되고 개발자에게 알림이 갑니다.
> **핵심 포인트**: CodePipeline은 각 도구를 연결하는 "접착제" 역할을 합니다.

> 🔍 **예시 19.5.2: IaC와 CI/CD의 결합**
>
> **상황**: CloudFormation 템플릿을 Git에 저장하고, 템플릿이 변경되면 자동으로 인프라를 업데이트하고 싶습니다.
> **CodePipeline 설정**:
> ```
> Stage 1 — Source: GitHub (CloudFormation 템플릿 저장소)
> Stage 2 — Deploy: CloudFormation (스택 업데이트)
> ```
> **결과**: 개발자가 CloudFormation 템플릿을 수정하고 Git에 푸시하면, CodePipeline이 자동으로 CloudFormation 스택을 업데이트합니다. **인프라 변경도 코드 배포처럼 자동화**됩니다!
> **핵심 포인트**: IaC + CI/CD를 결합하면 인프라 변경까지 자동화된 파이프라인으로 관리할 수 있습니다.

### 미니 실습 (Hands-on Mini Lab)

> 🧪 **Mini Lab 19.5: CodePipeline 콘솔 탐색**
>
> **목표**: CodePipeline 콘솔의 구조를 탐색하고 파이프라인의 개념을 시각적으로 이해합니다.
> **예상 소요 시간**: 5분
> **비용**: Free Tier 범위 내 (탐색만 하므로 비용 없음)
>
> **Step 1**: AWS 콘솔 상단 검색창에 `CodePipeline`을 입력하고 서비스를 클릭합니다.
>
> **Step 2**: CodePipeline 대시보드가 표시됩니다. 현재 파이프라인이 없으므로 빈 목록이 보입니다.
>
> **Step 3**: **[파이프라인 생성(Create pipeline)]** 버튼을 클릭합니다 (실제 생성하지 않고 구조만 확인합니다).
>
> **Step 4**: 파이프라인 생성 마법사를 통해 다음 구조를 확인합니다:
> - **파이프라인 이름** 설정
> - **소스 스테이지**: 어디서 코드를 가져올지 (GitHub, CodeCommit, S3 등)
> - **빌드 스테이지**: 어떤 빌드 서비스를 사용할지 (CodeBuild 등)
> - **배포 스테이지**: 어디에 배포할지 (S3, CloudFormation, ECS 등)
>
> **확인**: 파이프라인이 Source → Build → Deploy 단계로 구성되는 것을 시각적으로 확인합니다.
>
> **🧹 정리**: 실제 파이프라인을 생성하지 않았으므로 별도 정리가 필요 없습니다. 브라우저에서 마법사를 닫거나 **[취소(Cancel)]** 를 클릭합니다.

### 흔한 실수와 주의사항 (Common Pitfalls)

> ⚠️ **주의**: CodePipeline과 CodeBuild를 혼동하지 마세요
>
> - **CodeBuild**: 빌드와 테스트를 **실행하는** 서비스 (일꾼)
> - **CodePipeline**: 여러 단계를 **연결하고 자동 실행하는** 서비스 (관리자/지휘자)
> - CodePipeline은 CodeBuild 없이도 동작할 수 있고 (빌드 단계를 건너뛸 수 있음), CodeBuild도 CodePipeline 없이 독립적으로 사용할 수 있습니다.

### Section 요약 (Section Summary)

- **CodePipeline**은 CI/CD 파이프라인의 각 단계를 자동으로 연결하는 **오케스트레이션** 서비스이다
- 소스(Source), 빌드(Build), 배포(Deploy) **스테이지**로 구성되며, 각 스테이지에서 다른 AWS 서비스를 활용한다
- CodePipeline 자체는 빌드나 배포를 수행하지 않고, 다른 도구들을 **올바른 순서로 자동 실행**한다
- IaC(CloudFormation)와 결합하면 인프라 변경까지 자동화할 수 있다

---

## 19.6 추가 개발자 도구

> 💡 **한 줄 요약**: AWS Amplify, Cloud9, CodeArtifact 등 개발 생산성을 높이는 추가 도구들을 간략히 살펴봅니다.

### 직관적 이해 (Intuitive Understanding)

지금까지 IaC(CloudFormation, CDK, SAM)와 CI/CD(CodeBuild, CodePipeline)를 배웠습니다. 이것들은 인프라와 배포의 핵심 도구입니다. 이번 Section에서는 개발 과정을 더 편리하게 만드는 **보조 도구들**을 간략히 소개합니다.

이 도구들은 "필수"는 아니지만, 특정 상황에서 개발 속도를 크게 높여주는 도구입니다.

### 핵심 개념 설명 (Core Explanation)

#### AWS Amplify

> 📝 **AWS Amplify**: **웹 및 모바일 애플리케이션**을 빠르게 구축하고 배포할 수 있는 개발 플랫폼입니다. 프론트엔드 개발자가 백엔드 인프라를 쉽게 설정하고, 웹 앱을 자동 배포할 수 있습니다.

Amplify는 비유하자면 **"올인원 가구 키트"**와 같습니다. 일반적으로 책상을 만들려면 나무(EC2), 못(API Gateway), 페인트(S3 정적 호스팅) 등을 따로 사야 하지만, Amplify는 이 모든 것을 하나의 키트로 제공합니다.

Amplify의 주요 기능:
- **Amplify Hosting**: Git 리포지토리에 코드를 푸시하면 자동으로 웹 앱을 빌드하고 배포 (CI/CD 내장)
- **Amplify Studio**: 시각적 인터페이스로 백엔드를 설계
- React, Vue, Angular, Flutter 등 다양한 프레임워크 지원

> 💬 **참고**: Amplify는 CLF-C02 시험 범위에 포함됩니다. "웹/모바일 앱을 빠르게 배포하려면 어떤 서비스?"라는 유형의 문제에서 정답으로 출제될 수 있습니다.

#### AWS Cloud9

> 📝 **AWS Cloud9**: 브라우저에서 바로 사용할 수 있는 **클라우드 기반 통합 개발 환경(IDE)**입니다. 별도 소프트웨어 설치 없이 웹 브라우저만으로 코드를 작성, 실행, 디버깅할 수 있습니다.

Cloud9은 비유하자면 **"휴대용 사무실"**입니다. 어떤 컴퓨터에서든 웹 브라우저만 열면 동일한 개발 환경에 접속할 수 있습니다. 집 컴퓨터, 회사 컴퓨터, 심지어 태블릿에서도 같은 환경에서 코드를 작성할 수 있습니다.

Cloud9의 특징:
- 브라우저 기반이므로 **어디서든 접속** 가능
- AWS CLI, SAM CLI 등이 **사전 설치**되어 있어 AWS 개발에 바로 활용 가능
- 실시간 **공동 편집**(페어 프로그래밍) 지원

#### AWS CodeArtifact

> 📝 **AWS CodeArtifact**: 소프트웨어 **패키지(라이브러리)**를 저장하고 공유하는 완전 관리형 아티팩트 저장소입니다. npm, pip, Maven 등의 패키지 관리자와 연동됩니다.

일상적 비유로 설명하면, CodeArtifact는 **"회사 전용 도구 창고"**입니다. 외부에서 구매한 도구(공개 라이브러리)와 직접 만든 도구(사내 라이브러리)를 한 곳에 보관하고, 팀원들이 필요할 때 가져다 쓸 수 있게 합니다.

### 상세 예시 (Detailed Examples)

> 🔍 **예시 19.6.1: Amplify로 React 웹 앱 배포**
>
> **상황**: React로 만든 포트폴리오 웹사이트를 빠르게 인터넷에 공개하고 싶습니다.
> **Amplify 활용**: GitHub 리포지토리를 Amplify에 연결하면, 코드를 푸시할 때마다 자동으로 빌드 → 배포가 이루어집니다. 도메인 연결, HTTPS 설정도 자동으로 처리됩니다.
> **비교**: 같은 일을 직접 하려면 S3 정적 호스팅 설정, CloudFront 배포, ACM 인증서 발급, CodePipeline 설정 등 여러 서비스를 개별적으로 구성해야 합니다.
> **핵심 포인트**: Amplify는 웹/모바일 앱 배포에 필요한 여러 서비스를 하나로 통합하여 복잡성을 줄여줍니다.

> 🔍 **예시 19.6.2: 개발자 도구 선택 가이드**
>
> **상황**: 어떤 도구를 사용해야 할지 선택해야 합니다.
>
> | 필요한 것 | 추천 도구 |
> |-----------|----------|
> | 웹/모바일 앱을 빠르게 배포 | **Amplify** |
> | 브라우저에서 바로 코딩 | **Cloud9** |
> | 팀 내부 패키지 관리 | **CodeArtifact** |
> | 인프라를 코드로 관리 | **CloudFormation / CDK / SAM** |
> | 빌드 & 테스트 자동화 | **CodeBuild** |
> | 전체 파이프라인 오케스트레이션 | **CodePipeline** |
>
> **핵심 포인트**: 각 도구는 고유한 역할이 있으며, 필요에 따라 조합하여 사용합니다.

### 흔한 실수와 주의사항 (Common Pitfalls)

> ⚠️ **주의**: CLF-C02 시험에서의 출제 포인트
>
> 이 Section의 서비스 중 **Amplify**는 시험에 출제될 수 있습니다. "웹/모바일 앱을 빠르게 배포하는 서비스"라는 키워드로 기억하세요. Cloud9과 CodeArtifact는 개념만 알면 충분합니다.

### Section 요약 (Section Summary)

- **AWS Amplify**는 웹/모바일 앱을 빠르게 빌드·배포하는 올인원 플랫폼이다 (시험 범위)
- **AWS Cloud9**은 브라우저 기반 클라우드 IDE로, 어디서든 동일한 개발 환경을 사용할 수 있다
- **AWS CodeArtifact**는 소프트웨어 패키지를 저장·공유하는 아티팩트 저장소이다
- 각 도구는 고유한 역할이 있으며, 필요에 따라 선택하여 사용한다

---

## Chapter 핵심 요약 (Chapter Summary)

이번 Chapter에서는 AWS 인프라와 배포 과정을 **자동화**하는 핵심 개념과 서비스를 학습했습니다.

| Section | 핵심 내용 |
|---------|----------|
| **19.1 IaC 개요** | 인프라를 코드로 정의하여 반복 가능성, 일관성, 버전 관리, 자동화를 달성하는 방법론 |
| **19.2 CloudFormation** | AWS의 IaC 서비스. YAML/JSON 템플릿으로 스택(리소스 모음)을 생성·업데이트·삭제. 드리프트 감지로 일관성 유지 |
| **19.3 CDK와 SAM** | CloudFormation 위에서 동작하는 도구. CDK는 프로그래밍 언어로, SAM은 서버리스에 특화된 간결한 문법으로 IaC 작성 |
| **19.4 CI/CD 파이프라인** | 코드 변경 시 자동으로 빌드→테스트→배포하는 자동화 워크플로. CodeBuild가 빌드/테스트 담당 |
| **19.5 CodePipeline** | CI/CD 각 단계를 자동 연결하는 오케스트레이션 서비스. 컨베이어 벨트 역할 |
| **19.6 추가 개발자 도구** | Amplify(웹/모바일 앱 배포), Cloud9(클라우드 IDE), CodeArtifact(패키지 저장소) |

---

## 핵심 용어 정리 (Glossary)

| 용어 | 정의 | 관련 Section |
|------|------|-------------|
| Infrastructure as Code (IaC) | 인프라를 코드 파일로 정의하고 자동으로 관리하는 방법론 | 19.1 |
| AWS CloudFormation | AWS의 IaC 서비스. 템플릿 기반으로 리소스를 자동 생성·관리 | 19.2 |
| 템플릿 (Template) | CloudFormation에서 인프라를 정의하는 YAML/JSON 파일 | 19.2 |
| 스택 (Stack) | 하나의 템플릿에서 생성된 AWS 리소스의 모음 | 19.2 |
| 드리프트 (Drift) | 템플릿 정의와 실제 리소스 상태 간의 차이 | 19.2 |
| AWS CDK | 프로그래밍 언어로 인프라를 정의하는 오픈소스 프레임워크 | 19.3 |
| AWS SAM | 서버리스 애플리케이션에 특화된 IaC 프레임워크 | 19.3 |
| CI (Continuous Integration) | 코드 변경을 자주 통합하고 자동 빌드/테스트하는 관행 | 19.4 |
| CD (Continuous Deployment/Delivery) | 테스트 통과 코드를 자동으로 배포하는 관행 | 19.4 |
| AWS CodeBuild | 소스 코드 빌드와 테스트를 수행하는 완전 관리형 서비스 | 19.4 |
| AWS CodeDeploy | 애플리케이션을 자동 배포하는 서비스 (시험 범위 외, 참고) | 19.4 |
| AWS CodePipeline | CI/CD 단계를 자동 연결하는 오케스트레이션 서비스 | 19.5 |
| 오케스트레이션 (Orchestration) | 여러 도구/서비스를 정해진 순서로 자동 조율하는 것 | 19.5 |
| AWS Amplify | 웹/모바일 앱을 빠르게 빌드·배포하는 플랫폼 | 19.6 |
| AWS Cloud9 | 브라우저 기반 클라우드 IDE | 19.6 |
| AWS CodeArtifact | 소프트웨어 패키지 저장·공유 서비스 | 19.6 |

---

## 개념 연결 맵 (Connection Map)

```
[Chapter 5: 컴퓨팅 서비스]
  EC2, Lambda 등의 인프라 리소스 개념을 배움
        │
        ▼
[Chapter 19: 배포 자동화와 IaC] ◀── 현재 Chapter
  이 인프라 리소스들을 "코드로 정의"하고 "자동으로 배포"하는 방법을 배움
  - CloudFormation: EC2, S3 등을 템플릿으로 정의
  - CDK/SAM: CloudFormation을 더 편하게 사용
  - CI/CD: 코드 변경 → 자동 배포 파이프라인
        │
        ▼
[Chapter 24: Well-Architected Framework]
  IaC와 CI/CD는 운영 우수성(Operational Excellence) 원칙의 핵심 실천 방법
  - "인프라를 코드로 관리한다" = 운영 우수성
  - "배포를 자동화한다" = 운영 우수성
```

---

## 자기 점검 질문 (Self-Check Questions)

**Q1.** CloudFormation 템플릿에서 반드시 포함해야 하는 유일한 필수 섹션은 무엇인가?

<details>
<summary>정답</summary>

**Resources** 섹션입니다. 생성할 AWS 리소스를 정의하는 섹션으로, 템플릿에서 유일한 필수 항목입니다.
</details>

**Q2.** O/X: AWS CDK로 작성한 코드는 CloudFormation을 거치지 않고 직접 AWS 리소스를 생성한다.

<details>
<summary>정답</summary>

**X (거짓)**. CDK 코드는 CloudFormation 템플릿으로 변환(synthesize)된 후, CloudFormation 엔진을 통해 리소스가 생성됩니다. CDK는 CloudFormation 위에서 동작하는 도구입니다.
</details>

**Q3.** CloudFormation에서 "드리프트(Drift)"란 무엇을 의미하는가?

<details>
<summary>정답</summary>

CloudFormation으로 생성한 리소스를 누군가 콘솔 등에서 수동으로 변경하여, **템플릿에 정의된 상태와 실제 리소스 상태가 달라진 것**을 의미합니다.
</details>

**Q4.** CodeBuild와 CodePipeline의 차이를 한 문장으로 설명하시오.

<details>
<summary>정답</summary>

**CodeBuild**는 소스 코드를 빌드하고 테스트하는 "일꾼" 서비스이고, **CodePipeline**은 소스→빌드→배포의 전체 단계를 자동으로 연결하는 "지휘자/오케스트레이션" 서비스입니다.
</details>

**Q5.** O/X: CloudFormation 서비스를 사용하면 CloudFormation 자체에 대한 요금이 발생한다.

<details>
<summary>정답</summary>

**X (거짓)**. CloudFormation 서비스 자체는 무료입니다. CloudFormation이 생성하는 AWS 리소스(EC2, S3 등)에 대해서만 해당 리소스의 요금이 발생합니다.
</details>

**Q6.** 웹/모바일 애플리케이션을 Git 리포지토리에서 자동으로 빌드하고 배포하려면 어떤 AWS 서비스를 사용하는 것이 가장 간편한가?

<details>
<summary>정답</summary>

**AWS Amplify**입니다. Git 리포지토리를 연결하면 CI/CD가 내장되어 코드 푸시 시 자동으로 빌드·배포되며, 도메인 연결과 HTTPS 설정도 자동으로 처리됩니다.
</details>

**Q7.** IaC의 4가지 핵심 이점을 나열하시오.

<details>
<summary>정답</summary>

1. **반복 가능성(Repeatability)**: 같은 코드로 동일한 환경을 반복 생성
2. **일관성(Consistency)**: 환경 간 차이 방지
3. **버전 관리(Version Control)**: 변경 이력 추적과 롤백 가능
4. **자동화(Automation)**: 수동 작업 제거, Human Error 감소
</details>

---

## 🧪 통합 실습: CloudFormation으로 정적 웹사이트 인프라 구축하기

> **시나리오**: 당신은 소규모 스타트업의 개발자입니다. 회사 소개 웹사이트를 AWS에 호스팅하려고 합니다. 수동으로 만들면 팀원들이 동일한 환경을 재현하기 어려우므로, CloudFormation을 사용하여 인프라를 코드로 관리하기로 했습니다.

### 실습 개요

| 항목 | 내용 |
|------|------|
| **목표** | CloudFormation 템플릿으로 S3 정적 웹사이트 호스팅 환경을 구축하고, 스택의 전체 생명주기를 체험한다 |
| **사용 서비스** | CloudFormation, S3 |
| **활용 개념** | Section 19.1 IaC 이점, Section 19.2 CloudFormation 템플릿/스택 생명주기 |
| **선수 실습** | 없음 |
| **예상 소요 시간** | 20분 |
| **비용** | Free Tier 범위 내 |

### 아키텍처 다이어그램

```
[CloudFormation 템플릿 (.yaml)]
        │
        ▼
[CloudFormation 스택]
        │
        ├── S3 Bucket (정적 웹사이트 호스팅 활성화)
        │       │
        │       ├── index.html (직접 업로드)
        │       └── 퍼블릭 액세스 설정
        │
        └── S3 Bucket Policy (공개 읽기 허용)
```

### 실습 단계

> **Phase 1: CloudFormation 템플릿 작성** (활용 개념: Section 19.1, 19.2)
>
> **Step 1**: 로컬 컴퓨터에 `website-stack.yaml` 파일을 만들고 다음 내용을 붙여넣습니다:
>
> ```yaml
> AWSTemplateFormatVersion: '2010-09-09'
> Description: 'Static website hosting with S3'
>
> Resources:
>   WebsiteBucket:
>     Type: AWS::S3::Bucket
>     Properties:
>       WebsiteConfiguration:
>         IndexDocument: index.html
>       PublicAccessBlockConfiguration:
>         BlockPublicAcls: false
>         BlockPublicPolicy: false
>         IgnorePublicAcls: false
>         RestrictPublicBuckets: false
>
>   WebsiteBucketPolicy:
>     Type: AWS::S3::BucketPolicy
>     Properties:
>       Bucket: !Ref WebsiteBucket
>       PolicyDocument:
>         Version: '2012-10-17'
>         Statement:
>           - Effect: Allow
>             Principal: '*'
>             Action: 's3:GetObject'
>             Resource: !Sub '${WebsiteBucket.Arn}/*'
>
> Outputs:
>   WebsiteURL:
>     Description: 'URL of the static website'
>     Value: !GetAtt WebsiteBucket.WebsiteURL
>   BucketName:
>     Description: 'Name of the S3 bucket'
>     Value: !Ref WebsiteBucket
> ```
>
> **Step 2**: 이 템플릿이 무엇을 정의하는지 확인합니다:
> - `WebsiteBucket`: 정적 웹사이트 호스팅이 활성화된 S3 버킷
> - `WebsiteBucketPolicy`: 누구나 버킷의 파일을 읽을 수 있도록 허용하는 정책
> - `Outputs`: 스택 생성 후 웹사이트 URL과 버킷 이름을 출력
>
> **✅ 체크포인트**: `website-stack.yaml` 파일이 로컬에 저장되어 있어야 합니다.

> **Phase 2: CloudFormation 스택 생성** (활용 개념: Section 19.2)
>
> **Step 1**: AWS 콘솔에서 CloudFormation 서비스로 이동합니다.
>
> **Step 2**: **[스택 생성(Create stack)] → [새 리소스 사용(With new resources)]** 을 클릭합니다.
>
> **Step 3**: 템플릿 소스로 "템플릿 파일 업로드"를 선택하고, `website-stack.yaml`을 업로드합니다. **[다음]** 을 클릭합니다.
>
> **Step 4**: 스택 이름에 `my-website-stack`을 입력합니다. **[다음]** 을 클릭합니다.
>
> **Step 5**: 스택 옵션은 기본값 그대로 두고 **[다음]** 을 클릭합니다.
>
> **Step 6**: 검토 페이지 하단에서 "AWS CloudFormation이 IAM 리소스를 생성할 수 있음을 인정합니다" 체크박스가 있으면 체크하고, **[제출(Submit)]** 을 클릭합니다.
>
> **Step 7**: 스택 상태가 `CREATE_IN_PROGRESS`에서 `CREATE_COMPLETE`로 변경될 때까지 기다립니다 (약 1~2분).
>
> **✅ 체크포인트**: 스택 상태가 `CREATE_COMPLETE`이고, **[리소스]** 탭에서 S3 버킷과 버킷 정책이 생성된 것을 확인합니다.

> **Phase 3: 웹 페이지 업로드 및 확인** (활용 개념: Section 19.2)
>
> **Step 1**: CloudFormation 스택의 **[출력(Outputs)]** 탭에서 `BucketName`의 값을 복사합니다.
>
> **Step 2**: S3 콘솔로 이동하여 해당 버킷을 클릭합니다.
>
> **Step 3**: 로컬에 간단한 `index.html` 파일을 만듭니다:
> ```html
> <!DOCTYPE html>
> <html>
> <head><title>My First IaC Website</title></head>
> <body>
>   <h1>Hello from CloudFormation!</h1>
>   <p>This website was deployed using Infrastructure as Code.</p>
> </body>
> </html>
> ```
>
> **Step 4**: S3 버킷에 **[업로드(Upload)]** 버튼을 클릭하여 `index.html` 파일을 업로드합니다.
>
> **Step 5**: CloudFormation 스택의 **[출력(Outputs)]** 탭에서 `WebsiteURL` 값을 복사하여 브라우저에 붙여넣습니다.
>
> **✅ 체크포인트**: 브라우저에 "Hello from CloudFormation!"이 표시됩니다.

> **Phase 4: IaC의 가치 체험 — 스택 삭제로 깔끔한 정리** (활용 개념: Section 19.1, 19.2)
>
> **Step 1**: CloudFormation 콘솔에서 `my-website-stack`을 선택합니다.
>
> **Step 2**: **[삭제(Delete)]** 를 클릭합니다.
>
> **Step 3**: 확인 팝업에서 **[삭제]** 를 클릭합니다.
>
> **💬 참고**: S3 버킷에 파일이 있으면 삭제가 실패할 수 있습니다. 이 경우:
> 1. S3 콘솔에서 버킷으로 이동합니다
> 2. 모든 파일을 선택하고 **[삭제(Delete)]** 합니다
> 3. CloudFormation에서 스택 삭제를 다시 시도합니다
>
> **✅ 체크포인트**: 스택 상태가 `DELETE_COMPLETE`가 되고, S3 버킷도 함께 삭제됩니다.

### 최종 확인

- CloudFormation 템플릿 하나로 S3 버킷, 버킷 정책이 자동 생성되는 것을 확인했습니다
- Outputs를 통해 생성된 리소스의 정보(URL)를 자동으로 확인했습니다
- 스택 삭제 한 번으로 모든 리소스가 깔끔하게 정리되는 IaC의 이점을 체험했습니다

### 🧹 리소스 정리 (Clean-up)

> ⚠️ **비용 방지**: Phase 4에서 스택을 이미 삭제했습니다. 아래 사항을 확인하세요.
>
> 1. **CloudFormation 스택** — Phase 4에서 삭제 완료 확인 (상태: `DELETE_COMPLETE`)
> 2. **S3 버킷** — 스택 삭제 시 자동으로 함께 삭제됨. S3 콘솔에서 버킷이 없는지 확인
>
> 💬 **참고**: 이 실습에서 생성한 리소스는 이후 Chapter에서 사용하지 않으므로 모두 삭제합니다.

### 트러블슈팅 (Troubleshooting)

> **Q: 스택 생성 시 `CREATE_FAILED` 상태가 됩니다.**
> A: **[이벤트(Events)]** 탭에서 실패 원인을 확인하세요. 가장 흔한 원인은 YAML 문법 오류(들여쓰기 오류)이거나, S3 버킷 이름이 이미 다른 사용자에 의해 사용 중인 경우입니다. 이 템플릿에서는 `BucketName`을 지정하지 않아 자동 생성되므로 이름 충돌은 거의 발생하지 않습니다.

> **Q: 스택 삭제가 실패합니다 (`DELETE_FAILED`).**
> A: S3 버킷에 파일이 남아있으면 버킷을 삭제할 수 없습니다. S3 콘솔에서 버킷의 모든 파일을 먼저 삭제(Empty)한 후, CloudFormation에서 스택 삭제를 다시 시도하세요.

> **Q: 웹사이트 URL에 접속하면 `403 Forbidden` 오류가 나옵니다.**
> A: 버킷 정책이 제대로 적용되지 않았을 수 있습니다. S3 콘솔에서 해당 버킷의 **[권한(Permissions)]** 탭을 확인하세요. 또한 `index.html` 파일이 올바르게 업로드되었는지 확인하세요.

---

## 문제 풀이 (Problem Set)

### Practice (연습 문제) — 기본 개념 확인

> **Practice 19.1**: Infrastructure as Code(IaC)의 이점으로 **올바르지 않은** 것은?
>
> A. 동일한 인프라를 반복적으로 생성할 수 있다
> B. 인프라 변경 이력을 버전 관리할 수 있다
> C. AWS 콘솔 접속이 완전히 불필요해진다
> D. 사람의 실수(Human Error)를 줄일 수 있다
>
> <details>
> <summary>정답 및 해설</summary>
>
> **정답**: C
> **해설**: IaC는 인프라의 생성과 변경을 코드로 관리하지만, 모니터링, 디버깅, 일회성 확인 작업 등에서는 AWS 콘솔이 여전히 유용합니다. IaC가 콘솔을 완전히 대체하는 것은 아닙니다.
> </details>

> **Practice 19.2**: CloudFormation 템플릿에서 유일하게 필수인 섹션은?
>
> A. Parameters
> B. Outputs
> C. Resources
> D. Description
>
> <details>
> <summary>정답 및 해설</summary>
>
> **정답**: C
> **해설**: `Resources` 섹션은 생성할 AWS 리소스를 정의하는 곳으로, CloudFormation 템플릿에서 반드시 포함해야 하는 유일한 필수 섹션입니다. Parameters, Outputs, Description 등은 모두 선택 사항입니다.
> </details>

> **Practice 19.3**: CloudFormation에서 "스택(Stack)"이란 무엇인가?
>
> A. 템플릿을 저장하는 S3 버킷
> B. 하나의 템플릿에서 생성된 AWS 리소스의 모음
> C. CloudFormation의 요금 단위
> D. 여러 템플릿을 묶은 패키지
>
> <details>
> <summary>정답 및 해설</summary>
>
> **정답**: B
> **해설**: 스택은 하나의 CloudFormation 템플릿을 실행하여 실제로 생성된 AWS 리소스의 모음입니다. 스택 단위로 리소스를 생성, 업데이트, 삭제할 수 있습니다.
> </details>

> **Practice 19.4**: AWS CDK와 CloudFormation의 관계로 올바른 것은?
>
> A. CDK는 CloudFormation을 대체하는 별도의 서비스이다
> B. CDK 코드는 CloudFormation 템플릿으로 변환된 후 실행된다
> C. CloudFormation은 CDK의 일부 기능이다
> D. CDK와 CloudFormation은 서로 호환되지 않는다
>
> <details>
> <summary>정답 및 해설</summary>
>
> **정답**: B
> **해설**: CDK는 Python, TypeScript 등의 프로그래밍 언어로 작성된 코드를 CloudFormation 템플릿으로 변환(synthesize)합니다. 최종적으로 CloudFormation 엔진이 리소스를 생성합니다. CDK는 CloudFormation 위에서 동작하는 도구입니다.
> </details>

> **Practice 19.5**: CI/CD에서 CI(Continuous Integration)의 주요 목적은?
>
> A. 코드를 운영 서버에 배포하는 것
> B. 코드 변경사항을 자주 통합하고 자동으로 빌드·테스트하는 것
> C. 서버의 성능을 지속적으로 모니터링하는 것
> D. 인프라를 코드로 관리하는 것
>
> <details>
> <summary>정답 및 해설</summary>
>
> **정답**: B
> **해설**: CI(지속적 통합)는 개발자들이 코드 변경사항을 자주 중앙 저장소에 통합하고, 통합할 때마다 자동으로 빌드와 테스트를 실행하는 관행입니다. 운영 서버 배포는 CD(지속적 배포)의 영역입니다.
> </details>

> **Practice 19.6**: AWS CodePipeline의 역할로 가장 적절한 것은?
>
> A. 소스 코드를 컴파일하고 테스트를 실행한다
> B. 빌드된 코드를 서버에 배포한다
> C. 소스, 빌드, 배포 단계를 자동으로 연결하고 오케스트레이션한다
> D. 프로그래밍 언어로 인프라를 정의한다
>
> <details>
> <summary>정답 및 해설</summary>
>
> **정답**: C
> **해설**: CodePipeline은 CI/CD 파이프라인의 각 단계(소스, 빌드, 배포)를 자동으로 연결하는 오케스트레이션 서비스입니다. A는 CodeBuild, B는 CodeDeploy, D는 CDK의 역할입니다.
> </details>

> **Practice 19.7**: 웹/모바일 앱을 Git 리포지토리에서 자동으로 빌드하고 배포하는 올인원 AWS 서비스는?
>
> A. AWS CloudFormation
> B. AWS CodeBuild
> C. AWS Amplify
> D. AWS Cloud9
>
> <details>
> <summary>정답 및 해설</summary>
>
> **정답**: C
> **해설**: AWS Amplify는 웹/모바일 앱을 빠르게 빌드하고 배포하는 올인원 플랫폼입니다. Git 리포지토리를 연결하면 CI/CD가 내장되어 자동으로 빌드·배포됩니다.
> </details>

---

### Exercise (응용 문제) — 개념 적용 및 통합

> **Exercise 19.1**: 다음 시나리오를 읽고 질문에 답하세요.
>
> 한 회사에서 개발 환경, 스테이징 환경, 운영 환경 3개를 AWS에 구축해야 합니다. 각 환경은 EC2 인스턴스 2대, RDS 데이터베이스 1대, S3 버킷 1개로 구성됩니다. 팀 리더는 "세 환경이 완전히 동일해야 한다"고 요구합니다.
>
> (a) 이 요구사항을 충족하기 위해 수동 관리와 IaC 중 어떤 접근이 적합한지 설명하세요.
> (b) CloudFormation을 사용한다면, 세 환경을 어떻게 구성할지 설명하세요.
> (c) 3개월 후 운영 환경의 EC2 보안 그룹이 누군가에 의해 수동으로 변경되었습니다. 이를 어떻게 감지할 수 있을까요?
>
> <details>
> <summary>모범 답안</summary>
>
> **접근 방법**: IaC의 핵심 이점(반복 가능성, 일관성)과 CloudFormation의 기능(스택, 드리프트 감지)을 활용합니다.
>
> **(a)** IaC(CloudFormation)가 적합합니다.
> - 수동으로 3개 환경을 만들면 총 12개 리소스(4개 × 3환경)를 하나하나 생성해야 하고, 미묘한 설정 차이가 발생할 수 있습니다.
> - IaC를 사용하면 하나의 템플릿으로 동일한 환경을 3번 생성하므로 완전한 일관성이 보장됩니다.
>
> **(b)** 하나의 CloudFormation 템플릿을 작성하고, 이 템플릿으로 **3개의 스택**을 생성합니다:
> - `dev-stack` (개발 환경)
> - `staging-stack` (스테이징 환경)
> - `prod-stack` (운영 환경)
> - 세 스택 모두 동일한 템플릿을 사용하므로 동일한 구성이 보장됩니다.
> - 환경별로 다른 값(예: 인스턴스 크기)이 필요하면 `Parameters`를 사용하여 입력값만 다르게 줄 수 있습니다.
>
> **(c)** CloudFormation의 **드리프트 감지(Drift Detection)** 기능을 사용합니다.
> - 운영 환경 스택에서 드리프트 감지를 실행하면, 템플릿에 정의된 보안 그룹 설정과 현재 실제 설정의 차이를 감지하고 보여줍니다.
> - 이를 통해 누가 어떤 변경을 했는지는 알 수 없지만(이것은 CloudTrail의 역할), 원래 정의와 다르게 변경되었음을 확인할 수 있습니다.
>
> **보충 설명**: 드리프트를 감지한 후 원래 상태로 되돌리려면, 스택을 업데이트하여 템플릿의 정의대로 리소스를 복구할 수 있습니다.
> </details>

> **Exercise 19.2**: 아래의 AWS 서비스/도구를 CI/CD 파이프라인의 올바른 단계에 배치하세요.
>
> 서비스: CodeBuild, CodePipeline, GitHub, CodeDeploy, CloudFormation
>
> 파이프라인 단계:
> ```
> [소스] → [빌드 & 테스트] → [인프라 배포] → [앱 배포]
> ```
>
> 또한, 이 전체 흐름을 오케스트레이션하는 서비스는 무엇인지 설명하세요.
>
> <details>
> <summary>모범 답안</summary>
>
> **접근 방법**: 각 서비스의 역할을 파이프라인 단계에 매핑합니다.
>
> ```
> [소스: GitHub]  →  [빌드 & 테스트: CodeBuild]  →  [인프라 배포: CloudFormation]  →  [앱 배포: CodeDeploy]
> ```
>
> - **GitHub**: 소스 코드 저장소. 코드 변경을 감지하여 파이프라인 시작
> - **CodeBuild**: 소스 코드를 빌드하고 자동 테스트를 실행
> - **CloudFormation**: IaC 템플릿으로 인프라를 생성/업데이트
> - **CodeDeploy**: 빌드된 애플리케이션을 EC2 등에 배포
>
> **오케스트레이션**: **CodePipeline**이 전체 흐름을 자동으로 연결하고 관리합니다. CodePipeline은 각 단계를 순서대로 실행하며, 한 단계가 실패하면 파이프라인을 중단합니다.
>
> **보충 설명**: 이 예시에서 CodePipeline은 파이프라인 자체이고, 나머지 서비스들은 각 스테이지에서 실행되는 액션입니다. IaC와 CI/CD가 결합되면 인프라 변경과 코드 배포가 모두 자동화됩니다.
> </details>

> **Exercise 19.3**: CloudFormation, CDK, SAM 중 다음 각 시나리오에 가장 적합한 도구를 선택하고 이유를 설명하세요.
>
> (a) Python 개발자가 100개의 유사한 S3 버킷을 for 루프로 만들고 싶다.
> (b) 서버리스 API(Lambda + API Gateway)를 최소한의 코드로 빠르게 만들고 싶다.
> (c) YAML에 익숙한 운영팀이 EC2와 RDS를 포함한 인프라를 관리하고 싶다.
>
> <details>
> <summary>모범 답안</summary>
>
> **(a) AWS CDK**
> - 이유: CDK는 Python 등 프로그래밍 언어를 사용하므로 for 루프로 100개의 버킷을 효율적으로 생성할 수 있습니다. CloudFormation YAML로는 100개 버킷을 일일이 작성해야 합니다.
>
> **(b) AWS SAM**
> - 이유: SAM은 서버리스 리소스에 특화되어, Lambda + API Gateway를 약 10줄의 YAML로 정의할 수 있습니다. 순수 CloudFormation으로 같은 것을 만들면 50~70줄이 필요합니다.
>
> **(c) AWS CloudFormation**
> - 이유: YAML에 익숙하고 서버리스가 아닌 일반 인프라(EC2, RDS)를 관리하므로, CloudFormation이 가장 직접적이고 적합합니다. CDK는 프로그래밍 학습이 필요하고, SAM은 서버리스에 특화되어 있습니다.
>
> **보충 설명**: 세 도구 모두 최종적으로 CloudFormation 템플릿을 생성합니다. 선택 기준은 팀의 기술 스택, 대상 리소스, 복잡도에 따라 결정합니다.
> </details>

---

### Problem (심화 문제) — 깊이 있는 사고와 창의적 문제 해결

> **Problem 19.1**: 한 중견 기업이 현재 모든 인프라를 AWS 콘솔에서 수동으로 관리하고 있습니다. 다음 문제들이 반복적으로 발생합니다:
>
> - 개발 환경과 운영 환경의 보안 그룹 설정이 달라 배포 후 장애 발생
> - 인프라 변경 시 누가 무엇을 바꿨는지 추적 불가
> - 재해 복구(DR) 시 다른 리전에 동일한 환경을 구축하는 데 3일 소요
> - 매번 새 프로젝트마다 인프라 구축에 1주일 소요
>
> 이 기업에 IaC 도입을 제안하는 보고서를 작성하세요. 각 문제에 대해 IaC가 어떻게 해결하는지, 구체적으로 어떤 AWS 서비스를 사용할지, 도입 시 예상되는 이점과 주의사항은 무엇인지 포함하세요.
>
> <details>
> <summary>풀이 가이드</summary>
>
> **핵심 아이디어**: IaC의 네 가지 이점(반복 가능성, 일관성, 버전 관리, 자동화)을 각 문제에 매핑하여 해결 방안을 제시합니다.
>
> **풀이 전략**:
>
> | 문제 | IaC 이점 | 해결 방안 |
> |------|---------|----------|
> | 환경 간 보안 그룹 차이 | **일관성** | 하나의 CloudFormation 템플릿으로 모든 환경 생성 → 동일한 보안 그룹 보장 |
> | 변경 추적 불가 | **버전 관리** | 템플릿을 Git에 저장 → 모든 변경 이력 추적 가능. CloudFormation 드리프트 감지로 수동 변경 탐지 |
> | DR 구축 3일 소요 | **반복 가능성** | 같은 템플릿을 다른 리전에서 실행 → 수 시간 내 동일 환경 구축 |
> | 프로젝트 인프라 구축 1주일 | **자동화** | 표준 인프라 템플릿을 준비해두면 새 프로젝트마다 스택 생성만으로 완료 |
>
> **구체적 AWS 서비스 활용**:
> - **CloudFormation**: 핵심 IaC 도구. 모든 인프라를 템플릿으로 정의
> - **CDK**: 개발팀이 프로그래밍에 익숙하다면 CDK로 더 효율적으로 작성
> - **CodePipeline + CodeBuild**: 템플릿 변경 시 자동으로 인프라를 업데이트하는 CI/CD 파이프라인 구축
>
> **주의사항**:
> - 기존 수동 인프라를 CloudFormation으로 전환(Import)하는 과정이 필요 (기존 리소스를 스택으로 가져오기)
> - 팀원들의 IaC 학습 곡선 고려 필요
> - 전환 초기에는 콘솔과 IaC를 병행하되, 점진적으로 IaC 비율을 높이는 것이 현실적
> - 운영 환경의 스택에는 반드시 삭제 방지(Termination Protection)를 활성화
>
> **확장 생각**: IaC 도입은 단순히 도구 변경이 아닌 **운영 문화의 변화**입니다. "인프라 변경은 반드시 코드를 통해서"라는 원칙을 조직에 정착시키는 것이 기술 도입보다 중요할 수 있습니다. 이것은 Chapter 24에서 배울 Well-Architected Framework의 운영 우수성 원칙과 직결됩니다.
> </details>

> **Problem 19.2**: 다음 아키텍처를 위한 CI/CD 파이프라인을 설계하세요.
>
> **아키텍처**: GitHub에서 관리되는 웹 애플리케이션이 있으며, 프론트엔드(React)는 S3에 호스팅하고, 백엔드(Lambda)는 SAM으로 배포합니다. 개발 환경과 운영 환경이 있으며, 코드 변경 시 먼저 개발 환경에 배포하고, 수동 승인 후 운영 환경에 배포해야 합니다.
>
> (a) 이 파이프라인의 스테이지를 설계하세요 (각 스테이지에서 사용할 AWS 서비스 포함).
> (b) "수동 승인" 단계는 파이프라인의 어디에 위치해야 하며, 왜 필요한가요?
> (c) 이 파이프라인에서 IaC(SAM)와 CI/CD(CodePipeline)가 어떻게 결합되는지 설명하세요.
>
> <details>
> <summary>풀이 가이드</summary>
>
> **핵심 아이디어**: CI/CD 파이프라인 설계 시, 안전한 배포를 위해 개발→승인→운영 단계를 구분하고, IaC를 파이프라인에 통합합니다.
>
> **(a) 파이프라인 스테이지 설계**:
>
> ```
> Stage 1 — Source (GitHub)
>   : 코드 변경 감지
>       │
> Stage 2 — Build (CodeBuild)
>   : 프론트엔드 빌드 + 백엔드 테스트
>       │
> Stage 3 — Deploy to Dev (CloudFormation/SAM + S3)
>   : 개발 환경에 배포
>       │
> Stage 4 — Manual Approval
>   : 담당자가 개발 환경 확인 후 승인
>       │
> Stage 5 — Deploy to Prod (CloudFormation/SAM + S3)
>   : 운영 환경에 배포
> ```
>
> 전체를 **CodePipeline**이 오케스트레이션합니다.
>
> **(b) 수동 승인의 위치와 필요성**:
> - **위치**: 개발 환경 배포(Stage 3)와 운영 환경 배포(Stage 5) 사이
> - **필요성**: 자동 테스트만으로는 포착할 수 없는 문제(UI 이상, 비즈니스 로직 검증 등)를 사람이 직접 확인하기 위함. 운영 환경에 문제가 있는 코드가 자동으로 배포되는 것을 방지합니다.
> - CodePipeline은 수동 승인 액션을 기본 제공하며, SNS를 통해 승인 요청 알림을 보낼 수 있습니다.
>
> **(c) IaC와 CI/CD의 결합**:
> - **SAM 템플릿**이 Git에 코드와 함께 저장되어 있습니다.
> - CodeBuild가 SAM 템플릿을 빌드하고 CloudFormation 템플릿으로 변환합니다.
> - 배포 스테이지에서 CloudFormation이 변환된 템플릿으로 Lambda, API Gateway 등의 **인프라를 자동 생성/업데이트**합니다.
> - 즉, 코드 변경뿐 아니라 인프라 변경까지 하나의 파이프라인에서 자동으로 처리됩니다.
>
> **확장 생각**: 실제 운영 환경에서는 카나리 배포(일부 트래픽만 새 버전으로 보내 안전하게 검증)나 블루/그린 배포(이전 버전과 새 버전을 동시에 유지) 전략을 추가로 적용합니다. 이러한 배포 전략은 CLF-C02 범위를 넘지만, CI/CD의 궁극적인 목표인 "안전하고 빠른 배포"를 실현하는 핵심 기법입니다.
> </details>

---

## 다음 단계 안내 (What's Next)

이번 Chapter에서 인프라와 배포를 **자동화**하는 방법을 배웠습니다. 코드로 인프라를 관리하고(IaC), 변경사항을 자동으로 빌드·배포하는(CI/CD) 것은 현대 클라우드 운영의 핵심 관행입니다.

이러한 자동화 원칙은 이후 **Chapter 24: Well-Architected Framework**에서 **운영 우수성(Operational Excellence)** 원칙의 핵심 실천 방법으로 다시 등장합니다. "인프라를 코드로 관리하고, 배포를 자동화하라"는 이번 Chapter의 가르침이 AWS의 모범 사례 프레임워크에서 어떤 위치를 차지하는지 확인하게 될 것입니다.

---

## 추가 학습 자원 (Further Resources)

- **AWS CloudFormation 공식 문서**: [AWS CloudFormation User Guide](https://docs.aws.amazon.com/cloudformation/) — 템플릿 문법, 리소스 유형 레퍼런스
- **AWS CDK 공식 문서**: [AWS CDK Developer Guide](https://docs.aws.amazon.com/cdk/) — CDK 시작하기, API 레퍼런스
- **AWS SAM 공식 문서**: [AWS SAM Developer Guide](https://docs.aws.amazon.com/serverless-application-model/) — SAM 템플릿 작성법
- **AWS Skill Builder**: "Introduction to AWS CloudFormation" 무료 강좌 — 실습 중심 학습
- **AWS Well-Architected Labs**: IaC 관련 실습 — Well-Architected 원칙에 기반한 실전 실습
