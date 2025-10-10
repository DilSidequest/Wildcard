# Pages Overview - Wildcard Crypto Trading App

## Overview
This document provides a comprehensive overview of all pages in the Wildcard app based on the Figma design analysis.

## Page Structure Summary

| Page | Route | Purpose | Key Components |
|------|-------|---------|----------------|
| Home | `/` | Landing page with token overview | Hero, TokenGrid |
| Advanced | `/advanced` | Trading interface | Charts, TradingPanel, DataTable |
| Community | `/community` | Community features | TokenGrid, ActivityFeed |
| How it Works | `/how-it-works` | Educational content | StepIndicator, InfoSections |
| Support | `/support` | Help and support | FAQ, ContactForm |

## Page Specifications

### 1. Home Page (`/`)
**File**: `app/page.tsx`

**Purpose**: 
- Main landing page accessible through logo
- Overview of available tokens
- Entry point to the application

**Sections**:
1. **Hero Section**
   - Large Wildcard logo/branding
   - Tagline or brief description
   - Call-to-action buttons

2. **Token Grid Section**
   - Grid of token cards (4-5 columns on desktop)
   - Each card shows: token image, name, symbol, price, 24h change
   - Hover effects with neon glow
   - Click to navigate to advanced trading

**Key Features**:
- Responsive token grid
- Real-time price updates
- Search and filter functionality
- Smooth animations and transitions

**Components Used**:
- `TokenCard`
- `GridLayout`
- `PriceDisplay`
- `RetroButton`

### 2. Advanced Page (`/advanced`)
**File**: `app/advanced/page.tsx`

**Purpose**:
- Full trading interface
- Detailed charts and market data
- Buy/sell functionality

**Sections**:
1. **Chart Area** (Left side, ~70% width)
   - Interactive price charts
   - Multiple timeframes (1h, 4h, 1d, 1w)
   - Chart type toggles (candlestick, line, area)
   - Volume indicators

2. **Trading Panel** (Right side, ~30% width)
   - Buy/Sell toggle
   - Amount input
   - Price calculation
   - Order placement buttons
   - Portfolio summary

3. **Data Table** (Bottom section)
   - All tokens with detailed information
   - Sortable columns: Name, Price, Change, Volume, Market Cap
   - Pagination or infinite scroll

**Key Features**:
- Real-time chart updates
- Interactive trading interface
- Comprehensive market data
- Responsive layout (stacks on mobile)

**Components Used**:
- `TradingChart`
- `TradingInterface`
- `DataTable`
- `PriceDisplay`
- `GlowCard`

### 3. Community Page (`/community`)
**File**: `app/community/page.tsx`

**Purpose**:
- Community-driven features
- Token discovery
- Social trading elements

**Sections**:
1. **Community Header**
   - Page title and description
   - Community statistics

2. **Featured Tokens** (Left side)
   - Curated token selection
   - Community favorites
   - Trending tokens

3. **Community Activity** (Right side)
   - Recent trades
   - User activities
   - Social feed elements

**Key Features**:
- Community-curated content
- Social trading features
- Activity feeds
- Token recommendations

**Components Used**:
- `TokenGrid`
- `ActivityFeed`
- `GlowCard`
- `Badge`

### 4. How It Works Page (`/how-it-works`)
**File**: `app/how-it-works/page.tsx`

**Purpose**:
- Educational content
- Step-by-step process explanation
- User onboarding

**Sections**:
1. **Hero Section**
   - Large "How it Works" title
   - Brief overview description

2. **Process Steps**
   - Step 1: Create Account / Connect Wallet
   - Step 2: Browse and Select Tokens
   - Step 3: Buy/Sell with Ease
   - Step 4: Track Your Portfolio

3. **Additional Information**
   - FAQ section
   - Getting started tips
   - Links to support

**Key Features**:
- Clear step-by-step process
- Visual indicators and icons
- Progressive disclosure of information
- Call-to-action to get started

**Components Used**:
- `StepIndicator`
- `GlowCard`
- `RetroButton`
- `Modal` (for detailed explanations)

### 5. Support Page (`/support`)
**File**: `app/support/page.tsx`

**Purpose**:
- Help and support resources
- Contact information
- Troubleshooting guides

**Sections**:
1. **Support Header**
   - Page title
   - Quick help options

2. **FAQ Section** (Left side)
   - Expandable accordion
   - Common questions and answers
   - Search functionality

3. **Contact Form** (Right side)
   - Contact form for specific issues
   - Support ticket submission
   - Response time expectations

4. **Additional Resources**
   - Documentation links
   - Video tutorials
   - Community forums

**Key Features**:
- Searchable FAQ
- Contact form with validation
- Resource links
- Responsive layout

**Components Used**:
- `Accordion` (from shadcn/ui)
- `ContactForm`
- `GlowCard`
- `RetroButton`

## Common Page Elements

### Page Wrapper
All pages should use a consistent wrapper:
```typescript
interface PageProps {
  children: React.ReactNode;
  title: string;
  description?: string;
}
```

### Loading States
Each page should include:
- Skeleton loaders for content
- Loading spinners for data fetching
- Error boundaries for error handling

### SEO Considerations
- Proper meta tags for each page
- Open Graph tags for social sharing
- Structured data where applicable

## Navigation Flow

```
Home (/) 
├── Advanced (/advanced) - Main trading interface
├── Community (/community) - Social features
├── How it Works (/how-it-works) - Education
└── Support (/support) - Help resources
```

## Data Requirements

### Home Page
- Token list with prices
- Market data
- Featured tokens

### Advanced Page
- Real-time price data
- Chart data for multiple timeframes
- Order book data
- User portfolio data

### Community Page
- Community token selections
- User activity data
- Social metrics

### How it Works Page
- Static content
- Process steps
- FAQ data

### Support Page
- FAQ content
- Contact form handling
- Support resources

## Implementation Priority

1. **Phase 1**: Home page (core functionality)
2. **Phase 2**: Advanced page (trading interface)
3. **Phase 3**: How it Works page (static content)
4. **Phase 4**: Support page (help resources)
5. **Phase 5**: Community page (social features)

Each page should be built with proper TypeScript interfaces, error handling, and responsive design following the retro aesthetic established in the design system.
