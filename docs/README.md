# Kyro 문서

이 문서 세트는 지금까지 논의한 제품 방향과 기존 `k8s-ops`에서 검증한 내용을 Kyro의 새 구현 계획으로 정리한 것이다.

## 한 문장 정의

> Kyro는 Kubernetes 장애 증거를 수집하고, 판단 근거와 함께 원인을 설명하고, 안전한 수정안을 제안한 뒤 실제 회복까지 검증하는 도구다.

## 문서 지도

| 문서 | 내용 |
|---|---|
| [01. 제품 정의](01-product-definition.md) | 해결할 문제, 사용자, 차별점, 범위 |
| [02. 사용자 경험과 명령어](02-user-experience-and-commands.md) | `diagnose`, `watch`, `fleet`의 의미와 사용 흐름 |
| [03. 목표 아키텍처](03-target-architecture.md) | CLI, Hub, Agent, Console, Store의 역할과 연결 방식 |
| [04. 진단과 안전한 수정](04-diagnosis-and-remediation.md) | 증거, Analyzer, Incident, Draft PR, 회복 확인 |
| [05. 데이터·보안·신뢰](05-data-security-and-trust.md) | 수집 범위, Secret 정책, 권한, 보존, 장애 격리 |
| [06. 설치와 수명주기](06-installation-and-lifecycle.md) | Homebrew, Helm, 재연결, 중복 설치, 이전과 제거 |
| [07. AI와 개인정보](07-ai-and-privacy.md) | 규칙 우선, 로컬 AI, Claude/Codex 어댑터, 가명화 |
| [08. 오픈소스 생태계](08-open-source-ecosystem.md) | Rule Pack, 기여 구조, 신뢰 확보, 도입 이유 |
| [09. 구현 로드맵](09-implementation-roadmap.md) | 단계별 산출물과 완료 조건 |
| [10. Java 기술 결정](10-java-architecture-decision.md) | Python에서 Java로 전환하는 판단과 권장 스택 |
| [11. 기존 k8s-ops 이전](11-current-k8s-ops-migration.md) | 보존할 계약, 버릴 복잡성, 수직 이전 전략 |
| [12. Java와 Python 상세 비교](12-java-vs-python.md) | 접근 제어, interface, 타입, 동시성, 배포와 Kyro 적용 비교 |
| [13. Python 선행·Java 포팅 계획](13-python-first-java-port-plan.md) | k8s-ops 정리 완료 조건과 Java 단계별 인수 계획 |

## 확정한 명칭

| 개념 | 명칭 |
|---|---|
| 제품과 CLI 명령 | Kyro / `kyro` |
| 중앙 제어 서버 | Kyro Hub |
| 클러스터 수집 프로세스 | Kyro Agent |
| 웹 UI | Kyro Console |
| PostgreSQL 데이터 계층 | Kyro Store |
| 여러 클러스터의 논리적 묶음 | Fleet |
| 장애 판단 모듈 | Analyzer |
| 배포 가능한 Analyzer 묶음 | Rule Pack |
| 한 시점의 불변 진단 자료 | Evidence Bundle |
| 장애 단위 | Incident |
| 안전한 수정 제안 | Remediation Plan |
| 변경 후 회복 판정 | Recovery Check |

`Management`라는 제품명은 사용하지 않는다. 문맥상 관리 계층 전체를 가리킬 때만 일반 명사로 사용하고, 실행 인스턴스는 `Hub`라고 부른다.

## 현재 상태

- `k8s-ops`: Python 기반 행동 참조 구현으로 먼저 정리한다.
- `Kyro`: Java 기반 제품 구현을 시작할 새 디렉터리다.
- 이 문서 작성 시점에는 Kyro 애플리케이션 코드가 없다.
- 기존 저장소에서 확인한 대표 계약은 ImagePullBackOff 증거 수집, 결정론적 RCA, 제한된 GitOps Draft PR, 배포 후 회복 검증이다.
