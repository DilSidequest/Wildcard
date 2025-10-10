# How It Works Page - Wildcard Crypto Trading App

## Overview
The "How It Works" page provides educational content explaining the process of using the Wildcard platform. Based on the Figma design, it features a step-by-step guide with visual elements and clear explanations.

## Page Structure

### File Location
`app/how-it-works/page.tsx`

### Layout Breakdown
```
┌─────────────────────────────────────────────────────┐
│                  Navigation                         │
├─────────────────────────────────────────────────────┤
│                                                     │
│                 Hero Section                        │
│            [Large Title + Subtitle]                 │
│                                                     │
├─────────────────────────────────────────────────────┤
│                                                     │
│                   Step 1                            │
│         [Icon] [Title] [Description]                │
│                                                     │
├─────────────────────────────────────────────────────┤
│                                                     │
│                   Step 2                            │
│         [Icon] [Title] [Description]                │
│                                                     │
├─────────────────────────────────────────────────────┤
│                                                     │
│                   Step 3                            │
│         [Icon] [Title] [Description]                │
│                                                     │
├─────────────────────────────────────────────────────┤
│                                                     │
│              Call to Action                         │
│            [Get Started Button]                     │
│                                                     │
└─────────────────────────────────────────────────────┘
```

## Hero Section Component

### Design Specifications
- **Background**: Dark with subtle gradient and glow effects
- **Typography**: Large heading with retro styling
- **Animation**: Subtle floating and glow animations
- **Content**: Clear value proposition

### Hero Implementation
```typescript
const HowItWorksHero = () => {
  return (
    <section className="py-20 px-6 text-center relative overflow-hidden">
      {/* Background Effects */}
      <div className="absolute inset-0 bg-gradient-to-b from-transparent via-neon-green/5 to-transparent" />
      <div className="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 w-96 h-96 bg-neon-green/10 rounded-full blur-3xl" />
      
      <div className="relative z-10 max-w-4xl mx-auto">
        {/* Main Title */}
        <h1 className="text-6xl font-bold text-white mb-6 neon-text">
          How It <span className="text-neon-green">Works</span>
        </h1>
        
        {/* Subtitle */}
        <p className="text-xl text-text-secondary mb-8 max-w-2xl mx-auto leading-relaxed">
          Get started with Wildcard in just a few simple steps. 
          Create, trade, and manage cryptocurrency tokens with ease.
        </p>
        
        {/* Visual Element */}
        <div className="mb-12">
          <div className="inline-block p-4 rounded-full bg-neon-green/20 animate-pulse">
            <Zap className="w-16 h-16 text-neon-green" />
          </div>
        </div>
      </div>
    </section>
  );
};
```

## Process Steps Component

### Step Data Structure
```typescript
interface ProcessStep {
  id: number;
  title: string;
  description: string;
  icon: React.ReactNode;
  details: string[];
  image?: string;
  color: 'green' | 'blue' | 'purple' | 'pink';
}

const processSteps: ProcessStep[] = [
  {
    id: 1,
    title: "Connect Your Wallet",
    description: "Link your cryptocurrency wallet to start trading on Wildcard",
    icon: <Wallet className="w-12 h-12" />,
    details: [
      "Support for MetaMask, WalletConnect, and more",
      "Secure connection with industry-standard encryption",
      "No personal information required"
    ],
    color: 'green'
  },
  {
    id: 2,
    title: "Discover Tokens",
    description: "Browse our extensive collection of cryptocurrency tokens",
    icon: <Search className="w-12 h-12" />,
    details: [
      "Real-time price data and market information",
      "Community ratings and trending tokens",
      "Advanced filtering and search options"
    ],
    color: 'blue'
  },
  {
    id: 3,
    title: "Trade with Confidence",
    description: "Buy and sell tokens using our intuitive trading interface",
    icon: <TrendingUp className="w-12 h-12" />,
    details: [
      "Interactive charts and technical analysis",
      "Instant order execution",
      "Portfolio tracking and management"
    ],
    color: 'purple'
  },
  {
    id: 4,
    title: "Track Your Portfolio",
    description: "Monitor your investments and track performance over time",
    icon: <BarChart3 className="w-12 h-12" />,
    details: [
      "Real-time portfolio valuation",
      "Performance analytics and insights",
      "Export data for tax reporting"
    ],
    color: 'pink'
  }
];
```

