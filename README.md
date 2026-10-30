# Data Analysis Skills

Codex용 데이터 분석·시제품 과제 키트. 에이전트용 규칙은 [AGENTS.md](AGENTS.md), 작업 절차와 파일 구조는 [guide.md](guide.md)에 있다. 이 README의 나머지는 사람이 읽는 용도다.

## 과제 시작 전 설치 (Codex를 켜기 전에 터미널에서)

```bash
git clone https://github.com/zzenn-lee/skills /tmp/kit
mkdir -p .agents/skills && cp -r /tmp/kit/skills/* .agents/skills/
cp -n /tmp/kit/guide.md .
```

- 과제에 `AGENTS.md`가 없으면 `cp /tmp/kit/AGENTS.md .`로 복사한다. 이미 있으면 덮어쓰지 말고 맨 뒤에 `## 작업 키트 (과제 지시가 우선)` 제목을 달아 이어 붙인다.
- 키트 파일은 작업 결과와 섞이지 않게 커밋 하나로 따로 넣는다 (`chore: add working kit`).
- AGENTS.md는 Codex를 시작할 때 읽힌다. 복사한 뒤 Codex를 (다시) 시작하고 `/status`, `/skills`로 보이는지 확인한다. 스킬이 안 보여도 AGENTS.md가 파일 경로로 직접 읽게 한다.
- Codex 업데이트 안내가 떠도 업데이트하지 않는다.

## 구성과 출처

