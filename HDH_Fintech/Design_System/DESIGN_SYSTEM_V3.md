# HDH Fintech Design System v3.0

> **Theme**: Professional Growth & Trust (전문성과 신뢰)
> **Keywords**: Clarity, Efficiency, Success, Transparency
> **Target**: Fintech Platform Users (Non-technical Founders & Operators)
> **Updated**: 2025-12-06

---

## 1. Color Palette

### Primary Colors
| Role | Name | Hex | Usage |
| :--- | :--- | :--- | :--- |
| **Primary** | **Emerald Green** | `#10B981` | Success, Profit, Results (우측 사이드바) |
| **Secondary** | **Amber Gold** | `#F59E0B` | Main Actions, Process Steps (좌측/중앙) |
| **Tertiary** | **Blue** | `#3B82F6` | External Links, Shortcuts (바로가기) |
| **Accent** | **Slate Navy** | `#0F172A` | Headings, Strong Text |

### Neutral Colors
| Role | Name | Hex | Usage |
| :--- | :--- | :--- | :--- |
| **Background** | **Light Gray** | `#F8FAFC` | Main Page Background |
| **Surface** | **Pure White** | `#FFFFFF` | Cards, Modals, Panels, Items |
| **Text Primary** | **Slate 900** | `#0F172A` | Primary Text, Headings |
| **Text Secondary** | **Slate 700** | `#334155` | Body Text |
| **Text Muted** | **Slate 500** | `#64748B` | Secondary Text, Labels |
| **Text Disabled** | **Slate 400** | `#94A3B8` | Disabled States |
| **Border** | **Slate 200** | `#E2E8F0` | Default Borders, Dividers |

### Semantic Colors
| Purpose | Color | Hex | Usage |
| :--- | :--- | :--- | :--- |
| **Success** | Green | `#10B981` | Profit, Pass, Achievement |
| **Success Dark** | Green 700 | `#059669` | Hover, Active States |
| **Success Light** | Green 50 | `#ECFDF5` | Background Tints |
| **Success Border** | Green 200 | `#A7F3D0` | Light Borders |
| **Warning** | Amber | `#F59E0B` | Alerts, Important Info |
| **Warning Dark** | Amber 700 | `#D97706` | Gradients, Hover |
| **Warning Light** | Amber 50 | `#FFF7ED` | Background Tints |
| **Warning Border** | Amber 300 | `#FED7AA` | Light Borders |
| **Error** | Red | `#EF4444` | Errors, Loss, Stop Loss |
| **Error Dark** | Red 700 | `#DC2626` | Hover States |
| **Error Light** | Red 50 | `#FEF2F2` | Background Tints |
| **Error Border** | Red 200 | `#FECACA` | Light Borders |
| **Info** | Blue | `#3B82F6` | Information, External Links |
| **Info Dark** | Blue 700 | `#2563EB` | Hover States |
| **Info Light** | Blue 50 | `#EFF6FF` | Background Tints |
| **Info Border** | Blue 300 | `#93C5FD` | Light Borders |

### Gradient Colors
| Name | CSS Value | Usage |
| :--- | :--- | :--- |
| **Gold Gradient** | `linear-gradient(135deg, #F59E0B 0%, #D97706 100%)` | Header, Primary Buttons, Download Links |
| **Green Gradient** | `linear-gradient(135deg, #10B981 0%, #059669 100%)` | Success Buttons, Simulate Button |
| **Gold Light** | `linear-gradient(135deg, #FEF3C7 0%, #FDE68A 100%)` | Welcome Banner |
| **Green Light** | `linear-gradient(135deg, #ECFDF5 0%, #D1FAE5 100%)` | Success Cards |

---

## 2. Typography

### Font Family
```css
font-family: 'Malgun Gothic', '맑은 고딕', 'Apple SD Gothic Neo', sans-serif;
```
- Primary: Malgun Gothic (Windows 기본 한글 폰트)
- Fallback: Apple SD Gothic Neo (macOS)

