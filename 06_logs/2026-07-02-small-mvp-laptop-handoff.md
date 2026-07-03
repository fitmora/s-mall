# SMALL MVP — 랩탑 작업 인계 로그 (2026-07-02)

## 완료한 작업

- `fitmora/s-mall` 저장소 생성 및 push
- GitHub Pages 배포
- Route 53 `small.weecl.kr` CNAME 설정
- HTTPS 정상 확인
- Channel Talk pluginKey 적용
- 카카오 상담 제거
- 목마교 공동구매 카드 전체 클릭 구조
- WEECL SELECT 카드 이동
- SMALL 메인 복귀 (`showSmallLandingFromApp`)
- `ORDER_VENDOR` / `ORDER_CAMPAIGN` 추가
- n8n `Internal Processor` vendor/campaign 백업 JSON 수정
- Codex 검증 통과
- 실제 주문 테스트 통과

---

## 확정 커밋

### s-mall

- `9039c6088e511b61def59b460c85641fe789817d`
- `c7ba5bf8953916f72ee03229d87c4b1bd7cd59e7`

### groupbuy-form

- `009ac65`

---

## 현재 운영 기대값

### small.weecl.kr 주문

```text
소속 = 목마교
벤더 = 영산
캠페인 = 2026-07 온유어마크 공동구매
```

### 기존 witee.co.kr 주문

```text
소속 = 목마교 또는 썬데이서울
벤더 = 영산
캠페인 = 빈칸
```

---

## 주의사항

- `s-mall`과 `groupbuy-form`은 아직 저장소 분리 유지
- `s-mall`을 `weecl-kr` 안으로 편입하지 않음
- `weecl-kr/00_context` 문서 체계와 `s-mall/00_context` 문서 체계는 통일
- n8n 백업은 장기적으로 `s-mall/_docs/n8n-backup`으로 복사 검토
- `groupbuy-form/_docs`는 기존 witee 레거시 보존용

---

## 오피스에서 이어 할 일

- s-mall repo pull
- groupbuy-form repo pull
- small.weecl.kr 주문 테스트 재확인
- `order_list` 벤더/캠페인 기록 확인
- 필요 시 `s-mall/_docs/n8n-backup` 복사 작업 진행
