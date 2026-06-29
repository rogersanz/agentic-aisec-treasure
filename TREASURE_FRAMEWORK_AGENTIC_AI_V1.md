# TREASURE Framework
## Defense-in-Depth Architecture for Agentic AI Systems

> *Tiered Resilient Execution Architecture for Secure Unified Robust Environments*

[![License: CC0-1.0](https://img.shields.io/badge/License-CC0_1.0-lightgrey.svg)](https://creativecommons.org/publicdomain/zero/1.0/)
[![OWASP](https://img.shields.io/badge/Aligned-OWASP%20GenAI%20Security-blue)](https://genai.owasp.org)
[![CSA MAESTRO](https://img.shields.io/badge/Aligned-CSA%20MAESTRO-orange)](https://cloudsecurityalliance.org)
[![NIST AI RMF](https://img.shields.io/badge/Aligned-NIST%20AI%20RMF-green)](https://www.nist.gov/artificial-intelligence)
[![MITRE ATLAS](https://img.shields.io/badge/Aligned-MITRE%20ATLAS-red)](https://atlas.mitre.org)
[![ISO 42001](https://img.shields.io/badge/Aligned-ISO%2FIEC%2042001-blue)](https://www.iso.org/standard/81230.html)
[![Version](https://img.shields.io/badge/Version-1.0-brightgreen)]()

---

**Author:** Roger Sanz, PhD  
**Role:** AI Security Lead — Plain Concepts | Senior Researcher — Universidad Isabel I  
Lead Editor, OWASP AI Exchange | Contributor, MITRE ATLAS · CSA · ISMS Forum · DAMA  
TAISE · CRISC · C|CISO · CCSK · CCZT · ISO 27001/22301/42001 LA  
**Contact:** [roger.sanz@owasp.org](mailto:roger.sanz@owasp.org)  
**Version:** 1.0 · June 2026

---

## Editor's Notice

The TREASURE AI Security Framework is an innovative security framework developed by Roger Sanz, PhD, explicitly designed to address the complex vulnerabilities and risk vectors of Agentic AI systems.

This framework is open to every contributor and practitioner with a clear focus on security research, testing, or interest in the Agentic AI Security scenario evolution. This initial version provides the starting point of the framework's evolution and should be used in a tailored manner depending on the specific organization's scenario. It is intended to complement — not substitute — other frameworks, and takes into account future integrations based on community development.

> **Central principle:** Protect your AgenticAI Security treasure. If you do not govern your agents, they will work for your adversaries.

**Licensing & Rights Notice (CC0 1.0):** To the extent possible under law, the author has waived all copyright and related rights to this specific layout and textual implementation. You are free to copy, modify, distribute, and build upon this text, even for commercial purposes, without seeking prior permission. → [View CC0 1.0 Legal Code](https://creativecommons.org/publicdomain/zero/1.0/)

---

## Executive Summary

Enterprise organizations are deploying autonomous AI agents at an accelerating pace. Unlike traditional generative AI systems that respond to prompts in isolation, agentic systems plan, act, remember, and collaborate across multi-step workflows — invoking APIs, modifying databases, communicating with other agents, and operating continuously with minimal human oversight. This qualitative leap in capability introduces a qualitative leap in attack surface that no single perimeter control, guardrail, or content filter is architecturally capable of addressing.

The TREASURE Framework responds with a five-layer defense-in-depth architecture specifically engineered for the threat model of agentic AI. Each layer addresses a distinct attack class while maintaining structural independence so that the failure of any single layer does not cascade into a system-wide breach. The framework is not a product, a policy template, or a checklist: it is an operational architecture grounded in the adversarial evidence base of 2025–2026.

The core adversarial problem this document addresses is the **double-agent threat**: an autonomous agent that, through memory poisoning, RAG poisoning, or inter-agent communication manipulation, operates against the interests of its legitimate principals while appearing to function normally. Three documented incidents — EchoLeak (CVE-2025-32711), OpenClaw (CVE-2026-25253), and the Replit Meltdown (Incident #1152, July 2025) — demonstrate that this threat class is not theoretical.

---

## Table of Contents

1. [The Agentic AI Threat Landscape](#1-the-agentic-ai-threat-landscape)
2. [TREASURE Framework — Architecture Overview](#2-treasure-framework--architecture-overview)
3. [Layer Technical Specifications](#3-layer-technical-specifications)
4. [OWASP Agentic Top 10 — Complete Mapping](#4-owasp-agentic-top-10--complete-mapping)
5. [CSA MAESTRO Integration](#5-csa-maestro-integration)
6. [AIUC-1, GUARD, and AI DEFEND — Technical Alignment](#6-aiuc-1-owasp-ai-exchange-guard-and-ai-defend--technical-alignment)
7. [Platform Implementation Examples](#7-platform-implementation-examples)
8. [Reference Architecture](#8-reference-architecture)
9. [Empirical Evidence Base](#9-empirical-evidence-base)
10. [Implementation Roadmap](#10-implementation-roadmap)
11. [Real-World Attack Case Studies](#11-real-world-attack-case-studies)
- [Appendix A: Detailed AIUC-1 Control Mapping](#appendix-a-detailed-aiuc-1-control-by-control-mapping)
- [References](#references)

---

## 1. The Agentic AI Threat Landscape

### 1.1 Why Traditional Security Fails

Conventional cybersecurity operates on a stateless, perimeter-first model: identify the boundary, filter inputs, validate outputs. Agentic AI systems break every one of these assumptions simultaneously.

An autonomous agent is a distributed cognitive system: the agent itself is a service; each skill is a function or Lambda; memory is a database with read/write semantics; tools are external APIs with real-world side effects; the orchestrator is a workflow engine with branching logic. The attack surface scales accordingly.

Guardrails cover only the first and last points of a trajectory that may span dozens of intermediate steps. Everything between the initial prompt and the final response — tool calls, memory reads and writes, skill invocations, inter-agent communications, state modifications — is entirely invisible to guardrail-based defenses. In a system where the attack is embedded in a retrieved document (EchoLeak), hidden in a supply-chain skill (OpenClaw), or propagated through an inter-agent reflection mechanism (AiTM, arXiv:2502.14847), the guardrail is not merely insufficient: it is architecturally bypassed by design.

### 1.2 The Three Attack Vectors This Framework Addresses

| Vector | Description | Research | Success Rate |
|--------|-------------|----------|-------------|
| **Memory Poisoning** | Persistent corruption of an agent's semantic memory through embedding manipulation | MemoryGraft (arXiv:2512.16962), GeminiJack (Noma Security, Jun 2025) | >80% |
| **RAG Poisoning** | Contamination of retrieval-augmented generation indexes through maliciously crafted documents | AgentPoison (arXiv:2407.12784), MINJA (NeurIPS 2025) | >80–95% |
| **Inter-Agent Communication Poisoning** | Manipulation of messages exchanged between agents via the reflect() mechanism | AiTM (arXiv:2502.14847, ACL 2025) | >70% |

Each of these attack classes exploits a different architectural layer. No single control mitigates all three. Defense in depth across all five TREASURE layers is the most comprehensive approach currently available.

---

## 2. TREASURE Framework — Architecture Overview

The TREASURE Framework organizes agentic AI defenses into five layers in a strict dependency hierarchy: each layer provides the foundational guarantees that the layers above it rely upon.

| # | Layer | Name | Primary Threat Addressed | Design Principle |
|---|-------|------|--------------------------|-----------------|
| 1 | **DATA LAYER** | Diamond Record | Memory & RAG Poisoning (ASI06) | Single Governed Truth |
| 2 | **EXECUTION LAYER** | Skills & Runtime | Tool Misuse, Code Execution (ASI02/ASI05) | Critical Attack Surface Control |
| 3 | **GOVERNANCE LAYER** | Code-Grade Governance | Agentic Drift, Supply Chain (ASI08) | Policy-as-Code Discipline |
| 4 | **CONTROL LAYER** | Human-in-the-Loop | Rogue Agent, Excessive Agency (ASI10) | Encapsulated Autonomy |
| 5 | **SECURITY LAYER** | Defense-in-Depth | Lateral Movement, Exfiltration (ASI03/ASI09) | Blast Radius Engineering |

```
SECURITY LAYER    ← Blast Radius Engineering
      ↑
CONTROL LAYER     ← Encapsulated Autonomy
      ↑
GOVERNANCE LAYER  ← Policy-as-Code Discipline
      ↑
EXECUTION LAYER   ← Critical Attack Surface ⚠️
      ↑
DATA LAYER        ← Single Governed Truth (foundation)
```

### 2.1 Standards Alignment Matrix

| TREASURE Layer | OWASP ASI | CSA MAESTRO | AIUC-1 | NIST RMF | OWASP AI Exchange |
|----------------|-----------|------------|--------|----------|------------------|
| DATA LAYER | ASI06 | L2 Data Ops | UC-DATA-01/02 | Map / Measure | GUARD: Data Controls |
| EXECUTION LAYER | ASI02, ASI05 | L3, L4, L5 | UC-EXEC-01–04 | Manage | AI DEFEND: Runtime |
| GOVERNANCE LAYER | ASI08 | L7 Governance | UC-GOV-01–05 | Govern | GUARD: Lifecycle |
| CONTROL LAYER | ASI10, ASI01 | L6 Human-AI | UC-CTRL-01/02 | Govern / Manage | GUARD: Human Oversight |
| SECURITY LAYER | ASI03, ASI04, ASI07, ASI09 | L1, L4 | UC-SEC-01–06 | Measure / Manage | AI DEFEND: Detection |

### 2.2 Limitations and Known Challenges

**Scale of trajectory logging.** Comprehensive logging generates substantial data volumes — potentially tens of gigabytes per day in high-throughput environments. Organizations must implement intelligent sampling, compression, and tiered retention policies while preserving forensic value.

**Performance overhead of full signing + sandboxing.** Representative benchmarks show 15–35% additional latency for signed skill invocation and up to 40% resource overhead for strict sandboxing compared to unsandboxed execution. Tiered enforcement (lightweight for low-risk agents, full for privileged ones) is recommended.

**Challenges in open skill marketplaces.** Sophisticated obfuscation and rapid iteration can evade initial provenance checks. Closed or curated skill registries are recommended for high-assurance deployments; zero-day supply-chain compromises remain a risk until marketplaces implement mandatory human review or cryptographic attestation from trusted publishers only.

**Evasion of behavioral baselining.** Patient attackers can gradually shift agent behavior within the "normal" envelope. Continuous adversarial testing, ensemble detection models, and periodic baseline resets tied to governance reviews are required to maintain effectiveness.

**Multi-modal agent risks (future).** Current specifications focus primarily on text and structured data. As agents incorporate vision, audio, and robotic control interfaces, new attack vectors emerge: visual prompt injection, audio command hijacking, sensor spoofing. Future extensions will address multi-modal provenance, hardware-in-the-loop controls, and physical blast radius engineering.

---

## 3. Layer Technical Specifications

### 3.1 DATA LAYER — Diamond Record (Single Governed Truth)

> *OWASP: ASI06 – Memory & Context Poisoning | CSA MAESTRO: L2 – Data Operations | AIUC-1: UC-DATA-01/02*

The Data Layer is the foundational stratum. Every inference made by an agent, every RAG retrieval, every memory read ultimately originates here. A corrupted data foundation propagates corruption upward through all subsequent layers regardless of how well those layers are otherwise defended.

The primary threat is the **persistent semantic backdoor**: an attacker injects a maliciously crafted document into the vector index. Every subsequent semantically related query triggers retrieval of the malicious payload, delivered to the agent as apparently trustworthy context.

**Technical Controls:**

- **Governed Ingestion Pipeline** — Semantic validation detecting embedded instruction patterns, prompt injection signatures, and anomalous directives; provenance verification (author, timestamp, originating system); policy enforcement restricting per-agent index segment access.
- **Differential Privacy in Embeddings** — Degrades backdoor effectiveness without material impact on legitimate retrieval utility.
- **Cryptographically Verified Memory Snapshots** — Append-only snapshots with cryptographic integrity hashes stored outside the agent's write surface; enables drift detection and rollback to verified clean states.
- **Identity-Scoped Query Constraints** — Per-agent access controls enforced at query time. An agent in the financial workflow domain cannot retrieve documents from legal or HR segments.
- **Continuous Semantic Monitoring** — Anomaly scores above threshold trigger human review before content is promoted to the live index.

> **Failure mode:** `Poisoned data → Embedded → Silently retrieved → Reused → Amplified across sessions → Cascading hallucination chain`

---

### 3.2 EXECUTION LAYER — Skills & Runtime ⚠️ CRITICAL

> *OWASP: ASI02 – Tool Misuse · ASI05 – Unexpected Code Execution | CSA MAESTRO: L3/L4/L5 | AIUC-1: UC-EXEC-01–04*

Skills are reusable behavioral components that codify multi-step workflows, tool orchestration, filesystem access, network operations, and cross-session state management — architecturally equivalent to production code with elevated system privileges. A single compromised skill propagates to every agent that imports it.

**OpenClaw (CVE-2026-25253)** demonstrated that a malicious skill in a marketplace, installed without provenance verification, produces RCE and credential exfiltration. Skills are the new supply chain: the npm dependency problem, reproduced in the agentic AI layer.

**Technical Controls:**

- **Cryptographic Skill Signing** — No skill may be instantiated without a valid cryptographic signature over its complete definition. The skill registry operates as the Certificate Authority. Unsigned skills are rejected at mounting, before execution begins.
- **Minimal-Privilege Skill Manifests** — Each skill declares its exact permission surface at registration; the runtime enforces as hard constraints, not advisory policy.
- **Runtime Sandboxing** — Skill execution in isolated contexts; MCP server processes run with reduced-privilege identity, without access to orchestrator credentials, with explicit network egress restrictions.
- **Pre-Call Hooks and Output Validation Pipelines** — Intercept every tool invocation: pre-call hooks validate parameters against declared goal/plan state; output validation scans tool responses for embedded prompt injection before context delivery.
- **Immutable Skill Audit Trail** — Append-only, off-agent log per invocation: agent identity, skill identifier + version hash, parameter hash, output hash, timestamps.

### 3.2.1 Skills Threat Taxonomy (AST01–AST10)

> *Operational extension used within TREASURE. Not an official OWASP publication.*

| ID | Risk | Severity | TREASURE Control | MAESTRO Layer |
|----|------|----------|-----------------|--------------|
| AST01 | Malicious Skills Injection | **CRITICAL** | Cryptographic signing + registry scanning | L5 Ecosystem |
| AST02 | Skill Privilege Escalation | **CRITICAL** | Minimal-privilege manifests + runtime enforcement | L3 Frameworks |
| AST03 | Unauthorized Tool Invocation | HIGH | Allow-lists at runtime + pre-call hooks | L3/L4 Infra |
| AST04 | Skill-to-Skill Lateral Movement | HIGH | Agent isolation + no shared credentials | L4 Deploy |
| AST05 | Persistent State Manipulation | HIGH | Versioned snapshots + integrity verification | L2 Data |
| AST06 | Resource Hijacking via Skills | HIGH | Token/cost budgets + circuit breakers | L4 Infra |
| AST07 | Skill Output Tampering | MEDIUM | Output validation pipelines + DLP | L6 Human-AI |
| AST08 | Cross-Agent Skill Reuse Attack | HIGH | Per-agent skill namespacing + isolation | L3 Frameworks |
| AST09 | Skill Supply Chain Compromise | **CRITICAL** | Provenance tracking + AIBOM + signing | L5 Ecosystem |
| AST10 | Cross-Platform Skill Reuse | HIGH | Universal Skill Format validation + scanning | L5/L7 |

---

### 3.3 GOVERNANCE LAYER — Code-Grade Governance

> *OWASP: ASI08 – Supply Chain Compromise | CSA MAESTRO: L7 – Governance & Audit | AIUC-1: UC-GOV-01–05 | ISO/IEC 42001 Clause 5.3 & Annex B*

An agent without code-grade governance is equivalent to production software deployed without source control, without testing, and without change management.

ISO/IEC 42001:2023 Clause 5.3 requires every consequential agent action to be traceable to a named accountable party. Annex B requires documented impact assessments revisited whenever the agent's operational context changes.

**Technical Controls:**

- **Versioned Agent Artifact Repository** — All agent behavioral specifications in version control; every change requires pull-request, review, approval, and merge. Commit history is the authoritative regulatory audit trail.
- **Policy-as-Code Enforcement** — Declarative, machine-executable formats (OPA/Rego or YAML). Natural-language policies in PDFs are unenforceable by the runtime.
- **CI/CD Integration with Automated Red Teaming** — Static analysis of workflow definitions; behavioral regression against adversarial prompt suite covering all OWASP ASI classes; automated red teaming; AIBOM generation and validation. An agent failing any gate cannot be promoted to production.
- **Drift Detection and Behavioral Baselining** — Continuous comparison of production behavioral profile against CI/CD-validated baseline; divergence above threshold triggers automated alerts.
- **Agent SBOM (AIBOM)** — AI Bill of Materials: foundation model version and provider; all skills with version hashes and signing certificates; all tool integrations with API schema versions; knowledge sources accessible to the agent.

---

### 3.4 CONTROL LAYER — Human-in-the-Loop (Encapsulated Autonomy)

> *OWASP: ASI10 – Rogue Agent Behaviour · ASI01 – Agent Goal Hijack | CSA MAESTRO: L6 – Human-AI Interface | AIUC-1: UC-CTRL-01/02 | NIST AI RMF: Govern*

The **Replit Meltdown (Incident #1152, July 2025)** demonstrated the consequence of an absent Control Layer: an agent operating without an Agency Envelope or kill-switch deleted a production database. The agent was not compromised; it executed its task with full fidelity. The failure was architectural.

The Agency Envelope is an enforcement constraint implemented in the Agent Runtime Control Plane, evaluated before every action, not subject to modification by the agent itself.

**Technical Controls:**

- **Decision Boundary Matrix** — Formally classifies every action type by authorization tier. Informational actions execute autonomously; financial, legal, data-modification, and production-system actions require human authorization before execution.
- **Agency Envelope Enforcement** — Defines the agent's complete action space per session: accessible tools, maximum autonomous steps, system modification categories, spending limits, maximum session duration. Evaluation before every tool call; actions outside envelope trigger escalation or termination.
- **Human-on-the-Loop vs. Human-in-the-Loop** — Mode selection is a property of the task definition, not a runtime user preference.
- **Infrastructure Kill-Switch** — Implemented at the infrastructure layer, independent of application logic: immediately halts execution, revokes all JIT credentials, quarantines memory state for forensic analysis. **Must be tested periodically through controlled drills. An untested kill-switch is an unverified control.**

---

### 3.5 SECURITY LAYER — Defense-in-Depth (Blast Radius Engineering)

> *OWASP: ASI03 · ASI04 · ASI07 · ASI09 | CSA MAESTRO: L1/L4 | AIUC-1: UC-SEC-01–06*

Every agent must be a bounded failure domain. When agents share credentials or implicitly trust messages from other agents, a single compromised agent becomes a stepping stone for lateral movement. AiTM (arXiv:2502.14847, ACL 2025) demonstrated this with >70% success rate. The architectural response is zero-trust between agents.

**Technical Controls:**

- **Per-Agent Identity with JIT Credentials** — Unique cryptographic identity per agent; access tokens ephemeral and Just-In-Time: generated for the specific tool invocation, scoped to minimum required permission, valid for minimum required duration. No shared credentials between agents.
- **Tool Allow-Lists and Sandbox Enforcement** — Enforced at Tool Router level, not in system prompt. No shared tool credential pools between agents.
- **Network Micro-Segmentation** — All egress routes through a controlled proxy enforcing permitted endpoint allow-list. Inter-agent communication only through the authorized orchestration channel.
- **Full Trajectory Logging** — Complete execution trajectory in append-only, off-agent, cryptographically signed log store: every reasoning step, tool call with parameters and response, memory reads/writes, state transitions, inter-agent messages.
- **Behavioral Baselining and Anomaly Detection** — Statistical baselines established during CI/CD cycle; continuous production comparison; anomaly scores above threshold trigger alerts.
- **Circuit Breakers** — Per agent-to-agent communication path; quarantine protocol for agents producing anomalous outputs.

---

## 4. OWASP Agentic Top 10 — Complete Mapping

> *OWASP Top 10 for Agentic Applications (ASI taxonomy, December 2025)*

| ID | Risk | Severity | TREASURE Layer | Key Control |
|----|------|----------|----------------|------------|
| ASI01 | Agent Goal Hijack | **CRITICAL** | CONTROL + DATA | Intent validation gates; goal-plan consistency checks; HITL on plan deviation |
| ASI02 | Tool Misuse & Exploitation | **CRITICAL** | EXECUTION | Tool allow-lists; per-call minimal scope; pre-call hooks; sandbox enforcement |
| ASI03 | Identity & Privilege Abuse | **CRITICAL** | SECURITY | Ephemeral JIT credentials; per-agent identity; no shared credentials; strong audit trail |
| ASI04 | Resource Exhaustion | HIGH | SECURITY | Token/cost budgets per agent; rate limiting; circuit breakers; session time limits |
| ASI05 | Unexpected Code Execution | **CRITICAL** | EXECUTION | Strict sandbox guardrails; container isolation; code scanning in pre-call hooks |
| ASI06 | Memory & Context Poisoning | HIGH | DATA | Input sanitisation; versioned memory snapshots; semantic validation; query constraints |
| ASI07 | Cascading Agent Failures | HIGH | SECURITY | Circuit breakers; per-agent failure domains; behavioral baselining; observability |
| ASI08 | Supply Chain Compromise | HIGH | GOVERNANCE | Cryptographic signing; AIBOM; dependency scanning; CI/CD gate enforcement |
| ASI09 | Data Leakage & Exfiltration | **CRITICAL** | SECURITY | Output DLP; steganography detection; log scrubbing; network egress filtering |
| ASI10 | Rogue Agent Behaviour | **CRITICAL** | CONTROL | Behavioural baselining; kill-switch; Agency Envelope; intent monitoring |

---

## 5. CSA MAESTRO Integration

TREASURE operates as an implementation overlay on top of MAESTRO: where MAESTRO identifies the threat surface at each architectural layer, TREASURE specifies the defensive controls.

| L | MAESTRO Layer | Primary Threat | TREASURE Coverage | Key Technical Response |
|---|--------------|---------------|------------------|----------------------|
| L1 | Foundation Models | Model theft, adversarial prompt injection | SECURITY + EXECUTION | Adversarial robustness testing; input validation; sandbox isolation |
| L2 | Data Operations | RAG poisoning, context leakage | DATA LAYER | Differential privacy; semantic validation; versioned snapshots; query constraints |
| L3 | Agent Frameworks | Insecure orchestration, logic bugs | GOVERNANCE + EXECUTION | Formal workflow verification; static analysis; behavioral regression testing |
| L4 | Deploy / Infrastructure | Container escapes, insecure APIs, MCP compromise | SECURITY + EXECUTION | Micro-segmentation; runtime sandboxing; JIT credentials; network egress filtering |
| L5 | Ecosystem & Tooling | Third-party skill poisoning, supply chain | EXECUTION + GOVERNANCE | Cryptographic signing; AIBOM; skill registry governance; dependency scanning |
| L6 | Human-AI Interface | Social engineering via agent outputs | CONTROL LAYER | Decision Boundary Matrix; output validation; HITL checkpoints; behavioral alerts |
| L7 | Governance & Audit | Accountability gaps, compliance drift | GOVERNANCE LAYER | Policy-as-Code; versioned artifacts; ISO 42001 AIMS; CI/CD audit trail |

---

## 6. AIUC-1, OWASP AI Exchange GUARD, and AI DEFEND — Technical Alignment

> *Integration summary: AIUC-1 provides the control requirements; GUARD provides the operational lifecycle; AI DEFEND provides the runtime pattern library. TREASURE implements all three simultaneously.*

> **Note:** AI DEFEND is a runtime defense pattern catalogue developed by the AI security community. It is distinct from and not part of the OWASP AI Exchange, though frequently used in conjunction with GUARD-based programs.

### 6.1 AIUC-1 Coverage

AIUC-1 controls UC-DATA-01 through UC-SEC-06 are fully addressed by the TREASURE Framework. No AIUC-1 agentic control requires a defensive mechanism outside the five-layer architecture. See [Appendix A](#appendix-a-detailed-aiuc-1-control-by-control-mapping) for the complete control-by-control mapping.

### 6.2 OWASP AI Exchange — GUARD Operational Lifecycle

| Phase | TREASURE Implementation |
|-------|------------------------|
| **G — Govern** | Agent Risk Register; Agency Envelope Policy; Agentic Drift Tolerance Policy; AIBOM Template. Satisfies ISO/IEC 42001 Clauses 5.3, 6.1, Annex B, 9.1 and NIST AI RMF Govern function. |
| **U — Understand** | CSA MAESTRO seven-layer threat decomposition; OWASP ASI01–ASI10 tactical catalogue; threat intelligence feed (arXiv cs.CR weekly; MITRE ATLAS update feed; OWASP AI Exchange; CVE/NVD). Living Threat Model updated quarterly or within 5 business days of high-severity publication. |
| **A — Assess** | CI/CD pipeline: static analysis → adversarial regression (ASI01–ASI10) → automated red teaming → AIBOM validation. Continuous: behavioral baselining engine + semantic anomaly monitor + trajectory log. Metrics: Blast Radius + Mean Time to Detection (MTTD) documented in Agent Risk Register before production authorization. |
| **R — Respond** | Kill-switch sequence (target: <30s): activation → JIT credential revocation → memory namespace quarantine → trajectory log snapshot → agent termination → incident ticket. Recovery: index integrity verification → snapshot rollback → re-ingestion pipeline → CI/CD re-assessment → staged re-deployment. Decommissioning per ISO/IEC 42001 lifecycle procedures. |
| **D — Defend** | Three properties required: (1) Architectural independence from agent reasoning — all controls at ARCP or below; (2) Trajectory-wide coverage — pre-call hooks + output validation + behavioral baselining + trajectory logging; (3) Defense-in-depth resilience — five independently enforced layers. Continuous improvement: GUARD Understand → TREASURE red teaming suite updated → CI/CD gates updated → agent re-assessed. |

### 6.3 AI DEFEND — Runtime Defense Pattern Integration

AI DEFEND organizes runtime patterns into five categories; the following maps each to TREASURE mechanisms:

**Input Defense** — Governed ingestion pipeline for knowledge base inputs; output validation pipeline screening tool responses before context delivery (three passes: structural, semantic, context-consistency). Failed screening: quarantine + human review (ingestion); sanitized delivery + trajectory flag (tool output); message rejection + circuit breaker trigger (inter-agent).

**Execution Defense** — Tool Router allow-list as hard constraint; pre-call hooks with goal-plan consistency scoring; behavioral baselining sequential pattern analysis for plan integrity monitoring; sandbox isolation with inter-skill communication screening (prevents AST04). Consistency score below threshold → HITL escalation or tool call rejection.

**Output Defense** — Output validation pipeline for NL outputs (DLP + injection amplification + semantic exfiltration); Agency Envelope Validator for write-side tool calls; entropy monitoring for steganographic exfiltration detection (Shannon entropy baseline per agent class; per-session Z-score; cross-session correlation for distributed patterns).

**Memory Defense** — Four AI DEFEND properties implemented in TREASURE: isolation (identity-scoped query constraints in Memory Manager); integrity (HMAC verification on versioned snapshots); provenance (ingestion pipeline provenance metadata schema: author identity, source system, ingestion timestamp, validation results); freshness (TTL policies enforced at retrieval time). Memory incident response: quarantine → serve previous verified snapshot → differential analysis → remove confirmed poisoned entries → re-validate → restore.

**Identity Defense** — Agent identity: unique cryptographic principal per AIBOM configuration; JIT credential per tool invocation. Principal identity: Agency Envelope binding + Policy Engine scope verification. Inter-agent identity: signed inter-agent messages verified by receiving ARCP; delegation scope checked against Governance Layer policy. Identity revocation propagates to all ARCPs within defined SLA.

---

## 7. Platform Implementation Examples

### 7.1 Hybrid Pattern: Microsoft Azure AI Foundry + AWS Bedrock

| TREASURE Layer | Azure AI Foundry Service | AWS Service | Integration Pattern / Key Gap |
|----------------|------------------------|------------|------------------------------|
| DATA LAYER | Azure AI Search + Azure Content Safety | Amazon OpenSearch Serverless | ADF governed pipeline; ACS semantic validation; Azure Blob immutable snapshots + HMAC via Function |
| EXECUTION LAYER | Azure Container Apps + ACR Notation signing | AWS Lambda + ECR cosign | Managed Identity JIT; IAM Roles Anywhere OIDC federation; APIM pre-call hooks — **long-lived keys = critical gap** |
| GOVERNANCE LAYER | Azure DevOps + SK YAML Policy-as-Code | AWS CodePipeline | Branch protection; unified AIBOM task; Azure Monitor + Sentinel drift detection on dual telemetry |
| CONTROL LAYER | Copilot Studio HITL + SK Planner constraints | AWS Step Functions | Agency Envelope as SK constraints; Logic App kill-switch → deactivation + STS revocation in <30s |
| SECURITY LAYER | Entra Agent ID + Azure Sentinel | AWS STS OIDC + CloudWatch Logs | Per-agent JIT via OIDC; VNet + VPC private endpoints; dual-write trajectory log; Sentinel analytics rules |

> ⚠️ **Most common gap:** Developers reverting to long-lived AWS access keys stored in Key Vault when IAM Roles Anywhere is not configured eliminates the JIT property required by UC-SEC-01.

### 7.2 Google Cloud — Vertex AI Agent Builder

| TREASURE Layer | Google Cloud / Vertex AI Primitive | Implementation Note / Critical Gap |
|----------------|----------------------------------|-----------------------------------|
| DATA LAYER | Vertex AI Search + Cloud Dataflow + Document AI | Access control labels per Workload Identity; Cloud KMS HMAC on Storage exports; custom semantic validation Dataflow transform required |
| EXECUTION LAYER | Vertex AI Extensions + Cloud Endpoints proxy | **ADK allow-list is advisory only** — Cloud Endpoints proxy is mandatory for TREASURE hard enforcement; KMS asymmetric signing for extension manifests |
| GOVERNANCE LAYER | Cloud Build + OPA sidecar (Policy-as-Code) + SLSA provenance (AIBOM) | OPA evaluates all actions before execution; Artifact Registry for policy versioning |
| CONTROL LAYER | Custom A2A middleware (Cloud Run) + ADK Planner constraints | **A2A default trust = unmitigated AiTM surface; WIF token verification middleware is REQUIRED, not optional** |
| SECURITY LAYER | Workload Identity (per-revision SA) + VPC Service Controls + Cloud Audit Logs + BigQuery ML | SA bound per Cloud Run revision; BigQuery ML scheduled baselining job |

### 7.3 AWS Standalone — Amazon Bedrock Agents

| TREASURE Layer | AWS Bedrock Primitive | Gap / Implementation Note |
|----------------|-----------------------|--------------------------|
| DATA LAYER | Bedrock Knowledge Base + OpenSearch Serverless + Step Functions pipeline | Custom Lambda validation chain required; S3 Object Lock WORM; DynamoDB provenance metadata |
| EXECUTION LAYER | Action Groups (OpenAPI schema) + ECR cosign + two-phase Lambda handler | **Pre-call hooks not injectable into Bedrock path** — two-phase handler pattern required; cosign via IAM condition; Guardrails ≠ Agency Envelope |
| GOVERNANCE LAYER | CodePipeline + CodeGuru + Verified Permissions Cedar + CycloneDX AIBOM | Cedar policy via Lambda authorizer on Agent alias; CodeCommit branch protection |
| CONTROL LAYER | Verified Permissions (Agency Envelope) + SNS/SQS HITL + EventBridge kill-switch Lambda | Kill-switch: alias deactivation + STS revocation + Glacier archive; target <30s |
| SECURITY LAYER | IAM ExternalId role per agent + VPC + CloudWatch + Bedrock invocation log + Amazon Detective | No native JIT per invocation — compensate with short MaxSessionDuration + rotation |

### 7.4 Failure Case: OpenClaw (CVE-2026-25253) — Layer-by-Layer Analysis

| # | Attack Action | Missing AIUC-1 Control | TREASURE Layer | TREASURE Counterfactual |
|---|--------------|------------------------|----------------|------------------------|
| 1 | Malicious skill installed from marketplace without provenance check | UC-EXEC-02: No skill signing | EXECUTION | Notation signature required at registration; Skill Executor rejects unsigned manifest — automatic gate |
| 2 | Skill reads agent complete credential namespace | UC-EXEC-01: No minimal-privilege manifest | EXECUTION | Manifest declares specific credential IDs; Tool Router enforces namespace; undeclared credentials architecturally inaccessible |
| 3 | GitHub token modifies workflow; platform API disables sandbox config | UC-GOV-01/02: No branch protection; sandbox as config | GOVERNANCE | Branch protection blocks workflow write; sandbox as infra primitive not disableable by API credential |
| 4 | Container breakout: sandbox disabled at config level | UC-EXEC-03: Sandbox not infrastructure-grade | EXECUTION | seccomp + AppArmor + dropped capabilities; sandbox requires kernel exploit to bypass |
| 5 | Lateral movement to internal systems from compromised host | UC-SEC-02: No network micro-segmentation | SECURITY | VPC isolation + egress proxy: post-breakout shell can only reach declared endpoints |

> **Key finding:** The attack required simultaneous absence of controls across three TREASURE layers. Closing any single gap would have broken the chain before the RCE stage.

---

## 8. Reference Architecture

### 8.1 Agent Runtime Control Plane (ARCP)

The ARCP is the central enforcement mechanism — an infrastructure-layer component that the agent runtime depends on for every action. It implements:

- **Memory Manager** — Enforces identity-scoped query constraints; validates retrieved content through the pre-ingestion pipeline before delivery to agent context; logs all memory operations.
- **Tool Router** — Enforces per-agent tool allow-lists; rejects invocations not on the allow-list before passing to the tool; applies pre-call hooks and output validation pipelines.
- **Skill Executor** — Verifies cryptographic signatures before instantiation; executes in isolated sandbox environments; generates immutable invocation audit records.
- **Policy Engine** — Evaluates all agent actions against Policy-as-Code before execution authorization; enforces Agency Envelope constraints; escalates to HITL when required.

### 8.2 Architecture Diagram

```
[User / External Input]
         │
         ▼
[Orchestrator + Intent Monitoring]
         │
         ▼
[Agent Runtime Control Plane]
    ├── Memory Manager         ← Diamond Record (L1 DATA)
    ├── Tool Router            ← Allow-lists + pre-call hooks (L2 EXEC)
    ├── Skill Executor         ← Signed skills + sandbox (L2 EXEC)
    └── Policy Engine          ← Policy-as-Code enforcement (L3 GOV)
         │
         ▼
[Agency Envelope Validator]    ← Decision Boundary Matrix (L4 CTRL)
         │
    ┌────┘
    │ [HITL Checkpoint]        ← Human escalation if action outside envelope
    └────┐
         ▼
[Diamond Record + Scoped Tool APIs]   (L5 SECURITY: JIT creds, sandbox)
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

## 9. Empirical Evidence Base

### 9.1 Real-World Incidents

| Incident | Vector | OWASP Classification | Missing TREASURE Layer |
|----------|--------|---------------------|----------------------|
| **EchoLeak CVE-2025-32711** (Feb 2025) | Malicious email → RAG context injection → zero-click mailbox exfiltration via M365 Copilot | ASI01 Goal Hijack + ASI06 Memory Poisoning | DATA LAYER: No semantic validation on RAG ingestion; no trajectory monitoring |
| **OpenClaw CVE-2026-25253** | Malicious skill in marketplace → installed by developer → RCE + credential theft | ASI05 Code Execution + ASI08 Supply Chain | EXECUTION LAYER: No skill signing; no registry governance; no sandbox enforcement |
| **Replit Meltdown Incident #1152** (Jul 2025) | Coding agent without Agency Envelope or kill-switch deleted production database | ASI10 Rogue Agent + ASI02 Tool Misuse | CONTROL LAYER: No Agency Envelope; no decision boundary; no kill-switch |

### 9.2 Research Evidence

- **MemoryGraft (arXiv:2512.16962)** — Persistent memory poisoning via targeted embedding manipulation. Directly motivates Data Layer controls.
- **AgentPoison (arXiv:2407.12784)** — RAG poisoning achieving >80% attack success rate. Motivates governed ingestion pipeline and continuous index monitoring.
- **MINJA (NeurIPS 2025)** — Query-only RAG poisoning achieving ~95% success without network segmentation. Motivates network micro-segmentation.
- **AiTM (arXiv:2502.14847, ACL 2025)** — Adversarial inter-agent manipulation via reflect() mechanism achieving >70% success. Motivates per-agent identity, JIT credentials, and inter-agent communication validation.

---

## 10. Implementation Roadmap

| Phase | Weeks | Focus | Key Deliverables |
|-------|-------|-------|-----------------|
| **Phase 1 — Foundation** | 1–4 | Data Layer | Audit all data sources; implement governed ingestion pipeline; enable append-only snapshots with integrity hashing; enforce identity-scoped query constraints |
| **Phase 2 — Execution Control** | 5–8 | Execution Layer | Establish skill registry with cryptographic signing; revoke authorization for unsigned skills; implement runtime sandboxing; deploy pre-call hooks and output validation pipelines |
| **Phase 3 — Governance** | 9–12 | Governance Layer | Migrate all agent artifacts to version-controlled repositories; implement Policy-as-Code; integrate automated red teaming in CI/CD; produce AIBOM for all production deployments |
| **Phase 4 — Human Control** | 13–16 | Control Layer | Define Decision Boundary Matrix per agent deployment; implement Agency Envelope Validator; deploy kill-switch mechanisms; conduct initial drill |
| **Phase 5 — Security Hardening** | 17–20 | Security Layer | Implement per-agent JIT credentials; eliminate shared credential pools; deploy network micro-segmentation; enable full trajectory logging; establish behavioral baselines; implement circuit breakers |

---

## 11. Real-World Attack Case Studies

### 11.1 EchoLeak — CVE-2025-32711 (February / June 2025)

Zero-click data exfiltration vulnerability in Microsoft 365 Copilot. An attacker embeds adversarial instructions in a malicious email. When the Copilot agent retrieves it as RAG context, the embedded instructions hijack the agent's goal, silently exfiltrating emails, calendar events, and Teams messages — with no visible action or warning.

**TREASURE Layer Analysis:** DATA LAYER (primary — no semantic validation on RAG ingestion); EXECUTION LAYER (secondary — no intent monitoring to detect plan deviation toward exfiltration); SECURITY LAYER (tertiary — no output DLP to catch content encoded in URL parameters).

- OWASP: ASI01 + ASI06 + ASI09 | AIUC-1 absent: UC-DATA-01/02, UC-EXEC-05, UC-SEC-06
- [Aim Security disclosure](https://www.aim.security/lp/echoleak) | [MSRC CVE-2025-32711](https://msrc.microsoft.com/update-guide/vulnerability/CVE-2025-32711)

### 11.2 Gemini Memory Attack & GeminiJack (February / June 2025)

Johann Rehberger (Feb 2025): malicious content in Gmail/Drive causes Gemini to write false episodic memory — fake user identity persisting across all future sessions. GeminiJack (Noma Security, Jun 2025): extends to cross-Workspace data exfiltration via image tag src attribute — zero clicks, zero alerts, zero user interaction.

**TREASURE Layer Analysis:** DATA LAYER (primary — no memory write validation; no versioned snapshots for rollback); GOVERNANCE LAYER (secondary — no behavioral drift detection).

- OWASP: ASI06 | AIUC-1 absent: UC-DATA-01/02/04, UC-GOV-05
- [Rehberger disclosure](https://embracethered.com/blog/posts/2024/google-gemini-persistent-memory-attack/) | [Noma Security GeminiJack](https://www.noma.ai/blog/geminijack-how-we-discovered-a-zero-day-that-could-compromise-google-workspace-agents)

### 11.3 AgentPoison (arXiv:2407.12784, 2024)

RAG backdoor attack achieving >80% success rate. Only write access to a single document in the knowledge base is required to produce a persistent backdoor that activates on semantically related queries indefinitely, without further attacker interaction. Optimized documents evade naive content filters while maximizing retrieval likelihood for trigger queries.

**TREASURE Layer Analysis:** DATA LAYER (primary — differential privacy in embeddings degrades optimization surface; semantic validation catches instruction patterns; continuous semantic monitoring detects anomalous retrieval behavior).

- OWASP: ASI06 | AIUC-1 absent: UC-DATA-01/02/03
- [arXiv:2407.12784](https://arxiv.org/abs/2407.12784)

### 11.4 AiTM — Adversarial Agent-in-the-Middle (arXiv:2502.14847, ACL 2025)

A compromised agent uses a reflect() mechanism: it analyzes conversation context before generating a malicious instruction that fits semantically into the ongoing conversation, corrupting the orchestrator's goal representation. Result: >70% success rate on AutoGen, MetaGPT, and custom frameworks. The attack compromises the entire system by manipulating messages — no individual agent needs to be compromised.

**TREASURE Layer Analysis:** SECURITY LAYER (primary — per-agent JIT identity + signed inter-agent messages prevent reflect() injection); CONTROL LAYER (secondary — plan integrity monitoring detects orchestrator goal divergence).

- OWASP: ASI07 | AIUC-1 absent: UC-SEC-01/02, UC-CTRL-01
- [arXiv:2502.14847](https://arxiv.org/abs/2502.14847)

### 11.5 Atlassian Rovo — Indirect Prompt Injection via Confluence (2025)

An attacker with write access to a single Confluence page embeds adversarial instructions. When Rovo's agent is invoked, it retrieves the malicious page as RAG context and exfiltrates content from Confluence spaces the attacker cannot directly access — amplified by the agent's broad read permissions across the organization.

**TREASURE Layer Analysis:** DATA LAYER (primary — no semantic validation on Confluence retrieval; no identity-scoped query constraints preventing cross-space retrieval); EXECUTION LAYER (secondary — no intent monitoring to detect task shift from summarize to exfiltrate).

- OWASP: ASI01 + ASI06 + ASI09 | AIUC-1 absent: UC-DATA-01/03, UC-EXEC-05, UC-SEC-06
- [Atlassian Community report](https://community.atlassian.com/forums/Atlassian-Platform-Community/Rovo-Agent-Data-Exfiltration-via-Indirect-Prompt-Injection/ba-p/3001198)

### 11.6 Replit Meltdown — Incident #1152 (July 2025)

A coding agent executed DROP TABLE on a production database during a refactoring task. The agent was not compromised — it executed its task with full fidelity to its own goal interpretation. No Agency Envelope existed to classify destructive database operations as requiring human authorization. No kill-switch was available to halt execution before completion. Data recovery was not possible.

**TREASURE Layer Analysis:** CONTROL LAYER (primary — no Decision Boundary Matrix; no Agency Envelope Validator; no kill-switch); GOVERNANCE LAYER (secondary — no Agency Envelope Policy classifying destructive operations on production resources); EXECUTION LAYER (tertiary — no minimal-privilege manifest restricting database tool to read + create/update on test databases only).

- OWASP: ASI10 + ASI02 | AIUC-1 absent: UC-CTRL-01/02/03, UC-EXEC-01
- [Wired reporting](https://www.wired.com/story/replit-ai-code-database-deletion/)

### 11.7 Consolidated Attack-to-TREASURE Mapping

| # | Incident | OWASP ASI | TREASURE Layer(s) | Primary AIUC-1 Controls Absent |
|---|----------|-----------|------------------|-------------------------------|
| 11.1 | EchoLeak CVE-2025-32711 | ASI01+ASI06+ASI09 | DATA+EXECUTION+SECURITY | UC-DATA-01/02, UC-EXEC-05, UC-SEC-06 |
| 11.2 | Gemini Memory Attack / GeminiJack | ASI06 | DATA+GOVERNANCE | UC-DATA-01/02/04, UC-GOV-05 |
| 11.3 | AgentPoison arXiv:2407.12784 | ASI06 | DATA | UC-DATA-01/02/03 |
| 11.4 | AiTM arXiv:2502.14847 | ASI07 | SECURITY+CONTROL | UC-SEC-01/02, UC-CTRL-01 |
| 11.5 | Atlassian Rovo Indirect PI | ASI01+ASI06+ASI09 | DATA+EXECUTION+SECURITY | UC-DATA-01/03, UC-EXEC-05, UC-SEC-06 |
| 11.6 | Replit Meltdown #1152 | ASI10+ASI02 | CONTROL+GOVERNANCE+EXECUTION | UC-CTRL-01/02/03, UC-EXEC-01 |

> **Common pattern:** Every successful attack exploited the absence of controls in the DATA LAYER or CONTROL LAYER as its primary entry point. In five of six cases, a governed ingestion pipeline (UC-DATA-01/02) **or** an Agency Envelope with decision boundary enforcement (UC-CTRL-01) would have independently broken the attack chain — confirming these two controls represent the minimum viable security posture for any agentic AI deployment.

---

## Appendix A: Detailed AIUC-1 Control-by-Control Mapping

| Control ID | AIUC-1 Control Statement | TREASURE Implementation | Security Rationale |
|------------|--------------------------|------------------------|--------------------|
| **UC-DATA-01** | Establish a single authoritative knowledge source with documented provenance for all data used in agent reasoning | Diamond Record: governed ingestion pipeline; provenance metadata schema enforced at ingest; source attestation stored alongside each document chunk | CRITICAL — Without provenance, poisoned documents are indistinguishable from legitimate ones at retrieval time |
| **UC-DATA-02** | Implement embedding integrity controls capable of detecting and preventing vector index manipulation | Differential privacy in embeddings; cryptographic hash of index state per snapshot; semantic anomaly scoring on candidate ingest documents | HIGH — EchoLeak and AgentPoison both exploit the absence of this control |
| **UC-DATA-03** | Enforce access control at the retrieval layer, not solely at the application layer | Identity-scoped query constraints enforced by the Memory Manager in the ARCP; agents receive only embeddings within their authorized namespace | HIGH — Application-layer access control is bypassable via prompt injection; retrieval-layer enforcement is not |
| **UC-DATA-04** | Maintain versioned, rollback-capable snapshots of all agent knowledge bases | Append-only vector index snapshots with HMAC integrity; snapshot metadata stored in the governance repository; rollback procedure documented and tested | MEDIUM — Enables recovery from detected poisoning without full re-ingestion |
| **UC-EXEC-01** | Enforce least-privilege execution permissions for all agent tools and skills; no tool may be invoked with permissions exceeding those declared in its manifest | Minimal-privilege skill manifests with declarative permission surface; Tool Router enforces allow-lists as hard constraints; manifest violations abort execution | CRITICAL — Over-privileged tools are the primary enabler of ASI02 (Tool Misuse) |
| **UC-EXEC-02** | Implement cryptographic signing for all executable agent components prior to deployment | Skill registry acts as CA; all skills require a valid signature over their complete definition before mounting; unsigned skills are rejected at the Skill Executor before instantiation | CRITICAL — OpenClaw exploited the absence of skill signing in a marketplace context |
| **UC-EXEC-03** | Sandbox all agent code execution environments; execution must not propagate to the host runtime | Runtime sandboxing with process isolation per skill; MCP server processes run under reduced-privilege identities; container-level egress filtering applied per skill network declarations | CRITICAL — ASI05 (Unexpected Code Execution) requires sandbox integrity as an independent defense layer |
| **UC-EXEC-04** | Maintain an immutable audit trail of all agent tool invocations, including parameters, results, and execution context | Off-agent append-only invocation log; records include agent identity, skill ID + version hash, input parameter hash, output hash, timestamps, duration; log is cryptographically signed | HIGH — Without this record, trajectory manipulation attacks are forensically undetectable post-incident |
| **UC-EXEC-05** | Implement pre-invocation intent validation for all tool calls; calls inconsistent with the agent's declared goal must be blocked or escalated | Pre-call hooks in the ARCP evaluate tool call parameters against the agent's current plan state; goal-plan consistency scores below threshold trigger HITL escalation | HIGH — Intent monitoring is the primary detection mechanism for ASI01 (Goal Hijack) at the execution layer |
| **UC-GOV-01** | Version-control all agent behavioral specifications including prompts, workflows, skill definitions, tool chains, and policies | Agent artifact repository with full commit history; all artifact types subject to pull-request workflow with required review approvals; merge history constitutes regulatory audit trail | CRITICAL — An unversioned agent is architecturally equivalent to production code without source control |
| **UC-GOV-02** | Express all agent behavioral policies in machine-executable, declarative formats enforced at runtime | OPA/Rego or YAML policy schemas interpreted by the Policy Engine in the ARCP; natural-language policies are not enforceable and do not satisfy this control | HIGH — Policy-as-Code is the prerequisite for runtime enforcement; narrative policy is an unverifiable paper control |
| **UC-GOV-03** | Integrate automated security testing in the agent CI/CD pipeline; no agent artifact may be promoted to production without passing all gates | Static analysis of workflow definitions; behavioral regression against adversarial prompt suite; automated red teaming using OWASP ASI catalogue; AIBOM generation and validation | HIGH — CI/CD security gates are the primary prevention mechanism for agentic supply chain compromise (ASI08) |
| **UC-GOV-04** | Produce and maintain an AI Bill of Materials (AIBOM) for every agent deployment | AIBOM documents: foundation model version + provider; skills with version hashes and signing certificates; tool integrations with API schema versions; knowledge sources with provenance hashes | HIGH — AIBOM is the prerequisite for supply chain risk assessment and incident attribution |
| **UC-GOV-05** | Implement continuous drift detection comparing production agent behavior against CI/CD-validated behavioral baseline | Behavioral metrics collected in production compared against baseline established at last CI/CD cycle; divergence thresholds defined per agent class; threshold breaches trigger automated alerts and escalation | MEDIUM — Agentic drift is a slow-moving attack vector that standard security monitoring does not detect |
| **UC-CTRL-01** | Define and enforce an Agency Envelope formally specifying the complete action space permitted for each agent deployment | Decision Boundary Matrix specifies authorization tier per action type; Agency Envelope Validator in ARCP evaluates every action before execution; envelope is a versioned governance artifact | CRITICAL — The Replit Meltdown resulted directly from the absence of this control |
| **UC-CTRL-02** | Implement an infrastructure-level kill-switch capable of immediately halting agent execution and revoking all associated credentials | Infrastructure kill-switch independent of application logic; terminates execution, revokes JIT tokens, quarantines memory state, generates forensic snapshot; verified by periodic drills | CRITICAL — Application-level stop mechanisms are bypassable by a sufficiently compromised agent runtime |
| **UC-CTRL-03** | Implement human oversight checkpoints at action categories classified as requiring authorization in the Decision Boundary Matrix | HITL checkpoint workflow integrates with the Agency Envelope Validator; escalation paths defined per action tier; response time SLAs documented; default-deny on timeout | HIGH — Human oversight is not effective when implemented as an optional UI element; it must be an enforcement gate |
| **UC-SEC-01** | Assign each agent a unique cryptographic identity; prohibit shared credentials between agents or between agents and human operators | Per-agent identity via Entra Agent ID or equivalent; JIT credential issuance per tool invocation; no shared pools; credential lifespan bounded to minimum necessary duration | CRITICAL — Shared credentials eliminate agent isolation and enable lateral movement (ASI07 + AiTM) |
| **UC-SEC-02** | Enforce network micro-segmentation preventing agents from accessing systems outside their declared scope | All agent egress via controlled proxy enforcing endpoint allow-list; inter-agent communication via authorized orchestration channel only; agents cannot discover or contact peers outside their defined graph | HIGH — Uncontrolled network access enables both exfiltration (ASI09) and inter-agent infection (AiTM) |
| **UC-SEC-03** | Capture the complete execution trajectory of every agent session in an immutable, off-agent log store | Full trajectory log: reasoning steps, tool calls with parameters and responses, memory reads/writes, state transitions, inter-agent messages; stored append-only outside agent write surface; HMAC-signed | CRITICAL — Trajectory logs are the only mechanism for detecting trajectory manipulation attacks post-hoc |
| **UC-SEC-04** | Establish behavioral baselines for all agent deployments and implement continuous anomaly detection against those baselines | Statistical baselines: tool call frequency distributions, sequence patterns, memory access profiles, output entropy; anomaly scoring in production; threshold alerts; automated escalation paths | HIGH — Behavioral anomaly detection is the primary mechanism for detecting ASI10 (Rogue Agent) without known-bad signatures |
| **UC-SEC-05** | Implement circuit breakers on all inter-agent communication paths to prevent cascading failure propagation | Circuit breakers on each agent-to-agent path; quarantine protocol for agents producing anomalous outputs; downstream agents notified before dependency is severed | HIGH — Without circuit breakers, a single compromised agent can disable or corrupt a multi-agent network (ASI07) |
| **UC-SEC-06** | Implement output data loss prevention and exfiltration detection on all agent output channels | Output DLP pipeline scanning for PII, credential patterns, and semantic exfiltration indicators; steganography detection on structured outputs; entropy monitoring on outbound data streams | CRITICAL — ASI09 (Data Exfiltration) is the highest-impact consequence class for agentic AI compromise |

---

## References

### Standards & Frameworks

- [OWASP Top 10 for Agentic Applications 2026](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/)
- [OWASP AI Exchange — Agentic AI Threats and Mitigations](https://genai.owasp.org/resource/agentic-ai-threats-and-mitigations/)
- [CSA MAESTRO — Agentic AI Threat Modeling Framework](https://cloudsecurityalliance.org/blog/2025/02/06/agentic-ai-threat-modeling-framework-maestro)
- [CSA — Agentic AI Identity & Access Management](https://cloudsecurityalliance.org/artifacts/agentic-ai-identity-and-access-management-a-new-approach)
- [CSA — Securing Autonomous AI Agents (Survey 2026)](https://cloudsecurityalliance.org/artifacts/securing-autonomous-ai-agents)
- [NIST AI RMF 1.0](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework)
- [NIST AI 600-1 — Generative AI Profile](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf)
- [ISO/IEC 42001:2023 — AI Management Systems](https://www.iso.org/standard/81230.html)
- [MITRE ATLAS](https://atlas.mitre.org/)
- EU AI Act, 2024/1689, Official Journal of the European Union

### Research Papers

- [MemoryGraft — arXiv:2512.16962](https://arxiv.org/abs/2512.16962)
- [AgentPoison — arXiv:2407.12784](https://arxiv.org/abs/2407.12784)
- [AiTM — arXiv:2502.14847 (ACL 2025)](https://arxiv.org/abs/2502.14847)
- MINJA — NeurIPS 2025 (proceedings.neurips.cc)
- [The Attack and Defense Landscape of Agentic AI — arXiv:2603.11088](https://arxiv.org/abs/2603.11088)
- [Agentic AI Security: Threats, Defenses, Evaluation — arXiv:2510.23883](https://arxiv.org/abs/2510.23883)

### Incidents & CVEs

- EchoLeak CVE-2025-32711 — [Aim Security](https://www.aim.security/lp/echoleak) · [MSRC](https://msrc.microsoft.com/update-guide/vulnerability/CVE-2025-32711)
- GeminiJack — [Noma Security, June 2025](https://www.noma.ai/blog/geminijack-how-we-discovered-a-zero-day-that-could-compromise-google-workspace-agents)
- Gemini Memory Attack — [Johann Rehberger, February 2025](https://embracethered.com/blog/posts/2024/google-gemini-persistent-memory-attack/)
- OpenClaw CVE-2026-25253 — [MITRE ATLAS](https://atlas.mitre.org/)
- Replit Meltdown Incident #1152 — [Wired, July 2025](https://www.wired.com/story/replit-ai-code-database-deletion/)
- Atlassian Rovo — [Community report](https://community.atlassian.com/forums/Atlassian-Platform-Community/Rovo-Agent-Data-Exfiltration-via-Indirect-Prompt-Injection/ba-p/3001198)

---

## License

**CC0 1.0 Universal — Public Domain Dedication**

To the extent possible under law, Roger Sanz González has waived all copyright and related rights to this specific layout and textual implementation of the TREASURE AI Security Framework. You are free to copy, modify, distribute, and build upon this text, even for commercial purposes, without seeking prior permission or providing mandatory attribution.

→ [View CC0 1.0 Legal Code](https://creativecommons.org/publicdomain/zero/1.0/)

Contributions and feedback: [roger.sanz@owasp.org](mailto:roger.sanz@owasp.org)

---

*TREASURE Framework v1.0 · Roger Sanz González · Plain Concepts · OWASP AI Exchange · June 2026*
