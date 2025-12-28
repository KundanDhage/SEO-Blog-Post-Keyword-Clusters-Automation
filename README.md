SEO Blog Post & Keyword Clusters Automation
Purpose
Fully automated SEO-optimized blog post creation system that transforms keyword clusters into publication-ready, research-backed articles and publishes them directly to WordPress.

Workflow Architecture
Phase 1: Scheduled Trigger & Keyword Selection
Scheduler Configuration

Trigger Type: Cron-based schedule
Schedule: Every Tuesday at 1:02 AM (2 1 * * 2)
Automation Level: Fully autonomous (no manual intervention required)

Keyword Cluster Retrieval
Data Source: Google Sheets ("Keywords - NEW")

Sheet: "Pillar Post #1 Name"
Filter Logic: Looks for rows where Completed = "No"
Selection Method: Returns first uncompleted cluster
Data Extracted:

Keywords list
Primary keyword
Search intent
Cluster metadata



Input Data Format:
Keywords: "SEO strategy, content marketing, keyword research, on-page SEO"
Primary Keyword: "SEO strategy"
Intent: "User wants to learn comprehensive SEO strategies for business growth"

Phase 2: Multi-Stage AI Content Creation Pipeline
Stage 1: Preliminary Planning (O1-Mini Model)
AI Model: OpenAI O1-Mini (via OpenRouter)
System Instructions:

Analyze keywords and search intent
Identify discussion points
Create preliminary blog post outline
Ensure all keywords can be naturally incorporated
Focus on satisfying user's search intent

Output: Dot-point preliminary plan
Example Output:
- Introduction to SEO strategy (use primary keyword)
- Why SEO matters for businesses
- Core components of effective SEO
- Keyword research fundamentals
- On-page optimization techniques
- Content marketing integration
- Measurement and analytics

Stage 2: Deep Research (Perplexity AI)
AI Model: Perplexity AI (sonar-pro model)
Research Instructions:
"You are conducting research for a world-class blog post.

Given keywords, search intent, and preliminary plan, you must:
- Find high-quality, reputable sources
- Extract key facts, statistics, and expert insights
- Ensure research is directly relevant to keywords
- Provide source URLs for all information
- Focus on recent, authoritative content"
Research Query Construction:
Combines all three inputs:

Keywords
Search intent
Preliminary plan

Output Processing:

Extracts research findings with citations
Replaces citation markers [1], [2], etc. with actual source URLs
Creates structured research document with inline source links

Research Output Format:
Point 1: SEO drives 1000%+ more traffic than organic social - source: https://...
Point 2: 68% of online experiences begin with search - source: https://...
Point 3: First organic result gets 28% of clicks - source: https://...

Stage 3: Detailed Plan Creation (O1-Preview Model)
AI Model: OpenAI O1-Preview (highest reasoning capability)
Planning Instructions (comprehensive):
"Create a DETAILED blog post plan using:
- Keywords (must place ALL keywords naturally)
- Primary keyword (must go in title + intro)
- Search intent (must fully satisfy)
- Research findings (must include with source URLs)
- Preliminary plan (starting framework)

Requirements:
- Very detailed (copywriter-ready)
- Include which keywords go in each section
- Include all research points with sources
- Specify technical details (not just "define X" but "define X as...")
- Natural flow and structure
- Section-by-section keyword placement
- For 5th-grade reading level
- 2000-2500 words minimum"
Key Innovation: Plan includes exact content, not just topics

Instead of: "Explain keyword research"
Provides: "Explain keyword research as the process of identifying search terms users enter into search engines, typically using tools like Google Keyword Planner or SEMrush to find..."

Output: Comprehensive, implementation-ready plan

Stage 4: Blog Post Writing (Claude 3.5 Sonnet)
AI Model: Claude 3.5 Sonnet (via OpenRouter)
Copywriting Instructions:
"Write the complete blog post following the detailed plan.

Content Requirements:
✓ Follow plan bit-by-bit
✓ Short paragraphs (3-4 sentences max)
✓ Bullet points and subheadings with keywords
✓ No fluff - value-dense content only
✓ Very detailed and comprehensive
✓ Place specified keywords in each section
✓ Include research sources as hyperlinks
✓ Primary keyword in: title, H1, early introduction
✓ One keyword per section heading
✓ Use synonyms and LSI keywords naturally
✓ 2000-2500 words minimum
✓ 5th-grade reading level
✓ Write ENTIRE post in one output (no cutting short)

Writing Style:
- Direct and actionable
- Clear and accessible
- Professional but conversational
- Evidence-based (cite research)"
Output: Complete blog post draft (2000-2500 words)

