# 산출물 템플릿

산출물 선택 스텝(6단계)에서 사용자가 고른 형식에 따라 아래 골격을 채운다.

---

## ⓐ Markdown 리포트

`{주제}-5Why통합분석.md` 로 저장(작업 폴더 또는 사용자가 지정한 위치). 아래 섹션 순서 유지.

```markdown
# {주제} — 5Why 통합분석 리포트

## 1. 문제 정의 (5W2H)
| 요소 | 내용 |
|---|---|
| What | {…} |
| Where | {…} |
| When | {…} |
| Who | {…} |
| Why(중요성) | {…} |
| How | {…} |
| How much | {…} |

## 2. 원인 공간 확장 (피시본/6M)

> mermaid는 피시본 전용 다이어그램 타입이 없어 `graph LR`로 스파인+가지 구조를 흉내낸다.

```mermaid
graph LR
    P[{문제}]
    Man[Man] --> P
    Machine[Machine] --> P
    Material[Material] --> P
    Method[Method] --> P
    Measurement[Measurement] --> P
    Environment[Environment] --> P
    Man1[{원인 후보}] --> Man
    Method1[{원인 후보}] --> Method
```

(브레인스토밍한 범주만 포함, 스킵한 범주는 제외)

## 3. 다중경로 병렬 5Why
| 범주 | Why 사슬 | 근본원인 후보 |
|---|---|---|
| {Man} | {증상} → {why1} → {why2} → … | {actionable cause} |
| {Method} | {증상} → {why1} → … | {actionable cause} |

## 4. FMEA 리스크 우선순위 (RPN 내림차순)
| 근본원인 후보 | Severity | Occurrence | Detection | RPN | 우선순위 |
|---|---|---|---|---|---|
| {…} | {1-10} | {1-10} | {1-10} | {S×O×D} | 1 |
| {…} | {1-10} | {1-10} | {1-10} | {S×O×D} | 2 |

## 5. 검증 근거
| 원인 | 빈도 데이터 | 시점 일치 | 조건 차이 | 판정 |
|---|---|---|---|---|
| {…} | {…} | {…} | {…} | ✅ 검증됨 / ⚠️ 추가 데이터 필요 |

## 6. 대응설계
{검증된 원인별 교정조치 — 우선순위(RPN) 순으로}
```

---

## ⓑ 인터랙티브 HTML (Artifact)

`artifact-design` 스킬을 먼저 로드한 뒤 작성. Artifact 도구로 배포.

**필수 구성 요소**
1. **문제정의 카드**: 5W2H 7요소를 카드/표로 표시.
2. **피시본 다이어그램**: mermaid가 아닌 커스텀 CSS/SVG로 실제 생선뼈 모양 구현 — 중앙 스파인
   에서 6M 범주가 대각선 가지로 뻗고, 각 가지에 원인 후보를 자식 노드로 배치.
3. **다중경로 5Why 트리/표**: 범주별 사슬을 아코디언 또는 표로, 마지막 노드(근본원인 후보)를 강조.
4. **FMEA RPN 정렬 바 차트 또는 표**: RPN 내림차순, 상위 항목 강조색. S/O/D 개별 값도 표시.
5. **검증 배지**: 원인별 ✅(검증됨) / ⚠️(추가 데이터 필요) 배지.

**스타일 규칙**
- self-contained: 모든 CSS/JS 인라인, 외부 요청 금지.
- 라이트/다크 테마 양쪽 대응(`prefers-color-scheme` + `data-theme`).
- 반응형: 표·다이어그램은 `overflow-x:auto` 컨테이너 안에서 스크롤. body 가로 스크롤 금지.
- `<title>` = "{주제} — 5Why 통합분석", favicon 이모지 예: 🐟 (피시본 연상) 또는 🔍.
