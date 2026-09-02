# **CC표준2: CC 작업이력·의사결정 (v3.0 / 2026-05-12)**

**기준일:** 2026-05-12  
 **이전 버전:** v2.0 (2026-04-11, 영문 사이트 구축 완료, JSON·JS 영문화, Genspark CDN 잔여 4건 제거)  
 **변경 사유:** 카카오톡 오픈채팅 상담채널 추가(데스크탑·모바일), GA4 kakao\_click 이벤트 추가, 소프트주사 계열 관련 의사결정 삭제(당분간 미진행)  
 **참조 문서:** CC표준1(마스터문서), CC표준3(잔여작업·로드맵)

---

## **1\. 완료 작업 이력**

### **2026-03-01 \~ 03-03: 홈페이지 리뉴얼 및 마케팅 보고서**

홈페이지 전면 리뉴얼 완료. 8개 시술 페이지 독립 구축, 메인 슬로건 “당신의 라인을 예술로 조각하다” 적용. 마케팅팀 종합보고서 작성(시술 체계, 블로그 현황, 트래픽 분석 포함).

### **2026-03-14: SEO 강화 및 AI 크롤러 대응**

llms.txt(52줄), llms-full.txt(442줄), 8개 시술별 Markdown 파일([index.html.md](http://index.html.md/)) 추가. sitemap.xml에 22개 URL 등록(커밋 21de856). 웹사이트 제작 최종보고서 작성.

### **2026-03-17: robots.txt 업데이트**

21개 AI 크롤러(GPTBot, ClaudeBot, PerplexityBot 등)에 Allow: / 명시 설정. 레거시 Cafe24 경로 8개 Disallow 유지.

### **2026-04-10: 개발환경 전환 (Genspark → Codespaces)**

Genspark AI Builder 폐기, GitHub Codespaces \+ VS Code \+ Live Server 환경으로 전환. cclinic, cclinicfile 두 저장소 모두에 .devcontainer/devcontainer.json 추가. 월 $24.99\~$249 비용 절감.

### **2026-04-10: og-image.jpg 로컬 교체**

index.html 메타태그(line 33)와 JSON-LD(line 119)의 og:image를 Genspark CDN → [https://cclinic.kr/images/og-image.jpg](https://cclinic.kr/images/og-image.jpg) (27,714 B, JPEG, 720×712 px)로 교체(커밋 30e392b). Git LFS hook 오류 해결(.git/hooks/pre-push, post-commit 삭제).

### **2026-04-10: 리포지토리 마이그레이션**

[file.cclinic.kr](http://file.cclinic.kr/) 먼저 테스트: GitHub 리포명 cclinic-file → cclinicfile 변경 시도. Cloudflare Pages가 GitHub 리다이렉트를 통해 자동 연동됨을 확인(커밋 782990e 배포 성공). 단, Cloudflare 프로젝트명과 pages.dev URL은 자동 변경 불가임을 확인.

[file.cclinic.kr](http://file.cclinic.kr/) 무중단 전환: 리포명을 cclinic-file로 원복 → 새 리포 cclinicfile 생성 → 파일 복사 업로드 → Cloudflare Pages에 신규 프로젝트 cclinicfile 생성·연동 → cclinicfile.pages.dev 정상 확인 → 기존 cclinic-file 프로젝트에서 [file.cclinic.kr](http://file.cclinic.kr/) 도메인 제거 → 신규 cclinicfile 프로젝트에 [file.cclinic.kr](http://file.cclinic.kr/) 도메인 추가 → Active 확인 → 기존 Cloudflare 프로젝트 cclinic-file 삭제.

[cclinic.kr](http://cclinic.kr/) 전환: DNS가 Cloudflare Pages(CNAME → cclinic-github.pages.dev)임을 확인(GitHub Pages가 아님). 새 리포 cclinic 생성 → 기존 cclinic-github에서 파일 복사 업로드 → .devcontainer/devcontainer.json 생성(name: “cclinic”) → [README.md](http://readme.md/) 수정 → Cloudflare Pages에 신규 프로젝트 cclinic 생성·연동 → cclinic.pages.dev 정상 확인 → DNS CNAME을 cclinic-github.pages.dev → cclinic.pages.dev로 변경([cclinic.kr](http://cclinic.kr/), [www.cclinic.kr](http://www.cclinic.kr/) 모두) → Custom domains Active 확인.

결과:

| 항목 | 변경 전 | 변경 후 |
| ----- | ----- | ----- |
| 메인 GitHub 리포 | cyjung23/cclinic-github | cyjung23/cclinic |
| 메인 Cloudflare 프로젝트 | cclinic-github | cclinic |
| 메인 pages.dev | cclinic-github.pages.dev | cclinic.pages.dev |
| 파일 GitHub 리포 | cyjung23/cclinic-file | cyjung23/cclinicfile |
| 파일 Cloudflare 프로젝트 | cclinic-file | cclinicfile |
| 파일 pages.dev | cclinic-file.pages.dev | cclinicfile.pages.dev |
| DNS [cclinic.kr](http://cclinic.kr/) CNAME | cclinic-github.pages.dev | cclinic.pages.dev |
| DNS [file.cclinic.kr](http://file.cclinic.kr/) CNAME | cclinic-file.pages.dev | cclinicfile.pages.dev |

### **2026-04-10: Genspark CDN 이미지 제거 (1차 — 19건)**

Genspark CDN 이미지 로컬 이전 작업을 진행하려 했으나, 소스 파일 확인 결과 이미 모든 이미지가 로컬로 교체된 상태였음을 확인. HTML 파일 전체에서 grep \-r “sspark” \--include=“\*.html” 결과 0건. 이전에 업로드된 변환 이미지 19개(profile.jpg, procedure.jpg 등)는 기존 로컬 이미지(dr\_1.jpg, cases/fat\_graft\_01.jpg 등)와 중복이므로 삭제(커밋 b5dfc2b). 브라우저 개발자도구 Network 탭에서 sspark 요청 0건 최종 확인.

### **2026-04-10: 기존 프로젝트 정리**

Cloudflare Pages 프로젝트 cclinic-github 삭제. GitHub 리포지토리 cyjung23/cclinic-github 삭제. Cloudflare 캐시 Purge Everything 실행. Cloudflare Pages 재배포 트리거(커밋 9daadef).

### **2026-04-10: 문서 체계 수립**

기존 단일 마스터 보고서를 3개 표준문서로 분리. CC표준1(마스터문서), CC표준2(작업이력·의사결정), CC표준3(잔여작업·로드맵).

### **2026-04-11: 영문 사이트 구축 ([cclinic.kr/en/](http://cclinic.kr/en/))**

모바일 페이지(m/)를 기반으로 en/ 폴더에 영문 원페이지 사이트를 구축했습니다. 시술 상세 링크 없이 원페이지 내에서 완결되는 구조입니다.

**Step 1 — 폴더 구조 생성:** m/ 폴더를 en/으로 복사하여 기본 구조를 생성했습니다.

**Step 2 — en/index.html 영문 전환:** HTML lang 속성, meta 태그(title, description, keywords), OG 태그(og:title, og:description, og:locale=“en\_US”), JSON-LD(alternateName), 히어로 섹션, 서비스 카드 8종, 네비게이션, 푸터, 버튼 텍스트, ARIA 속성 등을 sed 스크립트로 일괄 영문 전환했습니다. 가격표 이미지를 price\_en.webp로 변경했습니다.

**Step 3 — hreflang 태그 삽입:** index.html, m/index.html, en/index.html 모두에 `<link rel="alternate" hreflang="ko">`, `<link rel="alternate" hreflang="en">`, `<link rel="alternate" hreflang="x-default">` 태그를 삽입했습니다.

**Step 4 — sitemap.xml 및 llms.txt 업데이트:** sitemap.xml에 `https://cclinic.kr/en/` 엔트리(priority 0.8, monthly) 추가. llms.txt에 영문 사이트 항목 추가.

### **2026-04-11: 서비스 상세 JSON 영문 전환 (16개 파일)**

en/data/ 폴더 내 전체 JSON 파일을 한글에서 영어로 전환했습니다.

**서비스 상세 (8개):** fatgraft.json, adhesion.json, eyelid.json, faceline.json, vline.json, powerline.json, cellulite.json, striae.json — 각 파일의 title, intro, howItWorks(3단계), benefits, faq(Q\&A), targetAreas, treatmentInfo, cases(caption), improvementScale 등 전체 필드를 영문으로 교체했습니다.

**서비스 인덱스 (1개):** services-index.json — 6개 서비스의 title, titlePlain, desc, badge를 영문으로 교체했습니다.

**리뷰 (6개):** fatgraft.json, adhesion.json, eyelid.json, faceline.json, vline.json, powerline.json — 각 파일의 category, title, quote, author, part, tags를 영문으로 교체했습니다.

**미디어 (1개):** articles.json — sectionTitle, 7건 기사의 title, excerpt, doctorQuote, reporter를 영문으로 교체했습니다.

전환 후 `grep -rPn '[\x{AC00}-\x{D7A3}]' en/data/` 결과 **0건** 확인.

### **2026-04-11: JSON 키 불일치 수정 (process → howItWorks)**

영문 JSON 작성 시 `process` 키를 사용했으나, service-panel.js가 `data.howItWorks`를 참조하여 사이드 패널이 열리지 않는 오류가 발생했습니다. 8개 서비스 JSON 파일 모두에서 `"process"` → `"howItWorks"`로 키 이름을 변경하여 해결했습니다(커밋 18ce644). 원인 분석 과정에서 브라우저 Console 에러(`Cannot read properties of undefined (reading 'map')`, service-panel.js:105)와 JS 코드의 `data.howItWorks.map()` 호출을 확인하여 키 불일치를 특정했습니다.

### **2026-04-11: JS UI 텍스트 영문 전환 (4개 파일)**

en/js/ 폴더의 4개 JS 파일에 하드코딩된 한글 UI 텍스트를 영문으로 전환했습니다(커밋 7100ccc).

**review-panel.js:** “스와이프하여 더 많은 후기 보기” → “Swipe to see more reviews”, “상담·문의하기” → “Book a Consultation”, “후기 카페에서 더 보기” → “See more reviews on Café”

**media-panel.js:** “참의원 정창영 원장” → “Dr. Jung Chang-young, Charm Clinic”, “원문 기사 보기” → “Read Original Article”, 한글 주석 12건 → 영문 주석

**app.js:** “전송 중…” → “Sending…”, “전송 완료\!” → “Sent successfully\!”, “전송 실패” → “Send failed”, alert 메시지 2건 영문 전환, iframe title, trackEvent 라벨 등 한글 주석·문자열 전체 영문 전환

**service-panel.js:** “실제 사례” → “Actual Cases”

### **2026-04-11: 영문 thank-you 페이지 생성 및 폼 리다이렉트 수정**

en/index.html의 상담 폼 전송 후 `https://cclinic.kr/thank-you/`(한글)로 리다이렉트되는 문제를 발견했습니다. en/thank-you/index.html을 영문으로 신규 생성(lang=“en”, 영문 제목·본문·버튼, Return to Home → [cclinic.kr/en/](http://cclinic.kr/en/))하고, en/index.html 863번 줄의 인라인 JS에서 리다이렉트 경로를 `https://cclinic.kr/en/thank-you/`로 수정했습니다(커밋 0d60736).

### **2026-04-11: Genspark CDN 잔여 4건 제거 (2차 — 최종)**

1차 제거(4/10) 시 HTML 파일만 검사하여 0건으로 확인했으나, 영문 사이트 구축 과정에서 `m/data/services/` JSON 파일에 Genspark CDN URL 4건이 잔존하고 있음을 발견했습니다. `m/data/services/cellulite.json`에 2건(cellulite\_01, cellulite\_02), `m/data/services/striae.json`에 2건(striae\_01, striae\_02)이 있었습니다. 사례 이미지 4장(cellulite\_01.jpg, cellulite\_02.jpg, striae\_01.jpg, striae\_02.jpg)을 images/cases/에 추가하고, JSON의 Genspark URL을 로컬 경로로 교체했습니다(커밋 e0696bd). `grep -rn 'sspark\|genspark' m/data/ en/data/ ./data/` 결과 **0건** 최종 확인. 프로젝트 전체에서 Genspark CDN 의존성이 완전히 제거되었습니다.

### **2026-04-13 \~ 04-15: 문서 관리 체계 진화**

Google Docs 표준문서 4개(CC표준1\~3 \+ 온보딩) 생성 완료. 이후 공개 레포지토리(pubrepo/cclinic-docs/)를 거쳐 cclinic 전용 공개 레포(cclinic\_pub/docs/)로 최종 이전. 팀 구성 확정: 기획1팀(총괄 기획·개발), 기획2팀(콘텐츠·번역), 마케팅1팀(전략), 마케팅2팀(실행).

### **2026-05-12: 카카오톡 오픈채팅 상담채널 추가**

데스크탑(index.html)과 모바일(m/index.html)의 상담 섹션(\#consultation)에 카카오톡 오픈채팅 1:1 링크를 추가했습니다. 전화, 문자 아래에 카카오톡 버튼이 배치되어 클릭 시 “참의원 상담” 오픈채팅방([https://open.kakao.com/o/szrVRzui](https://open.kakao.com/o/szrVRzui))으로 연결됩니다.

작업 과정에서 최초 오픈채팅방 링크([open.kakao.com/me/idcharm23](http://open.kakao.com/me/idcharm23))가 존재하지 않는 링크여서 “존재하지 않는 오픈채팅방입니다” 오류가 발생했고, 즉시 복원한 뒤 올바른 오픈채팅 1:1 방을 생성하여 재적용했습니다. 복원 과정에서 `</div>` 태그 1개가 함께 삭제되어 전화/문자와 업무시간의 좌우 레이아웃이 깨지는 문제가 발생했으나, 누락된 태그를 추가하여 정상 복원했습니다.

영문 사이트(/en/)에는 카카오톡을 추가하지 않습니다.

### **2026-05-12: GA4 kakao\_click 이벤트 추가**

데스크탑과 모바일 카카오톡 링크 모두에 `onclick="trackEvent('kakao_click','카카오톡 상담')"` GA4 이벤트를 추가하여 클릭 추적이 가능하도록 했습니다.

---

## **2\. 의사결정 로그**

| 일자 | 결정 사항 | 근거 | 결과 |
| ----- | ----- | ----- | ----- |
| 2026-03-01 | 정적 HTML/CSS/JS로 사이트 구축 | 22개 URL, 8개 시술 페이지의 소규모 사이트. 프레임워크 불필요 | 유지 중. 50-100페이지 초과 시 재검토 |
| 2026-03-14 | llms.txt 및 Markdown 시술문서 제공 | AI 검색엔진(ChatGPT, Claude, Perplexity) 대응 | sitemap.xml에 등록 완료 |
| 2026-03-17 | 21개 AI 크롤러 Allow 설정 | AI 검색 노출 극대화 | robots.txt 반영 완료 |
| 2026-04-10 | Genspark Builder 폐기 → Codespaces 전환 | 월 $24.99\~$249 비용 절감, GitHub 직접 제어 가능 | 전환 완료 |
| 2026-04-10 | 리포명에서 하이픈 제거 (cclinic-github → cclinic) | 관리 편의성, 프로젝트명 통일 | 마이그레이션 완료 |
| 2026-04-10 | file.cclinic.kr로 먼저 테스트 후 [cclinic.kr](http://cclinic.kr/) 전환 | file.cclinic.kr이 단순·중요도 낮아 테스트에 적합 | 무중단 전환 성공 |
| 2026-04-10 | Cloudflare 프로젝트 삭제·재생성 방식 채택 | Cloudflare Pages 프로젝트명은 변경 불가. 삭제 후 재생성이 유일한 방법 | 프로젝트명 통일 완료 |
| 2026-04-10 | 이미지 호스팅 옵션 A(로컬 /images/) 선택 | 총 용량 1MB 미만. 같은 도메인 서빙이 SEO·성능 모두 유리 | 이미 적용된 상태 확인 |
| 2026-04-10 | 미사용 이미지 19개 삭제 | 기존 로컬 이미지와 중복. 리포 용량 최소화 | 삭제 완료(커밋 b5dfc2b) |
| 2026-04-10 | 문서 체계 3분할 | SCP의 6개 문서는 과다. [cclinic.kr](http://cclinic.kr/) 규모에 맞게 3개로 축소 | 본 문서 체계 |
| 2026-04-11 | 영문 사이트를 m/(모바일) 기반 원페이지로 구축 | 모바일 페이지가 원페이지 구조로 영문 사이트에 적합. 시술 상세 페이지 별도 링크 불필요 | en/ 폴더 구축 완료 |
| 2026-04-11 | 가격표 이미지를 price\_en.webp로 분리 | 한글 가격표와 영문 가격표를 독립적으로 관리. price\_en.webp는 추후 영문 변경 예정 | file.cclinic.kr에 배치 |
| 2026-04-11 | WhatsApp 미추가, 010 문자상담만 유지 | 외국인 환자 접점으로 WhatsApp을 검토했으나, 현 단계에서는 기존 010 문자상담으로 충분 | en/index.html에 010 번호만 표기 |
| 2026-04-11 | 서비스 JSON 키를 JS 기대값에 맞춤 (process → howItWorks) | service-panel.js가 data.howItWorks를 참조. 원본 m/ JSON의 키가 howItWorks임을 확인 | 8개 JSON 수정 완료 |
| 2026-04-11 | Genspark CDN 잔여 제거 범위를 JSON까지 확대 | 1차(4/10)에서 HTML만 검사하여 누락. JSON에서 동적 로드되는 이미지까지 포함해야 완전 제거 | 4건 제거 완료, 전체 0건 확인 |
| 2026-04-11 | 문서를 Markdown 파일로 세분화, docs/ 폴더 구조(docs/01-site, 02-history, 03-roadmap 등) 생성 | 각 100\~300줄 단위로 분할하여 세밀한 편집 가능 | 19개 MD 파일 생성 |
| 2026-04-13 | Google Docs 표준문서 재통합 | MD 파일 19개는 Google Drive 커넥터에서 개별 관리 어려움. 3개 표준 \+ 온보딩 \= 4개 문서로 재통합 | Google Docs 생성 완료 |
| 2026-04-15 | cclinic\_pub 전용 공개 레포로 문서 이전 | pubrepo 공유 시 프로젝트 간 충돌 가능성. cclinic 전용 레포로 독립 관리 | cclinic\_pub/docs/ 이전 완료 |
| 2026-04-15 | 팀 구성 확정 | 기획1(총괄·개발), 기획2(콘텐츠·번역), 마케팅1(전략), 마케팅2(실행) | infra.md에 팀 테이블 추가 |
| 2026-05-12 | 카카오톡 상담채널 방식: 오픈채팅 1:1 | 플러스친구(채널) 미사용 상태. 웹사이트 링크로 누구나 접속 가능한 방식은 오픈채팅이 유일 | 데스크탑·모바일 적용 완료 |
| 2026-05-12 | 영문 사이트에 카카오톡 미추가 | 카카오톡은 한국 서비스. 영문 사이트 타겟(외국인)에게 카카오톡은 부적합 | en/ 미변경 |
| 2026-05-12 | 소프트주사 계열 당분간 미진행 | 원장님 결정. 시술 런칭 시기 미정 | CC표준1\~3에서 소프트주사 관련 내용 전체 삭제 |

---

## **3\. 진행 중·보류 작업**

| 상태 | 작업 | 비고 |
| ----- | ----- | ----- |
| 완료 | 영문 사이트 구축 ([cclinic.kr/en/](http://cclinic.kr/en/)) | 2026-04-11 전체 완료 |
| 완료 | Genspark CDN 완전 제거 | 2026-04-10\~11 총 23건 제거, 잔존 0건 |
| 완료 | 카카오톡 오픈채팅 상담채널 추가 | 2026-05-12 데스크탑·모바일 완료 |
| 완료 | GA4 kakao\_click 이벤트 추가 | 2026-05-12 데스크탑·모바일 완료 |
| 보류 | 네이버 스마트플레이스 소개글 등록 | 특수문자 오류(▶→\>, ·→,)만 수정하면 등록 가능 |
| 보류 | sitemap.xml lastmod 갱신 | 2026-05-12 변경 반영 필요 |
| 보류 | 영문 가격표 이미지(price\_en.webp) 영문 변경 | 현재 한글로 되어 있으며 추후 영문 변경 예정 |
| 보류 | llms.txt 영문 사이트 정보 보강 | 현재 엔트리만 추가된 상태, 상세 설명 추가 검토 |

상세 내용은 CC표준3(잔여작업·로드맵) 참조.

---

**CC표준2 끝**

---

