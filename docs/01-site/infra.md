# 인프라 및 개발 환경

> 최종 갱신: 2026-04-11

## 호스팅

| 항목 | cclinic.kr | file.cclinic.kr |
|------|-----------|-----------------|
| 호스팅 | Cloudflare Pages (무료) | Cloudflare Pages (무료) |
| 저장소 | github.com/cyjung23/cclinic (private) | github.com/cyjung23/cclinicfile (private) |
| CF 프로젝트명 | cclinic | cclinicfile |
| pages.dev | cclinic.pages.dev | cclinicfile.pages.dev |
| SSL | Cloudflare 자동 | Cloudflare 자동 |
| 캐시 | Cloudflare 기본 | max-age=300 (5분) |
| CORS | 해당 없음 | Access-Control-Allow-Origin: * |
| DNS CNAME | cclinic.pages.dev | cclinicfile.pages.dev |

## 개발 환경 — GitHub Codespaces

두 저장소 모두 Codespaces + VS Code + Live Server(포트 5500). Genspark AI Builder는 2026-04-10 폐기.

## 작업 워크플로우

**cclinic.kr**: Codespace 열기 → Live Server 미리보기 → 파일 수정 → 브라우저 확인 → git add/commit/push → Cloudflare Pages 자동 배포. 광고 운영 중이므로 dev 브랜치 테스트 후 main 병합 권장.

**file.cclinic.kr**: Codespace에서 images/price.webp 교체 → Live Server 미리보기 → 커밋 → 푸시 → 자동 배포(1~2분) → 전 채널 자동 업데이트.

## file.cclinic.kr 가격표 CDN

| 파일 | 용도 |
|------|------|
| images/price.webp | 가격표 — 한글 (128,660 B) |
| images/price_en.webp | 가격표 — 영문 (추후 변경 예정) |
| index.html | 안내 페이지 (noindex, nofollow) |
| 404.html | 3초 후 cclinic.kr로 리다이렉트 |
| _headers | CORS *, cache max-age=300, nosniff |

## 비용 구조

| 항목 | 월 비용 |
|------|---------|
| Cloudflare Pages ×2 | $0 |
| GitHub Codespaces | $0 (월 120 core-hours 무료) |
| Anthropic API | ~$1 미만 |
| Genspark Builder | $0 (해지, 이전 $24.99~$249) |
| 합계 | ~$1 미만 |