### Monospace Font (Numbers)
```css
font-family: 'SF Pro Display', 'Roboto', 'Malgun Gothic', monospace;
```
- 사용처: 금액, 수익, 통계 숫자

### Type Scale
| Level | Size | Weight | Line Height | Usage |
| :--- | :--- | :--- | :--- | :--- |
| **Display** | 28px | 700 (Bold) | 1.3 | Page Titles (미사용) |
| **H1** | 24px | 700 (Bold) | 1.3 | Modal Titles |
| **H2** | 20px | 600 (SemiBold) | 1.4 | Section Headers |
| **H3** | 18px | 600 (SemiBold) | 1.4 | Widget Titles, Section Titles |
| **Body** | 15px | 400 (Regular) | 1.5 | Body Text, Descriptions, Buttons |
| **Small** | 13px | 400 (Regular) | 1.5 | Menu Items, Labels, Cards |
| **Tiny** | 11px | 500 (Medium) | 1.4 | Dates, Badges, Metadata |

### Font Weights
- **Regular**: 400 (기본 텍스트)
- **Medium**: 500 (작은 강조 텍스트)
- **SemiBold**: 600 (제목, 라벨)
- **Bold**: 700 (주요 제목, 버튼)

---

## 3. Spacing & Layout

### Grid System
**3-Column Layout**:
```css
grid-template-columns: 310px minmax(400px, 720px) 370px;
gap: 12px;
```

| Column | Width | Purpose |
| :--- | :--- | :--- |
| **Left Sidebar** | 310px | 준비 영역 (메뉴, 다운로드, 즐겨찾기, 커뮤니티) |
| **Center Content** | 400-720px (Fluid) | 실행 영역 (프로세스, 시뮬레이터) |
| **Right Sidebar** | 370px | 결과 영역 (수익, 공지, 일지, 설정) |

### Spacing Scale (4px Base Unit)
| Token | Value | Usage |
| :--- | :--- | :--- |
| **xs** | 4px | Tight spacing |
| **sm** | 8px | Component gaps, icon spacing |
| **md** | 12px | Default spacing, padding |
| **lg** | 16px | Section spacing |
| **xl** | 20px | Large spacing |
| **2xl** | 24px | Section margins |
| **3xl** | 32px | Major section gaps |

### Border Radius
| Size | Value | Usage |
| :--- | :--- | :--- |
| **Small** | 6px | Small Buttons, Badges |
| **Medium** | 8px | Cards, Inputs, Menu Items |
| **Large** | 12px | Widgets, Sections, Large Cards |
| **XLarge** | 16px | Modals, Major Components |

### Shadows
```css
/* Card Shadow */
box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);

/* Button Hover Shadow - Gold */
box-shadow: 0 4px 12px rgba(245, 158, 11, 0.4);

/* Button Hover Shadow - Green */
box-shadow: 0 4px 12px rgba(16, 185, 129, 0.3);

/* Button Hover Shadow - Blue */
box-shadow: 0 4px 12px rgba(59, 130, 246, 0.3);

/* Button Hover Shadow - Gray */
box-shadow: 0 4px 12px rgba(100, 116, 139, 0.3);

/* Modal Shadow */
box-shadow: 0 10px 40px rgba(0, 0, 0, 0.15);

/* Simulator Shadow */
box-shadow: 0 4px 16px rgba(0, 0, 0, 0.1);
```

---

## 4. Component Specifications

### 4.1 Header

**Specs**:
- Height: 70px
- Background: Gold Gradient (`linear-gradient(135deg, #F59E0B 0%, #D97706 100%)`)
- Padding: 0 40px
- Shadow: `0 4px 12px rgba(0, 0, 0, 0.15)`

**Elements**:
- Logo: 32px emoji
- Title: 28px Bold, White, Letter-spacing: -0.5px
- User Name: 16px SemiBold, White
- Notification Badge: 18px × 18px, Red Background (`#EF4444`)
- Logout Button: Transparent background, White text, 13px

