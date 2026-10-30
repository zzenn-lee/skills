---
name: analysis-checklist
description: "Write a short pre-analysis checklist (goal and metric, data assumptions, analysis steps, pass criteria) before touching the data. Use at the start of any data analysis task or problem statement, before explore-data, so later steps and the final validation have explicit criteria to check against."
---

# Analysis Checklist

문제를 받으면 데이터를 열기 **전에** 아래 네 항목을 체크리스트로 먼저 작성한다.
이 문서가 이후 분석의 기준이 되고, 마지막 검증(validate-data, verification-before-completion)은 이 기준에 대해 수행한다.

## 작성 규칙

- 파일로 남긴다: 작업 폴더에 `CHECKLIST.md` (작업 이력이 평가 대상이므로 채팅에만 쓰지 않는다).
- 짧게 쓴다: 항목당 1~5줄. 모르는 것은 추측하지 말고 `가정:` 또는 `확인 필요:`로 표시한다.
- 문제 문장에 있는 요구사항(산출물, 지표, 형식, 제약)은 빠짐없이 옮긴다. 하나라도 빠지면 ④에서 실패다.

## 템플릿

```markdown
# CHECKLIST: <문제 한 줄 요약>

## ① 목표와 평가 지표
- 질문: <답해야 할 질문을 한 문장으로>
- 산출물: <제출해야 하는 것: 수치, 표, 그래프, 파일, 형식>
- 평가 지표: <정확도/RMSE/p-value/비율 등, 정의와 단위 포함>

## ② 데이터 가정
- 파일·테이블: <경로, 행 단위(grain), 키>
- 가정: <결측 처리, 기간, 단위, 시간대, 필터 등>
- 확인 필요: <데이터를 열어 확인해야 할 가정>

## ③ 분석 단계
- [ ] 1. 데이터 프로파일링 (explore-data)
- [ ] 2. 품질 점검, 필요 시 (analyze-data-quality)
- [ ] 3. <핵심 분석 단계: 전처리, 모델, 검정 등>
- [ ] 4. 결과 검증 (validate-data)

## ④ 합격 기준
- [ ] <요구사항 1이 산출물에 있다>
- [ ] <핵심 수치를 독립적으로 재계산해 일치했다>
- [ ] <형식/제약 조건을 지켰다>
- [ ] 모든 결론에 실행 근거(코드·출력)가 있다
```

## 진행 중 갱신

- 데이터를 연 뒤 ②의 `확인 필요` 항목을 확인 결과로 바꾼다. 가정이 틀렸으면 ③을 고친다.
- ③의 단계를 끝낼 때마다 체크한다.
- 마지막에 ④의 각 항목을 실제 출력과 대조해 체크한다. 체크하지 못한 항목은 최종 답변에 명시한다.
