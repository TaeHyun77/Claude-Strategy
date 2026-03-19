**Claude Code 기본적인 설정**

https://www.youtube.com/watch?v=1_bRmkUvjHA&t=867s

### **컨텍스트 엔지니어링**

---

> AI에게 작업을 요청할 때, 불필요한 정보는 줄이고 꼭 필요한 정보만 정확하게 전달하는 기술
> 

AI는 입력된 맥락을 바탕으로 요청을 해석하고 결과를 생성하기 때문에, 어떤 정보를 얼마나, 어떤 구조로 제공하느냐에 따라 결과 품질이 크게 달라집니다.

Claude Code 환경에서는 이러한 컨텍스트를 체계적으로 제공하기 위해 claude.md 파일을 활용합니다.

### Claude.md

---

> 
> 
> 
> Claude Code가 시작될 때 자동으로 읽는 마크다운 파일로, AI에게 프로젝트의 배경지식과 작업 규칙을 지속적으로 제공하는 컨텍스트 문서입니다.
> 

이 파일에는 보통 프로젝트 개요, 기술 스택, 폴더 구조, 코딩 스타일, 아키텍쳐 규칙, 개발 지침 등이 포함되어 있습니다.

즉, claude.md는 매 세션마다 반복해서 설명하기 번거로운 내용을 미리 정리해 두는 문서입니다.

Claude는 이를 바탕으로 프로젝트를 더 빠르게 이해하고, 더 일관된 방식으로 응답하거나 코드를 생성할 수 있습니다.

Anthropic 공식 문서의 설명에 따르면, claude.md는 단순 참고 메모가 아니라 claude의 프롬프트 일부로 작동하는 고영향 문서라고 합니다.

**왜 CLAUDE.md가 필요한가**

LLM ( Large Language Model, 대규모 언어 모델 )은 자연어를 이해하고 생성할 수 있지만, 한 번에 처리할 수 있는 입력과 출력의 길이에는 제한이 있으며, 이를 `컨텍스트 윈도우`라고 합니다.

또한, LLM은 세션 간 상태를 자동으로 저장하지 않기 때문에, 새로운 세션이 시작되면 프로젝트에 대해 아무것도 모르는 상태에서 시작됩니다.

컨텍스트 윈도우가 제한되어 있기 때문에, 대화가 길어지거나 정보가 많아질수록 오래된 맥락이나 덜 중요한 정보는 점차 밀려나고 잊히게 되므로 초기에는 프로젝트 구조, 기술 스택, 아키텍처 원칙, 디버깅 배경 등을 잘 이해하고 있었더라도, 여러 번의 질의응답과 수정 과정을 거치다 보면 AI가 처음의 전제를 놓치는 경우가 생길 수 있습니다.

이때, claude.md는 세션마다 프로젝트의 핵심 정보와 규칙을 다시 불러오는 기준점 역할을 합니다.

즉, 단순한 설명 문서가 아니라 프로젝트의 기억을 붙잡아 주는 앵커 역할

**CLAUDE.md가 제공하는 효과**

1. 새로운 세션에서도 Claude가 프로젝트 구조와 기술 스택, 도메인 개념을 빠르게 파악할 수 있습니다.
2. 코드 스타일과 아키텍처 규칙, 작업 방식이 더 일관되게 유지됩니다.
3. 긴 대화 중 일부 컨텍스트가 유실되어도 다시 기준점을 복원할 수 있습니다.
4. 매번 반복해서 설명해야 하는 내용을 줄여 작업 효율이 높힙니다.
5. 범용 AI를 프로젝트 맥락에 맞는 맞춤형 개발 에이전트처럼 활용할 수 있습니다.

**Claude.md 관리 5원칙**

1. 짧고 명확하게 300줄 이하를 유지해라
2. 추측 불가능한 정보만 넣기
    
    ex ) 이 프로젝트만의 디렉터리 구조, 내부 도메인 규칙, 여러 규칙 등등
    
3. 세부 내용은 Progressive Disclosure로 분리하기
    
    모든 내용을 claude.md에 한 번에 넣지 말고, 핵심만 남기고 세부 문서는 별도로 분리한 뒤 필요할 때 불러오는 구조가 좋습니다.
    
    이렇게 하면 claude.md는 가볍게 유지되고, 자세한 내용은 필요할 때만 참조할 수 있습니다.
    
    ```jsx
    CLAUDE.md → 핵심 개요와 문서 안내
    agent_docs/building_the_project.md
    agent_docs/running_tests.md
    agent_docs/code_conventions.md
    ```
    
4. 실수가 발생하면 즉시 반영해 반복 실수를 줄이자
5. 주기적으로 리뷰하고 불필요한 내용을 정리해 최신 상태를 유지하자

