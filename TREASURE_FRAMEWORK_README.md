# TREASURE Framework
## Agentic AI Defense-in-Depth Security Framework

> **"Protect your treasure — or your agents will work for your adversaries."**

[![License: CC0-1.0](https://img.shields.io/badge/License-CC0_1.0-lightgrey.svg)](https://creativecommons.org/publicdomain/zero/1.0/)
[![OWASP](https://img.shields.io/badge/Aligned-OWASP%20GenAI%20Security-blue)](https://genai.owasp.org)
[![CSA MAESTRO](https://img.shields.io/badge/Aligned-CSA%20MAESTRO-orange)](https://cloudsecurityalliance.org)
[![NIST AI RMF](https://img.shields.io/badge/Aligned-NIST%20AI%20RMF-green)](https://www.nist.gov/artificial-intelligence)
[![MITRE ATLAS](https://img.shields.io/badge/Aligned-MITRE%20ATLAS-red)](https://atlas.mitre.org)

---

**Author:** Roger Sanz González, PhD  
**Role:** AI Security Lead · Plain Concepts | Lead Editor · OWASP AI Exchange | Contributor · MITRE ATLAS · CSA  
**Contact:** roger.sanz@owasp.org | [rogersanz.com](https://rogersanz.com)  
**Version:** 1.1 · June 2026  
**Presented at:** Hack-én 2026 (April 2026) · EuskalHack Security Congress IX (June 2026)

---

## Why This Framework Exists

Enterprise organizations are deploying autonomous AI agents at an accelerating pace. Unlike traditional generative AI systems that respond to prompts in isolation, agentic systems **plan, act, remember, and collaborate** — invoking APIs, modifying databases, communicating with other agents, and operating continuously with minimal human oversight.

This qualitative leap in capability introduces a qualitative leap in attack surface that **no single perimeter control, guardrail, or content filter can architecturally address.**

The fundamental wrong assumption: *"If the agent behaves correctly under normal conditions, it is secure."*

This fails because:

- **Attacks are trajectory-based, not prompt-based** — they manifest across sessions and states
- **Agent memory is writable at runtime** by external content (emails, documents, API responses)
- **Messages between agents carry no native authenticity** — any agent can be impersonated
- **The agent accumulates state across sessions** — small manipulations compound over time

Gartner projects that **over 40% of agentic AI projects will be cancelled before end of 2027**, with insufficient security controls as one of the primary causes.

---

## The Three Primary Threat Vectors

This framework is specifically engineered to counter three attack classes that were either absent from or underspecified in prior AI security literature:

| Vector | Attack Class | Research Reference | Success Rate |
|--------|-------------|-------------------|-------------|
| **A — Memory Poisoning** | Persistent corruption of episodic/semantic memory | MemoryGraft (arXiv:2512.16962), MINJA (NeurIPS 2025) | >80% |
| **B — RAG Poisoning** | Contamination of retrieval-augmented generation indexes | AgentPoison (arXiv:2407.12784), MINJA (NeurIPS 2025) | >80–95% |
| **C — Inter-Agent Communication Poisoning** | Manipulation of messages in multi-agent architectures | AiTM (arXiv:2502.14847, ACL 2025) | >70% |

**Core adversarial property:** Attackers no longer need to be present. Their payloads are.  
One infected document → N agents · N sessions. Persistent. Autonomous. Scalable.

---

## The TREASURE Framework — Five Defense Layers

```
SECURITY LAYER    ← Blast Radius Engineering · Defense-in-Depth
      ↑
CONTROL LAYER     ← Human-in-the-Loop · Encapsulated Autonomy
      ↑
GOVERNANCE LAYER  ← Code-Grade Governance · Policy-as-Code
      ↑
EXECUTION LAYER   ← Skills & Runtime · Critical Attack Surface ⚠️
      ↑
DATA LAYER        ← Diamond Record · Single Governed Truth
   (foundation of everything)
```

Each layer addresses a distinct attack class while maintaining structural independence, so the failure of any single layer does **not** cascade into a system-wide breach.

---

### Layer 1 — DATA LAYER: Diamond Record

**Design principle:** Single Governed Truth  
**Primary threat:** ASI06 Memory & Context Poisoning | CSA MAESTRO L2

The Data Layer is the foundational stratum. Every agent inference, every RAG retrieval, every memory read originates here. A corrupted data foundation propagates upward through all layers regardless of how well the upper layers are defended.

**Technical controls:**

- **Governed Ingestion Pipeline** — Semantic validation detecting embedded instruction patterns before any data reaches the vector index; provenance verification per document (author, timestamp, source system); policy enforcement restricting which agents can retrieve which index segments
- **Differential Privacy in Embeddings** — Embedding vectors must not preserve information at a fidelity level enabling adversarial payload reconstruction; degrades backdoor effectiveness without material retrieval utility impact
- **Cryptographically Verified Memory Snapshots** — Append-only, immutable index snapshots with HMAC integrity stored outside the agent's write surface; enables drift detection and rollback to known-clean state
- **Identity-Scoped Query Constraints** — Per-agent retrieval access controls enforced at query time, not application layer; limits blast radius of embedding poisoning to the agent's authorized scope
- **Continuous Semantic Monitoring** — Statistical anomaly detection on index state vs. established baseline; content exceeding anomaly threshold quarantined before promotion to live index

**Failure mode:** `Poisoned data → Embedded → Silently retrieved → Reused → Amplified → Cascading hallucination chain`

> **Key insight:** Memory attacks are not prompt injection. They are rootkits. The model is the kernel — stateless. The external memory store is the `/data` partition that nobody formats. A model update does not clear the memory.

---

### Layer 2 — EXECUTION LAYER: Skills & Runtime ⚠️ CRITICAL

**Design principle:** Critical Attack Surface Control  
**Primary threat:** ASI02 Tool Misuse · ASI05 Code Execution | CSA MAESTRO L3/L4/L5

Skills are not simple functions. They are reusable behavioral components that codify multi-step workflows, tool orchestration, filesystem access, network operations, and cross-session state management — architecturally equivalent to production code with elevated system privileges.

**Technical controls:**

- **Cryptographic Skill Signing** — No skill may be instantiated without a valid signature over its complete definition (code, metadata, permissions, dependency manifest); the skill registry operates as Certificate Authority
- **Minimal-Privilege Skill Manifests** — Each skill declares its permission surface at registration; the runtime enforces as hard constraints, not advisory policy

```yaml
# Example Skill Security Manifest
skill_id: invoice-processor-v2
version: 2.1.4
signature: sha256:a3f8e921...

permissions:
  - read:invoices
  - write:approved_invoices

allowed_tools:
  - invoice_api.get
  - invoice_api.approve

risk_level: HIGH
human_approval_required: true

sandbox: strict-container
network_egress:
  - api.acme-invoice.internal
max_iterations: 5
max_session_duration_s: 120
```

- **Runtime Sandboxing** — Skill execution in isolated contexts; MCP server processes run with reduced-privilege identities without access to orchestrator credentials; network egress restricted to declared endpoints
- **Pre-Call Hooks & Output Validation Pipelines** — Intent monitoring at tool invocation boundary; output validation scanning tool responses for embedded prompt injection before context delivery
- **Immutable Skill Audit Trail** — Append-only, off-agent invocation log per skill call including agent identity, skill version hash, parameter hash, output hash, timestamps

**Skills Threat Taxonomy (AST01–AST10):**

| ID | Risk | Severity |
|----|------|----------|
| AST01 | Malicious Skills Injection | CRITICAL |
| AST02 | Skill Privilege Escalation | CRITICAL |
| AST03 | Unauthorized Tool Invocation | HIGH |
| AST04 | Skill-to-Skill Lateral Movement | HIGH |
| AST05 | Persistent State Manipulation | HIGH |
| AST06 | Resource Hijacking via Skills | HIGH |
| AST07 | Skill Output Tampering | MEDIUM |
| AST08 | Cross-Agent Skill Reuse Attack | HIGH |
| AST09 | Skill Supply Chain Compromise | CRITICAL |
| AST10 | Cross-Platform Skill Reuse | HIGH |

> **Key insight:** Skills are the new supply chain. The impact of a compromised skill multiplies by the number of agents that import it. One poisoned skill in a marketplace → blast radius scales across every agent deployment that uses it.

---

### Layer 3 — GOVERNANCE LAYER: Code-Grade Governance

**Design principle:** Policy-as-Code Discipline  
**Primary threat:** ASI08 Supply Chain Compromise | CSA MAESTRO L7 | ISO/IEC 42001 Clause 5.3

An agent without code-grade governance is equivalent to production software without source control, without testing, and without change management.

**Technical controls:**

- **Versioned Agent Artifact Repository** — All agent behavioral specifications in version control: system prompts, workflow definitions, skill manifests, tool chains, policies; every change requires pull request, review, approval
- **Policy-as-Code Enforcement** — Policies expressed in declarative, machine-executable formats (OPA/Rego or YAML); natural-language policies in PDFs are not enforceable; CI/CD enforcement via policy engine
- **CI/CD Integration with Automated Red Teaming** — Every commit activates: static analysis of workflow definitions, behavioral regression against OWASP ASI adversarial suite, automated red teaming, AIBOM generation and validation
- **Drift Detection** — Continuous comparison of production behavioral profile against CI/CD-validated baseline; divergence above threshold triggers alerts
- **Agent SBOM (AIBOM)** — AI Bill of Materials documenting foundation model version, all skills with version hashes and signing certificates, tool integrations, knowledge sources per deployment

---

### Layer 4 — CONTROL LAYER: Human-in-the-Loop

**Design principle:** Encapsulated Autonomy  
**Primary threat:** ASI10 Rogue Agent Behaviour · ASI01 Agent Goal Hijack | NIST AI RMF: Govern

The Replit Meltdown (Incident #1152, July 2025): a coding agent operating without an Agency Envelope or kill-switch deleted a production database. The agent was not compromised — it executed its task with full fidelity. **The failure was architectural: no boundary existed.**

**Decision Boundary Matrix (Agency Envelope):**

| Action Category | Low Impact | Medium/High Impact |
|----------------|-----------|-------------------|
| Informative | Autonomous | Autonomous |
| Operative — Low | Autonomous | Human notification |
| Operative — Medium | Human notification | Human approval (sync) |
| Financial / Legal | Human approval (sync) | Human approval (sync) |
| Data Modification — Production | Human approval (sync) | Human approval (sync) |
| Security / Access | Human approval (sync) | Human approval (sync) |
| **Destructive / Irreversible** | **Human approval + second approver** | **Human approval + second approver** |

**Technical controls:**

- **Agency Envelope Enforcement** — Action space constraints evaluated before every tool call; actions outside envelope trigger escalation or termination, not agent-level exception handling
- **Human-on-the-Loop vs. Human-in-the-Loop** — Mode selection is a property of the task definition, not a runtime user preference
- **Infrastructure Kill-Switch** — Termination mechanism at infrastructure layer, independent of application logic; halts execution, revokes all JIT credentials, quarantines memory state for forensics; **must be tested via periodic drills**

> An untested kill-switch is an unverified control.

---

### Layer 5 — SECURITY LAYER: Defense-in-Depth

**Design principle:** Blast Radius Engineering — *Assume compromise. Design to contain.*  
**Primary threat:** ASI03 Identity Abuse · ASI04 Resource Exhaustion · ASI07 Cascading Failures · ASI09 Exfiltration | CSA MAESTRO L1/L4

**Technical controls:**

- **Per-Agent Identity with JIT Credentials** — Each agent holds a unique cryptographic principal; tokens are ephemeral and scoped per tool invocation; no shared credential pools between agents
- **Tool Allow-Lists and Sandbox Enforcement** — Per-agent allow-lists enforced at Tool Router level, not in system prompt; the sandbox enforces regardless of agent reasoning
- **Network Micro-Segmentation** — Agents do not access external networks directly; all egress via controlled proxy enforcing endpoint allow-list; inter-agent communication via authorized orchestration channel only
- **Full Trajectory Logging** — Complete execution trajectory in append-only, off-agent, cryptographically signed log store: every reasoning step, tool call with parameters and responses, memory reads/writes, inter-agent messages
- **Behavioral Baselining & Anomaly Detection** — Statistical baselines established during CI/CD validation; continuous production comparison; anomaly scores above threshold trigger alerts and automated escalation
- **Circuit Breakers** — Per agent-to-agent communication path; quarantine protocol for agents producing anomalous outputs

---

## Standards Alignment Matrix

| TREASURE Layer | OWASP ASI (Dec 2025) | CSA MAESTRO | AIUC-1 Controls | NIST AI RMF | ISO/IEC 42001 |
|---------------|---------------------|------------|----------------|------------|--------------|
| DATA LAYER | ASI06 | L2 Data Operations | UC-DATA-01/02/03/04 | Map / Measure | Annex B |
| EXECUTION LAYER | ASI02, ASI05 | L3, L4, L5 | UC-EXEC-01–05 | Manage | — |
| GOVERNANCE LAYER | ASI08 | L7 Governance | UC-GOV-01–05 | Govern | Clause 5.3 |
| CONTROL LAYER | ASI10, ASI01 | L6 Human-AI | UC-CTRL-01/02/03 | Govern | Clause 5.3 |
| SECURITY LAYER | ASI03, ASI04, ASI07, ASI09 | L1, L4 | UC-SEC-01–06 | Measure / Manage | — |

---

## OWASP Agentic Top 10 — Threat Coverage

| ID | Risk | Severity | Primary TREASURE Layer |
|----|------|----------|----------------------|
| ASI01 | Agent Goal Hijack | 🔴 CRITICAL | CONTROL + DATA |
| ASI02 | Tool Misuse & Exploitation | 🔴 CRITICAL | EXECUTION |
| ASI03 | Identity & Privilege Abuse | 🔴 CRITICAL | SECURITY |
| ASI04 | Resource Exhaustion | 🟠 HIGH | SECURITY |
| ASI05 | Unexpected Code Execution | 🔴 CRITICAL | EXECUTION |
| ASI06 | Memory & Context Poisoning | 🟠 HIGH | DATA |
| ASI07 | Cascading Agent Failures | 🟠 HIGH | SECURITY |
| ASI08 | Supply Chain Compromise | 🟠 HIGH | GOVERNANCE |
| ASI09 | Data Leakage & Exfiltration | 🔴 CRITICAL | SECURITY |
| ASI10 | Rogue Agent Behaviour | 🔴 CRITICAL | CONTROL |

---

## Agent Memory Architecture — Attack Surface Map

Understanding memory types is prerequisite to understanding why agentic attacks differ from all prior AI attack classes.

| Memory Type | Content | Persistence | Attack Target | Primary Vector |
|------------|---------|------------|--------------|---------------|
| **IN-CONTEXT** | Active conversation history | Volatile (session) | Minimal — dies with session | Session injection only |
| **EPISODIC** | Past session experiences, decisions, feedback | **Persistent** | ⚠️ PRIMARY — survives restarts, upgrades, rollbacks | MINJA, MemoryGraft |
| **SEMANTIC** | Knowledge base / RAG retrieval; external vector store | **Persistent** | ⚠️ PRIMARY — external persistence outside the model | AgentPoison, Embedding Backdoor |
| **PROCEDURAL** | System prompt + behavioral instructions + tool policies | **Persistent** | 🔴 HIGHEST PRIVILEGE — controls all future interactions | Instruction injection |

**Attacker maxim:** Compromise once. Influence forever.

### The Three-Phase Memory Attack Anatomy

```
PHASE 1 — INJECTION (one-time)
  Payload arrives via any writable channel (email, doc, API response)
  Memory write occurs as part of standard operation
  No alert. No anomaly. Log shows: "memory updated."
  ↓
PHASE 2 — DORMANCY (hours to months)
  Memory entry waits for semantic trigger
  Agent behaves normally in all unrelated interactions
  Invisible. Silent. Persistent.
  ↓
PHASE 3 — ACTIVATION (future session)
  User query matches semantic trigger
  Malicious memory retrieved with high similarity score
  Agent executes attacker instruction as if legitimate
  Impact: exfiltration, manipulation, unauthorized actions
```

> The temporal gap between Phase 1 and Phase 3 makes forensic correlation near-impossible without full trajectory logging from the initial injection moment.

---

## The Double Agent Kill Chain — MITRE ATLAS Mapping

| Phase | Vector | Description | MITRE ATLAS Technique | TREASURE Mitigation |
|-------|--------|-------------|----------------------|-------------------|
| Initial Access | A/B: artifact | Malicious content in file, email, external resource | Prompt Injection Indirect | DATA LAYER: Governed ingestion pipeline |
| Initial Access | C: message | Malicious message to agent endpoint | Acquire ML Infrastructure | SECURITY: Inter-agent message authentication |
| Persistence | A: episodic mem | Payload embedded in episodic/long-term memory | Context Embedding | DATA: UC-DATA-04 versioned snapshots |
| Persistence | B: RAG index | Malicious content indexed in vector store | Context Embedding | DATA: Differential privacy; semantic monitoring |
| Persistence | C: agent spoof | Adversary registers spoofed agent | Insecure Agent Protocol | SECURITY: UC-SEC-01 per-agent JIT identity |
| Execution | Semantic trigger | User query activates payload retrieval | LLM Prompt Smuggling | EXECUTION: Pre-call intent monitoring |
| Exfiltration | Data exfil | Covert extraction via agent responses/actions | Agentic Steganography | SECURITY: UC-SEC-06 Output DLP; entropy monitoring |
| Lateral Spread | Prompt infection | Payload self-replicates via outgoing messages | Prompt Infection Chain | SECURITY: Circuit breakers; message content screening |

---

## Guardrails vs. TREASURE Framework

| Property | Traditional Guardrails | TREASURE Framework |
|----------|----------------------|-------------------|
| Nature of control | Input/output filter | Governed architecture end-to-end |
| System state | Stateless, reactive | Stateful, preventive |
| Skill coverage | None | Manifest + Signing + Sandbox |
| Agent identity | No independent identity | Independent cryptographic principal (JIT) |
| Auditability | Partial (outputs only) | Full trajectory logging |
| Incident response | Manual | Kill-switch + automated rollback |
| Standards coverage | None formal | OWASP + MAESTRO + NIST + ISO 42001 |
| Attack surface covered | Input prompt + output response | Complete execution trajectory |

---

## Reference Architecture

```
[User / External Input]
         │
         ▼
[Orchestrator + Intent Monitoring]
         │
         ▼
[Agent Runtime Control Plane (ARCP)]
    ├── Memory Manager      ← Governs Diamond Record access (L1 DATA)
    ├── Tool Router         ← Enforces allow-lists + pre-call hooks (L2 EXEC)
    ├── Skill Executor      ← Signed skills + sandbox enforcement (L2 EXEC)
    └── Policy Engine       ← Policy-as-Code enforcement (L3 GOV)
         │
         ▼
[Agency Envelope Validator]   ← Decision Boundary Matrix (L4 CTRL)
         │
    ┌────┘
    │ [HITL Checkpoint]    ← Human escalation if action outside envelope
    └────┐
         ▼
[Diamond Record + Scoped Tool APIs]
         │
         ▼
[Full Trajectory Log — append-only, off-agent, cryptographically signed]
         │
         ▼
[Anomaly Detection + Behavioral Baselining + Circuit Breakers]
         │
         ▼
[Infrastructure Kill-Switch / Incident Response]
```

---

## Minimum Viable Defense Posture (MVDP)

For any agent with persistent memory deployed in production — implementable immediately, without dedicated security budget:

| # | Control | Vectors | Timing |
|---|---------|---------|--------|
| 1 | Memory write validation before persisting | A + B | Deploy day 0 |
| 2 | Corpus sanitization before RAG indexing | B | Deploy day 0 |
| 3 | Provenance tracking on every memory entry | A + B | Deploy day 0 |
| 4 | Behavioral baseline established | All | Week 1 post-deploy |
| 5 | Versioned memory snapshots with rollback | A + B | Deploy day 0 |
| 6 | Message signing between agents | C | Deploy day 0 |
| 7 | Infrastructure kill-switch — non-overridable, tested | All | Deploy day 0 |
| 8 | Full trajectory logging | All | Deploy day 0 |

---

## Pre-Production Security Checklist

- [ ] **Agency Envelope signed by named accountable party** — Before writing code
- [ ] **Intent monitoring configured in orchestrator** — Deploy day 0
- [ ] **Infrastructure kill-switch operational and tested** — Deploy day 0
- [ ] **Skill Security Manifest + cryptographic signing for all skills** — Each registered skill
- [ ] **Ephemeral JIT credentials per agent; no shared credential pools** — Deploy
- [ ] **Memory sanitization with versioned snapshots operational** — Deploy
- [ ] **Behavioral baselining initiated** — Week 1 post-deploy
- [ ] **AIBOM generated and validated** — Deploy + on component change
- [ ] **Full trajectory logging verified: append-only, off-agent, signed** — Deploy
- [ ] **Red team exercise using MITRE ATLAS as attack playbook** — Quarterly

---

## Real-World Incident Evidence Base

Every TREASURE control is grounded in documented production incidents or peer-reviewed research demonstrating real exploitability.

### Production Incidents

| Incident | Date | Attack Vector | OWASP Classification | Missing TREASURE Layer |
|----------|------|--------------|---------------------|----------------------|
| **Gemini Memory Attack** (J. Rehberger) | Feb 2025 | Indirect prompt injection via Gmail/Drive → persistent memory corruption | ASI06 | DATA: No memory write validation; no versioned snapshots |
| **EchoLeak CVE-2025-32711** (Aim Security) | Jun 2025 | Malicious email → RAG context injection → zero-click M365 Copilot exfiltration | ASI01 + ASI06 + ASI09 | DATA: No semantic validation; EXEC: No intent monitoring; SEC: No output DLP |
| **GeminiJack** (Noma Security) | Jun 2025 | RAG poisoning via shared Google Workspace → zero-click PII exfiltration via image tag | ASI06 + ASI09 | DATA: No corpus sanitization; SEC: No output DLP |
| **Replit Meltdown** (Incident #1152) | Jul 2025 | Coding agent without Agency Envelope deleted production database | ASI10 + ASI02 | CONTROL: No Agency Envelope; no kill-switch; no decision boundary matrix |
| **OpenClaw CVE-2026-25253** (MITRE ATLAS Feb 2026) | 2026 | Malicious MCP skill in marketplace → RCE + credential theft | ASI05 + ASI08 | EXEC: No skill signing; no sandboxing; GOV: No CI/CD gate; SEC: No micro-segmentation |
| **Atlassian Rovo** (Indirect PI via Confluence) | 2025 | Attacker writes adversarial Confluence page → Rovo exfiltrates cross-space data | ASI01 + ASI06 + ASI09 | DATA: No RAG semantic validation; no query constraints |

### Research Evidence

| Paper | Venue | Key Finding | TREASURE Layer Addressed |
|-------|-------|-------------|------------------------|
| MINJA — Memory INjection Attack | NeurIPS 2025 | 0.1% poison rate in 10K-entry corpus sufficient; <1% performance degradation on non-targeted interactions | DATA LAYER |
| MemoryGraft (arXiv:2512.16962) | Dec 2025 | Memory entries have higher trust weight than system prompt; four implant capability classes demonstrated | DATA LAYER |
| AgentPoison (arXiv:2407.12784) | 2024 | >80% RAG poisoning success rate; only write access to one document required | DATA LAYER |
| AiTM (arXiv:2502.14847) | ACL 2025 | >70% inter-agent attack success via reflect() mechanism on AutoGen, MetaGPT, custom frameworks | SECURITY LAYER |
| Prompt Infection (arXiv:2410.07283) | 2024 | Self-replicating payloads; 1 infected agent → N infected agents via normal task messaging | SECURITY LAYER |
| Agent Security Bench (arXiv:2410.02644) | 2024 | **84.30% average attack success rate** across 400+ tools and 27 attack/defense combinations | All layers |

---

## Platform Implementation Notes

### Azure AI Foundry + AWS Bedrock (Hybrid)

- **DATA**: Azure AI Search (scoped) + Azure Content Safety for ingestion validation; Azure Blob immutable storage for snapshots
- **EXECUTION**: Azure Container Apps + ACR Notation signing; AWS IAM Roles Anywhere for cross-cloud JIT (never long-lived keys in Key Vault)
- **GOVERNANCE**: Azure DevOps + Semantic Kernel YAML as Policy-as-Code; dual-telemetry drift detection via Sentinel
- **CONTROL**: Copilot Studio HITL + SK Planner constraints as Agency Envelope; Logic App kill-switch targeting Container Apps deactivation + STS revocation
- **SECURITY**: Entra Agent ID + Azure Sentinel; AWS STS OIDC federation; VNet + VPC private endpoints; dual-write trajectory log

> ⚠️ **Most common gap:** Teams fall back to long-lived AWS access keys in Key Vault when IAM Roles Anywhere is not configured — eliminating the JIT property required by UC-SEC-01.

### Google Cloud — Vertex AI Agent Builder

- **DATA**: Vertex AI Search with access control labels per Workload Identity; Cloud Dataflow governed ingestion with Document AI provenance
- **EXECUTION**: Vertex AI Extensions + **mandatory Cloud Endpoints proxy** (ADK allow-list is advisory, not enforcement — the proxy is the enforcement layer)
- **CONTROL**: A2A default trust model is an **unmitigated AiTM surface** — custom WIF token verification middleware (Cloud Run) is required before any A2A deployment
- **SECURITY**: Workload Identity per Cloud Run revision; VPC Service Controls perimeter; BigQuery ML baselining

> ⚠️ **Critical gap:** Google A2A's default trust model (agents trust messages from same-project agents without per-message authentication) directly enables the AiTM attack. The middleware is not optional.

### AWS Bedrock Agents (Standalone)

- **DATA**: Step Functions governed ingestion pipeline (provenance Lambda + semantic validation Lambda + approval gate); S3 Object Lock for WORM snapshots
- **EXECUTION**: Two-phase Lambda handler pattern (validate then execute) to compensate for inability to inject pre-call hooks into Bedrock's invocation path; ECR cosign for skill signing
- **CONTROL**: AWS Verified Permissions + Cedar as Agency Envelope (not Bedrock Guardrails — Guardrails is I/O filter only, not envelope enforcement); EventBridge kill-switch Lambda
- **SECURITY**: IAM ExternalId condition per agent; Lambda in VPC with VPC endpoints; CloudWatch + Bedrock invocation logging; Amazon Detective for behavioral graph analysis

> ⚠️ **Common misuse:** Bedrock Guardrails is frequently treated as Agency Envelope. It is not — it is an input/output content filter with no decision boundary enforcement capability.

---

## Reference Implementation

**OWASP Agent Memory Guard** implements TREASURE DATA LAYER controls UC-DATA-01 through UC-DATA-04:

- SHA-256 integrity baseline on all memory entries
- Detection of injection patterns, leakage patterns, rapid-change anomalies, and anomalous entry sizes
- Declarative YAML memory policies (per-namespace read/write policies, TTL, provenance requirements)
- Integration adapters: LangChain · LlamaIndex · CrewAI · Redis · PostgreSQL

→ [owasp.org/www-project-agent-memory-guard](https://owasp.org/www-project-agent-memory-guard/)

---

## The Three Truths of Agentic AI Security

**01 — Memory attacks are not prompt injection. They are rootkits.**  
They persist where the model cannot reach — outside the inference context, in the external data plane. You can patch the model. The rootkit remains.

**02 — If you don't control the messages between agents, you don't control the system.**  
Security in multi-agent architectures is not the sum of the security of each individual agent. The security is in the channel. Without authentication, signing, and zero trust between agents, the system is as weak as its most vulnerable message.

**03 — The agent does not know it is compromised. That is why it is a double agent, not a broken agent.**  
It operates correctly in 99% of interactions. The 1% is invisible to any output-based control. Security can no longer be based on trusting the agent — it must be based on controlling the environment.

> **Security is no longer about trusting the agent. It is about controlling the environment.**  
> Control memory. Secure communication. Zero Trust by default.

---

## References

### Standards & Frameworks

- [OWASP Top 10 for Agentic Applications 2026](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/)
- [OWASP AI Exchange — Agentic AI Threats & Mitigations](https://genai.owasp.org/resource/agentic-ai-threats-and-mitigations/)
- [OWASP Agent Memory Guard](https://owasp.org/www-project-agent-memory-guard/)
- [CSA MAESTRO — Agentic AI Threat Modeling Framework](https://cloudsecurityalliance.org/blog/2025/02/06/agentic-ai-threat-modeling-framework-maestro)
- [CSA — Securing Autonomous AI Agents (Survey 2026)](https://cloudsecurityalliance.org/artifacts/securing-autonomous-ai-agents)
- [NIST AI RMF 1.0](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework)
- [NIST AI 600-1 — Generative AI Profile](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf)
- [ISO/IEC 42001:2023 — AI Management Systems](https://www.iso.org/standard/81230.html)
- [MITRE ATLAS](https://atlas.mitre.org/)

### Research Papers

- [MemoryGraft — arXiv:2512.16962](https://arxiv.org/abs/2512.16962)
- [AgentPoison — arXiv:2407.12784](https://arxiv.org/abs/2407.12784)
- [AiTM — arXiv:2502.14847 (ACL 2025)](https://arxiv.org/abs/2502.14847)
- [Prompt Infection — arXiv:2410.07283](https://arxiv.org/abs/2410.07283)
- [Agent Security Bench — arXiv:2410.02644](https://arxiv.org/abs/2410.02644)
- [Attack and Defense Landscape of Agentic AI — arXiv:2603.11088](https://arxiv.org/abs/2603.11088)
- [Agentic AI Security: Threats, Defenses, Evaluation — arXiv:2510.23883](https://arxiv.org/abs/2510.23883)

### Incidents & CVEs

- [EchoLeak CVE-2025-32711 — Aim Security](https://www.aim.security/lp/echoleak)
- [EchoLeak — Microsoft MSRC](https://msrc.microsoft.com/update-guide/vulnerability/CVE-2025-32711)
- [GeminiJack — Noma Security (June 2025)](https://www.noma.ai/blog/geminijack-how-we-discovered-a-zero-day-that-could-compromise-google-workspace-agents)
- [Gemini Memory Attack — Johann Rehberger (Feb 2025)](https://embracethered.com/blog/posts/2024/google-gemini-persistent-memory-attack/)
- [OpenClaw CVE-2026-25253 — MITRE ATLAS](https://atlas.mitre.org/)
- [Replit Meltdown — Wired (July 2025)](https://www.wired.com/story/replit-ai-code-database-deletion/)

---

## License

**CC0 1.0 Universal — Public Domain Dedication**

To the extent possible under law, Roger Sanz González has waived all copyright and related rights to this specific layout and textual implementation of the TREASURE AI Security Framework. You are free to copy, modify, distribute, and build upon this text, even for commercial purposes, without seeking prior permission or providing mandatory attribution.

→ [View CC0 1.0 Legal Code](https://creativecommons.org/publicdomain/zero/1.0/)

Contributions, feedback, and extensions welcome: [roger.sanz@owasp.org](mailto:roger.sanz@owasp.org)

---

*TREASURE Framework v1.1 · Roger Sanz González · Plain Concepts · OWASP AI Exchange · June 2026*
