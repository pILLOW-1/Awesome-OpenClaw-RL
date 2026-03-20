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

### [OpenClaw-RL](https://github.com/Gen-Verse/OpenClaw-RL) ![GitHub stars](https://img.shields.io/github/stars/Gen-Verse/OpenClaw-RL?style=social)
`TypeScript` | Train a personalized agent simply by talking to it.

- Fully asynchronous 4-component loop: serving, rollout collection, PRM/judge evaluation, policy training
- Three learning paradigms: **Binary RL** (GRPO), **OPD** (On-Policy Distillation), **Combine**
- General agent support: terminal, GUI, SWE, tool-call scenarios
- LoRA training + local GPU / cloud ([Tinker](https://thinkingmachines.ai/tinker/)) deployment
- Zero manual labeling — automatically organizes multi-turn interactions into training trajectories
- 📄 [Technical Report](https://arxiv.org/abs/2603.10165) — #1 on [HuggingFace Daily Papers](https://huggingface.co/papers/2603.10165)

### [MetaClaw](https://github.com/aiming-lab/MetaClaw) ![GitHub stars](https://img.shields.io/github/stars/aiming-lab/MetaClaw?style=social)
`Python` | Just talk to your agent — it learns and EVOLVES.

- OpenAI-compatible proxy intercepts interactions + injects skills + meta-learns
- No GPU cluster needed — cloud LoRA training via Tinker/MinT
- Smart scheduler: RL weight updates only during idle/sleep/meeting windows
- Auto skill summarization and evolution after each session
- Three modes: `skills_only` / `rl` / `madmax` (default: RL + scheduler)

### [Claw-R1](https://github.com/AgentR1/Claw-R1) ![GitHub stars](https://img.shields.io/github/stars/AgentR1/Claw-R1?style=social)
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

### [Agent-R1](https://github.com/AgentR1/Agent-R1) ![GitHub stars](https://img.shields.io/github/stars/AgentR1/Agent-R1?style=social)
`Python` | Training Powerful LLM Agents with End-to-End RL.

- Define domain-specific tools and reward functions to extend
- Supports GRPO, Reinforce++, process rewards
- Multi-modal support (VLM)
- Custom tool environments (e.g., ReTool implementation)
- 📄 [Technical Report](https://arxiv.org/abs/2511.14460)

### [rLLM](https://github.com/rllm-org/rllm) ![GitHub stars](https://img.shields.io/github/stars/rllm-org/rllm?style=social)
`Python` | Democratizing Reinforcement Learning for Language Agents.

- Custom agents & environments, RL training + deployment in one framework
- **AgentWorkflowEngine** for training over arbitrary agentic programs
- Flagship models: [DeepCoder-14B](https://huggingface.co/collections/rLLM/deepcoder-preview-67a40fa53b2d9f72c6c1b0cd) (matches o3-mini), [DeepSWE-32B](https://huggingface.co/collections/rLLM/deepswe-preview-67a40fa53b2d9f72c6c1b0cd) (#1 open-weight on SWEBench)
- Integrated verl-0.5.0 + Megatron, LoRA and VLM training support
- 🏫 UC Berkeley Sky Computing Lab
- 📄 [Blog](https://rllm-project.com/blog)

### [ProRL Agent](https://github.com/NVIDIA-NeMo/ProRL-Agent-Server) ![GitHub stars](https://img.shields.io/github/stars/NVIDIA-NeMo/ProRL-Agent-Server?style=social)
Python | Rollout-as-a-Service infrastructure for RL training of multi-turn LLM agents (NVIDIA NeMo Gym).

- **Rollout-as-a-Service**: decouples rollout orchestration from training loop via API service
- Standardized and extensible sandbox environments for diverse agentic tasks
- Validated on software engineering, math, STEM, and coding tasks
- Rootless HPC deployment support
- 🏢 NVIDIA NeMo Gym
- 📄 [Paper](https://arxiv.org/abs/2603.18815)

### [MiniMax Forge](https://www.minimax.io/news/forge-scalable-agent-rl-framework-and-algorithm)
Scalable Agent RL framework and algorithm from MiniMax.

- Middleware-based architecture (inspired Claw-R1's design)
- Decouples agent serving and RL training
- Designed for large-scale online service agents
- Context Management modeled as agent action for explicit training awareness
- Prefix Tree Merging with MagiAttention for training-side KV cache sharing
- Dynamic MTP, PD-disaggregated scheduling, global L3 KV Cache Pool

### [ROLL](https://github.com/alibaba/ROLL) ![GitHub stars](https://img.shields.io/github/stars/alibaba/ROLL?style=social)
`Python` | Agentic RL training framework for terminal environments (Alibaba).

- Fully asynchronous training pipeline with environment-level async rollout
- Two modes: **Roll-Managed** (flexible training-side context) / **CLI-Native** (deployment-consistent)
- Companion tools: [ROCK](https://github.com/alibaba/ROCK) (sandbox manager) + [iFlow CLI](https://github.com/iflow-ai/iflow-cli) (agent framework)
- Strict environment management to prevent reward hacking via residual artifacts
- Chunked MDP: reward and importance sampling at environment-interaction chunk level
- LLM-as-Judge data validation (ground-truth + no-op checks)
- Model: [iFlow-ROME](https://huggingface.co/FutureLivingLab/iFlow-ROME)
- 📄 [Technical Report](https://arxiv.org/abs/2512.24873) | [ROLL Flash](https://arxiv.org/abs/2510.11345) | [ROLLART](https://arxiv.org/abs/2512.22560)

### [RAGEN](https://github.com/mll-lab-nu/RAGEN) ![GitHub stars](https://img.shields.io/github/stars/mll-lab-nu/RAGEN?style=social)
`Python` | Flexible RL framework for training reasoning agents (Northwestern University).

- **StarPO** framework (State-Thinking-Action-Reward Policy Optimization) for unified multi-turn agent RL
- V2: **Reasoning Collapse diagnostics** + SNR-Adaptive Filtering for stable training
- 10 built-in environments (Sokoban, WebShop, DeepCoder, Lean, Sudoku, etc.)
- Gym-compatible interface for custom environments
- 🏫 Northwestern University (Jiajun Wu, Fei-Fei Li, Yejin Choi, Kyunghyun Cho)
- 📄 [Paper V1](https://arxiv.org/abs/2504.20073) | [Paper V2](https://ragen-ai.github.io/v2)

### [RLAnything](https://github.com/Gen-Verse/Open-AgentRL) ![GitHub stars](https://img.shields.io/github/stars/Gen-Verse/Open-AgentRL?style=social)
`Python` | Closed-loop RL optimization across terminal, GUI, SWE, and tool-call settings.

- Joint optimization of policy, reward model, and environment in a closed loop
- Step-wise reward signals from optimized reward model outperform outcome-only human labels
- Automatic environment adaptation via critic feedback from both policy and reward model
- Released policy models (RLAnything-7B/8B) and reward models (RLAnything-Reward-8B/14B)
- 📄 [Paper](https://arxiv.org/abs/2602.02488) | [Models](https://huggingface.co/collections/Gen-Verse/open-agentrl)

### [DemyAgent](https://github.com/Gen-Verse/Open-AgentRL) ![GitHub stars](https://img.shields.io/github/stars/Gen-Verse/Open-AgentRL?style=social)
`Python` | Agentic RL with deliberative reasoning — even 4B models outperform 32B.

- Systematic study across data, algorithms, and reasoning modes for agentic RL
- Real end-to-end trajectories + high-diversity datasets significantly outperform synthetic data
- Exploration-friendly techniques: reward clipping + entropy maintenance
- Deliberative reasoning with selective tool calls surpasses frequent invocation or verbose self-reasoning
- DemyAgent-4B beats 32B models on AIME2024/2025, GPQA-Diamond, LiveCodeBench-v6
- High-quality released data: 3K SFT + 30K RL samples
- 📄 [Paper](https://arxiv.org/abs/2510.11701) | [Model](https://huggingface.co/Gen-Verse/DemyAgent-4B)

### [SkyRL-Agent](https://github.com/NovaSky-AI/SkyRL) ![GitHub stars](https://img.shields.io/github/stars/NovaSky-AI/SkyRL?style=social)
`Python` | Efficient multi-turn, long-horizon agent RL training (UC Berkeley).

- Optimized asynchronous pipeline dispatcher (1.55x speedup over naive async batching)
- AST-based search tool for code navigation during rollout
- Backend interoperability with veRL, Tinker, and other RL frameworks
- SA-SWE-32B: 39.4% Pass@1 on SWE-Bench Verified with 2x+ cost reduction
- 🏫 UC Berkeley Sky Computing Lab (Ion Stoica, Matei Zaharia, Joseph Gonzalez)
- 📄 [Paper](https://arxiv.org/abs/2511.16108)

---

## ⚙️ RL Training Infrastructure

Foundational RL training libraries that power the Agentic RL ecosystem.

### [OpenRLHF](https://github.com/OpenRLHF/OpenRLHF) ![GitHub stars](https://img.shields.io/github/stars/OpenRLHF/OpenRLHF?style=social)
`Python` | High-performance, production-ready RLHF framework.

- Ray + vLLM distributed architecture with unified agent-based design
- Algorithms: PPO, REINFORCE++, GRPO, RLOO, DAPO, TIS
- Single-turn and multi-turn agent RL training
- Production-ready (NVIDIA ProRL V2 uses REINFORCE++-baseline)
- 📖 [Documentation](https://openrlhf.readthedocs.io/)

### [veRL](https://github.com/volcengine/verl) ![GitHub stars](https://img.shields.io/github/stars/volcengine/verl?style=social)
`Python` | Flexible and efficient RL training library (ByteDance).

- Hybrid-Controller programming model for flexible RL dataflows
- Integrates FSDP, Megatron-LM, vLLM, SGLang
- Flexible device mapping across cluster sizes
- HuggingFace model integration
- 📄 [HybridFlow Paper](https://arxiv.org/abs/2409.19256)

### [TRL](https://github.com/huggingface/trl) ![GitHub stars](https://img.shields.io/github/stars/huggingface/trl?style=social)
`Python` | HuggingFace's official RL training library.

- Deep integration with HF ecosystem (Trainer API)
- PPO, DPO, RLOO, GRPO
- Largest community, most comprehensive documentation

### [PRIME](https://github.com/PRIME-RL/PRIME) ![GitHub stars](https://img.shields.io/github/stars/PRIME-RL/PRIME?style=social)
`Python` | Scalable RL with implicit process rewards.

- Implicit PRM training — no process annotations needed
- Integrated into veRL main branch
- Used for process reward normalization in Agent-R1
- 📄 [Paper](https://arxiv.org/abs/2502.01456)

### [Slime](https://github.com/THUDM/slime) ![GitHub stars](https://img.shields.io/github/stars/THUDM/slime?style=social)
`Python` | SGLang-native post-training framework for RL scaling (Tsinghua University).

- Deep integration with SGLang inference engine for native prefix caching support
- Efficient rollout generation with SGLang's optimized serving backend
- 🏫 Tsinghua University (THUDM)

### [AReaL](https://github.com/inclusionAI/AReaL) ![GitHub stars](https://img.shields.io/github/stars/inclusionAI/AReaL?style=social)
`Python` | Efficient RL training with Dynamic Tree Attention (Ant Group).

- **AREAL-DTA**: DFS-based prefix tree traversal for rollout KV cache sharing during training
- Materializes only a single root-to-leaf path at a time — avoids full attention mask
- Load-balanced distributed batching across multiple GPUs
- Up to 8.31x training throughput improvement
- 📄 [Paper](https://arxiv.org/abs/2602.00482)

### [Ray](https://github.com/ray-project/ray) ![GitHub stars](https://img.shields.io/github/stars/ray-project/ray?style=social)
`Python` | Unified distributed AI compute engine.

- Core distributed runtime + AI libraries (Data, Train, Tune, RLlib, Serve)
- **RLlib**: scalable reinforcement learning library
- Powers distributed training in OpenRLHF and many other RL frameworks
- Flexible task parallelism, fault tolerance, and elastic scaling

### [Seer](https://arxiv.org/abs/2511.14617)
Online context learning system for fast synchronous LLM reinforcement learning (Kimi/Moonshot).

- **Divided Rollout**: splits requests into 8K chunks for dynamic load balancing
- **Context-Aware Scheduling**: uses speculative requests to estimate group response lengths
- **Adaptive Grouped Speculative Decoding** with distributed compressed suffix tree
- 74-97% rollout throughput improvement, 75-93% long-tail latency reduction

---

## 🏗️ Agent Infrastructure

Agent orchestration and deployment frameworks (where Agentic RL models are served).

### [LangGraph](https://github.com/langchain-ai/langgraph) ![GitHub stars](https://img.shields.io/github/stars/langchain-ai/langgraph?style=social)
`Python` | Build resilient language agents as graphs.
- Durable execution, human-in-the-loop, comprehensive memory
- Production deployment via LangSmith
- Trusted by Klarna, Replit, Elastic

### [AutoGen](https://github.com/microsoft/autogen) ![GitHub stars](https://img.shields.io/github/stars/microsoft/autogen?style=social)
`Python` | Multi-agent AI framework (Microsoft).
- Multi-agent conversation patterns, MCP tool integration
- AgentTool for nested agent-as-tool patterns
- No-code GUI (AutoGen Studio)

### [CrewAI](https://github.com/crewAIInc/crewAI) ![GitHub stars](https://img.shields.io/github/stars/crewAIInc/crewAI?style=social)
`Python` | Role-driven multi-agent framework.
- Role-based agent definition (Role, Goal, Backstory)
- Sequential / Hierarchical task flows

### [ThunderAgent](https://github.com/Agentic-Kinetics/ThunderAgent) ![GitHub stars](https://img.shields.io/github/stars/Agentic-Kinetics/ThunderAgent?style=social)
`Python` | Program-aware agentic inference system for optimized serving and RL rollout.

- Abstracts agent workflows as **LLM Programs** with unified KV cache / tool / state management
- **State-Aware Pausing**: pauses low-priority programs under memory pressure, releases KV cache
- Hook-based garbage collection + asynchronous environment preparation
- 1.5-3.6x throughput in serving, 1.8-3.9x in RL rollout, up to 4.2x disk memory savings
- 📄 [Paper](https://arxiv.org/abs/2602.13692)

### [OpenClaw](https://github.com/openclaw/openclaw) ![GitHub stars](https://img.shields.io/github/stars/openclaw/openclaw?style=social)
`TypeScript` | Personal AI assistant platform.
- Single-user, local-first, 20+ channels (WhatsApp/Telegram/Discord/Feishu...)
- Skill system, persistent memory, sub-agent orchestration
- The primary target platform for OpenClaw-RL and MetaClaw

---

## 📊 Comparison Matrix

| Project | Stars | Language | Core Focus | Key Differentiator |
|---------|-------|----------|------------|-------------------|
| **OpenClaw-RL** | ![GitHub stars](https://img.shields.io/github/stars/Gen-Verse/OpenClaw-RL?style=flat) | TS | Conversation → RL for OpenClaw | Fully async, zero labeling, 3 learning paradigms |
| **MetaClaw** | ![GitHub stars](https://img.shields.io/github/stars/aiming-lab/MetaClaw?style=flat) | Python | Meta-learning + continual evolution | No GPU needed, smart scheduler, skill injection |
| **Claw-R1** | ![GitHub stars](https://img.shields.io/github/stars/AgentR1/Claw-R1?style=flat) | Python | RL middleware for general agents | White-box/black-box decoupling, zero intrusion |
| **Agent-R1** | ![GitHub stars](https://img.shields.io/github/stars/AgentR1/Agent-R1?style=flat) | Python | End-to-end agent RL training | Tool environment abstraction, process rewards |
| **rLLM** | ![GitHub stars](https://img.shields.io/github/stars/rllm-org/rllm?style=flat) | Python | Full-stack language agent RL | AgentWorkflowEngine, multiple SOTA models |
| **OpenRLHF** | ![GitHub stars](https://img.shields.io/github/stars/OpenRLHF/OpenRLHF?style=flat) | Python | General RLHF infrastructure | Ray+vLLM, production-ready, comprehensive algorithms |
| **veRL** | ![GitHub stars](https://img.shields.io/github/stars/volcengine/verl?style=flat) | Python | LLM RL training library | HybridFlow, flexible dataflows |
| **TRL** | ![GitHub stars](https://img.shields.io/github/stars/huggingface/trl?style=flat) | Python | HF official RL library | Largest community, HF ecosystem integration |
| **PRIME** | ![GitHub stars](https://img.shields.io/github/stars/PRIME-RL/PRIME?style=flat) | Python | Implicit process reward RL | No annotation PRM, integrated into veRL |
| **ROLL** | ![GitHub stars](https://img.shields.io/github/stars/alibaba/ROLL?style=flat) | Python | Terminal agent RL training | Async pipeline, strict env management, chunked MDP |
| **RAGEN** | ![GitHub stars](https://img.shields.io/github/stars/mll-lab-nu/RAGEN?style=flat) | Python | Reasoning agent RL (StarPO) | Reasoning collapse diagnostics, 10+ environments |
| **SkyRL-Agent** | ![GitHub stars](https://img.shields.io/github/stars/NovaSky-AI/SkyRL?style=flat) | Python | Efficient multi-turn agent RL | Async dispatcher, AST-based tool, backend interoperability |
| **Slime** | ![GitHub stars](https://img.shields.io/github/stars/THUDM/slime?style=flat) | Python | SGLang-native RL post-training | Native SGLang integration, prefix caching |
| **AReaL** | ![GitHub stars](https://img.shields.io/github/stars/inclusionAI/AReaL?style=flat) | Python | Efficient RL with Tree Attention | DFS-based prefix tree, 8.31x throughput |
| **RLAnything** | ![GitHub stars](https://img.shields.io/github/stars/Gen-Verse/Open-AgentRL?style=flat) | Python | Closed-loop agentic RL | Joint policy+reward+env optimization |
| **DemyAgent** | ![GitHub stars](https://img.shields.io/github/stars/Gen-Verse/Open-AgentRL?style=flat) | Python | Deliberative agentic RL | 4B beats 32B, exploration-friendly techniques |
| **Ray** | ![GitHub stars](https://img.shields.io/github/stars/ray-project/ray?style=flat) | Python | Distributed AI compute engine | RLlib, powers OpenRLHF and many RL frameworks |

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
8. **KV Cache Management & Sharing** — Cross-request prefix sharing, global cache pools, and program-aware scheduling (ThunderAgent, ForgeRL, Seer)
9. **Reasoning Collapse in Agent RL** — Diagnosing and mitigating template collapse during multi-turn agent training (RAGEN V2)
10. **Environment Isolation & Integrity** — Preventing reward hacking through strict sandbox management and residual artifact cleanup (ROLL, ThunderAgent)

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
- [ROLL: Agentic RL in Terminal Environments](https://arxiv.org/abs/2512.24873)
- [RAGEN: Understanding Self-Evolution in LLM Agents via Multi-Turn RL](https://arxiv.org/abs/2504.20073)
- [SkyRL-Agent: Efficient RL Training for Multi-turn LLM Agent](https://arxiv.org/abs/2511.16108)
- [ThunderAgent: Program-Aware Agentic Inference System](https://arxiv.org/abs/2602.13692)
- [Seer: Online Context Learning for Fast Synchronous LLM RL](https://arxiv.org/abs/2511.14617)
- [AREAL-DTA: Dynamic Tree Attention for Efficient RL](https://arxiv.org/abs/2602.00482)
- [RLAnything: Closed-loop RL Optimization](https://arxiv.org/abs/2602.02488)
- [ProRL Agent: Rollout-as-a-Service for RL Training of Multi-Turn LLM Agents](https://arxiv.org/abs/2603.18815)
- [DemyAgent: Agentic RL with Deliberative Reasoning](https://arxiv.org/abs/2510.11701)

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
