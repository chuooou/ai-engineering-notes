# Compound Engineering - AI 코딩을 반복 작업이 아니라 쌓이는 개발로 만드는 방법

> 참고 문서: https://every.to/guides/compound-engineering  
> Every - Compound Engineering  
> 2026.09.10  

## 

`Compound Engineering`이라는 말을 처음 봤을 때는
그냥 AI한테 코드를 좀 더 잘 짜게 만드는 개발 방법론인가? 싶었다.

근데 읽어보니 단순히 **AI로 코드를 빨리 만드는 방법**은 아니었다.

내가 이해한 핵심은 이거다.

> 이번 개발에서 얻은 경험이 다음 개발에도 남아 있어야 한다.

보통은 기능 하나를 만들고 문제가 생기면 고친 다음 바로 다음 기능으로 넘어간다.

```text
기능 개발
↓
버그 발생
↓
수정
↓
PR
↓
끝
```

Compound Engineering에서는 여기서 끝내지 않는다.

```text
기능 개발
↓
문제 발견
↓
수정
↓
왜 문제가 생겼는지 정리
↓
재사용 가능한 규칙으로 만듦
↓
문서 / 테스트 / AGENTS.md 등에 남김
↓
다음 개발에서는 같은 문제를 처음부터 피함
```

즉 **코드만 좋아지는 게 아니라 개발 시스템 자체가 점점 좋아지는 것**이다.

---

# 기본 흐름

원문에서 이야기하는 기본 Loop는 다음과 같다.

```text
Plan
↓
Work
↓
Review
↓
Compound
↓
Repeat
```

처음 세 단계까지는 기존 개발에서도 어느 정도 하던 일이다.

중요한 건 마지막 `Compound`다.

Compound가 빠지면 결국

> AI를 이용해서 기존 개발 프로세스를 조금 더 빠르게 한 것

에 가깝다.

---

# 1. Plan

AI한테 요청하자마자 바로 코드를 짜게 하지 않는다.

예를 들어 회원가입 기능을 만든다고 했을 때

```text
회원가입 페이지 만들어줘
```

하고 바로 구현시키는 게 아니라 먼저 프로젝트를 조사하게 한다.

```text
회원가입 기능을 구현하려고 한다.

바로 코드를 수정하지 말고 먼저 확인해줘.

- 현재 auth 구조
- 기존 API 호출 방식
- React Hook Form 사용 방식
- Zod schema 구조
- Query 사용 방식
- 비슷한 feature
- 수정이 필요한 파일
- 예상되는 edge case

확인 후 구현 계획을 작성해줘.
```

여기서 중요한 건 AI가 코딩을 못 해서 계획을 세우는 게 아니다.

AI도 결국 **현재 프로젝트에 대한 Context가 있어야 좋은 결정을 할 수 있기 때문**이다.

Framework에서 일반적으로 좋은 코드와
내 프로젝트에서 좋은 코드는 다를 수 있다.

그래서 구현 전에

```text
요구사항
+
기존 코드
+
프로젝트 규칙
+
기존에 해결한 문제
```

를 먼저 읽게 하는 게 중요하다.

---

# 2. Work

Plan이 정해졌으면 그다음부터 구현한다.

이때는 개발자가 AI가 생성하는 코드를 한 줄씩 지켜볼 필요는 없다고 한다.

대신 Plan과 검증 장치가 중요하다.

```text
Plan
↓
구현
↓
Lint
↓
Type Check
↓
Test
↓
Build
```

물론 프로젝트에 실제로 존재하는 검증 명령만 실행해야 한다.

중간에 문제가 발생하면 그냥 계속 밀고 가지 않고

```text
문제 확인
↓
원인 분석
↓
Plan 수정
↓
다시 구현
```

한다.

여기까지는 내가 기존에 AI 코딩하면서 하던 방식과 크게 다르지 않았다.

---

# 3. Review

