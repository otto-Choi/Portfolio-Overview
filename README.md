# Portfolio — 감사 실무의 판단 구조를 데이터·AI 시스템으로 연결하는 회계인

<div align="center">

**공인회계사(KICPA)** · **Python / SQL** · **Audit Analytics** · **LLM Systems** · **Explainable AI**

</div>

> 감사 현장의 판단 구조를 재사용 가능한 데이터·AI 시스템으로 전환하는 작업을 해왔습니다.
> 아래 프로젝트는 **무엇을 만들 수 있는가보다 왜 그렇게 판단했는가**를 보여주는 것을 목표로 합니다.

회계·감사 도메인을 기반으로, 감사 자동화 · LLM 시스템 설계 · 금융 모델링 · 인과 검증 영역에서 문제 해결형 프로젝트를 수행했습니다. 각 저장소의 README는 기술 스택보다 **설계 의사결정 → 근거 → 결과 → 한계** 순서로 정리되어 있습니다.

---

## About Me

- 공인회계사(KICPA) 자격을 바탕으로 **Deloitte 안진에서 외부감사 실무**(기말감사·재고실사·감사조서 작성)를 수행했습니다.
- 대규모 회계 데이터를 다루며 마주한 병목을 출발점으로, **감사 판단·리스크 우선순위·분석 워크플로를 개선하는 데이터·AI 시스템**을 만듭니다.
- 관심의 축은 **회계·감사 도메인과 audit analytics, explainable AI가 교차하는 지점**입니다.

---

## Featured Projects

