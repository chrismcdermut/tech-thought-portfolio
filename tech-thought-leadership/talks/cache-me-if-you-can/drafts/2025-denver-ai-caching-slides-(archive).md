# Cache Me If You Can - Slide Structure
## ~35 slides for 30-40 minutes of content

---

## SECTION 1: INTRO & PROBLEM (5 min, ~5 slides)

### Slide 1: Title Slide
**Cache Me If You Can**
Accelerating AI While Reducing Cost, Latency, and Chaos
- Chris McDermut
- Denver AI Summit | September 17, 2025

### Slide 2: The $10,000 Question
- "How many times have you paid OpenAI to answer the same question?"
- Visual: Dollar bills flying into a black hole
- Stats: Average production app makes 40% duplicate LLM calls

### Slide 3: The Real Cost of Stateless AI
- **Cost**: $0.03/call × 1M calls/month = $30,000
- **Latency**: 2-3 seconds per call
- **Inconsistency**: Different answers for same question
- **Scale**: Linear cost growth = death by API bills

### Slide 4: What If I Told You...
- 60-80% cost reduction
- 50ms response times (from 2+ seconds)
- Consistent, predictable responses
- Same exact LLM quality
- Visual: Before/After comparison chart

### Slide 5: Today's Journey
1. Exact-Match Caching (Quick wins)
2. Semantic Caching (Smart matching)
3. Production Architecture
4. Tools & Tradeoffs
5. Real-world Results

---

## SECTION 2: EXACT-MATCH CACHING (10 min, ~8 slides)

### Slide 6: The Simplest Win
**Exact-Match Caching**
- User asks: "What's your refund policy?"
- 1,000 users ask the same question
- Why call GPT-4 1,000 times?

### Slide 7: Basic Implementation
```python
cache_key = hash(prompt + model)
if cache.exists(cache_key):
    return cache.get(cache_key)  # 10ms
else:
    response = llm.generate(prompt)  # 2000ms
    cache.set(cache_key, response, ttl=3600)
```

### Slide 8: Key Normalization Matters
**Same question, different formats:**
- "What's your refund policy?"
- "what is your refund policy"
- "Refund policy?"
- "How do refunds work?"
Solution: Normalize before hashing

### Slide 9: TTL Strategy
| Use Case | TTL | Why |
|----------|-----|-----|
| FAQ | 24 hours | Rarely changes |
| Product search | 1 hour | Inventory updates |
| News summary | 15 min | Fresh content |
| Legal/Compliance | No cache | Always fresh |

### Slide 10: Real Results - FAQ Bot
- **Before**: 2.3s average response, $1,200/month
- **After**: 180ms average, $240/month
- **Cache hit rate**: 78%
- Visual: Response time histogram

### Slide 11: Demo - Live Speed Test
[Live demo or video showing side-by-side]
- Uncached: Loading... (2.5 seconds)
- Cached: Instant (45ms)

### Slide 12: Implementation Checklist
✅ Normalize inputs (lowercase, trim, etc.)
✅ Include model version in cache key
✅ Set appropriate TTLs
✅ Monitor hit rates
✅ Add cache warming for common queries

### Slide 13: When Exact-Match Fails
- "What's the refund policy?"
- "Can I return this?"
- "How do I get my money back?"
- Same intent, different words
→ Enter Semantic Caching

---

## SECTION 3: SEMANTIC CACHING (10 min, ~8 slides)

### Slide 14: The Similarity Problem
**Users don't ask questions the same way**
Visual: Word cloud of different phrasings

### Slide 15: Embeddings to the Rescue
1. Convert text → vector (embeddings)
2. Find similar vectors in cache
3. Return cached response if similarity > threshold
Visual: Vector space diagram

### Slide 16: Semantic Cache Architecture
```
User Query → Embedding Model → Vector DB
                                    ↓
                              Similar? (>0.95)
                               Yes → Return
                               No → Generate
```

### Slide 17: Similarity Thresholds
| Threshold | Use Case | Risk |
|-----------|----------|------|
| 0.99 | Medical/Legal | Very safe |
| 0.95 | Customer support | Balanced |
| 0.90 | Content generation | Some drift |
| 0.85 | Creative tasks | Higher drift |

### Slide 18: Real Example - Support Bot
**Query**: "My package hasn't arrived"
**Cached Similar Queries**:
- "Where is my order?" (0.96 similarity)
- "Package not delivered" (0.97 similarity)
- "Tracking shows delivered but not here" (0.91)

### Slide 19: Embedding Cache Performance
- Embedding generation: 50ms
- Vector search: 20ms
- Total overhead: 70ms
- Still 20x faster than LLM call!