여기서 처음 궁금했던 게 있었다.

원문에

> Have multiple agents review the output.

이라는 내용이 나온다.

처음에는

> Codex로 코드를 만들었으면 Claude한테 검증시키라는 건가?

라고 이해했다.

근데 꼭 그런 의미는 아니었다.

핵심은 **다른 회사의 AI를 사용하는 것**이 아니라
**구현과 독립된 관점에서 여러 Reviewer가 코드를 보는 것**이다.

예를 들면

```text
구현 Agent
↓
코드 생성

Reviewer 1
→ TypeScript / Type Safety

Reviewer 2
→ React 구조

Reviewer 3
→ Architecture

Reviewer 4
→ Security

Reviewer 5
→ Performance

Reviewer 6
→ Code Simplicity
```

처럼 역할을 나눌 수 있다.

그래서 이런 것도 가능하다.

```text
Codex 구현
→ 별도의 Codex Reviewer

Claude 구현
→ Claude Sub Agent 여러 개로 Review

Codex 구현
→ Claude Review

Claude 구현
→ Codex Review
```

즉

```text
Codex → Claude
```

가 필수 규칙은 아니다.

내가 이해한 핵심은 **구현한 Agent와 Review하는 역할을 분리하는 것**이다.

같은 모델을 사용하더라도 별도의 Agent나 Context에서

```text
TypeScript 관점으로 검토해줘.

React lifecycle 관점으로 검토해줘.

불필요하게 복잡한 부분이 있는지 검토해줘.
```

처럼 나눌 수 있다.

다만 구현과 검증 모델까지 다르게 하면 서로 놓치는 부분이 다를 수 있기 때문에 추가 검증 수단으로 사용할 수는 있을 것 같다.

그래서 앞으로는

```text
AI가 코드 생성
→ 내가 처음부터 끝까지 직접 Review
```

만 하는 방식보다는

```text
AI 구현
↓
AI Review
↓
문제 후보 정리
↓
내가 최종 판단
```

형태로 활용해보려고 한다.

중요한 건 AI Reviewer가 말한 걸 무조건 수정하는 게 아니다.

Review 결과를 예를 들어

```text
P1 - 반드시 수정
P2 - 수정 권장
P3 - 개선 가능
```

처럼 나눈 다음 최종 판단은 개발자가 하는 방식이다.

---

# 4. Compound

여기가 이 글의 핵심이다.

나도 처음에는

> 그러면 AI한테 "Compound Engineering 적용해서 개발해줘"라고 하면 되는 건가?

라는 생각이 들었다.

결론은 **처음 시작할 때는 그렇게 요청할 수 있지만 그것만으로 Compound가 되는 건 아니다.**

예를 들어 오늘 AI한테

```text
Compound Engineering 방식으로 개발해줘.
```

라고 해서

```text
Plan
→ 구현
→ Review
→ 문제 정리
```

까지 잘했다고 해도

다음 세션에서 그 지식이 아무 데도 남아 있지 않으면 다시 처음부터 시작한다.

그건 Compound라고 하기 어렵다.

Compound에서 중요한 건 **이번 작업에서 배운 걸 프로젝트에 남기는 것**이다.

예를 들면 이런 구조를 만들 수 있다.

```text
project/
├─ AGENTS.md
│
├─ docs/
│  ├─ plans/
│  └─ solutions/
│
└─ src/
```

### AGENTS.md

AI가 작업할 때 항상 알아야 하는 프로젝트 규칙을 적는다.

예를 들면

```text
서버 상태는 TanStack Query로 관리한다.

Form은 React Hook Form + Zod를 사용한다.

API 함수 안에서 navigate나 toast를 실행하지 않는다.

불필요한 useEffect를 만들지 않는다.
```

같은 내용이다.

### docs/plans

기능을 만들기 전에 결정한 내용을 남긴다.

