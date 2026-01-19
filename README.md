```mermaid
flowchart LR
  A[입력 RGB 카메라 프레임] --> B[프레임 전처리<br/>Resize / Normalize / ROI]
  B --> C[YOLO 객체 검출<br/>Person BoundingBox]
  C --> D[객체 추적(MOT)<br/>TrackID 유지]
  D --> E[접근 영역(Zone) 정의]
  E --> F[Zone 접근 판정<br/>InZone 여부]
  F --> G{상태 변화 발생?}

  G -->|Zone 진입| H[접근 이벤트 발생<br/>Enter Time 기록]
  G -->|Zone 유지| I[체류 시간 누적<br/>Dwell Time 계산]
  G -->|Zone 이탈| J[이탈 이벤트 발생<br/>Exit Time 기록]

  H --> K[출력<br/>PERSON_APPROACH]
  I --> L[출력<br/>IN_ZONE = True<br/>DWELL_TIME]
  J --> M[출력<br/>PERSON_LEAVE<br/>DWELL_TIME 종료]
