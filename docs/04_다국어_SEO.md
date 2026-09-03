# **CC문서: 다국어(i18n) 구조 및 SEO 구성**

**기준일:** 2026-09-03
**출처:** CC표준1 §2-2, §2-5
**참조:** README.md (문서 인덱스)

---

### **2-2. 다국어(i18n) 구조 (2026-04-11 신규)**

영문 사이트는 모바일 페이지(m/)를 기반으로 en/ 폴더에 구축되었으며, 원페이지 구조로 시술 상세 링크 없이 자체 완결됩니다. 서비스 상세는 JSON 데이터에서 동적 로드되며, 사이드 패널로 표시됩니다.

**폴더 구조:**

en/

├── index.html           (영문 메인 페이지, lang="en")

├── thank-you/

│   └── index.html       (영문 상담완료 페이지)

├── data/

│   ├── services-index.json

│   ├── services/         (8개: fatgraft, adhesion, eyelid, faceline, vline, powerline, cellulite, striae)

│   ├── reviews/          (6개: fatgraft, adhesion, eyelid, faceline, vline, powerline)

│   └── media/

│       └── articles.json

└── js/

    ├── app.js

    ├── service-panel.js

    ├── review-panel.js

    ├── media-panel.js

    └── ga4-events.js

**hreflang 설정:** index.html, m/index.html, en/index.html 모두에 `<link rel="alternate" hreflang="ko">`, `<link rel="alternate" hreflang="en">`, `<link rel="alternate" hreflang="x-default">` 태그가 삽입되어 있습니다.

**영문 번역 범위:** 서비스 카드 9종(결절제거 포함), 서비스 상세 패널(How It Works, Benefits, FAQ), 리뷰 6개 카테고리, 언론보도 7건, UI 텍스트(버튼, 안내문구, 폼 메시지), 메타태그(title, description, OG), JSON-LD, thank-you 페이지 전체가 영문으로 전환되었습니다.

**영문 가격표:** file.cclinic.kr/images/price_en.webp로 연결되어 있으며, 2026-09-03 영문 이미지로 교체·배포 완료되었습니다.

**국제 환자 상담:** 기존 010 문자상담만 유지하며, WhatsApp 링크는 추가하지 않기로 결정했습니다.


### **2-5. SEO 및 AI 크롤러 구성**

robots.txt (2026-03-17 갱신): 모든 주요 AI 봇(GPTBot, ChatGPT-User, OAI-SearchBot, ClaudeBot, Claude-Web, PerplexityBot, Google-Extended, Googlebot, Bingbot, BingPreview, Amazonbot, FacebookBot, meta-externalagent, Bytespider, Applebot, Applebot-Extended, cohere-ai, YouBot)에 Allow: / 설정. 레거시 Cafe24 경로 8개와 /thank-you/ Disallow. Sitemap 2건(sitemap.xml, llms.txt) 선언.

JSON-LD 스키마 (5종): FAQPage(8개 시술 페이지 × FAQ 총 94개), MedicalProcedure(8개), LocalBusiness, Person, WebSite. Schema Validator 검증 시 오류 0건.

OpenGraph 태그: og:image → [https://cclinic.kr/images/og-image.jpg](https://cclinic.kr/images/og-image.jpg), og:type, og:title, og:description 설정 완료. 10개 HTML 파일에 참조. 영문 페이지(en/index.html)에는 og:locale=“en\_US”, og:title=“Charm Clinic Seoul \- Non-Steroidal Adipocytolysis Injection” 별도 설정.

hreflang 태그: index.html, m/index.html, en/index.html에 ko, en, x-default 3개 언어 태그 설정 완료. sitemap.xml에 en/ 엔트리 추가 완료. llms.txt에 영문 사이트 항목 추가 완료.

NAP 일관성: "관악로 164"와 "02-838-3380"이 index.html에 각 4회 등장. 네이버 플레이스, 블로그, 홈페이지 간 주소·전화번호 일치. 영문 페이지에서는 국제 전화번호 형식(+82-2-838-3380)으로 표기.

