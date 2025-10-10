# Support Page - Wildcard Crypto Trading App

## Overview
The Support page provides comprehensive help resources, contact options, and troubleshooting guides for users. It features a clean, organized layout with easy access to common solutions and support channels.

## Page Structure

### File Location
`app/support/page.tsx`

### Layout Breakdown
```
┌─────────────────────────────────────────────────────┐
│                  Navigation                         │
├─────────────────────────────────────────────────────┤
│                                                     │
│               Support Header                        │
│          [Title + Quick Actions]                    │
│                                                     │
├─────────────────────────────────────────────────────┤
│                                                     │
│    FAQ Section (60%)      │  Contact Form (40%)     │
│                           │                         │
│  [Search Bar]             │  [Support Form]         │
│  [Category Filters]       │  [Contact Info]         │
│  [Accordion FAQ]          │  [Response Times]       │
│                           │                         │
├─────────────────────────────────────────────────────┤
│                                                     │
│              Additional Resources                   │
│    [Documentation] [Tutorials] [Community]         │
│                                                     │
└─────────────────────────────────────────────────────┘
```

## Support Header Component

### Design Specifications
- **Background**: Dark with subtle gradient
- **Content**: Page title, quick help options
- **Actions**: Search, live chat, emergency contact
- **Styling**: Retro theme with neon accents

### Header Implementation
```typescript
const SupportHeader = () => {
  return (
    <section className="py-16 px-6 text-center">
      <div className="max-w-4xl mx-auto">
        {/* Title */}
        <h1 className="text-5xl font-bold text-white mb-4">
          Support Center
        </h1>
        <p className="text-xl text-text-secondary mb-8">
          Get help with your Wildcard experience. We're here to assist you.
        </p>
        
        {/* Quick Actions */}
        <div className="grid grid-cols-1 md:grid-cols-3 gap-4 mb-8">
          <GlowCard className="p-6 cursor-pointer hover-lift" glowColor="green" intensity="low">
            <MessageCircle className="w-8 h-8 text-neon-green mx-auto mb-3" />
            <h3 className="text-lg font-semibold text-white mb-2">Live Chat</h3>
            <p className="text-text-secondary text-sm">Get instant help from our support team</p>
          </GlowCard>
          
          <GlowCard className="p-6 cursor-pointer hover-lift" glowColor="blue" intensity="low">
            <Mail className="w-8 h-8 text-neon-blue mx-auto mb-3" />
            <h3 className="text-lg font-semibold text-white mb-2">Email Support</h3>
            <p className="text-text-secondary text-sm">Send us a detailed message</p>
          </GlowCard>
          
          <GlowCard className="p-6 cursor-pointer hover-lift" glowColor="purple" intensity="low">
            <Phone className="w-8 h-8 text-neon-purple mx-auto mb-3" />
            <h3 className="text-lg font-semibold text-white mb-2">Emergency</h3>
            <p className="text-text-secondary text-sm">Urgent security or account issues</p>
          </GlowCard>
        </div>
        
        {/* Global Search */}
        <div className="max-w-2xl mx-auto">
          <div className="relative">
            <Search className="absolute left-4 top-1/2 transform -translate-y-1/2 w-5 h-5 text-text-secondary" />
            <input
              type="text"
              placeholder="Search for help articles, guides, and FAQs..."
              className="input-retro w-full pl-12 pr-4 py-4 text-lg"
            />
          </div>
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
  category: 'account' | 'trading' | 'security' | 'technical' | 'billing';
  tags: string[];
  helpful: number;
}

interface FAQCategory {
  id: string;
  name: string;
  icon: React.ReactNode;
  color: 'green' | 'blue' | 'purple' | 'pink';
}

const faqCategories: FAQCategory[] = [
  { id: 'account', name: 'Account', icon: <User />, color: 'green' },
  { id: 'trading', name: 'Trading', icon: <TrendingUp />, color: 'blue' },
  { id: 'security', name: 'Security', icon: <Shield />, color: 'purple' },
  { id: 'technical', name: 'Technical', icon: <Settings />, color: 'pink' },
  { id: 'billing', name: 'Billing', icon: <CreditCard />, color: 'green' }
];

const faqItems: FAQItem[] = [
  {
    id: '1',
    question: "How do I connect my wallet to Wildcard?",
    answer: "To connect your wallet, click the 'Connect Wallet' button in the top right corner and select your preferred wallet provider (MetaMask, WalletConnect, etc.). Follow the prompts to authorize the connection.",
    category: 'account',
    tags: ['wallet', 'connection', 'setup'],
    helpful: 45
  },
  {
    id: '2',
    question: "What are the trading fees on Wildcard?",
    answer: "Wildcard charges a 0.25% trading fee on each transaction. This fee covers network costs and platform maintenance. There are no hidden fees or additional charges.",
    category: 'trading',
    tags: ['fees', 'trading', 'costs'],
    helpful: 32
  },
  // Add more FAQ items...
];
```

