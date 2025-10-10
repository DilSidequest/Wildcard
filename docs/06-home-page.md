# Home Page - Wildcard Crypto Trading App

## Overview
The home page serves as the main landing page and token discovery interface. Based on the Figma design, it features a hero section and a comprehensive grid of cryptocurrency tokens.

## Page Structure

### File Location
`app/page.tsx`

### Layout Breakdown
```
┌─────────────────────────────────────────────────────┐
│                  Navigation                         │
├─────────────────────────────────────────────────────┤
│                                                     │
│                 Hero Section                        │
│            [Wildcard Logo/Branding]                 │
│               [Tagline/CTA]                         │
│                                                     │
├─────────────────────────────────────────────────────┤
│                                                     │
│                 Token Grid                          │
│   [Token] [Token] [Token] [Token] [Token]          │
│   [Token] [Token] [Token] [Token] [Token]          │
│   [Token] [Token] [Token] [Token] [Token]          │
│   [Token] [Token] [Token] [Token] [Token]          │
│                                                     │
└─────────────────────────────────────────────────────┘
```

## Hero Section

### Design Specifications
- **Background**: Dark with subtle gradient
- **Logo**: Large Wildcard SVG logo (provided separately)
- **Typography**: Large heading with neon green accent
- **Animation**: Subtle glow effects and floating animation

### Content Structure
```typescript
interface HeroSectionProps {
  title: string;
  subtitle: string;
  ctaText?: string;
  onCtaClick?: () => void;
}
```

### Hero Implementation
```typescript
const HeroSection = () => {
  return (
    <section className="relative py-20 px-6 text-center">
      {/* Background effects */}
      <div className="absolute inset-0 bg-gradient-to-b from-transparent via-neon-green/5 to-transparent" />
      
      {/* Logo */}
      <div className="mb-8 animate-float">
        <WildcardLogo className="w-32 h-32 mx-auto text-neon-green" />
      </div>
      
      {/* Title */}
      <h1 className="text-6xl font-bold mb-4 neon-text text-neon-green">
        WILDCARD
      </h1>
      
      {/* Subtitle */}
      <p className="text-xl text-text-secondary mb-8 max-w-2xl mx-auto">
        Create, buy, and sell cryptocurrency tokens in one powerful platform
      </p>
      
      {/* CTA Button */}
      <RetroButton 
        variant="primary" 
        size="lg" 
        glow
        onClick={() => router.push('/advanced')}
      >
        Start Trading
      </RetroButton>
    </section>
  );
};
```

## Token Grid Section

### Design Specifications
- **Layout**: Responsive grid (5 columns desktop, 3 tablet, 1 mobile)
- **Cards**: Dark background with neon borders
- **Hover Effects**: Glow animation and lift effect
- **Data**: Real-time token information

### Token Card Structure
Based on the Figma design, each token card includes:
- Profile image (circular)
- Token name and symbol
- Current price (monospace font)
- 24h price change (color-coded)
- Market cap (optional)

### Token Interface
```typescript
interface Token {
  id: string;
  name: string;
  symbol: string;
  image: string;
  currentPrice: number;
  priceChange24h: number;
  marketCap?: number;
  volume24h?: number;
}
```

### TokenCard Component
```typescript
const TokenCard = ({ token, onClick }: TokenCardProps) => {
  const changeColor = token.priceChange24h >= 0 ? 'text-neon-green' : 'text-red-500';
  const changePrefix = token.priceChange24h >= 0 ? '+' : '';
  
  return (
    <GlowCard 
      className="p-6 cursor-pointer hover-lift"
      onClick={() => onClick?.(token)}
      glowColor="green"
      intensity="low"
    >
      {/* Token Image */}
      <div className="flex justify-center mb-4">
        <img 
          src={token.image} 
          alt={token.name}
          className="w-16 h-16 rounded-full border-2 border-border-default"
        />
      </div>
      
      {/* Token Info */}
      <div className="text-center">
        <h3 className="text-lg font-semibold text-white mb-1">
          {token.name}
        </h3>
        <p className="text-text-secondary text-sm mb-3">
          {token.symbol.toUpperCase()}
        </p>
        
        {/* Price */}
        <PriceDisplay 
          value={token.currentPrice}
          size="lg"
          className="mb-2"
        />
        
        {/* 24h Change */}
        <div className={`text-sm font-mono ${changeColor}`}>
          {changePrefix}{token.priceChange24h.toFixed(2)}%
        </div>
      </div>
    </GlowCard>
  );
};
```

