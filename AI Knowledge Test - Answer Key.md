# AI Knowledge Test - Answer Key & Study Resources

## Basic Level

### 1. What's the difference between supervised and unsupervised learning?

**Correct Answer:** 
- **Supervised**: Learning with labeled data (input-output pairs). Examples: image classification with labeled cat/dog photos, sentiment analysis with labeled positive/negative reviews.
- **Unsupervised**: Learning patterns from data without labels. Examples: clustering customers by behavior, finding topics in documents, dimensionality reduction.

**Your Answer Assessment:** You described RLHF, which is a form of reinforcement learning. Close conceptually but different category.

**Study Resources:**
- "Pattern Recognition and Machine Learning" by Bishop - Chapters 1-3
- Andrew Ng's ML Course (Coursera) - Week 1
- "The Elements of Statistical Learning" - Chapter 2

---

### 2. What does "gradient descent" do?

**Correct Answer:** 
Gradient descent is an optimization algorithm that iteratively moves in the direction of steepest descent (negative gradient) to minimize a loss function. It updates parameters by: θ = θ - α∇J(θ)

**Your Answer Assessment:** You got the optimization and weight-finding part right! Just needed more precision about following gradients.

**Study Resources:**
- "Deep Learning" by Goodfellow, Bengio, Courville - Chapter 4
- 3Blue1Brown Neural Networks series - Episode on gradient descent
- CS231n Stanford - Lecture on optimization

---

### 3. What's the purpose of a validation set?

**Correct Answer:** 
To evaluate model performance on unseen data during training without touching the test set. Prevents overfitting by providing unbiased performance estimates for hyperparameter tuning and model selection.

**Your Answer Assessment:** You confused validation with training data. Validation is for evaluation, not training.

**Study Resources:**
- "Hands-On Machine Learning" by Aurélien Géron - Chapter 2
- CS229 Stanford - Notes on bias/variance tradeoff
- Andrew Ng's ML Course - Cross-validation section

---

## Intermediate Level

### 4. Explain the vanishing gradient problem and one solution.

**Correct Answer:** 
In deep networks, gradients become exponentially smaller as they backpropagate through layers, making early layers learn very slowly. Solutions include: residual connections (ResNet), LSTM/GRU gates, proper initialization (Xavier/He), batch normalization.

**Study Resources:**
- "Deep Learning" by Goodfellow et al. - Chapter 8.2.5
- Original ResNet paper: "Deep Residual Learning for Image Recognition"
- "Understanding the difficulty of training deep feedforward neural networks" by Glorot & Bengio
- CS231n - Lecture on training neural networks

---

### 5. What's the key innovation of the Transformer architecture over RNNs?

**Correct Answer:** 
Self-attention mechanism allows parallel processing and direct connections between any positions, solving RNN's sequential bottleneck and long-range dependency issues.

**Your Answer Assessment:** Excellent! You correctly identified attention as the key innovation.

**Study Resources:**
- "Attention Is All You Need" - Original Transformer paper
- "The Illustrated Transformer" by Jay Alammar
- CS224n Stanford - Attention and Transformers lecture
- "Formal Algorithms for Transformers" by Phuong & Hutter

---

### 6. How does batch normalization help training?

**Correct Answer:** 
Normalizes inputs to each layer (mean=0, std=1), reducing internal covariate shift. This stabilizes training, allows higher learning rates, acts as regularization, and reduces dependence on initialization.

**Your Answer Assessment:** You thought of data deduplication, but batch norm is about normalizing layer inputs during training.

**Study Resources:**
- "Batch Normalization: Accelerating Deep Network Training by Reducing Internal Covariate Shift"
- CS231n - Batch normalization lecture
- "Deep Learning" by Goodfellow et al. - Section 8.7.1

---

## Advanced Level

### 7. Explain the difference between model parallelism and data parallelism in distributed training.

**Correct Answer:** 
- **Data Parallelism**: Same model on multiple devices, different data batches. Gradients averaged across devices.
- **Model Parallelism**: Different parts of model on different devices. For models too large for single device memory.

