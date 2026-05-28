# Stats-RAG-Assistant

신뢰할 수 있는 통계 가이드라인 기반의 RAG 보조 어시스턴트.
Penn State STAT 501·504 강의 자료를 벡터 DB로 구축하고, 질문에 대해 **검증된 출처만**을 근거로 한국어로 답변합니다.

> 📚 출처: [Penn State STAT 501 Regression Methods](https://online.stat.psu.edu/stat501/), [STAT 504 Analysis of Discrete Data](https://online.stat.psu.edu/stat504/)

---

## 🏗️ 아키텍처

```
[사용자 질문]
    ↓
[Streamlit Web UI]                  ← Step 4 예정
    ↓
[FAISS 벡터 검색 — 상위 4개 청크]
    ↓
[GPT-4o-mini + 시스템 프롬프트]
    ↓
[한국어 답변 + 출처(Penn State URL) 표기]
```

**기술 스택**: BeautifulSoup + markdownify → LangChain + FAISS → GPT-4o-mini → Streamlit

---

## 📁 폴더 구조

```
opensource_statchatbot/
├── data/                          # 크롤링한 원본 텍스트
│   ├── stat501_full_data.txt
│   └── stat504_full_data.txt
├── vector_db/                     # FAISS 인덱스
│   ├── faiss_stat501_db/          # STAT 501 단독
│   └── faiss_stat_integrated_db/  # STAT 501 + 504 통합
├── notebooks/
│   ├── crawling/                  # Penn State 사이트 크롤링
│   ├── build_db/                  # 텍스트 → 벡터 DB 변환
│   ├── mvp/                       # RAG 챗봇 MVP
│   └── _archive/                  # 옛 실험 노트북 (참고용)
├── .env.example                   # 환경 변수 템플릿
├── .gitignore
├── requirements.txt
└── README.md
```

---

## 🚀 빠른 시작

### 1. 레포지토리 클론

```bash
git clone https://github.com/csm4165/Stats-RAG-Assistant.git
cd Stats-RAG-Assistant
```

### 2. 가상환경 + 의존성 설치 (권장)

```bash
python -m venv .venv
# Windows
.venv\Scripts\activate
# macOS / Linux
source .venv/bin/activate

pip install -r requirements.txt
```

### 3. OpenAI API 키 설정

`.env.example`을 복사해서 `.env`를 만들고, 본인의 OpenAI API 키를 넣습니다.

```bash
cp .env.example .env   # Windows에서는 copy .env.example .env
```

`.env` 파일을 메모장으로 열어서:
```
OPENAI_API_KEY=sk-proj-여기에_본인의_키
```

> ⚠️ `.env`는 `.gitignore`로 제외되어 GitHub에 올라가지 않습니다. 절대 `.env.example`에 실제 키를 넣지 마세요.

### 4. 챗봇 MVP 실행

```bash
jupyter notebook
```
브라우저에서 `notebooks/mvp/MVPmodel(501db).ipynb` 열고 **Cell → Run All** 실행 → 미리 설정된 통계 질문에 대한 한국어 답변이 나옵니다.

---

## 🔄 처음부터 다시 빌드하고 싶다면

1. **크롤링 다시**: `notebooks/crawling/` 안의 두 노트북 실행 → `data/`에 텍스트 파일 생성
2. **DB 빌드**: `notebooks/build_db/vector_db501.ipynb` → `notebooks/build_db/build_integrated_db.ipynb` 순서로 실행
3. **챗봇 테스트**: `notebooks/mvp/MVPmodel(501db).ipynb`

> 💡 이미 빌드된 `vector_db/faiss_stat_integrated_db/`가 있다면 크롤링·DB 빌드는 건너뛰어도 됩니다.

---

## 👥 팀 역할 분담

| 담당 영역 | 작업 |
|---|---|
| 통계 도메인 & 데이터 | 크롤링 페이지 선정, 텍스트 검수, QA 평가 질문 작성 |
| 파이프라인 & 백엔드 | 크롤링 스크립트, LangChain RAG, FAISS 인덱싱 |
| 프론트엔드 & 프롬프트 | Streamlit UI, 시스템 프롬프트 튜닝 |

---

## 📝 라이선스 및 데이터 출처

- 코드: 학습/연구용 오픈소스
- 데이터: Penn State Eberly College of Science 공개 강의 자료
  - [STAT 501: Regression Methods](https://online.stat.psu.edu/stat501/)
  - [STAT 504: Analysis of Discrete Data](https://online.stat.psu.edu/stat504/)

---

## 🔗 참고 자료

- [LangChain Documentation](https://python.langchain.com/)
- [FAISS Documentation](https://faiss.ai/)
- [Streamlit Documentation](https://docs.streamlit.io/)
- 레퍼런스 프로젝트: [Legal-RAG-Chatbot](https://github.com/wngud09/Legal-RAG-Chatbot)
