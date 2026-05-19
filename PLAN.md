# 머슬팩토리 경상대점 랜딩페이지 전면 재설계 플랜

## Context

현재 페이지는 다크 블랙 배경 + 공격적인 빨간색(#ef4444) 조합으로,
"하드코어 보디빌딩 헬스장" 분위기를 풍긴다.
그러나 타겟은 **운동이 두려운 초보자** — 이 디자인 톤은 핵심 전환 목표와 정반대다.

목표: 심리적 진입장벽을 제거하는 전환율 중심 랜딩페이지.
한 줄 핵심: "운동 잘해야 오는 곳이 아닙니다."

---

## 파일 정보

- **수정 파일**: `/home/user/cat/index.html` (단일 파일 — HTML/CSS/JS 모두 포함)
- 빌드 도구 없음, 외부 JS 라이브러리 없음
- 폰트: Noto Sans KR (Google Fonts)
- 브랜치: `claude/gym-landing-page-mr9IH`

---

## 1. 디자인 시스템 전환 (가장 중요)

### FROM (현재) → TO (목표)

| 요소 | 현재 | 변경 후 |
|------|------|---------|
| 배경 | `#0c0c0e` 다크 블랙 | `#ffffff` / `#f8f9fa` 화이트 |
| 텍스트 | `#f0eff4` 흰색 | `#1a1a2e` 진한 차콜 |
| 포인트 | `#ef4444` 공격적 레드 | `#FF6B35` 따뜻한 오렌지 |
| 분위기 | 하드코어 보디빌딩 | 친근한 동네 헬스장 |
| 감정 | 긴장/위압 | 안심/환영 |

### 새 CSS 변수 시스템

```css
:root {
  --bg: #ffffff;
  --bg2: #f8f9fa;
  --bg-warm: #fff8f5;       /* 오렌지 틴트 섹션용 */
  --bg-orange: #FF6B35;     /* 메인 포인트 컬러 */
  --bg-orange2: #FF8C5A;
  --surface: #ffffff;
  --surface2: #f3f4f6;
  --border: #e5e7eb;
  --border2: #d1d5db;
  --text: #1a1a2e;          /* 헤딩 */
  --text2: #4a4a6a;         /* 본문 */
  --muted: #9ca3af;
  --accent: #FF6B35;
  --accent2: #FF8C5A;
  --accent-light: rgba(255,107,53,0.08);
  --accent-border: rgba(255,107,53,0.2);
  --green: #16a34a;
  --radius-xl: 24px;
  --radius-lg: 16px;
  --radius-md: 12px;
  --radius-sm: 8px;
}
```

---

## 2. 전체 섹션 구조 (신규 순서)

```
1. [유지] 스티키 내비게이션 — 화이트 배경으로 전환
2. [개선] 히어로 섹션
3. [신규] 트러스트 바 (신뢰 지표 가로 스크롤)
4. [개선] 공감 섹션 (bg2)
5. [개선] 핵심 장점 4개 카드
6. [개선] 시설 소개 (모자이크 그리드)
7. [신규] 실제 회원 후기 3개
8. [개선] 추천 대상 체크리스트
9. [개선] 이용 흐름 STEP (모바일 세로 타임라인)
10. [신규] 머슬팩토리의 약속 (보장 섹션)
11. [개선] FAQ (max-height 수정)
12. [개선] 가격 (가격대 힌트 포함)
13. [유지] 연락 CTA
14. [개선] 마지막 CTA
15. [신규] 모바일 플로팅 하단 CTA 바
16. [유지] 푸터
```

---

## 3. 섹션별 상세 구현

### 3-1. 스티키 내비게이션

변경:
- 배경: `rgba(255,255,255,0.92)` + `backdrop-filter: blur(12px)` + 하단 그림자
- 텍스트: `--text` (진한 차콜)
- CTA 버튼: `--accent` 오렌지

### 3-2. 히어로 섹션

레이아웃: 2컬럼 (텍스트 좌, 이미지 우) → 모바일 1컬럼
배경: 흰색, 상단에 매우 연한 오렌지 radial-gradient 장식

핵심 카피:
```
[배지] 진주 가좌동 · 24시간 · 트레이너 상주

[H1] 운동 처음이어도
      괜찮습니다.

[H2] 기구 몰라도 편하게 시작하세요.
     바로 옆에서 알려드릴게요.

[설명] 경상대 근처, 가좌동 누구나 편하게 시작하는
      24시간 헬스장입니다.
```

우측: 실제 사진 들어갈 이미지 영역 (aspect-ratio: 4/5, rounded-2xl)
CTA: "💬 무료 상담 문의" (오렌지 버튼) + "가격 보기" (아웃라인 버튼)

신뢰 뱃지 하단:
- 🕐 24시간 연중무휴
- 👨‍💼 트레이너 항시 상주
- 🔰 초보자 기구 안내
- 🙅 PT 강매 없음

### 3-3. 트러스트 바 [신규]

가로 스크롤 가능한 바 (overflow-x: auto, 모바일에서 스크롤)
4개 항목:

```
| 🕐 24시간 운영 | 👨‍💼 트레이너 상주 | 💪 기구 무료 안내 | ✋ PT 강매 없음 |
```

배경: `--bg-warm` (연한 오렌지 틴트)
각 항목: 아이콘 + 한줄 텍스트, 구분선

### 3-4. 공감 섹션

3개 카드 (학생/직장인/초보·시니어) — 배경 `--bg2`
각 카드 불안 목록 → 하단에 공감 답변 박스 (오렌지 아웃라인)

공감 답변 카피:
```
머슬팩토리 경상대점은
운동 잘하는 사람만 오는 곳이 아닙니다.

처음 운동하는 분, 기구 사용이 어려운 분,
혼자 시작하기 부담스러운 분들도
편하게 이용할 수 있도록 도와드립니다.
```

### 3-5. 핵심 장점 섹션

2×2 카드 그리드 (모바일: 1열)
카드 스타일: 흰색 배경 + 연한 그림자 + 오렌지 top-border (4px)

각 카드 구조:
- 큰 아이콘 (이모지 or SVG)
- 번호 레이블 (01, 02...)
- 제목
- 따옴표 강조 카피
- 불릿 리스트

카드 4개:
1. ⏰ 24시간 운영 — "내 시간에 운동하세요"
2. 🧑‍🏫 트레이너 상주 — "이 기구 어떻게 써요? 편하게 물어보세요"
3. 🌱 초보자 환영 — "PT 등록 안 해도 기본 안내 가능합니다"
4. 📍 가좌동 접근성 — "경상대 근처, 걸어서 올 수 있어요"

### 3-6. 시설 소개

모자이크 그리드:
```
[전체 전경 — 가로 2칸] [유산소 존]
[웨이트 존]            [스트레칭 존]
[샤워실]               [락커룸]
```

각 셀에 hover overlay: 오렌지 반투명 + 구역명 텍스트
배경: `--bg2`

### 3-7. 회원 후기 [신규]

3개 카드:
```
⭐⭐⭐⭐⭐ | "헬스 처음인데 기구 사용법 하나하나 알려주셔서 너무 좋았어요"
— 김지수 (경상대 3학년)

⭐⭐⭐⭐⭐ | "새벽 6시에도 안전하게 이용할 수 있어서 정말 좋습니다"  
— 박민준 (직장인, 30대)

⭐⭐⭐⭐⭐ | "PT 강요 전혀 없고 트레이너분이 친절하게 설명해주세요"
— 이영희 (주부, 40대)
```

상단에 큰 따옴표 장식, 오렌지 별점, 이름+페르소나
배경: 흰색

### 3-8. 추천 대상

2열 체크리스트 8개 (모바일 1열)
각 아이템: 오렌지 원형 체크마크 + 텍스트
배경: `--bg-warm` (연한 오렌지 틴트)
중앙 정렬, max-width: 700px

### 3-9. 이용 흐름

데스크탑: 가로 5단계 + 연결선
모바일: 세로 타임라인 (중앙 수직선 + 좌우 교대 배치)

```
STEP 1 상담 문의 → STEP 2 시설 안내 → STEP 3 운동 목적 상담 
→ STEP 4 기구 설명 → STEP 5 자유운동 시작
```

5단계 (기존 4단계에서 "운동 목적 상담" 추가)
각 단계: 오렌지 원 번호 + 제목 + 설명

### 3-10. 머슬팩토리의 약속 [신규]

배경: `--bg2`
제목: "저희가 약속드립니다"

약속 4개 (2×2 그리드):
```
🚫 PT 강요 절대 없음     | 🤝 처음도 편하게
기본 안내는 무료          | 언제든 물어보세요
-----------------------+------------------
⏰ 24시간 항상 열려있음  | 🧹 깨끗하고 쾌적한 시설
새벽도, 야간도 OK        | 기구 항상 관리
```

각 약속: 아이콘 + 제목 + 한줄 설명

### 3-11. FAQ

기존 아코디언 유지, 수정:
- `max-height: 200px` → `max-height: 600px`
- 배경: 흰색
- 질문 배지: 오렌지
- 하단에 "더 궁금하신 점이 있으신가요?" + 카카오 문의 버튼

### 3-12. 가격

3개 플랜 카드:
- 각 카드에 "월 X만원대" 가격 힌트 추가 (구체적 숫자는 상담)
- "인기" 뱃지 → 중간 플랜
- 학생 할인 / 친구 추천 이벤트 배너

```
[1개월] 월 7만원대  [3개월 인기] 월 5만원대  [6개월] 월 4만원대
```

하단 강조: "정확한 금액은 방문 상담 시 안내 (숨겨진 비용 없음)"

### 3-13. 마지막 CTA

배경: 오렌지 그라디언트 (`#FF6B35` → `#FF8C5A`)
흰색 텍스트

```
운동 잘해야 오는 곳이 아닙니다.
시작하려는 마음만 있으면 됩니다.

[💬 무료 상담 문의] [📞 전화 문의]
```

### 3-14. 모바일 플로팅 CTA 바 [신규]

```css
.mobile-cta-bar {
  position: fixed;
  bottom: 0; left: 0; right: 0;
  z-index: 999;
  display: none;  /* hidden on desktop */
  background: white;
  border-top: 1px solid var(--border);
  padding: 12px 16px;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 10px;
  box-shadow: 0 -4px 20px rgba(0,0,0,0.08);
}
@media (min-width: 641px) {
  .mobile-cta-bar { display: none; }
}
```

두 버튼:
- 왼쪽: "💬 카카오 문의" (노란색 배경 #FEE500, 진한 갈색 텍스트)
- 오른쪽: "📞 전화 문의" (오렌지 배경, 흰 텍스트)

모바일에서 항상 보임 → 전환율에 가장 직접적 영향

---

## 4. 카피라이팅 전략

### 감정 흐름 설계

```
두려움/불안 인식 → 공감 표현 → 해결 증명 → 신뢰 구축 → 쉬운 첫 걸음
(Hero/공감)       (공감섹션)    (장점/시설)   (후기/약속)   (STEP/CTA)
```

### 핵심 카피 원칙
1. 짧게 → "운동 처음이어도 괜찮습니다" (8자)
2. 구체적 불안 언급 → "PT 강매 없음"을 명시
3. 숫자 활용 → "24시간" "4단계"
4. 허락하는 말투 → "편하게 물어보세요", "부담 없이 시작하세요"
5. 부정문 활용 → "운동 잘해야 오는 곳이 아닙니다"

---

## 5. 기술 구현 상세

### JS 변경 및 추가 사항

#### 5-1. FAQ 토글 — scrollHeight 방식으로 업그레이드 (CSS max-height 제거)
```javascript
function toggleFaq(btn) {
  const item = btn.closest('.faq-item');
  const answer = item.querySelector('.faq-a');
  const inner = item.querySelector('.faq-a-inner');
  const isOpen = item.classList.contains('open');
  // 다른 열린 항목 모두 닫기
  document.querySelectorAll('.faq-item.open').forEach(el => {
    el.classList.remove('open');
    el.querySelector('.faq-a').style.maxHeight = '0';
  });
  if (!isOpen) {
    item.classList.add('open');
    answer.style.maxHeight = inner.scrollHeight + 'px';
  }
}
```
→ CSS에서 `.faq-item.open .faq-a { max-height: 200px; }` 라인은 **삭제**

#### 5-2. 모바일 햄버거 내비게이션
```javascript
const navToggle = document.getElementById('navToggle');
const nav = document.querySelector('nav');
if (navToggle) {
  navToggle.addEventListener('click', () => {
    nav.classList.toggle('nav-open');
  });
  document.getElementById('navLinks').querySelectorAll('a').forEach(link => {
    link.addEventListener('click', () => nav.classList.remove('nav-open'));
  });
}
```

#### 5-3. 모바일 플로팅 CTA — 연락 섹션 진입 시 숨김
```javascript
const contactSection = document.getElementById('contact');
const mobileCta = document.getElementById('mobileCta');
if (contactSection && mobileCta) {
  const cObserver = new IntersectionObserver(entries => {
    mobileCta.style.transform = entries[0].isIntersecting
      ? 'translateY(100%)' : 'translateY(0)';
  }, { threshold: 0.1 });
  cObserver.observe(contactSection);
}
```
→ `.mobile-cta-bar`에 `transition: transform 0.3s ease` 추가 필요

### 유지할 기존 JS/CSS
- IntersectionObserver 코드 (fade-in) — 그대로 재사용
- Noto Sans KR Google Fonts link
- 섹션 ID (nav 앵커 링크 유지: `#empathy`, `#advantages`, `#steps`, `#price`, `#faq`, `#contact`)

### 기술 주의사항
- **모바일 플로팅 바**: `display: none`을 기본으로, `@media (max-width: 768px)`에서 `display: flex` — 순서 중요
- **safe-area-inset**: `padding-bottom: calc(10px + env(safe-area-inset-bottom))` — iPhone 홈 인디케이터 대응
- **body padding**: `@media (max-width: 768px) { body { padding-bottom: 80px; } }` — 플로팅 바가 콘텐츠 가리는 것 방지
- **모바일 햄버거 nav-toggle button**: `background: none; border: none; cursor: pointer;` 리셋 필요

### 반응형 전략
```
모바일 기준 (max-width: 540px):
- 1열 레이아웃
- padding: 16px
- 플로팅 CTA 바 표시

태블릿 (max-width: 860px):
- 2열로 축소
- 단계 세로 타임라인

데스크탑 (min-width: 861px):
- 2~4열 풀 레이아웃
- 가로 단계 흐름
```

---

## 6. 구현 순서 (권장)

1. `:root` CSS 변수 교체 (라이트 테마로 일괄 전환)
2. `rgba(239,68,68,...)` → `rgba(255,107,53,...)` 전체 치환
3. Nav HTML 수정 (햄버거 버튼 추가) + 관련 CSS
4. Hero 2컬럼 분할 레이아웃 + 이미지 영역 + 첫방문 배너
5. 트러스트 바 섹션 추가 (Hero 바로 다음)
6. 공감 섹션 — 답변 박스 강화 (big-quote, 체크 태그)
7. 장점 섹션 — 아이콘 배경 원형, 모바일 1열 브레이크포인트
8. 시설 섹션 — hover overlay 추가
9. 이용 흐름 — 모바일 세로 타임라인 (`.step-content` 래퍼 추가)
10. FAQ — `toggleFaq()` scrollHeight 방식으로 교체, 하단 CTA 프롬프트 추가
11. **[신규] 회원 후기 섹션** 추가 (FAQ 다음)
12. 가격 — 가격대 힌트, 무료상담 배너 추가
13. **[신규] 약속 섹션** 추가 (가격 다음)
14. 마지막 CTA — 배경/카피 업데이트
15. 연락 섹션 — 운영정보 바 추가
16. 푸터 색상 업데이트
17. **[신규] 모바일 플로팅 CTA 바** (body 마지막에 추가)
18. `<script>` 블록에 JS 3개 추가

---

## 7. 전환율 향상 근거

| 개선 요소 | 기대 효과 |
|-----------|-----------|
| 다크→라이트 테마 | 진입 거부감 제거 (타겟층: 일반 주민) |
| 모바일 플로팅 CTA | 모바일 전환 직접 기여 |
| 후기 섹션 추가 | 사회적 증명 (가장 강력한 신뢰 요소) |
| 약속 섹션 추가 | "PT 강매" 불안 직접 해소 |
| 가격 힌트 추가 | 가격 불확실성 → 상담 문의 장벽 감소 |
| 5단계 흐름 | "방문이 어떻게 진행되나" 미지의 공포 제거 |
| 트러스트 바 | 첫 5초 안에 핵심 장점 전달 |

---

## 7. 검증 방법

1. `python3 -m http.server 8080` 또는 `npx serve` 로컬 서버 실행
2. Chrome DevTools → 모바일 에뮬레이션 (iPhone 12 Pro, 390px)으로 확인
3. 체크리스트:
   - [ ] 플로팅 CTA 바 모바일에서 하단 고정 확인
   - [ ] FAQ 아코디언 전체 열림 확인 (max-height 600px)
   - [ ] 모든 섹션 fade-in 애니메이션 동작
   - [ ] 네비게이션 앵커 링크 정상 동작
   - [ ] 데스크탑에서 플로팅 바 숨겨짐 확인
   - [ ] 색상 대비 가독성 확인 (흰 배경 + 차콜 텍스트)
   - [ ] 히어로 2컬럼 → 모바일 1컬럼 전환
   - [ ] 단계 섹션 세로 타임라인 모바일 확인
