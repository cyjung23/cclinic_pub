# cclinic 프로젝트 — 기획팀장 업무인수인계 매뉴얼

> 작성일: 2026-04-13
> 작성자: 전임 기획팀장 (AI 어시스턴트)
> 대상: 신임 기획팀장 (AI 어시스턴트)
> 목적: 채팅 세션 교체 시 업무 공백 없이 프로젝트를 이어받기 위한 완전한 인수인계 문서

---

## 1. 프로젝트 개요

### 1-1. 무엇을 하는 프로젝트인가

cclinic 프로젝트는 서울 관악구에 위치한 참의원(Charm Clinic)의 웹사이트(cclinic.kr)를 운영·개선하는 프로젝트이다. 원장(정창영, 닉네임 Chase, 직업 Doctor)이 직접 기획·지시·검토를 수행하며, 기획팀장(AI 어시스턴트)이 기술 구현 지원, 문서 관리, SEO 전략, 콘텐츠 기획을 담당한다.

### 1-2. 참의원 핵심 정보

참의원은 비스테로이드 지방파괴주사를 이용한 비수술 체형교정 전문 클리닉이다. 40,000건 이상의 시술 경험과 98% 이상의 만족도를 보유하고 있으며, 눈두덩이주사는 특허출원된 고유 시술이다. 지방흡입 후 유착·울퉁불퉁 개선, 지방이식 후 과생착·뭉침 제거도 전문으로 한다.

### 1-3. 원장님과의 커뮤니케이션 원칙

- 전문적인 대화 톤을 사용한다. 캐주얼하거나 과도하게 친근한 톤은 피한다
- 마케팅과 의학적 관점을 모두 중시한다
- 데이터 기반 의사결정을 선호한다 (키워드 검색량, 트래픽 분석 등)
- 작업 지시가 오면 구체적 실행 명령어(sed, git 등)를 즉시 제공한다
- 보고서 업데이트 요청 시 원장님이 직접 파일을 편집하지 않도록, 실행 가능한 명령어를 한 번에 제공한다
- 원장님은 의사이지 개발자가 아니다. 기술 용어는 필요할 때만 간결하게 설명한다

---

## 2. 기술 환경 요약

### 2-1. 두 개의 저장소

cclinic 프로젝트는 두 개의 GitHub 저장소로 구성된다.

첫째, github.com/cyjung23/cclinic (private)은 메인 웹사이트 저장소이다. cclinic.kr, cclinic.kr/m/, cclinic.kr/en/ 세 버전의 사이트가 들어있다. Cloudflare Pages 프로젝트명은 "cclinic"이고, cclinic.pages.dev로 연결되며, 커스텀 도메인은 cclinic.kr과 www.cclinic.kr이다.

둘째, github.com/cyjung23/cclinicfile (private)은 가격표 이미지 전용 CDN 저장소이다. price.webp(한글)와 price_en.webp(영문, 아직 한글 상태) 두 파일만 관리한다. Cloudflare Pages 프로젝트명은 "cclinicfile"이고, file.cclinic.kr로 연결된다.

### 2-2. 기술 스택

순수 정적 HTML/CSS/JS이다. 프레임워크, DB, 서버사이드 렌더링 없음. Cloudflare Pages 무료 호스팅이며, 개발 환경은 GitHub Codespaces + VS Code + Live Server(포트 5500)이다. 배포는 git push만 하면 Cloudflare Pages가 1~2분 내 자동 배포한다.

### 2-3. 사이트 구조

데스크탑 버전(cclinic.kr/)은 메인 페이지 + 8개 시술 독립 페이지 + 리뷰 + 미디어 페이지로 구성된다. 모바일 버전(cclinic.kr/m/)은 원페이지 구조이며 서비스 상세를 사이드 패널로 표시한다. 영문 버전(cclinic.kr/en/)은 모바일 기반 원페이지로, JSON 데이터에서 서비스 상세를 동적 로드한다. sitemap.xml에 24개 URL이 등록되어 있다.

### 2-4. 광고 운영 주의사항

cclinic.kr은 Google Ads 유료 광고가 운영 중이다. 코드 수정 시 반드시 dev 브랜치에서 테스트 후 main에 병합해야 한다. main에 직접 push하여 사이트가 깨지면 광고비가 낭비된다.

---

## 3. 프로젝트 문서 체계 (가장 중요)

### 3-1. 문서의 위치와 목적

모든 프로젝트 문서는 cclinic 저장소의 docs/ 폴더에 Markdown 파일로 관리된다. 이 체계는 2026-04-11에 기존 HTML 보고서 3개(CC표준1·2·3)를 19개 Markdown 파일로 세분화하여 전환한 것이다. 목적은 AI 어시스턴트가 필요한 파일만 선택적으로 읽고 수정하여 토큰 효율을 극대화하는 것이다.

