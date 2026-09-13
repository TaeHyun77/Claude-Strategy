Claude를 사용하여 개발을 진행할 때의 Flow를 정리했습니다.

기본적으로 Plan 모드에서 요구사항과 기술적 설계를 구체화한 뒤, 구현 계획을 수립하고 Phase별로 구현을 진행합니다.<br><br>

### 개발 진행 Flow

<img width="796" height="198" alt="image" src="https://github.com/user-attachments/assets/1be5a708-86be-4130-96c5-6dc0b57529e6" />


1. AI와 함께 설계 문서 작성

   구현할 기능의 요구사항과 기술적 설계를 AI와 함께 정리합니다.
    
2. `/decompose-design` 실행

   설계 내용을 실제 구현 가능한 작업 단위로 분해합니다.

   작업 간 의존성을 분석하고, 이를 바탕으로 Phase를 구성하고 구현 순서를 결정합니다.
    
3. 구현 계획 검토 및 확정

   분해된 작업, 의존성, Phase 구성을 검토하고 필요한 부분을 수정한 뒤, 사용자 확인을 거쳐 최종 구현 계획을 확정합니다.

   확정된 계획은 설계 문서의 `## 구현 계획`에 저장합니다.
    
4. Jira 이슈 생성

   확정된 구현 계획을 Jira에 등록할지 사용자에게 확인하고, 승인 시 `create-jira-subtasks` 스킬을 실행하여 하나의 주제를 Epic으로, 구현 작업을 Task/Subtask로 생성합니다.

   생성된 각 Jira 이슈에는 해당 Phase와 구현 순서를 반영하고, 이슈 키를 설계 문서의 구현 계획에 역기록합니다.
    
5. Phase 순서에 따라 구현

   Jira에서 작업을 하나씩 확인하며 설계 문서에 정의된 Phase 및 의존성 순서에 따라 구현합니다.

   이때 Jira 상태는 GitHub 작업 흐름과 연동되어 자동으로 변경됩니다.

   - 진행 중: 브랜치 생성
   - 검토 중: PR 생성
   - 완료: PR 병합
   
   따라서, 개발자가 Jira에서 작업 상태를 별도로 변경할 필요가 없습니다.
    
6. PR 리뷰 및 결과 검토

    PR이 병합되면 자동으로 PR 리뷰를 실행하여 구현 결과를 검토합니다.
    
    이를 통해 설계 → 작업 분해 → 구현 → 리뷰까지의 개발 흐름을 연결합니다.

### 설정 사항

[ Jira 상태는 GitHub 작업 흐름과 연동되게 하기 위해서는 깃허브 계정을 연동하고 Jira에서 자동화 작업을 생성해야합니다 ]

<img width="1030" height="469" alt="ㅇㅇㅇ" src="https://github.com/user-attachments/assets/62271b37-a8be-4189-b31d-7f4386d3b0d9" /><br>

[ 목록 관리 ]

<img width="1061" height="568" alt="ㅇㅇㅇㅇ" src="https://github.com/user-attachments/assets/81e6384e-4de8-44da-8b1c-8df760221645" />