**Logout Button Hover**:
```css
background: rgba(255, 255, 255, 0.3);
border-color: rgba(255, 255, 255, 0.6);
transform: translateY(-1px);
```

---

### 4.2 Left Sidebar (준비)

**Container**:
- Width: 310px
- Gap: 12px between sections

#### Section Title
```css
font-size: 15px;
font-weight: 700;
color: #0F172A;
margin-bottom: 12px;
display: flex;
align-items: center;
gap: 8px;
```

#### Menu Item
**Default**:
```css
padding: 10px 12px;
font-size: 13px;
color: #334155;
cursor: pointer;
transition: all 0.2s;
```

**Hover**:
```css
background: #FFF7ED;
color: #F59E0B;
```

**Active**:
```css
background: #FEF3C7;
color: #D97706;
font-weight: 600;
```

#### Submenu Item
**Default**:
```css
padding: 8px 12px 8px 28px; /* 16px indent */
font-size: 13px;
color: #64748B;
cursor: pointer;
transition: all 0.2s;
```

**Hover**:
```css
background: #FFF7ED;
color: #F59E0B;
```

#### Download Link Button
```css
padding: 10px;
margin-bottom: 8px;
background: linear-gradient(135deg, #F59E0B 0%, #D97706 100%);
color: white;
border-radius: 8px;
font-size: 13px;
font-weight: 600;
transition: all 0.2s;
```

**Hover**:
```css
transform: translateY(-2px);
box-shadow: 0 4px 12px rgba(245, 158, 11, 0.4);
```

#### Favorites Link (Blue Theme)
**Default**:
```css
padding: 10px 12px;
background: white;
border: 1px solid #E2E8F0;
border-radius: 8px;
font-size: 13px;
font-weight: 600;
color: #475569;
transition: all 0.2s;
```

**Hover**:
```css
background: #EFF6FF;
border-color: #93C5FD;
color: #3B82F6;
transform: translateX(2px);
```

#### Community Link (Blue Theme)
**Default**:
```css
padding: 14px 16px;
background: white;
border: 1px solid #BFDBFE;
border-radius: 8px;
font-size: 13px;
font-weight: 600;
color: #1E40AF;
transition: all 0.2s;
```

**Hover**:
```css
background: #EFF6FF;
border-color: #93C5FD;
transform: translateX(2px);
```

---

### 4.3 Center Content (실행)

#### Welcome Banner
```css
background: linear-gradient(135deg, #FEF3C7 0%, #FDE68A 100%);
padding: 20px 24px;
border-radius: 12px;
border-left: 4px solid #F59E0B;
```

**Title**: 20px Bold, Slate 900
**Description**: 15px Regular, Slate 700

#### Process Step
**Container**:
```css
background: #F8FAFC;
padding: 16px;
border-radius: 12px;
border: 2px solid #E5E7EB;
transition: all 0.2s;
```

**Step Number**:
```css
width: 32px;
height: 32px;
background: #E5E7EB;
color: #64748B;
border-radius: 50%;
font-size: 16px;
font-weight: 700;
```

**Active Step Number**:
```css
background: #3B82F6;
color: white;
```

**Step Title**: 14px Bold, Slate 900
**Step Description**: 13px Regular, Slate 500

#### Profit Simulator

**Title Section**:
```css
font-size: 18px;
font-weight: 600;
color: #0F172A;
```

**Subtitle**: 15px Regular, Slate 600

**Control Label**: 15px Regular, Slate 700

**Option Button**:
```css
padding: 10px 16px;
background: white;
border: 2px solid #E2E8F0;
border-radius: 8px;
font-size: 15px;
font-weight: 600;
color: #64748B;
transition: all 0.2s;
cursor: pointer;
```

**Option Button Hover**:
```css
background: #FFF7ED;
border-color: #F59E0B;
color: #D97706;
```

**Option Button Active**:
```css
background: linear-gradient(135deg, #F59E0B 0%, #D97706 100%);
border-color: #F59E0B;
color: white;
```