### 3-2. 파일 목록과 각 파일의 역할

docs/README.md — 전체 문서 목차와 버전 관리표이다. 작업 시작 시 이 파일을 가장 먼저 읽어서 어떤 파일을 추가로 읽어야 하는지 판단한다.

docs/01-site/overview.md — 병원 기본 정보(이름, 원장, 연락처, 주소, 업무시간), 온라인 채널 URL 목록, 기술 스택 요약이 들어있다. 병원 정보가 변경되면 이 파일을 수정한다.

docs/01-site/pages.md — sitemap.xml에 등록된 전체 페이지 목록이다. URL, 시술명, lastmod, priority가 기록되어 있다. 새 페이지가 추가되거나 sitemap이 변경되면 이 파일을 수정한다.

docs/01-site/seo.md — robots.txt 설정, JSON-LD 스키마(5종), OpenGraph 태그, hreflang 태그, NAP 일관성 정보가 들어있다. SEO 관련 작업 시 참조한다.

docs/01-site/i18n.md — 영문 사이트(en/) 폴더 구조, 번역 범위, JS가 참조하는 JSON 키 목록, 가격표 상태, 국제 환자 상담 방침이 기록되어 있다. 영문 사이트 작업 시 반드시 이 파일을 먼저 읽는다. 특히 JSON 키가 howItWorks(process가 아님)임에 주의한다.

docs/01-site/infra.md — 두 저장소의 호스팅 정보(Cloudflare 프로젝트명, pages.dev URL, DNS CNAME 등), 개발 환경 설정, 작업 워크플로우, file.cclinic.kr 가격표 CDN 구조, 월간 비용이 기록되어 있다.

docs/01-site/images.md — 전체 이미지 현황이다. 어떤 이미지가 로컬이고 어떤 것이 외부 CDN인지, Genspark CDN 제거 상태(0건 확인), /images/cases/ 파일 16개 목록이 들어있다.

docs/01-site/treatments.md — 참의원의 전체 시술 체계이다. 지방파괴주사 8종의 목적·부위·특징과 소프트주사 계열 4종(+예비 1종)의 개발 배경·적용 분야·네이밍·대칭 구조가 기록되어 있다. 블로그 콘텐츠 작성이나 홈페이지 시술 설명 작업 시 반드시 참조한다.

docs/01-site/blog.md — 네이버 블로그 게시글 목록(날짜, 제목, logNo), 네이버 홈판 분석, 작성 완료된 콘텐츠(광대살·땅콩형 얼굴, 뒷구리살) 정보가 들어있다. 블로그 콘텐츠 기획 시 참조한다.

docs/01-site/guidelines.md — 원장님의 작업 스타일, 지방파괴주사와 소프트주사의 핵심 차별점(모든 콘텐츠에 일관 적용해야 함), 기술적 주의사항, 영문 사이트 유지보수 규칙이 기록되어 있다. 모든 작업 전에 이 파일을 숙지해야 한다.

docs/02-history/2026-03.md — 2026년 3월 작업이력이다. 홈페이지 리뉴얼, SEO 강화, robots.txt 업데이트 기록이 들어있다.

docs/02-history/2026-04.md — 2026년 4월 작업이력이다. Codespaces 전환, 리포지토리 마이그레이션, Genspark CDN 제거(1차 19건 + 2차 4건), 영문 사이트 구축, JSON·JS 영문화, sitemap·robots.txt 갱신, 검색엔진 등록 기록과 주요 커밋 해시 목록이 들어있다.

docs/02-history/decisions.md — 프로젝트 전체의 주요 의사결정 로그이다. 날짜, 결정 사항, 근거, 결과가 표로 기록되어 있다. 새로운 의사결정이 내려지면 이 파일에 행을 추가한다.

docs/03-roadmap/analytics.md — 웹 트래픽 현황 데이터이다. 네이버 애널리틱스 3개 기간 비교, GA4 채널별 세션·참여율·체류시간, Google Ads 캠페인별 세션, 채널별 질적 순위가 기록되어 있다. GA4 ID는 G-1VDP80PB70이다.

docs/03-roadmap/backlog.md — 전체 잔여 작업 목록이다. 과제번호, 우선순위, 상태가 표로 정리되어 있고, GA4 Key Event, 스마트플레이스, 콘텐츠 동기화 등의 상세 내용이 포함되어 있다.

docs/03-roadmap/sprint-current.md — 현재 진행 중인 단기(1~2주) 작업 목록이다. 완료/미착수 상태가 표시되어 있다. 작업이 완료되면 이 파일에서 상태를 업데이트하고, 완료된 항목은 completed.md로 이동한다.

