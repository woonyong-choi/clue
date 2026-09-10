# 🔎 Clue

Kubernetes 장애의 증거 수집 → 원인 설명 → 제한된 수정 제안 → 회복 확인을 연결하는 오픈소스 도구를 설계합니다.

**현재는 설계 문서 저장소입니다.** 애플리케이션 코드, 설치 가능한 CLI와 배포 artifact는 아직 없습니다. 실행 가능한 기존 Python 구현은 [k8s-clue-python-reference](https://github.com/woonyong-kr/k8s-clue-python-reference)에 있습니다.

## 읽는 순서

1. [제품 정의](docs/01-product-definition.md): 해결할 문제와 첫 구현의 범위.
2. [목표 아키텍처](docs/03-target-architecture.md): CLI, Hub, Agent, Console, Store의 역할.
3. [구현 로드맵](docs/09-implementation-roadmap.md): Python의 행동 계약을 Java로 옮기는 순서와 완료 조건.

[전체 문서](docs/README.md)에는 보안·데이터 보존·설치 수명주기·언어 선택의 설계 근거가 있습니다. 문서의 `clue diagnose` 등은 목표 인터페이스이며 현재 실행 명령이 아닙니다.
