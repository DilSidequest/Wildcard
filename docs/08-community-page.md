# Community Page - Wildcard Crypto Trading App

## Overview
The Community page showcases community-driven features, token discovery, and social trading elements. It provides a platform for users to discover trending tokens and engage with the trading community.

## Page Structure

### File Location
`app/community/page.tsx`

### Layout Breakdown
```
┌─────────────────────────────────────────────────────┐
│                  Navigation                         │
├─────────────────────────────────────────────────────┤
│                                                     │
│               Community Header                      │
│          [Title + Community Stats]                  │
│                                                     │
├─────────────────────────────────────────────────────┤
│                                                     │
│  Featured Tokens (60%)    │  Community Feed (40%)   │
│                           │                         │
│  [Token Grid]             │  [Activity Feed]        │
│  [Trending Tokens]        │  [Recent Trades]        │
│  [Community Picks]        │  [User Activities]      │
│                           │  [Social Elements]      │
│                                                     │
└─────────────────────────────────────────────────────┘
```

## Community Header Component

### Design Specifications
- **Background**: Dark with subtle gradient
- **Content**: Page title, community statistics
- **Stats**: Active users, total trades, featured tokens
- **Styling**: Retro theme with neon accents

### Header Implementation
```typescript
interface CommunityStats {
  activeUsers: number;
  totalTrades: number;
  featuredTokens: number;
  totalVolume: number;
}

const CommunityHeader = ({ stats }: { stats: CommunityStats }) => {
  return (
    <section className="py-16 px-6 text-center">
      <div className="max-w-4xl mx-auto">
        {/* Title */}
        <h1 className="text-5xl font-bold text-white mb-4">
          Community
        </h1>
        <p className="text-xl text-text-secondary mb-12">
          Discover trending tokens and connect with fellow traders
        </p>
        
        {/* Community Stats */}
        <div className="grid grid-cols-2 md:grid-cols-4 gap-6">
          <GlowCard className="p-6" glowColor="green" intensity="low">
            <div className="text-3xl font-bold text-neon-green mb-2">
              {formatNumber(stats.activeUsers)}
            </div>
            <div className="text-text-secondary">Active Users</div>
          </GlowCard>
          
          <GlowCard className="p-6" glowColor="blue" intensity="low">
            <div className="text-3xl font-bold text-neon-blue mb-2">
              {formatNumber(stats.totalTrades)}
            </div>
            <div className="text-text-secondary">Total Trades</div>
          </GlowCard>
          
          <GlowCard className="p-6" glowColor="purple" intensity="low">
            <div className="text-3xl font-bold text-neon-purple mb-2">
              {stats.featuredTokens}
            </div>
            <div className="text-text-secondary">Featured Tokens</div>
          </GlowCard>
          
          <GlowCard className="p-6" glowColor="pink" intensity="low">
            <div className="text-3xl font-bold text-neon-pink mb-2">
              ${formatNumber(stats.totalVolume)}
            </div>
            <div className="text-text-secondary">24h Volume</div>
          </GlowCard>
        </div>
      </div>
    </section>
  );
};
```

## Featured Tokens Section

### Design Specifications
- **Layout**: Multiple sections (Trending, Community Picks, New Listings)
- **Cards**: Enhanced token cards with community metrics
- **Features**: Voting, favorites, community ratings

### Token Categories
```typescript
interface CommunityToken extends Token {
  communityRating: number;
  votes: number;
  isFavorited: boolean;
  trendingScore: number;
  communityPick: boolean;
}

interface FeaturedTokensProps {
  trendingTokens: CommunityToken[];
  communityPicks: CommunityToken[];
  newListings: CommunityToken[];
  onTokenSelect: (token: CommunityToken) => void;
  onVote: (tokenId: string, vote: 'up' | 'down') => void;
  onFavorite: (tokenId: string) => void;
}
```

