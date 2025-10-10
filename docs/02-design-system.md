# Design System - Wildcard Crypto Trading App

## Overview
This document defines the design system for the Wildcard app, focusing on the retro aesthetic with neon colors and dark theme as shown in the Figma design.

## Color Palette

### Primary Colors
```css
:root {
  /* Background Colors */
  --bg-primary: #0a0a0a;      /* Main background */
  --bg-secondary: #1a1a1a;    /* Card backgrounds */
  --bg-tertiary: #2a2a2a;     /* Elevated surfaces */
  
  /* Neon Accent Colors */
  --neon-green: #00ff41;      /* Primary accent */
  --neon-blue: #0099ff;       /* Secondary accent */
  --neon-purple: #9945ff;     /* Tertiary accent */
  --neon-pink: #ff0080;       /* Quaternary accent */
  
  /* Text Colors */
  --text-primary: #ffffff;     /* Primary text */
  --text-secondary: #b3b3b3;   /* Secondary text */
  --text-muted: #666666;       /* Muted text */
  
  /* Border Colors */
  --border-default: #333333;   /* Default borders */
  --border-glow: #00ff41;      /* Glowing borders */
  
  /* Status Colors */
  --success: #00ff41;          /* Success states */
  --error: #ff4444;            /* Error states */
  --warning: #ffaa00;          /* Warning states */
  --info: #0099ff;             /* Info states */
}
```

### Usage Guidelines
- **Primary Background**: Use for main app background
- **Secondary Background**: Use for cards, modals, and elevated content
- **Neon Green**: Primary CTAs, success states, positive values
- **Neon Blue**: Secondary actions, info states, neutral highlights
- **Neon Purple**: Special features, premium content
- **Neon Pink**: Alerts, important notifications

## Typography

### Font Families
```css
/* Primary font for UI text */
font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;

/* Monospace font for numbers, code, data */
font-family: 'JetBrains Mono', 'Fira Code', monospace;
```

### Font Scale
```css
/* Headings */
.text-h1 { font-size: 3rem; font-weight: 700; line-height: 1.2; }
.text-h2 { font-size: 2.5rem; font-weight: 600; line-height: 1.3; }
.text-h3 { font-size: 2rem; font-weight: 600; line-height: 1.4; }
.text-h4 { font-size: 1.5rem; font-weight: 500; line-height: 1.4; }

/* Body text */
.text-lg { font-size: 1.125rem; line-height: 1.6; }
.text-base { font-size: 1rem; line-height: 1.6; }
.text-sm { font-size: 0.875rem; line-height: 1.5; }
.text-xs { font-size: 0.75rem; line-height: 1.4; }

/* Data/Numbers */
.text-mono { font-family: 'JetBrains Mono', monospace; }
```

## Spacing System
```css
/* Spacing scale (based on 4px grid) */
--space-1: 0.25rem;   /* 4px */
--space-2: 0.5rem;    /* 8px */
--space-3: 0.75rem;   /* 12px */
--space-4: 1rem;      /* 16px */
--space-5: 1.25rem;   /* 20px */
--space-6: 1.5rem;    /* 24px */
--space-8: 2rem;      /* 32px */
--space-10: 2.5rem;   /* 40px */
--space-12: 3rem;     /* 48px */
--space-16: 4rem;     /* 64px */
--space-20: 5rem;     /* 80px */
```

## Component Styles

### Cards
```css
.retro-card {
  background: var(--bg-secondary);
  border: 1px solid var(--border-default);
  border-radius: 8px;
  padding: var(--space-6);
  transition: all 0.3s ease;
}

.retro-card:hover {
  border-color: var(--neon-green);
  box-shadow: 0 0 20px rgba(0, 255, 65, 0.2);
}

.retro-card-glow {
  border-color: var(--neon-green);
  box-shadow: 0 0 20px rgba(0, 255, 65, 0.3);
}
```

### Buttons
```css
.btn-primary {
  background: linear-gradient(135deg, var(--neon-green), #00cc33);
  color: #000000;
  border: none;
  padding: var(--space-3) var(--space-6);
  border-radius: 6px;
  font-weight: 600;
  transition: all 0.3s ease;
}

.btn-primary:hover {
  box-shadow: 0 0 20px rgba(0, 255, 65, 0.5);
  transform: translateY(-2px);
}

.btn-secondary {
  background: transparent;
  color: var(--neon-blue);
  border: 1px solid var(--neon-blue);
  padding: var(--space-3) var(--space-6);
  border-radius: 6px;
  font-weight: 500;
  transition: all 0.3s ease;
}

.btn-secondary:hover {
  background: rgba(0, 153, 255, 0.1);
  box-shadow: 0 0 15px rgba(0, 153, 255, 0.3);
}
```

### Inputs
```css
.input-retro {
  background: var(--bg-tertiary);
  border: 1px solid var(--border-default);
  color: var(--text-primary);
  padding: var(--space-3) var(--space-4);
  border-radius: 6px;
  font-family: 'JetBrains Mono', monospace;
  transition: all 0.3s ease;
}

.input-retro:focus {
  outline: none;
  border-color: var(--neon-blue);
  box-shadow: 0 0 10px rgba(0, 153, 255, 0.3);
}
```

## Animations & Effects

### Glow Effects
```css
@keyframes glow-pulse {
  0%, 100% { box-shadow: 0 0 5px var(--neon-green); }
  50% { box-shadow: 0 0 20px var(--neon-green), 0 0 30px var(--neon-green); }
}

.glow-animation {
  animation: glow-pulse 2s ease-in-out infinite;
}
```

### Hover Transitions
```css
.hover-lift {
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.hover-lift:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.3);
}
```

### Loading States
```css
@keyframes shimmer {
  0% { background-position: -200px 0; }
  100% { background-position: calc(200px + 100%) 0; }
}

.loading-shimmer {
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.1), transparent);
  background-size: 200px 100%;
  animation: shimmer 1.5s infinite;
}
```

## Responsive Breakpoints
```css
/* Mobile first approach */
@media (min-width: 640px) { /* sm */ }
@media (min-width: 768px) { /* md */ }
@media (min-width: 1024px) { /* lg */ }
@media (min-width: 1280px) { /* xl */ }
@media (min-width: 1536px) { /* 2xl */ }
```

## Usage Examples

### Tailwind Classes
```html
<!-- Primary card -->
<div class="bg-card-bg border border-border-default rounded-lg p-6 hover:border-neon-green hover:shadow-[0_0_20px_rgba(0,255,65,0.2)] transition-all duration-300">

<!-- Neon text -->
<h1 class="text-neon-green text-4xl font-bold neon-text">

<!-- Data display -->
<span class="font-mono text-neon-blue">$1,234.56</span>
```

This design system ensures consistency across all components while maintaining the retro, cyberpunk aesthetic shown in the Figma design.
