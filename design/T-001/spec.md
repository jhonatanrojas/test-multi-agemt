# Design Specification: Portfolio SPA - T-001

## Overview
Portfolio web minimalista de una sola página (SPA) con estructura semántica HTML5, Tailwind CSS via CDN y JavaScript básico para interacciones.

## Design Tokens

### Colors (Tailwind)
- **Background**: `bg-white` (#FFFFFF)
- **Text Primary**: `text-gray-800` / `text-gray-900` (#333333)
- **Text Secondary**: `text-gray-600` (#666666)
- **Text Muted**: `text-gray-500` (#6B7280)
- **Border**: `border-gray-100` / `border-gray-200`
- **Accent CTA**: `bg-gray-900` (primary buttons)

### Typography
- **Font Family**: Inter (Google Fonts)
- **Weights**: 400 (regular), 500 (medium), 600 (semibold), 700 (bold), 800 (extrabold)
- **Scale**:
  - Hero: `text-4xl sm:text-5xl lg:text-6xl`
  - Section titles: `text-3xl sm:text-4xl`
  - Body: `text-lg`
  - Small: `text-sm`

### Spacing
- **Container**: `max-w-6xl mx-auto px-4 sm:px-6 lg:px-8`
- **Section padding**: `py-20 sm:py-24`
- **Card padding**: `p-6`
- **Gap**: `gap-4`, `gap-6`, `gap-8`

### Border Radius
- **Small**: `rounded-lg` (0.5rem)
- **Medium**: `rounded-xl` (0.75rem)
- **Large**: `rounded-2xl` (1rem)
- **Full**: `rounded-full` (pill buttons, badges)

## Layout Structure

### HTML5 Semantic Landmarks
```
├── <header> (fixed navigation)
├── <main>
│   ├── <section id="hero">
│   ├── <section id="projects">
│   ├── <section id="about">
│   └── <section id="contact">
└── <footer>
```

### Sections

#### Header (Fixed)
- Position: `fixed top-0 inset-x-0 z-50`
- Background: `bg-white/90 backdrop-blur-sm`
- Border: `border-b border-gray-100`
- Height: `h-16`
- Contains: Logo + Navigation links + Mobile menu button

#### Hero Section
- Height: `min-h-screen`
- Alignment: Flex centered
- Content: Badge + Headline + Description + CTA buttons

#### Projects Section
- Background: `bg-gray-50`
- Layout: Responsive grid `md:grid-cols-2 xl:grid-cols-3`
- Card style: Bordered, rounded-2xl, hover lift effect

#### About Section
- Layout: Two-column `lg:grid-cols-[1.3fr_0.7fr]`
- Content: Text + Skills badges + Placeholder image

#### Contact Section
- Background: `bg-gray-50`
- Layout: Three-column grid for contact cards
- Cards: LinkedIn, GitHub, Email with icons

#### Footer
- Border: `border-t border-gray-100`
- Content: Copyright + Navigation links

## Accessibility Features

### WCAG 2.1 AA Compliance
1. **Skip Link**: Keyboard navigation bypass to main content
2. **ARIA Labels**: All interactive elements have descriptive labels
3. **Focus Management**: Visible focus rings with `ring-2 ring-offset-2`
4. **Reduced Motion**: Respects `prefers-reduced-motion`
5. **Semantic HTML**: Proper heading hierarchy and landmarks
6. **Screen Reader**: `sr-only` class for visually hidden content

### Focus States
- Custom outline: `ring-2 ring-offset-2 ring-gray-900`
- Removed default outline: `outline-none`
- Visible on `:focus-visible`

### Motion Preferences
```css
@media (prefers-reduced-motion: reduce) {
  html { scroll-behavior: auto; }
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

## Responsive Breakpoints

| Breakpoint | Changes |
|------------|----------|
| Mobile (<640px) | Stacked buttons, single column grid, hidden nav links |
| SM (640px+) | Larger typography, flex row buttons |
| MD (768px+) | Two-column project grid, visible nav links |
| LG (1024px+) | Three-column project grid, two-column about |
| XL (1280px+) | Full layout, all features enabled |

## Interactions

### Mobile Menu Toggle
- Button: `#menu-button`
- Menu: `#mobile-menu`
- State: `aria-expanded` toggled on click
- Auto-close on link click

### Smooth Scroll
- HTML class: `scroll-smooth`
- Anchor links: Navigate to sections via ID
- Offset: Header height compensated with `pt-16` on main

## Implementation Notes

### CDN Dependencies
1. **Tailwind CSS**: `https://cdn.tailwindcss.com`
2. **Inter Font**: Google Fonts with `preconnect` for performance

### Tailwind Config Extension
```javascript
tailwind.config = {
  theme: {
    extend: {
      fontFamily: {
        inter: ['Inter', 'system-ui', 'sans-serif'],
      },
    },
  },
};
```

### Custom Base Layer
- Body: `bg-white text-gray-800 font-inter antialiased`
- Focus states: Consistent ring styling
- Reduced motion: Global override

## File Structure
```
projects/test-multi-agemt/
└── index.html (entry point)
```

## Acceptance Criteria Status
- [x] `projects/test-multi-agemt/index.html` created
- [x] DOCTYPE HTML5 valid
- [x] Tailwind CSS loaded via CDN
- [x] Inter font loaded from Google Fonts
- [x] Meta viewport configured for responsiveness
- [x] Base colors applied: bg-white, text-gray-800