### Featured Tokens Implementation
```typescript
const FeaturedTokens = ({ 
  trendingTokens, 
  communityPicks, 
  newListings,
  onTokenSelect,
  onVote,
  onFavorite 
}: FeaturedTokensProps) => {
  return (
    <div className="space-y-12">
      {/* Trending Tokens */}
      <div>
        <div className="flex items-center justify-between mb-6">
          <h2 className="text-2xl font-bold text-white flex items-center gap-2">
            <TrendingUp className="w-6 h-6 text-neon-green" />
            Trending Now
          </h2>
          <Badge variant="secondary" className="text-neon-green">
            🔥 Hot
          </Badge>
        </div>
        
        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
          {trendingTokens.map((token) => (
            <CommunityTokenCard
              key={token.id}
              token={token}
              onClick={() => onTokenSelect(token)}
              onVote={onVote}
              onFavorite={onFavorite}
              showTrending
            />
          ))}
        </div>
      </div>
      
      {/* Community Picks */}
      <div>
        <div className="flex items-center justify-between mb-6">
          <h2 className="text-2xl font-bold text-white flex items-center gap-2">
            <Users className="w-6 h-6 text-neon-blue" />
            Community Picks
          </h2>
          <Badge variant="secondary" className="text-neon-blue">
            👥 Voted
          </Badge>
        </div>
        
        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
          {communityPicks.map((token) => (
            <CommunityTokenCard
              key={token.id}
              token={token}
              onClick={() => onTokenSelect(token)}
              onVote={onVote}
              onFavorite={onFavorite}
              showRating
            />
          ))}
        </div>
      </div>
      
      {/* New Listings */}
      <div>
        <div className="flex items-center justify-between mb-6">
          <h2 className="text-2xl font-bold text-white flex items-center gap-2">
            <Sparkles className="w-6 h-6 text-neon-purple" />
            New Listings
          </h2>
          <Badge variant="secondary" className="text-neon-purple">
            ✨ New
          </Badge>
        </div>
        
        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
          {newListings.map((token) => (
            <CommunityTokenCard
              key={token.id}
              token={token}
              onClick={() => onTokenSelect(token)}
              onVote={onVote}
              onFavorite={onFavorite}
              showNew
            />
          ))}
        </div>
      </div>
    </div>
  );
};
```

## Community Token Card Component

### Enhanced Token Card
```typescript
const CommunityTokenCard = ({ 
  token, 
  onClick, 
  onVote, 
  onFavorite,
  showTrending,
  showRating,
  showNew 
}: CommunityTokenCardProps) => {
  return (
    <GlowCard 
      className="p-4 cursor-pointer hover-lift relative"
      onClick={() => onClick(token)}
      glowColor="green"
      intensity="low"
    >
      {/* Badges */}
      <div className="absolute top-2 right-2 flex gap-1">
        {showTrending && (
          <Badge className="bg-neon-green text-black text-xs">
            🔥 #{token.trendingScore}
          </Badge>
        )}
        {showNew && (
          <Badge className="bg-neon-purple text-white text-xs">
            ✨ New
          </Badge>
        )}
      </div>
      
      {/* Token Image */}
      <div className="flex justify-center mb-3">
        <img 
          src={token.image} 
          alt={token.name}
          className="w-12 h-12 rounded-full border-2 border-border-default"
        />
      </div>
      
      {/* Token Info */}
      <div className="text-center mb-3">
        <h3 className="text-lg font-semibold text-white mb-1">
          {token.name}
        </h3>
        <p className="text-text-secondary text-sm mb-2">
          {token.symbol.toUpperCase()}
        </p>
        
        <PriceDisplay 
          value={token.currentPrice}
          change={token.priceChange24h}
          showChange
          size="md"
        />
      </div>
      
      {/* Community Features */}
      <div className="border-t border-border-default pt-3">
        {showRating && (
          <div className="flex items-center justify-center gap-2 mb-2">
            <div className="flex">
              {[1, 2, 3, 4, 5].map((star) => (
                <Star
                  key={star}
                  className={`w-4 h-4 ${
                    star <= token.communityRating
                      ? 'text-neon-green fill-current'
                      : 'text-gray-600'
                  }`}
                />
              ))}
            </div>
            <span className="text-sm text-text-secondary">
              ({token.votes})
            </span>
          </div>
        )}
        
        {/* Action Buttons */}
        <div className="flex justify-between items-center">
          <div className="flex gap-1">
            <button
              onClick={(e) => {
                e.stopPropagation();
                onVote(token.id, 'up');
              }}
              className="p-1 rounded hover:bg-neon-green/20 transition-colors"
            >
              <ChevronUp className="w-4 h-4 text-neon-green" />
            </button>
            <button
              onClick={(e) => {
                e.stopPropagation();
                onVote(token.id, 'down');
              }}
              className="p-1 rounded hover:bg-red-500/20 transition-colors"
            >
              <ChevronDown className="w-4 h-4 text-red-500" />
            </button>
          </div>
          
          <button
            onClick={(e) => {
              e.stopPropagation();
              onFavorite(token.id);
            }}
            className="p-1 rounded hover:bg-neon-pink/20 transition-colors"
          >
            <Heart 
              className={`w-4 h-4 ${
                token.isFavorited 
                  ? 'text-neon-pink fill-current' 
                  : 'text-text-secondary'
              }`} 
            />
          </button>
        </div>
      </div>
    </GlowCard>
  );
};
```