⭐⭐⭐⭐

대부분의 세션은 Plan 모드에서 시작하는 것이 좋습니다.  ( Windows : `Shift+Tab` or `alt+m` )

Plan 모드에서 계획을 충분히 다듬은 뒤, Auto-accept 모드로 전환하여 실행하면 대체로 만족스러운 결과를 한 번에 얻을 수 있습니다.

1. 프로젝트의 WHAT(구조) , WHY(목적, 의도) , HOW(작동 방식) 을 간결히 담는 것이 좋습니다. ( 과하게 x )
2. LLM은 약 150~200개의 지시사항을 안정적으로 따를 수 있으므로 가능한 보편적이고 적은 지시사항을 추가하자
3. 대형 프로젝트에서는 모든 정보를 하나의 파일에 담기 어렵기 때문에, 필요한 정보만 단계적으로 제공하는 방식을 사용하는 것이 좋습니다.
    
    세부 지침은 agent_docs/ 폴더에 별도 마크다운 파일로 분리하고, CLAUDE.md에는 문서 목록, 간단한 설명, 필요 시 참조하라는 지시만 포함하며 코드 스니펫 대신 `file:line` 참조를 사용해 최신성을 유지하는 것이 좋습니다.
    
4. 스타일은 도구로 강제하고, AI는 사고와 설계에 집중하게 만들어라
5. /init 같은 기능으로 claude.md 초안을 만들 수는 있지만, 이 내용을 그대로 신뢰하고 사용하는 것은 추천되지 않습니다.
    
    최종 내용은 직접 검토하고 다듬는 것이 좋으며, 한 줄 한 줄이 실제로 필요한 규칙인지 확인하는 것이 좋습니다.
    

```jsx
### 1. Plan Node Default
- Enter plan mode for ANY non-trivial task (3+ steps or architectural decisions)
- If something goes sideways, STOP and re-plan immediately - don't keep pushing
- Use plan mode for verification steps, not just building
- Write detailed specs upfront to reduce ambiguity

// 계획먼저 세우고 문제가 생기면 멈추어 재설계를 하며 항상 더 좋은 방법이 있는지 고민하게 한다.

### 2. Subagent Strategy
- Use subagents liberally to keep main context window clean
- Offload research, exploration, and parallel analysis to subagents
- For complex problems, throw more compute at it via subagents
- One tack per subagent for focused execution

// Subagent를 활용하자

### 3. Self-Improvement Loop
- After ANY correction from the user: update `tasks/lessons.md` with the pattern
- Write rules for yourself that prevent the same mistake
- Ruthlessly iterate on these lessons until mistake rate drops
- Review lessons at session start for relevant project

// 사용자의 수정 사항이 생길 때마다 특정 파일에 업데이트하여 같은 실수를 반복하지 않도록 하자.

### 4. Verification Before Done
- Never mark a task complete without proving it works
- Diff behavior between main and your changes when relevant
- Ask yourself: "Would a staff engineer approve this?"
- Run tests, check logs, demonstrate correctness

// 테스트 전에 절대 작업 완료를 하지 않도록 하여 신뢰성을 높히자

### 5. Demand Elegance (Balanced)
- For non-trivial changes: pause and ask "is there a more elegant way?"
- If a fix feels hacky: "Knowing everything I know now, implement the elegant solution"
- Skip this for simple, obvious fixes - don't over-engineer
- Challenge your own work before presenting it

// 중요한 변경 사항의 모호한 답변이라고 판단된다면, 멈추고 더 좋은 방법에 대해 탐색을 요구해라
// 간단한 사항의 경우는 x

### 6. Autonomous Bug Fizing
- When given a bug report: just fix it. Don't ask for hand-holding
- Point at logs, errors, failing tests - then resolve them
- Zero context switching required from the user
- Go fix failing CI tests without being told how

// 버그가 발생하면 일일이 응답하지 않고 바로 수정하도록 하자

## Task Management

1. **Plan First**: Write plan to `tasks/todo.md` with checkable items
2. **Verify Plan**: Check in before starting implementation
3. **Track Progress**: Mark items complete as you go
4. **Explain Changes**: High-level summary at each step
5. **Document Results**: Add review section to `tasks/todo.md`
6. **Capture Lessons**: Update `tasks/lessons.md` after corrections

1. 계획 우선
2. 계획 검증
3. 진행 사항 추적
4. 변경 사항 설명
5. 결과 문서화
6. 수정 사항을 md 파일에 업데이트

## Core Principles

- **Simplicity First**: Make every change as simple as possible. Impact minimal code.
- **No Laziness**: Find root causes. No temporary fixes. Senior developer standards.
- **Minimat Impact**: Changes should only touch what's necessary. Avoid introducing bugs.
```

**Claude.md 작성**

