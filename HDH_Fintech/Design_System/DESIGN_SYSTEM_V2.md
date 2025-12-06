# SSALWorks Design System v2.0 (Prototype)

> **Theme**: Organic Growth (유기적 성장)
> **Keywords**: Growth, Warmth, Professional, Trust
> **Target**: Non-technical Founders (Avoiding "Dark Mode" Developer Tool look)

---

## 1. Color Palette (Organic Growth)

### Primary Colors
| Role | Name | Hex | Usage |
| :--- | :--- | :--- | :--- |
| **Primary** | **Emerald Green** | `#10B981` | Brand Identity, Main Actions, Active States (Growth/Rice) |
| **Secondary** | **Amber Gold** | `#F59E0B` | Highlights, Call-to-Actions, Accents (Sun/Fruit) |
| **Tertiary** | **Slate Navy** | `#0F172A` | Headings, Strong Text, Footer Background (Earth/Stability) |

### Neutral Colors
| Role | Name | Hex | Usage |
| :--- | :--- | :--- | :--- |
| **Background** | **Warm White** | `#FAFAF9` | Main Page Background (Stone-50) |
| **Surface** | **Pure White** | `#FFFFFF` | Cards, Modals, Panels |
| **Text Main** | **Slate 900** | `#0F172A` | Primary Text |
| **Text Muted** | **Slate 500** | `#64748B` | Secondary Text, Descriptions |
| **Border** | **Slate 200** | `#E2E8F0` | Dividers, Card Borders |

### Semantic Colors
- **Success**: `#10B981` (Same as Primary)
- **Warning**: `#F59E0B` (Same as Secondary)
- **Error**: `#EF4444` (Red 500)
- **Info**: `#3B82F6` (Blue 500)

---

## 2. Typography

**Font Family**:
- `Pretendard` (Primary Korean/English) - *Recommended for web*
- Fallback: `Malgun Gothic`, `sans-serif`

**Scale**:
- **Display**: 28px (Bold)
- **H1**: 24px (Bold)
- **H2**: 20px (SemiBold)
- **H3**: 18px (SemiBold)
- **Body**: 15px (Regular)
- **Small**: 13px (Regular)
- **Tiny**: 11px (Medium)

---

## 3. Spacing & Layout

**Grid System**:
- 4px Base Unit (Tailwind Default)
- **Layout**: 3-Column Grid (Sidebar Left - Workspace - Sidebar Right)
    - Left: 240px (Fixed)
    - Center: Flex (Fluid)
    - Right: 280px (Fixed)

**Radius**:
- **Small**: 4px (Buttons)
- **Medium**: 8px (Cards)
- **Large**: 12px (Modals)

---

## 4. Components

### Buttons
- **Primary**: Emerald Background, White Text
- **Secondary**: White Background, Slate Border, Slate Text
- **Ghost**: Transparent Background, Slate Text (Hover: Slate-100)

### Cards
- White Background
- Border: 1px solid Slate-200
- Shadow: `shadow-sm` (Tailwind)
- Hover: `shadow-md`, `border-emerald-200`

### Navigation
- **Sidebar**: White Background, Border-Right Slate-200
- **Active Item**: Emerald-50 Background, Emerald-600 Text, Emerald-500 Left Border
- **Menu Item**: Slate-700 Text, Hover: Emerald-50 Background
- **Submenu**: Indented 16px, Slate-600 Text, Smaller Font (13px)

