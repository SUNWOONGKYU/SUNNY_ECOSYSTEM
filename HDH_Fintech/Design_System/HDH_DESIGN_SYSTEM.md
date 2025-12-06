# HDH Fintech Design System

> **전문적이고 신뢰감 있는 금융 거래 플랫폼을 위한 디자인 시스템**
>
> **최종 업데이트:** 2025-12-06
> **버전:** 1.0
> **테마:** Professional Trading (전문 트레이딩)

---

## 목차

1. [디자인 원칙](#디자인-원칙)
2. [색상 체계 (Color Palette)](#색상-체계-color-palette)
3. [타이포그래피 (Typography)](#타이포그래피-typography)
4. [간격 체계 (Spacing)](#간격-체계-spacing)
5. [레이아웃 (Layout)](#레이아웃-layout)
6. [컴포넌트 (Components)](#컴포넌트-components)
7. [애니메이션 & 효과 (Effects)](#애니메이션--효과-effects)
8. [접근성 (Accessibility)](#접근성-accessibility)
9. [반응형 디자인 (Responsive)](#반응형-디자인-responsive)
10. [디자인 토큰 (Design Tokens)](#디자인-토큰-design-tokens)

---

## 디자인 원칙

### 핵심 가치

**1. 신뢰성 (Trust)**
- 금융 거래 플랫폼으로서 신뢰감과 안정성 전달
- 전문적이고 깔끔한 인터페이스

**2. 명확성 (Clarity)**
- 복잡한 거래 프로세스를 단순하고 명확하게 표현
- 사용자가 현재 단계를 즉시 파악 가능

**3. 실시간성 (Real-time)**
- 거래 상태, 수익, 알람을 즉각적으로 표시
- 동적인 데이터 시각화

**4. 안전성 (Safety)**
- 주의사항, 경고 메시지를 명확하게 전달
- 오류 방지를 위한 시각적 피드백

**5. 효율성 (Efficiency)**
- 최소 클릭으로 거래 실행
- 자주 사용하는 기능에 빠른 접근

---

## 색상 체계 (Color Palette)

### 브랜드 컬러 (Brand Colors)

#### Primary - Golden Gradient (황금빛 그라데이션)
```css
/* 주요 용도: 브랜드 아이덴티티, 수익 강조, 프리미엄 느낌 */
--primary: #F59E0B;          /* 메인 골드 (Amber 500) */
--primary-dark: #D97706;     /* 어두운 골드 (Amber 600) */
--primary-light: #FCD34D;    /* 밝은 골드 (Amber 300) */
--primary-gradient: linear-gradient(135deg, #F59E0B 0%, #D97706 100%);
--primary-alpha-10: rgba(245, 158, 11, 0.1);
--primary-alpha-20: rgba(245, 158, 11, 0.2);
```

**사용 예시:**
- 헤더 그라데이션
- 수익 금액 강조
- 중요 CTA 버튼
- 성공 알림 배경

**색상 이론:**
- 골드는 부, 성공, 프리미엄을 상징
- 금융 서비스에 신뢰감 부여

#### Secondary - Trading Green (트레이딩 그린)
```css
/* 전용 용도: 수익/상승/포지티브 상태 */
--secondary: #10B981;        /* 메인 그린 (Emerald 500) */
--secondary-dark: #059669;   /* 어두운 그린 (Emerald 600) */
--secondary-light: #34D399;  /* 밝은 그린 (Emerald 400) */
--secondary-alpha-10: rgba(16, 185, 129, 0.1);
```

**사용 예시:**
- 수익 금액 (+167,000원)
- 상승/매수 버튼
- 거래 성공 상태
- 목표 달성 표시

#### Tertiary - Trading Red (트레이딩 레드)
```css
/* 전용 용도: 손실/하락/네거티브 상태 */
--tertiary: #EF4444;         /* 메인 레드 (Red 500) */
--tertiary-dark: #DC2626;    /* 어두운 레드 (Red 600) */
--tertiary-light: #F87171;   /* 밝은 레드 (Red 400) */
--tertiary-alpha-10: rgba(239, 68, 68, 0.1);
```

**사용 예시:**
- 손실 금액 표시
- 하락/매도 버튼
- 위험 경고
- SL(손절) 설정

### 상태 색상 (Status Colors)

#### Active/In-Progress (활성/진행 중)
```css
--active: #3B82F6;           /* 블루 (Blue 500) */
--active-bg: #DBEAFE;        /* 블루 배경 (Blue 100) */
--active-text: #1E3A8A;      /* 블루 텍스트 (Blue 900) */
```

**사용 예시:**
- 현재 진행 중인 거래 단계
- 활성화된 프로세스
- 선택된 시간대

#### Waiting/Pending (대기)
```css
--waiting: #64748B;          /* 슬레이트 (Slate 500) */
--waiting-bg: #F1F5F9;       /* 슬레이트 배경 (Slate 100) */
--waiting-text: #0F172A;     /* 슬레이트 텍스트 (Slate 900) */
```

**사용 예시:**
- 아직 시작하지 않은 단계
- 비활성 시간대
- 대기 중 상태

#### Warning (주의)
```css
--warning: #F59E0B;          /* Primary와 동일 */
--warning-bg: #FEF3C7;       /* 앰버 배경 (Amber 100) */
--warning-text: #92400E;     /* 앰버 텍스트 (Amber 900) */
--warning-border: #FCD34D;   /* 앰버 테두리 (Amber 300) */
```

**사용 예시:**
- 주의사항 알림
- 중요 공지
- 확인 필요 항목

### 기본 색상 (Base Colors)

#### Background (배경)
```css
--bg-main: #F8FAFC;          /* 메인 배경 (Slate 50) */
--bg-white: #FFFFFF;         /* 화이트 배경 (카드, 패널) */
--bg-dark: #0F172A;          /* 다크 배경 (Slate 900) */
--bg-overlay: rgba(0, 0, 0, 0.6);  /* 모달 오버레이 */
```

#### Text (텍스트)
```css
--text-primary: #0F172A;     /* 주요 텍스트 (Slate 900) */
--text-secondary: #64748B;   /* 보조 텍스트 (Slate 500) */
--text-tertiary: #94A3B8;    /* 3차 텍스트 (Slate 400) */
--text-inverse: #FFFFFF;     /* 역전 텍스트 */
```

#### Border (테두리)
```css
--border-color: #E2E8F0;     /* 기본 테두리 (Slate 200) */
--border-light: #F1F5F9;     /* 밝은 테두리 (Slate 100) */
--border-dark: #CBD5E1;      /* 어두운 테두리 (Slate 300) */
```

### 색상 조합 가이드

#### ✅ 권장 조합
```css
/* 수익 표시 */
color: var(--secondary);       /* Green */
font-weight: 600;

/* 손실 표시 */
color: var(--tertiary);        /* Red */
font-weight: 600;

/* 골드 강조 */
background: var(--primary-gradient);
color: white;

/* 진행 중 단계 */
background: var(--active-bg);
border-left: 4px solid var(--active);
```

#### ❌ 피해야 할 조합
```css
/* 명암비 부족 */
background: var(--bg-light);
color: var(--text-tertiary);  /* 너무 밝음 */

/* 색상 충돌 */
background: var(--secondary);  /* Green */
color: var(--tertiary);        /* Red - 충돌 */
```

---

## 타이포그래피 (Typography)

### 폰트 패밀리 (Font Family)

#### 기본 폰트 스택
```css
--font-family-base: 'Malgun Gothic', '맑은 고딕', 'Pretendard', 'Noto Sans KR', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
--font-family-heading: 'Malgun Gothic', '맑은 고딕', 'Segoe UI', 'Arial', sans-serif;
--font-family-mono: 'Consolas', 'Monaco', 'Courier New', monospace;
--font-family-number: 'SF Pro Display', 'Roboto', 'Malgun Gothic', monospace;
```

**폰트 선택 이유:**
- **Malgun Gothic (맑은 고딕)**: 한글 가독성 우수, Windows 기본
- **Pretendard**: 모던하고 깔끔한 느낌
- **Consolas/Monaco**: 숫자/금액 표시에 최적
- **SF Pro Display**: 금융 데이터 표시에 전문적

### 폰트 크기 (Font Size)

```css
/* Display - 큰 제목 */
--font-size-display: 28px;
--line-height-display: 1.2;

/* Heading 1 - 페이지 제목 */
--font-size-h1: 24px;
--line-height-h1: 1.3;

/* Heading 2 - 섹션 제목 */
--font-size-h2: 18px;
--line-height-h2: 1.4;

/* Heading 3 - 카드 제목 */
--font-size-h3: 16px;
--line-height-h3: 1.5;

/* Heading 4 - 작은 제목 */
--font-size-h4: 14px;
--line-height-h4: 1.5;

/* Body - 본문 */
--font-size-base: 14px;
--line-height-base: 1.6;

/* Small - 보조 텍스트 */
--font-size-sm: 13px;
--line-height-sm: 1.5;

/* Extra Small - 캡션 */
--font-size-xs: 12px;
--line-height-xs: 1.4;

/* Tiny - 배지 */
--font-size-2xs: 11px;
--line-height-2xs: 1.4;

/* Numbers - 금액 표시 */
--font-size-number-large: 32px;   /* 큰 금액 (누적 수익) */
--font-size-number-medium: 18px;  /* 중간 금액 (일일 수익) */
--font-size-number-small: 14px;   /* 작은 금액 (목록) */
```

### 폰트 굵기 (Font Weight)

```css
--font-weight-regular: 400;      /* 일반 텍스트 */
--font-weight-medium: 500;       /* 중간 강조 */
--font-weight-semibold: 600;     /* 강조 텍스트, 금액 */
--font-weight-bold: 700;         /* 굵은 텍스트 */
--font-weight-extrabold: 800;    /* 매우 굵은 텍스트 */
```

#### 금액/숫자 표시 전용 스타일
```css
.amount {
    font-family: var(--font-family-number);
    font-weight: var(--font-weight-semibold);
    letter-spacing: -0.5px;
}

.amount-large {
    font-size: var(--font-size-number-large);  /* 32px */
    font-weight: var(--font-weight-bold);      /* 700 */
}

.amount-positive {
    color: var(--secondary);  /* Green */
}

.amount-negative {
    color: var(--tertiary);   /* Red */
}
```

---

## 간격 체계 (Spacing)

### 기본 간격 단위

```css
/* 4px 기반 스케일 시스템 (Tailwind 호환) */
--spacing-0: 0;
--spacing-1: 2px;      /* 0.5 × 4 */
--spacing-2: 4px;      /* 1 × 4 */
--spacing-3: 6px;      /* 1.5 × 4 */
--spacing-4: 8px;      /* 2 × 4 (기본 단위) */
--spacing-6: 12px;     /* 3 × 4 */
--spacing-8: 16px;     /* 4 × 4 */
--spacing-10: 20px;    /* 5 × 4 */
--spacing-12: 24px;    /* 6 × 4 */
--spacing-16: 32px;    /* 8 × 4 */
--spacing-20: 40px;    /* 10 × 4 */
```

**간격 사용 가이드:**

| 간격 | 값 | 사용 예시 |
|------|-----|-----------|
| 0 | 0px | 간격 제거 |
| 2 | 4px | 배지/아이콘 간격 |
| 3 | 6px | 버튼 내부 간격 |
| 4 | 8px | 기본 요소 간격 |
| 6 | 12px | 카드 내부 간격 |
| 8 | 16px | 섹션 간격 |
| 10 | 20px | 사이드바 padding |
| 12 | 24px | 큰 섹션 간격 |
| 16 | 32px | 컨테이너 padding |
| 20 | 40px | 페이지 상하 여백 |

---

## 레이아웃 (Layout)

### Grid 시스템

#### 메인 레이아웃 (3-Column)
```css
.main-container {
    display: grid;
    grid-template-columns: 250px 1fr 280px;  /* 좌측 | 중앙 | 우측 */
    gap: 20px;
    padding: 20px;
    min-height: calc(100vh - 70px);  /* 헤더 제외 */
}
```

**레이아웃 구성:**
```
┌─────────────────────────────────────────┐
│           Header (70px)                 │
│  HDH Fintech - Double Hedge Trading     │
├──────────┬────────────────┬─────────────┤
│  Left    │    Center      │    Right    │
│ Sidebar  │   거래 프로세스  │   Sidebar   │
│ (250px)  │     (1fr)      │   (280px)   │
│          │                │             │
│ 준비     │   1. 시간 확인   │  공지사항   │
│ - 솔루션 │   2. 시스템     │  주의사항   │
│ - 매뉴얼 │   3. 코인 매입   │  누적 수익  │
│ - 교육   │   4. 포지션     │  수익 일지  │
│ - 다운로드│   ...          │             │
│          │                │             │
└──────────┴────────────────┴─────────────┘
```

### 반응형 Grid
```css
/* 태블릿 (768px ~ 1024px) */
@media (max-width: 1024px) {
    .main-container {
        grid-template-columns: 200px 1fr 240px;
        gap: 16px;
        padding: 16px;
    }
}

/* 모바일 (~ 768px) */
@media (max-width: 768px) {
    .main-container {
        grid-template-columns: 1fr;  /* 단일 컬럼 */
        gap: 12px;
        padding: 12px;
    }

    .left-sidebar,
    .right-sidebar {
        width: 100%;
    }
}
```

---

## 컴포넌트 (Components)

### 헤더 (Header)

```css
.header {
    background: var(--primary-gradient);
    color: white;
    height: 70px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 var(--spacing-16);
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.header-logo {
    font-size: var(--font-size-display);
    font-weight: var(--font-weight-bold);
    letter-spacing: -0.5px;
}

.header-tagline {
    font-size: var(--font-size-base);
    opacity: 0.9;
}
```

### 사이드바 (Sidebar)

#### 좌측 사이드바 (준비)
```css
.left-sidebar {
    background: var(--bg-white);
    border-radius: 8px;
    padding: var(--spacing-8);
    overflow-y: auto;
}

.sidebar-section {
    margin-bottom: var(--spacing-6);
    padding-bottom: var(--spacing-6);
    border-bottom: 1px solid var(--border-color);
}

.section-title {
    font-size: var(--font-size-h4);
    font-weight: var(--font-weight-semibold);
    color: var(--text-primary);
    margin-bottom: var(--spacing-4);
    display: flex;
    align-items: center;
    gap: var(--spacing-2);
}

.menu-item {
    padding: var(--spacing-3) var(--spacing-4);
    font-size: var(--font-size-sm);
    color: var(--text-secondary);
    cursor: pointer;
    border-radius: 4px;
    transition: all 0.2s ease;
}

.menu-item:hover {
    background: var(--primary-alpha-10);
    color: var(--primary);
}
```

#### 우측 사이드바 (결과/공지)
```css
.right-sidebar {
    background: var(--bg-white);
    border-radius: 8px;
    padding: var(--spacing-8);
    overflow-y: auto;
}

.widget {
    margin-bottom: var(--spacing-8);
    padding: var(--spacing-6);
    background: var(--bg-main);
    border-radius: 8px;
}

.widget-title {
    font-size: var(--font-size-h4);
    font-weight: var(--font-weight-semibold);
    color: var(--text-primary);
    margin-bottom: var(--spacing-4);
    display: flex;
    align-items: center;
    gap: var(--spacing-2);
}
```

### 거래 프로세스 스텝 (Process Steps)

```css
.process-step {
    background: var(--bg-white);
    border-radius: 8px;
    padding: var(--spacing-6);
    margin-bottom: var(--spacing-4);
    border: 2px solid var(--border-color);
    transition: all 0.3s ease;
}

.process-step.active {
    background: linear-gradient(135deg, #DBEAFE 0%, #BFDBFE 100%);
    border-color: var(--active);
    box-shadow: 0 4px 12px rgba(59, 130, 246, 0.2);
}

.step-header {
    display: flex;
    align-items: center;
    gap: var(--spacing-4);
    margin-bottom: var(--spacing-3);
}

.step-number {
    width: 32px;
    height: 32px;
    background: var(--primary-gradient);
    color: white;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: var(--font-size-sm);
    font-weight: var(--font-weight-bold);
}

.step-title {
    font-size: var(--font-size-h3);
    font-weight: var(--font-weight-semibold);
    color: var(--text-primary);
    flex: 1;
}

.step-status {
    font-size: 20px;
}

.step-description {
    font-size: var(--font-size-sm);
    color: var(--text-secondary);
    line-height: 1.6;
}

.step-description a {
    color: var(--active);
    text-decoration: none;
    font-weight: var(--font-weight-medium);
    transition: color 0.2s ease;
}

.step-description a:hover {
    color: var(--active-dark);
    text-decoration: underline;
}
```

### 버튼 (Buttons)

```css
/* 기본 버튼 */
.btn {
    padding: var(--spacing-3) var(--spacing-6);
    font-size: var(--font-size-sm);
    font-weight: var(--font-weight-semibold);
    border-radius: 6px;
    border: 2px solid transparent;
    cursor: pointer;
    transition: all 0.2s ease;
    display: inline-flex;
    align-items: center;
    gap: var(--spacing-2);
}

/* Primary 버튼 (골드) */
.btn-primary {
    background: var(--primary-gradient);
    color: white;
    border-color: var(--primary);
}

.btn-primary:hover {
    background: var(--primary-dark);
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(245, 158, 11, 0.3);
}

/* Success 버튼 (그린) */
.btn-success {
    background: var(--secondary);
    color: white;
    border-color: var(--secondary);
}

.btn-success:hover {
    background: var(--secondary-dark);
}

/* Danger 버튼 (레드) */
.btn-danger {
    background: var(--tertiary);
    color: white;
    border-color: var(--tertiary);
}

.btn-danger:hover {
    background: var(--tertiary-dark);
}

/* 알람 버튼 */
.btn-alarm {
    background: white;
    color: var(--active);
    border: 2px solid var(--active);
}

.btn-alarm:hover {
    background: var(--active);
    color: white;
}
```

### 위젯 컴포넌트 (Widgets)

#### 누적 수익 위젯
```css
.result-widget {
    text-align: center;
    padding: var(--spacing-8);
}

.result-value {
    font-family: var(--font-family-number);
    font-size: var(--font-size-number-large);
    font-weight: var(--font-weight-bold);
    color: var(--secondary);  /* Green */
    margin-bottom: var(--spacing-4);
    letter-spacing: -1px;
}

.achievement {
    margin-top: var(--spacing-4);
    padding: var(--spacing-3) var(--spacing-6);
    background: var(--secondary-alpha-10);
    border-radius: 20px;
    display: inline-block;
}

.achievement-text {
    font-size: var(--font-size-sm);
    color: var(--secondary-dark);
    font-weight: var(--font-weight-medium);
}
```

#### 수익 일지 위젯
```css
.diary-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: var(--spacing-3) 0;
    border-bottom: 1px solid var(--border-light);
    font-size: var(--font-size-sm);
}

.diary-date {
    color: var(--text-secondary);
    font-weight: var(--font-weight-medium);
}

.diary-amount {
    font-family: var(--font-family-number);
    font-weight: var(--font-weight-semibold);
}

.diary-amount.positive {
    color: var(--secondary);  /* Green */
}

.diary-amount.negative {
    color: var(--tertiary);   /* Red */
}
```

#### 공지사항/주의사항
```css
.notice-item,
.warning-item {
    padding: var(--spacing-4);
    margin-bottom: var(--spacing-3);
    border-radius: 6px;
    font-size: var(--font-size-sm);
}

.notice-item {
    background: var(--active-bg);
    border-left: 4px solid var(--active);
}

.notice-date {
    font-size: var(--font-size-xs);
    color: var(--text-tertiary);
    margin-bottom: var(--spacing-1);
}

.warning-item {
    background: var(--warning-bg);
    border-left: 4px solid var(--warning);
    color: var(--warning-text);
}
```

### 퀵 링크 (Quick Links)

```css
.quick-links {
    margin-top: var(--spacing-12);
    padding: var(--spacing-8);
    background: var(--bg-main);
    border-radius: 8px;
}

.quick-links-title {
    font-size: var(--font-size-h4);
    font-weight: var(--font-weight-semibold);
    color: var(--text-primary);
    margin-bottom: var(--spacing-6);
    display: flex;
    align-items: center;
    gap: var(--spacing-2);
}

.links-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: var(--spacing-4);
}

.quick-link-btn {
    padding: var(--spacing-6);
    background: white;
    border: 2px solid var(--border-color);
    border-radius: 8px;
    text-align: center;
    font-size: var(--font-size-sm);
    color: var(--text-primary);
    text-decoration: none;
    transition: all 0.2s ease;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: var(--spacing-2);
}

.quick-link-btn:hover {
    background: var(--primary-gradient);
    color: white;
    border-color: var(--primary);
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(245, 158, 11, 0.2);
}
```

---

## 애니메이션 & 효과 (Effects)

### Transition (전환 효과)

```css
--transition-fast: 0.15s ease;
--transition-base: 0.2s ease;
--transition-slow: 0.3s ease;
```

### Shadow (그림자)

```css
--shadow-sm: 0 1px 3px rgba(0, 0, 0, 0.12);
--shadow-md: 0 4px 6px rgba(0, 0, 0, 0.1);
--shadow-lg: 0 10px 20px rgba(0, 0, 0, 0.15);
--shadow-gold: 0 4px 12px rgba(245, 158, 11, 0.3);  /* 골드 그림자 */
--shadow-active: 0 4px 12px rgba(59, 130, 246, 0.2);  /* 활성 그림자 */
```

### Border Radius (모서리 둥글기)

```css
--border-radius-sm: 4px;      /* 작은 요소 */
--border-radius: 6px;         /* 기본 (버튼) */
--border-radius-md: 8px;      /* 중간 (카드) */
--border-radius-lg: 12px;     /* 큰 요소 */
--border-radius-xl: 16px;     /* 매우 큰 요소 */
--border-radius-full: 50%;    /* 원형 */
```

### 호버 효과

```css
/* 카드 호버 */
.card:hover {
    transform: translateY(-2px);
    box-shadow: var(--shadow-md);
}

/* 버튼 호버 */
.btn:hover {
    transform: translateY(-2px);
    box-shadow: var(--shadow-gold);
}

/* 프로세스 스텝 호버 */
.process-step:hover {
    border-color: var(--primary);
}
```

---

## 접근성 (Accessibility)

### 색상 명암비
```
WCAG 2.1 AA 기준:
- 일반 텍스트: 최소 4.5:1
- 큰 텍스트 (18pt+): 최소 3:1
```

### 포커스 표시
```css
*:focus {
    outline: 2px solid var(--primary);
    outline-offset: 2px;
}
```

---

## 반응형 디자인 (Responsive)

### 브레이크포인트

```css
--breakpoint-sm: 640px;
--breakpoint-md: 768px;
--breakpoint-lg: 1024px;
--breakpoint-xl: 1280px;
```

### 모바일 대응
```css
@media (max-width: 768px) {
    .main-container {
        grid-template-columns: 1fr;
    }

    .links-grid {
        grid-template-columns: repeat(2, 1fr);
    }

    .header-logo {
        font-size: 20px;
    }
}
```

---

## 디자인 토큰 (Design Tokens)

### 전체 토큰 정의 (CSS Variables)

```css
:root {
    /* ===== Colors ===== */

    /* Primary - Golden */
    --primary: #F59E0B;
    --primary-dark: #D97706;
    --primary-light: #FCD34D;
    --primary-gradient: linear-gradient(135deg, #F59E0B 0%, #D97706 100%);
    --primary-alpha-10: rgba(245, 158, 11, 0.1);
    --primary-alpha-20: rgba(245, 158, 11, 0.2);

    /* Secondary - Green */
    --secondary: #10B981;
    --secondary-dark: #059669;
    --secondary-light: #34D399;
    --secondary-alpha-10: rgba(16, 185, 129, 0.1);

    /* Tertiary - Red */
    --tertiary: #EF4444;
    --tertiary-dark: #DC2626;
    --tertiary-light: #F87171;
    --tertiary-alpha-10: rgba(239, 68, 68, 0.1);

    /* Status */
    --active: #3B82F6;
    --active-bg: #DBEAFE;
    --active-text: #1E3A8A;

    --waiting: #64748B;
    --waiting-bg: #F1F5F9;
    --waiting-text: #0F172A;

    --warning: #F59E0B;
    --warning-bg: #FEF3C7;
    --warning-text: #92400E;
    --warning-border: #FCD34D;

    /* Base */
    --bg-main: #F8FAFC;
    --bg-white: #FFFFFF;
    --bg-dark: #0F172A;
    --bg-overlay: rgba(0, 0, 0, 0.6);

    --text-primary: #0F172A;
    --text-secondary: #64748B;
    --text-tertiary: #94A3B8;
    --text-inverse: #FFFFFF;

    --border-color: #E2E8F0;
    --border-light: #F1F5F9;
    --border-dark: #CBD5E1;

    /* ===== Typography ===== */

    --font-family-base: 'Malgun Gothic', '맑은 고딕', 'Pretendard', 'Noto Sans KR', sans-serif;
    --font-family-heading: 'Malgun Gothic', '맑은 고딕', 'Segoe UI', 'Arial', sans-serif;
    --font-family-mono: 'Consolas', 'Monaco', 'Courier New', monospace;
    --font-family-number: 'SF Pro Display', 'Roboto', 'Malgun Gothic', monospace;

    --font-size-display: 28px;
    --font-size-h1: 24px;
    --font-size-h2: 18px;
    --font-size-h3: 16px;
    --font-size-h4: 14px;
    --font-size-base: 14px;
    --font-size-sm: 13px;
    --font-size-xs: 12px;
    --font-size-2xs: 11px;

    --font-size-number-large: 32px;
    --font-size-number-medium: 18px;
    --font-size-number-small: 14px;

    --line-height-display: 1.2;
    --line-height-h1: 1.3;
    --line-height-h2: 1.4;
    --line-height-h3: 1.5;
    --line-height-base: 1.6;

    --font-weight-regular: 400;
    --font-weight-medium: 500;
    --font-weight-semibold: 600;
    --font-weight-bold: 700;
    --font-weight-extrabold: 800;

    /* ===== Spacing ===== */

    --spacing-0: 0;
    --spacing-1: 2px;
    --spacing-2: 4px;
    --spacing-3: 6px;
    --spacing-4: 8px;
    --spacing-6: 12px;
    --spacing-8: 16px;
    --spacing-10: 20px;
    --spacing-12: 24px;
    --spacing-16: 32px;
    --spacing-20: 40px;

    /* ===== Effects ===== */

    --border-radius-sm: 4px;
    --border-radius: 6px;
    --border-radius-md: 8px;
    --border-radius-lg: 12px;
    --border-radius-xl: 16px;
    --border-radius-full: 50%;

    --shadow-sm: 0 1px 3px rgba(0, 0, 0, 0.12);
    --shadow-md: 0 4px 6px rgba(0, 0, 0, 0.1);
    --shadow-lg: 0 10px 20px rgba(0, 0, 0, 0.15);
    --shadow-gold: 0 4px 12px rgba(245, 158, 11, 0.3);
    --shadow-active: 0 4px 12px rgba(59, 130, 246, 0.2);

    --transition-fast: 0.15s ease;
    --transition-base: 0.2s ease;
    --transition-slow: 0.3s ease;
}
```

---

## 버전 관리

**Version 1.0.0** (2025-12-06)
- HDH Fintech 전용 디자인 시스템 구축
- 금융 거래 플랫폼에 최적화된 색상 체계
- 골드 그라데이션 브랜드 컬러
- 거래 프로세스 컴포넌트 정의
- 수익/손실 시각화 가이드라인

---

**이 문서는 HDH Fintech 플랫폼의 공식 디자인 시스템 가이드라인입니다.**