docs/03-roadmap/seo-roadmap.md — 중기(1~2개월)와 장기(3개월+) SEO·콘텐츠 전략이 기록되어 있다.

docs/03-roadmap/completed.md — 완료된 과제의 전체 이력이다. 과제명, 완료일, 비고가 표로 기록되어 있다.

docs/templates/monthly-report.md — 월간 보고서 작성 시 사용하는 템플릿이다.

### 3-3. 문서 운영 규칙

작업 시작 시 docs/README.md를 가장 먼저 읽는다. 여기서 어떤 파일을 추가로 읽어야 하는지 판단한다. 예를 들어 SEO 작업이면 seo.md를, 영문 사이트 작업이면 i18n.md를 읽는다.

변경이 발생하면 해당 파일만 수정한다. 전체 파일을 다시 쓰지 않는다.

docs/README.md 하단의 버전 관리표에 날짜, 파일명, 변경 내용을 한 줄 추가한다.

월이 바뀌면 docs/02-history/에 새 파일(예: 2026-05.md)을 생성한다. 이전 월 파일은 그대로 보존한다.

sprint-current.md에서 완료된 항목은 completed.md로 이동하고 새 작업을 추가한다.

원장님이 "보고서 업데이트해 줘"라고 요청하면, 해당 파일을 crawler로 읽고 → 변경 내용을 파악하고 → sed 명령어 또는 VS Code에 붙여넣을 내용을 한 번에 제공한다. 원장님이 직접 파일을 찾아서 편집하게 하지 않는다.

---

## 4. 현재 프로젝트 상태 (2026-04-13 기준)

### 4-1. 최근 완료된 작업

2026-04-10에 Genspark AI Builder에서 GitHub Codespaces로 개발환경을 전환했다. 두 저장소 모두 리포명을 정리하고(하이픈 제거), Cloudflare Pages 프로젝트를 재생성했다. Genspark CDN 이미지 23건(1차 19건 + 2차 4건)을 모두 로컬로 교체하여 외부 의존성을 완전 제거했다.

2026-04-11에 영문 사이트(cclinic.kr/en/)를 구축했다. 모바일 페이지(m/)를 기반으로 원페이지 구조로 만들었으며, JSON 16개 파일과 JS 4개 파일을 영문으로 전환했다. hreflang 태그 삽입, sitemap·robots.txt·llms.txt 업데이트, Google Search Console·네이버 서치어드바이저 등록까지 완료했다. 같은 날 문서 체계를 HTML 3개에서 Markdown 19개로 세분화 전환했다.

2026-04-13에 Google Search Console에서 "리디렉션이 포함된 페이지" 99건 알림이 왔으나, 이는 레거시 Cafe24 URL의 301 리다이렉트와 http→https 리다이렉트가 정상 작동하는 것으로 조치 불필요하다.

### 4-2. 현재 미착수 작업 (sprint-current.md 참조)

네이버 스마트플레이스 소개글의 특수문자(▶→>, ·→,) 수정 후 재등록, GA4 Key Event 선행 조사(GTM 설치 여부, 버튼 HTML 구조 확인), 영문 가격표 이미지(price_en.webp) 영문 디자인 준비가 남아있다.

### 4-3. 중장기 과제 (backlog.md, seo-roadmap.md 참조)

GA4 Key Event 5개 설정(최우선), Paid Search 랜딩페이지 최적화, 네이버 검색 유입 강화, 유튜브·Referral 채널 확대, 영문↔한글 콘텐츠 동기화 체계 수립, 소프트주사 계열 홈페이지 구축이 백로그에 있다.

---

## 5. 자주 사용하는 작업 패턴

### 5-1. 코드 수정 후 배포

원장님이 Codespaces 터미널에서 실행할 명령어를 제공한다. 기본 패턴은 다음과 같다.

파일 수정 → git add -A → git commit -m "커밋 메시지" → git push

push 후 1~2분이면 Cloudflare Pages에 자동 배포된다. 배포 후 브라우저에서 Ctrl+Shift+R(하드 리프레시)로 확인한다.

### 5-2. 문서 업데이트

원장님이 "보고서 업데이트해 줘"라고 하면, crawler 도구로 해당 docs/ 파일을 읽고, 변경할 내용을 포함한 sed 명령어를 제공하거나 "VS Code에서 이 파일을 열고 이 내용을 붙여넣으세요"라고 안내한다.

### 5-3. 영문 사이트 수정

한글 사이트(m/) 콘텐츠가 변경되면 영문(en/) JSON·JS도 동기화해야 한다. i18n.md를 먼저 읽고, 변경 대상 파일을 특정한 후 수정 내용을 제공한다. JS가 참조하는 키는 howItWorks이지 process가 아님에 반드시 주의한다.

### 5-4. 블로그 콘텐츠 기획

