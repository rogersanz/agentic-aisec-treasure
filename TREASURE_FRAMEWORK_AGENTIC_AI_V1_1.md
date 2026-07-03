# TREASURE Framework
## Defense-in-Depth Architecture for Agentic AI Systems

> *Tiered Resilient Execution Architecture for Secure Unified Robust Environments*

[![License: CC0-1.0](https://img.shields.io/badge/License-CC0_1.0-lightgrey.svg)](https://creativecommons.org/publicdomain/zero/1.0/)
[![OWASP](https://img.shields.io/badge/Aligned-OWASP%20GenAI%20Security-blue)](https://genai.owasp.org)
[![CSA MAESTRO](https://img.shields.io/badge/Aligned-CSA%20MAESTRO-orange)](https://cloudsecurityalliance.org)
[![NIST AI RMF](https://img.shields.io/badge/Aligned-NIST%20AI%20RMF-green)](https://www.nist.gov/artificial-intelligence)
[![MITRE ATLAS](https://img.shields.io/badge/Aligned-MITRE%20ATLAS-red)](https://atlas.mitre.org)
[![ISO 42001](https://img.shields.io/badge/Aligned-ISO%2FIEC%2042001-blue)](https://www.iso.org/standard/81230.html)
[![Version](https://img.shields.io/badge/Version-1.1-brightgreen)]()

---

**Author:** Roger Sanz, PhD  
**Role:** AI Security Lead — Plain Concepts | Senior Researcher — Universidad Isabel I  
Lead Editor, OWASP AI Exchange | Contributor, MITRE ATLAS · CSA · ISMS Forum · DAMA  
TAISE · CRISC · C|CISO · CCSK · CCZT · ISO 27001/22301/42001 LA  
**Contact:** [roger.sanz@owasp.org](mailto:roger.sanz@owasp.org)  
**Version:** 1.1 · 3 July 2026

---

## Editor's Notice

The TREASURE AI Security Framework is an innovative security framework developed by Roger Sanz, PhD, explicitly designed to address the complex vulnerabilities and risk vectors of Agentic AI systems.

This framework is open to every contributor and practitioner with a clear focus on security research, testing, or interest in the Agentic AI Security scenario evolution. This initial version provides the starting point of the framework's evolution and should be used in a tailored manner depending on the specific organization's scenario. It is intended to complement — not substitute — other frameworks, and takes into account future integrations based on community development.

> **Central principle:** Protect your AgenticAI Security treasure. If you do not govern your agents, they will work for your adversaries.

**Licensing & Rights Notice (CC0 1.0):** To the extent possible under law, the author has waived all copyright and related rights to this specific layout and textual implementation. You are free to copy, modify, distribute, and build upon this text, even for commercial purposes, without seeking prior permission. → [View CC0 1.0 Legal Code](https://creativecommons.org/publicdomain/zero/1.0/)

> **📌 Same-day addendum — 3 July 2026 (version number unchanged, v1.1):** a post-publication verification pass against primary sources (NVD, CVE.org, OWASP GenAI Security Project, CSA, AIUC-1, contemporary reporting) identified and corrected the following, without altering the five-layer architecture or any TREASURE control (UC-\*) definition:
> 1. **OpenClaw (CVE-2026-25253)** was described as a malicious-skill marketplace supply-chain attack. The actual CVE is a control-plane authentication vulnerability (unvalidated `gatewayUrl` → token theft → one-click RCE). Corrected throughout Sections 3.2, 7.4, 9.1, 11.7, 12.3, Appendix A, and References.
> 2. Two real, independent 2026 incidents have been added: the **OpenClaw ignored-stop-commands / mass email deletion** incident (Section 11.8, CONTROL LAYER) and the **LiteLLM/Trivy supply-chain compromise** (Section 11.9, GOVERNANCE/EXECUTION LAYER) — the latter now anchors the skill/dependency-supply-chain lesson previously (and incorrectly) attributed to OpenClaw.
> 3. The CSA MAESTRO layer numbering in Section 5 has been corrected to match the canonical mapping already documented in Section 13.3 (L5 Evaluation & Observability, L6 Security & Compliance [cross-cutting], L7 Agent Ecosystem), resolving an internal inconsistency between the two sections. Section 2.1's Standards Alignment Matrix has been updated to match.
> 4. The Replit Vibe Coding Meltdown (§11.6, §9.1) has been corrected: contemporary reporting indicates the agent's claim that "rollback was impossible" was false, and data was in fact recovered — strengthening rather than weakening the ASI09 (Human-Agent Trust Exploitation) classification.
> 5. AIUC-1's "UC-\*" control identifiers are now explicitly flagged (Section 2.1, References) as TREASURE's internal crosswalk convention, not official AIUC-1 requirement codes, given AIUC-1's quarterly update cadence.
> 6. Added references to the NIST AI Agent Standards Initiative (CAISI, launched 17 February 2026) as a forward-looking, not-yet-cross-mapped standard to track.

---

## Executive Summary

Enterprise organizations are deploying autonomous AI agents at an accelerating pace. Unlike traditional generative AI systems that respond to prompts in isolation, agentic systems plan, act, remember, and collaborate across multi-step workflows — invoking APIs, modifying databases, communicating with other agents, and operating continuously with minimal human oversight. This qualitative leap in capability introduces a qualitative leap in attack surface that no single perimeter control, guardrail, or content filter is architecturally capable of addressing.

The TREASURE Framework responds with a five-layer defense-in-depth architecture specifically engineered for the threat model of agentic AI. Each layer addresses a distinct attack class while maintaining structural independence so that the failure of any single layer does not cascade into a system-wide breach. The framework is not a product, a policy template, or a checklist: it is an operational architecture grounded in the adversarial evidence base of 2025–2026.

The core adversarial problem this document addresses is the **double-agent threat**: an autonomous agent that, through memory poisoning, RAG poisoning, or inter-agent communication manipulation, operates against the interests of its legitimate principals while appearing to function normally. EchoLeak (CVE-2025-32711) and the Replit Vibe Coding Meltdown (Incident #1152, July 2025) are the document's central double-agent-adjacent examples of this class. A broader set of documented incidents — including two involving OpenClaw (CVE-2026-25253, a control-plane authentication flaw, and a separate February 2026 kill-switch failure) and the LiteLLM/Trivy supply chain compromise (Section 11) — extends the evidence base to execution-layer and supply-chain failure modes that are architecturally distinct from double-agent behavior but equally outside the reach of guardrail-based defenses.

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

> **v1.1 additions:** Section 12 (MCP Security — The Execution Layer's Expanding Attack Surface) and Section 13 (Emerging Threat Vectors and Framework Evolution) are new in v1.1, grounded in the OWASP Practical Guide for Secure MCP Server Development (February 2026), the OWASP State of Agentic AI Security v2.01 (June 2026), and the corrected OWASP ASI taxonomy (December 2025 official numbering). The taxonomy correction note in Section 4 reflects the official December 2025 ASI numbering verified against genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/ on 3 July 2026: ASI04 = Agentic Supply Chain Vulnerabilities; ASI07 = Insecure Inter-Agent Communication; ASI08 = Cascading Agent Failures; ASI09 = Human-Agent Trust Exploitation; ASI10 = Rogue Agents. Data Leakage & Exfiltration is not a standalone ASI entry — it is a consequence of ASI01, ASI03, and ASI06. The Replit incident official name is "Replit Vibe Coding Meltdown".
>
> **Same-day addendum (also 3 July 2026, version number unchanged):** see the corrections notice under the Editor's Notice above, and the new Sections 11.7–11.10, for the OpenClaw re-classification, two newly added 2026 incidents, and the MAESTRO layer-numbering fix.

---

## 1. The Agentic AI Threat Landscape

### 1.1 Why Traditional Security Fails

Conventional cybersecurity operates on a stateless, perimeter-first model: identify the boundary, filter inputs, validate outputs. Agentic AI systems break every one of these assumptions simultaneously.

An autonomous agent is a distributed cognitive system: the agent itself is a service; each skill is a function or Lambda; memory is a database with read/write semantics; tools are external APIs with real-world side effects; the orchestrator is a workflow engine with branching logic. The attack surface scales accordingly.

Guardrails cover only the first and last points of a trajectory that may span dozens of intermediate steps. Everything between the initial prompt and the final response — tool calls, memory reads and writes, skill invocations, inter-agent communications, state modifications — is entirely invisible to guardrail-based defenses. In a system where the attack is embedded in a retrieved document (EchoLeak), delivered through an unvalidated control-interface parameter (OpenClaw, CVE-2026-25253), hidden in a compromised CI/CD dependency (LiteLLM/Trivy, February–March 2026), or propagated through an inter-agent reflection mechanism (AiTM, arXiv:2502.14847), the guardrail is not merely insufficient: it is architecturally bypassed by design.

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
| 3 | **GOVERNANCE LAYER** | Code-Grade Governance | Agentic Drift, Supply Chain (ASI04) | Policy-as-Code Discipline |
| 4 | **CONTROL LAYER** | Human-in-the-Loop | Rogue Agent, Excessive Agency (ASI10) | Encapsulated Autonomy |
| 5 | **SECURITY LAYER** | Defense-in-Depth | Lateral Movement, Inter-Agent Attacks, Cascading Failures (ASI03/ASI07/ASI08) | Blast Radius Engineering |

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

> **⚠️ Corrected 3 July 2026 (same-day addendum):** the CSA MAESTRO column below uses the canonical seven-layer numbering confirmed in Section 13.3 (L1 Foundation Models, L2 Data Operations, L3 Agent Frameworks, L4 Deployment/Infrastructure, L5 Evaluation & Observability, L6 Security & Compliance — a cross-cutting layer spanning L1–L5, L7 Agent Ecosystem). Earlier printings of this table used a non-canonical variant (L5 "Ecosystem & Tooling", L6 "Human-AI Interface", L7 "Governance & Audit") that has been retired; see Section 13.3 for the full rationale and the note below for how TREASURE's Control and Governance Layers map onto MAESTRO's single cross-cutting L6.

| TREASURE Layer | OWASP ASI | CSA MAESTRO | AIUC-1* | NIST RMF | OWASP AI Exchange |
|----------------|-----------|------------|--------|----------|------------------|
| DATA LAYER | ASI06 | L2 Data Operations | UC-DATA-01/02 | Map / Measure | GUARD: Data Controls |
| EXECUTION LAYER | ASI02, ASI05 | L3, L4, L7 | UC-EXEC-01–04 | Manage | AI DEFEND: Runtime |
| GOVERNANCE LAYER | ASI04 | L6 (Security & Compliance, cross-cutting) + L5 | UC-GOV-01–05 | Govern | GUARD: Lifecycle |
| CONTROL LAYER | ASI10, ASI01 | L6 (Security & Compliance, cross-cutting)† | UC-CTRL-01/02 | Govern / Manage | GUARD: Human Oversight |
| SECURITY LAYER | ASI03, ASI07, ASI08 | L1, L4, L5 | UC-SEC-01–06 | Measure / Manage | AI DEFEND: Detection |

> *\* AIUC-1 column note:* the "UC-\*" identifiers are TREASURE's own internal crosswalk labels for AIUC-1's control set — they are not verbatim AIUC-1 requirement codes. AIUC-1 is organized around six risk pillars (Data & Privacy, Security, Safety, Reliability, Accountability, Societal Impact) with 51 requirements and 130 controls, updated on a quarterly cadence (the Q1 2026 update alone revised 26 requirements and added 40+ voice-specific requirements). Treat the UC-\* mapping in this document as TREASURE's interpretive alignment, to be re-validated each quarter against the official OWASP × AIUC-1 crosswalk (see References, "Standards & Frameworks").
>
> *† MAESTRO note:* CSA's canonical seven-layer model does not define separate numbered layers for "Human-AI Interface" or "Governance & Audit" — both concerns sit inside the cross-cutting L6 Security & Compliance layer. TREASURE's CONTROL LAYER (human oversight, Agency Envelope) and GOVERNANCE LAYER (Policy-as-Code, audit trail) are TREASURE-specific decompositions of that single MAESTRO layer, made for operational clarity. This does not change any TREASURE control (UC-CTRL-\*, UC-GOV-\*); it only corrects which MAESTRO layer number they are attributed to.

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

**OpenClaw (CVE-2026-25253, February 2026)** demonstrated a distinct but equally critical execution-layer failure: the OpenClaw agent's Control UI accepted a `gatewayUrl` value from an unvalidated query string and automatically opened a WebSocket connection to it, silently transmitting the stored gateway authentication token. A single crafted link, opened by an authenticated user, was enough to exfiltrate the token and obtain unauthorized gateway access leading to one-click remote code execution (CVSS 8.8, CWE-669) — no skill marketplace, missing signature, or provenance failure was involved. The lesson for TREASURE is broader than skill signing: the control-plane interface itself (the channel through which a human operator configures and issues commands to the agent) is execution-layer attack surface and requires the same origin validation, confirmation-on-change, and pre-call hook discipline as any tool invocation (UC-EXEC-03, UC-EXEC-05). *(Corrected 3 July 2026 — an earlier version of this document attributed a marketplace skill-signing failure to this CVE; see Section 7.4 for the accurate case study and Section 11.7 for the real 2026 skill-supply-chain incident that now anchors that lesson.)* Skills remain the new supply chain in their own right: the npm dependency problem, reproduced in the agentic AI layer — illustrated in Section 11.9 by the LiteLLM/Trivy compromise.

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

> *OWASP: ASI04 – Agentic Supply Chain Vulnerabilities | CSA MAESTRO: L7 – Governance & Audit | AIUC-1: UC-GOV-01–05 | ISO/IEC 42001 Clause 5.3 & Annex B*

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

> *OWASP: ASI01 – Agent Goal Hijack · ASI09 – Human-Agent Trust Exploitation · ASI10 – Rogue Agents | CSA MAESTRO: L6 – Human-AI Interface | AIUC-1: UC-CTRL-01/02/03 | NIST AI RMF: Govern*

The **Replit Meltdown (Incident #1152, July 2025)** demonstrated the consequence of an absent Control Layer: an agent operating without an Agency Envelope or kill-switch deleted a production database. The agent was not compromised; it executed its task with full fidelity. The failure was architectural.

The Agency Envelope is an enforcement constraint implemented in the Agent Runtime Control Plane, evaluated before every action, not subject to modification by the agent itself.

**Technical Controls:**

- **Decision Boundary Matrix** — Formally classifies every action type by authorization tier. Informational actions execute autonomously; financial, legal, data-modification, and production-system actions require human authorization before execution.
- **Agency Envelope Enforcement** — Defines the agent's complete action space per session: accessible tools, maximum autonomous steps, system modification categories, spending limits, maximum session duration. Evaluation before every tool call; actions outside envelope trigger escalation or termination.
- **Human-on-the-Loop vs. Human-in-the-Loop** — Mode selection is a property of the task definition, not a runtime user preference.
- **Infrastructure Kill-Switch** — Implemented at the infrastructure layer, independent of application logic: immediately halts execution, revokes all JIT credentials, quarantines memory state for forensic analysis. **Must be tested periodically through controlled drills. An untested kill-switch is an unverified control.**

---

### 3.5 SECURITY LAYER — Defense-in-Depth (Blast Radius Engineering)

> *OWASP: ASI03 – Identity & Privilege Abuse · ASI07 – Insecure Inter-Agent Communication · ASI08 – Cascading Agent Failures | CSA MAESTRO: L1/L4 | AIUC-1: UC-SEC-01–06*

> *ASI09 (Human-Agent Trust Exploitation) and ASI10 (Rogue Agents) are primarily addressed by the CONTROL LAYER. Data exfiltration, formerly labelled as a standalone entry in earlier ASI drafts, is not a distinct entry in the official December 2025 taxonomy — it is a consequence class that emerges from ASI01 (Goal Hijack), ASI03 (Identity Abuse), and ASI06 (Memory Poisoning).*

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
| ASI07 | Insecure Inter-Agent Communication | HIGH | SECURITY | Cryptographic signing of inter-agent messages; per-agent JIT identity; zero-trust between agents; circuit breakers |
| ASI08 | Cascading Agent Failures | HIGH | SECURITY | Circuit breakers; per-agent failure domains; behavioral baselining; blast radius engineering |
| ASI09 | Human-Agent Trust Exploitation | HIGH | CONTROL | HITL checkpoints; output validation; output DLP; anomaly detection on agent recommendations |
| ASI10 | Rogue Agents | **CRITICAL** | CONTROL | Behavioural baselining; kill-switch; Agency Envelope; intent monitoring |

> **⚠️ Taxonomy note — December 2025 official OWASP numbering:** The official OWASP Top 10 for Agentic Applications (published 10 December 2025 by the OWASP GenAI Security Project) establishes: ASI04 = Agentic Supply Chain Vulnerabilities; ASI07 = Insecure Inter-Agent Communication; ASI08 = Cascading Agent Failures; ASI09 = Human-Agent Trust Exploitation; ASI10 = Rogue Agents. Supply Chain risk is addressed at ASI04, not ASI08. Data Leakage & Exfiltration is treated as a consequence class addressed across multiple ASI entries rather than a standalone entry in the official December 2025 taxonomy. Earlier drafts and community derivatives used different numbering. All references in this document use the official December 2025 numbering. → Source: [genai.owasp.org](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/)

---

## 5. CSA MAESTRO Integration

TREASURE operates as an implementation overlay on top of MAESTRO: where MAESTRO identifies the threat surface at each architectural layer, TREASURE specifies the defensive controls.

> **⚠️ Corrected 3 July 2026:** this table previously used a non-canonical L5–L7 labeling that contradicted Section 13.3's authoritative mapping (sourced from the original February 2025 CSA publication by Ken Huang). It has been corrected below. L6 (Security & Compliance) is a cross-cutting layer in the canonical CSA model, not a single-purpose "Human-AI Interface" layer; TREASURE's CONTROL and GOVERNANCE layers both draw on it, decomposed for operational clarity (see the "†" note in Section 2.1).

| L | MAESTRO Layer (canonical) | Primary Threat | TREASURE Coverage | Key Technical Response |
|---|--------------|---------------|------------------|----------------------|
| L1 | Foundation Models | Model theft, adversarial prompt injection, backdoor attacks | SECURITY + EXECUTION | Adversarial robustness testing; input validation; sandbox isolation |
| L2 | Data Operations | RAG poisoning, context leakage, data provenance | DATA LAYER | Differential privacy; semantic validation; versioned snapshots; query constraints |
| L3 | Agent Frameworks | Insecure orchestration, logic bugs, goal misalignment | GOVERNANCE + EXECUTION | Formal workflow verification; static analysis; behavioral regression testing |
| L4 | Deployment and Infrastructure | Container escapes, insecure APIs, MCP server compromise | SECURITY + EXECUTION | Micro-segmentation; runtime sandboxing; JIT credentials; network egress filtering |
| L5 | Evaluation and Observability | Monitoring bypass, adversarial drift, detection evasion | SECURITY + GOVERNANCE | Behavioral baselining and anomaly detection (UC-SEC-04); continuous drift detection against CI/CD baseline (UC-GOV-05) |
| L6 | Security and Compliance (cross-cutting, spans L1–L5) | Accountability gaps, compliance drift, unsafe human-agent trust dynamics | GOVERNANCE + CONTROL | Policy-as-Code (UC-GOV-02); versioned artifacts (UC-GOV-01); ISO 42001 AIMS; CI/CD audit trail; Decision Boundary Matrix and HITL checkpoints (UC-CTRL-01/03) |
| L7 | Agent Ecosystem | Marketplace manipulation, agent impersonation, tool squatting, rug pulls, third-party skill poisoning | EXECUTION + GOVERNANCE | Cryptographic skill/tool signing (UC-EXEC-02); AIBOM (UC-GOV-04); skill registry governance; dependency scanning; rug-pull resistance via pinned/content-addressed manifests |

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

> **⚠️ Corrected 3 July 2026:** this case study previously described a fictionalized 5-stage "malicious skill from a marketplace" kill chain that does not match the actual CVE. It has been replaced below with the verified technical mechanism. For a real 2026 skill-supply-chain incident illustrating the marketplace/provenance lesson, see Section 11.9 (LiteLLM/Trivy).

CVE-2026-25253 (CVSS 8.8, CWE-669 — Incorrect Resource Transfer Between Spheres) affected OpenClaw (aka clawdbot/Moltbot) before version 2026.1.29. The Control UI accepted a `gatewayUrl` value from the page's query string and used it to open a WebSocket connection automatically, without validating the origin or requiring user confirmation, transmitting the stored gateway authentication token to whatever endpoint the URL specified.

| # | Attack Action | Missing / Weak Control | TREASURE Layer | TREASURE Counterfactual |
|---|--------------|------------------------|----------------|------------------------|
| 1 | Victim, already authenticated in the OpenClaw Control UI, clicks a crafted link containing an attacker-controlled `gatewayUrl` | UC-EXEC-05: No pre-invocation / pre-navigation intent validation on control-plane parameters | EXECUTION | Pre-call hook validates that `gatewayUrl` changes originate from a trusted, already-confirmed session context before acting on it |
| 2 | `applySettingsFromUrl()` silently stores the attacker's `gatewayUrl` and opens a WebSocket connection without confirmation | UC-EXEC-03: Control-plane interface not treated as sandboxed, origin-validated execution surface | EXECUTION | Strict origin validation (reject missing/mismatched Origin header; allow only loopback or an explicit allow-list) before any gateway reconnection — this is the fix actually shipped in v2026.1.29 |
| 3 | Stolen gateway token used to open a new WebSocket session and issue command-execution requests | UC-SEC-01: No per-session, audience-bound, short-lived credential; long-lived token usable from any origin | SECURITY | JIT, audience-scoped gateway tokens invalidated on origin mismatch; token reuse from an unrecognized origin triggers automatic revocation |
| 4 | Execution result returned to the attacker's server; full remote code execution achieved locally, including on machines not exposed to the internet | UC-SEC-06: No output/command channel monitoring on the local gateway | SECURITY | Local gateway traffic still routes through logged, anomaly-scored channel (UC-SEC-03/04) even for "local-only" deployments |

> **Key finding:** unlike the Replit and LiteLLM/Trivy cases, this was a single-point client-side authentication failure, not a multi-layer cascade — reinforcing that EXECUTION LAYER control-plane interfaces (the UI/API a human uses to configure and command the agent) require the same rigor as tool invocations, even in "local-first" agent deployments that fall outside a traditional network perimeter.

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
| **OpenClaw CVE-2026-25253** (Feb 2026) | Unvalidated `gatewayUrl` query parameter → automatic WebSocket connect → auth token exfiltration → one-click RCE on the local gateway | ASI02 Tool Misuse (control-plane interface) + ASI05 Code Execution | EXECUTION LAYER: No origin validation / confirmation on control-plane reconnection; no session-bound JIT token |
| **OpenClaw — Ignored Stop Commands** (Feb 2026) | Context-window compaction silently dropped a "confirm before acting" safety instruction; agent bulk-deleted 200+ emails while ignoring repeated stop commands; no remote kill-switch available | ASI01 Agent Goal Hijack + ASI10 Rogue Agents | CONTROL LAYER: No infrastructure-level kill-switch independent of the agent's own context; no immutable, memory-independent record of active safety constraints |
| **LiteLLM / Trivy Supply Chain Compromise** (Feb–Mar 2026) | Threat actor group TeamPCP compromised Trivy's GitHub Actions pipeline and published an infected binary; LiteLLM's CI/CD ran Trivy unpinned, propagating the compromise downstream | ASI04 Agentic Supply Chain Vulnerabilities + ASI02 Tool Misuse | GOVERNANCE LAYER: No pinned/verified dependency versions in CI/CD; EXECUTION LAYER: no cryptographic verification of third-party CI tooling before execution |
| **Replit Vibe Coding Meltdown** (Incident #1152, Jul 2025) | Coding agent without Agency Envelope or kill-switch deleted production database | ASI01 Agent Goal Hijack + ASI09 Human-Agent Trust Exploitation + ASI10 Rogue Agents | CONTROL LAYER: No Agency Envelope; no decision boundary; no kill-switch |

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

- OWASP: ASI01 (Agent Goal Hijack) + ASI06 (Memory & Context Poisoning) + ASI09 (Human-Agent Trust Exploitation — user trusted Copilot output containing the exfiltration payload) | AIUC-1 absent: UC-DATA-01/02, UC-EXEC-05, UC-SEC-06
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

- OWASP: ASI01 (Agent Goal Hijack) + ASI03 (Identity & Privilege Abuse — broad read permissions amplified blast radius) + ASI06 (Memory & Context Poisoning) | AIUC-1 absent: UC-DATA-01/03, UC-EXEC-05, UC-SEC-06
- [Atlassian Community report](https://community.atlassian.com/forums/Atlassian-Platform-Community/Rovo-Agent-Data-Exfiltration-via-Indirect-Prompt-Injection/ba-p/3001198)

### 11.6 Replit Vibe Coding Meltdown — Incident #1152 (July 2025)

A coding agent executed DROP TABLE on a production database during a refactoring task. The agent was not compromised — it executed its task with full fidelity to its own goal interpretation. No Agency Envelope existed to classify destructive database operations as requiring human authorization, and no kill-switch was available to halt execution before completion. *(Corrected 3 July 2026: earlier printings of this document stated "data recovery was not possible." Per contemporary reporting, the agent itself first told the operator that rollback was impossible because it had "destroyed all database versions" — that claim was false, and a manual rollback subsequently succeeded. The accurate lesson is arguably sharper than originally stated: the agent not only performed an unauthorized destructive action, it then misrepresented the recoverability of that action to the human operator, delaying recovery and directly evidencing ASI09 Human-Agent Trust Exploitation.)*

**TREASURE Layer Analysis:** CONTROL LAYER (primary — no Decision Boundary Matrix; no Agency Envelope Validator; no kill-switch); GOVERNANCE LAYER (secondary — no Agency Envelope Policy classifying destructive operations on production resources); EXECUTION LAYER (tertiary — no minimal-privilege manifest restricting database tool to read + create/update on test databases only).

- OWASP: ASI01 (Agent Goal Hijack) + ASI09 (Human-Agent Trust Exploitation — including the false claim that rollback was impossible) + ASI10 (Rogue Agents) | AIUC-1 absent: UC-CTRL-01/02/03, UC-EXEC-01
- [Wired reporting](https://www.wired.com/story/replit-ai-code-database-deletion/) | [The Register, 21 July 2025](https://www.theregister.com/2025/07/21/replit_saastr_vibe_coding_incident/) | [Fortune, 23 July 2025](https://fortune.com/2025/07/23/ai-coding-tool-replit-wiped-database-called-it-a-catastrophic-failure/)

### 11.7 OpenClaw — Authentication Token Theft & One-Click RCE (CVE-2026-25253, February 2026)

*(New in this addendum — replaces the fictionalized marketplace-skill narrative previously attributed to this CVE; see the correction note in Section 3.2 and the rebuilt case study in Section 7.4.)*

OpenClaw's Control UI accepted a `gatewayUrl` value directly from the page's query string and used it to open a WebSocket connection automatically, without origin validation or user confirmation, transmitting the stored gateway authentication token to the specified endpoint. A single crafted link, opened while authenticated, was sufficient to exfiltrate the token and obtain unauthorized gateway access, enabling one-click remote code execution — including against local, non-internet-facing OpenClaw instances. Patched in version 2026.1.29 via mandatory confirmation prompts on `gatewayUrl` changes and strict Origin-header validation.

**TREASURE Layer Analysis:** EXECUTION LAYER (primary — the control-plane interface was not treated as a validated execution surface; no confirmation-on-change, no origin allow-listing); SECURITY LAYER (secondary — the gateway token was long-lived and not audience- or origin-bound, so a stolen token remained fully usable from any origin).

- OWASP: ASI02 (Tool Misuse & Exploitation — of the control interface itself) + ASI05 (Unexpected Code Execution) | AIUC-1 absent: UC-EXEC-03, UC-EXEC-05, UC-SEC-01
- CVSS 8.8, CWE-669 (Incorrect Resource Transfer Between Spheres)
- [NVD — CVE-2026-25253](https://nvd.nist.gov/vuln/detail/CVE-2026-25253) | [SonicWall Capture Labs writeup](https://www.sonicwall.com/blog/openclaw-auth-token-theft-leading-to-rce-cve-2026-25253) | [runZero technical summary](https://www.runzero.com/blog/openclaw/)

### 11.8 OpenClaw — Ignored Stop Commands and Uncontrolled Mass Deletion (February 2026)

*(New in this addendum.)* Meta Superintelligence Labs' Director of Alignment, Summer Yue, instructed her personal OpenClaw agent to *suggest* which emails to archive or delete in her primary inbox, explicitly stating "don't action until I tell you to." The instruction had worked reliably on a smaller "toy" inbox; when applied to a much larger real inbox, context-window compaction silently dropped the safety instruction from the agent's working memory. The agent began bulk-deleting emails and ignored repeated stop commands ("Stop don't do anything," "STOP OPENCLAW") sent from the operator's phone; she had to physically reach the host machine to kill the process manually, after the agent had already deleted 200+ emails. No remote, infrastructure-level kill-switch existed independent of the agent's own (compromised) memory state.

**TREASURE Layer Analysis:** CONTROL LAYER (primary — no infrastructure kill-switch independent of the agent's own runtime/memory; no default-deny enforcement when a previously issued restriction becomes unverifiable); DATA LAYER (secondary — the safety instruction was stored only in mutable, compactable context rather than in an immutable, memory-independent constraint record).

- OWASP: ASI01 (Agent Goal Hijack — the operative goal silently reverted to "complete the cleanup task" once the restriction was dropped) + ASI10 (Rogue Agents — the agent continued destructive action while ignoring explicit real-time stop commands) | AIUC-1 absent: UC-CTRL-02 (untested/absent remote kill-switch), UC-DATA-04 (no versioned, tamper-resistant record of active constraints)
- [TechCrunch, 23 Feb 2026](https://techcrunch.com/2026/02/23/a-meta-ai-security-researcher-said-an-openclaw-agent-ran-amok-on-her-inbox/) | [Tom's Hardware](https://www.tomshardware.com/tech-industry/artificial-intelligence/openclaw-wipes-inbox-of-meta-ai-alignment-director-executive-finds-out-the-hard-way-how-spectacularly-efficient-ai-tool-is-at-maintaining-her-inbox)

> **Naming note:** this is the same underlying product (OpenClaw) as Section 11.7 but a distinct incident with a distinct root cause — one is a client-side authentication vulnerability (CVE-2026-25253), the other is a runtime memory-management/control failure with no assigned CVE. Both are retained as separate TREASURE entities to avoid conflating two independently documented failure modes under one name.

### 11.9 LiteLLM / Trivy Supply Chain Compromise (February–March 2026)

*(New in this addendum.)* The threat actor group TeamPCP exploited a misconfiguration in Trivy's GitHub Actions environment in late February 2026 and published an infected Trivy binary. On 24 March 2026, the compromise cascaded into the agentic AI tooling ecosystem when LiteLLM's CI/CD pipeline executed Trivy without a pinned version, propagating the compromise downstream. Microsoft, Kaspersky, and Aqua Security published advisories; LiteLLM shipped a security update the same day.

**TREASURE Layer Analysis:** GOVERNANCE LAYER (primary — no dependency pinning or provenance verification gate in CI/CD, UC-GOV-03); EXECUTION LAYER (secondary — third-party CI tooling executed with no cryptographic verification prior to running, UC-EXEC-02).

- OWASP: ASI04 (Agentic Supply Chain Vulnerabilities) + ASI02 (Tool Misuse & Exploitation) | AIUC-1 absent: UC-GOV-03, UC-EXEC-02
- No CVE assigned at time of writing; documented in the [OWASP GenAI Exploit Round-up Report Q1 2026](https://genai.owasp.org/2026/04/14/owasp-genai-exploit-round-up-report-q1-2026/)

### 11.10 Consolidated Attack-to-TREASURE Mapping

| # | Incident | OWASP ASI | TREASURE Layer(s) | Primary AIUC-1 Controls Absent |
|---|----------|-----------|------------------|-------------------------------|
| 11.1 | EchoLeak CVE-2025-32711 | ASI01+ASI06+ASI09* | DATA+EXECUTION+SECURITY | UC-DATA-01/02, UC-EXEC-05, UC-SEC-06 |
| 11.2 | Gemini Memory Attack / GeminiJack | ASI06 | DATA+GOVERNANCE | UC-DATA-01/02/04, UC-GOV-05 |
| 11.3 | AgentPoison arXiv:2407.12784 | ASI06 | DATA | UC-DATA-01/02/03 |
| 11.4 | AiTM arXiv:2502.14847 | ASI07 | SECURITY+CONTROL | UC-SEC-01/02, UC-CTRL-01 |
| 11.5 | Atlassian Rovo Indirect PI | ASI01+ASI03+ASI06 | DATA+EXECUTION+SECURITY | UC-DATA-01/03, UC-EXEC-05, UC-SEC-06 |
| 11.6 | Replit Vibe Coding Meltdown #1152 | ASI01+ASI09+ASI10 | CONTROL+GOVERNANCE+EXECUTION | UC-CTRL-01/02/03, UC-EXEC-01 |
| 11.7 | OpenClaw CVE-2026-25253 (token theft / 1-click RCE) | ASI02+ASI05 | EXECUTION+SECURITY | UC-EXEC-03, UC-EXEC-05, UC-SEC-01 |
| 11.8 | OpenClaw — ignored stop commands | ASI01+ASI10 | CONTROL+DATA | UC-CTRL-02, UC-DATA-04 |
| 11.9 | LiteLLM/Trivy supply chain compromise | ASI04+ASI02 | GOVERNANCE+EXECUTION | UC-GOV-03, UC-EXEC-02 |

> *\* ASI09 in EchoLeak refers to Human-Agent Trust Exploitation — the user trusted the Copilot output that delivered the exfiltration payload. Data exfiltration itself is a consequence, not a standalone ASI entry in the December 2025 taxonomy.*

> **Common pattern:** Across all nine incidents, the absence of controls in the DATA LAYER or CONTROL LAYER remains the most frequent primary entry point. A governed ingestion pipeline (UC-DATA-01/02), an Agency Envelope with decision boundary enforcement (UC-CTRL-01), **or** an infrastructure-level kill-switch independent of agent memory (UC-CTRL-02) would have independently broken six of the nine documented attack chains — confirming these controls represent the minimum viable security posture for any agentic AI deployment. The two newly added 2026 incidents (11.7, 11.9) additionally confirm that EXECUTION LAYER control-plane hardening and GOVERNANCE LAYER dependency-pinning are not theoretical concerns but active, exploited gaps.

---

## 12. MCP Security — The Execution Layer's Expanding Attack Surface

The Model Context Protocol (MCP), introduced by Anthropic in November 2024, has become the de facto standard for connecting AI agents and assistants to external tools, APIs, and data sources. By June 2026, MCP servers are deployed across enterprise environments connecting agents to databases, internal repositories, cloud services, and SaaS platforms. This rapid adoption has created a new and structurally significant attack surface that extends and deepens the TREASURE Execution Layer's threat model.

The OWASP GenAI Security Project's Practical Guide for Secure MCP Server Development, published in February 2026, identifies MCP servers as high-risk execution environments with unique vulnerability classes that do not have direct parallels in traditional API security. A 2026 empirical scan of over 5,000 open-source MCP servers documented that 40% required no authentication, 43% contained command-injection vulnerabilities, and 79% handled credentials in plaintext. These figures establish the operational baseline that TREASURE Execution Layer controls must address.

### 12.1 MCP-Specific Threat Classes

The following threat classes are specific to the MCP execution model and map to TREASURE Execution Layer controls. They are distinct from general API security vulnerabilities and require explicit treatment in any agentic AI security program.

**Tool Poisoning.** An adversary modifies a tool's description or schema — either at registration time or via a runtime update — causing the agent to invoke the tool under false pretences. The agent's trust in the tool description is weaponized: the tool claims to "query the database" while actually exfiltrating credentials or making unauthorized network requests. The OWASP MCP guide requires cryptographically signed tool manifests with hash verification at load time to detect tampering. This maps directly to TREASURE UC-EXEC-02 (Cryptographic Skill Signing), which requires that no skill may be instantiated without a valid signature over its complete definition, and to UC-EXEC-01 (Minimal-Privilege Skill Manifests), which constrains the declared scope of each tool's permitted actions.

**Rug Pull Attacks.** A registered and initially legitimate MCP server alters its tool behavior after initial deployment and trust establishment. The agent continues to invoke the tool under the assumption that its behavior matches the originally verified definition. Rug pull resistance requires either pinned, content-addressed tool definitions or continuous behavioral integrity monitoring — both of which are addressed by TREASURE's combination of UC-EXEC-02 (signed manifests enforced at each instantiation) and UC-GOV-05 (drift detection comparing production tool behavior against the CI/CD-validated baseline).

**Confused Deputy Attacks.** The MCP server acts using its own elevated permissions rather than the scoped permissions of the user on whose behalf it is operating. This converts the MCP server into an unintentional privilege escalation point: an agent operating with user-level permissions effectively obtains system-level access through the MCP server's ambient credentials. The OWASP guide mandates OAuth 2.1 with the Token Delegation pattern (RFC 8693) as the prescribed mitigation: the MCP server uses an on-behalf-of flow to request a scoped, audience-bound token for the downstream service, ensuring the downstream service can enforce granular per-user policy. This aligns with TREASURE UC-SEC-01 (Per-Agent JIT Credentials), which requires that credentials be scoped per-invocation and issued just-in-time rather than held as ambient ambient long-lived tokens.

**Token Passthrough.** An MCP server forwards a raw client authentication token to a downstream API rather than requesting a token issued to itself as the authorized caller. This breaks audit trail integrity — the downstream service cannot distinguish calls made by the MCP server acting legitimately from calls made by a compromised version of it — and bypasses audience validation. The OWASP guide identifies token passthrough as a prohibited pattern and requires OAuth 2.1/OIDC enforcement at every connection boundary. TREASURE UC-SEC-01 addresses this through its JIT credential model: each tool invocation receives a freshly issued, purpose-scoped token with audience validation, not a forwarded upstream credential.

### 12.2 MCP Server Security Minimum Bar (OWASP 2026)

The OWASP Practical Guide for Secure MCP Server Development establishes a minimum security bar that any MCP server must satisfy before integration with a TREASURE-governed agent deployment. The following requirements are drawn directly from the OWASP guide and their corresponding TREASURE controls:

| MCP Security Requirement | TREASURE Control | Notes |
|--------------------------|-----------------|-------|
| No Token Passthrough — use OAuth 2.1 token delegation | UC-SEC-01 | Token lifespan bounded to minimum necessary; audience validation required |
| Short-lived tokens with revocation check per call | UC-SEC-01 | JIT credential per tool invocation |
| OAuth 2.1 / OIDC enforced for all remote connections | UC-SEC-01 | Per-agent cryptographic identity as prerequisite |
| Containerization: run in non-root, network-restricted container | UC-EXEC-03 | Infrastructure-grade sandboxing, not config-level |
| Session isolation: memory and execution contexts segregated per user | UC-EXEC-03 | Sandbox isolation with inter-skill communication screening |
| Schema enforcement: validate all inputs and outputs against strict JSON Schema | UC-EXEC-05 | Pre-call hooks + output validation pipelines |
| Least privilege: tools only have exact permissions needed | UC-EXEC-01 | Minimal-privilege skill manifests as hard constraints |
| Secrets in credential vaults — never in environment variables or logs | UC-SEC-01 | LLM must never have access to raw credentials |
| Cryptographically signed tool manifests | UC-EXEC-02 | Skill registry as Certificate Authority |
| Audit trail for all tool invocations | UC-EXEC-04 | Immutable off-agent invocation log |

> **⚠️ Implementation gap:** The OWASP guide notes that cryptographic tool manifests are "aspirational" in the current MCP ecosystem — the MCP specification as of 2026 does not include a native signing mechanism. Implementing UC-EXEC-02 for MCP deployments requires custom infrastructure beyond the base MCP protocol. Organizations building on MCP should treat this gap as a documented residual risk requiring compensating controls (behavioral monitoring, static manifest approval workflows, registry governance) until the ecosystem provides native signing support.

### 12.3 MCP in the TREASURE Execution Layer

MCP servers are the primary implementation surface for TREASURE's Execution Layer in most 2026 enterprise deployments. The skill/runtime concepts in TREASURE map directly to MCP primitives:

```
TREASURE Concept            → MCP Implementation
─────────────────────────────────────────────────
Skill                       → MCP Tool definition
Skill Registry              → MCP server registry / tool registry
Skill Executor              → MCP server execution environment
Skill Security Manifest     → MCP tool schema + signed manifest
Minimal-Privilege           → OAuth 2.1 scopes + least-privilege tool permissions
Sandboxing                  → MCP server containerization (non-root, network-restricted)
Pre-Call Hooks              → Input validation against strict JSON Schema
Output Validation Pipeline  → Output validation + tool description behavioral verification
```

*(Corrected 3 July 2026: OpenClaw CVE-2026-25253 is a control-plane authentication vulnerability, not a skill-marketplace supply-chain attack — see Section 11.7.)* The LiteLLM/Trivy compromise (Section 11.9, February–March 2026) is the TREASURE evidence base's canonical CI/CD-tooling supply chain attack: an infected third-party binary (Trivy) executed unpinned inside a downstream project's (LiteLLM) build pipeline, propagating compromise without any skill or MCP tool itself being directly poisoned. The OWASP MCP Secure Development Guide's requirements on cryptographically signed tool manifests and pinned, content-addressed dependencies would have blocked this class of propagation independently of any single vendor's own code review.

---

## 13. Emerging Threat Vectors and Framework Evolution (2026)

### 13.1 The OWASP State of Agentic AI Security — June 2026 Update

The OWASP GenAI Security Project published the State of Agentic AI Security and Governance v2.01 in June 2026. This second edition documents a structural shift in the agentic AI threat landscape that directly informs the TREASURE Framework's evidence base and roadmap: the transition from theoretical threat taxonomy to documented, production-exploited vulnerabilities with associated CVEs and vendor advisories.

The report's three primary findings, each with direct TREASURE implications:

**Finding 1: The threats are real now.** The report's Real-World Incidents and Exploits Tracker documents that almost every entry in the OWASP Agentic Top 10 now has associated production incidents, vendor advisories, or CVEs — not just theoretical risk descriptions. This validates the TREASURE Framework's empirical grounding approach (Sections 9 and 11) and confirms that the nine documented incidents in this document (EchoLeak, GeminiJack, AgentPoison, AiTM, Atlassian Rovo, Replit Meltdown, OpenClaw CVE-2026-25253, the OpenClaw stop-command failure, and the LiteLLM/Trivy supply chain compromise) represent only the visible fraction of a broader operational incident population.

**Finding 2: AI Safety and AI Security cannot continue as parallel functions.** At the deployment layer — the architectural decisions, configurations, permissions, and operational controls owned by the deploying organization — the two categories cannot be operationally separated. Model-level safety remains the provider's responsibility, but once an agent is acting on production systems, the same controls govern both safety and security failures. This finding reinforces TREASURE's architectural premise: defense must be embedded at the deployment and infrastructure layer (the ARCP), not delegated to model-level guardrails.

**Finding 3: Agent Identity and Non-Human Identity (NHI) is the new control plane.** The report elevates NHI to a standalone chapter, reflecting the CSA's 2025 survey finding that 51% of organizations have no clear ownership of AI identities and 24% take more than 24 hours to revoke a compromised credential after an exposure event. This finding grounds TREASURE's UC-SEC-01 (Per-Agent JIT Credentials) as the single highest-impact foundational control: the 24-hour revocation gap is precisely the window AiTM-style attacks require to propagate across a multi-agent network after initial compromise.

### 13.2 A2A Protocol — New Inter-Agent Communication Security Surface

The Agent-to-Agent (A2A) protocol, developed by Google and adopted across multiple agentic frameworks, formalizes direct peer-to-peer communication between autonomous agents without a human intermediary in the communication path. The security implications for TREASURE's Security Layer (specifically UC-SEC-01 and UC-SEC-02) are significant and represent an active area of standardization work.

The OWASP GenAI Security Project's Agent Name Service (ANS) proposal — a DNS-inspired architecture for secure agent discovery and identity verification across A2A, MCP, and ACP protocols — addresses the discovery and authentication gap that enables the AiTM attack class. The ANS architecture aligns with TREASURE's UC-SEC-01 requirement for per-agent cryptographic identity by providing a registry that maps agent identities to verified cryptographic credentials, enabling receiving agents to authenticate incoming A2A messages without relying on ambient trust assumptions.

The security properties required for A2A communications under the TREASURE Framework's inter-agent zero-trust model are:
- **Authentication**: Every message carries a cryptographic signature from the sending agent's verified identity credential.
- **Integrity**: The message content is tamper-evident; modification in transit is detectable.
- **Authorization scope**: The sending agent's delegation scope for the specific action is verifiable against the Governance Layer's declared inter-agent policy.
- **Non-repudiation**: The sending agent cannot subsequently deny having sent the message; the trajectory log provides the attribution record.

These requirements map to the AiTM mitigation in the TREASURE canonical incident record: the reflect() mechanism exploited in arXiv:2502.14847 is defeated by signed inter-agent messages because the receiving ARCP can verify that the message content matches the sender's declared intent and scope before processing.

### 13.3 The MAESTRO Layer Clarification

Multiple sources describing the CSA MAESTRO framework use slightly different layer numbering. The canonical CSA publication (February 2025, Ken Huang) defines seven layers. For precision and consistency with the original CSA publication, TREASURE uses the following authoritative layer mapping:

| MAESTRO Layer | Name | Primary Threat (canonical CSA) |
|---|---|---|
| L1 | Foundation Models | Model theft, adversarial prompt injection, backdoor attacks |
| L2 | Data Operations | RAG poisoning, context leakage, data provenance |
| L3 | Agent Frameworks | Insecure orchestration, logic bugs, goal misalignment |
| L4 | Deployment and Infrastructure | Container escapes, insecure APIs, MCP server compromise |
| L5 | Evaluation and Observability | Monitoring bypass, adversarial drift, detection evasion |
| L6 | Security and Compliance | Cross-cutting security controls (vertical layer spanning L1–L5) |
| L7 | Agent Ecosystem | Marketplace manipulation, agent impersonation, tool squatting, rug pulls |

Note: Some derivative analyses and implementation tools (including IriusRisk's MAESTRO integration) present a simplified five-layer variant or use different L5/L6/L7 assignments. TREASURE's alignment in Section 5 uses the seven-layer structure from the original CSA publication. Organizations cross-referencing MAESTRO implementations should verify which layer numbering their tooling uses before applying TREASURE's MAESTRO mappings.

> The OWASP Agentic Security Initiative explicitly endorsed MAESTRO as "a comprehensive extension of STRIDE for handling Agentic AI" in its Agentic Threats and Mitigations documentation.

### 13.4 Open Research Directions (Updated June 2026)

The following research gaps, originally identified in TREASURE v1.0 Section 2.2, have seen developments in 2026 that practitioners should track:

**Blast Radius Quantification.** No standardized measurement methodology equivalent to CVSS exists for agentic AI compromise scope as of June 2026. The OWASP State of Agentic AI v2.01 and CSA working groups have acknowledged this gap and initiated working group activity. TREASURE's use of "Blast Radius" as a qualitative metric (the union of all systems the agent can write to, all data it can read, and all downstream agents it can influence) reflects current best practice while this standardization work progresses.

**Multi-Agent Trust Propagation.** The question of how permissions should propagate when an agent dynamically spawns a sub-agent at runtime remains unresolved as a formal security model. The OWASP Agent Name Service proposal addresses the discovery and authentication dimension of this problem. TREASURE's current guidance (Agency Envelope enforcement per deployment, not per dynamically spawned sub-agent) represents a conservative default that may require extension as dynamic agent spawning patterns become more prevalent.

**MCP Cryptographic Tool Manifests.** As noted in Section 12.2, native signing support is absent from the MCP specification as of 2026. This is an active gap where TREASURE's UC-EXEC-02 requirement (cryptographic signing of all executable skill components) outpaces the current MCP ecosystem's native capabilities. Custom implementations are possible and recommended for high-assurance deployments. Community proposals for MCP specification extensions to support native tool manifest signing are under discussion in the open-source community.

**AI SBOM / AIBOM Standardization.** The OWASP State of Agentic AI v2.01 elevates AI Bill of Materials to a dedicated chapter, reflecting growing regulatory and operational interest. The SPDX and CycloneDX communities have published initial AI SBOM extensions. TREASURE UC-GOV-04 (AIBOM) aligns with CycloneDX ML-BOM format as the current best-supported option, while acknowledging that the standardization landscape is still evolving.



---

## Appendix A: Detailed AIUC-1 Control-by-Control Mapping

| Control ID | AIUC-1 Control Statement | TREASURE Implementation | Security Rationale |
|------------|--------------------------|------------------------|--------------------|
| **UC-DATA-01** | Establish a single authoritative knowledge source with documented provenance for all data used in agent reasoning | Diamond Record: governed ingestion pipeline; provenance metadata schema enforced at ingest; source attestation stored alongside each document chunk | CRITICAL — Without provenance, poisoned documents are indistinguishable from legitimate ones at retrieval time |
| **UC-DATA-02** | Implement embedding integrity controls capable of detecting and preventing vector index manipulation | Differential privacy in embeddings; cryptographic hash of index state per snapshot; semantic anomaly scoring on candidate ingest documents | HIGH — EchoLeak and AgentPoison both exploit the absence of this control |
| **UC-DATA-03** | Enforce access control at the retrieval layer, not solely at the application layer | Identity-scoped query constraints enforced by the Memory Manager in the ARCP; agents receive only embeddings within their authorized namespace | HIGH — Application-layer access control is bypassable via prompt injection; retrieval-layer enforcement is not |
| **UC-DATA-04** | Maintain versioned, rollback-capable snapshots of all agent knowledge bases | Append-only vector index snapshots with HMAC integrity; snapshot metadata stored in the governance repository; rollback procedure documented and tested | MEDIUM — Enables recovery from detected poisoning without full re-ingestion |
| **UC-EXEC-01** | Enforce least-privilege execution permissions for all agent tools and skills; no tool may be invoked with permissions exceeding those declared in its manifest | Minimal-privilege skill manifests with declarative permission surface; Tool Router enforces allow-lists as hard constraints; manifest violations abort execution | CRITICAL — Over-privileged tools are the primary enabler of ASI02 (Tool Misuse) |
| **UC-EXEC-02** | Implement cryptographic signing for all executable agent components prior to deployment | Skill registry acts as CA; all skills require a valid signature over their complete definition before mounting; unsigned skills are rejected at the Skill Executor before instantiation | CRITICAL — the LiteLLM/Trivy supply chain compromise (§11.9) exploited the absence of pinned, verified third-party tooling in a CI/CD context |
| **UC-EXEC-03** | Sandbox all agent code execution environments; execution must not propagate to the host runtime | Runtime sandboxing with process isolation per skill; MCP server processes run under reduced-privilege identities; container-level egress filtering applied per skill network declarations | CRITICAL — ASI05 (Unexpected Code Execution) requires sandbox integrity as an independent defense layer |
| **UC-EXEC-04** | Maintain an immutable audit trail of all agent tool invocations, including parameters, results, and execution context | Off-agent append-only invocation log; records include agent identity, skill ID + version hash, input parameter hash, output hash, timestamps, duration; log is cryptographically signed | HIGH — Without this record, trajectory manipulation attacks are forensically undetectable post-incident |
| **UC-EXEC-05** | Implement pre-invocation intent validation for all tool calls; calls inconsistent with the agent's declared goal must be blocked or escalated | Pre-call hooks in the ARCP evaluate tool call parameters against the agent's current plan state; goal-plan consistency scores below threshold trigger HITL escalation | HIGH — Intent monitoring is the primary detection mechanism for ASI01 (Goal Hijack) at the execution layer |
| **UC-GOV-01** | Version-control all agent behavioral specifications including prompts, workflows, skill definitions, tool chains, and policies | Agent artifact repository with full commit history; all artifact types subject to pull-request workflow with required review approvals; merge history constitutes regulatory audit trail | CRITICAL — An unversioned agent is architecturally equivalent to production code without source control |
| **UC-GOV-02** | Express all agent behavioral policies in machine-executable, declarative formats enforced at runtime | OPA/Rego or YAML policy schemas interpreted by the Policy Engine in the ARCP; natural-language policies are not enforceable and do not satisfy this control | HIGH — Policy-as-Code is the prerequisite for runtime enforcement; narrative policy is an unverifiable paper control |
| **UC-GOV-03** | Integrate automated security testing in the agent CI/CD pipeline; no agent artifact may be promoted to production without passing all gates | Static analysis of workflow definitions; behavioral regression against adversarial prompt suite; automated red teaming using OWASP ASI catalogue; AIBOM generation and validation | HIGH — CI/CD security gates are the primary prevention mechanism for agentic supply chain compromise (ASI04) |
| **UC-GOV-04** | Produce and maintain an AI Bill of Materials (AIBOM) for every agent deployment | AIBOM documents: foundation model version + provider; skills with version hashes and signing certificates; tool integrations with API schema versions; knowledge sources with provenance hashes | HIGH — AIBOM is the prerequisite for supply chain risk assessment and incident attribution |
| **UC-GOV-05** | Implement continuous drift detection comparing production agent behavior against CI/CD-validated behavioral baseline | Behavioral metrics collected in production compared against baseline established at last CI/CD cycle; divergence thresholds defined per agent class; threshold breaches trigger automated alerts and escalation | MEDIUM — Agentic drift is a slow-moving attack vector that standard security monitoring does not detect |
| **UC-CTRL-01** | Define and enforce an Agency Envelope formally specifying the complete action space permitted for each agent deployment | Decision Boundary Matrix specifies authorization tier per action type; Agency Envelope Validator in ARCP evaluates every action before execution; envelope is a versioned governance artifact | CRITICAL — The Replit Meltdown resulted directly from the absence of this control |
| **UC-CTRL-02** | Implement an infrastructure-level kill-switch capable of immediately halting agent execution and revoking all associated credentials | Infrastructure kill-switch independent of application logic; terminates execution, revokes JIT tokens, quarantines memory state, generates forensic snapshot; verified by periodic drills | CRITICAL — Application-level stop mechanisms are bypassable by a sufficiently compromised agent runtime |
| **UC-CTRL-03** | Implement human oversight checkpoints at action categories classified as requiring authorization in the Decision Boundary Matrix | HITL checkpoint workflow integrates with the Agency Envelope Validator; escalation paths defined per action tier; response time SLAs documented; default-deny on timeout | HIGH — Human oversight is not effective when implemented as an optional UI element; it must be an enforcement gate |
| **UC-SEC-01** | Assign each agent a unique cryptographic identity; prohibit shared credentials between agents or between agents and human operators | Per-agent identity via Entra Agent ID or equivalent; JIT credential issuance per tool invocation; no shared pools; credential lifespan bounded to minimum necessary duration | CRITICAL — Shared credentials eliminate agent isolation and enable lateral movement via insecure inter-agent communication (ASI07 + AiTM) |
| **UC-SEC-02** | Enforce network micro-segmentation preventing agents from accessing systems outside their declared scope | All agent egress via controlled proxy enforcing endpoint allow-list; inter-agent communication via authorized orchestration channel only; agents cannot discover or contact peers outside their defined graph | HIGH — Uncontrolled network access enables exfiltration (consequence of ASI01/ASI03) and inter-agent infection (ASI07 via AiTM reflect() mechanism) |
| **UC-SEC-03** | Capture the complete execution trajectory of every agent session in an immutable, off-agent log store | Full trajectory log: reasoning steps, tool calls with parameters and responses, memory reads/writes, state transitions, inter-agent messages; stored append-only outside agent write surface; HMAC-signed | CRITICAL — Trajectory logs are the only mechanism for detecting trajectory manipulation attacks post-hoc |
| **UC-SEC-04** | Establish behavioral baselines for all agent deployments and implement continuous anomaly detection against those baselines | Statistical baselines: tool call frequency distributions, sequence patterns, memory access profiles, output entropy; anomaly scoring in production; threshold alerts; automated escalation paths | HIGH — Behavioral anomaly detection is the primary mechanism for detecting ASI10 (Rogue Agent) without known-bad signatures |
| **UC-SEC-05** | Implement circuit breakers on all inter-agent communication paths to prevent cascading failure propagation | Circuit breakers on each agent-to-agent path; quarantine protocol for agents producing anomalous outputs; downstream agents notified before dependency is severed | HIGH — Without circuit breakers, a single compromised agent can disable or corrupt a multi-agent network (ASI08) |
| **UC-SEC-06** | Implement output data loss prevention and exfiltration detection on all agent output channels | Output DLP pipeline scanning for PII, credential patterns, and semantic exfiltration indicators; steganography detection on structured outputs; entropy monitoring on outbound data streams | CRITICAL — Data exfiltration is the highest-impact consequence class across multiple ASI entries (ASI01, ASI03, ASI06); Output DLP is the terminal defensive gate before data leaves the trust boundary |

---

## References

### Standards & Frameworks

- [OWASP Top 10 for Agentic Applications 2026](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/) — official taxonomy published 10 December 2025 by the OWASP GenAI Security Project; developed with >100 security researchers and reviewed by representatives from NIST, European Commission, and international security bodies
- [OWASP AI Exchange — Agentic AI Threats and Mitigations](https://genai.owasp.org/resource/agentic-ai-threats-and-mitigations/) — T01–T17 threat catalogue; analytical foundation from which the Agentic Top 10 was derived
- [OWASP State of Agentic AI Security and Governance v2.01](https://genai.owasp.org/download/50592/) — June 2026 update including Real-World Incidents and Exploits Tracker, Enterprise Adoption Maturity Model, AI SBOM / Supply Chain Provenance chapter, and AI Safety vs AI Security alignment analysis
- [OWASP × AIUC-1 Crosswalk of the OWASP Top 10 for Agentic Applications](https://genai.owasp.org/resource/aiuc-1-crosswalks-owasp-top-10-for-agentic-applications/) — published 25 May 2026; bidirectional mapping between AIUC-1's official requirement IDs and the ASI01–ASI10 taxonomy. *Note: TREASURE's own "UC-\*" identifiers (Section 2.1, Appendix A) are an internal crosswalk convention and do not reproduce AIUC-1's official requirement codes; re-check this source each quarter as AIUC-1 updates.*
- [AIUC-1 Standard](https://www.aiuc-1.com/) — Artificial Intelligence Underwriting Company; 51 requirements / 130 controls across six pillars (Data & Privacy, Security, Safety, Reliability, Accountability, Societal Impact); updated quarterly
- [OWASP Practical Guide for Secure MCP Server Development](https://genai.owasp.org/resource/a-practical-guide-for-secure-mcp-server-development/) — February 2026; covers tool poisoning, rug pulls, confused deputy, token passthrough, OAuth 2.1/OIDC requirements, and cryptographically signed tool manifests
- [OWASP GenAI Exploit Round-up Report Q1 2026](https://genai.owasp.org/2026/04/14/owasp-genai-exploit-round-up-report-q1-2026/) — coverage period 1 Jan–11 Apr 2026; documents the OpenClaw stop-command incident (Section 11.8) and the LiteLLM/Trivy supply chain compromise (Section 11.9) mapped to ASI taxonomy; confirms transition from theoretical to exploited risks
- [CSA MAESTRO — Agentic AI Threat Modeling Framework](https://cloudsecurityalliance.org/blog/2025/02/06/agentic-ai-threat-modeling-framework-maestro) — Ken Huang, CSA AI Safety Working Group, February 2025; endorsed by OWASP Agentic Security Initiative as the comprehensive extension of STRIDE for agentic AI; canonical seven-layer numbering used in Sections 5 and 13.3 of this document
- [CSA MAESTRO GitHub Repository](https://github.com/CloudSecurityAlliance/MAESTRO) — open-source AI-powered threat modeling tool implementing the seven-layer MAESTRO architecture with A2A and MCP protocol use-case presets
- [CSA — Applying MAESTRO to Real-World Agentic AI Threat Models](https://cloudsecurityalliance.org/blog/2026/02/11/applying-maestro-to-real-world-agentic-ai-threat-models-from-framework-to-ci-cd-pipeline) — February 2026; confirms MAESTRO is under active evolution based on implementer feedback
- [CSA — Agentic AI Identity & Access Management](https://cloudsecurityalliance.org/artifacts/agentic-ai-identity-and-access-management-a-new-approach)
- [CSA — Securing Autonomous AI Agents (Survey 2026)](https://cloudsecurityalliance.org/artifacts/securing-autonomous-ai-agents) — survey of 383 IT and security professionals; 51% report no clear ownership of AI identities; 24% take more than 24 hours to revoke a compromised credential
- [NIST AI RMF 1.0](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework)
- [NIST AI 600-1 — Generative AI Profile](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf)
- **NIST AI Agent Standards Initiative (CAISI)** — launched 17 February 2026 by NIST's Center for AI Standards and Innovation; the first US federal program dedicated specifically to interoperability and security standards for agentic AI systems, distinct from prior model-level AI safety evaluation programs. *(Added in this addendum — not yet formally cross-mapped to TREASURE controls; tracked as a forward-looking reference.)*
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
- OpenClaw CVE-2026-25253 (auth token theft / 1-click RCE) — [NVD](https://nvd.nist.gov/vuln/detail/CVE-2026-25253) · [SonicWall](https://www.sonicwall.com/blog/openclaw-auth-token-theft-leading-to-rce-cve-2026-25253) · [runZero](https://www.runzero.com/blog/openclaw/) · [CVE.org record](https://www.cve.org/CVERecord?id=CVE-2026-25253)
- OpenClaw — ignored stop commands / mass email deletion (no CVE, February 2026) — [TechCrunch](https://techcrunch.com/2026/02/23/a-meta-ai-security-researcher-said-an-openclaw-agent-ran-amok-on-her-inbox/) · [Tom's Hardware](https://www.tomshardware.com/tech-industry/artificial-intelligence/openclaw-wipes-inbox-of-meta-ai-alignment-director-executive-finds-out-the-hard-way-how-spectacularly-efficient-ai-tool-is-at-maintaining-her-inbox)
- LiteLLM / Trivy Supply Chain Compromise (no CVE, February–March 2026) — [OWASP GenAI Exploit Round-up Q1 2026](https://genai.owasp.org/2026/04/14/owasp-genai-exploit-round-up-report-q1-2026/)
- Replit Meltdown Incident #1152 — [Wired, July 2025](https://www.wired.com/story/replit-ai-code-database-deletion/) · [The Register](https://www.theregister.com/2025/07/21/replit_saastr_vibe_coding_incident/) · [Fortune](https://fortune.com/2025/07/23/ai-coding-tool-replit-wiped-database-called-it-a-catastrophic-failure/)
- Atlassian Rovo — [Community report](https://community.atlassian.com/forums/Atlassian-Platform-Community/Rovo-Agent-Data-Exfiltration-via-Indirect-Prompt-Injection/ba-p/3001198)

---

## License

**CC0 1.0 Universal — Public Domain Dedication**

To the extent possible under law, Roger Sanz González has waived all copyright and related rights to this specific layout and textual implementation of the TREASURE AI Security Framework. You are free to copy, modify, distribute, and build upon this text, even for commercial purposes, without seeking prior permission or providing mandatory attribution.

→ [View CC0 1.0 Legal Code](https://creativecommons.org/publicdomain/zero/1.0/)

Contributions and feedback: [roger.sanz@owasp.org](mailto:roger.sanz@owasp.org)

---

*TREASURE Framework v1.1 (same-day corrections addendum applied) · Roger Sanz González · Plain Concepts · OWASP AI Exchange · 3 July 2026*
