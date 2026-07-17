# SMALL / small.weecl.kr — 프로젝트 시작 문서

## 프로젝트 정체성

- 외부명: **SMALL**
- 내부명: **S-MALL**
- 도메인: https://small.weecl.kr
- 저장소: `fitmora/s-mall`
- 역할: WEECL 생태계 안의 멤버 전용 구매 채널 / 폐쇄몰 진입점

---

## 저장소 경계

- 기존 `witee.co.kr` / `fitmora/groupbuy-form`은 목마교·썬데이서울 주문폼 운영을 위해 당분간 유지하며, 장기적으로 프론트를 `s-mall`로 통합할 예정입니다.
- 기존 공유 링크(회원들이 이미 사용 중인 주문폼 URL) 보호가 최우선입니다.
- SMALL 작업에서 `groupbuy-form` 프론트를 직접 수정하지 않습니다 (n8n 백업 JSON 등 명시적으로 승인된 예외는 있었음).
- `weecl-kr` / WEECL Checkout v1.3.4.1은 수정하지 않습니다.

---

## 현재 배포 상태

- GitHub Pages 배포 완료
- Route 53 `small.weecl.kr` CNAME 설정 완료
- HTTPS 정상 작동 확인
- Channel Talk 적용 완료
- 카카오 상담 제거 완료
- SMALL 랜딩 / 목마교 인증 / 주문 제출 / WEECL SELECT 이동 정상 확인

---

## 현재 커밋 상태

### s-mall 주요 커밋

- `9039c6088e511b61def59b460c85641fe789817d` — Initial SMALL MVP with WEECL Channel Talk
- `c7ba5bf8953916f72ee03229d87c4b1bd7cd59e7` — Add vendor campaign metadata to SMALL orders

### groupbuy-form 관련 n8n 백업 커밋

- `009ac65` — Internal Processor vendor/campaign fields 반영
- rebase 후 fast-forward push 완료
- force push 없음
- merge commit 없음

---

## 화면 구조

```text
public_landing
  - 목마교 공동구매 카드
  - WEECL SELECT 카드
auth_gate
  - 목마교 회원 인증
main_app
  - 기존 주문폼 기능
  - SMALL 메인 복귀 버튼
```

---

## 데이터 기준

- 소속 = 목마교 / 썬데이서울 등 크루 구분
- 벤더 = 영산
- 캠페인 = 내부 운영/회차/분기 기준
- 채널 컬럼은 현재 사용하지 않음
- 온유어마크와 영산은 별도 컬럼으로 분리하지 않고, 벤더는 영산으로 통일

---

## Google Sheet 기준

파일명:

```text
WEECL SMALL Operations
```

탭명 유지:

```text
member_list
order_list
discount_rules
manual_products
WEECL_CRM
notices
```

`order_list` 추가 컬럼:

```text
벤더
캠페인
```

---

## n8n 기준

SMALL·기존 witee 공유 n8n 기준 백업:

```text
s-mall/_docs/n8n-backup/
```

- 운영 Workflow, webhook, Google Sheet는 SMALL과 기존 witee가 계속 공유
- JSON 복사는 Workflow 분리나 복제가 아니며, 백업 JSON의 관리 소유권만 `s-mall`로 이전
- 2026-07 이후 공유 n8n JSON의 유일한 편집·import 기준은 위 경로
- `groupbuy-form/_docs/n8n-backup/`의 두 기준 JSON은 전환 이전 원본이자 이후 동결된 레거시 스냅샷
- 운영 n8n 반영은 효빠가 전체 Workflow JSON import 방식으로 수행
- JSON은 n8n에 import하기 전까지 운영에 영향을 주지 않음

`Internal Processor` 수정 내용:

- `Normalize Submit Payload`에서 vendor/campaign 보존
- `Build Rows (per item)`에서 벤더/캠페인 기록
- 기존 witee 주문은 벤더=영산 fallback, 캠페인=빈칸
- `Append Order Rows` 컬럼 스키마 새로고침 필요
- n8n 반영 방식은 기존 기준대로 전체 Workflow JSON import 방식

---

## 다음 작업

- 신규 크루 입점 구조 검토
- 영산 외 벤더가 추가될 때 벤더별 주문 분기 설계
- WEECL SELECT 카드 콘텐츠 및 연결 경로 고도화
