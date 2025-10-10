# Assets Requirements - Wildcard Crypto Trading App

## Overview
This document outlines all the visual assets, SVGs, images, and icons required to build the Wildcard crypto trading app frontend based on the Figma design.

## Logo and Branding Assets

### Primary Logo
- **File**: `wildcard-logo.svg`
- **Usage**: Navigation bar, hero section, favicon
- **Variants Needed**:
  - Full logo with text
  - Icon-only version
  - Monochrome version
  - Different sizes (16x16, 32x32, 64x64, 128x128, 256x256)
- **Colors**: Neon green (#00ff41) with retro styling
- **Format**: SVG (scalable), PNG fallbacks

### Favicon Set
- **Files**: 
  - `favicon.ico` (16x16, 32x32)
  - `favicon-16x16.png`
  - `favicon-32x32.png`
  - `apple-touch-icon.png` (180x180)
  - `android-chrome-192x192.png`
  - `android-chrome-512x512.png`

## Navigation Icons

### Menu Icons (SVG)
- **Home Icon**: House/dashboard symbol
- **Advanced Icon**: Chart/graph symbol
- **Community Icon**: Users/people symbol
- **How It Works Icon**: Question mark or info symbol
- **Support Icon**: Headset or help symbol

### Interactive Icons
- **Search Icon**: Magnifying glass
- **Menu Toggle**: Hamburger menu (mobile)
- **Close Icon**: X symbol
- **Arrow Icons**: Left, right, up, down arrows
- **External Link**: Arrow pointing out

## Trading and Chart Icons

### Chart Controls
- **Timeframe Icons**: Clock symbols for 1h, 4h, 1d, 1w, 1m
- **Chart Type Icons**: 
  - Candlestick chart icon
  - Line chart icon
  - Area chart icon
- **Zoom Icons**: Plus/minus, zoom in/out
- **Fullscreen Icon**: Expand/compress arrows

### Trading Interface
- **Buy Icon**: Plus or upward arrow (green)
- **Sell Icon**: Minus or downward arrow (red)
- **Wallet Icon**: Wallet symbol
- **Portfolio Icon**: Pie chart or briefcase
- **Transaction Icons**: Send/receive arrows

## Token and Cryptocurrency Assets

### Placeholder Token Images
- **Default Token Icon**: Generic coin symbol
- **Popular Cryptocurrencies**: 
  - Bitcoin (BTC) icon
  - Ethereum (ETH) icon
  - Generic altcoin icons
- **Format**: SVG preferred, PNG fallback
- **Size**: 64x64px minimum, scalable

### Status Indicators
- **Price Change Icons**:
  - Green up arrow (positive change)
  - Red down arrow (negative change)
  - Neutral dash (no change)
- **Trending Icons**: Fire, trending up/down
- **New Listing Badge**: "NEW" or star symbol

## UI Component Icons

### Form Elements
- **Input Icons**:
  - Search magnifying glass
  - Email envelope
  - Password eye (show/hide)
  - Calendar for dates
- **Validation Icons**:
  - Check mark (success)
  - X mark (error)
  - Warning triangle
  - Info circle

### Interactive Elements
- **Button Icons**:
  - Loading spinner
  - Success checkmark
  - Error X
  - Arrow for CTAs
- **Card Icons**:
  - Heart (favorite)
  - Star (rating)
  - Share arrow
  - More options (three dots)

## Social and Community Icons

### Community Features
- **Social Icons**:
  - Like/thumbs up
  - Dislike/thumbs down
  - Comment bubble
  - Share arrow
- **User Icons**:
  - User profile circle
  - Users group
  - Crown (admin/featured)
  - Badge/verification

### Activity Feed
- **Activity Type Icons**:
  - Trade completed
  - New listing
  - Price alert
  - Community vote
- **Notification Icons**:
  - Bell
  - Dot indicator
  - Badge with number

## Background and Decorative Assets

### Background Elements
- **Gradient Overlays**: Subtle neon gradients
- **Grid Patterns**: Retro grid backgrounds
- **Glow Effects**: Radial gradients for card glows
- **Noise Textures**: Subtle grain for retro feel

### Decorative Graphics
- **Geometric Shapes**: Retro-style geometric elements
- **Circuit Patterns**: Tech-inspired line patterns
- **Particle Effects**: Dot patterns for backgrounds
- **Border Elements**: Neon-style borders and frames

## Chart and Data Visualization

### Chart Elements
- **Candlestick Graphics**: OHLC bar representations
- **Volume Bars**: Bar chart elements
- **Trend Lines**: Arrow and line graphics
- **Grid Lines**: Chart background grids

### Data Display
- **Progress Bars**: Loading and progress indicators
- **Gauge Charts**: Circular progress indicators
- **Sparklines**: Mini chart graphics
- **Data Points**: Dots and markers for charts

## Loading and State Assets

### Loading States
- **Spinners**: Rotating loading indicators
- **Progress Bars**: Linear progress indicators
- **Skeleton Loaders**: Placeholder shapes
- **Pulse Animations**: Breathing/pulsing effects

### Empty States
- **No Data Icons**: Empty folder, no results
- **Error Icons**: Warning triangles, error symbols
- **Success Icons**: Checkmarks, thumbs up
- **Info Icons**: Information circles, question marks

## File Organization Structure

```
public/
├── images/
│   ├── logo/
│   │   ├── wildcard-logo.svg
│   │   ├── wildcard-icon.svg
│   │   └── wildcard-logo-mono.svg
│   ├── tokens/
│   │   ├── default-token.svg
│   │   ├── btc.svg
│   │   ├── eth.svg
│   │   └── placeholder-tokens/
│   ├── backgrounds/
│   │   ├── hero-gradient.svg
│   │   ├── grid-pattern.svg
│   │   └── noise-texture.png
│   └── decorative/
│       ├── geometric-shapes/
│       ├── circuit-patterns/
│       └── glow-effects/
├── icons/
│   ├── navigation/
│   ├── trading/
│   ├── ui/
│   ├── social/
│   └── status/
└── favicon/
    ├── favicon.ico
    ├── favicon-16x16.png
    ├── favicon-32x32.png
    └── apple-touch-icon.png
```

## Icon Library Integration

### Lucide React Icons
Primary icon library for consistent styling:
```typescript
import { 
  Home, TrendingUp, Users, HelpCircle, Headphones,
  Search, Menu, X, ArrowLeft, ArrowRight,
  Plus, Minus, Wallet, PieChart, Send,
  Heart, Star, Share, MoreHorizontal,
  ThumbsUp, ThumbsDown, MessageCircle,
  Bell, Check, AlertTriangle, Info
} from 'lucide-react';
```

### Custom SVG Icons
For brand-specific and specialized icons:
- Wildcard logo variations
- Cryptocurrency symbols
- Custom chart elements
- Retro-styled decorative elements

## Asset Optimization

### SVG Optimization
- Minimize file sizes
- Remove unnecessary metadata
- Optimize paths and shapes
- Ensure scalability

### Image Formats
- **SVG**: For icons, logos, and scalable graphics
- **PNG**: For complex images with transparency
- **WebP**: For optimized web delivery
- **ICO**: For favicon compatibility

### Performance Considerations
- Lazy loading for non-critical images
- Sprite sheets for frequently used icons
- CDN delivery for static assets
- Proper caching headers

## Accessibility Requirements

### Icon Accessibility
- Alt text for all images
- ARIA labels for interactive icons
- High contrast alternatives
- Screen reader friendly descriptions

### Color Considerations
- Sufficient contrast ratios
- Color-blind friendly alternatives
- High contrast mode support
- Alternative visual indicators

## Asset Creation Guidelines

### Style Consistency
- Maintain retro/cyberpunk aesthetic
- Use consistent stroke weights
- Follow neon color palette
- Ensure scalability across sizes

### Technical Specifications
- SVG viewBox optimization
- Consistent naming conventions
- Proper file organization
- Version control for assets

This comprehensive asset list ensures all visual elements needed for the Wildcard app are properly planned and organized for efficient development and maintenance.
