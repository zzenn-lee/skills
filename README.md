# Data Analysis Skills

데이터 분석 에이전트용 스킬 묶음. 사용 순서는 [AGENTS.md](AGENTS.md)에 있다.

## 설치

Codex: `skills/` 아래 폴더를 프로젝트의 `.agents/skills/`에 폴더째 복사하고, `AGENTS.md`를 프로젝트 루트에 둔다.

## 구성과 출처

| 스킬 | 역할 | 출처 | 라이선스 |
|---|---|---|---|
| analysis-checklist | 분석 전 기준·점검표 작성 | 이 저장소 (직접 작성) | — |
| explore-data | 데이터 프로파일링 | [anthropics/knowledge-work-plugins](https://github.com/anthropics/knowledge-work-plugins/tree/2574e29377c7173d0cecffef29a6ecbd7f8ccb5d/data/skills/explore-data) `data/skills/explore-data` | Apache-2.0 |
| statistical-analysis | 기술통계·이상치·가설검정 | [anthropics/knowledge-work-plugins](https://github.com/anthropics/knowledge-work-plugins/tree/2574e29377c7173d0cecffef29a6ecbd7f8ccb5d/data/skills/statistical-analysis) `data/skills/statistical-analysis` | Apache-2.0 |
| analyze-data-quality | 데이터 품질 심층 점검 | [openai/plugins](https://github.com/openai/plugins/tree/0722921d5542fc593105c27bd52630babd8b8c2a/plugins/data-analytics/skills/analyze-data-quality) `plugins/data-analytics/skills/analyze-data-quality` | Proprietary (plugin.json 기준) |
| validate-data | 결과 검증·판정 | [openai/plugins](https://github.com/openai/plugins/tree/0722921d5542fc593105c27bd52630babd8b8c2a/plugins/data-analytics/skills/validate-data) `plugins/data-analytics/skills/validate-data` | Proprietary (plugin.json 기준) |
| verification-before-completion | 실행 근거 없는 완료 선언 방지 | [obra/superpowers](https://github.com/obra/superpowers/tree/2ce8aa15d05bd57213e6f746f953aafb7ded7a8b/skills/verification-before-completion) `skills/verification-before-completion` | MIT |

외부 스킬은 위 커밋 기준으로 원문 그대로 복사했다 (2026-10-30).

## 참고

- `openai/role-specific-plugins`는 현재 placeholder README만 남아 있고, 해당 스킬들은 `openai/plugins`의 `data-analytics` 플러그인으로 옮겨져 있다.
- `openai/plugins`의 data-analytics 플러그인은 `plugin.json`에 `"license": "Proprietary"`로 표기되어 있다. 이 저장소를 공개하기 전에 재배포 가능 여부를 확인할 것.
- 포함하지 않은 후보: `create-data-context`(openai, 스크립트·커넥터 의존이 큼), `writing-plans`(superpowers, analysis-checklist가 대신함). 토큰 사용량을 고려해 6개로 제한했다.
