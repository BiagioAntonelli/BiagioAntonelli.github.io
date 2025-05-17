---
layout: post
title: "[Notes] Welcome to the Era of Experience"
date: 2025-05-17
categories: [ai]
---

# Welcome to the Era of Experience

Notes on a [short paper](https://storage.googleapis.com/deepmind-media/Era-of-Experience%20/The%20Era%20of%20Experience%20Paper.pdf) released a few weeks ago by David Silver and Richard Sutton, and is a preprint of a chapter from the soon to be published book `Designing an Intelligence` which I look forward to reading. 

> Artificial intelligence (AI) has made remarkable strides over recent years by training on massive amounts of
human-generated data and fine-tuning with expert human examples and preferences. This approach is exemplified by large language models (LLMs) that have achieved a sweeping level of generality. A single LLM
can now perform tasks spanning from writing poetry and solving physics problems to diagnosing medical
issues and summarising legal documents.
However, while imitating humans is enough to reproduce many human capabilities to a competent level,
this approach in isolation has not and likely cannot achieve superhuman intelligence across many important
topics and tasks. In key domains such as mathematics, coding, and science, the knowledge extracted from
human data is rapidly approaching a limit.

> Furthermore, valuable new insights, such as new theorems, technologies or scientific
breakthroughs, lie beyond the current boundaries of human understanding and cannot be captured by existing
human data

The paper starts with the current issue with LLMs and how they learn (by imitation) is reaching a plateau, and how reaching a new level of intelligence beyond human capabilities necessarily requires a new approach. A new source of data is therefore needed.

> This data must be generated in a way that
continually improves as the agent becomes stronger; any static procedure for synthetically generating data
will quickly become outstripped

> AI is at the cusp of
a new period in which experience will become the dominant medium of improvement and ultimately dwarf
the scale of human data used in today's systems.

> This transition may have already started
... [AlphaProof](https://deepmind.google/discover/blog/ai-solves-imo-problems-at-silver-medal-level/) recently became the first program to
achieve a medal in the International Mathematical Olympiad, eclipsing the performance of human-centric
approaches, ... recent work
from [DeepSeek](https://github.com/deepseek-ai/DeepSeek-R1) "underscores the power and beauty of reinforcement learning: rather than explicitly teaching
the model on how to solve a problem, we simply provide it with the right incentives, and it autonomously
develops advanced problem-solving strategies."

> Our contention is that **incredible new capabilities will arise once the full potential of experiential learning
is harnessed**. This era of experience will likely be characterised by agents and environments that, in addition
to learning from vast quantities of experiential data, will break through the limitations of human-centric AI
systems in several further dimensions:
- Agents will inhabit streams of experience, rather than short snippets of interaction. 
-  Their actions and observations will be richly grounded in the environment, rather than interacting via
human dialogue alone.
- Their rewards will be grounded in their experience of the environment, rather than coming from human
prejudgement.
- They will plan and/or reason about experience, rather than reasoning solely in human terms

## Limitation of Current Systems
> In the era of human data, language-based AI has largely:
- focused on short interactionn episodes: e.g., a user asks a question and (perhaps after a few thinking steps or tool-use actions) the agent responds.
- the agent aims exclusively for outcomes
within the current episode, such as directly answering a user's question

>On the contrary, humans may select actions to achieve long-term goals like improving their health,learning a language, or achieving a scientific breakthrough
...An individual step may not provide any immediate benefit, or may even be detrimental in the
short term, but may nevertheless contribute in aggregate to longer term success.

## Actions and Observations

> Recently, a new wave of prototype agents have started to interact with computers in an even more
general manner, by using the same interface that humans use to [operate a computer](https://www.anthropic.com/news/3-5-models-and-computer-use). . These
changes herald a transition from exclusively human-privileged communication, to much more autonomous
interactions where the agent is able to act independently in the world...

## Rewards

> Human-centric LLMs typically optimise for rewards based on human prejudgement: an expert observes
the agent's action and decides whether it is a good action...Relying on human prejudgement in this manner
usually leads to an impenetrable ceiling on the agent's performance: the agent cannot discover better strategies that are underappreciated by the human. To discover new ideas that go far beyond existing human
knowledge, it is instead necessary to use grounded rewards: **signals that arise from the environment itself**.
... Grounded rewards may arise from humans that are part of the agent's environment. For example, a human user could report whether they found a cake tasty, how fatigued they are after exercising, or the level
of pain from a headache, enabling an assistant agent to provide better recipes, refine its fitness suggestions,
or improve its recommended medication

## Planning and Reasoning
> Conceptually, LLMs can act as a universal computer: an LLM can
append tokens into its own context, allowing it to execute arbitrary algorithms before outputting a final result.
In the era of human data, these reasoning methods have been explicitly designed to imitate human thought
processes...
However, it is highly unlikely that human language provides the optimal instance of a universal computer.
More efficient mechanisms of thought surely exist, using non-human languages that may for example utilise
symbolic, distributed, continuous, or differentiable computations. A self-learning system can in principle
discover or improve such approaches by learning how to think from experience

## Why Now?
> Learning from experience is not new. Reinforcement learning systems have previously mastered a large
number of complex tasks..However, agents based on this paradigm did not leap the gap between simulation (closed problems with singular, precisely defined rewards) to reality.
The era of human data offered an appealing solution. Massive corpuses of human data contain examples
of natural language for a huge diversity of tasks..
**However, something was lost in this transition: an agent's ability to self-discover its own knowledge**.

# Conclusion Notes
The paradigm shift is evident both from latest works such as [computer use](https://www.anthropic.com/news/3-5-models-and-computer-use) and RL post-training is now becoming a standard for all reasoning models. As a practitioner designing AI agents applications, it also feels like we are missing tools to adequately evaluate and improve such powerful systems, and previous human-centric approaches and single/few turns evaluation techniques are starting to fall short. I'm very excited about this line of research and the potential it holds for developing truly autonomous, self-improving AI systems.