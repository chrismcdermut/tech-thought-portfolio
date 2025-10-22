# Cache Me If You Can
### Cutting AI Costs Without Cutting Corners

#### Colorado Startup Week 2025
##### Chris McDermut

---

## The Billable ~~minutes~~ Tokens Problem
### AI charges like a lawyer - except it never remembers your case

^ 3-4 minutes
^ Start with the pain everyone knows
^ This is my actual story

---

# What's a Token?

**The currency of AI:**
- ~4 characters = 1 token
- 1 word ≈ 1.3 tokens
- 1 page of text ≈ 500 tokens
- Average website ≈ 2,000 tokens
- This slide ≈ 85 tokens

**GPT-4: $0.01 per 1K tokens (input) / $0.03 per 1K tokens (output)**

^ 1-2 minutes
^ Quick education before the pain
^ Now they understand the bills

---

# The Math That Hurts

**Job Seeker (200 jobs/month):**
- 2K input tokens × $0.01 = $0.02
- 250 output tokens × $0.03 = $0.0075
- Per job: ~$0.03 × 200 = **$6/month**

**Real Estate Underwriter (800 comps/month):**
- 5 pages × 2K tokens × $0.01 = $0.10 input
- 250 output tokens × $0.03 = $0.0075
- Per comp: ~$0.11 × 800 = **$88/month**

## Now multiply by 100 users...

^ 2-3 minutes
^ Real use cases from Inflow
^ This gets expensive fast

---

# Cost Calculators

**Know before you go:**
- https://yourgpt.ai/tools/openai-and-other-llm-api-pricing-calculator
- OpenAI Tokenizer → Count tokens before sending
- tiktoken (Python) → Programmatic token counting

**Pro tip:** Always estimate costs BEFORE deploying

^ 2 minutes
^ Use these before you build
^ Avoid bill shock

---

# Monitoring Tools

**Track your actual spend:**
- OpenAI Usage Dashboard → Daily/monthly spend
- Helicone.ai → Analytics & cost tracking  
- LangSmith → Token usage per request
- DIY: Log `{prompt, tokens_used, cost, timestamp}`

**You can't optimize what you don't measure**

^ 2 minutes  
^ Pick one and start today
^ The data will guide your caching strategy

----
## Before Caching: The Pain
---
![](job-capture-pre-cache-dev.mp4)

^ Show the actual latency and cost
^ Watch the token counter climb
^ Feel their pain

---
## After Caching: The Result
---
![](job-capture-post-cache-dev.mp4)

^ Instant responses
^ Minimal cost
^ Same quality output

---

# The Solution: Three-Layer Cache

```
Layer 1: Local Cache (Redis) - $0.00001/query
    ↓ (miss)
Layer 2: Vector DB (Pinecone) - $0.0001/query
    ↓ (miss)
Layer 3: LLM (GPT-4) - $0.10/query
```

**Most queries never reach Layer 3**

^ 5-6 minutes
^ Explain each layer's role
^ 1000x cost difference between layers

---

# Strategy 1: Exact Match Cache

**How it works:**
- User analyzes same document + prompt
- Cache key: `doc_id + prompt` 
- "job_listing_123 + summarize" → cached result
- Hit = return instantly (<1ms)

**Best for:** Repeated document analysis, same reports

^ 3-4 minutes
^ Simplest to implement
^ Start here

---

# Strategy 2: Pre-hydration

**Proactive caching (using cheaper models):**
1. Analyze your logs → find top queries
2. Generate responses during off-peak hours
3. Use cheaper models (GPT-3.5) for batch processing
4. Load cache before users wake up
5. First-time users get instant responses

**Best for:** Predictable questions, onboarding, demos

^ 3-4 minutes
^ Be proactive
^ Cache before they ask

---

# Strategy 3: Vector Similarity Cache

**How it works:**
- User asks: "How do I change my password?"
- Convert to vector embedding (~$0.0001)
- Search for similar vectors (>85% match)
- "password reset" = 94% similar → return cached

**Best for:** Variations of same intent

^ 3-4 minutes
^ Handles variations
^ The real magic

---

# Real Code (Simplified)

```python
class SmartCache:
    def get_response(self, query):
        # Try Redis first
        if cached := self.redis.get(query):
            return cached
        
        # Try vector similarity
        embedding = get_embedding(query)
        if similar := self.vector_db.query(embedding, threshold=0.85):
            return similar.response
        
        # Last resort: expensive LLM
        return call_llm(query)
```

^ 3-4 minutes
^ Walk through the logic
^ Emphasize simplicity

---

# The Projected Results

**Before:** $1,650/month, 3-5 second responses
**After:** $165/month, <100ms responses

## 90% cost reduction
## 50x faster

^ 2-3 minutes
^ These are realistic projections
^ Based on my actual data

---

# Common Pitfalls

1. **Measure before optimizing**
2. **Choose the right TTL**
3. **Start with 0.8 similarity threshold**
4. **Version your cache on models/prompts/context updates**

^ 2-3 minutes
^ Quick warnings
^ Keep it practical

---

# Quick Wins You Can Do Today

1. Log your LLM calls (30 mins)
2. Find your top 10 queries (1 hour)
3. Cache those 10 (2 hours)
4. **Save 30% by tomorrow**

^ 2-3 minutes
^ Send them home with action

---

# Let's Connect

**I'm building this now. Want to compare notes?**

Email: chrismcdermut@gmail.com
Projects: careerops.com + useinflow.io
Github: chrismcdermut
Website: chrismcdermut.com
LinkedIn: /in/chrismcdermut

## Q&A Time

^ Leave 10-15 for discussion
^ Get their horror stories

---
# Resources

Henry Shi's AI crash course https://github.com/henrythe9th/AI-Crash-Course
Book: Alex Xu's System Design Interview I + II
Learning platform: pluralsight.com + trysexponent.com
Certs: AWS developer AWS Solutions Architect

---

# Remember

## Every cached query is runway extended

### Thank you!