### FAQ Implementation
```typescript
const FAQSection = ({ items, categories }: FAQSectionProps) => {
  const [selectedCategory, setSelectedCategory] = useState<string>('all');
  const [searchTerm, setSearchTerm] = useState<string>('');
  
  const filteredItems = items.filter(item => {
    const matchesCategory = selectedCategory === 'all' || item.category === selectedCategory;
    const matchesSearch = item.question.toLowerCase().includes(searchTerm.toLowerCase()) ||
                         item.answer.toLowerCase().includes(searchTerm.toLowerCase()) ||
                         item.tags.some(tag => tag.toLowerCase().includes(searchTerm.toLowerCase()));
    return matchesCategory && matchesSearch;
  });
  
  return (
    <div className="space-y-6">
      {/* Category Filters */}
      <div className="flex flex-wrap gap-3">
        <button
          onClick={() => setSelectedCategory('all')}
          className={`px-4 py-2 rounded-lg transition-all ${
            selectedCategory === 'all'
              ? 'bg-neon-green text-black font-semibold'
              : 'bg-bg-tertiary text-text-secondary hover:text-white'
          }`}
        >
          All Categories
        </button>
        {categories.map((category) => (
          <button
            key={category.id}
            onClick={() => setSelectedCategory(category.id)}
            className={`px-4 py-2 rounded-lg transition-all flex items-center gap-2 ${
              selectedCategory === category.id
                ? `bg-neon-${category.color} text-black font-semibold`
                : 'bg-bg-tertiary text-text-secondary hover:text-white'
            }`}
          >
            <span className="w-4 h-4">{category.icon}</span>
            {category.name}
          </button>
        ))}
      </div>
      
      {/* Search within FAQ */}
      <div className="relative">
        <Search className="absolute left-3 top-1/2 transform -translate-y-1/2 w-4 h-4 text-text-secondary" />
        <input
          type="text"
          placeholder="Search FAQ..."
          value={searchTerm}
          onChange={(e) => setSearchTerm(e.target.value)}
          className="input-retro w-full pl-10 pr-4"
        />
      </div>
      
      {/* FAQ Accordion */}
      <GlowCard className="p-6" glowColor="blue" intensity="low">
        <Accordion type="single" collapsible className="space-y-4">
          {filteredItems.map((item) => (
            <AccordionItem 
              key={item.id} 
              value={item.id}
              className="border-border-default"
            >
              <AccordionTrigger className="text-left text-white hover:text-neon-blue">
                <div className="flex items-start justify-between w-full pr-4">
                  <span>{item.question}</span>
                  <div className="flex items-center gap-2 text-sm text-text-secondary">
                    <ThumbsUp className="w-4 h-4" />
                    <span>{item.helpful}</span>
                  </div>
                </div>
              </AccordionTrigger>
              <AccordionContent className="text-text-secondary">
                <div className="space-y-4">
                  <p>{item.answer}</p>
                  
                  {/* Tags */}
                  <div className="flex flex-wrap gap-2">
                    {item.tags.map((tag) => (
                      <Badge key={tag} variant="secondary" className="text-xs">
                        {tag}
                      </Badge>
                    ))}
                  </div>
                  
                  {/* Helpful Actions */}
                  <div className="flex items-center gap-4 pt-2 border-t border-border-default">
                    <span className="text-sm text-text-secondary">Was this helpful?</span>
                    <button className="flex items-center gap-1 text-neon-green hover:text-neon-green/80">
                      <ThumbsUp className="w-4 h-4" />
                      <span className="text-sm">Yes</span>
                    </button>
                    <button className="flex items-center gap-1 text-text-secondary hover:text-red-500">
                      <ThumbsDown className="w-4 h-4" />
                      <span className="text-sm">No</span>
                    </button>
                  </div>
                </div>
              </AccordionContent>
            </AccordionItem>
          ))}
        </Accordion>
        
        {filteredItems.length === 0 && (
          <div className="text-center py-8">
            <AlertCircle className="w-12 h-12 text-text-secondary mx-auto mb-4" />
            <p className="text-text-secondary">No FAQ items found matching your search.</p>
          </div>
        )}
      </GlowCard>
    </div>
  );
};
```