```text
왜 이렇게 구현하는지
어떤 파일을 수정하는지
어떤 상태를 source of truth로 사용할지
어떤 edge case가 있는지
```

등을 기록한다.

### docs/solutions

실제 개발 중 발생한 문제와 해결 방법을 저장한다.

예를 들어 WebSocket을 구현하다 이런 문제가 생겼다고 하자.

```text
Reconnect 이후 message listener가 중복 등록됨.
```

그냥

```text
removeEventListener 추가
→ 해결
```

하고 끝내면 일반적인 버그 수정이다.

Compound 방식이라면

```text
문제
왜 발생했는지
어떻게 해결했는지
비슷한 문제가 어디에서 다시 발생할 수 있는지
다음에는 어떻게 예방할지
```

까지 남긴다.

그리고 정말 반복적으로 적용할 수 있는 규칙이라면 `AGENTS.md`까지 올린다.

```text
WebSocket listener 등록 시 cleanup을 반드시 확인한다.

Reconnect 시 listener가 중복 등록되지 않는지 확인한다.
```

여기서 더 나아가 자동 테스트로 잡을 수 있다면 테스트로 만든다.

그러면 다음에는 사람이

> listener cleanup 빠졌는데?

라고 직접 말하지 않아도 시스템이 문제를 발견할 수 있다.

내가 이해한 Compound의 가장 중요한 질문은 결국 이것이다.

> 다음에 같은 문제가 생겼을 때 내가 또 직접 알려줘야 하나?

YES라면 아직 제대로 Compound되지 않은 것이고,

```text
AGENTS.md
Test
Lint Rule
Reviewer
docs/solutions
```

중 하나가 자동으로 알려줄 수 있다면 이전보다 한 단계 좋아진 시스템이 된다.

---

# 모든 걸 AGENTS.md에 넣는 건 아니다

여기서 하나 주의할 점이 있다.

문제가 생길 때마다 AGENTS.md에 다 적기 시작하면 파일이 계속 커지고 결국 AI가 중요한 규칙을 찾기 어려워질 수 있다.

그래서 나는 대략 이렇게 구분하면 될 것 같다.

```text
항상 지켜야 하는 프로젝트 규칙
→ AGENTS.md

특정 문제의 원인과 해결 과정
→ docs/solutions

특정 기능을 설계하면서 내린 결정
→ docs/plans

기계적으로 검증 가능한 규칙
→ Test / ESLint / Type Check
```

예를 들어

```text
2026년 9월 10일 회원가입 개발 중
Axios refresh 요청이...
```

같은 긴 사건 기록을 AGENTS.md에 적는 게 아니다.

`docs/solutions/auth/duplicate-refresh-request.md`

같은 곳에 상세 내용을 적고,

거기서 나온 일반적인 규칙만

```text
Refresh API는 인증 401 interceptor를 다시 타지 않도록 한다.
```

같이 AGENTS.md에 남기는 방식이다.

---

# BowChat에 대입해보기

내 프로젝트에서 이미 비슷한 예가 있다.

인증 처리에서 동시에 여러 API가 401을 반환할 수 있다.

```text
Request A ─ 401
Request B ─ 401
Request C ─ 401
```

여기서 요청마다 refresh를 보내면

```text
Refresh A
Refresh B
Refresh C
```

가 발생할 수 있다.

그래서 `refreshPromise`를 공유해서

```text
Request A ─┐
Request B ─┼─ 401
Request C ─┘
           ↓
       Refresh 1회
           ↓
     새로운 Access Token
           ↓
       원 요청 재실행
```

하도록 구현했다.

여기서 그냥 코드만 만들고 끝내면 이 구현은 현재 코드 안에만 존재한다.

Compound 방식으로 생각하면 여기서

```text
docs/solutions/auth/concurrent-401-refresh.md
```

를 만들고

왜 `_retry`와 `refreshPromise`가 각각 필요한지 기록할 수 있다.

