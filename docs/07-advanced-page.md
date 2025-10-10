# Advanced Page - Wildcard Crypto Trading App

## Overview
The Advanced page is the core trading interface of the Wildcard app. Based on the Figma design, it features comprehensive charts, trading panels, and market data tables.

## Page Structure

### File Location
`app/advanced/page.tsx`

### Layout Breakdown
```
┌─────────────────────────────────────────────────────┐
│                  Navigation                         │
├─────────────────────────────────────────────────────┤
│                                                     │
│  Chart Area (70%)          │  Trading Panel (30%)   │
│                            │                        │
│  [Interactive Chart]       │  [Buy/Sell Toggle]     │
│  [Timeframe Controls]      │  [Amount Input]        │
│  [Chart Type Toggle]       │  [Price Display]       │
│                            │  [Order Button]        │
│                            │  [Portfolio Summary]   │
├────────────────────────────┴────────────────────────┤
│                                                     │
│                 Market Data Table                   │
│  [Token] [Price] [Change] [Volume] [Market Cap]     │
│                                                     │
└─────────────────────────────────────────────────────┘
```

## Chart Area Component

### Design Specifications
- **Size**: 70% of viewport width on desktop
- **Chart Types**: Candlestick, Line, Area
- **Timeframes**: 1h, 4h, 1d, 1w, 1m
- **Features**: Interactive tooltips, zoom, pan
- **Colors**: Retro green/red theme

### Chart Interface
```typescript
interface ChartData {
  timestamp: number;
  open: number;
  high: number;
  low: number;
  close: number;
  volume: number;
}

interface ChartAreaProps {
  tokenId: string;
  data: ChartData[];
  timeframe: string;
  chartType: 'candlestick' | 'line' | 'area';
  onTimeframeChange: (timeframe: string) => void;
  onChartTypeChange: (type: string) => void;
}
```

### Chart Implementation
```typescript
const ChartArea = ({ tokenId, data, timeframe, chartType }: ChartAreaProps) => {
  return (
    <GlowCard className="h-full p-6" glowColor="blue" intensity="low">
      {/* Chart Header */}
      <div className="flex justify-between items-center mb-6">
        <div>
          <h2 className="text-2xl font-bold text-white">
            {tokenId.toUpperCase()}/USD
          </h2>
          <PriceDisplay 
            value={data[data.length - 1]?.close || 0}
            change={calculateChange(data)}
            showChange
            size="lg"
          />
        </div>
        
        {/* Chart Controls */}
        <div className="flex gap-4">
          {/* Timeframe Selector */}
          <div className="flex gap-2">
            {['1h', '4h', '1d', '1w', '1m'].map((tf) => (
              <button
                key={tf}
                className={`px-3 py-1 rounded text-sm transition-all ${
                  timeframe === tf 
                    ? 'bg-neon-green text-black' 
                    : 'bg-transparent text-text-secondary hover:text-neon-green'
                }`}
                onClick={() => onTimeframeChange(tf)}
              >
                {tf}
              </button>
            ))}
          </div>
          
          {/* Chart Type Selector */}
          <div className="flex gap-2">
            {['candlestick', 'line', 'area'].map((type) => (
              <button
                key={type}
                className={`px-3 py-1 rounded text-sm transition-all ${
                  chartType === type 
                    ? 'bg-neon-blue text-black' 
                    : 'bg-transparent text-text-secondary hover:text-neon-blue'
                }`}
                onClick={() => onChartTypeChange(type)}
              >
                {type}
              </button>
            ))}
          </div>
        </div>
      </div>
      
      {/* Chart Component */}
      <div className="h-96">
        <TradingChart 
          data={data}
          type={chartType}
          height={384}
          showVolume
          timeframe={timeframe}
        />
      </div>
    </GlowCard>
  );
};
```

## Trading Panel Component

### Design Specifications
- **Size**: 30% of viewport width on desktop
- **Features**: Buy/Sell toggle, amount input, order placement
- **Real-time**: Live price updates and calculations
- **Validation**: Input validation and error handling

