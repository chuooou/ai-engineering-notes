# AI Engineering Notes

AI/AX를 공부하면서 읽은 아티클, 새롭게 배운 개념,  
개발 및 업무에 적용해본 아이디어와 실험을 기록하는 저장소입니다.

단순히 내용을 요약하는 것보다  
**왜 이런 방식이 필요한지, 실제 업무에는 어떻게 적용할 수 있는지**를 생각하며 정리하는 것을 목표로 합니다.

---

## Documents

### AX

#### DTO 변경 대응 업무를 AX 관점에서 재설계해보기

프론트엔드 개발에서 반복적으로 발생하는 DTO 변경 대응 업무를 대상으로  
현재 Workflow를 분석하고 `Rule / AI / Human`의 역할을 나눠 AX 관점에서 다시 설계해본 기록입니다.

주요 내용

- 기존 DTO 변경 대응 Workflow 분석
- AX 적용 후보 업무 선정
- Rule / AI / Human 역할 분리
- Before / After Workflow 설계
- AX 적용 효과를 측정하기 위한 평가 기준 정의
- 추후 OpenAPI 기반 자동화 구현 계획

📄 [문서 보기](./ax/DTO%20변경%20대응%20업무를%20AX%20관점에서%20재설계해보기.md)

---

### Compound Engineering

#### AI 코딩을 반복 작업이 아니라 쌓이는 개발로 만드는 방법

Compound Engineering 관련 글을 읽고,  
AI를 단순 코드 생성 도구로 사용하는 것을 넘어  
개발 과정에서 얻은 지식과 해결 방법을 다음 작업에 재사용하는 방식에 대해 정리했습니다.

주요 내용

- AI Coding과 Compound Engineering의 차이
- 반복되는 문제 해결 과정을 지식으로 축적하는 방법
- `plans / solutions / AGENTS.md`를 활용한 개발 Context 관리
- AI와 함께 개발할 때 Context를 누적시키는 방법

📄 [문서 보기](./compound-engineering/AI%20코딩을%20반복%20작업이%20아니라%20쌓이는%20개발로%20만드는%20방법.md)

---

## What I'm Learning

현재 다음 주제를 중심으로 공부하고 있습니다.

- AI / LLM
- AX (AI Transformation)
- AI-assisted Software Engineering
- Compound Engineering
- RAG
- AI Agent
- Tool Calling / MCP
- Workflow Automation

앞으로 공부하면서 생긴 질문이나 실제 개발 업무에서 느낀 불편함을  
작은 설계와 실험으로 연결해 기록할 예정입니다.
