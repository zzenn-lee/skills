---
name: analysis-checklist
description: "Before touching the data or code, break the problem into numbered requirements (R1, R2...) with their source, submission format, metric, constraints, assumptions, stakeholder questions and out-of-scope items, then write a step plan with output files and done criteria, and a log skeleton. Use at the start of any data analysis, modeling or prototype task, so later steps and the final validation have explicit criteria to check against."
---

# Analysis Checklist

문제를 받으면 데이터나 코드를 열기 **전에** 아래 세 파일을 쓴다. 이후 작업은 이 기준을 따르고, 마지막 검증은 이 기준에 대해 수행한다. 전체 절차는 `guide.md`를 따른다.

## 작성 규칙

- 채팅이 아니라 파일로 남긴다 (작업 이력이 평가 대상).
- 짧게 쓴다. 모르는 것은 추측하지 말고 `A#` 가정으로 쓴다.
- 문제 문장의 요구사항은 빠짐없이 `R#`로 옮긴다. AI가 떠올린 기능은 사용자가 채택하기 전까지 R#가 아니다.
- 담당자 질문은 답에 따라 결과가 달라지는 것만, 많아야 3개 정도로 만든다.
- 맞지 않는 항목은 `해당 없음: <이유>`로 남긴다.

## `docs/00_problem.md`

```markdown
# 문제: <한 줄 요약>

유형: 데이터 분석 | 시제품 | 혼합

## 요구사항
| R# | 내용 | 출처 | 상태 |
|---|---|---|---|
| R1 | <요구사항 하나> | README §<위치> / Q# / 사용자 채택 | 확정 / 가정 / 미정 |

## 제출물 형식
- <파일 이름·형식, 컬럼, 정밀도, 분량 등>

## 평가 지표
- <지표: 정의, 단위, 높을수록/낮을수록 좋음>

## 제약
- <시간, 허용 도구·라이브러리, 외부 데이터 사용 여부 등>

## 가정
- A1: <가정> (확인 방법: <데이터에서 무엇을 보면 확인되는지>)

## 담당자 질문
| Q# | 질문 | 묻는 이유 (답에 따라 결과가 어떻게 달라지나) | 답 전까지의 가정 | 답 |
|---|---|---|---|---|

## 안 할 일
- <요구되지 않아 만들지 않을 것>
```

## `docs/01_plan.md`

```markdown
# 계획

| 단계 | 할 일 | 만들 파일 | 완료 조건 | 충족 R# |
|---|---|---|---|---|
| 1 | 데이터 파악 (explore-data, 필요 시 data-validation A) | docs/02_data_profile.md | grain·키·결측·그룹 구조 기록됨 | — |
| 2 | <첫 end-to-end 결과> | src/..., outputs/... | <확인 가능한 조건> | R# |
| 3 | <분석·모델·기능 추가> | ... | ... | R# |
| 4 | 평가·기준선 비교 | src/evaluate.py, outputs/metrics.* | 기준선 대비 수치가 파일에 있음 | R# |
| 5 | 검증 (data-validation B) | docs/04_validation.md | 모든 R#가 결과물에 대응됨 | 전체 |

- [ ] 모든 R#가 어느 단계에 배정됐다
- [ ] 각 완료 조건이 파일이나 출력으로 확인 가능하다
```

시제품 과제라면 1단계를 "가장 작은 end-to-end 흐름"으로 바꾸고, 단계마다 확인 명령(테스트나 실행)을 적는다.

## `docs/03_analysis_log.md`

```markdown
# 작업 기록

## 현재 상태 (단계가 바뀔 때마다 덮어쓴다)
- 단계: <지금 단계>
- 끝난 것: <...>
- 남은 것 (우선순위순): <...>
- 알려진 문제: <...>
- 다음 첫 행동: <...>

## 결정
| 시각 | 결정 | 버린 대안 | 이유 (사용자 본인의 말) | 근거 (파일:줄, 수치) | AI 제안 채택/거절 |
|---|---|---|---|---|---|
```

## 진행 중 갱신

- 세 파일을 쓰면 R# 목록, 담당자 질문 후보, 계획 요약을 보고하고 멈춘다. 사용자가 승인하기 전에는 데이터 분석이나 구현을 시작하지 않는다.
- 담당자 답을 받으면 `Q#`의 답 칸과 관련 `R#`·`A#`의 상태를 고친다.
- 계획이 바뀌면 `01_plan.md`를 고치고 `03_analysis_log.md`의 결정 표에 이유를 남긴다.