### Trading Interface
```typescript
interface TradingPanelProps {
  tokenId: string;
  currentPrice: number;
  onTrade: (type: 'buy' | 'sell', amount: number) => void;
}

interface TradeOrder {
  type: 'buy' | 'sell';
  amount: number;
  price: number;
  total: number;
}
```

### Trading Panel Implementation
```typescript
const TradingPanel = ({ tokenId, currentPrice, onTrade }: TradingPanelProps) => {
  const [tradeType, setTradeType] = useState<'buy' | 'sell'>('buy');
  const [amount, setAmount] = useState<string>('');
  const [loading, setLoading] = useState(false);
  
  const total = parseFloat(amount) * currentPrice || 0;
  
  const handleTrade = async () => {
    if (!amount || parseFloat(amount) <= 0) return;
    
    setLoading(true);
    try {
      await onTrade(tradeType, parseFloat(amount));
      setAmount('');
    } catch (error) {
      console.error('Trade failed:', error);
    } finally {
      setLoading(false);
    }
  };
  
  return (
    <GlowCard className="h-full p-6" glowColor="green" intensity="medium">
      {/* Trade Type Toggle */}
      <div className="mb-6">
        <div className="flex rounded-lg bg-bg-tertiary p-1">
          <button
            className={`flex-1 py-2 px-4 rounded-md transition-all ${
              tradeType === 'buy'
                ? 'bg-neon-green text-black font-semibold'
                : 'text-text-secondary hover:text-white'
            }`}
            onClick={() => setTradeType('buy')}
          >
            Buy
          </button>
          <button
            className={`flex-1 py-2 px-4 rounded-md transition-all ${
              tradeType === 'sell'
                ? 'bg-red-500 text-white font-semibold'
                : 'text-text-secondary hover:text-white'
            }`}
            onClick={() => setTradeType('sell')}
          >
            Sell
          </button>
        </div>
      </div>
      
      {/* Current Price */}
      <div className="mb-6">
        <label className="block text-text-secondary text-sm mb-2">
          Current Price
        </label>
        <PriceDisplay 
          value={currentPrice}
          size="lg"
          className="text-neon-blue"
        />
      </div>
      
      {/* Amount Input */}
      <div className="mb-6">
        <label className="block text-text-secondary text-sm mb-2">
          Amount ({tokenId.toUpperCase()})
        </label>
        <input
          type="number"
          value={amount}
          onChange={(e) => setAmount(e.target.value)}
          placeholder="0.00"
          className="input-retro w-full"
          min="0"
          step="0.01"
        />
      </div>
      
      {/* Total Calculation */}
      <div className="mb-6">
        <label className="block text-text-secondary text-sm mb-2">
          Total (USD)
        </label>
        <div className="text-2xl font-mono text-white">
          ${total.toFixed(2)}
        </div>
      </div>
      
      {/* Order Button */}
      <RetroButton
        variant="primary"
        size="lg"
        className="w-full mb-6"
        onClick={handleTrade}
        loading={loading}
        disabled={!amount || parseFloat(amount) <= 0}
      >
        {tradeType === 'buy' ? 'Buy' : 'Sell'} {tokenId.toUpperCase()}
      </RetroButton>
      
      {/* Portfolio Summary */}
      <div className="border-t border-border-default pt-6">
        <h3 className="text-lg font-semibold text-white mb-4">
          Portfolio
        </h3>
        <PortfolioSummary />
      </div>
    </GlowCard>
  );
};
```

## Market Data Table Component

### Design Specifications
- **Full Width**: Spans entire bottom section
- **Columns**: Token, Price, 24h Change, Volume, Market Cap
- **Features**: Sortable, searchable, paginated
- **Styling**: Retro table with hover effects

### Table Interface
```typescript
interface MarketData {
  id: string;
  name: string;
  symbol: string;
  image: string;
  currentPrice: number;
  priceChange24h: number;
  volume24h: number;
  marketCap: number;
}
```