1. 프로젝트의 코드컨벤션, 아키텍처, 스트럭처를 문서화
2. 항상 참고하고 코드를 생성할 수 있는 베스트프랙틱스 코드 컨텍스트를 만들어두자
3. /init 을 통해 CLAUDE.md 파일을 생성하고 위 1, 2번의 내용을 포함시켜서 재구성

위 방식으로도 항상 지침을 따르지 않으므로 자신의 프로젝트에 맞는 custom hook을 하나씩 생성해야 합니다.

### TIP

---

- `CLAUDE.md`는 팀 협업을 위한 파일이므로 기본적으로 Git에 커밋하여 팀원 간 공유하는 것이 권장됩니다.
- Claude가 잘못된 결과를 생성한 경우, 같은 실수를 반복하지 않도록 `CLAUDE.md`에 해당 instruction을 기록해 두는 것이 좋습니다.
- 반복적으로 수행하는 작업은 커맨드 형태로 저장하여, 같은 프롬프트를 매번 다시 입력하지 않도록 하는 것이 좋습니다.
    
    ex ) `add → commit → push`처럼 자주 반복되는 Git 작업 흐름은 하나의 명령으로 묶어 재사용하자
    

- Subagent 전략
    
    복잡한 작업을 하나의 AI에게 모두 맡기면 컨텍스트가 혼잡해지고 집중력이 떨어질 수 있으므로 역할을 나누어 Subagent를 반복적으로 사용하는 방식이 좋습니다.
    
    ![image.png](attachment:18fe7c13-6fa8-4659-bbed-3e744dd0ffc4:image.png)
    
    - `code-arch` → 코드 구조 정리, 리팩토링, 아키텍처 점검
    - `build-vali` → 빌드 확인, 테스트 검증, 실행 검토
    
    이 방식의 핵심은 AI가 하나의 작업에 집중하도록 역할을 분리해 과도한 역할 부담을 줄이는 것입니다.
    

- Verification Before Done
    
    Claude Code의 결과를 신뢰하려면 “완료” 전에 반드시 검증이 있어야합니다.
    
    작업 완료 후 다른 Subagent( 백그라운드 )로 결과를 검증하도록 하자 ( 혼자 끝내지 말고, 다른 AI로 검사 )
    
    작업 끝나는 순간 자동 실행되는 Stop Hook을 사용하여 자동 검증되도록 하자
    
- 권한 자동화 옵션
    
    장시간 작업에서는 중간중간 권한 확인이 작업 흐름을 끊을 수 있으므로, sandbox 환경에서는 다음과 같은 옵션을 사용해 승인 프롬프트를 줄일 수 있습니다.
    
    작업 중간 권한을 물어보는 권한 옵션을 자동화하여 멈추지 않고 계속 진행하도록 하자
    
    - --permission-mode=dontAsk
    - --dangerously-skip-permissions
    
    핵심 목적은 중간 승인 대기로 멈추지 않고 자동 흐름을 유지하는 것입니다.
    

- important 혹은 you must로 강조하면 규칙 준수율이 높아집니다.

- 훅( Hook )과 자동화
    
    린터나 포매터 같은 반복 검증은 claude.md에 지시사항으로 넣기보다, 훅으로 자동 실행되게 만드는 편이 좋습니다.
    
    > 훅 : 특정 이벤트가 발생했을 때 자동으로 실행되는 작업
    > 
    - 작업 종료 시 → Stop Hook으로 검증 실행
    - 커밋 전 → pre-commit 훅으로 린트 실행
    - push 후 → CI에서 테스트 실행
    
    즉, 기억에 의존하지 말고 시스템으로 강제하자는 뜻
    

- 자동 검증과 피드백 루프
    
    Claude Code가 자신의 작업을 스스로 검증할 수 있는 도구를 갖추면, 자체적인 피드백 루프가 형성되어 결과 품질이 크게 향상될 수 있습니다.
    
    검증 방식은 도메인별로 다르므로, 각 프로젝트에 맞는 검증 방법을 설계해 제공하는 것이 중요합니다.
    

- 실무적으로 추천하는 CLAUDE.md 구성
    
    [ 포함시킬 것 ]
    
    - 프로젝트 한 줄 소개
    - 기술 스택
    - 핵심 디렉터리 구조
    - 주요 아키텍처 원칙
    - 반드시 알아야 할 도메인 규칙
    - 빌드/테스트/실행 문서 위치
    - 관련 문서 목록
    
    [ 포함시키지 말 것 ] 
    
    - 과도한 스타일 규칙
    - 일반적인 코딩 상식
    - 현재 작업과 무관한 세부 절차
    - 긴 코드 스니펫
    - 자동 생성된 설명을 검토 없이 복붙한 내용
