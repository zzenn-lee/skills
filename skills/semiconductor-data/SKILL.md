---
name: semiconductor-data
description: "Pitfalls for semiconductor manufacturing data: lot/wafer/die keys, yield denominators, retests, bin codes, wafer maps, process/equipment measurements, SPC limits, and lot-level leakage. Use whenever data has lot, wafer, die, yield, bin, wafer map, chamber, recipe, or equipment columns."
---

# Semiconductor Data

반도체 데이터에서 자주 틀리는 지점이다. 해당되는 항목만 확인하고, 데이터로 답할 수 없는 것은 담당자 질문(`Q#`)으로 만든다.

## 키와 grain

- `wafer_id`는 lot 안에서만 유일할 수 있다. 키는 `(lot_id, wafer_id)`, die는 `(lot_id, wafer_id, x, y)`로 잡고 중복을 확인한다.
- ID는 문자열로 읽는다 (`W01`, `0007`의 앞자리 0 보존). lot당 wafer 수(예: 25)를 가정하지 않는다.

## 수율과 분모

- 수율은 `합계(pass die) / 합계(판정된 die)`다. wafer별 수율의 단순 평균과 다르다. 둘 다 필요하면 둘 다 이름을 붙여 보고한다.
- 분모에 edge·dummy·미측정 die를 넣는지 확인한다. 분모가 0이면 0%가 아니라 N/A다.
- 결함(defect) 수는 불량 die 수가 아니다. `1 - 결함 수/die 수`는 수율이 아니다.
- 재테스트가 있으면 first-pass, 최종, 시도별 수율이 모두 다르다. 어떤 것을 원하는지 묻고, 중복 행을 그냥 지우지 않는다.
- 변화는 %p와 상대 변화(%)를 구분해 쓴다.

## Bin과 wafer map

- 어떤 bin 코드가 pass인지는 데이터로 추측하지 말고 정의를 확인한다. hard bin(최종 판정)과 soft bin(세부 원인)을 구분한다. bin 정의를 `02_data_profile.md`에 표로 남긴다.
- wafer map은 좌표계(원점, x·y 방향, notch 위치)를 먼저 확인한다. 반경 구간(center/middle/edge)으로 나눠 보면 edge ring, center, scratch(선), cluster 패턴이 드러난다.

## 공정·장비 데이터

- 장비·챔버 이름 표기 변형(대소문자, `CH-1`/`CH1`)과 단위 혼합(Torr/mTorr 등)을 정리한 뒤 집계한다. 0이나 빈칸은 측정 실패일 수 있다.
- 장비·챔버별 불량률을 비교할 때는 그룹 크기를 같이 보고, PM(정비) 전후를 나눠 본다.
- 관리 한계(control limit)와 규격 한계(spec limit)는 다르다. 기준 기간을 고정해 관리 한계를 구하고, 실제 LSL/USL 없이 Cpk를 계산하지 않는다. 규격 경계값이 합격인지(이상/초과) 확인한다.

## 모델링과 누수

- 학습·평가 분할은 lot(최소 wafer) 단위로 한다 (`GroupKFold` 등). 같은 lot의 die가 양쪽에 있으면 성능이 부풀려진다.
- 시간 순서가 있으면 이전 lot으로 학습하고 이후 lot으로 평가한다.
- hold, 판정, result, disposition 같은 열은 결과 이후에 생긴 값일 수 있다. 타깃 누수로 의심하고 확인 전까지 입력에서 뺀다.
