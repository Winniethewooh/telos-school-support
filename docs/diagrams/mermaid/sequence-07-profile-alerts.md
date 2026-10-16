# 마이페이지·자막 설정·소리 알림

[Mermaid 코드](sequence-07-profile-alerts.mmd) · [원본](../sequence.pdf#page=7) · [목록](README.md)

보관 이미지의 요소와 관계를 Mermaid로 복원했습니다. 배치는 자동으로 재구성됩니다.

원본의 `setNotificationSettings` 첫 번째 인자는 `크기`로 읽히며 그대로 옮겼습니다. 설정 의미나 인터페이스를 새로 설계하지 않았습니다.

```mermaid
sequenceDiagram
    actor User as 사용자
    participant Page as 마이페이지서비스
    participant Profile as 프로필저장소
    participant Notification as 알림설정저장소
    participant Subtitle as 자막설정저장소
    participant Sound as 사운드시각서비스
    participant Noise as 소음측정센서
    participant Siren as 소리및음성인식센서
    User->>Page: getSharedProfile()
    Page->>Profile: fetchProfile(shared=true)
    Profile-->>Page: 공유 프로필 데이터
    Page-->>User: 공유 프로필 표시()
    User->>Page: getPrivateInfo()
    Page->>Profile: fetchProfile(shared=false)
    Profile-->>Page: 비공개 정보
    Page-->>User: 비공개 정보 표시()
    User->>Page: setNotificationSettings(크기, 진동)
    Page->>Notification: 저장
    Notification-->>Page: 저장 완료
    User->>Page: setSubtitleSettings(크기, 색상)
    Page->>Subtitle: 저장
    Subtitle-->>Page: 저장 완료
    Sound->>Noise: measureNoiseLevel()
    alt 소음 레벨이 임계치를 넘는 경우
        Note over Page: 소음 과다, 이동 권고
    end
    Sound->>Siren: listenForSirenOrBroadcast()
    alt 사이렌 또는 긴급 방송 감지
        Siren-->>User: 문자 알림 (긴급 상황 발생)
    end
```
