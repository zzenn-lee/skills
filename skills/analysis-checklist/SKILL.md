---
name: analysis-checklist
description: "Before touching the data, break the problem into numbered requirements (R1, R2...), submission format, metric, constraints and assumptions, then write a step plan with output files and done criteria. Use at the start of any data analysis or modeling task, before explore-data, so later steps and the final validation have explicit criteria to check against."
---

# Analysis Checklist

문제를 받으면 데이터를 열기 **전에** 두 파일을 쓴다. 이후 분석은 이 기준을 따르고, 마지막 검증(validate-data, verification-before-completion)은 이 기준에 대해 수행한다. 전체 절차는 저장소 루트의 `guide.md`를 따른다.

## 작성 규칙

- 채팅이 아니라 파일로 남긴다 (작업 이력이 평가 대상).
- 짧게 쓴다. 모르는 것은 추측하지 말고 `A#` 가정으로 표시한다.
- 문제 문장에 있는 요구사항은 빠짐없이 `R#`로 옮긴다. 하나라도 빠지면 검증에서 실패다.
- 문제 유형에 맞지 않는 항목은 `해당 없음: <이유>`로 남긴다.

## `docs/00_problem.md`

```markdown
# 문제: <한 줄 요약>

## 요구사항
- R1: <요구사항 하나>
- R2: ...

## 제출물 형식
- <파일 이름·형식, 컬럼, 정밀도, 분량 등>

## 평가 지표
- <지표 이름: 정의, 단위, 높을수록/낮을수록 좋음>

## 제약
- <시간, 허용 도구·라이브러리, 외부 데이터 사용 여부 등>

## 가정
- A1: <애매한 부분에 대한 가정> (확인 방법: <데이터에서 무엇을 보면 확인되는지>)
```

## `docs/01_plan.md`

```markdown
# 계획

| 단계 | 할 일 | 만들 파일 | 완료 조건 | 충족 요구사항 |
|---|---|---|---|---|
| 1 | 데이터 파악 (explore-data, 필요 시 analyze-data-quality) | docs/02_data_profile.md | grain·키·결측·그룹 구조 기록됨 | — |
| 2 | <전처리> | src/preprocess.py | <확인 가능한 조건> | R# |
| 3 | <분석·모델> | src/analyze.py, outputs/... | <확인 가능한 조건> | R# |
| 4 | 평가·기준선 비교 | src/evaluate.py, outputs/metrics.* | <기준선 대비 수치가 파일에 있음> | R# |
| 5 | 검증 (validate-data) | docs/04_validation.md | 모든 R#가 결과물에 대응됨 | 전체 |

## 점검
- [ ] 모든 R#가 어느 단계에 배정됐다
- [ ] 각 완료 조건이 파일이나 출력으로 확인 가능하다
```

## 진행 중 갱신

- 사람이 함께 작업 중이면 `01_plan.md`를 보여주고 승인을 받은 뒤 진행한다.
- 데이터를 연 뒤 `A#` 가정을 확인 결과로 갱신한다. 가정이 틀려 계획이 바뀌면 `01_plan.md`를 고치고 `03_analysis_log.md`에 이유를 남긴다.
