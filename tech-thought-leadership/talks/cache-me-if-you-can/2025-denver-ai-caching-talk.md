# Cache Me If You Can: Accelerating AI While Reducing Cost, Latency, and Chaos

**Event:** Denver AI Summit  
**Date:** Wednesday, September 17, 2025  
**Time:** 11:00am - 12:00pm MDT  
**Location:** Gravity Hause Denver  
**Speaker:** Chris McDermut

---

## Talk Abstract

LLMs are powerful, but treating them as stateless black boxes is a recipe for slow responses, soaring API costs, and inconsistent behavior. In this session, we'll explore how caching (yes, caching) is the unsung hero of scalable AI systems.

Whether you are building internal tools, customer-facing products, or developer infrastructure, caching frequently used prompts, completions, and embeddings can massively reduce cost, increase speed, and stabilize behavior. We will cover exact-match and semantic caching patterns, compare tools like Redis and vector databases, and walk through real-world architectures that unlock performance and consistency without sacrificing flexibility.

If you are tired of paying for the same answers twice or burning cycles on predictable output, this talk will give you the mental model and tooling to scale smarter.

---

## Key Takeaways

1. **Cost Reduction**: How caching can cut LLM API costs by 60-80% in production systems
2. **Latency Optimization**: Turn 2-second LLM calls into 50ms cache hits
3. **Consistency**: Eliminate the "different answer every time" problem for deterministic use cases
4. **Architecture Patterns**: Real-world caching architectures that scale
5. **Tool Comparison**: Redis vs Vector DBs vs Edge caching for different scenarios

---

## Talk Outline

### 1. The Hidden Cost of Stateless AI (5 min)
- Why every LLM call shouldn't be treated as unique
- The compound cost of repeated questions
- Latency kills user experience

### 2. Exact-Match Caching Patterns (10 min)
- Simple prompt → response caching
- Key normalization strategies
- TTL strategies for different use cases
- Demo: 100x speedup on FAQ-style queries

### 3. Semantic Caching with Embeddings (15 min)
- When exact match isn't enough
- Vector similarity for "close enough" queries
- Embedding cache architecture
- Demo: Semantic cache for customer support

### 4. Tool Comparison & Architecture (15 min)
- Redis: Simple, fast, proven
- Vector databases: Pinecone, Weaviate, Qdrant
- Edge caching: Cloudflare Workers AI
- Hybrid approaches for maximum efficiency

### 5. Production Patterns & Pitfalls (10 min)
- Cache invalidation strategies
- Monitoring cache hit rates
- A/B testing cached vs fresh responses
- Legal/compliance considerations

### 6. Q&A (5 min)

---

## Code Examples

### Basic Exact-Match Cache

```python
import hashlib
import redis
import json

class LLMCache:
    def __init__(self):
        self.redis_client = redis.Redis()
        self.ttl = 3600  # 1 hour
    
    def get_or_generate(self, prompt, model="gpt-4"):
        # Normalize and hash the prompt
        cache_key = self._generate_key(prompt, model)
        
        # Check cache
        cached = self.redis_client.get(cache_key)
        if cached:
            return json.loads(cached)
        
        # Generate fresh response
        response = call_llm(prompt, model)
        
        # Cache for next time
        self.redis_client.setex(
            cache_key, 
            self.ttl, 
            json.dumps(response)
        )
        
        return response
    
    def _generate_key(self, prompt, model):
        normalized = prompt.strip().lower()
        return f"llm:{model}:{hashlib.md5(normalized.encode()).hexdigest()}"
```

### Semantic Cache with Embeddings

```python
import numpy as np
from qdrant_client import QdrantClient

class SemanticCache:
    def __init__(self, similarity_threshold=0.95):
        self.qdrant = QdrantClient("localhost", port=6333)
        self.threshold = similarity_threshold
        
    def search_similar(self, prompt_embedding):
        results = self.qdrant.search(
            collection_name="prompt_cache",
            query_vector=prompt_embedding,
            limit=1
        )
        
        if results and results[0].score > self.threshold:
            return results[0].payload["response"]
        
        return None
```

---

## Resources & Links

- [GitHub: Example Implementations](https://github.com/chrismcdermut/llm-caching-patterns)
- [Blog: "The Economics of LLM Caching"](https://example.com/blog)
- [Tool Comparison Matrix](https://example.com/tools)

---

## About the Speaker

Chris McDermut is a product-minded engineering leader focused on AI-augmented systems and caching strategies that reduce cost and eliminate friction. Currently building CareerOps/Inflow, an AI-powered data extraction platform.

---

## Contact

- Email: [YOUR EMAIL]
- LinkedIn: [YOUR LINKEDIN]
- Twitter/X: [YOUR HANDLE]
- CareerOps: https://www.careerops.com

---

*Note: This talk focuses on practical, production-ready patterns that attendees can implement immediately, not theoretical or academic approaches.*