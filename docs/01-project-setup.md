# Project Setup - Wildcard Crypto Trading App

## Overview
This document outlines the initial setup for the Wildcard crypto trading app frontend, built with Next.js, TypeScript, and modern UI libraries.

## Tech Stack
- **Framework**: Next.js 14+ with App Router
- **Language**: TypeScript
- **Package Manager**: pnpm
- **UI Libraries**: 
  - shadcn/ui (primary component library)
  - Hero UI (additional components)
  - Aceternity UI (special effects and animations)
- **Styling**: Tailwind CSS
- **Charts**: Recharts or TradingView widgets
- **Icons**: Lucide React

## Initial Setup Commands

```bash
# Create Next.js project
npx create-next-app@latest wildcard-app --typescript --tailwind --eslint --app --src-dir --import-alias "@/*"

cd wildcard-app

# Install shadcn/ui
npx shadcn-ui@latest init

# Install additional dependencies
pnpm add @heroui/react @aceternity/ui
pnpm add lucide-react recharts
pnpm add framer-motion clsx tailwind-merge
pnpm add @radix-ui/react-slot @radix-ui/react-dialog
pnpm add class-variance-authority

# Development dependencies
pnpm add -D @types/node
```

## Project Structure
```
src/
├── app/
│   ├── globals.css
│   ├── layout.tsx
│   ├── page.tsx
│   ├── advanced/
│   ├── community/
│   ├── how-it-works/
│   └── support/
├── components/
│   ├── ui/          # shadcn/ui components
│   ├── layout/      # Navigation, header, footer
│   ├── trading/     # Trading-specific components
│   ├── charts/      # Chart components
│   └── common/      # Reusable components
├── lib/
│   ├── utils.ts
│   └── constants.ts
├── styles/
└── types/
```

## Configuration Files

### tailwind.config.js
```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
  darkMode: ["class"],
  content: [
    './pages/**/*.{ts,tsx}',
    './components/**/*.{ts,tsx}',
    './app/**/*.{ts,tsx}',
    './src/**/*.{ts,tsx}',
  ],
  theme: {
    extend: {
      colors: {
        // Retro color scheme
        'neon-green': '#00ff41',
        'neon-blue': '#0099ff',
        'neon-purple': '#9945ff',
        'dark-bg': '#0a0a0a',
        'card-bg': '#1a1a1a',
        'border-glow': '#333333',
      },
      fontFamily: {
        'mono': ['JetBrains Mono', 'monospace'],
        'sans': ['Inter', 'sans-serif'],
      },
      animation: {
        'glow': 'glow 2s ease-in-out infinite alternate',
        'float': 'float 3s ease-in-out infinite',
      },
      keyframes: {
        glow: {
          '0%': { boxShadow: '0 0 5px #00ff41' },
          '100%': { boxShadow: '0 0 20px #00ff41, 0 0 30px #00ff41' },
        },
        float: {
          '0%, 100%': { transform: 'translateY(0px)' },
          '50%': { transform: 'translateY(-10px)' },
        },
      },
    },
  },
  plugins: [require("tailwindcss-animate")],
}
```

### globals.css additions
```css
@import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;600;700&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap');

body {
  background: #0a0a0a;
  color: #ffffff;
  font-family: 'Inter', sans-serif;
}

.retro-glow {
  box-shadow: 0 0 10px rgba(0, 255, 65, 0.3);
}

.neon-text {
  text-shadow: 0 0 10px currentColor;
}
```

## Environment Setup
Create `.env.local`:
```
NEXT_PUBLIC_APP_NAME=Wildcard
NEXT_PUBLIC_API_URL=http://localhost:3000/api
```

## Next Steps
1. Set up the basic layout structure
2. Implement the design system and theme
3. Create reusable UI components
4. Build individual pages according to the Figma design

## Development Commands
```bash
# Start development server
pnpm dev

# Build for production
pnpm build

# Run linting
pnpm lint

# Add shadcn/ui components as needed
npx shadcn-ui@latest add button
npx shadcn-ui@latest add card
npx shadcn-ui@latest add dialog
```