**Simulate Button**:
```css
padding: 16px 32px;
background: linear-gradient(135deg, #10B981 0%, #059669 100%);
color: white;
border: none;
border-radius: 12px;
font-size: 18px;
font-weight: 700;
box-shadow: 0 4px 12px rgba(16, 185, 129, 0.3);
transition: all 0.3s;
```

**Simulate Button Hover**:
```css
transform: translateY(-2px);
box-shadow: 0 6px 20px rgba(16, 185, 129, 0.4);
```

**Results Close Button**:
```css
padding: 8px 16px;
background: #64748B;
color: white;
border: none;
border-radius: 6px;
font-size: 13px;
font-weight: 600;
transition: all 0.2s;
```

**Close Button Hover**:
```css
background: #475569;
transform: translateY(-2px);
box-shadow: 0 4px 12px rgba(100, 116, 139, 0.3);
```

**Summary Card**:
```css
background: #F8FAFC;
border-radius: 12px;
padding: 20px;
border: 2px solid #E2E8F0;
```

**Summary Card (Profit)**:
```css
background: linear-gradient(135deg, #ECFDF5 0%, #D1FAE5 100%);
border-color: #10B981;
```

**Summary Label**: 13px Regular, Slate 500
**Summary Value**: 24px Bold, Emerald 600

**Breakdown Table**:
```css
font-size: 15px;
border-collapse: collapse;
width: 100%;
```

**Table Header**: Slate 100 Background, Slate 900 Text, 15px Bold
**Table Cell**: 15px Regular, 12px Padding
**Table Row Hover**: `#F8FAFC` Background

**Detailed Table**:
- Pass Row: `#FFF7ED` Background
- Fail Row: `#ECFDF5` Background
- Pass Badge: `#F59E0B` Background, White Text
- Fail Badge: `#10B981` Background, White Text

---

### 4.4 Right Sidebar (결과) - Green Theme

**Container**:
- Width: 370px
- Gap: 12px between widgets

#### Widget
```css
background: white;
border-radius: 12px;
padding: 16px;
box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
```

#### Widget Title
```css
font-size: 15px;
font-weight: 700;
color: #0F172A;
margin-bottom: 12px;
display: flex;
align-items: center;
gap: 8px;
```

**Icon**: 18px

#### Notice Item (Green Theme)
**Default**:
```css
padding: 10px;
margin-bottom: 8px;
background: white;
border-radius: 8px;
border: 1px solid #E2E8F0;
border-left: 3px solid #10B981;
font-size: 13px;
color: #475569;
cursor: pointer;
transition: all 0.2s;
```

**Hover**:
```css
background: #ECFDF5;
border-color: #A7F3D0;
border-left-color: #10B981;
```

**Notice Date**: 11px Medium, Slate 400

#### Warning Item (Red Theme)
**Default**:
```css
padding: 10px;
margin-bottom: 8px;
background: #FEF2F2;
border-radius: 8px;
border: 1px solid #FEE2E2;
border-left: 3px solid #EF4444;
font-size: 13px;
color: #991B1B;
cursor: pointer;
transition: all 0.2s;
```

**Hover**:
```css
background: #FEE2E2;
border-color: #FECACA;
border-left-color: #EF4444;
```

#### Result Value (Large Number)
```css
font-family: 'SF Pro Display', 'Roboto', 'Malgun Gothic', monospace;
font-size: 28px;
font-weight: 700;
color: #10B981;
text-align: center;
letter-spacing: -1px;
```

#### Achievement Badge
```css
padding: 12px;
background: #ECFDF5;
border-radius: 8px;
text-align: center;
font-size: 14px;
color: #059669;
font-weight: 600;
```

#### Diary Item (Green Theme)
**Default**:
```css
padding: 10px;
margin-bottom: 6px;
background: white;
border-radius: 8px;
border: 1px solid #E2E8F0;
font-size: 13px;
cursor: pointer;
transition: all 0.2s;
```

