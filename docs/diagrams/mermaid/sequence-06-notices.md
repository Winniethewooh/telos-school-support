# 학교·학급·자원센터 공지

[Mermaid 코드](sequence-06-notices.mmd) · [원본](../sequence.pdf#page=6) · [목록](README.md)

보관 이미지의 요소와 관계를 Mermaid로 복원했습니다. 배치는 자동으로 재구성됩니다.

원본에는 시각화 요청을 받는 참여자와 응답을 보내는 참여자가 서로 다르게 그려져 있습니다. 이를 임의로 수정하지 않고 별도 참여자로 유지했습니다. 오른쪽 참여자 명칭은 흐릿하여 원본과 함께 확인해 주세요.

```mermaid
sequenceDiagram
    actor User as 사용자
    participant Notice as 공지서비스
    participant School as 학교API
    participant Calendar as 학급캘린더
    participant Training as 훈련예정서비스
    participant Location as 위치서비스
    participant Center as 센터API
    participant Drill as 훈련예정서비스2차서비스
    User->>Notice: 학교 공지 요청()
    Notice->>School: getSchoolNotices()
    School-->>Notice: 공지 목록 반환()
    Notice-->>User: 공지 목록 표시()
    User->>Notice: 학급 일정 요청()
    Notice->>Calendar: getClassSchedule()
    Calendar-->>Notice: 일정 목록 반환()
    alt 일정 중 대피훈련 포함
        Notice->>Training: getTrainingVisualization()
        Drill-->>Notice: 시각화 자료 반환()
        Notice-->>User: 일정 + 시각화 표시()
    else 대피훈련 미포함
        Notice-->>User: 일정만 표시()
    end
    User->>Notice: 자원센터 공지 요청()
    Notice->>Location: getCurrentLocation()
    Location-->>Notice: [lat, lng]
    opt 반경 1km 이내 센터 있음
        Notice-->>User: 근처 센터 알림
    end
    Notice->>Center: getNearbyCenterNotices(lat, lng)
    Center-->>Notice: 센터 공지 반환()
    Notice-->>User: 센터 공지 표시()
```