### Grid Implementation
```typescript
const TokenGrid = ({ tokens, onTokenSelect }: TokenGridProps) => {
  return (
    <section className="py-16 px-6">
      <div className="max-w-7xl mx-auto">
        {/* Section Header */}
        <div className="text-center mb-12">
          <h2 className="text-4xl font-bold text-white mb-4">
            Available Tokens
          </h2>
          <p className="text-text-secondary text-lg">
            Discover and trade the latest cryptocurrency tokens
          </p>
        </div>
        
        {/* Search and Filters */}
        <div className="mb-8 flex justify-center">
          <SearchInput 
            placeholder="Search tokens..."
            className="max-w-md"
          />
        </div>
        
        {/* Token Grid */}
        <div className="grid grid-cols-1 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5 gap-6">
          {tokens.map((token) => (
            <TokenCard 
              key={token.id}
              token={token}
              onClick={onTokenSelect}
            />
          ))}
        </div>
        
        {/* Load More */}
        <div className="text-center mt-12">
          <RetroButton variant="secondary" size="lg">
            Load More Tokens
          </RetroButton>
        </div>
      </div>
    </section>
  );
};
```

## Page Implementation

### Main Page Component
```typescript
// app/page.tsx
import { HeroSection } from '@/components/home/HeroSection';
import { TokenGrid } from '@/components/home/TokenGrid';
import { useTokens } from '@/hooks/useTokens';

export default function HomePage() {
  const { tokens, loading, error } = useTokens();
  
  const handleTokenSelect = (token: Token) => {
    router.push(`/advanced?token=${token.id}`);
  };
  
  if (loading) return <LoadingSpinner />;
  if (error) return <ErrorMessage error={error} />;
  
  return (
    <div className="min-h-screen bg-dark-bg">
      <HeroSection />
      <TokenGrid 
        tokens={tokens}
        onTokenSelect={handleTokenSelect}
      />
    </div>
  );
}
```

## Interactive Features

### Search Functionality
- Real-time search as user types
- Search by token name or symbol
- Highlight matching results

### Filtering Options
- Filter by market cap
- Filter by price range
- Filter by 24h change
- Sort by various metrics

### Responsive Behavior
- **Desktop (1200px+)**: 5 columns
- **Large Tablet (768px-1199px)**: 3-4 columns
- **Small Tablet (480px-767px)**: 2 columns
- **Mobile (<480px)**: 1 column

## Performance Considerations

### Optimization Strategies
- Virtual scrolling for large token lists
- Image lazy loading
- Debounced search input
- Memoized components
- Efficient re-rendering

### Data Management
- Real-time price updates via WebSocket
- Caching strategy for token data
- Error handling and retry logic
- Loading states for better UX

## Accessibility

### ARIA Labels
- Proper labels for interactive elements
- Screen reader friendly descriptions
- Keyboard navigation support

### Color Contrast
- Ensure sufficient contrast ratios
- Alternative indicators beyond color
- High contrast mode support

## Components to Build

1. **HeroSection.tsx** - Hero area with logo and CTA
2. **TokenGrid.tsx** - Grid container for tokens
3. **TokenCard.tsx** - Individual token display
4. **SearchInput.tsx** - Token search functionality
5. **FilterPanel.tsx** - Filtering and sorting options
6. **LoadingSpinner.tsx** - Loading state indicator

## Assets Required

- Wildcard logo SVG
- Placeholder token images
- Background gradient assets
- Icon set for UI elements

This home page serves as the primary entry point and should provide an excellent first impression while being highly functional for token discovery and navigation to trading features.

## Advanced Trading Page Design Reference

### Design Inspiration: BullX.io Interface
The advanced trading page (`/advanced`) should be designed to closely resemble the **BullX.io** trading interface. BullX.io is a multi-chain DEX trading platform known for its comprehensive and user-friendly trading interface.

### Key BullX.io Interface Elements to Implement

#### Layout Structure
- **Multi-panel layout** with dedicated sections for different trading functions
- **Real-time price charts** with advanced charting capabilities
- **Order book display** showing buy/sell orders
- **Trading panel** for executing trades
- **Token information panel** with detailed metrics
- **Portfolio/positions overview**

#### Core Features from BullX.io
1. **Real-Time Charts**
   - TradingView-style charts with multiple timeframes
   - Technical indicators and drawing tools
   - Price action visualization with candlestick charts

2. **Trading Interface**
   - Buy/Sell order forms
   - Limit order functionality
   - Market order execution
   - Slippage settings
   - Gas fee estimation

3. **Market Data Display**
   - Live price feeds
   - 24h volume and price changes
   - Market cap information
   - Liquidity metrics

4. **Filtering and Search**
   - Advanced token filtering options
   - Search functionality
   - Sorting by various metrics (price, volume, market cap)

5. **User Interface Elements**
   - Dark theme with neon accents (matching Wildcard's retro aesthetic)
   - Responsive grid layouts
   - Hover effects and animations
   - Clear data visualization

### Implementation Notes
- Maintain Wildcard's retro/neon color scheme while adopting BullX.io's layout structure
- Ensure all trading functionality is desktop-optimized
- Integrate with the existing design system components (RetroButton, GlowCard, etc.)
- Follow the same responsive design principles as the home page

### Navigation Integration
The "Start Trading" CTA button on the home page should navigate users to this advanced trading interface:
```typescript
onClick={() => router.push('/advanced')}
```

This advanced page will serve as the primary trading hub, providing users with professional-grade tools and interface similar to BullX.io's proven design.
