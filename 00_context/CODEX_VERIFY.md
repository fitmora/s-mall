# Codex 검증 기준 — SMALL / s-mall

## 기본 원칙

- Codex는 **read-only 검증 전용**입니다.
- 파일 수정 금지
- commit/push 금지
- n8n / Google Sheet / DNS / GitHub Pages 수정 금지

Codex는 항상 결과를 "통과 / 조건부 통과 / 실패"로 보고하고, 문제 발견 시 위치·내용·위험성·수정 제안만 제시합니다. 직접 고치지 않습니다.

---

## 검증 대상별 체크리스트

### 1. s-mall `index.html`

- `currentCrew`가 `'목마교'`인지
- `SESSION_KEY`가 `'small_mokmagyo_session'`인지
- webhook URL(`AUTH_URL`/`VALIDATE_URL`/`SUBMIT_URL`/`NOTICE_URL`/`MANUAL_PRODUCTS_URL`) 변경 여부
- `ADMIN_EMAIL` 변경 여부
- `buildPayload`/`validateRequired`/`doValidate`/`submitFinal`/`renderOrderCard` 로직 변경 여부
- Channel Talk(`ChannelIO`, `pluginKey`) 변경 여부
- 카드 전체 클릭 구조(`cardGroupbuy`/`cardSelect`) 변경 여부
- `showSmallLandingFromApp()` 변경 여부
- `vendor`/`campaign` 필드 존재 및 값 확인 (`ORDER_VENDOR`/`ORDER_CAMPAIGN`)
- `channel` 필드가 새로 추가되지 않았는지
- `CNAME`/`howto.jpg` 변경 여부

### 2. groupbuy-form n8n 백업 JSON

- 대상: `_docs/n8n-backup/Internal Processor.json`, `Form Gateway.json`
- JSON 문법 유효성
- 변경 파일 범위가 지시된 파일 하나로 국한되는지
- diff가 지시된 노드/필드에만 국한되는지 (예: `Normalize Submit Payload`, `Build Rows (per item)`)
- webhook path / `webhookId` / Google Sheet credential / Spreadsheet ID 변경 여부
- `order_list` 탭명 및 기존 컬럼명 유지 여부
- 목적 외 변경(계좌 문구, 이메일/알림 로직, `WEECL_CRM` 로직 등) 포함 여부 — 포함 시 반드시 별도 보고

### 3. weecl-kr / WEECL Checkout 보호

- `02_plugins/weecl-checkout/` 이하 파일 변경 여부
- WEECL Checkout Router / Shortcode / Point Safety / My Account / Address Book 관련 파일 변경 여부
- `customer-fields.php`, `weecl-checkout.js`, `weecl-checkout.css` 변경 여부
- WooCommerce core, PGAll/PAFW 원본, `mshop-address-ex` 원본, PortOne/iamport 플러그인 원본 변경 여부

---

## 항상 확인할 것 (공통)

- `git remote -v` — 대상 저장소가 지시받은 저장소가 맞는지
- `git status` — 의도한 파일만 변경되었는지, untracked 파일이 실수로 포함되지 않았는지
- `git diff` 범위 — 지시된 최소 범위를 벗어나지 않는지
- webhook URL 변경 여부
- `currentCrew` / `SESSION_KEY` 유지 여부
- Channel Talk 변경 여부
- `vendor`/`campaign` 변경 여부
- `channel` 필드 추가 금지 원칙 준수 여부
- 기존 `groupbuy-form` 프론트(운영 중인 index.html/index-open.html 등) 미수정 확인
- WEECL Checkout 미수정 확인
