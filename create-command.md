# .claude/commands/xxx.md 형태로 커스텀 커맨드 생성<br><br>

### 1. 자동 pr 생성 커맨드
---
현재 작업 내용을 분석하여 브랜치 생성 → 커밋 → push → PR 생성까지 수행한다.

**규칙**

- 커밋 규칙: @rules/commit.md 를 반드시 참고하며 따른다


**플로우**

- 1단계: 변경 사항 분석

  - `git diff HEAD`와 `git status`로 변경 내용을 파악한다
  - 변경된 파일 목록, 추가/수정/삭제 내용을 분석한다

- 2단계: 후보 제시 ( 사용자 컨펌 필수 )

분석 결과를 바탕으로 브랜치명 + 커밋 메시지 조합을 2~3개 제안한다.
가장 적합한 1개에 (추천) 표시를 붙인다.

예시 형식
```
1. (추천)
   - 브랜치: docs/update-claude-md-compact-instructions
   - 커밋: docs CLAUDE.md Compact Instructions 섹션 보강

2.
   - 브랜치: chore/claude-md-cleanup
   - 커밋: chore CLAUDE.md 패턴 및 에러 핸들링 섹션 정리

3.
   - 브랜치: docs/add-pattern-error-handling-rules
   - 커밋: docs 패턴과 에러 핸들링 규칙 문서화
```

**반드시 사용자에게 선택을 받은 후 다음 단계로 진행한다.**


- 3단계: 실행

사용자가 선택한 후보로 다음을 순서대로 수행한다:

1. `git checkout -b <브랜치명>` — 새 브랜치 생성
2. `git add .` — 모든 변경 사항 스테이징
3. `git commit -m "<커밋 메시지>"` — 커밋
4. `git push -u origin <브랜치명>` — 푸시
5. `gh pr create --base main` — main 대상 PR 생성

- 4단계: 결과 보고

- 생성된 PR URL을 사용자에게 전달한다