Phase 3: Internal Linking & SEO Enhancement
Previous Posts Retrieval
Source: Google Sheets ("Completed Keywords")

Fetches all previously published blog posts
Extracts: titles, URLs, keywords, topics

Aggregation

Consolidates all previous post data
Prepares context for internal linking analysis

Internal Link Insertion (Claude 3.5 Sonnet)
Instructions:
"Analyze the blog post and previous posts to add strategic internal links.

Rules:
- Add 3-7 internal links naturally
- Link to relevant previous posts only
- Use descriptive anchor text (not 'click here')
- Place links where contextually appropriate
- Don't force links where they don't fit
- Maintain natural reading flow

Previous posts available:
{{ previous-posts data }}

Current post:
{{ blog content }}"
Output: Blog post with internal linking strategy applied

Phase 4: HTML Conversion & Formatting
Markdown to HTML Conversion (Claude)

Converts blog post from markdown to clean HTML
Preserves formatting, headings, lists, links
Ensures WordPress-compatible HTML structure
Adds proper semantic HTML tags (h2, h3, strong, em, ul, ol)

Output: HTML-formatted blog post

Phase 5: SEO Metadata Generation
URL Slug Creation (GPT-4)
Instructions:
"Generate SEO-friendly URL slug from blog post title.

Rules:
- Lowercase only
- Hyphens instead of spaces
- No special characters
- Include primary keyword
- 3-6 words maximum
- Clear and descriptive"
Example:

Title: "The Complete Guide to SEO Strategy in 2025"
Slug: complete-guide-seo-strategy-2025


SEO Title Optimization (GPT-4)
Instructions:
"Create optimized SEO title from blog post content.

Rules:
- 50-60 characters
- Include primary keyword near beginning
- Compelling and click-worthy
- Accurately represents content
- Include year if time-sensitive
- Use power words (Guide, Complete, Ultimate, etc.)"
Example: "SEO Strategy Guide 2025: Boost Rankings & Traffic"

Meta Description Creation (GPT-4)
Instructions:
"Write meta description for blog post.

Rules:
- 150-160 characters
- Include primary keyword naturally
- Compelling call-to-action
- Summarize key benefit/value
- Encourage click-through
- Active voice"
Example: "Learn proven SEO strategies to boost rankings and drive organic traffic. Complete guide with actionable tips, research-backed tactics, and real examples."

Phase 6: Visual Content Generation
Featured Image Creation (DALL-E 3)
Image Generation Prompt (GPT-4 constructed):
"Create professional blog header image for:

Topic: {{ blog title }}
Style: Modern, clean, professional
Colors: Brand-appropriate
Elements: Visual metaphors for {{ primary keyword }}
Format: 1200x630px (social media optimized)
Quality: High resolution, suitable for web
Mood: Professional, trustworthy, educational

No text in image."
Processing:

GPT-4 analyzes blog content
Constructs detailed DALL-E prompt
Generates featured image
Returns image URL

Output: Professional header image URL

Phase 7: WordPress Publication
Field Preparation
Consolidates all generated content:

HTML blog post content
SEO title
Meta description
URL slug
Featured image URL
Categories/tags (from keyword cluster)
Publication date

