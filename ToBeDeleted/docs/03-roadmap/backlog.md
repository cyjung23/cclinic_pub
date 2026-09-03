# 잔여 작업 목록 (Backlog)

> 최종 갱신: 2026-04-11

| # | 과제 | 우선순위 | 상태 |
|---|------|---------|------|
| 1 | GA4 Key Event 설정 | 최우선 | 미착수 |
| 2 | Paid Search 랜딩페이지 최적화 (322세션/주, 70% 이탈) | 높음 | 미착수 |
| 3 | 네이버 검색 유입 강화 (블로그, SEO, 스마트플레이스) | 높음 | 일부 진행 |
| 4 | 유튜브·Referral 채널 확대 | 중간 | 미착수 |
| 5 | 네이버 스마트플레이스 소개글 특수문자 수정 후 등록 | 중간 | 보류 |
| 8 | 영문 가격표 이미지 (price_en.webp) 영문화 | 중간 | 미착수 |
| 9 | 영문-한글 콘텐츠 동기화 체크리스트 수립 | 낮음 | 미착수 |
| 10 | 소프트주사 계열 홈페이지 구축 (시술 런칭 시) | 대기 | 미착수 |

## 과제 1 상세: GA4 Key Event

| 전환 행동 | 이벤트명 | 트리거 |
|----------|---------|--------|
| 네이버예약 클릭 | click_naver_booking | URL contains booking.naver |
| 예약 클릭 | click_reservation | 자체 예약 버튼 |
| 이메일 상담 | click_email_consult | URL contains mailto: |
| 전화 (대표) | click_call (02) | URL contains tel:02-838-3380 |
| 전화 (상담) | click_call (010) | URL contains tel:010-9832-3380 |

선행 확인: GTM 설치 여부, 버튼 HTML 구조, 광고 대행사 설정 가능 여부.

## 과제 5 상세: 스마트플레이스

허용 특수문자: - _ ( ) : & ! [ ] , . % + ~ @ * ^ ' / ? 등. 수정: 삼각형→>, 가운뎃점→쉼표

## 과제 9 상세: 동기화 대상

en/data/services/ (8개 JSON), en/data/reviews/ (6개 JSON), en/data/media/articles.json, en/data/services-index.json, en/js/ (4개 JS), en/js/service-panel.js serviceIdMap.