## Contact Form Component

### Form Implementation
```typescript
interface ContactFormData {
  name: string;
  email: string;
  category: string;
  priority: 'low' | 'medium' | 'high' | 'urgent';
  subject: string;
  message: string;
  attachments?: File[];
}

const ContactForm = () => {
  const [formData, setFormData] = useState<ContactFormData>({
    name: '',
    email: '',
    category: 'general',
    priority: 'medium',
    subject: '',
    message: ''
  });
  const [loading, setLoading] = useState(false);
  const [submitted, setSubmitted] = useState(false);
  
  const handleSubmit = async (e: React.FormEvent) => {
    e.preventDefault();
    setLoading(true);
    
    try {
      // Submit form logic
      await submitSupportTicket(formData);
      setSubmitted(true);
    } catch (error) {
      console.error('Failed to submit support ticket:', error);
    } finally {
      setLoading(false);
    }
  };
  
  if (submitted) {
    return (
      <GlowCard className="p-8 text-center" glowColor="green" intensity="medium">
        <CheckCircle className="w-16 h-16 text-neon-green mx-auto mb-4" />
        <h3 className="text-2xl font-bold text-white mb-4">Ticket Submitted!</h3>
        <p className="text-text-secondary mb-6">
          We've received your support request and will respond within 24 hours.
        </p>
        <p className="text-sm text-text-secondary">
          Ticket ID: <span className="text-neon-green font-mono">#WC-{Date.now()}</span>
        </p>
      </GlowCard>
    );
  }
  
  return (
    <GlowCard className="p-8" glowColor="purple" intensity="low">
      <h2 className="text-2xl font-bold text-white mb-6">Contact Support</h2>
      
      <form onSubmit={handleSubmit} className="space-y-6">
        {/* Name and Email */}
        <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
          <div>
            <label className="block text-text-secondary text-sm mb-2">Name</label>
            <input
              type="text"
              value={formData.name}
              onChange={(e) => setFormData({...formData, name: e.target.value})}
              className="input-retro w-full"
              required
            />
          </div>
          <div>
            <label className="block text-text-secondary text-sm mb-2">Email</label>
            <input
              type="email"
              value={formData.email}
              onChange={(e) => setFormData({...formData, email: e.target.value})}
              className="input-retro w-full"
              required
            />
          </div>
        </div>
        
        {/* Category and Priority */}
        <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
          <div>
            <label className="block text-text-secondary text-sm mb-2">Category</label>
            <select
              value={formData.category}
              onChange={(e) => setFormData({...formData, category: e.target.value})}
              className="input-retro w-full"
            >
              <option value="general">General Question</option>
              <option value="technical">Technical Issue</option>
              <option value="account">Account Problem</option>
              <option value="trading">Trading Issue</option>
              <option value="security">Security Concern</option>
            </select>
          </div>
          <div>
            <label className="block text-text-secondary text-sm mb-2">Priority</label>
            <select
              value={formData.priority}
              onChange={(e) => setFormData({...formData, priority: e.target.value as any})}
              className="input-retro w-full"
            >
              <option value="low">Low</option>
              <option value="medium">Medium</option>
              <option value="high">High</option>
              <option value="urgent">Urgent</option>
            </select>
          </div>
        </div>
        
        {/* Subject */}
        <div>
          <label className="block text-text-secondary text-sm mb-2">Subject</label>
          <input
            type="text"
            value={formData.subject}
            onChange={(e) => setFormData({...formData, subject: e.target.value})}
            className="input-retro w-full"
            required
          />
        </div>
        
        {/* Message */}
        <div>
          <label className="block text-text-secondary text-sm mb-2">Message</label>
          <textarea
            value={formData.message}
            onChange={(e) => setFormData({...formData, message: e.target.value})}
            className="input-retro w-full h-32 resize-none"
            required
          />
        </div>
        
        {/* Submit Button */}
        <RetroButton
          type="submit"
          variant="primary"
          size="lg"
          className="w-full"
          loading={loading}
        >
          Submit Support Ticket
        </RetroButton>
      </form>
      
      {/* Response Time Info */}
      <div className="mt-6 p-4 bg-bg-tertiary rounded-lg">
        <h4 className="text-white font-semibold mb-2">Response Times</h4>
        <div className="space-y-1 text-sm text-text-secondary">
          <div>• Low Priority: 48-72 hours</div>
          <div>• Medium Priority: 24-48 hours</div>
          <div>• High Priority: 12-24 hours</div>
          <div>• Urgent: 2-6 hours</div>
        </div>
      </div>
    </GlowCard>
  );
};
```

