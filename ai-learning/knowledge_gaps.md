# Knowledge Gaps Tracker

## Current Gaps (Priority Order)

### High Priority (Blocking current work)
- [ ] **Structured Output Guarantees**: How to ensure LLM outputs match schema 100%
- [ ] **Token Optimization**: Reducing costs while maintaining quality
- [ ] **Error Recovery**: Best patterns for handling LLM failures in production

### Medium Priority (Would improve current work)
- [ ] **Fine-tuning vs Prompting**: When is each approach worth it?
- [ ] **Embedding Models**: How to choose and optimize for specific domains
- [ ] **Agent Memory**: Patterns for maintaining context across sessions

### Low Priority (Future exploration)
- [ ] **Multi-modal Models**: Image + text for screenshot parsing
- [ ] **Local Model Deployment**: Running smaller models on-device
- [ ] **Training Custom Models**: When/how to train vs use existing

## Questions from Papers

### From Transformer Paper
- [ ] Why exactly does multi-head attention work better than single?
- [ ] How do position encodings preserve sequence information?

### From GPT-3 Paper
- [ ] What's the relationship between model size and emergent abilities?
- [ ] How does few-shot learning actually work internally?

## Implementation Challenges
- [ ] How to test non-deterministic AI features?
- [ ] Best practices for prompt version control
- [ ] Monitoring and debugging agent chains in production

## Concepts to Clarify
- [ ] Difference between fine-tuning, RAG, and prompt engineering trade-offs
- [ ] When to use function calling vs structured prompts
- [ ] Temperature vs top-p vs top-k in practice

## Tools/Frameworks to Explore
- [ ] LangChain vs building custom orchestration
- [ ] Vector databases: Pinecone vs Weaviate vs pgvector
- [ ] Evaluation frameworks for LLM applications

## Notes
- Add items here whenever confused
- Review weekly and prioritize based on current needs
- Research high-priority items during next study session