| 스킬 | 역할 | 출처 | 라이선스 |
|---|---|---|---|
| analysis-checklist | 요구사항(R#)·담당자 질문·계획·작업 기록 뼈대 | 이 저장소 (직접 작성) | — |
| semiconductor-data | lot·wafer·die·수율·bin·공정 데이터 함정 | 이 저장소 (직접 작성) | — |
| explore-data | 데이터 프로파일링 | [anthropics/knowledge-work-plugins](https://github.com/anthropics/knowledge-work-plugins/tree/2574e29377c7173d0cecffef29a6ecbd7f8ccb5d/data/skills/explore-data) `data/skills/explore-data` | Apache-2.0 (폴더에 LICENSE) |
| statistical-analysis | 기술통계·이상치·가설검정 | [anthropics/knowledge-work-plugins](https://github.com/anthropics/knowledge-work-plugins/tree/2574e29377c7173d0cecffef29a6ecbd7f8ccb5d/data/skills/statistical-analysis) `data/skills/statistical-analysis` | Apache-2.0 (폴더에 LICENSE) |
| data-validation | 데이터 품질 점검(A)·결과 검증과 판정(B) | 이 저장소 (직접 작성) | — |
| verification-before-completion | 실행 근거 없는 완료 선언 방지 | [obra/superpowers](https://github.com/obra/superpowers/tree/2ce8aa15d05bd57213e6f746f953aafb7ded7a8b/skills/verification-before-completion) `skills/verification-before-completion` | MIT (폴더에 LICENSE) |

외부 스킬은 위 커밋 기준으로 원문 그대로 복사했다 (2026-10-30). 직접 작성한 부분의 아이디어 일부는 같은 해커톤용으로 공개된 다른 키트들을 참고했고, 문구는 새로 썼다.

## 사람이 할 일

**단계별 지시문** (AI는 지시한 단계만 하고 멈춘다. 결정은 내가 하고, 이유는 내 말로 말해 준다.)

| 단계 | 붙여 넣을 지시 | 내가 확인·결정할 것 |
|---|---|---|
| ① 문제 분석 | `과제 README를 읽고 analysis-checklist로 docs/00_problem.md, 01_plan.md, 03_analysis_log.md를 써줘. 담당자 질문 후보도 뽑아줘.` | 빠진 R#, 담당자에게 실제로 물을 질문 |
| ② 답변 반영 | `담당자 답변: <답>. 00_problem.md의 Q#·R#·A#와 01_plan.md에 반영해줘.` | 계획 승인 또는 수정 |
| ③ 데이터 파악 | `explore-data로 데이터를 보고 docs/02_data_profile.md를 써줘. 품질 문제가 보이면 data-validation A도. 처리 규칙은 선택지로 줘.` | 결측·중복·재테스트 등 처리 규칙 |
| ④ 첫 결과 | `01_plan.md의 2단계까지 구현하고 핵심 수치와 기준선 비교를 보여줘.` | 계속할지, 방법을 바꿀지 |
| ⑤ 추가 작업 | `<R#>을 해줘. 끝나면 테스트 결과와 바뀐 수치를 보여줘.` | 다음 R# 순서, 140분이면 중단 |
| ⑥ 검증 | `data-validation B와 verification-before-completion으로 docs/04_validation.md를 써줘. 처음부터 다시 실행해서 재현도 확인해줘.` | 막는 문제 수정 여부, 제출 여부 |
| ⑦ 정리 | `docs/05_summary.md를 써줘 (과제가 지정한 제출 파일이 있으면 그 형식으로). 커밋해줘.` | 약점 3개를 내 말로 확인 |

결정할 때는 `A로 하자. 이유는 ~` 처럼 이유를 같이 말한다. 그 말이 결정 표에 그대로 남아 서술형 답변의 재료가 된다.

**담당자에게 물을 때**
- 결과 숫자를 바꾸는 것만 묻는다: 분모·기준값, 동점·중복·취소 처리, 결과를 누가 어디에 쓰는지, 성공을 판단할 숫자.
- 구체적인 과거 사례 하나를 들어 달라고 하면 숨은 조건이 잘 나온다. 답은 `docs/00_problem.md`의 Q# 표에 바로 적게 한다.

**시간**
- Codex는 화면의 타이머를 볼 수 없다. 단계가 바뀔 때 남은 시간을 직접 알려 준다.
- 140분쯤 기능 추가를 멈추고, 170분쯤 제출을 시작한다.

**서술형 대비 (AI 없이 5분씩)**
- 작업 중에 `docs/03_analysis_log.md`의 결정 표 "이유" 칸은 내 말로 채운다. 그게 답변 재료다.
- 제출 전에 직접 3가지를 정리해 둔다: 가장 큰 트레이드오프, 가장 위험한 실패 지점, Codex 결과를 다시 확인한 곳.
- 문항마다: 약 40초 읽기 → 약 3분 쓰기 (결론 → 이유 → 근거 수치 → 한계) → 약 1분 사실 확인.

## 참고: 시험 규칙 (비공식)

다른 참가자들의 공개 키트에 정리된 내용이다. 공식 안내로 반드시 다시 확인할 것.

- 과제는 최대 180분, 이후 AI·복사 없이 서술형 6문항(문항당 5분, 이전 문항으로 돌아갈 수 없음). 문항 생성 시간도 전체 종료 시각에 포함된다.
- 제공된 Codex만 사용. 개인 API 키, 다른 모델, Computer Use, git push, 외부 전송 금지.
- 공개 저장소는 clone해서 쓸 수 있다. PC 파일 업로드나 비공개 저장소는 안 된다. 사용한 저장소는 결과 발표 때까지 공개로 유지해야 한다.
- 대화, 터미널, git log/diff, 테스트, 토큰 사용량이 수집된다.
- pip 설치 허용 여부는 키트마다 말이 다르다. 사전 체험 때 확인할 것.

## 라이선스 참고

- 처음에는 `openai/plugins` data-analytics 플러그인의 `analyze-data-quality`, `validate-data`를 넣었다가 뺐다. `plugin.json`에 `"license": "Proprietary"`로 표기되어 있고 LICENSE 파일이 없어 공개 재배포 허락이 확인되지 않기 때문이다. 대신 같은 역할을 하는 `data-validation`을 직접 썼다. 이전 커밋 기록에는 원본 사본이 남아 있다.
- 포함하지 않은 후보: `create-data-context`(openai, 같은 라이선스 문제), `writing-plans`(superpowers, analysis-checklist가 대신함).