## Additional Resources Section

### Resources Implementation
```typescript
const AdditionalResources = () => {
  const resources = [
    {
      title: "Documentation",
      description: "Comprehensive guides and API documentation",
      icon: <Book className="w-8 h-8" />,
      link: "/docs",
      color: "green"
    },
    {
      title: "Video Tutorials",
      description: "Step-by-step video guides for common tasks",
      icon: <Play className="w-8 h-8" />,
      link: "/tutorials",
      color: "blue"
    },
    {
      title: "Community Forum",
      description: "Connect with other users and share experiences",
      icon: <Users className="w-8 h-8" />,
      link: "/community",
      color: "purple"
    }
  ];
  
  return (
    <section className="py-16 px-6">
      <div className="max-w-6xl mx-auto">
        <div className="text-center mb-12">
          <h2 className="text-4xl font-bold text-white mb-4">
            Additional Resources
          </h2>
          <p className="text-text-secondary text-lg">
            Explore more ways to get help and learn about Wildcard
          </p>
        </div>
        
        <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
          {resources.map((resource) => (
            <GlowCard 
              key={resource.title}
              className="p-8 text-center cursor-pointer hover-lift"
              glowColor={resource.color as any}
              intensity="low"
            >
              <div className={`text-neon-${resource.color} mb-4`}>
                {resource.icon}
              </div>
              <h3 className="text-xl font-bold text-white mb-3">
                {resource.title}
              </h3>
              <p className="text-text-secondary mb-6">
                {resource.description}
              </p>
              <RetroButton variant="secondary" size="sm">
                Learn More
              </RetroButton>
            </GlowCard>
          ))}
        </div>
      </div>
    </section>
  );
};
```

## Page Implementation

### Main Support Page
```typescript
// app/support/page.tsx
export default function SupportPage() {
  const { faqItems, categories } = useSupportData();
  
  return (
    <div className="min-h-screen bg-dark-bg">
      <SupportHeader />
      
      <div className="max-w-7xl mx-auto px-6 pb-16">
        <div className="grid grid-cols-1 lg:grid-cols-3 gap-8">
          {/* FAQ Section */}
          <div className="lg:col-span-2">
            <FAQSection items={faqItems} categories={categories} />
          </div>
          
          {/* Contact Form */}
          <div className="lg:col-span-1">
            <ContactForm />
          </div>
        </div>
      </div>
      
      <AdditionalResources />
    </div>
  );
}
```

## Components to Build

1. **SupportHeader.tsx** - Header with quick actions
2. **FAQSection.tsx** - FAQ with search and filtering
3. **ContactForm.tsx** - Support ticket form
4. **AdditionalResources.tsx** - Resource links
5. **LiveChat.tsx** - Live chat integration
6. **TicketStatus.tsx** - Support ticket tracking

This support page provides comprehensive help resources while maintaining the retro aesthetic and ensuring users can easily find solutions or get in touch with support.