| 프로젝트 | 한 줄 소개 | 핵심 역량 | 저장소 |
|---|---|---|---|
| **SAP ERP Risk Analytics** | 수십만 건 GL 전표를 리스크 기반으로 우선순위화하는 audit analytics pipeline | 감사 × AI 브리지 (대표작) | [audit-analysis](https://github.com/otto-Choi/Project-audit-analysis) |
| **LectureNote** | 음성·문서·필기를 맥락 손실 없이 구조화하는 LLM 파이프라인 | LLM 실용 이해 + 시스템 설계 | [Lecture_Note](https://github.com/otto-Choi/Project_Lecture_Note) |
| **퇴직연금 ETF (XAI)** | 개인 위험 점수로 ETF 비중을 산출하고 근거를 XAI로 설명 | 금융공학 + XAI + 비즈니스 판단 | [Retirement_Pension_RA](https://github.com/otto-Choi/Project-Retirement_Pension_RA) |
| **유가 / GPR 예측력 검증** | 널리 쓰이는 선행지표 GPR이 인과 검증 앞에서 실패함을 실증 | 분석 엄밀성 / 인과 추론 | [Oil_Price](https://github.com/otto-Choi/Project-Oil_Price) |
| **국내 상장 리츠 가치평가** | 회계 왜곡을 제거해 조정 FFO를 재구성한 내재가치 분석 | 회계·금융 도메인 이해 | [K_REITs](https://github.com/otto-Choi/Project-K_REITs) |

<details>
<summary>📂 <b>프로젝트 상세</b> — 문제 정의 · 핵심 판단 · 결과 · 스택 (펼치기)</summary>

<br/>

### 1. SAP ERP Risk Analytics Pipeline — 대표작

> 수십만 건의 GL line item 중 감사인이 어디부터 봐야 하는지를 결정하는 파이프라인. config 교체만으로 클라이언트마다 다른 ERP 구조와 리스크 기준에 대응한다.

- **기간·유형** 2026.03 – 2026.05 · 개인 (정규 스터디)
- **역할** End-to-End (설계·구현·검증)
- **핵심 판단** anomaly detection이 아니라 *탐색 우선순위* 문제로 재정의. 모델 성능 대신 **audit explainability**를 KPI로 삼아, ML이 아닌 Rule Engine을 선택했다. 코드와 파라미터를 분리(3-layer Config)해 새 클라이언트는 코드 수정 없이 config만 교체한다.
- **대표 결과** 단일 SAP 샘플(332,103개 GL line items)에서 8 Rule × 3-layer Config 재사용성 검증 — 차대불균형 21,374건·계정별 이상금액 2,068건 탐지, CONFIG 셀 1개 교체로 Excel 조서 3시트 자동 생성.
- **스택** `Python · Pandas · Streamlit · PyYAML · OpenPyXL`
- 🔗 [저장소](https://github.com/otto-Choi/Project-audit-analysis)

### 2. LectureNote — 맥락 인지형 LLM 파이프라인

> 음성·문서·필기가 각기 다른 채널로 들어와도, 상위 컨텍스트(커리큘럼·용어 체계·평가 방향)를 잃지 않고 구조화된 학습 노트를 생성한다.

- **기간·유형** 2026.03 – 2026.06 · 개인 (학교 과제)
- **역할** End-to-End (아키텍처 설계·전체 구현·배포)
- **핵심 판단** 문제의 본질이 모델 성능이 아니라 **context orchestration**이라면, 해법도 prompt engineering이 아니라 context architecture여야 한다. 단일 도메인 환경에서는 retrieval precision보다 사전 구축된 context consistency가 중요하다고 판단해, Full RAG 대신 **Step 0 context injection (Simplified RAG)** 을 채택했다.
- **대표 결과** 2시간 분량 강의 음성+PDF 입력 기준 구조화 노트 약 34초 생성, 전체 테스트 LLM 비용 약 $4. Step 0 용어 사전이 있는 항목은 환각 0건(자체 검토 기준).
- **스택** `FastAPI · SSE · SQLite · Gemini 2.5-flash · PyMuPDF · Vanilla SPA`
- 🔗 [저장소](https://github.com/otto-Choi/Project_Lecture_Note) · [Live Demo](https://lecturenote.up.railway.app) · Android (Google Play 심사 통과·비공개 테스트 단계)

### 3. 퇴직연금 ETF 포트폴리오 최적화 — XAI 기반 위험 개인화

> 한국 DC/IRP 가입자를 위해 개인 위험 점수로 ETF 비중을 산출하고, 그 근거를 XAI로 투명하게 제시하는 투자 참고 정보 시스템.

- **기간·유형** 2026.04 – 2026.05 · 팀 (데이터분석 학회 학술제)
- **역할** 포트폴리오 파트 전담 (금융 이론·파라미터·구현 검증)
- **핵심 판단** 퇴직연금의 핵심 비대칭성("손실 후 회복할 시간이 없다")에 맞춰 표준편차 대신 하방공분산 Σ_down(Estrada 2007)을 위험 측도로, 목적함수를 Sortino 비율 최대화로 일관되게 설계. **초기 구현이 설계와 달랐던 5개 지점을 직접 검토로 발견·수정**한 것이 백테스트 신뢰도의 전제였다.
- **대표 결과** (2016~2025, 38분기 표본외) 원리금보장형 방치 CAGR 1.97% 대비 Step5b **CAGR 6.60% (+4.63%p)**, 소르티노 0.659.
- **스택** `Python · Black-Litterman · Sortino(SLSQP) · SHAP · pandas`
- 🔗 [저장소](https://github.com/otto-Choi/Project-Retirement_Pension_RA)
- ⚖️ 모든 출력은 「자본시장법」 제6조에 따른 투자 추천이 아닌 **투자 참고 정보**입니다.

### 4. 지정학적 리스크 지수(GPR)의 예측력 실패 — 인과 검증

> "GPR은 기존 거시 변수 대비 추가적인 예측력을 갖는가?"를 Granger 인과·이벤트 스터디·GARCH-X로 정량 검증한 결과, GPR이 선행지표가 아니라 후행지표에 가깝다는 구조적 한계를 실증했다.

- **기간·유형** 2026.03 · 팀 (DArt-B 토이 프로젝트)
- **역할** 가설 설계·인과 검증·모델링 주도
- **핵심 판단** "더 나은 예측 모델"을 만드는 대신, 널리 쓰이는 가정이 실제로 성립하는지를 검증하는 데 초점. 상관이 아니라 인과를 묻는 도구(Granger·이벤트 스터디·외생성을 명시적으로 다루는 GARCH-X)로 구성. V1~V9 폐기 과정 자체를 성과로 문서화했다.
- **대표 결과** GPR→유가 Granger 검정 p=0.59(기각). 분산 채널만 통계적 유의(δ p=0.0016)하나, GPR이 9배 상승해도 예측 밴드폭 확대는 $1.0(4%)에 불과 — **통계적 유의성 ≠ 실질적 유의성**을 실증.
- **스택** `Python · GARCH-X · Granger · LightGBM · statsmodels`
- 🔗 [저장소](https://github.com/otto-Choi/Project-Oil_Price)

### 5. 국내 상장 리츠 가치평가 — 회계 정규화와 FFO 재구성

> 리츠는 당기순이익만으로 평가할 수 없다. 회계 왜곡을 제거해 조정 FFO를 재구성하고, 국내 상장 리츠의 내재가치와 시장 할인 구조를 분석했다.

- **기간·유형** 2025.10 – 2025.11 · 팀 (데이터분석 학회 학술제)
- **역할** 가치평가 회계·모델(FFO·DCF/DDM·회계 조정) 담당
- **핵심 판단** 감가상각 과대·자산처분이익·배당 의무·유상증자 등 구조적 요인이 당기순이익을 실질 현금창출력에서 괴리시키므로, 가치평가 이전에 **회계 정규화가 전제 조건**. DCF(조정 FFO)와 DDM(조정 배당)을 병행 교차검증한 뒤, 국내 리츠 현황에서는 DDM 내재가치가 실무적으로 더 해석 가능하다고 논증했다.
- **대표 결과** 처분이익 포함 여부만으로 DCF 내재가치가 ±20~40% 변동 — 이 민감도가 DDM 대체 채택의 정당화. 시장 할인은 단순 오평가보다 불확실성에 대한 가격 반영에 가까웠다.
- **스택** `DCF/DDM · FFO 재구성 · CAPM · DART · GARCH-M`
- 🔗 [저장소](https://github.com/otto-Choi/Project-K_REITs)

</details>

---

## 경력 사항 (Professional Experience)

### Deloitte 안진 회계법인 — 수습 공인회계사 · 2025.12 ~ 2026.02
- 제조·유통·숙박·플랫폼 등 산업의 기말감사 및 재고실사 업무 참여
- 실증절차 · 재무제표 검토 · 롤포워드 · 감사조서 작성 수행
- 해외 계열사 관련 글로벌 협업 업무 및 증빙 검토 경험
- 대규모 회계 데이터 검토 과정에서 **데이터 분석·자동화의 필요성을 체감** (→ 이 문제의식이 SAP·자동화 프로젝트의 출발점)

### 중앙대학교 외국인지원센터 — 유학생 멘토 · 2026.03 ~ 2026.06
- 유학생 대상 학습 멘토링 진행 및 학습 수준별 맞춤형 진도 관리
- 매주 AI·음성 녹음 기반 복습 자료와 추가 학습 자료 제작 (→ LectureNote 문제의식과 직결)
- 멘티 맞춤형 피드백을 통한 학습 이해도 향상 지원
- 우수한 멘토링 운영·보고서 평가로 **학기 우수 멘토 선정**

---

## 보유 역량 (Skills)

| 역량 | 도구 · 방법론 |
|---|---|
| **Audit Analytics** | SAP GL 분석 · Rule Engine · Risk Scoring · YAML Config 추상화 |
| **Financial Modeling** | DCF/DDM · Black-Litterman · Sortino · CAPM · GARCH-M |
| **LLM Systems** | Context Orchestration · Simplified RAG · Prompt Pipeline · FastAPI/SSE |
| **Causal & Statistics** | Granger 인과 · Event Study · GARCH-X · 시계열 분석 |
| **Data Analysis** | Python · SQL · Pandas · 데이터 시각화 |
| **Automation** | Excel(OpenPyXL) 자동화 · 업무 프로세스 구조화 |

---

## 자격 사항 (Certifications)

| 자격 | 발급 기관 | 취득 |
|---|---|---|
| **KICPA** (한국공인회계사) | 금융위원회 | 2025 |
| **정보처리기사** | 한국산업인력공단 | 2025 |
| **AICE Associate** | KT · 한국경제신문 | 2026 |
| **SQLD** | 한국데이터산업진흥원 | 2025 |
| **컴퓨터활용능력 1급** | 대한상공회의소 | 2021 |
| **빅데이터분석기사** (필기 합격 · 실기 예정) | 한국데이터산업진흥원 | 2026 |

---

<details>
<summary>📎 <b>부록</b> — 추가 프로젝트 · 업무 개선 · 학습 기록</summary>

<br/>

메인 프로젝트를 뒷받침하는 추가 분석·업무 개선·학습 기록입니다.

**호텔 예약 분석 (Hotel Booking Analysis)** — 팀 프로젝트
- 호텔 예약 데이터 기반 고객 세분화 및 취소율 분석, K-Means 클러스터링으로 고객 유형 정의
- 🔗 [저장소](https://github.com/otto-Choi/Project-hotel_booking)

**Portfolio Study — 데이터 분석 학습·연습 기록**
- SQL · Python · 머신러닝 모델링 실습, 다양한 데이터셋 미니 프로젝트 모음
- 🔗 [저장소](https://github.com/otto-Choi/Portfolio-Study)

**업무 프로세스 개선 — 스터디카페 운영·총무 (2023.06 ~ 2025.02)**
- 엑셀 기반 인수인계 시스템 제작, 예약·환불 업무 프로세스 표준화로 업무 효율·일관성 개선
- 반복 업무를 체계화하는 과정에서 디지털 도구 활용·문제 해결 경험 축적

</details>

---

## 이 포트폴리오를 읽는 법

- **판단 과정 > 기술 스택 > 모델 성능** 순으로 강조했습니다. 각 README의 "왜 이 접근을 택했는가"가 핵심입니다.
- **수치는 결론이 아니라 근거(supporting evidence)** 이며, **한계도 함께 적었습니다** — 무엇을 검증하지 못했는지가 무엇을 했는지만큼 중요하다고 보기 때문입니다.

---

> 각 프로젝트의 설계 의사결정·검증 기록은 해당 저장소의 README와 `docs/`에 정리되어 있습니다.