### Steps Implementation
```typescript
const ProcessSteps = ({ steps }: { steps: ProcessStep[] }) => {
  return (
    <section className="py-16 px-6">
      <div className="max-w-6xl mx-auto">
        <div className="space-y-16">
          {steps.map((step, index) => (
            <div key={step.id} className="relative">
              {/* Step Connector Line */}
              {index < steps.length - 1 && (
                <div className="absolute left-1/2 top-32 w-px h-16 bg-gradient-to-b from-neon-green to-transparent transform -translate-x-1/2 z-0" />
              )}
              
              <div className={`grid grid-cols-1 lg:grid-cols-2 gap-12 items-center ${
                index % 2 === 1 ? 'lg:grid-flow-col-dense' : ''
              }`}>
                {/* Step Content */}
                <div className={`${index % 2 === 1 ? 'lg:col-start-2' : ''}`}>
                  <GlowCard 
                    className="p-8 h-full"
                    glowColor={step.color}
                    intensity="medium"
                  >
                    {/* Step Number */}
                    <div className="flex items-center gap-4 mb-6">
                      <div className={`w-12 h-12 rounded-full flex items-center justify-center font-bold text-black ${
                        step.color === 'green' ? 'bg-neon-green' :
                        step.color === 'blue' ? 'bg-neon-blue' :
                        step.color === 'purple' ? 'bg-neon-purple' :
                        'bg-neon-pink'
                      }`}>
                        {step.id}
                      </div>
                      <h2 className="text-3xl font-bold text-white">
                        {step.title}
                      </h2>
                    </div>
                    
                    {/* Description */}
                    <p className="text-lg text-text-secondary mb-6 leading-relaxed">
                      {step.description}
                    </p>
                    
                    {/* Details List */}
                    <ul className="space-y-3">
                      {step.details.map((detail, detailIndex) => (
                        <li key={detailIndex} className="flex items-start gap-3">
                          <Check className={`w-5 h-5 mt-0.5 flex-shrink-0 ${
                            step.color === 'green' ? 'text-neon-green' :
                            step.color === 'blue' ? 'text-neon-blue' :
                            step.color === 'purple' ? 'text-neon-purple' :
                            'text-neon-pink'
                          }`} />
                          <span className="text-text-secondary">{detail}</span>
                        </li>
                      ))}
                    </ul>
                  </GlowCard>
                </div>
                
                {/* Step Visual */}
                <div className={`${index % 2 === 1 ? 'lg:col-start-1' : ''} flex justify-center`}>
                  <div className={`relative p-8 rounded-2xl ${
                    step.color === 'green' ? 'bg-neon-green/10' :
                    step.color === 'blue' ? 'bg-neon-blue/10' :
                    step.color === 'purple' ? 'bg-neon-purple/10' :
                    'bg-neon-pink/10'
                  }`}>
                    <div className={`${
                      step.color === 'green' ? 'text-neon-green' :
                      step.color === 'blue' ? 'text-neon-blue' :
                      step.color === 'purple' ? 'text-neon-purple' :
                      'text-neon-pink'
                    } animate-float`}>
                      {step.icon}
                    </div>
                    
                    {/* Decorative Elements */}
                    <div className={`absolute -top-2 -right-2 w-4 h-4 rounded-full ${
                      step.color === 'green' ? 'bg-neon-green' :
                      step.color === 'blue' ? 'bg-neon-blue' :
                      step.color === 'purple' ? 'bg-neon-purple' :
                      'bg-neon-pink'
                    } animate-pulse`} />
                    <div className={`absolute -bottom-2 -left-2 w-3 h-3 rounded-full ${
                      step.color === 'green' ? 'bg-neon-green' :
                      step.color === 'blue' ? 'bg-neon-blue' :
                      step.color === 'purple' ? 'bg-neon-purple' :
                      'bg-neon-pink'
                    } animate-pulse`} style={{ animationDelay: '0.5s' }} />
                  </div>
                </div>
              </div>
            </div>
          ))}
        </div>
      </div>
    </section>
  );
};
```