**Your Answer Assessment:** You got model parallelism partially right but missed data parallelism concept.

**Study Resources:**
- "Efficient Large-Scale Language Model Training on GPU Clusters Using Megatron-LM"
- PyTorch Distributed Training tutorials
- "ZeRO: Memory Optimizations Toward Training Trillion Parameter Models"
- Google's "GPipe" paper on pipeline parallelism

---

### 8. What's the intuition behind why larger models tend to be more sample efficient?

**Correct Answer:** 
Larger models can represent more complex functions and learn richer representations, allowing them to extract more information from each training example. They also benefit from better inductive biases and can memorize more patterns.

**Your Answer Assessment:** Good mention of scaling laws! You understand the performance relationship, just needed the sample efficiency angle.

**Study Resources:**
- "Scaling Laws for Neural Language Models" by OpenAI
- "Training Compute-Optimal Large Language Models" (Chinchilla paper)
- "Deep Double Descent" paper
- Anthropic's "Constitutional AI" papers

---

### 9. Describe the alignment problem in AI safety and why it's non-trivial.

**Correct Answer:** 
The difficulty of ensuring AI systems pursue intended objectives rather than gaming metrics. Non-trivial due to: specification gaming, distributional shift, emergent capabilities, and the fundamental challenge of encoding human values.

**Your Answer Assessment:** Great perspective on bias and subjectivity! You touched on key issues, just missing the specification gaming angle.

**Study Resources:**
- "Concrete Problems in AI Safety" by Amodei et al.
- Stuart Russell's "Human Compatible"
- Anthropic's Constitutional AI papers
- "AI Alignment: Why It's Hard, and Where to Start" by Eliezer Yudkowsky
- OpenAI's "Learning to Summarize with Human Feedback"

---

## Expert Level

### 10. Explain the mechanistic interpretability approach to understanding neural networks.

**Correct Answer:** 
Reverse-engineering neural networks by identifying specific circuits, features, and algorithms learned by the model. Goes beyond black-box analysis to understand the actual computational mechanisms.

**Study Resources:**
- Anthropic's "Toy Models of Superposition"
- "A Mathematical Framework for Transformer Circuits"
- Distill.pub articles on neural network interpretability
- Chris Olah's work on feature visualization
- "Towards Monosemanticity" by Anthropic

---

### 11. What are the theoretical implications of the lottery ticket hypothesis?

**Correct Answer:** 
Suggests dense networks contain sparse subnetworks that can achieve comparable accuracy when trained in isolation. Implies redundancy in over-parameterization and questions about the role of initialization in optimization.

**Study Resources:**
- "The Lottery Ticket Hypothesis: Finding Sparse, Trainable Neural Networks"
- "Proving the Lottery Ticket Hypothesis: Pruning is All You Need"
- "Linear Mode Connectivity and the Lottery Ticket Hypothesis"
- ICLR 2019 presentation and follow-up papers

---

### 12. How do emergence and grokking relate to phase transitions in learning?

**Correct Answer:** 
Both represent sudden, qualitative changes in model behavior. Emergence shows capabilities appearing suddenly at scale, while grokking shows sudden generalization after long overfitting. Both suggest non-smooth learning dynamics.

**Study Resources:**
- "Emergent Abilities of Large Language Models" by Google
- "Grokking: Generalization Beyond Overfitting on Small Algorithmic Datasets"
- "Phase Transitions in Random Circuit Sampling"
- Papers on scaling laws and emergent capabilities
- Anthropic's work on mechanistic interpretability and phase changes

---

## Recommended Learning Path

1. **Fill Foundation Gaps**: Focus on gradient descent, batch normalization, validation concepts
2. **Dive into Transformers**: Read "Attention Is All You Need" and follow-up papers
3. **Study Scaling Laws**: Chinchilla, GPT scaling papers
4. **Explore Safety/Alignment**: Constitutional AI, RLHF papers
5. **Advanced Topics**: Mechanistic interpretability, emergence research

Your theoretical intuitions are strong - focus on filling technical implementation details!