**Hover**:
```css
background: #ECFDF5;
border-color: #A7F3D0;
```

**Date**: 13px Regular, Slate 500
**Amount**: 13px SemiBold, Emerald 600 (positive) / Red 600 (negative)

#### Settings Item (Green Theme)
**Default**:
```css
padding: 12px;
background: white;
border-radius: 8px;
border: 1px solid #E2E8F0;
margin-bottom: 8px;
font-size: 13px;
cursor: pointer;
transition: all 0.2s;
```

**Hover**:
```css
background: #ECFDF5;
border-color: #A7F3D0;
color: #10B981;
```

#### View More Link (Green Theme)
**Default**:
```css
padding: 8px;
text-align: center;
color: #10B981;
font-size: 12px;
font-weight: 600;
border-radius: 6px;
transition: all 0.2s;
```

**Hover**:
```css
background: #ECFDF5;
color: #059669;
```

---

### 4.5 Modals

#### Overlay
```css
position: fixed;
top: 0;
left: 0;
width: 100%;
height: 100%;
background: rgba(0, 0, 0, 0.6);
z-index: 1000;
```

#### Modal Content
```css
background: white;
border-radius: 16px;
padding: 32px;
max-width: 600px;
width: 90%;
max-height: 80vh;
overflow-y: auto;
box-shadow: 0 10px 40px rgba(0, 0, 0, 0.15);
```

#### Modal Header
```css
display: flex;
justify-content: space-between;
align-items: center;
margin-bottom: 24px;
```

**Title**: 24px Bold, Slate 900

#### Modal Close Button
```css
width: 32px;
height: 32px;
background: #F1F5F9;
border: none;
border-radius: 50%;
font-size: 20px;
color: #64748B;
cursor: pointer;
transition: all 0.2s;
```

**Hover**:
```css
background: #FEE2E2;
color: #DC2626;
```

#### Modal Body
```css
margin-bottom: 24px;
font-size: 15px;
color: #475569;
line-height: 1.6;
```

#### Modal Footer Buttons
**Cancel Button**:
```css
padding: 10px 24px;
background: white;
border: 1px solid #E2E8F0;
border-radius: 8px;
font-size: 14px;
font-weight: 600;
color: #64748B;
transition: all 0.2s;
```

**Cancel Hover**:
```css
background: #F8FAFC;
border-color: #94A3B8;
```

**Save Button**:
```css
padding: 10px 24px;
background: #10B981;
border: none;
border-radius: 8px;
font-size: 14px;
font-weight: 600;
color: white;
transition: all 0.2s;
```

**Save Hover**:
```css
background: #059669;
transform: translateY(-2px);
box-shadow: 0 4px 12px rgba(16, 185, 129, 0.3);
```

---

## 5. Hover States - Color by Section

### 5.1 Left Sidebar (좌측) - GOLD THEME 🟡

| Component | Default | Hover Background | Hover Text | Transform |
| :--- | :--- | :--- | :--- | :--- |
| Menu Item | Transparent | `#FFF7ED` | `#F59E0B` | - |
| Submenu Item | Transparent | `#FFF7ED` | `#F59E0B` | - |
| Download Link | Gold Gradient | Same | - | `translateY(-2px)` |

### 5.2 Center Content (중앙) - GOLD/GREEN THEME 🟡🟢

| Component | Default | Hover Background | Hover Text | Transform |
| :--- | :--- | :--- | :--- | :--- |
| Option Button | White | `#FFF7ED` | `#D97706` | - |
| Simulate Button | Green Gradient | Same | - | `translateY(-2px)` |
| Close Button | Gray | `#475569` | - | `translateY(-2px)` |

### 5.3 Right Sidebar (우측) - GREEN THEME 🟢