## Community Feed Component

### Activity Feed
```typescript
interface ActivityItem {
  id: string;
  type: 'trade' | 'listing' | 'vote' | 'favorite';
  user: string;
  token: string;
  amount?: number;
  timestamp: Date;
  details: string;
}

const CommunityFeed = ({ activities }: { activities: ActivityItem[] }) => {
  return (
    <GlowCard className="p-6 h-fit sticky top-6" glowColor="blue" intensity="low">
      <h2 className="text-2xl font-bold text-white mb-6">
        Community Activity
      </h2>
      
      <div className="space-y-4 max-h-96 overflow-y-auto">
        {activities.map((activity) => (
          <div key={activity.id} className="flex items-start gap-3 p-3 rounded-lg bg-bg-tertiary">
            <div className="w-8 h-8 rounded-full bg-neon-green/20 flex items-center justify-center">
              {getActivityIcon(activity.type)}
            </div>
            
            <div className="flex-1">
              <div className="text-sm text-white mb-1">
                <span className="font-semibold text-neon-green">
                  {activity.user}
                </span>
                {' '}
                {activity.details}
                {' '}
                <span className="font-semibold text-neon-blue">
                  {activity.token}
                </span>
              </div>
              
              <div className="text-xs text-text-secondary">
                {formatTimeAgo(activity.timestamp)}
              </div>
            </div>
          </div>
        ))}
      </div>
      
      <div className="mt-4 text-center">
        <RetroButton variant="ghost" size="sm">
          View All Activity
        </RetroButton>
      </div>
    </GlowCard>
  );
};
```

## Page Implementation

### Main Community Page
```typescript
// app/community/page.tsx
export default function CommunityPage() {
  const { communityStats } = useCommunityStats();
  const { trendingTokens, communityPicks, newListings } = useCommunityTokens();
  const { activities } = useCommunityActivity();
  
  const handleTokenSelect = (token: CommunityToken) => {
    router.push(`/advanced?token=${token.id}`);
  };
  
  const handleVote = async (tokenId: string, vote: 'up' | 'down') => {
    // Implement voting logic
    console.log(`Vote ${vote} for ${tokenId}`);
  };
  
  const handleFavorite = async (tokenId: string) => {
    // Implement favorite logic
    console.log(`Toggle favorite for ${tokenId}`);
  };
  
  return (
    <div className="min-h-screen bg-dark-bg">
      <CommunityHeader stats={communityStats} />
      
      <div className="max-w-7xl mx-auto px-6 pb-16">
        <div className="grid grid-cols-1 lg:grid-cols-3 gap-8">
          {/* Featured Tokens */}
          <div className="lg:col-span-2">
            <FeaturedTokens
              trendingTokens={trendingTokens}
              communityPicks={communityPicks}
              newListings={newListings}
              onTokenSelect={handleTokenSelect}
              onVote={handleVote}
              onFavorite={handleFavorite}
            />
          </div>
          
          {/* Community Feed */}
          <div className="lg:col-span-1">
            <CommunityFeed activities={activities} />
          </div>
        </div>
      </div>
    </div>
  );
}
```

## Components to Build

1. **CommunityHeader.tsx** - Header with stats
2. **FeaturedTokens.tsx** - Token sections container
3. **CommunityTokenCard.tsx** - Enhanced token card
4. **CommunityFeed.tsx** - Activity feed
5. **VotingSystem.tsx** - Token voting functionality
6. **ActivityItem.tsx** - Individual activity display

## Features to Implement

- Token voting system
- Favorite tokens functionality
- Community ratings
- Activity feed with real-time updates
- Social features (following users, comments)
- Token discovery algorithms

This community page creates an engaging social trading environment while maintaining the retro aesthetic and providing valuable community-driven insights.
