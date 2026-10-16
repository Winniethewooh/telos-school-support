# 건청 학생 학교생활 흐름

[Mermaid 코드](sequence-08-hearing-student.mmd) · [원본](../sequence.pdf#page=8) · [목록](README.md)

보관 이미지의 요소와 관계를 Mermaid로 복원했습니다. 배치는 자동으로 재구성됩니다.

원본의 메시지 번호와 화살표를 유지했습니다. `7.1` 랭킹 생성은 원본에서 학생→서비스 화살표로 표시되어 있습니다.

```mermaid
sequenceDiagram
    actor Student as 건청학생
    participant Service as 서비스
    participant AI as AI
    par 마이페이지
        Student->>Service: 1a. 마이페이지 열람
    and 정보 확인
        Student->>Service: 1b. 난청학생의 특성 및 보조기구에 대한 정보 확인
    and 공지 확인
        Service->>Student: 2. 학교 및 학급 공지 알림
        Student->>Service: 3. 학교 및 학급 공지 확인
    and 교과 학습
        par 학습 자료
            Student->>Service: 4a. 학습 자료 이용
        and 모둠활동
            Student->>Service: 4b. 모둠활동 시 자신의 역할 분배 확인
            Student->>Service: 5. 난청 학생의 대화 이해에 대한 피드백 확인
        end
    and 미션 빙고
        Student->>Service: 1c. 학생 간 대화 빈도 수집
        Service->>AI: 6. 학생 대화 빈도에 대한 정보 제공
        AI-->>Service: 6.1. 미션 빙고 제공
        Student->>Service: 7. 미션 빙고 수행
        Student->>Service: 7.1. 미션 빙고 수행 결과에 따른 랭킹 생성
        Student->>Service: 8. 랭킹 확인
    and 학급 학생의 기분 제시
        Student->>Service: 1d. 오늘의 기분 선택
        Service->>Service: 1d.1. 학급 학생들의 기분 수합
        Service-->>Student: 1d.2. 반 전체 학생의 기분 시각적으로 제시
    end
```
