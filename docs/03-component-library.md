# Component Library - Wildcard Crypto Trading App

## Overview
This document outlines all the reusable components needed to build the Wildcard app based on the Figma design.

## Core UI Components

### 1. TokenCard Component
**Purpose**: Display individual cryptocurrency tokens with profile images and basic info
**Location**: `components/trading/TokenCard.tsx`

```typescript
interface TokenCardProps {
  id: string;
  name: string;
  symbol: string;
  image: string;
  price: number;
  change24h: number;
  marketCap?: number;
  onClick?: () => void;
}
```

**Features**:
- Profile image with fallback
- Token name and symbol
- Current price (monospace font)
- 24h change with color coding (green/red)
- Hover effects with glow
- Click handler for navigation

### 2. TradingChart Component
**Purpose**: Display price charts with candlestick/line views
**Location**: `components/charts/TradingChart.tsx`

```typescript
interface TradingChartProps {
  data: ChartDataPoint[];
  type: 'candlestick' | 'line' | 'area';
  height?: number;
  showVolume?: boolean;
  timeframe: '1h' | '4h' | '1d' | '1w';
}
```

**Features**:
- Multiple chart types
- Interactive tooltips
- Time range selector
- Volume bars (optional)
- Retro green/red color scheme

### 3. DataTable Component
**Purpose**: Display trading data in tabular format
**Location**: `components/common/DataTable.tsx`

```typescript
interface DataTableProps {
  columns: ColumnDef[];
  data: any[];
  sortable?: boolean;
  pagination?: boolean;
  className?: string;
}
```

**Features**:
- Sortable columns
- Pagination
- Row hover effects
- Responsive design
- Custom cell renderers

### 4. RetroButton Component
**Purpose**: Styled buttons matching the retro theme
**Location**: `components/ui/RetroButton.tsx`

```typescript
interface RetroButtonProps {
  variant: 'primary' | 'secondary' | 'ghost' | 'danger';
  size: 'sm' | 'md' | 'lg';
  glow?: boolean;
  loading?: boolean;
  children: React.ReactNode;
  onClick?: () => void;
}
```

**Variants**:
- Primary: Neon green background
- Secondary: Transparent with neon border
- Ghost: No background, text only
- Danger: Red accent for destructive actions

### 5. GlowCard Component
**Purpose**: Container with retro glow effects
**Location**: `components/ui/GlowCard.tsx`

```typescript
interface GlowCardProps {
  children: React.ReactNode;
  glowColor?: 'green' | 'blue' | 'purple' | 'pink';
  intensity?: 'low' | 'medium' | 'high';
  className?: string;
}
```

**Features**:
- Customizable glow colors
- Intensity levels
- Hover animations
- Dark background with borders

### 6. PriceDisplay Component
**Purpose**: Format and display cryptocurrency prices
**Location**: `components/trading/PriceDisplay.tsx`

```typescript
interface PriceDisplayProps {
  value: number;
  currency?: string;
  change?: number;
  showChange?: boolean;
  size?: 'sm' | 'md' | 'lg' | 'xl';
}
```

**Features**:
- Monospace font for numbers
- Color-coded changes
- Currency formatting
- Multiple sizes

### 7. StepIndicator Component
**Purpose**: Show progress steps (for "How it Works" page)
**Location**: `components/common/StepIndicator.tsx`

```typescript
interface StepIndicatorProps {
  steps: Step[];
  currentStep?: number;
  orientation?: 'horizontal' | 'vertical';
}

interface Step {
  id: string;
  title: string;
  description: string;
  icon?: React.ReactNode;
}
```

**Features**:
- Connected step indicators
- Active/completed states
- Icons for each step
- Responsive layout

## Layout Components

### 8. Navigation Component
**Purpose**: Top navigation bar with logo and menu items
**Location**: `components/layout/Navigation.tsx`

```typescript
interface NavigationProps {
  currentPage?: string;
}
```