### Modals
- **Overlay**: rgba(0,0,0,0.5) Background, z-index: 10000
- **Content**: White Background, 420px Width, Centered (top: 50%, left: 50%, transform: translate(-50%, -50%))
- **Border Radius**: 16px
- **Shadow**: 0 10px 40px rgba(0,0,0,0.2)
- **Animation**: modalZoomIn (0.3s ease-out), modalZoomOut (0.3s ease-in)
- **Header**: 24px Font, Bold, Slate-900 Color
- **Body**: 15px Font, Slate-700 Color, 14px Padding
- **Footer Button**: Full Width, 12px Padding, Blue Background (#007bff)

### Input Fields
- **Text Input**: White Background, Border: 1px solid Slate-300
- **Focus**: Border: Emerald-500, Box-Shadow: 0 0 0 3px Emerald-100
- **Disabled**: Slate-100 Background, Slate-400 Text
- **Error**: Border: Red-500, Box-Shadow: 0 0 0 3px Red-100
- **Height**: 40px (Default), 32px (Small)
- **Padding**: 12px Horizontal

### Textarea
- **Same as Text Input** with additional:
- **Min Height**: 120px
- **Resize**: Vertical Only

### Alerts & Toasts
- **Success**: Emerald-50 Background, Emerald-800 Text, Emerald-500 Left Border
- **Warning**: Amber-50 Background (#fff3cd), Amber-800 Text, Amber-500 Left Border (#ffc107)
- **Error**: Red-50 Background, Red-800 Text, Red-500 Left Border
- **Info**: Blue-50 Background, Blue-800 Text, Blue-500 Left Border
- **Border Width**: 4px (Left)
- **Padding**: 14px
- **Radius**: 8px

### Badges
- **Primary**: Emerald-100 Background, Emerald-800 Text
- **Secondary**: Slate-100 Background, Slate-800 Text
- **Warning**: Amber-100 Background, Amber-800 Text
- **Padding**: 4px 8px
- **Font Size**: 12px
- **Radius**: 4px

### Progress Bar
- **Track**: Slate-200 Background
- **Fill**: Emerald-500 Background
- **Height**: 8px
- **Radius**: 4px
- **Animation**: Smooth transition (0.3s ease)

### Tooltips
- **Background**: Slate-900
- **Text**: White
- **Font Size**: 13px
- **Padding**: 8px 12px
- **Radius**: 6px
- **Arrow**: 6px Triangle, Same Color as Background
- **Max Width**: 200px

### Dropdowns
- **Menu**: White Background, Border: 1px solid Slate-200
- **Shadow**: 0 4px 6px rgba(0,0,0,0.1)
- **Item**: 14px Font, Slate-700 Text
- **Hover**: Emerald-50 Background, Emerald-700 Text
- **Active**: Emerald-500 Background, White Text
- **Padding**: 10px 16px per Item

### Tables
- **Header**: Slate-100 Background, Slate-900 Text, 14px Font (Bold)
- **Row**: White Background, Slate-700 Text
- **Hover**: Slate-50 Background
- **Border**: 1px solid Slate-200 (Bottom)
- **Padding**: 12px per Cell
- **Alternating Rows**: Optional Slate-50 Background (Zebra Stripe)

---

## 5. Animations

### Keyframes Defined

**modalZoomIn**:
```css
@keyframes modalZoomIn {
  from {
    opacity: 0;
    transform: translate(-50%, -50%) scale(0.8);
  }
  to {
    opacity: 1;
    transform: translate(-50%, -50%) scale(1);
  }
}
```

**modalZoomOut**:
```css
@keyframes modalZoomOut {
  from {
    opacity: 1;
    transform: translate(-50%, -50%) scale(1);
  }
  to {
    opacity: 0;
    transform: translate(-50%, -50%) scale(0.8);
  }
}
```

**fadeIn**:
```css
@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}
```

**fadeOut**:
```css
@keyframes fadeOut {
  from { opacity: 1; }
  to { opacity: 0; }
}
```

**Usage**:
- Modals: 0.3s duration
- Toasts: 0.5s duration
- Hover States: 0.2s transition
- All Smooth: `transition: all 0.3s ease`

---

## 6. Icons

**Icon Library**:
- Font Awesome 6.x (CDN) - For general UI icons
- Custom SVG Icons - For brand-specific icons

**Icon Sizes**:
- Small: 14px
- Medium: 18px (Default)
- Large: 24px
- XLarge: 32px

**Icon Colors**:
- Default: Slate-600
- Active: Emerald-600
- Disabled: Slate-400
- Error: Red-500

---

## 7. Responsive Breakpoints

**Breakpoints** (Tailwind CSS):
- **sm**: 640px
- **md**: 768px
- **lg**: 1024px
- **xl**: 1280px
- **2xl**: 1536px

**Layout Adaptations**:
- **Desktop (≥1024px)**: 3-Column Layout (Sidebar Left - Workspace - Sidebar Right)
- **Tablet (768px - 1023px)**: 2-Column Layout (Workspace - Sidebar Right, Left Sidebar Collapsible)
- **Mobile (<768px)**: 1-Column Layout (Workspace Only, Sidebars Hidden/Drawer)

---

## 8. Accessibility

**Focus States**:
- All Interactive Elements: 3px solid Emerald-500 outline with 2px offset
- Skip to Content Link (Hidden, Visible on Focus)

**Color Contrast**:
- Text/Background: Minimum WCAG AA (4.5:1)
- Large Text: Minimum WCAG AA (3:1)

**Keyboard Navigation**:
- Tab Order: Logical (Top to Bottom, Left to Right)
- Escape Key: Close Modals/Dropdowns
- Enter/Space: Activate Buttons/Links

**Screen Readers**:
- All Images: `alt` attribute
- All Interactive Elements: ARIA labels
- Modal Focus Trap: Enabled

---

## 9. Implementation Notes

### CSS Framework
- **Tailwind CSS v3.x** (Utility-First)
- Custom Components: Extended with `@layer components`

### File Structure
```
/css
  ├── tailwind.config.js    # Tailwind Configuration
  ├── globals.css           # Global Styles + Tailwind Imports
  ├── components.css        # Custom Component Styles
  └── animations.css        # Keyframe Animations
```

### CDN Links (Prototype)
- Tailwind CSS: `https://cdn.tailwindcss.com`
- Font Awesome: `https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css`
- Pretendard Font: `https://cdn.jsdelivr.net/gh/orioncactus/pretendard/dist/web/static/pretendard.css`

---

## 10. Brand Assets

### Logo
- **Format**: SVG (Vector)
- **Colors**: Emerald-500 + Amber-500 Gradient
- **Variations**:
  - Full Logo (Text + Icon)
  - Icon Only (Square)
  - Wordmark Only (Text)

### Favicon
- **Sizes**: 16×16, 32×32, 48×48, 64×64
- **Format**: ICO + PNG

---

## 11. Version History

| Version | Date | Changes |
| :--- | :--- | :--- |
| v1.0 | 2025-11-10 | Initial Design System |
| v2.0 | 2025-12-01 | Components Section Complete (Based on Prototype Analysis) |

---

**Document Complete**

This design system is now ready for implementation across the SSALWorks platform. All components have been documented based on the actual prototype implementation in `prototype_index_최종개선.html`.