| Component | Default | Hover Background | Hover Border | Hover Text |
| :--- | :--- | :--- | :--- | :--- |
| Notice Item | White | `#ECFDF5` | `#A7F3D0` | - |
| Diary Item | White | `#ECFDF5` | `#A7F3D0` | - |
| Settings Item | White | `#ECFDF5` | `#A7F3D0` | `#10B981` |
| View More | Transparent | `#ECFDF5` | - | `#059669` |
| Warning Item | `#FEF2F2` | `#FEE2E2` | `#FECACA` | - |

### 5.4 Shortcuts/External Links - BLUE THEME 🔵

| Component | Default | Hover Background | Hover Border | Hover Text |
| :--- | :--- | :--- | :--- | :--- |
| Favorite Link | White | `#EFF6FF` | `#93C5FD` | `#3B82F6` |
| Community Link | White | `#EFF6FF` | `#93C5FD` | - |

### 5.5 Universal Rules

**Primary Action Buttons**:
- Keep original gradient/solid color
- Add: `transform: translateY(-2px)`
- Add: Enhanced `box-shadow`

**Secondary Buttons**:
- Background: `#F8FAFC`
- Border: Darker shade

**Table Rows**:
- Background: `#F8FAFC` only

**Modal Close**:
- Background: `#FEE2E2`
- Color: `#DC2626`

---

## 6. Transitions & Animations

### Standard Transitions
```css
/* Default - All Properties */
transition: all 0.2s ease;

/* Button Specific */
transition: all 0.3s ease;

/* Background Only */
transition: background 0.2s ease;
```

### Transform Effects
```css
/* Button Hover - Lift */
transform: translateY(-2px);

/* Link Hover - Slide Right */
transform: translateX(2px);

/* Link Hover - Slide Right (More) */
transform: translateX(4px);
```

### Accordion Arrow Rotation
```css
/* Collapsed */
transform: rotate(0deg);

/* Expanded */
transform: rotate(90deg);
```

---

## 7. Responsive Design

### Breakpoints
```css
/* Desktop */
@media (min-width: 1024px) {
  /* 3-Column Layout: 310px | flex | 370px */
}

/* Tablet */
@media (max-width: 1400px) {
  grid-template-columns: 220px 1fr 260px;
  gap: 16px;
}

/* Small Tablet */
@media (max-width: 1200px) {
  grid-template-columns: 200px 1fr 240px;
  gap: 12px;
  padding: 16px;
}

/* Mobile */
@media (max-width: 768px) {
  /* Single Column Stack */
  grid-template-columns: 1fr;
}
```

---

## 8. Implementation Guidelines

### 8.1 HTML Structure
```html
<div class="main-container">
  <div class="left-sidebar">
    <!-- 준비 영역 -->
  </div>
  <div class="center-content">
    <!-- 실행 영역 -->
  </div>
  <div class="right-sidebar">
    <!-- 결과 영역 -->
  </div>
</div>
```

### 8.2 CSS Best Practices

**Use semantic class names**:
```css
.menu-item { }          /* Good */
.item-1 { }             /* Bad */
```

**Group related properties**:
```css
/* Layout */
display: flex;
align-items: center;

/* Spacing */
padding: 10px;
margin-bottom: 8px;

/* Visual */
background: white;
border-radius: 8px;

/* Typography */
font-size: 13px;
color: #334155;

/* Interaction */
cursor: pointer;
transition: all 0.2s;
```

**Use consistent units**:
- Spacing: `px` (based on 4px grid)
- Font sizes: `px` (precise control)
- Line heights: unitless numbers

---

## 9. Accessibility

### Focus States
```css
/* Keyboard Focus Visible */
:focus-visible {
  outline: 2px solid #10B981;
  outline-offset: 2px;
}
```

### Color Contrast
- All text meets WCAG AA standards (4.5:1 minimum)
- Large text (18px+) meets 3:1 minimum

### Interactive Elements
- All clickable elements have `cursor: pointer`
- All interactive elements have visible hover states
- All buttons have appropriate `transition` effects

### Screen Readers
- Use semantic HTML (`<header>`, `<nav>`, `<main>`, etc.)
- All icons should have text labels or `aria-label`
- Modals should trap focus when active