WordPress API Integration
Publication Parameters:
json{
  "title": "{{ SEO title }}",
  "content": "{{ HTML blog post }}",
  "slug": "{{ URL slug }}",
  "status": "publish",
  "meta_description": "{{ meta description }}",
  "featured_media": "{{ image URL }}",
  "categories": ["{{ category IDs }}"],
  "tags": ["{{ tag IDs }}"]
}
```

**Publishing Logic**:
- Uploads featured image to WordPress media library
- Creates new post with all metadata
- Sets publication status to "publish" (live)
- Assigns categories and tags
- Configures SEO settings (via Yoast/RankMath)

---

### **Phase 8: Completion Tracking**

#### **Google Sheets Update**
**Action**: Updates original keyword cluster sheet
- Finds row by primary keyword
- Changes `Completed` column from "No" to "Yes"
- Adds publication date timestamp
- Records WordPress post URL

#### **Completion Log (Second Sheet)**
**Recorded Data**:
```
- Cluster name
- Primary keyword
- Publication date
- WordPress URL
- Word count
- Keywords used
- Research sources count
- Internal links added
```

**Purpose**: 
- Prevents duplicate processing
- Maintains publication history
- Enables performance tracking
- Supports content audit

---

## **Technical Specifications**

### **AI Models Used** (4 different models)

| Stage | Model | Provider | Reasoning |
|-------|-------|----------|-----------|
| Preliminary Plan | O1-Mini | OpenAI | Fast, efficient planning |
| Research | Sonar-Pro | Perplexity | Real-time web research with citations |
| Detailed Plan | O1-Preview | OpenAI | Advanced reasoning, detailed instructions |
| Copywriting | Claude 3.5 Sonnet | Anthropic | Superior writing quality, long-form content |
| Internal Links | Claude 3.5 Sonnet | Anthropic | Context understanding |
| HTML Conversion | Claude 3.5 Sonnet | Anthropic | Formatting accuracy |
| SEO Metadata | GPT-4 | OpenAI | Concise, optimized text |
| Image Generation | DALL-E 3 | OpenAI | Visual content creation |

### **Integrations**
- Google Sheets API (OAuth2): Keyword management & tracking
- Perplexity AI API: Research & citations
- OpenAI API: Multiple model endpoints
- Anthropic API (via OpenRouter): Claude models
- WordPress REST API: Publication
- DALL-E 3 API: Image generation

### **Data Flow**
```
Schedule Trigger 
  → Google Sheets (keyword cluster)
  → O1-Mini (preliminary plan)
  → Perplexity (research)
  → O1-Preview (detailed plan)
  → Claude 3.5 (blog writing)
  → Google Sheets (previous posts)
  → Claude 3.5 (internal links)
  → Claude 3.5 (HTML conversion)
  → GPT-4 (slug, title, description)
  → DALL-E 3 (featured image)
  → WordPress (publication)
  → Google Sheets (completion tracking)

SEO Optimization Features
Keyword Strategy

Primary keyword placement: Title, H1, first 100 words, URL
Secondary keywords: Distributed across H2/H3 headings
LSI keywords: Natural semantic variations included
Keyword density: 1-2% (natural, not forced)
Long-tail variations: Addressed in body content

On-Page SEO

Meta title: 50-60 characters, primary keyword first
Meta description: 150-160 characters, includes CTA
URL structure: Clean, descriptive, keyword-rich
Header hierarchy: Proper H1→H2→H3 structure
Image alt text: Descriptive, keyword-inclusive (DALL-E generated)
Internal linking: 3-7 contextual links to related content
Content length: 2000-2500 words (comprehensive)
Readability: 5th-grade level (accessible)
Mobile-friendly: Clean HTML, responsive

Content Quality Signals

Research-backed: Multiple authoritative sources cited
Original content: AI-generated but unique and valuable
Comprehensive coverage: Addresses search intent fully
User engagement: Short paragraphs, bullet points, scannable
Expertise: Detailed technical information included
Freshness: Automated weekly publication
Multimedia: Featured images for every post


Content Quality Assurance
Built-in Quality Controls

Search Intent Validation: Every stage checks intent alignment
Keyword Coverage: Plan stage verifies all keywords placed
Source Credibility: Perplexity returns only reputable sources
Readability: Explicitly targets 5th-grade reading level
Completeness: Instruction to "write entire post, don't stop"
Value Density: "No fluff" requirement enforced
Natural Flow: Multiple AI reviews ensure coherence

AI Model Selection Strategy

O1-Mini: Planning (efficient)
O1-Preview: Deep planning (advanced reasoning)
Claude 3.5 Sonnet: Writing (best quality prose)
GPT-4: Concise tasks (titles, descriptions)
Perplexity: Research (specialized for web search)


Automation Benefits
Efficiency Gains

Time Saved: ~8-10 hours per blog post → 1 hour setup
Cost Reduction: No freelance writers needed
Consistency: Weekly publication schedule maintained
Scalability: Handles unlimited keyword clusters
Quality: Multiple AI models ensure high standards

SEO Benefits

Publishing Frequency: Consistent weekly content
Keyword Coverage: Systematic approach to all clusters
Internal Linking: Automatic discovery of link opportunities
Content Depth: 2000-2500 words per post
Research Quality: Only reputable sources cited
Technical SEO: Proper metadata and structure

Business Impact

Organic Traffic: Consistent content production
Domain Authority: Regular, quality publications
Thought Leadership: Comprehensive, research-backed content
Resource Optimization: Marketing team focuses on strategy
ROI: High-quality content at fraction of traditional cost


Use Cases
Perfect For:

Content Marketing Agencies: Scale client blog production
SaaS Companies: Maintain content calendars without writers
E-commerce: Product education and category content
B2B Companies: Thought leadership and SEO content
Startups: Bootstrap content marketing efforts
Marketing Teams: Augment existing content creation

Content Types Supported

How-to guides and tutorials
Ultimate/complete guides
Industry trend analysis
Product comparisons
Educational resources
Best practices articles
Pillar content pages
