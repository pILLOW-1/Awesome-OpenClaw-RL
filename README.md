# 🦞 Awesome-OpenClaw-RL

> A curated list of open-source projects at the intersection of **Agent Infrastructure** and **Reinforcement Learning** — focused on training and improving LLM Agents via RL, especially through natural conversation feedback and online continual learning.

[![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/sindresorhus/awesome)

---

## 📖 Table of Contents

- [Core Projects (OpenClaw Ecosystem)](#-core-projects---openclaw-ecosystem)
- [Agentic RL Frameworks](#-agentic-rl-frameworks)
- [RL Training Infrastructure](#-rl-training-infrastructure)
- [Agent Infrastructure](#-agent-infrastructure)
- [Comparison Matrix](#-comparison-matrix)
- [Key Research Directions](#-key-research-directions)
- [Related Resources](#-related-resources)

---

## 🎯 Core Projects — OpenClaw Ecosystem

Projects directly built on or derived from [OpenClaw](https://github.com/openclaw/openclaw) that bring RL training to personal AI assistants.

### [OpenClaw-RL](https://github.com/Gen-Verse/OpenClaw-RL) ⭐ 3k
`TypeScript` | Train a personalized agent simply by talking to it.

- Fully asynchronous 4-component loop: serving, rollout collection, PRM/judge evaluation, policy training
- Three learning paradigms: **Binary RL** (GRPO), **OPD** (On-Policy Distillation), **Combine**
- General agent support: terminal, GUI, SWE, tool-call scenarios
- LoRA training + local GPU / cloud ([Tinker](https://thinkingmachines.ai/tinker/)) deployment
- Zero manual labeling — automatically organizes multi-turn interactions into training trajectories
- 📄 [Technical Report](https://arxiv.org/abs/2603.10165) — #1 on [HuggingFace Daily Papers](https://huggingface.co/papers/2603.10165)

### [MetaClaw](https://github.com/aiming-lab/MetaClaw) ⭐ 1.3k
`Python` | Just talk to your agent — it learns and EVOLVES.

- OpenAI-compatible proxy intercepts interactions + injects skills + meta-learns
- No GPU cluster needed — cloud LoRA training via Tinker/MinT
- Smart scheduler: RL weight updates only during idle/sleep/meeting windows
- Auto skill summarization and evolution after each session
- Three modes: `skills_only` / `rl` / `madmax` (default: RL + scheduler)

### [Claw-R1](https://github.com/AgentR1/Claw-R1) ⭐ 99
`Python` | Empowering OpenClaw with Advanced Agentic RL.

- **Middleware Layer** (Gateway Server + DataPool) decouples Agent side from Training side
- Three modes: white-box offline, black-box offline, black-box online service
- Zero-code intrusion: black-box agents (LangChain, AutoGen, CrewAI) just point `base_url` to Gateway
- Async training & rollout decoupling
- 🏫 USTC Cognitive Intelligence State Key Lab
- 📄 [Documentation](https://agentr1.github.io/)

---

## 🤖 Agentic RL Frameworks

General-purpose frameworks for training LLM Agents with reinforcement learning.

### [Agent-R1](https://github.com/AgentR1/Agent-R1) ⭐ High
`Python` | Training Powerful LLM Agents with End-to-End RL.

- Define domain-specific tools and reward functions to extend
- Supports GRPO, Reinforce++, process rewards
- Multi-modal support (VLM)
- Custom tool environments (e.g., ReTool implementation)
- 📄 [Technical Report](https://arxiv.org/abs/2511.14460)

### [rLLM](https://github.com/rllm-org/rllm) ⭐ High
`Python` | Democratizing Reinforcement Learning for Language Agents.

- Custom agents & environments, RL training + deployment in one framework
- **AgentWorkflowEngine** for training over arbitrary agentic programs
- Flagship models: [DeepCoder-14B](https://huggingface.co/collections/rLLM/deepcoder-preview-67a40fa53b2d9f72c6c1b0cd) (matches o3-mini), [DeepSWE-32B](https://huggingface.co/collections/rLLM/deepswe-preview-67a40fa53b2d9f72c6c1b0cd) (#1 open-weight on SWEBench)
- Integrated verl-0.5.0 + Megatron, LoRA and VLM training support
- 🏫 UC Berkeley Sky Computing Lab
- 📄 [Blog](https://rllm-project.com/blog)

### [MiniMax Forge](https://www.minimax.io/news/forge-scalable-agent-rl-framework-and-algorithm)
Scalable Agent RL framework and algorithm from MiniMax.

- Middleware-based architecture (inspired Claw-R1's design)
- Decouples agent serving and RL training
- Designed for large-scale online service agents

---

## ⚙️ RL Training Infrastructure

Foundational RL training libraries that power the Agentic RL ecosystem.

### [OpenRLHF](https://github.com/OpenRLHF/OpenRLHF) ⭐ High
`Python` | High-performance, production-ready RLHF framework.

- Ray + vLLM distributed architecture with unified agent-based design
- Algorithms: PPO, REINFORCE++, GRPO, RLOO, DAPO, TIS
- Single-turn and multi-turn agent RL training
- Production-ready (NVIDIA ProRL V2 uses REINFORCE++-baseline)
- 📖 [Documentation](https://openrlhf.readthedocs.io/)

### [veRL](https://github.com/volcengine/verl) ⭐ High
`Python` | Flexible and efficient RL training library (ByteDance).

- Hybrid-Controller programming model for flexible RL dataflows
- Integrates FSDP, Megatron-LM, vLLM, SGLang
- Flexible device mapping across cluster sizes
- HuggingFace model integration
- 📄 [HybridFlow Paper](https://arxiv.org/abs/2409.19256)

### [TRL](https://github.com/huggingface/trl)
`Python` | HuggingFace's official RL training library.

- Deep integration with HF ecosystem (Trainer API)
- PPO, DPO, RLOO, GRPO
- Largest community, most comprehensive documentation

### [PRIME](https://github.com/PRIME-RL/PRIME) ⭐ Medium
`Python` | Scalable RL with implicit process rewards.

- Implicit PRM training — no process annotations needed
- Integrated into veRL main branch
- Used for process reward normalization in Agent-R1
- 📄 [Paper](https://arxiv.org/abs/2502.01456)

---

## 🏗️ Agent Infrastructure

Agent orchestration and deployment frameworks (where Agentic RL models are served).

### [LangGraph](https://github.com/langchain-ai/langgraph)
`Python` | Build resilient language agents as graphs.
- Durable execution, human-in-the-loop, comprehensive memory
- Production deployment via LangSmith
- Trusted by Klarna, Replit, Elastic

### [AutoGen](https://github.com/microsoft/autogen)
`Python` | Multi-agent AI framework (Microsoft).
- Multi-agent conversation patterns, MCP tool integration
- AgentTool for nested agent-as-tool patterns
- No-code GUI (AutoGen Studio)

### [CrewAI](https://github.com/crewAIInc/crewAI)
`Python` | Role-driven multi-agent framework.
- Role-based agent definition (Role, Goal, Backstory)
- Sequential / Hierarchical task flows

### [OpenClaw](https://github.com/openclaw/openclaw)
`TypeScript` | Personal AI assistant platform.
- Single-user, local-first, 20+ channels (WhatsApp/Telegram/Discord/Feishu...)
- Skill system, persistent memory, sub-agent orchestration
- The primary target platform for OpenClaw-RL and MetaClaw

---

## 📊 Comparison Matrix

| Project | Stars | Language | Core Focus | Key Differentiator |
|---------|-------|----------|------------|-------------------|
| **OpenClaw-RL** | 3k | TS | Conversation → RL for OpenClaw | Fully async, zero labeling, 3 learning paradigms |
| **MetaClaw** | 1.3k | Python | Meta-learning + continual evolution | No GPU needed, smart scheduler, skill injection |
| **Claw-R1** | 99 | Python | RL middleware for general agents | White-box/black-box decoupling, zero intrusion |
| **Agent-R1** | High | Python | End-to-end agent RL training | Tool environment abstraction, process rewards |
| **rLLM** | High | Python | Full-stack language agent RL | AgentWorkflowEngine, multiple SOTA models |
| **OpenRLHF** | High | Python | General RLHF infrastructure | Ray+vLLM, production-ready, comprehensive algorithms |
| **veRL** | High | Python | LLM RL training library | HybridFlow, flexible dataflows |
| **TRL** | — | Python | HF official RL library | Largest community, HF ecosystem integration |
| **PRIME** | Medium | Python | Implicit process reward RL | No annotation PRM, integrated into veRL |

---

## 🔑 Key Research Directions

1. **From Offline RL to Online Continual Learning** — Real-time conversation as training signal (OpenClaw-RL, MetaClaw)
2. **Agent-Training Decoupled Architecture** — Middleware design for black-box agent RL integration (Claw-R1, MiniMax Forge)
3. **Personalized Agent Training** — Low-cost personal agent training via Binary RL + OPD (OpenClaw-RL)
4. **Meta-Learning Scheduling** — Training during idle/sleep windows (MetaClaw's madmax mode)
5. **Multi-Modal Agent RL** — GUI, vision, and audio rewards for multi-modal agents (rLLM VLM, Agent-R1)
6. **Safety & Controllability** — Reward hacking prevention, constitutional RL constraints
7. **Evaluation Standardization** — Unified Agent RL benchmarks combining online tasks + offline metrics
   - [EvoClaw](https://arxiv.org/abs/2603.13428) — A benchmark evaluating AI agents on continuous software evolution via Milestone DAGs reconstructed from commit logs. Tests agents' ability to sustain system integrity and limit error accumulation over long-term evolution. Finds that frontier model performance drops from >80% on isolated tasks to ≤38% in continuous settings.

---

## 📚 Related Resources

### Papers
- [OpenClaw-RL: Train any agent simply by talking](https://arxiv.org/abs/2603.10165)
- [Agent-R1: Training Powerful LLM Agents with End-to-End RL](https://arxiv.org/abs/2511.14460)
- [PRIME: Process Reinforcement through Implicit Rewards](https://arxiv.org/abs/2502.01456)
- [EvoClaw: Evaluating AI Agents on Continuous Software Evolution](https://arxiv.org/abs/2603.13428)
- [SDFT: Self-Distilled Fine-Tuning](https://arxiv.org/abs/2601.19897)
- [SDPO: Self-Distilled Policy Optimization](https://arxiv.org/abs/2601.20802)
- [HybridFlow: A Flexible and Efficient RLHF Framework](https://arxiv.org/abs/2409.19256)

### Awesome Lists
- [Awesome-Agent-RL](https://github.com/0russwest0/Awesome-Agent-RL) — Papers & resources on Agent RL

### Platforms & Tools
- [OpenClaw](https://openclaw.ai) — Personal AI assistant platform
- [Tinker](https://thinkingmachines.ai/tinker/) — Cloud-based LoRA training backend
- [MinT](https://github.com/MindLab-Research/mindlab-toolkit) — Alternative cloud RL training backend

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an Issue first to discuss what you would like to add.

To add a new project:
1. It should be related to Agentic RL, Agent training, or RL infrastructure for LLMs
2. Add it to the appropriate section with a brief description
3. Include the GitHub link, language, and key features

---

## 📄 License

This list is provided under the [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/).