**Features**:
- Logo (SVG) that links to home
- Menu items: Advanced, Community, How it Works, Support
- Active state indicators
- Responsive mobile menu
- Retro styling with glow effects

### 9. PageLayout Component
**Purpose**: Consistent page wrapper with navigation
**Location**: `components/layout/PageLayout.tsx`

```typescript
interface PageLayoutProps {
  children: React.ReactNode;
  title?: string;
  description?: string;
  className?: string;
}
```

**Features**:
- Navigation integration
- Page title and meta
- Consistent spacing
- Dark background

### 10. GridLayout Component
**Purpose**: Responsive grid for token cards
**Location**: `components/layout/GridLayout.tsx`

```typescript
interface GridLayoutProps {
  children: React.ReactNode;
  columns?: number;
  gap?: number;
  className?: string;
}
```

**Features**:
- Responsive columns
- Customizable gaps
- Auto-fit behavior

## Specialized Components

### 11. TradingInterface Component
**Purpose**: Complete trading UI with buy/sell forms
**Location**: `components/trading/TradingInterface.tsx`

```typescript
interface TradingInterfaceProps {
  tokenId: string;
  onTrade?: (type: 'buy' | 'sell', amount: number) => void;
}
```

**Features**:
- Buy/sell toggle
- Amount input with validation
- Price calculation
- Order confirmation
- Real-time updates

### 12. TokenGrid Component
**Purpose**: Grid of token cards with filtering/sorting
**Location**: `components/trading/TokenGrid.tsx`

```typescript
interface TokenGridProps {
  tokens: Token[];
  onTokenSelect?: (token: Token) => void;
  filters?: FilterOptions;
  sortBy?: SortOption;
}
```

**Features**:
- Search functionality
- Category filters
- Sort options
- Infinite scroll or pagination

### 13. ChartContainer Component
**Purpose**: Wrapper for charts with controls
**Location**: `components/charts/ChartContainer.tsx`

```typescript
interface ChartContainerProps {
  children: React.ReactNode;
  title?: string;
  timeframes?: string[];
  onTimeframeChange?: (timeframe: string) => void;
}
```

**Features**:
- Chart title
- Timeframe selector
- Fullscreen toggle
- Loading states

## Utility Components

### 14. LoadingSpinner Component
**Purpose**: Retro-styled loading indicator
**Location**: `components/ui/LoadingSpinner.tsx`

### 15. Modal Component
**Purpose**: Overlay modals with retro styling
**Location**: `components/ui/Modal.tsx`

### 16. Tooltip Component
**Purpose**: Hover tooltips with glow effects
**Location**: `components/ui/Tooltip.tsx`

### 17. Badge Component
**Purpose**: Status badges and labels
**Location**: `components/ui/Badge.tsx`

## Component Dependencies

### Required shadcn/ui components:
```bash
npx shadcn-ui@latest add button
npx shadcn-ui@latest add card
npx shadcn-ui@latest add dialog
npx shadcn-ui@latest add table
npx shadcn-ui@latest add input
npx shadcn-ui@latest add badge
npx shadcn-ui@latest add tooltip
npx shadcn-ui@latest add tabs
npx shadcn-ui@latest add select
```

### Additional libraries:
- `recharts` - For chart components
- `framer-motion` - For animations
- `lucide-react` - For icons
- `@tanstack/react-table` - For data tables

## Implementation Priority

1. **Phase 1**: Core UI (RetroButton, GlowCard, Navigation)
2. **Phase 2**: Layout components (PageLayout, GridLayout)
3. **Phase 3**: Trading components (TokenCard, PriceDisplay)
4. **Phase 4**: Charts and data (TradingChart, DataTable)
5. **Phase 5**: Specialized features (TradingInterface, StepIndicator)

Each component should be built with TypeScript, include proper prop validation, and follow the retro design system established in the previous document.
