# AGENTS.md

데이터 분석 문제는 [guide.md](guide.md)의 절차와 파일 구조(`docs/00~04`, `src/`, `outputs/`)를 따르고, 아래 순서로 스킬을 사용한다. 단계를 건너뛰지 않는다.

1. **analysis-checklist** — 데이터를 열기 전에 `docs/00_problem.md`(요구사항 R#, 제출물 형식, 지표, 제약, 가정 A#)와 `docs/01_plan.md`(단계·생성 파일·완료 조건)를 작성한다.
2. **explore-data** — 데이터를 처음 열 때 행·열 수, grain, 결측률, 카디널리티, 분포, 그룹 구조를 프로파일링해 `docs/02_data_profile.md`에 남긴다.
3. **analyze-data-quality** — 프로파일링에서 중복, 결측 급증, 이상값, 조인 손실 같은 신호가 보이거나 문제가 데이터 신뢰성을 묻는 경우에만 실행한다.
4. **statistical-analysis** — 기술통계, 이상치, 가설검정(t-검정, 카이제곱, ANOVA 등)이 필요할 때 사용한다. 효과 크기와 신뢰구간을 함께 보고한다.
5. **validate-data** — 결과를 내기 전에 핵심 수치를 재계산하고 누수·기준선·함정(조인 중복, 분모 오류, 심슨의 역설 등)을 점검한 뒤 `Ready to share / Share with caveats / Needs revision`으로 판정해 `docs/04_validation.md`에 남긴다.
6. **verification-before-completion** — 완료를 선언하기 직전에 실행한다. 이번 작업에서 실제로 실행한 코드와 출력 없이 "완료", "정답"이라고 말하지 않는다. 처음부터 다시 실행해 재현되는지, `docs/00_problem.md`의 R#가 모두 충족됐는지 하나씩 대조한다.

## 공통 규칙

- 모든 수치는 실제로 실행한 코드의 출력에서 가져온다. 추정값은 추정이라고 표시한다.
- 일부 스킬 본문에 이 저장소에 없는 스킬(`$jupyter-notebooks`, `$visualize-data`, `$build-report`, `$design-kpis`, `$product-business-analysis`)이나 커넥터 플레이스홀더(`~~structured_data`, `~~operations_logs`, `CONNECTORS.md`)가 나온다. 없는 것은 무시하고, 로컬 파일과 Python/SQL로 같은 점검을 수행한다.
- 스킬 산출물이 보고서 형식을 요구해도, 문제가 요구한 산출물 형식이 우선한다.
