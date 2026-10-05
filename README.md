# RealWorld Web Service QA Project

공개 서비스 RealWorld(Conduit)를 대상으로 요구사항 분석, 테스트 설계, API 검증, E2E 자동화 과정을 기록하는 개인 QA 포트폴리오다. Web/App 서비스 QA 이직을 목표로 테스트의 선정 이유와 검증 근거를 함께 제시한다.

## 현재 진행 상태

- 초기 기능분해, 테스트 전략, 시나리오 초안 작성 완료
- 서비스 탐색, 테스트 실행, 결함 확인, 자동화 구현: 미수행
- 문서의 예상 결과는 테스트 기준이며 실제 실행 결과가 아니다.

## 대상과 근거

| 항목 | 기준 |
| --- | --- |
| 프로젝트 | [RealWorld 공식 저장소](https://github.com/realworld-apps/realworld) |
| Web 대상 후보 | [Conduit 공개 데모](https://demo.realworld.show/) |
| API 실행 명세 | [공개 API 문서](https://api.realworld.show/redoc) |
| 공통 기능 명세 | [공식 엔드포인트 명세](https://docs.realworld.show/specifications/backend/endpoints/) |
| 자료 확인일 | 2026-10-05 |

실행 전 UI 주소, 실제 API Base URL, 구현체/버전, 브라우저/OS, 실행일을 기록한다. 공통 명세와 실행 API 문서가 다르면 차이를 기록하고 기대 결과를 확정한다. 현재 서비스 동작과 가용성은 테스트하지 않았다.

공식 저장소는 공개 데모의 계정 간 데이터 격리를 안내한다. 두 테스트 계정 사이에서 데이터가 공유되는지 먼저 확인하며, 권한/팔로우/피드 검증이 불가능하면 해당 시나리오는 Blocked로 기록하고 별도 제어 가능한 공개 구현체 환경을 검토한다.

## 테스트 범위

- 회원가입, 로그인/로그아웃, 프로필 조회 및 수정
- 게시글 CRUD, 댓글 작성/조회/삭제
- 팔로우/해제, 즐겨찾기/해제, 태그 필터, 페이지네이션
- 정상/예외/경계 입력, 인증 및 소유권, 상태전이, UI ↔ API 조회 결과의 정합성
- 주요 사용자 여정의 회귀 검증과 네트워크 실패 시 UI 복구

초기 범위는 Web UI와 공개 API다. 네이티브 Android/iOS 앱, 결제, 서버 DB 직접 검증, 부하 테스트는 포함하지 않는다. DB 저장 여부는 직접 확인할 수 없으므로 후속 조회 결과를 통한 영속성 관찰로 표현한다. 모바일 화면 검증을 추가할 때 지원 화면 크기와 범위를 별도로 정한다.

## 사용 예정 기술

| 도구 | 활용 목적 | 상태 |
| --- | --- | --- |
| DevTools | 요청/응답, Console, UI와 API 연결 분석 | 예정 |
| Postman | API 요청, 응답 검증, 인증/테스트 데이터 관리 | 예정 |
| Playwright | 핵심 사용자 여정 E2E 및 회귀 자동화 | 예정 |

## 진행 단계

1. 서비스 탐색 및 명세 대조: 기능분해와 미확정 정책 보완
2. 핵심 사용자 여정과 리스크 우선순위 확정
3. 시나리오를 입력값·절차·기대 결과가 있는 상세 TC로 전환
4. DevTools 분석과 Postman API 검증, 근거 기록
5. 확인된 안정적인 핵심 흐름을 Playwright로 자동화
6. 결함 재검증, 회귀 실행, 결과와 한계 정리

## 저장소 구조

```text
realworld-web-qa/
├── README.md
├── .gitignore
├── docs/
│   ├── feature-analysis.md
│   ├── test-strategy.md
│   ├── test-scenarios.md
│   └── bug-report-template.md
├── postman/             # API 테스트 산출물 예정
├── tests/
│   └── e2e/             # Playwright 테스트 예정
└── reports/             # 비식별화한 실행 결과 예정
```

빈 산출물 폴더는 `.gitkeep`으로 유지한다. 자동화 코드와 실행 결과는 아직 없다.

## 문서

- [기능분해 및 확인 필요 정책](docs/feature-analysis.md)
- [테스트 전략](docs/test-strategy.md)
- [초기 테스트 시나리오](docs/test-scenarios.md)
- [결함 보고서 템플릿](docs/bug-report-template.md)

## 데이터 관리

공개 명세와 개인 테스트 데이터만 사용한다. 회사 기획서, 내부 API/DB/로그, 고객정보를 포함하지 않는다. 비밀번호, 인증 토큰, 인증 상태 파일은 커밋하지 않으며 캡처·HAR·Postman export는 민감값 제거 후 등록한다. 테스트 데이터에 실행 식별자를 붙이고 본인이 생성한 데이터만 정리한다.