### Slide 20: Demo - Semantic Matching
[Show live/video of semantic cache catching variations]

### Slide 21: Hybrid Approach
```
1. Try exact match (5ms)
2. If miss → try semantic (70ms)
3. If miss → call LLM (2000ms)
```
Best of both worlds!

---

## SECTION 4: TOOLS & ARCHITECTURE (8 min, ~6 slides)

### Slide 22: Tool Comparison Matrix
| Tool | Speed | Cost | Complexity | Best For |
|------|-------|------|------------|----------|
| Redis | ⚡⚡⚡ | $ | Low | Exact match |
| Pinecone | ⚡⚡ | $$$ | Medium | Semantic |
| Qdrant | ⚡⚡ | $$ | Medium | Self-hosted |
| Weaviate | ⚡⚡ | $$ | High | Full-text + vector |

### Slide 23: Production Architecture
Visual: Architecture diagram showing:
- API Gateway → Cache Layer → LLM
- Monitoring/Metrics dashboard
- Cache warming pipeline

### Slide 24: Edge Caching Pattern
**Cloudflare Workers Example**
- Cache at edge (5ms latency)
- Geographic distribution
- No infrastructure to manage
Code snippet showing Workers KV implementation

### Slide 25: Cache Invalidation Strategies
1. **TTL-based**: Simple, automatic
2. **Event-based**: On data changes
3. **Manual**: Admin panel for content updates
4. **Hybrid**: TTL + manual override

### Slide 26: Monitoring What Matters
- Cache hit rate (target: >60%)
- P50/P95/P99 latencies
- Cost savings dashboard
- Response quality metrics
Visual: Grafana dashboard

### Slide 27: A/B Testing Cache vs Fresh
- 10% fresh responses (control)
- 90% cached (treatment)
- Measure: User satisfaction, task completion
- Result: No statistical difference in quality

---

## SECTION 5: PRODUCTION LESSONS (7 min, ~5 slides)

### Slide 28: Common Pitfalls
❌ Caching personal/sensitive data
❌ Too aggressive similarity thresholds
❌ Not versioning cache keys
❌ Ignoring cache stampedes
❌ No monitoring

### Slide 29: Legal & Compliance
⚠️ **Consider**:
- GDPR/CCPA requirements
- Data residency
- Audit trails
- PII in prompts
- Cache encryption

### Slide 30: Case Study - E-commerce Assistant
**Before**: $45K/month OpenAI bill
**Implementation**: 2 weeks
**After**: 
- $8K/month (82% reduction)
- 150ms avg response (from 2.8s)
- 99.9% uptime
- Customer satisfaction ↑ 23%

### Slide 31: Start Small, Win Big
**Week 1**: Exact-match for FAQs
**Week 2**: Add semantic caching
**Week 3**: Production monitoring
**Month 2**: 70% cost reduction achieved

### Slide 32: Your Action Plan
1. Identify your repeated queries
2. Start with Redis + exact match
3. Measure hit rates
4. Add semantic for 80/20 coverage
5. Monitor and iterate

---

## SECTION 6: WRAP-UP (2 min, ~3 slides)

### Slide 33: Key Takeaways
✨ **Caching is not optional at scale**
✨ **Start simple (exact-match)**
✨ **80% of queries are duplicates**
✨ **Semantic caching catches the rest**
✨ **Monitor everything**

### Slide 34: Resources
- GitHub: github.com/chrismcdermut/llm-caching-patterns
- This presentation: [URL]
- Tool comparison guide: [URL]
- Connect: LinkedIn/Twitter

### Slide 35: Questions?
**Chris McDermut**
- Email: [your email]
- CareerOps: careerops.com
- Let's chat about your caching challenges!

---

## BACKUP SLIDES (for Q&A)

### Slide 36: Cache Size Calculations
- Average prompt: 500 tokens
- Average response: 800 tokens
- 10K cached items = ~50MB
- Cost: <$5/month Redis

### Slide 37: Multi-Model Caching
- Different cache pools per model
- GPT-4 vs GPT-3.5 vs Claude
- Model routing based on query complexity

### Slide 38: Code - Production Redis Setup
[Detailed code example with connection pooling, error handling]

### Slide 39: Streaming Response Caching
- Challenge: Token-by-token responses
- Solution: Cache complete responses, stream from cache

### Slide 40: Thank You!
**Remember: Every uncached LLM call is money left on the table**

---

## Presentation Tips:
1. **Slides 10 & 20**: Have videos ready as backup if live demo fails
2. **Keep code examples simple** - details in GitHub repo
3. **Use animations sparingly** - focus on content
4. **Have calculator ready** to show cost savings for audience examples
5. **Prepare 3-4 audience questions** to seed Q&A if needed