---
layout: post
title: "A Journey Through Key LLM Advancements"
date: 2024-02-01
categories: [ai, llms, deep-learning]
---

It's been fascinating experiencing the journey of Large Language Models (LLMs) and how they've transformed from specialized NLP tools to general-purpose AI systems. I feel very fortunate to be able to work on, and apply this technology on products used by millions of people. Since they were first proposed in 2017, a lot of things (although surprisingly not that many from a model architecture point of view as we will see) have changed, I'll break down the breakthoughs in 4 main areas which I believe played a role in making LLMs the powerful tech that it is now.

***Disclaimer***: this review is not exhaustive at all, it's just based on things that are on top of my head and random notes I've collected over the years and I'm sure I'll forget to cover some important topics.

- [The Foundation: Base Architectures](#the-foundation-attention-is-all-you-need)
  - [Efficiency Innovations](#efficiency-innovations)
  - [Scaling Laws](#the-scaling-laws-revelation)
- [Post-training and Alignment](#reasoning-and-learning)
  - [Few-Shot Learning](#few-shot-learning)
  - [Advanced Reasoning](#advanced-reasoning)
- [Augmenting LLM Capabilities](#rag-and-knowledge-integration)
  - [Prompt Engineering](#prompt-engineering-evolution)
  - [RAG](#rag-and-knowledge-integration)
  - [Tools and Agents](#agents-and-automation)
- [The Reasoning Paradigm](#reasoning-and-learning)
  - [Chain of Thought](#prompt-engineering-evolution)
  - [Reinforcement Learning](#agents-and-automation)
- [Killer Apps](#killer-apps)
    - [Cursor and Replit](#cursor-and-replit)
    - [NotebookLM](#notebooklm)
    - [Deepmind project](#deepmind-project)
    - [Meta glasses](#meta-glasses)


## The Foundation: Attention Is All You Need

[Attention Is All You Need](https://arxiv.org/abs/1706.03762) by Vaswani et al. introduced the Transformer architecture in 2017. While revolutionary, it took about a year for the community to realize its full potential. The key innovation wasn't just the attention mechanism, but how it enabled parallel processing of sequences, unlike previous RNN-based approaches.

What's particularly interesting is how this architecture has remained largely unchanged in modern LLMs as we're still using the same core building blocks:
- Multi-head attention
- Layer normalization
- Skip connections
- Feed-forward networks

Recent architectural innovations have been more about scale and efficiency than fundamental changes. The most notable exception might be the Mixture of Experts (MoE) approach used in models like [Mixtral](https://mistral.ai/news/mixtral-of-experts/) and [DeepSeek-MoE](https://github.com/deepseek-ai/DeepSeek-MoE), which dynamically routes inputs through specialized sub-networks. Otherwise, the core changes are minimal and related more to efficiency and resources optimization.

[TO ADD: Diagram showing base transformer architecture]

### Efficiency Innovations

Some of the most impactful innovations in making LLMs more efficient are:

#### Memory Management
1. **KV-Cache Optimization**
   - Standard KV-Cache for faster inference
   - Quantized KV-Cache for memory efficiency
   - [Paged Attention](https://vllm.ai/) for better memory utilization

#### Computation Optimization
1. **Flash Attention** ([paper](https://arxiv.org/abs/2205.14135))
   - Rethinks attention computation for better memory efficiency
   - Achieves significant speedups without accuracy loss

2. **Batching Innovations**
   - Continuous Batching for better throughput
   - Dynamic Batching strategies
   
3. **Grouped Query Attention**
   - Reduces memory requirements while maintaining model quality
   - Widely adopted in models like Llama 2

#### Model Compression
1. **LoRA and Variants**
   - [QLoRA](https://arxiv.org/abs/2305.14314) for efficient fine-tuning
   - Multi-LoRA serving for multiple adaptations
   
2. **Quantization**
   - Post-training quantization
   - Fine-tuned quantization approaches
   - [GPTQ](https://arxiv.org/abs/2210.17323) and variants

### Scaling Laws

One of the most impactful feature that made LLMs this successful is scale, both in therms of model size and amount of data ingested.

One of the most influential papers was OpenAI's [Scaling Laws for Neural Language Models](https://arxiv.org/abs/2001.08361). The key finding was remarkably simple yet profound:

> The loss scales as a power-law with model size, dataset size, and the amount of compute used for training, with some trends spanning more than seven orders of magnitude.

This insight connects with Rich Sutton's ["The Bitter Lesson"](http://www.incompleteideas.net/IncIdeas/BitterLesson.html), which argues that general methods leveraging computation consistently win over hand-crafted approaches.

[TO ADD: Graph showing parameter scaling across major models]


Big companies Like Meta (link to YT of Zuck), OpenAI (50B training  cluster) are still betting big on scaling laws, despite some concerns that we've reached a limit as Ilya pointed out some months ago at Neurips (add link)/

## Post-training and Alignment

The evolution of reasoning capabilities has been fascinating:

### Few-Shot Learning
OpenAI's [GPT-3 paper](https://arxiv.org/pdf/2005.14165) demonstrated that large models could learn from just a few examples:

[TO ADD: Few-shot learning performance graph from GPT-3 paper]

### Advanced Reasoning
Recent developments show impressive progress:
1. **OpenAI's O1 Series**
   - Improved logical reasoning
   - Better mathematical capabilities
   
2. **LLaVA-O1** ([paper](https://arxiv.org/abs/2310.03744))
   - Visual reasoning capabilities
   - Structured thought processes

3. **DeepSeek-R1** ([GitHub](https://github.com/deepseek-ai/DeepSeek-R1))
   - Self-reflective capabilities
   - Emergent reasoning from RL training

## Augmenting LLM Capabilities

After the success of ChatGPT, one of the main limitations that emerged was the outdated knowledge of the model, which would know events only until the training date, and Allucinations, which is now still not solved, but many techiques have been developed to reduce them. 

Innovations like Retrieval Augmented Generation (RAG), Prompt Engineering, and Tools and Agents have been developed to address these issues and make LLMs even more useful in real-world applications.

### Prompt Engineering

It turns out that we can improve the performances of LLMs by simply writing better prompts. During only a few years, the literature on prompt engineering has grown exponentially, here I will just mention some of the main techiques:

1. **Basic Techniques**
   - In-context learning
   - Few-shot prompting
   
2. **Advanced Methods**
   - Chain-of-Thought (CoT)
   - Tree of Thoughts
   - [Emotional Prompting](https://arxiv.org/pdf/2307.11760)
   
3. **Multi-turn Frameworks**
   - ReAct framework
   - Structured prompting

### RAG

Retrieval-Augmented Generation is a query expansion techinques which expand the context of the query by fetching relevant information from a database or from the internet using vector Databases and tools to query external data sources.

RAGs enabled right away hundreds on business applications, from querying internal documentations, to text to SQL, chat with documents/books, and more (not too mention a whole new market of VectorDB vendors). I won't go into details here but I will just write some known techniques and strategies which are commonly used in RAGs systems:

#### Core Components
1. **Chunking Strategies**
   - Semantic chunking
   - Overlapping windows
   - Hierarchical approaches

2. **Retrieval Methods**
   - Dense embeddings
   - Sparse vectors (BM25)
   - Hybrid approaches

#### Advanced Techniques
1. **Contextual Retrieval**
   - Anthropic's [research on contextual retrieval](https://www.anthropic.com/news/contextual-retrieval)
   - Query rewriting strategies
   
2. **Re-ranking**
   - Cross-encoder approaches
   - Fine-tuned retrievers
   - Ensemble methods

### Tools and Agents

The emergence of LLM-powered agents has opened new possibilities:

1. **Tool Usage**
   - [Toolformer](https://arxiv.org/abs/2302.04761)
   - Function calling capabilities
   
2. **Orchestration**
   - Task planning
   - Multi-agent coordination
   
3. **Monitoring and Control**
   - Safety guardrails
   - Performance tracking

## The Reasoning Paradigm

The reasoning paradigm in LLMs has evolved:

### Chain of Thought

[TO ADD: Detailed explanation of Chain of Thought prompting, its impact, and real-world applications]

### Reinforcement Learning

[TO ADD: Coverage of reinforcement learning in LLM training, including RLHF and other approaches]

More recently, DeepSeek-R1 has been trained using Reinforcement Learning without any human feedback, and it has been able to learn to reason and solve problems without any human intervention. 

The Deepseek researcher write about the moment where the model learns to reason by itself as follow:
> This moment is not only an “aha moment” for the model but also for the researchers observing its behavior. It underscores the power and beauty of reinforcement learning: rather than explicitly teaching the model on how to solve a problem, we simply provide it with the right incentives, and it autonomously develops advanced problem-solving strategies. The “aha moment” serves as a powerful reminder of the potential of RL to unlock new levels of intelligence in artificial systems, paving the way for more autonomous and adaptive models in the future.

This is a very exciting moment, and it shows the potential of RL to unlock new levels of intelligence and partially overcome the limitations about exhausting the amount of data available to train.

## What's Next?

The field continues to evolve rapidly. Key areas to watch:

1. **Multimodal Integration**
   - Llama 3's multimodal capabilities
   - LLaVA and CLIP advancements
   
2. **Efficient Adaptation**
   - Better fine-tuning methods
   - More efficient serving strategies

3. **Enhanced Reasoning**
   - Improved logical capabilities
   - Better mathematical understanding

I'll be updating this post as new developments emerge. The goal is to maintain a living document of the field's evolution, much like Simon Willison does with his technology tracking.

---

*This post is part of my ongoing series tracking AI developments. I'm experimenting with Simon Willison's approach to link blogging, where sharing interesting findings and adding context can be as valuable as original research.* 