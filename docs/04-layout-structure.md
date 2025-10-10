# Layout Structure - Wildcard Crypto Trading App

## Overview
This document defines the layout structure and navigation system for the Wildcard app based on the Figma design.

## Main Layout Structure

### Root Layout (`app/layout.tsx`)
```typescript
export default function RootLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return (
    <html lang="en" className="dark">
      <body className="bg-dark-bg text-white font-sans antialiased">
        <Navigation />
        <main className="min-h-screen">
          {children}
        </main>
        <Footer />
      </body>
    </html>
  )
}
```

## Navigation Component

### Top Navigation Bar
**Location**: `components/layout/Navigation.tsx`

**Structure**:
```
[Logo] ---- [Menu Items] ---- [User Actions]
```

**Menu Items** (from Figma design):
1. **Home** - Accessible only through logo click
2. **Advanced** - `/advanced` - Trading interface
3. **Community** - `/community` - Community features
4. **How it Works** - `/how-it-works` - Educational content
5. **Support** - `/support` - Help and support

### Navigation Implementation
```typescript
interface NavigationItem {
  label: string;
  href: string;
  icon?: React.ReactNode;
  isActive?: boolean;
}

const navigationItems: NavigationItem[] = [
  { label: 'Advanced', href: '/advanced' },
  { label: 'Community', href: '/community' },
  { label: 'How it Works', href: '/how-it-works' },
  { label: 'Support', href: '/support' },
];
```

**Features**:
- Logo SVG on the left (links to home)
- Horizontal menu items in center
- Active state with neon glow
- Responsive mobile hamburger menu
- Retro styling with hover effects

### Navigation Styling
```css
.nav-container {
  background: rgba(26, 26, 26, 0.95);
  backdrop-filter: blur(10px);
  border-bottom: 1px solid var(--border-default);
  position: sticky;
  top: 0;
  z-index: 50;
}

.nav-item {
  color: var(--text-secondary);
  transition: all 0.3s ease;
  padding: 0.75rem 1.5rem;
  border-radius: 6px;
}

.nav-item:hover {
  color: var(--neon-green);
  background: rgba(0, 255, 65, 0.1);
  box-shadow: 0 0 10px rgba(0, 255, 65, 0.2);
}

.nav-item.active {
  color: var(--neon-green);
  background: rgba(0, 255, 65, 0.15);
  box-shadow: 0 0 15px rgba(0, 255, 65, 0.3);
}
```

## Page Layouts

### 1. Home Page Layout
**Route**: `/`
**Layout**: Hero section + Token grid

```
┌─────────────────────────────────────┐
│            Navigation               │
├─────────────────────────────────────┤
│                                     │
│         Hero Section                │
│      (Logo + Tagline)               │
│                                     │
├─────────────────────────────────────┤
│                                     │
│         Token Grid                  │
│    [Card] [Card] [Card] [Card]      │
│    [Card] [Card] [Card] [Card]      │
│    [Card] [Card] [Card] [Card]      │
│                                     │
└─────────────────────────────────────┘
```

### 2. Advanced Page Layout
**Route**: `/advanced`
**Layout**: Trading interface with charts and data

```
┌─────────────────────────────────────┐
│            Navigation               │
├─────────────────────────────────────┤
│  Chart Area        │  Trading Panel │
│                    │                │
│                    │  [Buy/Sell]    │
│                    │  [Amount]      │
│                    │  [Price]       │
├────────────────────┼────────────────┤
│         Data Table                  │
│  [Token] [Price] [Change] [Volume]  │
│                                     │
└─────────────────────────────────────┘
```

### 3. Community Page Layout
**Route**: `/community`
**Layout**: Community features and token listings

```
┌─────────────────────────────────────┐
│            Navigation               │
├─────────────────────────────────────┤
│         Community Header            │
├─────────────────────────────────────┤
│  Featured Tokens  │   Community     │
│                   │   Activity      │
│  [Token Grid]     │   [Feed]        │
│                   │                 │
└─────────────────────────────────────┘
```

### 4. How It Works Page Layout
**Route**: `/how-it-works`
**Layout**: Educational content with steps

```
┌─────────────────────────────────────┐
│            Navigation               │
├─────────────────────────────────────┤
│              Hero                   │
│         "How it works"              │
├─────────────────────────────────────┤
│                                     │
│         Step 1                      │
│    [Icon] [Description]             │
│                                     │
│         Step 2                      │
│    [Icon] [Description]             │
│                                     │
│         Step 3                      │
│    [Icon] [Description]             │
│                                     │
└─────────────────────────────────────┘
```

### 5. Support Page Layout
**Route**: `/support`
**Layout**: Help and support content

```
┌─────────────────────────────────────┐
│            Navigation               │
├─────────────────────────────────────┤
│         Support Header              │
├─────────────────────────────────────┤
│    FAQ Section    │  Contact Form   │
│                   │                 │
│  [Accordion]      │  [Form Fields]  │
│                   │                 │
└─────────────────────────────────────┘
```

## Responsive Breakpoints

### Desktop (1024px+)
- Full navigation bar
- Multi-column layouts
- Large token grids (4-5 columns)
- Side-by-side chart and trading panel

### Tablet (768px - 1023px)
- Condensed navigation
- 2-3 column token grid
- Stacked chart and trading panel

### Mobile (< 768px)
- Hamburger menu
- Single column layouts
- Stacked components
- Full-width cards

## Container Specifications

### Page Container
```css
.page-container {
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 1.5rem;
}
```

### Section Spacing
```css
.section {
  padding: 4rem 0;
}

.section-sm {
  padding: 2rem 0;
}

.section-lg {
  padding: 6rem 0;
}
```

### Grid Systems
```css
/* Token grid */
.token-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 1.5rem;
}

/* Two-column layout */
.two-column {
  display: grid;
  grid-template-columns: 2fr 1fr;
  gap: 2rem;
}

@media (max-width: 1024px) {
  .two-column {
    grid-template-columns: 1fr;
  }
}
```

## Footer Component
**Location**: `components/layout/Footer.tsx`

**Content**:
- Copyright information
- Links to social media
- Legal links (Terms, Privacy)
- Minimal retro styling

## Layout Components to Build

1. **Navigation.tsx** - Top navigation bar
2. **PageLayout.tsx** - Common page wrapper
3. **GridLayout.tsx** - Responsive grid container
4. **TwoColumnLayout.tsx** - Side-by-side layout
5. **Footer.tsx** - Site footer
6. **MobileMenu.tsx** - Mobile navigation drawer

## Implementation Notes

- Use CSS Grid for main layouts
- Implement sticky navigation
- Ensure proper z-index stacking
- Add smooth transitions between pages
- Include loading states for page transitions
- Maintain consistent spacing throughout
- Follow the retro design system colors and effects