원장님이 블로그 글 작성을 요청하면, treatments.md에서 시술 정보를 확인하고, blog.md에서 기존 게시글과 중복이 없는지 확인하고, guidelines.md의 핵심 차별점(비스테로이드, 영구적 효과, 타이트닝 동시)을 반드시 포함한다. 키워드 리서치 → 제목에 키워드 배치 → 경쟁 콘텐츠 대비 차별화 구조를 따른다.

### 5-5. 검색엔진 관련 작업

sitemap.xml, robots.txt 변경 시 seo.md와 pages.md를 업데이트한다. Google Search Console(search.google.com/search-console)과 네이버 서치어드바이저(searchadvisor.naver.com)에서 재제출 또는 수집 요청한다. Google Search Console의 "리디렉션이 포함된 페이지" 알림은 레거시 301 리다이렉트로 조치 불필요하다.

---

## 6. 알려진 이슈 및 주의사항

### 6-1. _redirects 파일

루트에 _redirects 파일이 있으며, 레거시 Cafe24 URL 7개 경로를 현재 URL로 301 리다이렉트한다. 정적 리다이렉트와 와일드카드 동적 리다이렉트가 모두 설정되어 있다. Google Search Console에서 리디렉션 관련 알림이 올 수 있으나 정상이다.

### 6-2. Genspark CDN 완전 제거 확인

2026-04-11 기준 프로젝트 전체에서 Genspark CDN 참조가 0건이다. 새로운 외부 이미지를 추가할 때는 반드시 로컬(/images/)에 저장한다. 유일한 외부 참조는 file.cclinic.kr(가격표)뿐이다.

### 6-3. heredoc 사용 금지

Codespaces 터미널에서 heredoc(<< 'EOF')으로 Markdown 파일을 생성하면 코드 블록이나 특수문자에서 오류가 발생한다. 파일 생성·수정은 반드시 "code 파일명" 명령으로 VS Code에서 직접 편집하도록 안내한다.

### 6-4. 영문 사이트 JSON 키

service-panel.js가 data.howItWorks를 참조한다. JSON 파일에 "process" 키를 사용하면 사이드 패널이 열리지 않는 오류가 발생한다. 이 이슈는 2026-04-11에 해결했지만, 새 JSON을 만들 때 같은 실수를 반복하지 않도록 주의한다.

### 6-5. 네이버 블로그 제한

logNo=224069427392 게시글이 네이버 신고 기반 제한 상태이다. 콘텐츠 작성 시 네이버 가이드라인을 준수한다.

---

## 7. 관련 외부 서비스 계정

- Google Search Console: cclinic.kr 속성 등록됨
- Google Analytics 4: G-1VDP80PB70
- 네이버 서치어드바이저: cclinic.kr 등록됨
- Cloudflare: cclinic, cclinicfile 두 프로젝트
- GitHub: cyjung23/cclinic, cyjung23/cclinicfile (모두 private)
- 네이버 블로그: blog.naver.com/idcharm23
- 네이버 카페: cafe.naver.com/cclinic
- 유튜브: youtube.com/@charmclinicseoul
- 네이버 플레이스: m.place.naver.com/place/70976119
- 네이버 예약: booking.naver.com/booking/13/bizes/837910
- 폼 전송: formspree.io/f/xvzbpler

---

## 8. 첫 작업 시 체크리스트

신임 기획팀장이 첫 작업을 시작할 때 다음 순서를 따른다.

1. 이 문서(onboarding.md)를 끝까지 읽는다
2. docs/README.md를 읽어서 전체 문서 구조를 파악한다
3. docs/03-roadmap/sprint-current.md를 읽어서 현재 진행 중인 작업을 확인한다
4. docs/01-site/guidelines.md를 읽어서 작업 원칙을 숙지한다
5. 원장님의 지시에 따라 해당 작업에 필요한 파일만 추가로 읽고 작업을 시작한다

---

## 9. 문서 읽기 방법

docs/ 폴더의 파일은 GitHub private 레포에 있으므로, crawler 도구로 직접 접근할 수 없다. 다음 두 가지 방법으로 읽는다.

방법 A: 원장님이 레포를 임시로 public으로 변경하면 crawler로 https://raw.githubusercontent.com/cyjung23/cclinic/main/docs/파일경로 를 읽는다. 읽기가 끝나면 다시 private으로 변경 요청한다.

방법 B: 원장님에게 "docs/파일명의 내용을 공유해 주세요" 또는 "cat docs/파일명 결과를 붙여넣어 주세요"라고 요청한다.

---

이 문서와 docs/ 폴더의 19개 Markdown 파일이 cclinic 프로젝트의 전체 지식 베이스이다. 이 문서들을 기반으로 업무 공백 없이 프로젝트를 이어갈 수 있다.
