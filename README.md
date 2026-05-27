# 📊 신뢰할 수 있는 통계 가이드라인 기반의 RAG 보조 어시스턴트

> **데이터 분석 과정에서 마주하는 통계적 의사결정(분석 기법 선택, 가정 검증, 결과 해석 등)을 돕는 RAG 기반 AI 챗봇 웹 서비스입니다.**

기존 대형 언어 모델(LLM)의 고질적인 한계인 환각 현상(Hallucination)을 차단하기 위해, 사전 수집한 공신력 있는 전공 지식 베이스(Penn State)의 벡터 데이터베이스 안에서만 정답을 탐색하도록 통제하는 RAG 아키텍처를 구현했습니다.

---

## 🛠️ 주요 기능 (Key Features)
* **대화형 통계 컨설팅**: 자연어 질문(예: "Durbin-Watson 통계량이 1.1이 나왔어. 문제가 있는 거야?")에 대한 맞춤형 피드백 제공
* **철저한 근거 중심 답변**: 답변 출력 시 텍스트 하단에 참고한 통계 전공 문헌의 구체적인 출처 명시
* **안전한 환각 차단 (Exception Handling)**: 외부 문헌 DB에 관련 가이드라인이 존재하지 않을 경우 "가이드라인이 존재하지 않음"으로 예외 처리

---

## 🏗️ 시스템 아키텍처 (System Architecture)
Streamlit UI와 LangChain 파이프라인을 결합한 가볍고 빠른 로컬 RAG 시스템입니다.

1. **User UI (Streamlit)**: 사용자가 자연어로 통계 관련 질문 입력
2. **LangChain Pipeline**: 사용자 질문을 벡터화하여 로컬 Vector DB(FAISS)에서 관련 지식 문단 추출
3. **Prompt Engineering**: 검색된 DB 내용만을 절대적 근거로 삼도록 설계된 시스템 프롬프트 조립
4. **LLM (GPT-4o-mini)**: 팩트 기반의 통계 답변 및 정확한 레퍼런스 출처 출력

---

## 💻 기술 스택 (Tech Stack)
* **Frontend / UI**: Streamlit
* **RAG Framework**: LangChain
* **Vector Database**: FAISS (Meta)
* **LLM API**: OpenAI GPT-4o-mini
* **Data Scraping & Parsing**: BeautifulSoup, markdownify

---

## 👥 팀원 및 역할 분담 (Team & Roles)
* **통계 도메인 & 데이터 리드**: 크롤링 전공 웹페이지 선정, 추출 텍스트 노이즈 검수, 챗봇 답변의 통계학적 정확성(QA) 테스트
* **파이프라인 & 백엔드 리드**: BeautifulSoup 웹 크롤링 스크립트 작성, LangChain 기반 RAG 파이프라인 조립 및 FAISS 세팅
* **프론트엔드 & 프롬프트 리드**: Streamlit 웹 UI 구현, 외부 DB만 참고하도록 통제하는 시스템 프롬프트 작성 및 최적화