# SMALL·witee 공유 n8n 기준 백업

SMALL과 기존 witee 프론트는 동일한 운영 `Form Gateway`와 `Internal Processor`, webhook, Google Sheet를 공유합니다. 이 디렉터리는 2026-07 이후 그 공유 n8n Workflow JSON의 유일한 편집·import 기준입니다.

## 저장소 역할

- `s-mall/_docs/n8n-backup/`: 2026-07 이후 공유 n8n JSON의 유일한 편집·import 기준
- `groupbuy-form/_docs/n8n-backup/`: 전환 이전 원본이자 이후 동결된 레거시 스냅샷

이번 JSON 복사는 운영 Workflow의 분리나 복제를 의미하지 않습니다. 로컬·GitHub 백업 파일의 관리 소유권만 `s-mall`로 이전하며, `groupbuy-form`의 두 기준 JSON은 이동하거나 삭제하지 않고 전환 시점 상태로 동결합니다. 기존 witee 프론트는 당분간 유지하되 장기적으로 `s-mall`로 통합할 예정입니다.

## 기준 파일

```text
Form Gateway.json
Internal Processor.json
```

최초 기준본은 `groupbuy-form/_docs/n8n-backup/`의 동일 파일에서 복사했으며, 전환 시점에 JSON 문법, SHA-256, byte 단위 일치를 확인합니다.

## 운영 반영

- 이 디렉터리의 JSON은 n8n에 import하기 전까지 운영에 영향을 주지 않습니다.
- 운영 반영은 효빠가 n8n에서 전체 Workflow JSON import 방식으로 수행합니다.
- 동일 webhook path의 기존 Workflow와 새 Workflow를 동시에 Publish하지 않습니다.
- import 후 credential, Spreadsheet ID, webhook path, 컬럼 스키마와 실제 동작을 별도로 확인합니다.

## 변경 원칙

- 공유 Workflow 변경은 이 디렉터리의 JSON만을 기준으로 작업합니다.
- 변경 시 SMALL과 기존 witee 프론트의 회귀를 모두 검토하고 검증합니다.
- `groupbuy-form`의 두 기준 JSON은 전환 시점의 레거시 스냅샷이므로 수정하지 않습니다.
- 운영 n8n, Google Sheets, `groupbuy-form` 프론트, `s-mall/index.html`, `CNAME`, `howto.jpg`, `weecl-kr`는 이 백업 정리 작업의 범위가 아닙니다.
