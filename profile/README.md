> # 🎙️ 바르미 (Barmi)

**바르미(Barmi)** 는 청각장애인을 위한 **AI 기반 영어 발음 교정 및 실시간 튜터링 플랫폼**입니다.  
본 레포지토리는 서비스의 전체 시스템을 아우르는 마스터 저장소로, 각 모듈간의 유기적인 결합과 통합 아키렉처를 설명합니다.

---

## 🏗 통합 시스템 아키텍처

바르미는 **분산 서비스 아키텍처**를 기반으로 실시간성(WebRTC)과 고부하 연산(AI)을 동시에 처리합니다.
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/20bbf523-e38e-437d-96f6-366b5565273a" alt="바르미 아키텍처">
</div>

---

## 📂 저장소 구성 가이드

각 레포지토리는 독립적인 기술 스택을 가지며, 역할에 따라 최적화되어 있습니다.

| 모듈명 | 주요 기술 스택 | 핵심 역할 |
| :--- | :--- | :--- |
| **[Backend](https://github.com/BarmiSpeechLab/backend)** | Java 17, Spring Boot, JPA | **서비스 코**: 도메인 비즈니스 로직, 사용자 데이터 관리, AI 분석 작업 발행 |
| **[Frontend](https://github.com/BarmiSpeechLab/frontend)** | React, Vite, Axios | **인터랙티브 UI**: 오디오 전처리(WAV 변환), 실시간 화상 UI, 발음 시각화 |
| **[AI Gateway](https://github.com/BarmiSpeechLab/ai-gateway)** | Python, FastAPI, RabbitMQ | **AI 오케스트레이터**: 분석 파이프라인 제어, LLM 기반 데이터 합성 및 결과 취합, 결과 퍼블리싱 |
| **[AI Model](https://faceted-animantarx-5f1.notion.site/fine-tuning?source=copy_link)** | PyTorch, HuggingFace | **핵심 지능**: Wav2Vec2 기반 음소 단위(Phoneme) 발음 오류 검사 모델 |
| **[Docs](https://github.com/BarmiSpeechLab/docs)** | Markdown, Notion | **문서화 허브**: 시스템 설계서, API 명세서, 팀 컨벤션 관리 |
| **[Infra](https://github.com/BarmiSpeechLab/infra)** | Docker, Nginx, RabbitMQ | **인프라 자동화**: 서비스 컨테이너화 및 리버스 프록시 설정, 작업 큐 관리 |

---

## 🚀 서비스 핵심 가치 체인

### 1. 비동기 AI 분석 파이프라인 (The "Brain" Loop)
1. **Frontend**: 사용자 발음을 녹음하고 브라우저에서 **WAV(PCM 16bit)** 로 정규화하여 전송합니다.
2. **Backend**: 요청을 수신 즉시 **RabbitMQ**에 적재하고 사용자에게 `taskId`를 반환하여 블로킹 없는 UX를 제공합니다.
3. **AI Gateway**: 큐에서 작업을 가져와 **Wav2Vec2 모델**에 추론을 요청하고, 결과를 수집합니다.
4. **LLM Synthesis**: 수치화된 AI 분석 결과에 사용자의 누적 성취도를 결합하여 개인화된 피드백을 생성합니다.
5. **Callback**: 최종 분석 리포트가 완성되면 DB에 저장하고 사용자에게 알립니다.

### 2. 실시간 WebRTC 코칭
- **OpenVidu 서버 사이드 제어**: 백엔드에서 보안 토큰을 동적으로 생성하여 무단 접속을 차단합니다.
- **실시간 시그널링**: 튜터와 학생 간의 음성/영상을 넘어, **웹소켓 시그널**을 통한 실시간 자막(STT) 및 리포트 공유 기능을 제공합니다.

---
## 사용 설명
### 회원가입/로그인

### 메인페이지

### AI 발음 분석

### 회화연습

### 리포트 기능

### 튜터링



---

## 🛠 실행 및 설치 (Getting Started)

전체 시스템은 Docker Compose를 통해 한 번에 실행할 수 있습니다.

```bash
# 전체 서비스 구동
docker-compose up -d --build
```

**주요 접속 정보:**
- **Frontend**: `http://localhost:3000`
- **Backend API**: `http://localhost:8080/swagger-ui/index.html`
- **RabbitMQ Dashboard**: `http://localhost:15672` (ID/PW: .env 설정 참조)

---

## 🎓 프로젝트의 기술적 지향점
- **AI-Optimized Infrastructure**: AI 엔진의 부하와 서비스 로직을 완벽히 격리하여 안정성을 확보했습니다.
- **Micro-Interaction**: 지연 시간이 긴 AI 연산 과중 속에서도 사용자 중심의 즉각적인 응답 체계를 구축했습니다.
- **Engineering Depth**: 단순 CRUD를 넘어, 다양한 언어(Java, Python, JS)와 미들웨어(RabbitMQ, OpenVidu)의 유기적인 조합을 실무적으로 풀어냈습니다.

---

## 📑 기술개발문서
- [[WebRTC] OpenVidu 설계](https://www.notion.so/WebRTC-OpenVidu-2f4fc74069a68086a278f420bd0d8a55?source=copy_link)
- [학습 커리큘럼 설계](https://www.notion.so/2f4fc74069a680a586bfcf2cdac6da38?source=copy_link)

## 👥 협업 컨벤션 
### 📄 Git 협업
- [브랜치 → 커밋/PR WorkFlow](https://www.notion.so/PR-WorkFlow-2eafc74069a680c88429c9052440d470?source=copy_link)
- [Branch 전략](https://www.notion.so/Branch-2defc74069a6807e806be81f1e28627b?source=copy_link)
- [Git 커밋 컨벤션](https://www.notion.so/Git-2eafc74069a68056b085d7e44cefcef0?source=copy_link)
- [Pull Request 전략](https://www.notion.so/Pull-Request-2eafc74069a68007a9aedecce45cd6bc?source=copy_link)
### 📄 팀 협업
- [Jira 이슈 컨벤션](https://www.notion.so/Jira-2eafc74069a680cf9071c4e799523901?source=copy_link)
- [그라운드 룰](https://www.notion.so/2eafc74069a680ab86c0c0e398e371ab?source=copy_link)
- [기술 문서 작성 룰](https://www.notion.so/2eafc74069a6807ba7cff1feca1a83d1?source=copy_link)

## 💁‍♂️ 프로젝트 팀원
| **Frontend** | **Backend** | **WebRTC** | **AI** | **AI/Infra** | **PM/Infra** |
|:---:|:---:|:---:|:---:|:---:|:---:|
| ![](https://github.com/jeongunun.png?width=120&height=120) | ![](https://github.com/kz770.png??width=120&height=120) | ![](https://github.com/gahuily.png??width=120&height=120) | ![](https://github.com/Dae12-Han.png??width=120&height=120) | ![](https://github.com/sweetpotatolove.png??width=120&height=120) | ![](https://github.com/Thedduro.png??width=120&height=120) |
| [석정운](https://github.com/jeongunun) | [유현진](https://github.com/kz770) | [한가희](https://github.com/gahuily) | [김소원](https://github.com/Dae12-Han) | [박사랑](https://github.com/sweetpotatolove) | [임선우](https://github.com/Thedduro) |