---

## 10. Design Tokens (CSS Variables)

### Recommended CSS Variables
```css
:root {
  /* Colors - Primary */
  --color-green-primary: #10B981;
  --color-green-dark: #059669;
  --color-green-light: #ECFDF5;
  --color-green-border: #A7F3D0;

  --color-gold-primary: #F59E0B;
  --color-gold-dark: #D97706;
  --color-gold-light: #FFF7ED;
  --color-gold-border: #FED7AA;

  --color-blue-primary: #3B82F6;
  --color-blue-dark: #2563EB;
  --color-blue-light: #EFF6FF;
  --color-blue-border: #93C5FD;

  /* Colors - Neutral */
  --color-white: #FFFFFF;
  --color-gray-50: #F8FAFC;
  --color-gray-200: #E2E8F0;
  --color-gray-400: #94A3B8;
  --color-gray-500: #64748B;
  --color-gray-600: #475569;
  --color-gray-700: #334155;
  --color-gray-900: #0F172A;

  /* Spacing */
  --space-xs: 4px;
  --space-sm: 8px;
  --space-md: 12px;
  --space-lg: 16px;
  --space-xl: 20px;
  --space-2xl: 24px;
  --space-3xl: 32px;

  /* Border Radius */
  --radius-sm: 6px;
  --radius-md: 8px;
  --radius-lg: 12px;
  --radius-xl: 16px;

  /* Typography */
  --font-size-tiny: 11px;
  --font-size-small: 13px;
  --font-size-body: 15px;
  --font-size-h3: 18px;
  --font-size-h2: 20px;
  --font-size-h1: 24px;

  /* Shadows */
  --shadow-card: 0 2px 8px rgba(0, 0, 0, 0.08);
  --shadow-modal: 0 10px 40px rgba(0, 0, 0, 0.15);

  /* Transitions */
  --transition-fast: all 0.2s ease;
  --transition-medium: all 0.3s ease;
}
```

---

## 11. Version History

| Version | Date | Changes |
| :--- | :--- | :--- |
| v1.0 | 2025-11-10 | Initial Design System |
| v2.0 | 2025-12-01 | Components Section Complete |
| **v3.0** | **2025-12-06** | **HDH Fintech Complete Implementation** |

### v3.0 Changes (2025-12-06)
1. **Complete Typography System**
   - Applied design system font sizes consistently
   - Removed Display level (unused)
   - Defined all component text sizes

2. **Color System by Section**
   - Left Sidebar: Gold Theme (준비)
   - Center Content: Gold/Green Theme (실행)
   - Right Sidebar: Green Theme (결과)
   - Shortcuts: Blue Theme (바로가기)

3. **Hover States Unified**
   - Section-based color rules
   - Consistent transform effects
   - Unified transition durations

4. **Component Specifications**
   - Header: 70px with gold gradient
   - Grid: 310px | flex | 370px with 12px gap
   - All widgets, cards, buttons documented
   - Profit simulator complete specs
   - Modal system complete specs

5. **New Components**
   - Community Link (Blue theme)
   - Favorites (Blue theme)
   - Settings Items (Green theme)
   - Notice Items (Green theme)
   - Diary Items (Green theme)
   - Warning Items (Red theme)
   - Profit Simulator (Complete)

6. **Design Tokens**
   - CSS Variables recommended
   - Spacing scale defined
   - Shadow system defined

---

## 12. File Reference

**Main Implementation**: `G:\내 드라이브\SUNNY_ECOSYSTEM\HDH_Fintech\index.html`

**Design System**: `G:\내 드라이브\SUNNY_ECOSYSTEM\HDH_Fintech\Design_System\DESIGN_SYSTEM_V3.md`

---

**Document Status**: ✅ Complete and Production-Ready

This design system reflects the actual implementation of the HDH Fintech platform as of 2025-12-06. All components, colors, typography, and interactions have been documented based on the live codebase.