## FAQ Section Component

### FAQ Data Structure
```typescript
interface FAQItem {
  id: string;
  question: string;
  answer: string;
  category: 'getting-started' | 'trading' | 'security' | 'technical';
}

const faqItems: FAQItem[] = [
  {
    id: '1',
    question: "What wallets are supported?",
    answer: "Wildcard supports MetaMask, WalletConnect, Coinbase Wallet, and other popular Web3 wallets.",
    category: 'getting-started'
  },
  {
    id: '2',
    question: "Are there any trading fees?",
    answer: "We charge a small transaction fee for each trade to cover network costs and platform maintenance.",
    category: 'trading'
  },
  {
    id: '3',
    question: "How secure is the platform?",
    answer: "We use industry-standard security measures including encryption, secure connections, and regular security audits.",
    category: 'security'
  }
];
```

### FAQ Implementation
```typescript
const FAQSection = ({ items }: { items: FAQItem[] }) => {
  return (
    <section className="py-16 px-6">
      <div className="max-w-4xl mx-auto">
        <div className="text-center mb-12">
          <h2 className="text-4xl font-bold text-white mb-4">
            Frequently Asked Questions
          </h2>
          <p className="text-text-secondary text-lg">
            Find answers to common questions about using Wildcard
          </p>
        </div>
        
        <GlowCard className="p-8" glowColor="blue" intensity="low">
          <Accordion type="single" collapsible className="space-y-4">
            {items.map((item) => (
              <AccordionItem 
                key={item.id} 
                value={item.id}
                className="border-border-default"
              >
                <AccordionTrigger className="text-left text-white hover:text-neon-blue">
                  {item.question}
                </AccordionTrigger>
                <AccordionContent className="text-text-secondary">
                  {item.answer}
                </AccordionContent>
              </AccordionItem>
            ))}
          </Accordion>
        </GlowCard>
      </div>
    </section>
  );
};
```

## Call to Action Section

### CTA Implementation
```typescript
const CallToActionSection = () => {
  return (
    <section className="py-20 px-6 text-center">
      <div className="max-w-4xl mx-auto">
        <GlowCard className="p-12" glowColor="green" intensity="high">
          <h2 className="text-4xl font-bold text-white mb-6">
            Ready to Get Started?
          </h2>
          <p className="text-xl text-text-secondary mb-8 max-w-2xl mx-auto">
            Join thousands of traders who are already using Wildcard to 
            create and trade cryptocurrency tokens.
          </p>
          
          <div className="flex flex-col sm:flex-row gap-4 justify-center">
            <RetroButton 
              variant="primary" 
              size="lg" 
              glow
              onClick={() => router.push('/advanced')}
            >
              Start Trading Now
            </RetroButton>
            <RetroButton 
              variant="secondary" 
              size="lg"
              onClick={() => router.push('/community')}
            >
              Explore Community
            </RetroButton>
          </div>
        </GlowCard>
      </div>
    </section>
  );
};
```

## Page Implementation

### Main How It Works Page
```typescript
// app/how-it-works/page.tsx
export default function HowItWorksPage() {
  return (
    <div className="min-h-screen bg-dark-bg">
      <HowItWorksHero />
      <ProcessSteps steps={processSteps} />
      <FAQSection items={faqItems} />
      <CallToActionSection />
    </div>
  );
}
```

## Components to Build

1. **HowItWorksHero.tsx** - Hero section with title
2. **ProcessSteps.tsx** - Step-by-step guide
3. **StepCard.tsx** - Individual step component
4. **FAQSection.tsx** - Frequently asked questions
5. **CallToActionSection.tsx** - Final CTA section

## Content Management

### Static Content
- Step descriptions and details
- FAQ questions and answers
- Hero section copy
- CTA messaging

### Dynamic Elements
- Animated icons and effects
- Progressive disclosure of information
- Interactive FAQ accordion
- Smooth scrolling between sections

This "How It Works" page provides clear, educational content that helps users understand the platform while maintaining the retro aesthetic and engaging user experience.
