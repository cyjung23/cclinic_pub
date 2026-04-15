# CC 프로젝트 문서 (cclinic.kr)

> 이 폴더는 참의원(Charm Clinic) 웹사이트 프로젝트의 운영 문서를 관리합니다.  
> AI 어시스턴트가 필요한 파일만 선택적으로 읽고 수정하여 토큰 효율을 극대화합니다.

## 문서 구조

| 경로 | 설명 | 기존 문서 |
|------|------|-----------|
| `01-site/overview.md` | 병원 개요, URL 목록, 기술스택 | CC표준1 §1-1, 1-2, 2-1 |
| `01-site/pages.md` | 페이지별 URL·설명·priority | CC표준1 §1-3 |
| `01-site/seo.md` | robots.txt, sitemap, JSON-LD, OG, hreflang | CC표준1 §2-5 |
| `01-site/i18n.md` | 영문 사이트 구조, JSON/JS 파일 목록 | CC표준1 §2-2 |
| `01-site/infra.md` | 호스팅, DNS, Codespaces, 비용, 가격표 CDN | CC표준1 §2-1, 2-3, 2-6, 2-8 |
| `01-site/images.md` | 이미지 현황, 경로 목록 | CC표준1 §2-4 |
| `01-site/treatments.md` | 시술 체계 (지방파괴주사 8종 + 소프트주사) | CC표준1 §3, 4 |
| `01-site/blog.md` | 네이버 블로그 현황, 홈판 분석, 작성 콘텐츠 | CC표준1 §5 |
| `01-site/guidelines.md` | 작업 가이드라인, 차별점, 주의사항 | CC표준1 §6 |
| `02-history/2026-03.md` | 2026년 3월 작업이력 | CC표준2 §1 (3월분) |
| `02-history/2026-04.md` | 2026년 4월 작업이력 | CC표준2 §1 (4월분) |
| `02-history/decisions.md` | 주요 의사결정 로그 | CC표준2 §2 |
| `03-roadmap/analytics.md` | GA4, 네이버 애널리틱스, 트래픽 데이터 | CC표준3 §1 |
| `03-roadmap/backlog.md` | 전체 잔여작업 목록 | CC표준3 §2 |
| `03-roadmap/sprint-current.md` | 현재 진행 중인 단기작업 | CC표준3 §3 (단기) |
| `03-roadmap/seo-roadmap.md` | SEO·콘텐츠 전략 로드맵 (중장기) | CC표준3 §3 (중장기) |
| `03-roadmap/completed.md` | 완료된 과제 이력 | CC표준3 §4 |
| `templates/monthly-report.md` | 월간 보고서 템플릿 | 신규 |

## 버전 관리

| 날짜 | 파일 | 변경 내용 |
|------|------|-----------|
| 2026-04-11 | 전체 | 초기 생성 — CC표준1·2·3 (v4.0/v2.0/v2.0) 내용을 Markdown으로 마이그레이션 |
| 2026-04-11 | README.md | heredoc 오류 파일 3건 삭제, 파일 수 19개 확정 |