### Market Table Implementation
```typescript
const MarketDataTable = ({ data, onTokenSelect }: MarketDataTableProps) => {
  const [sortBy, setSortBy] = useState<string>('marketCap');
  const [sortOrder, setSortOrder] = useState<'asc' | 'desc'>('desc');
  
  const columns = [
    {
      key: 'name',
      label: 'Token',
      render: (item: MarketData) => (
        <div className="flex items-center gap-3">
          <img 
            src={item.image} 
            alt={item.name}
            className="w-8 h-8 rounded-full"
          />
          <div>
            <div className="font-semibold text-white">{item.name}</div>
            <div className="text-text-secondary text-sm">{item.symbol.toUpperCase()}</div>
          </div>
        </div>
      )
    },
    {
      key: 'currentPrice',
      label: 'Price',
      render: (item: MarketData) => (
        <PriceDisplay value={item.currentPrice} />
      )
    },
    {
      key: 'priceChange24h',
      label: '24h Change',
      render: (item: MarketData) => (
        <div className={`font-mono ${
          item.priceChange24h >= 0 ? 'text-neon-green' : 'text-red-500'
        }`}>
          {item.priceChange24h >= 0 ? '+' : ''}{item.priceChange24h.toFixed(2)}%
        </div>
      )
    },
    {
      key: 'volume24h',
      label: 'Volume',
      render: (item: MarketData) => (
        <div className="font-mono text-text-secondary">
          ${formatNumber(item.volume24h)}
        </div>
      )
    },
    {
      key: 'marketCap',
      label: 'Market Cap',
      render: (item: MarketData) => (
        <div className="font-mono text-text-secondary">
          ${formatNumber(item.marketCap)}
        </div>
      )
    }
  ];
  
  return (
    <GlowCard className="p-6" glowColor="purple" intensity="low">
      <div className="mb-6">
        <h2 className="text-2xl font-bold text-white">Market Data</h2>
      </div>
      
      <DataTable
        columns={columns}
        data={data}
        sortable
        onRowClick={onTokenSelect}
        className="retro-table"
      />
    </GlowCard>
  );
};
```

## Page Implementation

### Main Advanced Page
```typescript
// app/advanced/page.tsx
export default function AdvancedPage() {
  const [selectedToken, setSelectedToken] = useState('BTC');
  const [timeframe, setTimeframe] = useState('1d');
  const [chartType, setChartType] = useState<'candlestick' | 'line' | 'area'>('candlestick');
  
  const { chartData, loading: chartLoading } = useChartData(selectedToken, timeframe);
  const { marketData, loading: marketLoading } = useMarketData();
  const currentPrice = chartData[chartData.length - 1]?.close || 0;
  
  const handleTrade = async (type: 'buy' | 'sell', amount: number) => {
    // Implement trade logic
    console.log(`${type} ${amount} ${selectedToken}`);
  };
  
  return (
    <div className="min-h-screen bg-dark-bg p-6">
      <div className="max-w-7xl mx-auto">
        {/* Main Trading Interface */}
        <div className="grid grid-cols-1 lg:grid-cols-10 gap-6 mb-6">
          {/* Chart Area */}
          <div className="lg:col-span-7">
            <ChartArea
              tokenId={selectedToken}
              data={chartData}
              timeframe={timeframe}
              chartType={chartType}
              onTimeframeChange={setTimeframe}
              onChartTypeChange={setChartType}
            />
          </div>
          
          {/* Trading Panel */}
          <div className="lg:col-span-3">
            <TradingPanel
              tokenId={selectedToken}
              currentPrice={currentPrice}
              onTrade={handleTrade}
            />
          </div>
        </div>
        
        {/* Market Data Table */}
        <MarketDataTable
          data={marketData}
          onTokenSelect={(token) => setSelectedToken(token.symbol)}
        />
      </div>
    </div>
  );
}
```

## Components to Build

1. **ChartArea.tsx** - Chart container with controls
2. **TradingChart.tsx** - Interactive price chart
3. **TradingPanel.tsx** - Buy/sell interface
4. **MarketDataTable.tsx** - Market data display
5. **PortfolioSummary.tsx** - User portfolio overview
6. **PriceDisplay.tsx** - Formatted price component

## Required Libraries

- `recharts` or `lightweight-charts` for charting
- `@tanstack/react-table` for data tables
- Real-time data connection (WebSocket)
- Number formatting utilities

This advanced page provides comprehensive trading functionality while maintaining the retro aesthetic and user experience outlined in the Figma design.