```text
_retry
→ 동일 요청이 무한 반복되는 것 방지

refreshPromise
→ 동시에 발생한 여러 401이 각각 refresh를 호출하는 것 방지
```

그리고 AGENTS.md에는 더 일반적인 규칙만 남긴다.

```text
401 복구 구현 시 동일 요청 재시도 방지와
동시 Refresh 중복 방지를 별개의 문제로 본다.

Refresh API가 인증 interceptor를 다시 타지 않도록 확인한다.
```

그러면 나중에 AI가 인증 코드를 수정할 때 이 규칙을 먼저 볼 수 있다.

이게 내가 이해한 Compound Engineering이다.

---

# 그러면 실제 개발할 때 어떻게 요청할까?

처음에는 AI한테 명시적으로 이렇게 요청해도 될 것 같다.

```text
이번 작업은 Compound Engineering 방식으로 진행해줘.

1. AGENTS.md 확인
2. 기존 코드 조사
3. docs/solutions에 관련 사례가 있는지 확인
4. 구현 Plan 작성
5. Plan 기준으로 최소 변경 구현
6. 프로젝트 검증 명령 실행
7. TypeScript / React / Architecture / Security 관점 Review
8. Review 결과 수정
9. 이번 작업에서 다시 사용할 수 있는 지식이 있는지 확인
10. 필요한 경우 docs/solutions 또는 AGENTS.md 업데이트
```

하지만 계속 이렇게 긴 프롬프트를 입력하는 게 최종 목표는 아니다.

결국 이 Workflow 자체도 `AGENTS.md`에 넣는다.

그러면 나중에는

```text
입찰방 구현해줘.
```

정도만 요청해도 AI가

```text
프로젝트 규칙 확인
↓
기존 코드 조사
↓
Plan
↓
Work
↓
Review
↓
Compound
```

순서를 따르게 만드는 게 목표다.

즉 **좋은 프롬프트를 매번 작성하는 것보다 좋은 개발 환경을 한 번 만들어 놓는 게 중요하다.**

---

# 내가 이해한 개발자의 역할 변화

예전에는 AI Coding이라고 하면

```text
내가 요구사항 설명
↓
AI 코드 생성
↓
내가 코드 검토
↓
수정
```

정도로 생각했다.

Compound Engineering에서는 개발자의 역할이 조금 달라진다.

직접 코드를 많이 입력하는 것보다는

```text
무엇을 만들지 정의
↓
어떤 방식으로 만들어야 하는지 Plan
↓
AI가 따라야 할 규칙 정의
↓
결과 Review
↓
잘못된 패턴 발견
↓
그 패턴을 시스템에 다시 반영
```

하는 일이 중요해진다.

결국 개발자는 AI한테 일을 던지는 사람이 아니라

> AI가 계속 좋은 코드를 만들 수 있는 환경을 만드는 사람

에 가까워지는 것 같다.

---

# 정리

처음에는 Compound Engineering이 새로운 AI Coding 기법인 줄 알았다.

지금은 조금 다르게 이해하고 있다.

```text
AI Coding
= 이번 코드를 AI가 잘 만들어주는 것

Compound Engineering
= 이번 개발을 통해 다음 AI 개발까지 더 좋아지게 만드는 것
```

특히 중요한 건 마지막 `Compound` 단계다.

```text
버그를 수정했다.
```

에서 끝나는 게 아니라

```text
왜 발생했지?

다시 발생할 수 있나?

다음에는 AI가 알아서 피할 수 있나?

문서로 남길까?

AGENTS.md 규칙으로 만들까?

Test나 Lint로 자동 검증할 수 있을까?
```

까지 생각한다.

앞으로 AI를 사용해서 개발할 때는
단순히 **"이번 코드 잘 나왔나?"**만 보는 것보다

> **"이번 개발에서 배운 게 다음 개발에도 남았나?"**

를 같이 확인해보려고 한다.
