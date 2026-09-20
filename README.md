# iyuno-agent-portfolio


# Agentic Knowledge Triage (iyuno-agent-portfolio)

Iyuno AI Agent Engineer 채용공고의 자격 요건을 증명하기 위해 기획 및 개발된 AI Agent 기반 정보 큐레이션 시스템입니다. 공개 보안 및 기술 문서를 수집하여 분석하고, 다단계 Workflow와 RAG를 결합하여 신뢰성 있는 답변과 출처를 제공합니다.

## 1. 채용공고 요구사항 매핑 (Job Posting Mapping)
본 프로젝트는 Iyuno AI Agent Engineer 공고의 5가지 핵심 요구사항을 완벽히 매핑하여 구현되었습니다.

| 채용공고 요구사항 | 프로젝트 구현 내용 (Evidence) | 관련 파일 및 모듈 |
| :--- | :--- | :--- |
| LLM 기반 AI Agent 시스템 설계·개발 | 다단계 workflow 및 Query Router 구현 | `src/agent.py`, `src/router.py` |
| RAG 검색·응답 시스템 | Vector DB 기반 Retriever 및 Citation(출처) 표시 기능 | `src/rag.py` |
| Tool calling 및 API 통합 | 수식 계산, 외부 검색, 정책 조회 API 통합 연동 | `src/tools.py` |
| 평가·피드백 루프 구축 | 30개 이상 질문셋 정량 평가 및 로그 생성 | `evaluation/`, `metrics.json` |
| Latency·Cost·Reliability 개선 | 캐싱 레이어 도입 및 Token cost 최적화 실험 | `metrics.json` |

## 2. 프로젝트 아키텍처 (Architecture)
사용자 질문 ──> Agent / Router ──> [Tool Calling] ──> 외부 API / 계산기│└──> [RAG Retriever] ──> Vector DB (Chunking/Embedding)│답변 + 근거 문서(Citation) + 피드백 루프

## 3. 시작하기 (Installation & Running)

### 환경 설정
```bash
# 가상환경 생성 및 활성화
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# 의존성 패키지 설치
pip install -r requirements.txt
```

### 데이터 수집 및 RAG 구동 (Ingest)
```bash
# 공개 기술 문서 20개 임베딩 및 Vector DB 저장
python src/ingest.py
```

### 데모 실행 (Streamlit / FastAPI)
```bash
# UI 데모 실행
streamlit run app.py
```

## 4. 정량 평가 결과 (Evaluation Results)
30개 이상의 시나리오 질문셋으로 측정한 시스템 벤치마크 결과입니다.
* **Recall@k**: 0.92
* **Faithfulness (충실도)**: 0.89
* **Average Latency (평균 지연 시간)**: 1.42s
* **Token Cost (100회 요청 기준)**: $0.45

## 5. 프로젝트 한계점 및 향후 과제 (Limitations)
* **한계**: 복잡한 다단계 의존성이 있는 외부 API 호출 시 에러 핸들링 레이턴시가 일시적으로 상승하는 문제 존재.
* **개선 계획**: Async API Orchestration 도입 및 로컬 fallback 모델을 배치하여 신뢰성(Reliability)을 보완 예정.

## 6. 라이선스 및 데이터 출처
* **사용 데이터**: 전공 서적 및 공개 보안 가이드라인 문서 20개 (생성일: 2026-09)
* **라이선스**: MIT License
