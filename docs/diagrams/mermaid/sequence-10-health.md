# 보건실 방문·후속조치

[Mermaid 코드](sequence-10-health.mmd) · [원본](../sequence.pdf#page=10) · [목록](README.md)

보관 이미지의 요소와 관계를 Mermaid로 복원했습니다. 배치는 자동으로 재구성됩니다.

원본에서 `14. 처치내용 기입`은 분기 이전에 배치되어 있습니다. 번호 순서나 업무 흐름을 임의로 재배열하지 않았습니다.

```mermaid
sequenceDiagram
    actor Nurse as 보건교사
    participant Student as 학생
    participant Health as 보건시스템 (서비스 외)
    participant Profile as 학생프로필 저장소
    participant Service as 서비스
    Nurse->>Profile: 1. 학생 명렬표 업로드
    Student-->>Nurse: 2. 학생 보건실 출입
    Nurse->>Student: 3. 학생 인적사항 요청
    Student->>Nurse: 4. 인적사항 제공
    Nurse->>Student: 5. 학생 상태 확인
    Nurse->>Profile: 6. 학생 정보 확인
    Nurse->>Service: 7. 학생 부상부위 정도 입력
    Nurse->>Service: 14. 처치내용 기입
    alt 후속조치가 필요한 경우
        Nurse->>Student: 8. 후속조치 안내
        Student->>Student: 9. 후속조치 이행
        Student-->>Nurse: 10. 물품 반납
        Nurse->>Health: 11. 반납 물품 확인
        Nurse->>Profile: 12. 보건일지 저장
    else 후속조치가 불필요한 경우
        Nurse->>Profile: 13. 보건일지 저장
    end
```
