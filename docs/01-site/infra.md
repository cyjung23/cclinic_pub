# 인프라 및 개발 환경

> 최종 갱신: 2026-04-15

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

## 문서 저장소

| 항목 | 내용 |
|------|------|
| 저장소 | github.com/cyjung23/cclinic_pub (public) |
| 문서 경로 | docs/ |
| 읽기 URL 패턴 | https://raw.githubusercontent.com/cyjung23/cclinic_pub/main/docs/{폴더}/{파일명} |
| 쓰기 | cclinic Codespaces에서 /workspaces/cclinic_pub/ clone + PAT 토큰 설정 후 push |

문서 관리 변천: HTML 3개(CC표준1·2·3) → Markdown 19개(cclinic 레포 docs/) → Google Docs 3개 → pubrepo/cclinic-docs/ → cclinic_pub/docs/(현행).

## 팀 구성

| 팀 | 역할 | 담당 영역 |
|---|---|---|
| 원장 (Chase) | 최종 의사결정권자 | 전체 승인, 시술 콘텐츠 감수 |
| 기획1팀 | 총괄 기획·개발 | 코드 수정, 페이지 구조, 배포, 인프라 |
| 기획2팀 | 보조 기획 | 콘텐츠 초안, 번역, 이미지 정리, 리서치 |
| 마케팅1팀 | 마케팅 자문 | 전략 자문, 고도 분석, 마케팅2팀 지원 |
| 마케팅2팀 | 마케팅 실무 | SEO, 블로그, 키워드 리서치, 네이버 플레이스, 트래픽 분석 |

## 개발 환경 — GitHub Codespaces

두 저장소 모두 Codespaces + VS Code + Live Server(포트 5500). Genspark AI Builder는 2026-04-10 폐기. cclinic Codespaces 내에 cclinic_pub도 clone되어 있어 문서 수정·push 가능.

## 작업 워크플로우

**cclinic.kr**: Codespace 열기 → Live Server 미리보기 → 파일 수정 → 브라우저 확인 → git add/commit/push → Cloudflare Pages 자동 배포. 광고 운영 중이므로 dev 브랜치 테스트 후 main 병합 권장.

**file.cclinic.kr**: Codespace에서 images/price.webp 교체 → Live Server 미리보기 → 커밋 → 푸시 → 자동 배포(1~2분) → 전 채널 자동 업데이트.

**문서 업데이트**: cd /workspaces/cclinic_pub → 파일 수정 → git add -A → git commit -m "update: 변경내용" → git push → cd /workspaces/cclinic.

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
