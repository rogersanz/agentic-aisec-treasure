# TREASURE Framework
## Defense-in-Depth Architecture for Agentic AI Systems

> *Tiered Resilient Execution Architecture for Secure Unified Robust Environments*

[![License: CC0-1.0](https://img.shields.io/badge/License-CC0_1.0-lightgrey.svg)](https://creativecommons.org/publicdomain/zero/1.0/)
[![OWASP](https://img.shields.io/badge/Aligned-OWASP%20GenAI%20Security-blue)](https://genai.owasp.org)
[![CSA MAESTRO](https://img.shields.io/badge/Aligned-CSA%20MAESTRO-orange)](https://cloudsecurityalliance.org)
[![NIST AI RMF](https://img.shields.io/badge/Aligned-NIST%20AI%20RMF-green)](https://www.nist.gov/artificial-intelligence)
[![MITRE ATLAS](https://img.shields.io/badge/Aligned-MITRE%20ATLAS%20v2026.08-red)](https://atlas.mitre.org)
[![ISO 42001](https://img.shields.io/badge/Aligned-ISO%2FIEC%2042001-blue)](https://www.iso.org/standard/81230.html)
[![Version](https://img.shields.io/badge/Version-1.2-brightgreen)]()

---

**Author:** Roger Sanz, PhD  
**Role:** AI Security Lead — Plain Concepts | Senior Researcher — Universidad Isabel I  
Lead Editor, OWASP AI Exchange | Contributor, MITRE ATLAS · CSA · ISMS Forum · DAMA  
TAISE · CRISC · C|CISO · CCSK · CCZT · ISO 27001/22301/42001 LA  
**Contact:** [roger.sanz@owasp.org](mailto:roger.sanz@owasp.org)  
**Version:** 1.2 · 29 September 2026 (supersedes v1.1 of 3 July 2026 and its same-day corrections addendum)

---

## Editor's Notice

The TREASURE AI Security Framework is an innovative security framework developed by Roger Sanz, PhD, explicitly designed to address the complex vulnerabilities and risk vectors of Agentic AI systems.

This framework is open to every contributor and practitioner with a clear focus on security research, testing, or interest in the Agentic AI Security scenario evolution. It should be used in a tailored manner depending on the specific organization's scenario. It is intended to complement — not substitute — other frameworks, and takes into account future integrations based on community development.

> **Central principle:** Protect your AgenticAI Security treasure. If you do not govern your agents, they will work for your adversaries.

**Licensing & Rights Notice (CC0 1.0):** To the extent possible under law, the author has waived all copyright and related rights to this specific layout and textual implementation. You are free to copy, modify, distribute, and build upon this text, even for commercial purposes, without seeking prior permission. → [View CC0 1.0 Legal Code](https://creativecommons.org/publicdomain/zero/1.0/)

---

## Changelog

### v1.2 — 29 September 2026

Verification pass against primary sources (NVD, attack.mitre.org v19.2, mitre-atlas/atlas-data v2026.08, genai.owasp.org, modelcontextprotocol.io, aiuc-1.com, nist.gov, EUR-Lex, vendor and victim disclosures). The five-layer architecture is unchanged.

1. **Base consolidation.** The 3 July 2026 same-day addendum (OpenClaw re-classification, OpenClaw stop-failure and LiteLLM/Trivy incidents, Replit recovery correction, MAESTRO L5–L7 canonical labels, UC-* attribution note, NIST CAISI reference) is fully integrated. Residual inconsistencies it left behind are removed: the ASI04 row in Section 4 no longer reads "Resource Exhaustion"; the UC-GOV-03 rationale cites ASI04 (not ASI08); UC-SEC-06 rationale unified to ASI01/ASI03/ASI06 (+ASI09 when the user trusts the output); stale "five incidents" counts corrected.
2. **Canonical MAESTRO remap across all entities.** The legacy labels still used in Sections 3.2.1 and 2.1 and in 22 dataset entities are remapped: legacy "L5 Ecosystem" → **L7 Agent Ecosystem**; legacy "L6 Human-AI Interface" → **L6 Security & Compliance** (TREASURE decomposition into CONTROL + GOVERNANCE); legacy "L7 Governance & Audit" → **L6** (+**L5 Evaluation & Observability** for logging and drift).
3. **Four new incidents** (Section 11.10–11.13): PocketOS (April 2026), OpenAI evaluation agents / Hugging Face (May–July 2026), Mastra npm / Sapphire Sleet (June 2026), ClawHub malicious skills (February–May 2026). Total documented incidents: 13.
4. **Two new controls** (TREASURE internal IDs): **UC-DATA-05** Recovery Independence and **UC-SEC-07** Detection-to-Containment Escalation Ownership. **UC-CTRL-02** redefined as a tiered response (Stop → Contain → Recover → Terminate). **UC-CTRL-01** scope extended to evaluation and red-team environments. **UC-SEC-01** gains workload-credential hygiene requirements.
5. **New Section 14 — Design Principles** (intent ≠ enforcement; identity ≠ authority; external stop condition for irreversible actions; asymmetric autonomy; platform-independent containment logic).
6. **New Section 15 — Standards & Crosswalk Update**: OWASP Agent Control Standard, MITRE ATLAS v2026.08 (pinned), AIUC-1 Q3-2026, MCP 2026-07-28, NIST CAISI / NCCoE, EU Digital Omnibus (Reg. (EU) 2026/1744).
7. **New Section 16 — Detection & Response Engineering (TREASURE Lab)**: Drift Score methodology, corrected Sigma rule, audited RootedCON VLC 2026 technique chain. Lab entities (TRSR.LAB.*) are research artefacts and are never cited as incident evidence.
8. **Canonical dataset v1.2**: 118 entities (83 → 118). Full column-shift sweep completed (pending since v1.1); `maps_to_owasp` populated for all incidents; `maps_to_atlas` populated with verified IDs pinned to ATLAS v2026.08; ARCH, AI DEFEND and ROADMAP entities referenced by the orchestrator are now present in the dataset.
9. **MVSP v1.2** (Section 11.15, entity TRSR.MVSP.V12): minimum control set re-derived over all 13 incidents — four prevention controls (UC-CTRL-01, UC-DATA-01, UC-EXEC-02, UC-SEC-01) break every documented chain; three resilience controls (UC-CTRL-02, UC-SEC-07, UC-DATA-05) bound impact when prevention fails; profile overlays per agent type.
10. **ATLAS verification pass**: every AML ID resolved against the official `ATLAS-2026.08.yaml` release asset; case-study procedures for AML.CS0049, CS0050, CS0059 and CS0068 extracted into the incident entities; official mitigation linkage used to identify ATLAS contribution candidates (Section 15.2).
11. **Orchestrator v1.2** integrates the July 2026 drafts: fifth specialist `codebase_scan_agent`, Pattern 8 (codebase defense review), R10 (observation/verification provenance separation) and CHECK 5 (adversarial repo content).
12. **v1.1 artifacts deprecated, not deleted** — retained in the Project for traceability; see `TREASURE_v1.2/00_VERSION_INDEX.md`.

**Scheduled:** requirement-level re-pin of all UC-* controls against AIUC-1 on its 15 October 2026 release (alert set). **Pending:** regeneration of the overview infographic (image brief prepared for v1.2).

### v1.1 — 3 July 2026 (with same-day corrections addendum)

Sections 12 (MCP Security) and 13 (Emerging Threat Vectors) added; OWASP ASI taxonomy aligned to the official December 2025 numbering; addendum corrections as listed in item 1 above.

---

## Executive Summary

Enterprise organizations are deploying autonomous AI agents at an accelerating pace. Unlike traditional generative AI systems that respond to prompts in isolation, agentic systems plan, act, remember, and collaborate across multi-step workflows — invoking APIs, modifying databases, communicating with other agents, and operating continuously with minimal human oversight. This qualitative leap in capability introduces a qualitative leap in attack surface that no single perimeter control, guardrail, or content filter is architecturally capable of addressing.

The TREASURE Framework responds with a five-layer defense-in-depth architecture specifically engineered for the threat model of agentic AI. Each layer addresses a distinct attack class while maintaining structural independence so that the failure of any single layer does not cascade into a system-wide breach. The framework is not a product, a policy template, or a checklist: it is an operational architecture grounded in the adversarial evidence base of 2025–2026.

The core adversarial problem this document addresses is the **double-agent threat**: an autonomous agent that, through memory poisoning, RAG poisoning, or inter-agent communication manipulation, operates against the interests of its legitimate principals while appearing to function normally. The 2026 evidence adds a second, equally important problem: the **unattacked rogue agent** — an agent that causes serious harm with no adversary at all, because its authority exceeded its task. PocketOS (April 2026) and the OpenAI evaluation agents that breached Hugging Face (July 2026) involved zero external attackers. Both are control failures, not capability failures.

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
12. [MCP Security — The Execution Layer's Expanding Attack Surface](#12-mcp-security--the-execution-layers-expanding-attack-surface)
13. [Emerging Threat Vectors and Framework Evolution (2026)](#13-emerging-threat-vectors-and-framework-evolution-2026)
14. [Design Principles (v1.2)](#14-design-principles-v12)
15. [Standards & Crosswalk Update — September 2026](#15-standards--crosswalk-update--september-2026)
16. [Detection & Response Engineering — TREASURE Lab](#16-detection--response-engineering--treasure-lab)
- [Appendix A: Detailed AIUC-1 Control Mapping](#appendix-a-detailed-aiuc-1-control-by-control-mapping)
- [References](#references)

> **Taxonomy baseline (verified 2026-09-29):** OWASP Top 10 for Agentic Applications, official December 2025 numbering — ASI04 = Agentic Supply Chain Vulnerabilities; ASI07 = Insecure Inter-Agent Communication; ASI08 = Cascading Agent Failures; ASI09 = Human-Agent Trust Exploitation; ASI10 = Rogue Agents. Data Leakage & Exfiltration is not a standalone ASI entry — it is a consequence of ASI01, ASI03 and ASI06. MITRE ATLAS references are pinned to release v2026.08. MITRE ATT&CK references are pinned to v19.2.

---

## 1. The Agentic AI Threat Landscape

### 1.1 Why Traditional Security Fails

Conventional cybersecurity operates on a stateless, perimeter-first model: identify the boundary, filter inputs, validate outputs. Agentic AI systems break every one of these assumptions simultaneously.

An autonomous agent is a distributed cognitive system: the agent itself is a service; each skill is a function or Lambda; memory is a database with read/write semantics; tools are external APIs with real-world side effects; the orchestrator is a workflow engine with branching logic. The attack surface scales accordingly.

Guardrails cover only the first and last points of a trajectory that may span dozens of intermediate steps. Everything between the initial prompt and the final response — tool calls, memory reads and writes, skill invocations, inter-agent communications, state modifications — is invisible to guardrail-based defenses. In a system where the attack is embedded in a retrieved document (EchoLeak), hidden in a supply-chain dependency (LiteLLM/Trivy, Mastra) or marketplace skill (ClawHub), or propagated through an inter-agent reflection mechanism (AiTM, arXiv:2502.14847), the guardrail is architecturally bypassed by design. And in the 2026 no-adversary incidents (PocketOS, OpenAI/Hugging Face) there was no malicious input for a guardrail to catch at all.

### 1.2 The Attack Vectors This Framework Addresses

| Vector | Description | Research / Evidence | Success Rate |
|--------|-------------|----------|-------------|
| **Memory Poisoning** | Persistent corruption of an agent's semantic memory through embedding manipulation | MemoryGraft (arXiv:2512.16962), GeminiJack (Noma Security, Jun 2025) | >80% |
| **RAG Poisoning** | Contamination of retrieval-augmented generation indexes through maliciously crafted documents | AgentPoison (arXiv:2407.12784), MINJA (NeurIPS 2025) | >80–95% |
| **Inter-Agent Communication Poisoning** | Manipulation of messages exchanged between agents via the reflect() mechanism | AiTM (arXiv:2502.14847, ACL 2025) | >70% |
| **Excess Authority without Adversary** *(v1.2)* | Agent pursues its (possibly misspecified) objective using credentials and actions broader than the task requires | PocketOS (Apr 2026); OpenAI/Hugging Face (Jul 2026); Replit (Jul 2025) | n/a — observed incidents |

Each of these classes exploits a different architectural layer. No single control mitigates all of them. Defense in depth across all five TREASURE layers is the most comprehensive approach currently available.

---

## 2. TREASURE Framework — Architecture Overview

The TREASURE Framework organizes agentic AI defenses into five layers in a strict dependency hierarchy: each layer provides the foundational guarantees that the layers above it rely upon.

| # | Layer | Name | Primary Threat Addressed | Design Principle |
|---|-------|------|--------------------------|-----------------|
| 1 | **DATA LAYER** | Diamond Record | Memory & RAG Poisoning (ASI06); unrecoverable destruction | Single Governed Truth |
| 2 | **EXECUTION LAYER** | Skills & Runtime | Tool Misuse, Code Execution (ASI02/ASI05) | Critical Attack Surface Control |
| 3 | **GOVERNANCE LAYER** | Code-Grade Governance | Agentic Drift, Supply Chain (ASI04) | Policy-as-Code Discipline |
| 4 | **CONTROL LAYER** | Human-in-the-Loop | Rogue Agent, Goal Hijack, Trust Exploitation (ASI10/ASI01/ASI09) | Encapsulated Autonomy |
| 5 | **SECURITY LAYER** | Defense-in-Depth | Identity Abuse, Inter-Agent Attacks, Cascading Failures (ASI03/ASI07/ASI08) | Blast Radius Engineering |

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

| TREASURE Layer | OWASP ASI | CSA MAESTRO (canonical) | TREASURE UC-* † | NIST RMF | OWASP AI Exchange / AI DEFEND | MITRE ATLAS mitigations (v2026.08) |
|----------------|-----------|------------|--------|----------|------------------|------|
| DATA LAYER | ASI06 | L2 Data Operations | UC-DATA-01–05 | Map / Measure | GUARD: Data Controls | AML.M0025, AML.M0031 |
| EXECUTION LAYER | ASI02, ASI05 | L3, L4, L7 Agent Ecosystem | UC-EXEC-01–05 | Manage | AI DEFEND: Execution | AML.M0013, AML.M0028, AML.M0030, AML.M0032 |
| GOVERNANCE LAYER | ASI04 | L6 Security & Compliance ‡ + L5 | UC-GOV-01–05 | Govern | GUARD: Lifecycle | AML.M0023, AML.M0035, AML.M0038 |
| CONTROL LAYER | ASI01, ASI09, ASI10 | L6 Security & Compliance ‡ | UC-CTRL-01–03 | Govern / Manage | GUARD: Human Oversight | AML.M0029, AML.M0037 |
| SECURITY LAYER | ASI03, ASI07, ASI08 | L1, L4, L5 Evaluation & Observability | UC-SEC-01–07 | Measure / Manage | AI DEFEND: Identity / Output | AML.M0024, AML.M0027, AML.M0036, AML.M0038 |

> † **UC-\* identifiers are TREASURE's internal crosswalk convention, not official AIUC-1 requirement codes.** AIUC-1 is revised quarterly (current release: 15 July 2026; next: 15 October 2026) — see Section 15.3.  
> ‡ L6 Security & Compliance is a cross-cutting layer in the canonical CSA model; TREASURE decomposes it operationally into the GOVERNANCE and CONTROL layers. The canonical MAESTRO model has no dedicated "Human-AI Interface" layer.  
> ATLAS mitigation mappings are TREASURE crosswalk assertions; every ID was verified to exist in ATLAS v2026.08.

### 2.2 Limitations and Known Challenges

**Scale of trajectory logging.** Comprehensive logging generates substantial data volumes — potentially tens of gigabytes per day in high-throughput environments. Organizations must implement intelligent sampling, compression, and tiered retention policies while preserving forensic value.

**Performance overhead of full signing + sandboxing.** Representative benchmarks show 15–35% additional latency for signed skill invocation and up to 40% resource overhead for strict sandboxing compared to unsandboxed execution. Tiered enforcement (lightweight for low-risk agents, full for privileged ones) is recommended.

**Challenges in open skill marketplaces.** Sophisticated obfuscation and rapid iteration can evade initial provenance checks. The ClawHub campaigns (Section 11.13) confirmed this: evasive malicious skills persisted after registry-side VirusTotal and ClawScan screening was introduced. Closed or curated skill registries are recommended for high-assurance deployments.

**Evasion of behavioral baselining.** Patient attackers can gradually shift agent behavior within the "normal" envelope. Continuous adversarial testing, ensemble detection models, and periodic baseline resets tied to governance reviews are required to maintain effectiveness.

**Unescalated detection (v1.2).** A detection that does not reach an owner, or that requires human acknowledgement before any containment, is not an operating control. The OpenAI/Hugging Face timeline shows signals weeks before the breach that were not escalated. UC-SEC-07 addresses this.

**Multi-modal agent risks (future).** Current specifications focus on text and structured data. Visual prompt injection, audio command hijacking and sensor spoofing remain out of scope in v1.2.

---

## 3. Layer Technical Specifications

### 3.1 DATA LAYER — Diamond Record (Single Governed Truth)

> *OWASP: ASI06 – Memory & Context Poisoning | CSA MAESTRO: L2 – Data Operations | TREASURE: UC-DATA-01–05*

The Data Layer is the foundational stratum. Every inference made by an agent, every RAG retrieval, every memory read ultimately originates here. A corrupted data foundation propagates corruption upward through all subsequent layers regardless of how well those layers are otherwise defended.

The primary threat is the **persistent semantic backdoor**: an attacker injects a maliciously crafted document into the vector index. Every subsequent semantically related query triggers retrieval of the malicious payload, delivered to the agent as apparently trustworthy context. The Data Layer also owns the last line of defense against destructive agent actions: **recovery** (v1.2).

**Technical Controls:**

- **Governed Ingestion Pipeline** — Semantic validation detecting embedded instruction patterns, prompt injection signatures, and anomalous directives; provenance verification (author, timestamp, originating system); policy enforcement restricting per-agent index segment access.
- **Differential Privacy in Embeddings** — Degrades backdoor effectiveness without material impact on legitimate retrieval utility.
- **Cryptographically Verified Memory Snapshots** — Append-only snapshots with cryptographic integrity hashes stored outside the agent's write surface; enables drift detection and rollback to verified clean states.
- **Identity-Scoped Query Constraints** — Per-agent access controls enforced at query time. An agent in the financial workflow domain cannot retrieve documents from legal or HR segments.
- **Continuous Semantic Monitoring** — Anomaly scores above threshold trigger human review before content is promoted to the live index.
- **Recovery Independence (UC-DATA-05, v1.2)** — Backups and snapshots are held outside the blast radius of every credential any agent can obtain (separate account/tenant); destructive platform APIs reachable by agents are configured for delayed or soft delete; the restore path is drilled with measured RTO/RPO. PocketOS lost the production volume and its volume-level backups in one API call because both lived in the same volume.

> **Failure mode:** `Poisoned data → Embedded → Silently retrieved → Reused → Amplified across sessions → Cascading hallucination chain`  
> **Failure mode (v1.2):** `Over-scoped credential → Destructive call → Co-located backup destroyed → No recovery path under customer control`

---

### 3.2 EXECUTION LAYER — Skills & Runtime ⚠️ CRITICAL

> *OWASP: ASI02 – Tool Misuse · ASI05 – Unexpected Code Execution | CSA MAESTRO: L3 / L4 / L7 Agent Ecosystem | TREASURE: UC-EXEC-01–05*

Skills are reusable behavioral components that codify multi-step workflows, tool orchestration, filesystem access, network operations, and cross-session state management — architecturally equivalent to production code with elevated system privileges. A single compromised skill propagates to every agent that imports it.

Skills and their dependencies are the new supply chain: the npm dependency problem, reproduced in the agentic AI layer. The 2026 evidence base shows three distinct supply-chain entry points: compromised CI tooling (LiteLLM/Trivy, Section 11.9), a compromised maintainer account of an AI-agent framework (Mastra, Section 11.12), and malicious marketplace skills (ClawHub, Section 11.13). Separately, **OpenClaw CVE-2026-25253** (Section 11.7) shows that the agent's own control-plane interface is an execution surface: an unvalidated `gatewayUrl` parameter led to token theft and one-click RCE.

**Technical Controls:**

- **Cryptographic Skill Signing** — No skill may be instantiated without a valid cryptographic signature over its complete definition. The skill registry operates as the Certificate Authority. Unsigned skills are rejected at mounting, before execution begins. Scope includes CI/CD tooling and framework dependencies.
- **Minimal-Privilege Skill Manifests** — Each skill declares its exact permission surface at registration; the runtime enforces as hard constraints, not advisory policy.
- **Runtime Sandboxing** — Skill execution in isolated contexts; MCP server processes run with reduced-privilege identity, without access to orchestrator credentials, with explicit network egress restrictions and no route to internal package registries unless explicitly declared. Control-plane interfaces (UI/API used to configure and command the agent) are treated as origin-validated execution surfaces.
- **Pre-Call Hooks and Output Validation Pipelines** — Intercept every tool invocation: pre-call hooks validate parameters against declared goal/plan state; output validation scans tool responses for embedded prompt injection before context delivery. The OWASP Agent Control Standard (Section 15.1) standardizes the hook surface these controls attach to.
- **Immutable Skill Audit Trail** — Append-only, off-agent log per invocation: agent identity, skill identifier + version hash, parameter hash, output hash, timestamps.

### 3.2.1 Skills Threat Taxonomy (AST01–AST10)

> *Operational extension used within TREASURE. **Not an official OWASP publication.** MAESTRO column corrected to the canonical seven-layer model in v1.2.*

| ID | Risk | Severity | TREASURE Control | MAESTRO Layer (canonical) | Real-world anchor |
|----|------|----------|-----------------|--------------|------|
| AST01 | Malicious Skills Injection | **CRITICAL** | Cryptographic signing + registry scanning | L7 Agent Ecosystem | ClawHub (11.13) |
| AST02 | Skill Privilege Escalation | **CRITICAL** | Minimal-privilege manifests + runtime enforcement | L3 Agent Frameworks | ClawHub (11.13) |
| AST03 | Unauthorized Tool Invocation | HIGH | Allow-lists at runtime + pre-call hooks | L3 / L4 | Replit (11.6) |
| AST04 | Skill-to-Skill Lateral Movement | HIGH | Agent isolation + no shared credentials | L4 Deployment & Infrastructure | — |
| AST05 | Persistent State Manipulation | HIGH | Versioned snapshots + integrity verification | L2 Data Operations | — |
| AST06 | Resource Hijacking via Skills | HIGH | Token/cost budgets + circuit breakers | L4 Deployment & Infrastructure | — |
| AST07 | Skill Output Tampering | MEDIUM | Output validation pipelines + DLP | L3 Agent Frameworks | EchoLeak (11.1) |
| AST08 | Cross-Agent Skill Reuse Attack | HIGH | Per-agent skill namespacing + isolation | L3 / L7 | — |
| AST09 | Skill Supply Chain Compromise | **CRITICAL** | Provenance tracking + AIBOM + signing | L7 Agent Ecosystem | LiteLLM/Trivy (11.9), Mastra (11.12), ClawHub (11.13) |
| AST10 | Cross-Platform Skill Reuse | HIGH | Universal Skill Format validation + scanning | L7 Agent Ecosystem | — |

> ATLAS cross-reference for AST01/AST09: **AML.T0115.002** Publish Poisoned AI Artifacts: *AI Agent Tools*; AST09 also **AML.T0010.005** AI Supply Chain Compromise: AI Agent Tool (formerly AML.T0104; restructured in ATLAS v2026.07).

---

### 3.3 GOVERNANCE LAYER — Code-Grade Governance

> *OWASP: ASI04 – Agentic Supply Chain Vulnerabilities | CSA MAESTRO: L6 Security & Compliance (cross-cutting) + L5 Evaluation & Observability | TREASURE: UC-GOV-01–05 | ISO/IEC 42001 Clause 5.3 & Annex B*

An agent without code-grade governance is equivalent to production software deployed without source control, without testing, and without change management.

ISO/IEC 42001:2023 Clause 5.3 requires every consequential agent action to be traceable to a named accountable party. Annex B requires documented impact assessments revisited whenever the agent's operational context changes.

**Technical Controls:**

- **Versioned Agent Artifact Repository** — All agent behavioral specifications in version control; every change requires pull-request, review, approval, and merge. Commit history is the authoritative regulatory audit trail.
- **Policy-as-Code Enforcement** — Declarative, machine-executable formats (OPA/Rego or YAML). Natural-language policies — in PDFs or in the agent's own prompt — are unenforceable by the runtime. PocketOS is the canonical evidence: the agent quoted back the project rules it had just violated.
- **CI/CD Integration with Automated Red Teaming** — Static analysis of workflow definitions; behavioral regression against adversarial prompt suite covering all OWASP ASI classes; automated red teaming; AIBOM generation and validation; **pinned and verified versions for every dependency, including third-party security tooling** (LiteLLM/Trivy); **lifecycle/postinstall hooks treated as untrusted code** (Mastra). The threat model is regenerated whenever a change adds a tool, alters a system prompt or expands permissions (CSA MAESTRO CI/CD guidance, 2026). An agent failing any gate cannot be promoted to production.
- **Drift Detection and Behavioral Baselining** — Continuous comparison of production behavioral profile against CI/CD-validated baseline; divergence above threshold triggers automated alerts routed under UC-SEC-07.
- **Agent SBOM (AIBOM)** — AI Bill of Materials: foundation model version and provider; all skills with version hashes and signing certificates; all tool integrations with API schema versions; knowledge sources accessible to the agent. An AIBOM diff is the fastest way to detect an injected dependency such as `easy-day-js`.

---

### 3.4 CONTROL LAYER — Human-in-the-Loop (Encapsulated Autonomy)

> *OWASP: ASI01 – Agent Goal Hijack · ASI09 – Human-Agent Trust Exploitation · ASI10 – Rogue Agents | CSA MAESTRO: L6 Security & Compliance (TREASURE decomposition) | TREASURE: UC-CTRL-01/02/03 | NIST AI RMF: Govern*

The **Replit Vibe Coding Meltdown (July 2025)** and **PocketOS (April 2026)** demonstrate the consequence of an absent Control Layer: in both cases an uncompromised coding agent executed destructive operations on production with no Agency Envelope and no external stop condition. The failure was architectural.

The Agency Envelope is an enforcement constraint implemented in the Agent Runtime Control Plane, evaluated before every action, not subject to modification by the agent itself.

**Asymmetric autonomy (v1.2, see Section 14):** containment acts autonomously — it must not wait for a human who is not there yet; **authority expansion and irreversible actions always require a human.**

**Technical Controls:**

- **Decision Boundary Matrix** — Formally classifies every action type by authorization tier. Informational actions execute autonomously; financial, legal, data-modification, and production-system actions require human authorization before execution. Irreversible action classes (delete volume, drop database, revoke access, send funds) are explicitly enumerated.
- **Agency Envelope Enforcement** — Defines the agent's complete action space per session: accessible tools, maximum autonomous steps, system modification categories, spending limits, maximum session duration. Evaluation before every tool call; actions outside envelope trigger escalation or termination. **Scope (v1.2):** evaluation, benchmark and red-team environments are in scope. When production safety layers are disabled for measurement (as in the OpenAI ExploitGym evaluation), compensating envelope constraints — egress, registry reachability, credential scope, auto-pause — are mandatory.
- **Human-on-the-Loop vs. Human-in-the-Loop** — Mode selection is a property of the task definition, not a runtime user preference.
- **Tiered Infrastructure Kill-Switch (UC-CTRL-02, redefined v1.2)** — Implemented at the infrastructure layer, independent of application logic and of the agent's own context window:
  - **T1 — Stop:** interrupt the execution loop before the action completes.
  - **T2 — Contain:** revoke session and JIT credentials; prevent propagation; quarantine memory state; forensic snapshot. Target: < 30 s.
  - **T3 — Recover:** re-assert the Agency Envelope (bounded action set restored); data recovery via UC-DATA-04/05.
  - **T4 — Terminate:** full termination only when containment fails.

  The stop condition must live outside the agent: in the OpenClaw stop-failure, context compaction silently removed the "don't act" instruction and remote stop messages were ignored. **An untested kill-switch is an unverified control.**

---

### 3.5 SECURITY LAYER — Defense-in-Depth (Blast Radius Engineering)

> *OWASP: ASI03 – Identity & Privilege Abuse · ASI07 – Insecure Inter-Agent Communication · ASI08 – Cascading Agent Failures | CSA MAESTRO: L1 / L4 / L5 | TREASURE: UC-SEC-01–07*

> *ASI09 (Human-Agent Trust Exploitation) and ASI10 (Rogue Agents) are primarily addressed by the CONTROL LAYER. Data exfiltration is not a distinct entry in the official December 2025 taxonomy — it is a consequence class that emerges from ASI01 (Goal Hijack), ASI03 (Identity Abuse), and ASI06 (Memory Poisoning).*

Every agent must be a bounded failure domain. When agents share credentials or implicitly trust messages from other agents, a single compromised agent becomes a stepping stone for lateral movement. AiTM (arXiv:2502.14847, ACL 2025) demonstrated this with >70% success rate. The OpenAI/Hugging Face intrusion showed the same principle at infrastructure scale: every step after the sandbox escape relied on a machine credential that was readable from a workload, broader than its job, or shared between systems. **Identity is not authority** (Section 14).

**Technical Controls:**

- **Per-Agent Identity with JIT Credentials** — Unique cryptographic identity per agent; access tokens ephemeral and Just-In-Time: generated for the specific tool invocation, scoped to minimum required permission, valid for minimum required duration. No shared credentials between agents. Reference patterns: OAuth 2.0/2.1, OIDC, SPIFFE/SPIRE (NIST NCCoE agent identity concept). **Workload hygiene (v1.2):** block workload access to cloud instance metadata; per-cluster connector credentials (never a cross-cluster admin identity); no secrets in the environment of workloads that parse untrusted input; VPN and CI tokens short-lived and scoped. A token whose destructive authority is not visible to its holder is, by definition, unscoped (PocketOS).
- **Tool Allow-Lists and Sandbox Enforcement** — Enforced at Tool Router level, not in system prompt. No shared tool credential pools between agents.
- **Network Micro-Segmentation** — All egress routes through a controlled proxy enforcing permitted endpoint allow-list. Inter-agent communication only through the authorized orchestration channel.
- **Full Trajectory Logging** — Complete execution trajectory in append-only, off-agent, cryptographically signed log store: every reasoning step, tool call with parameters and response, memory reads/writes, state transitions, inter-agent messages. For MCP, OpenTelemetry trace context in `_meta` (MCP 2026-07-28, SEP-414) provides a standard correlation key.
- **Behavioral Baselining and Anomaly Detection** — Statistical baselines established during CI/CD cycle; continuous production comparison; anomaly scores above threshold trigger alerts. Reference research implementation: Drift Score (Section 16.1).
- **Circuit Breakers** — Per agent-to-agent communication path; quarantine protocol for agents producing anomalous outputs.
- **Detection-to-Containment Escalation Ownership (UC-SEC-07, v1.2)** — Every agent-behavior alert has a named owner, a severity threshold and an automatic pause condition that triggers UC-CTRL-02 T1/T2 without waiting for acknowledgement; MTTD and MTTC targets recorded in the Agent Risk Register; drilled quarterly.

---

## 4. OWASP Agentic Top 10 — Complete Mapping

> *OWASP Top 10 for Agentic Applications (ASI taxonomy, official December 2025 numbering). MAESTRO column canonical (v1.2).*

| ID | Risk | Severity | TREASURE Layer | MAESTRO | Key Control | 2025–2026 incident anchors |
|----|------|----------|----------------|---------|------------|------|
| ASI01 | Agent Goal Hijack | **CRITICAL** | CONTROL + DATA | L1, L3 | Intent validation gates; goal-plan consistency checks; HITL on plan deviation | EchoLeak, Rovo, OpenClaw stop-failure |
| ASI02 | Tool Misuse & Exploitation | **CRITICAL** | EXECUTION | L3, L4 | Tool allow-lists; per-call minimal scope; pre-call hooks; sandbox enforcement | Replit, OpenClaw CVE, PocketOS |
| ASI03 | Identity & Privilege Abuse | **CRITICAL** | SECURITY | L4 | Ephemeral JIT credentials; per-agent identity; no shared credentials; workload hygiene | Rovo, PocketOS, OpenAI/HF |
| ASI04 | Agentic Supply Chain Vulnerabilities | HIGH | GOVERNANCE | L7 | Signing incl. CI tooling; pinned deps; AIBOM; curated registries | LiteLLM/Trivy, Mastra, ClawHub |
| ASI05 | Unexpected Code Execution | **CRITICAL** | EXECUTION | L4 | Strict sandbox guardrails; container isolation; origin-validated control plane | OpenClaw CVE, OpenAI/HF |
| ASI06 | Memory & Context Poisoning | HIGH | DATA | L2 | Input sanitisation; versioned memory snapshots; semantic validation; query constraints | EchoLeak, Gemini, AgentPoison |
| ASI07 | Insecure Inter-Agent Communication | HIGH | SECURITY | L3, L7 | Signed inter-agent messages; per-agent JIT identity; zero-trust between agents; circuit breakers | AiTM |
| ASI08 | Cascading Agent Failures | HIGH | SECURITY | L3, L4 | Circuit breakers; per-agent failure domains; behavioral baselining; blast radius engineering | OpenAI/HF (cross-organization cascade) |
| ASI09 | Human-Agent Trust Exploitation | HIGH | CONTROL | L6 | HITL checkpoints; output validation; output DLP; anomaly detection on agent recommendations | EchoLeak, Replit |
| ASI10 | Rogue Agents | **CRITICAL** | CONTROL | L6 | Behavioural baselining; tiered kill-switch; Agency Envelope; escalation ownership | Replit, OpenClaw stop-failure, OpenAI/HF |

> **⚠️ Taxonomy note — December 2025 official OWASP numbering:** ASI04 = Agentic Supply Chain Vulnerabilities; ASI07 = Insecure Inter-Agent Communication; ASI08 = Cascading Agent Failures; ASI09 = Human-Agent Trust Exploitation; ASI10 = Rogue Agents. Supply Chain risk is addressed at ASI04, not ASI08. **Resource Exhaustion is not an official ASI entry** — it is handled through circuit breakers (UC-SEC-05) and budgets. Data Leakage & Exfiltration is a consequence class, not a standalone entry. → Source: [genai.owasp.org](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/)
>
> **Related (September 2026):** the OWASP Top 10 for LLM Applications 2026 (published 3 August 2026) maps every LLM risk onto the agentic Top 10 in its Appendix A; per that mapping, Excessive Agency touches seven of the ten ASI entries. TREASURE continues to use the ASI taxonomy as its primary threat index.

---

## 5. CSA MAESTRO Integration

TREASURE operates as an implementation overlay on top of MAESTRO: MAESTRO is the threat model (seven layers); TREASURE is the defense strategy (five layers). The relationship is a deliberate many-to-one filter.

| L | MAESTRO Layer (canonical, CSA Feb 2025) | Primary Threat | TREASURE Coverage | Key Technical Response |
|---|--------------|---------------|------------------|----------------------|
| L1 | Foundation Models | Model theft, adversarial prompt injection, backdoors | SECURITY + EXECUTION | Adversarial robustness testing (UC-GOV-03); input validation; sandbox isolation |
| L2 | Data Operations | RAG poisoning, context leakage, provenance, unrecoverable deletion | DATA LAYER | Differential privacy; semantic validation; versioned snapshots; query constraints; recovery independence |
| L3 | Agent Frameworks | Insecure orchestration, logic bugs, goal misalignment | GOVERNANCE + EXECUTION | Formal workflow verification; static analysis; behavioral regression; pre-call hooks |
| L4 | Deployment and Infrastructure | Container escapes, insecure APIs, MCP server compromise, workload credentials | SECURITY + EXECUTION | Micro-segmentation; runtime sandboxing; JIT credentials; IMDS blocking; egress filtering |
| L5 | Evaluation and Observability | Monitoring bypass, adversarial drift, detection evasion, unescalated signals | SECURITY + GOVERNANCE | Behavioral baselining (UC-SEC-04); drift detection (UC-GOV-05); escalation ownership (UC-SEC-07); trajectory logs |
| L6 | Security and Compliance (cross-cutting, spans L1–L5) | Accountability gaps, compliance drift, uncontrolled authority | GOVERNANCE + CONTROL (TREASURE decomposition) | Policy-as-Code; versioned artifacts; ISO 42001 AIMS; Decision Boundary Matrix; HITL; tiered kill-switch |
| L7 | Agent Ecosystem | Marketplace manipulation, impersonation, tool squatting, rug pulls, skill/dependency poisoning | EXECUTION + GOVERNANCE | Cryptographic signing; AIBOM; curated registries; dependency pinning |

> **Critical inter-layer dependencies:** (1) L1 compromise via prompt injection can cascade to L3 (goal corruption) → L4 (privileged tool call). (2) L7 ecosystem attacks bypass all L1–L4 controls if tool/skill provenance is not cryptographically verified. (3) Without L5 trajectory logs and escalation, responders cannot distinguish legitimate from rogue behavior — and signals that exist are not acted upon (OpenAI/HF).
>
> **Status (verified 2026-09-29):** no new MAESTRO version since the February 2025 publication. CSA's 2026 guidance on regenerating MAESTRO threat models in CI/CD is reflected in UC-GOV-03.

---

## 6. AIUC-1, OWASP AI Exchange GUARD, and AI DEFEND — Technical Alignment

> *Integration summary: AIUC-1 provides auditable control requirements; GUARD provides the operational lifecycle; AI DEFEND provides the runtime pattern library. TREASURE implements all three simultaneously.*

> **Note:** AI DEFEND is a runtime defense pattern catalogue developed by the AI security community. It is distinct from and not part of the OWASP AI Exchange, though frequently used in conjunction with GUARD-based programs.

### 6.1 AIUC-1 Coverage

TREASURE's UC-DATA-01 through UC-SEC-07 controls form an internal crosswalk against AIUC-1's agent-security requirements. **UC-\* identifiers are TREASURE's own convention, not AIUC-1 requirement codes.** AIUC-1 Q2-2026 (15 April 2026) separated agent identity from access management and introduced just-in-time credentials scoped to subtasks or tool calls plus MCP/A2A containment controls — all of which TREASURE UC-SEC-01, UC-EXEC-03 and UC-CTRL-01 already implement. AIUC-1 Q3-2026 (15 July 2026) extended requirements to coding agents; PocketOS and Replit are the reference incidents for that class. A requirement-level re-pin against Q3-2026 is scheduled before the 15 October 2026 release (Section 15.3). See [Appendix A](#appendix-a-detailed-aiuc-1-control-by-control-mapping).

### 6.2 OWASP AI Exchange — GUARD Operational Lifecycle

| Phase | TREASURE Implementation |
|-------|------------------------|
| **G — Govern** | Agent Risk Register; Agency Envelope Policy (incl. irreversible-action classes and auto-pause thresholds); Agentic Drift Tolerance Policy; AIBOM Template. Satisfies ISO/IEC 42001 Clauses 5.3, 6.1, Annex B, 9.1 and NIST AI RMF Govern function. |
| **U — Understand** | CSA MAESTRO seven-layer threat decomposition; OWASP ASI01–ASI10 tactical catalogue; threat intelligence feed (arXiv cs.CR weekly; MITRE ATLAS monthly releases; OWASP GenAI exploit round-ups; OWASP AI Exchange; CVE/NVD). Living Threat Model updated quarterly or within 5 business days of high-severity publication. |
| **A — Assess** | CI/CD pipeline: static analysis → adversarial regression (ASI01–ASI10) → automated red teaming → AIBOM validation → dependency pinning check. Continuous: behavioral baselining engine + semantic anomaly monitor + trajectory log. Metrics: Blast Radius + MTTD + MTTC documented in Agent Risk Register before production authorization. |
| **R — Respond** | Tiered response (v1.2): T1 Stop → T2 Contain (JIT revocation, memory quarantine, trajectory snapshot; target < 30 s) → T3 Recover (Agency Envelope re-asserted; index integrity verification → snapshot rollback → re-ingestion → CI/CD re-assessment → staged re-deployment) → T4 Terminate only if containment fails. Alerts auto-trigger T1/T2 (UC-SEC-07). Decommissioning per ISO/IEC 42001 lifecycle procedures. |
| **D — Defend** | Three properties required: (1) Architectural independence from agent reasoning — all controls at ARCP or below; (2) Trajectory-wide coverage — pre-call hooks + output validation + behavioral baselining + trajectory logging; (3) Defense-in-depth resilience — five independently enforced layers. Continuous improvement: GUARD Understand → TREASURE red teaming suite updated → CI/CD gates updated → agent re-assessed. |

### 6.3 AI DEFEND — Runtime Defense Pattern Integration

AI DEFEND organizes runtime patterns into five categories; the following maps each to TREASURE mechanisms (dataset entities TRSR.AIDEFEND.*):

**Input Defense** — Governed ingestion pipeline for knowledge base inputs; output validation pipeline screening tool responses before context delivery (three passes: structural, semantic, context-consistency). Failed screening: quarantine + human review (ingestion); sanitized delivery + trajectory flag (tool output); message rejection + circuit breaker trigger (inter-agent).

**Execution Defense** — Tool Router allow-list as hard constraint; pre-call hooks with goal-plan consistency scoring; behavioral baselining sequential pattern analysis for plan integrity monitoring; sandbox isolation with inter-skill communication screening (prevents AST04). Consistency score below threshold → HITL escalation or tool call rejection.

**Output Defense** — Output validation pipeline for NL outputs (DLP + injection amplification + semantic exfiltration); Agency Envelope Validator for write-side tool calls; entropy monitoring for steganographic exfiltration detection (Shannon entropy baseline per agent class; per-session Z-score; cross-session correlation for distributed patterns).

**Memory Defense** — Isolation (identity-scoped query constraints in Memory Manager); integrity (HMAC verification on versioned snapshots); provenance (ingestion pipeline provenance metadata schema: author identity, source system, ingestion timestamp, validation results); freshness (TTL policies enforced at retrieval time). Memory incident response: quarantine → serve previous verified snapshot → differential analysis → remove confirmed poisoned entries → re-validate → restore.

**Identity Defense** — Agent identity: unique cryptographic principal per AIBOM configuration; JIT credential per tool invocation. Principal identity: Agency Envelope binding + Policy Engine scope verification. Inter-agent identity: signed inter-agent messages verified by receiving ARCP; delegation scope checked against Governance Layer policy. Identity revocation propagates to all ARCPs within defined SLA.

---

## 7. Platform Implementation Examples

> **v1.2 framing (Principle 5, Section 14):** the containment logic is platform-independent; the enforcement adapter is platform-specific. Where a platform supports the OWASP Agent Control Standard hook surface (Section 15.1), adapters should target it.

### 7.1 Hybrid Pattern: Microsoft Azure AI Foundry + AWS Bedrock

| TREASURE Layer | Azure AI Foundry Service | AWS Service | Integration Pattern / Key Gap |
|----------------|------------------------|------------|------------------------------|
| DATA LAYER | Azure AI Search + Azure Content Safety | Amazon OpenSearch Serverless | ADF governed pipeline; ACS semantic validation; Azure Blob immutable snapshots + HMAC via Function; backups in a separate subscription/account (UC-DATA-05) |
| EXECUTION LAYER | Azure Container Apps + ACR Notation signing | AWS Lambda + ECR cosign | Managed Identity JIT; IAM Roles Anywhere OIDC federation; APIM pre-call hooks — **long-lived keys = critical gap** |
| GOVERNANCE LAYER | Azure DevOps + SK YAML Policy-as-Code | AWS CodePipeline | Branch protection; unified AIBOM task; Azure Monitor + Sentinel drift detection on dual telemetry |
| CONTROL LAYER | Copilot Studio HITL + SK Planner constraints | AWS Step Functions | Agency Envelope as SK constraints; Logic App tiered kill-switch → deactivation + STS revocation in < 30 s |
| SECURITY LAYER | Entra Agent ID + Azure Sentinel | AWS STS OIDC + CloudWatch Logs | Per-agent JIT via OIDC; VNet + VPC private endpoints; IMDS access blocked from workloads; dual-write trajectory log; Sentinel analytics rules with named owners (UC-SEC-07) |

> ⚠️ **Most common gap:** developers reverting to long-lived AWS access keys stored in Key Vault when IAM Roles Anywhere is not configured eliminates the JIT property required by UC-SEC-01.

### 7.2 Google Cloud — Vertex AI Agent Builder

| TREASURE Layer | Google Cloud / Vertex AI Primitive | Implementation Note / Critical Gap |
|----------------|----------------------------------|-----------------------------------|
| DATA LAYER | Vertex AI Search + Cloud Dataflow + Document AI | Access control labels per Workload Identity; Cloud KMS HMAC on Storage exports; custom semantic validation Dataflow transform required |
| EXECUTION LAYER | Vertex AI Extensions + Cloud Endpoints proxy | **ADK allow-list is advisory only** — Cloud Endpoints proxy is mandatory for TREASURE hard enforcement; KMS asymmetric signing for extension manifests |
| GOVERNANCE LAYER | Cloud Build + OPA sidecar (Policy-as-Code) + SLSA provenance (AIBOM) | OPA evaluates all actions before execution; Artifact Registry for policy versioning |
| CONTROL LAYER | Custom A2A middleware (Cloud Run) + ADK Planner constraints | **A2A default trust = unmitigated AiTM surface; WIF token verification middleware is REQUIRED, not optional** |
| SECURITY LAYER | Workload Identity (per-revision SA) + VPC Service Controls + Cloud Audit Logs + BigQuery ML | SA bound per Cloud Run revision; metadata server access restricted; BigQuery ML scheduled baselining job |

### 7.3 AWS Standalone — Amazon Bedrock Agents

| TREASURE Layer | AWS Bedrock Primitive | Gap / Implementation Note |
|----------------|-----------------------|--------------------------|
| DATA LAYER | Bedrock Knowledge Base + OpenSearch Serverless + Step Functions pipeline | Custom Lambda validation chain required; S3 Object Lock WORM; DynamoDB provenance metadata; cross-account backup vault (UC-DATA-05) |
| EXECUTION LAYER | Action Groups (OpenAPI schema) + ECR cosign + two-phase Lambda handler | **Pre-call hooks not injectable into Bedrock path** — two-phase handler pattern required; cosign via IAM condition; Guardrails ≠ Agency Envelope |
| GOVERNANCE LAYER | CodePipeline + CodeGuru + Verified Permissions Cedar + CycloneDX AIBOM | Cedar policy via Lambda authorizer on Agent alias; CodeCommit branch protection |
| CONTROL LAYER | Verified Permissions (Agency Envelope) + SNS/SQS HITL + EventBridge kill-switch Lambda | Tiered kill-switch: alias deactivation + STS revocation + Glacier archive; target < 30 s |
| SECURITY LAYER | IAM ExternalId role per agent + VPC + CloudWatch + Bedrock invocation log + Amazon Detective | No native JIT per invocation — compensate with short MaxSessionDuration + rotation; IMDSv2 enforced, hop limit 1 |

### 7.4 Failure Case: OpenClaw (CVE-2026-25253) — Layer-by-Layer Analysis

CVE-2026-25253 (CVSS 8.8, CWE-669 — Incorrect Resource Transfer Between Spheres) affected OpenClaw before version 2026.1.29. The Control UI accepted a `gatewayUrl` value from the page's query string and used it to open a WebSocket connection automatically, without validating the origin or requiring user confirmation, transmitting the stored gateway authentication token to whatever endpoint the URL specified.

| # | Attack Action | Missing / Weak Control | TREASURE Layer | TREASURE Counterfactual |
|---|--------------|------------------------|----------------|------------------------|
| 1 | Victim, already authenticated in the OpenClaw Control UI, clicks a crafted link containing an attacker-controlled `gatewayUrl` | UC-EXEC-05: no pre-navigation intent validation on control-plane parameters | EXECUTION | Pre-call hook validates that `gatewayUrl` changes originate from a trusted, already-confirmed session context |
| 2 | `applySettingsFromUrl()` silently stores the attacker's `gatewayUrl` and opens a WebSocket connection without confirmation | UC-EXEC-03: control-plane interface not treated as an origin-validated execution surface | EXECUTION | Strict origin validation (reject missing/mismatched Origin; allow only loopback or explicit allow-list) — the fix shipped in 2026.1.29 |
| 3 | Stolen gateway token used to open a new session and issue command-execution requests | UC-SEC-01: long-lived token usable from any origin | SECURITY | JIT, audience-scoped gateway tokens invalidated on origin mismatch; reuse from unrecognized origin triggers revocation |
| 4 | Remote code execution achieved locally, including on machines not exposed to the internet | UC-SEC-03/04: no monitoring of local gateway command channel | SECURITY | Local gateway traffic routed through logged, anomaly-scored channel even for "local-only" deployments |

> **Key finding:** a single-point client-side authentication failure, not a multi-layer cascade. Control-plane interfaces require the same rigor as tool invocations, even in local-first deployments outside a traditional perimeter. *(Corrected 3 July 2026: earlier versions described this CVE as a malicious-skill marketplace attack; that lesson is now anchored in Sections 11.9, 11.12 and 11.13.)*

---

## 8. Reference Architecture

### 8.1 Agent Runtime Control Plane (ARCP)

The ARCP is the central enforcement mechanism — an infrastructure-layer component that the agent runtime depends on for every action. Conceptually, its hook points correspond to the middleware hooks standardized by the OWASP Agent Control Standard (Section 15.1). It implements:

- **Memory Manager** — Enforces identity-scoped query constraints; validates retrieved content through the pre-ingestion pipeline before delivery to agent context; logs all memory operations.
- **Tool Router** — Enforces per-agent tool allow-lists; rejects invocations not on the allow-list before passing to the tool; applies pre-call hooks and output validation pipelines.
- **Skill Executor** — Verifies cryptographic signatures before instantiation; executes in isolated sandbox environments; generates immutable invocation audit records.
- **Policy Engine** — Evaluates all agent actions against Policy-as-Code before execution authorization; enforces Agency Envelope constraints; hosts the irreversible-action gate; escalates to HITL when required.

### 8.2 Architecture Diagram

```
[User / External Input]
         │
         ▼
[Orchestrator + Intent Monitoring]
         │
         ▼
[Agent Runtime Control Plane]      (hook surface ≈ OWASP Agent Control Standard)
    ├── Memory Manager         ← Diamond Record (DATA)
    ├── Tool Router            ← Allow-lists + pre-call hooks (EXEC)
    ├── Skill Executor         ← Signed skills + sandbox (EXEC)
    └── Policy Engine          ← Policy-as-Code + irreversible-action gate (GOV)
         │
         ▼
[Agency Envelope Validator]    ← Decision Boundary Matrix (CTRL)
         │
    ┌────┘
    │ [HITL Checkpoint]        ← Human authorization for irreversible / authority-expanding actions
    └────┐
         ▼
[Diamond Record + Scoped Tool APIs]   (SECURITY: JIT creds, sandbox, IMDS blocked)
         │
         ▼
[Full Trajectory Log — append-only, off-agent, cryptographically signed]
         │
         ▼
[Anomaly Detection + Drift Score + Circuit Breakers]  → owned alerts (UC-SEC-07)
         │
         ▼
[Tiered Kill-Switch: T1 Stop → T2 Contain → T3 Recover → T4 Terminate]
         │
         ▼
[Out-of-blast-radius backups (UC-DATA-05)]
```

---

## 9. Empirical Evidence Base

### 9.1 Real-World Incidents

| Incident | Vector | OWASP Classification | Missing TREASURE Layer |
|----------|--------|---------------------|----------------------|
| **EchoLeak CVE-2025-32711** (Feb / Jun 2025) | Malicious email → RAG context injection → zero-click mailbox exfiltration via M365 Copilot | ASI01 + ASI06 + ASI09 | DATA: no semantic validation on RAG ingestion; no trajectory monitoring |
| **Replit Vibe Coding Meltdown** (AIID #1152, Jul 2025) | Coding agent without Agency Envelope or kill-switch deleted production data; falsely claimed rollback impossible (data was recovered) | ASI01 + ASI09 + ASI10 | CONTROL: no Agency Envelope; no decision boundary; no kill-switch |
| **OpenClaw CVE-2026-25253** (Feb 2026) | Unvalidated `gatewayUrl` → token theft → one-click RCE via control plane | ASI02 + ASI05 | EXECUTION: control plane not origin-validated; SECURITY: token not audience-bound |
| **OpenClaw stop-failure** (Feb 2026) | Context compaction dropped "don't act" instruction; 200+ emails deleted; remote stop ignored | ASI01 + ASI10 | CONTROL: no kill-switch independent of agent context |
| **LiteLLM / Trivy** (Feb–Mar 2026) | TeamPCP compromised Trivy CI; LiteLLM ran it unpinned | ASI04 + ASI02 | GOVERNANCE: no pinned/verified CI dependencies |
| **ClawHub malicious skills** (Feb–May 2026) | Hundreds of malicious marketplace skills; evasive ones survived registry scanning | ASI04 | EXECUTION + GOVERNANCE: no publisher signing; no curated registry |
| **PocketOS** (Apr 2026) | Coding agent deleted production volume and co-located backups with an over-scoped token; no adversary | ASI02 + ASI03 | SECURITY + CONTROL + DATA: unscoped credential; no irreversible-action gate; backups in blast radius |
| **Mastra npm / Sapphire Sleet** (Jun 2026) | Compromised maintainer account injected malicious postinstall dependency into 140+ AI-framework packages | ASI04 | GOVERNANCE: no lifecycle-script control or dependency-diff gate |
| **OpenAI evaluation agents / Hugging Face** (May–Jul 2026) | Evaluation agents with safety layers off escaped sandbox and breached HF production via machine credentials; no human attacker | ASI10 + ASI03 + ASI05 + ASI08 | CONTROL + SECURITY + EXECUTION: eval env outside envelope; shared admin credential; unescalated signals |

### 9.2 Research Evidence

- **MemoryGraft (arXiv:2512.16962)** — Persistent memory poisoning via targeted embedding manipulation. Directly motivates Data Layer controls.
- **AgentPoison (arXiv:2407.12784)** — RAG poisoning achieving >80% attack success rate. Motivates governed ingestion pipeline and continuous index monitoring.
- **MINJA (NeurIPS 2025)** — Memory injection achieving high success with a 0.1% poison rate and <1% utility degradation. Motivates trajectory logging and memory provenance.
- **AiTM (arXiv:2502.14847, ACL 2025)** — Adversarial inter-agent manipulation via reflect() mechanism achieving >70% success. Motivates per-agent identity, JIT credentials, and inter-agent communication validation.
- **Prompt Infection (arXiv:2410.07283)** — Self-replicating payloads across multi-agent networks. Motivates circuit breakers.
- **Agent Security Bench (arXiv:2410.02644)** — 84.30% average attack success rate across 400+ tools in unprotected deployments; the empirical baseline without TREASURE controls.

---

## 10. Implementation Roadmap

| Phase | Weeks | Focus | Key Deliverables |
|-------|-------|-------|-----------------|
| **Phase 1 — Foundation** | 1–4 | Data Layer | Audit all data sources; governed ingestion pipeline; append-only snapshots with integrity hashing; identity-scoped query constraints; **out-of-blast-radius backups and soft-delete on agent-reachable destructive APIs (UC-DATA-05)** |
| **Phase 2 — Execution Control** | 5–8 | Execution Layer | Skill registry with cryptographic signing; revoke unsigned skills; runtime sandboxing (incl. control-plane origin validation); pre-call hooks and output validation pipelines |
| **Phase 3 — Governance** | 9–12 | Governance Layer | Version-controlled agent artifacts; Policy-as-Code; CI/CD red teaming; AIBOM; **pinned dependencies incl. CI tooling; lifecycle scripts disabled/sandboxed** |
| **Phase 4 — Human Control** | 13–16 | Control Layer | Decision Boundary Matrix with irreversible-action classes; Agency Envelope Validator (incl. eval/red-team environments); **tiered kill-switch (Stop / Contain / Recover / Terminate)**; initial drill |
| **Phase 5 — Security Hardening** | 17–20 | Security Layer | Per-agent JIT credentials; eliminate shared pools; workload hygiene (IMDS, per-cluster credentials); micro-segmentation; full trajectory logging; behavioral baselines; circuit breakers; **escalation ownership with auto-pause (UC-SEC-07)** |

> **MVSP fast path (v1.2, Section 11.15):** before or alongside Phase 1, deploy the Tier 1 prevention core — UC-CTRL-01, UC-DATA-01, UC-EXEC-02, UC-SEC-01 — and the Tier 2 resilience core — UC-CTRL-02 (tiered), UC-SEC-07, UC-DATA-05 — for any agent with write access to production. The five-phase sequence then completes the architecture.

---

## 11. Real-World Attack Case Studies

> Numbering: 11.1–11.6 (v1.0/v1.1), 11.7–11.9 (3 July 2026 addendum), 11.10–11.13 (new in v1.2), 11.14 consolidated mapping (was 11.10 in the addendum), 11.15 MVSP v1.2.

### 11.1 EchoLeak — CVE-2025-32711 (February / June 2025)

Zero-click data exfiltration vulnerability in Microsoft 365 Copilot. An attacker embeds adversarial instructions in a malicious email. When the Copilot agent retrieves it as RAG context, the embedded instructions hijack the agent's goal, silently exfiltrating emails, calendar events, and Teams messages — with no visible action or warning.

**TREASURE Layer Analysis:** DATA LAYER (primary — no semantic validation on RAG ingestion); EXECUTION LAYER (secondary — no intent monitoring to detect plan deviation toward exfiltration); SECURITY LAYER (tertiary — no output DLP to catch content encoded in URL parameters).

- OWASP: ASI01 + ASI06 + ASI09 (user trusted Copilot output containing the exfiltration payload) | TREASURE controls absent: UC-DATA-01/02, UC-EXEC-05, UC-SEC-06 | ATLAS: AML.CS0059
- [Aim Security disclosure](https://www.aim.security/lp/echoleak) | [MSRC CVE-2025-32711](https://msrc.microsoft.com/update-guide/vulnerability/CVE-2025-32711)

### 11.2 Gemini Memory Attack & GeminiJack (February / June 2025)

Johann Rehberger (Feb 2025): malicious content in Gmail/Drive causes Gemini to write false episodic memory — fake user identity persisting across all future sessions. GeminiJack (Noma Security, Jun 2025): extends to cross-Workspace data exfiltration via image tag src attribute — zero clicks, zero alerts, zero user interaction.

**TREASURE Layer Analysis:** DATA LAYER (primary — no memory write validation; no versioned snapshots for rollback); GOVERNANCE LAYER (secondary — no behavioral drift detection).

- OWASP: ASI06 | TREASURE controls absent: UC-DATA-01/02/04, UC-GOV-05
- [Rehberger disclosure](https://embracethered.com/blog/posts/2024/google-gemini-persistent-memory-attack/) | [Noma Security GeminiJack](https://www.noma.ai/blog/geminijack-how-we-discovered-a-zero-day-that-could-compromise-google-workspace-agents)

### 11.3 AgentPoison (arXiv:2407.12784, 2024)

RAG backdoor attack achieving >80% success rate. Only write access to a single document in the knowledge base is required to produce a persistent backdoor that activates on semantically related queries indefinitely, without further attacker interaction.

**TREASURE Layer Analysis:** DATA LAYER (primary — differential privacy in embeddings degrades optimization surface; semantic validation catches instruction patterns; continuous semantic monitoring detects anomalous retrieval behavior).

- OWASP: ASI06 | TREASURE controls absent: UC-DATA-01/02/03
- [arXiv:2407.12784](https://arxiv.org/abs/2407.12784)

### 11.4 AiTM — Adversarial Agent-in-the-Middle (arXiv:2502.14847, ACL 2025)

A compromised agent uses a reflect() mechanism to generate a malicious instruction that fits semantically into the ongoing conversation, corrupting the orchestrator's goal representation. >70% success rate on AutoGen, MetaGPT, and custom frameworks. The attack compromises the entire system by manipulating messages.

**TREASURE Layer Analysis:** SECURITY LAYER (primary — per-agent JIT identity + signed inter-agent messages prevent reflect() injection); CONTROL LAYER (secondary — plan integrity monitoring detects orchestrator goal divergence).

- OWASP: ASI07 | TREASURE controls absent: UC-SEC-01/02, UC-CTRL-01
- [arXiv:2502.14847](https://arxiv.org/abs/2502.14847)

### 11.5 Atlassian Rovo — Indirect Prompt Injection via Confluence (2025)

An attacker with write access to a single Confluence page embeds adversarial instructions. When Rovo's agent is invoked, it retrieves the malicious page as RAG context and exfiltrates content from Confluence spaces the attacker cannot directly access — amplified by the agent's broad read permissions.

**TREASURE Layer Analysis:** DATA LAYER (primary — no semantic validation; no identity-scoped query constraints preventing cross-space retrieval); EXECUTION LAYER (secondary — no intent monitoring).

- OWASP: ASI01 + ASI03 + ASI06 | TREASURE controls absent: UC-DATA-01/03, UC-EXEC-05, UC-SEC-06
- [Atlassian Community report](https://community.atlassian.com/forums/Atlassian-Platform-Community/Rovo-Agent-Data-Exfiltration-via-Indirect-Prompt-Injection/ba-p/3001198)

### 11.6 Replit Vibe Coding Meltdown — AI Incident Database #1152 (July 2025)

A coding agent executed destructive operations on a production database during an explicit code freeze. The agent was not compromised — it executed its task with full fidelity to its own goal interpretation. No Agency Envelope existed to classify destructive database operations as requiring human authorization; no kill-switch was available. *Corrected 3 July 2026:* the agent claimed that rollback was impossible; that claim was false and the data was recovered via rollback — which strengthens the ASI09 classification.

**TREASURE Layer Analysis:** CONTROL LAYER (primary — no Decision Boundary Matrix; no Agency Envelope Validator; no kill-switch); GOVERNANCE LAYER (secondary — no policy classifying destructive operations on production resources); EXECUTION LAYER (tertiary — no minimal-privilege manifest excluding DELETE/DROP).

- OWASP: ASI01 + ASI09 + ASI10 | TREASURE controls absent: UC-CTRL-01/02/03, UC-EXEC-01
- [Wired reporting](https://www.wired.com/story/replit-ai-code-database-deletion/)

### 11.7 OpenClaw — CVE-2026-25253 (February 2026)

Control-plane authentication vulnerability (CVSS 8.8, CWE-669) in OpenClaw before 2026.1.29. The Control UI accepted `gatewayUrl` from the query string, auto-connected via WebSocket and transmitted the stored gateway token to the attacker's endpoint. A single crafted link opened while authenticated was sufficient to exfiltrate the token and obtain gateway access, enabling one-click RCE — including against local, non-internet-facing instances. Patched via mandatory confirmation on `gatewayUrl` changes and strict Origin-header validation. See Section 7.4 for the stage table.

**TREASURE Layer Analysis:** EXECUTION LAYER (primary — control-plane interface not treated as a validated execution surface); SECURITY LAYER (secondary — gateway token long-lived and not audience- or origin-bound).

- OWASP: ASI02 (misuse of the control interface itself) + ASI05 | TREASURE controls absent: UC-EXEC-03, UC-EXEC-05, UC-SEC-01 | ATLAS: AML.CS0050
- [NVD — CVE-2026-25253](https://nvd.nist.gov/vuln/detail/CVE-2026-25253) | [SonicWall Capture Labs](https://www.sonicwall.com/blog/openclaw-auth-token-theft-leading-to-rce-cve-2026-25253) | [runZero](https://www.runzero.com/blog/openclaw/)

### 11.8 OpenClaw — Ignored Stop Commands and Uncontrolled Mass Deletion (February 2026)

Meta Superintelligence Labs' Director of Alignment instructed her personal OpenClaw agent to *suggest* which emails to archive or delete, explicitly stating "don't action until I tell you to." On a much larger real inbox, context-window compaction silently dropped the safety instruction. The agent began bulk-deleting emails and ignored repeated stop commands sent from her phone; she had to reach the host machine to kill the process after 200+ emails were deleted. No remote, infrastructure-level kill-switch existed independent of the agent's own memory state.

**TREASURE Layer Analysis:** CONTROL LAYER (primary — no kill-switch independent of the agent's runtime/memory; no default-deny when a previously issued restriction becomes unverifiable); DATA LAYER (secondary — the safety instruction lived only in mutable, compactable context).

- OWASP: ASI01 + ASI10 | TREASURE controls absent: UC-CTRL-02, UC-DATA-04
- [TechCrunch, 23 Feb 2026](https://techcrunch.com/2026/02/23/a-meta-ai-security-researcher-said-an-openclaw-agent-ran-amok-on-her-inbox/)

> **Naming note:** same product as 11.7, distinct incident and root cause (runtime control failure vs. client-side authentication flaw). Kept as separate entities.

### 11.9 LiteLLM / Trivy Supply Chain Compromise (February–March 2026)

The threat actor group TeamPCP exploited a misconfiguration in Trivy's GitHub Actions environment in late February 2026 and published an infected Trivy binary. On 24 March 2026 the compromise cascaded into agentic AI tooling when LiteLLM's CI/CD pipeline executed Trivy without a pinned version. Microsoft, Kaspersky and Aqua Security published advisories; LiteLLM shipped a security update the same day.

**TREASURE Layer Analysis:** GOVERNANCE LAYER (primary — no dependency pinning or provenance gate in CI/CD, UC-GOV-03); EXECUTION LAYER (secondary — third-party CI tooling executed without cryptographic verification, UC-EXEC-02).

- OWASP: ASI04 + ASI02 | TREASURE controls absent: UC-GOV-03, UC-EXEC-02
- [OWASP GenAI Exploit Round-up Q1 2026](https://genai.owasp.org/2026/04/14/owasp-genai-exploit-round-up-report-q1-2026/)

### 11.10 PocketOS — Coding Agent Deletes Production Volume and Backups (April 2026) *(new in v1.2)*

On 24–25 April 2026 a Cursor coding agent running Claude Opus 4.6 hit a credential mismatch in the PocketOS staging environment and decided to resolve it by deleting a Railway storage volume. It used an API token whose authority to delete volumes was not apparent to the customer and issued a single `volumeDelete` call without confirmation. The call removed the production data volume together with the volume-level backups stored in the same volume, in about nine seconds. Asked to explain, the agent quoted the project rules it had violated. Railway recovered the data from offsite disaster backups (announced 27 April) and subsequently aligned its API with the dashboard's 48-hour soft-delete window. **No adversary and no prompt injection were involved.**

| # | Action | Missing Control | TREASURE Layer | Counterfactual |
|---|--------|-----------------|----------------|----------------|
| 1 | Agent decides to "fix" a staging credential mismatch by deleting infrastructure | UC-CTRL-01: no Decision Boundary Matrix entry for infrastructure deletion | CONTROL | Delete-volume classified as irreversible → requires HITL |
| 2 | Agent uses a token with undisclosed account-wide destructive authority | UC-SEC-01: credential not scoped to task or environment | SECURITY | Per-agent JIT credential scoped to staging, read/write only |
| 3 | Project rules forbidding destructive actions exist only as text in context | UC-GOV-02: policy not enforced by the Policy Engine | GOVERNANCE | Policy-as-Code denies the call regardless of the agent's reasoning |
| 4 | Single API call executes immediately, no confirmation | UC-CTRL-03: no HITL gate, no default-deny | CONTROL | Call blocked pending human confirmation within SLA |
| 5 | Volume-level backups destroyed with the volume | UC-DATA-05: backups inside the credential's blast radius | DATA | Backups in separate account; soft-delete window on destructive APIs |

> **Key finding:** intent is not enforcement (Principle 1). Every control that would have stopped this incident lives outside the agent.

- OWASP: ASI02 + ASI03 | TREASURE controls absent: UC-SEC-01, UC-CTRL-01/03, UC-GOV-02, UC-DATA-05 | ATLAS behavioral analogue: AML.T0101 (Data Destruction via AI Agent Tool Invocation)
- [The Register, 27 Apr 2026](https://www.theregister.com/software/2026/04/27/cursor-opus-agent-snuffs-out-startups-production-database/5224442) | [DEV postmortem with Railway changelog references](https://dev.to/axrisi/railway-database-deleted-by-an-ai-agent-the-pocketos-postmortem-2p7p)

### 11.11 OpenAI Evaluation Agents Escape Sandbox and Compromise Hugging Face (May–July 2026) *(new in v1.2)*

AI agents under evaluation on OpenAI's ExploitGym cyber-exploitation benchmark — GPT-5.6 Sol and an unreleased internal model, run with reduced cyber refusals and without OpenAI's production system prompts, auto-review models and safety classifiers — used the sandbox's access to an internal Artifactory package registry as foothold and message board, obtained administrator access through a token-refresh flaw, reached the internet via a 0-day from the package proxy cache, and rooted an exposed third-party evaluation harness. From there they submitted malicious dataset configurations to Hugging Face. Two dataset-processing flaws (local file read including `/proc/self/environ`; Jinja2 template injection in an fsspec reference specification) gave secret reads and then code execution in production workers. Kubernetes service-account tokens and EC2 instance-role credentials were harvested; a `system:masters` credential shared across clusters through a service connector gave cluster-admin on two clusters within one second; a Tailscale auth key and GitHub App tokens enabled lateral movement. Hugging Face reconstructed about 17,600 actions over 4.5 days (9–13 July). The agents' objective was the benchmark answer key — objective misspecification / reward hacking. Destructive calls were tested with `DryRun=True`, but the intrusion itself was real.

Detection failed on process, not tooling: anomalous agent behavior was seen in late May and flagged on 27 June without escalation; OpenAI states that chain-of-thought monitoring would have paged its security team more than a day before the Hugging Face breach. Hugging Face detected and contained independently; joint disclosure followed on 21 July.

| Phase | Action | Missing Control | TREASURE Counterfactual |
|-------|--------|-----------------|------------------------|
| Eval design | Safety layers disabled for measurement, no compensating envelope | UC-CTRL-01 (scope) | Eval environments inside the Agency Envelope; compensating egress/registry/credential limits |
| Sandbox exit | Internal registry reachable; proxy-cache 0-day to internet | UC-EXEC-03, UC-SEC-02 | No registry or internet route from the sandbox; egress allow-list |
| Early signals | May / 27 June anomalies not escalated | UC-SEC-07, UC-CTRL-02 | Owned alert with automatic T1/T2 containment |
| HF foothold | Dataset processing reads env secrets; template injection → RCE | UC-EXEC-03 (victim side) | Untrusted-input parsers without secrets in environment; no privileged pods |
| Credential chain | IMDS credentials; shared `system:masters`; VPN auth key | UC-SEC-01 | IMDS blocked; per-cluster credentials; short-lived VPN/CI tokens |
| Cascade | OpenAI → third-party harness → HF → internal repos | ASI08 / UC-SEC-05 | Per-organization failure domains; circuit breakers on automated channels |

> **Key findings:** (1) no human attacker is required for a full intrusion chain; (2) the chain was identity-driven end to end — identity is not authority (Principle 2); (3) a signal that does not escalate is not a control (UC-SEC-07); (4) containment must not wait for a human (Principle 4). *Presentation note:* the sandbox exit was application exploitation; ATT&CK T1611 (Escape to Host) applies only to the later privileged-pod-to-node step inside Hugging Face.

- OWASP: ASI10 + ASI03 + ASI05 + ASI08 | TREASURE controls absent: UC-CTRL-01/02, UC-EXEC-03, UC-SEC-01/02/07 | ATLAS: case study AML.CS0068 (v2026.08)
- [Hugging Face — technical timeline](https://huggingface.co/blog/agent-intrusion-technical-timeline) | [OpenAI — incident disclosure](https://openai.com/index/hugging-face-model-evaluation-security-incident/) | [OpenAI — report, 26 Aug 2026](https://openai.com/index/hugging-face-incident-and-the-road-ahead/)

### 11.12 Mastra npm Supply Chain Compromise — Sapphire Sleet (June 2026) *(new in v1.2)*

On 17 June 2026 the North Korean state actor Sapphire Sleet (BlueNoroff; Microsoft attribution with high confidence) compromised the npm maintainer account `ehindero`, which held publish rights on the `@mastra` scope, and republished 140+ packages of the Mastra TypeScript AI-agent framework with an injected typosquat dependency, `easy-day-js`, whose postinstall hook delivered a credential/crypto-wallet stealer and backdoor. The packages were removed and publish access revoked. It is a nation-state supply-chain operation aimed specifically at the AI-agent developer ecosystem.

**TREASURE Layer Analysis:** GOVERNANCE LAYER (primary — no lifecycle-script control; no new-dependency diff gate; AIBOM not compared across builds); EXECUTION LAYER (secondary — no provenance attestation required for framework packages).

- OWASP: ASI04 | TREASURE controls absent: UC-GOV-03, UC-GOV-04, UC-EXEC-02 | ATT&CK: T1195.002 | ATLAS: AML.T0010.001 (AI Supply Chain Compromise: AI Software)
- [Microsoft Security Blog, 17 Jun 2026](https://www.microsoft.com/en-us/security/blog/2026/06/17/postinstall-payload-inside-mastra-npm-supply-chain-compromise/) | [SecurityWeek](https://www.securityweek.com/north-korean-hackers-blamed-for-mastra-npm-supply-chain-attack/)

### 11.13 ClawHub Malicious Skills Campaigns (February–May 2026) *(new in v1.2)*

OpenClaw's skill marketplace was used for mass malware distribution: Koi Security's ClawHavoc disclosure documented 341 malicious skills and Trend Micro confirmed skills distributing Atomic macOS Stealer. ClawHub then integrated VirusTotal and ClawScan screening, yet Unit 42's February–May 2026 analysis still found evasive malicious skills that were not blocked (e.g. payload followed by large padding). China's CNCERT issued advisories in March 2026 warning of skill poisoning in the OpenClaw ecosystem. This is the real-world anchor for AST01/AST09 and for the marketplace limitation in Section 2.2 — replacing the incorrect use of CVE-2026-25253 in pre-addendum versions.

**TREASURE Layer Analysis:** EXECUTION LAYER (primary — no publisher signature requirement; manifests did not constrain credential access); GOVERNANCE LAYER (secondary — no curated internal registry or AIBOM gate).

- OWASP: ASI04 | TREASURE controls absent: UC-EXEC-01/02, UC-GOV-04 | ATLAS: case study AML.CS0049; techniques AML.T0115.002, AML.T0010.005
- [Unit 42, Jun 2026](https://unit42.paloaltonetworks.com/openclaw-ai-supply-chain-risk/) | [CNCERT advisory, 12 Mar 2026](https://www.cert.org.cn/publish/main/11/2026/20260312144519429724511/20260312144519429724511_.html)

### 11.14 Consolidated Attack-to-TREASURE Mapping

| # | Incident | OWASP ASI | TREASURE Layer(s) | Primary TREASURE Controls Absent |
|---|----------|-----------|------------------|-------------------------------|
| 11.1 | EchoLeak CVE-2025-32711 | ASI01+ASI06+ASI09 | DATA+EXEC+SEC | UC-DATA-01/02, UC-EXEC-05, UC-SEC-06 |
| 11.2 | Gemini Memory Attack / GeminiJack | ASI06 | DATA+GOV | UC-DATA-01/02/04, UC-GOV-05 |
| 11.3 | AgentPoison arXiv:2407.12784 | ASI06 | DATA | UC-DATA-01/02/03 |
| 11.4 | AiTM arXiv:2502.14847 | ASI07 | SEC+CTRL | UC-SEC-01/02, UC-CTRL-01 |
| 11.5 | Atlassian Rovo Indirect PI | ASI01+ASI03+ASI06 | DATA+EXEC+SEC | UC-DATA-01/03, UC-EXEC-05, UC-SEC-06 |
| 11.6 | Replit Vibe Coding Meltdown | ASI01+ASI09+ASI10 | CTRL+GOV+EXEC | UC-CTRL-01/02/03, UC-EXEC-01 |
| 11.7 | OpenClaw CVE-2026-25253 | ASI02+ASI05 | EXEC+SEC | UC-EXEC-03/05, UC-SEC-01 |
| 11.8 | OpenClaw stop-failure | ASI01+ASI10 | CTRL+DATA | UC-CTRL-02, UC-DATA-04 |
| 11.9 | LiteLLM / Trivy | ASI04+ASI02 | GOV+EXEC | UC-GOV-03, UC-EXEC-02 |
| 11.10 | PocketOS | ASI02+ASI03 | SEC+CTRL+DATA+GOV | UC-SEC-01, UC-CTRL-01/03, UC-GOV-02, UC-DATA-05 |
| 11.11 | OpenAI agents / Hugging Face | ASI10+ASI03+ASI05+ASI08 | CTRL+SEC+EXEC | UC-CTRL-01/02, UC-EXEC-03, UC-SEC-01/02/07 |
| 11.12 | Mastra npm / Sapphire Sleet | ASI04 | GOV+EXEC | UC-GOV-03/04, UC-EXEC-02 |
| 11.13 | ClawHub malicious skills | ASI04 | EXEC+GOV | UC-EXEC-01/02, UC-GOV-04 |

### 11.15 Minimum Viable Security Posture — MVSP v1.2

> Entity: TRSR.MVSP.V12. Supersedes the v1.0 claim (UC-DATA-01/02 **or** UC-CTRL-01 would have broken 5 of 6 chains), which remains valid for its original scope.

**Method.** For each of the 13 incidents, controls were classified from the stored counterfactual as **P — prevention breaker** (the control alone stops the chain before primary impact) or **L — impact limiter** (bounds, detects or recovers). An exhaustive search over prevention breakers then found the smallest set that breaks every chain.

| Incident | UC-CTRL-01 | UC-DATA-01 | UC-EXEC-02 | UC-SEC-01 | Other P | Resilience (L) |
|----------|:---:|:---:|:---:|:---:|---|---|
| 11.1 EchoLeak | | **P** | | | EXEC-05, SEC-06 | SEC-03 |
| 11.2 Gemini | | **P** | | | — | DATA-04, GOV-05 |
| 11.3 AgentPoison | | **P** | | | DATA-02 | DATA-03 |
| 11.4 AiTM | **P** | | | **P** | — | SEC-02, SEC-05 |
| 11.5 Rovo | | **P** | | | DATA-03, EXEC-05, SEC-06 | — |
| 11.6 Replit | **P** | | | | CTRL-03, EXEC-01 | CTRL-02, DATA-05 |
| 11.7 OpenClaw CVE | | | | **P** | EXEC-03, EXEC-05 | SEC-03 |
| 11.8 OpenClaw stop-failure | **P** | | | | — | CTRL-02, DATA-04 |
| 11.9 LiteLLM/Trivy | | | **P** | | GOV-03 | GOV-04 |
| 11.10 PocketOS | **P** | | | **P** | CTRL-03, GOV-02 | DATA-05 |
| 11.11 OpenAI/HF | **P** | | | L | SEC-02, EXEC-03 | SEC-07, CTRL-02 |
| 11.12 Mastra | | | **P** | | GOV-03 | GOV-04 |
| 11.13 ClawHub | | | **P** | | — | EXEC-01, GOV-04 |
| **Chains broken** | 5 | 4 | 3 | 3 | | |

**Result.**

- **No set of three controls breaks all 13 chains.** The minimum is four, with three equivalent solutions sharing UC-CTRL-01 + UC-DATA-01 + UC-EXEC-02 plus one of UC-SEC-01, UC-EXEC-03 or UC-EXEC-05.
- **Tier 1 — Prevention core (4):** **UC-CTRL-01** Agency Envelope → **UC-DATA-01** governed ingestion → **UC-EXEC-02** signing (skills, CI tooling, dependencies) → **UC-SEC-01** per-agent scoped JIT identity. Cumulative coverage 5 → 9 → 12 → **13/13**. UC-SEC-01 is chosen over the alternatives because it double-covers AiTM and PocketOS and also limits blast radius in OpenAI/HF (Principle 2).
- **Tier 2 — Resilience core (3):** **UC-CTRL-02** tiered kill-switch, **UC-SEC-07** escalation ownership, **UC-DATA-05** recovery independence. Mandatory because prevention is never complete (TRSR.LIMITS.MARKETPLACE, TRSR.LIMITS.BASELINE) and because in three incidents the only stored control that would have mattered after onset was containment or recovery.
- **Profile overlays:** coding / infrastructure agents **+UC-CTRL-03** (irreversible-action HITL gate); RAG / copilot agents **+UC-EXEC-05 +UC-SEC-06**; build pipelines **+UC-GOV-03**; multi-agent systems **+UC-SEC-05**.

> **Caveat.** This is a counterfactual analysis over documented incidents, not an empirical effectiveness measurement. The P/L classification follows the stored, author-reviewed counterfactuals; OpenClaw stop-failure → UC-CTRL-01 (bulk deletion classified as requiring HITL) is a v1.2 derivation.

---

## 12. MCP Security — The Execution Layer's Expanding Attack Surface

The Model Context Protocol (MCP), introduced by Anthropic in November 2024 and donated to the Linux Foundation's Agentic AI Foundation in December 2025, is the de facto standard for connecting AI agents to external tools, APIs, and data sources. Its rapid adoption created a structurally significant attack surface that extends the TREASURE Execution Layer's threat model.

The OWASP GenAI Security Project's Practical Guide for Secure MCP Server Development (February 2026) identifies MCP servers as high-risk execution environments with vulnerability classes that have no direct parallel in traditional API security. A 2026 empirical scan of over 5,000 open-source MCP servers documented that 40% required no authentication, 43% contained command-injection vulnerabilities, and 79% handled credentials in plaintext. MCP server CVEs disclosed through 2026 continue to be dominated by classic web flaw classes (path traversal, secrets returned in tool output, SSRF).

### 12.1 MCP-Specific Threat Classes

**Tool Poisoning.** An adversary modifies a tool's description or schema — at registration time or via a runtime update — causing the agent to invoke the tool under false pretences. The OWASP MCP guide requires cryptographically signed tool manifests with hash verification at load time. Maps to UC-EXEC-02 and UC-EXEC-01. ATLAS: AML.T0110 AI Agent Tool Poisoning (sub-techniques for definition/instructions, implementation and runtime response since v2026.07).

**Rug Pull Attacks.** A registered and initially legitimate MCP server alters its tool behavior after trust is established. Rug pull resistance requires pinned, content-addressed tool definitions or continuous behavioral integrity monitoring — UC-EXEC-02 (signed manifests enforced at each instantiation) and UC-GOV-05 (drift detection against the CI/CD-validated baseline). ATLAS: AML.T0109 AI Supply Chain Rug Pull.

**Confused Deputy Attacks.** The MCP server acts using its own elevated permissions rather than the scoped permissions of the user on whose behalf it operates. The OWASP guide mandates OAuth 2.1 with Token Delegation (RFC 8693): the MCP server requests a scoped, audience-bound token for the downstream service. Aligns with UC-SEC-01, which requires credentials scoped per invocation and issued just-in-time rather than held as ambient long-lived tokens.

**Token Passthrough.** An MCP server forwards a raw client authentication token to a downstream API rather than requesting a token issued to itself. This breaks audit trail integrity and bypasses audience validation. UC-SEC-01 addresses this through its JIT credential model.

### 12.2 MCP Server Security Minimum Bar (OWASP 2026) and the 2026-07-28 Specification

| MCP Security Requirement | TREASURE Control | Notes |
|--------------------------|-----------------|-------|
| No Token Passthrough — use OAuth 2.1 token delegation | UC-SEC-01 | Token lifespan bounded to minimum necessary; audience validation required |
| Short-lived tokens with revocation check per call | UC-SEC-01 | JIT credential per tool invocation |
| OAuth 2.1 / OIDC enforced for all remote connections | UC-SEC-01 | MCP 2026-07-28: clients MUST validate RFC 9207 `iss` when present (SEP-2468) and MUST NOT reuse credentials across authorization servers (SEP-2352) |
| Client registration | UC-SEC-01 | MCP 2026-07-28 deprecates Dynamic Client Registration in favour of Client ID Metadata Documents |
| Containerization: non-root, network-restricted container | UC-EXEC-03 | Infrastructure-grade sandboxing, not config-level |
| Session isolation: memory and execution contexts segregated per user | UC-EXEC-03 | MCP 2026-07-28 removes protocol-level sessions; cross-call state uses explicit server-minted handles — isolation must be enforced by the server, not assumed from a session |
| Schema enforcement: validate all inputs/outputs against strict JSON Schema | UC-EXEC-05 | 2026-07-28 allows full JSON Schema 2020-12 with `$ref` resolution bounds — validators must enforce those bounds |
| Least privilege: tools only have exact permissions needed | UC-EXEC-01 | Minimal-privilege skill manifests as hard constraints |
| Secrets in credential vaults — never in environment variables or logs | UC-SEC-01 | LLM must never have access to raw credentials |
| Cryptographically signed tool manifests | UC-EXEC-02 | **Still not in the MCP specification as of 2026-07-28** |
| Audit trail for all tool invocations | UC-EXEC-04 / UC-SEC-03 | OpenTelemetry trace context in `_meta` (SEP-414) as correlation key |

> **⚠️ Implementation gap (re-verified 2026-09-29):** the MCP 2026-07-28 changelog contains no native tool-manifest signing mechanism. Implementing UC-EXEC-02 for MCP still requires custom infrastructure. Treat as documented residual risk with compensating controls (behavioral monitoring, static manifest approval workflows, curated registries).

### 12.3 MCP in the TREASURE Execution Layer

```
TREASURE Concept            → MCP Implementation
─────────────────────────────────────────────────
Skill                       → MCP Tool definition
Skill Registry              → MCP server registry / tool registry
Skill Executor              → MCP server execution environment
Skill Security Manifest     → MCP tool schema + signed manifest (custom)
Minimal-Privilege           → OAuth 2.1 scopes + least-privilege tool permissions
Sandboxing                  → MCP server containerization (non-root, network-restricted)
Pre-Call Hooks              → Input validation against strict JSON Schema (+ ACS hooks where available)
Output Validation Pipeline  → Output validation + tool description behavioral verification
Trajectory correlation      → OpenTelemetry traceparent in _meta
```

> *Corrected 3 July 2026:* OpenClaw CVE-2026-25253 is not an MCP supply-chain attack. The canonical supply-chain evidence for the Execution Layer is LiteLLM/Trivy (11.9), Mastra (11.12) and ClawHub (11.13).

---

## 13. Emerging Threat Vectors and Framework Evolution (2026)

### 13.1 The OWASP State of Agentic AI Security — June 2026 Update

The OWASP GenAI Security Project published the State of Agentic AI Security and Governance v2.01 in June 2026, documenting the transition from theoretical taxonomy to production-exploited vulnerabilities.

**Finding 1: The threats are real now.** Almost every entry in the OWASP Agentic Top 10 now has associated production incidents, vendor advisories, or CVEs. TREASURE's evidence base grew from six documented incidents (v1.0) to thirteen (v1.2) — still only the visible fraction of the operational incident population.

**Finding 2: AI Safety and AI Security cannot continue as parallel functions.** At the deployment layer, the same controls govern both safety and security failures. The 2026 no-adversary incidents (PocketOS, OpenAI/Hugging Face) are the clearest demonstration: they are safety failures with security-grade consequences, prevented by the same ARCP-level controls.

**Finding 3: Agent Identity and Non-Human Identity (NHI) is the new control plane.** The CSA 2025 survey found 51% of organizations have no clear ownership of AI identities and 24% take more than 24 hours to revoke a compromised credential. The OpenAI/Hugging Face intrusion — every step after the sandbox escape used a machine credential — makes UC-SEC-01 the single highest-impact foundational control.

### 13.2 A2A Protocol — Inter-Agent Communication Security Surface

The Agent-to-Agent (A2A) protocol formalizes direct peer-to-peer communication between autonomous agents. The OWASP GenAI Security Project's Agent Name Service (ANS) proposal addresses the discovery and authentication gap that enables the AiTM attack class, aligning with UC-SEC-01.

Security properties required for A2A under TREASURE's inter-agent zero-trust model:
- **Authentication** — every message carries a signature from the sending agent's verified identity credential.
- **Integrity** — message content is tamper-evident.
- **Authorization scope** — the sender's delegation scope is verifiable against the Governance Layer's inter-agent policy.
- **Non-repudiation** — the trajectory log provides the attribution record.

### 13.3 The MAESTRO Layer Clarification

TREASURE uses the seven-layer structure of the original CSA publication (February 2025, Ken Huang):

| MAESTRO Layer | Name | Primary Threat (canonical CSA) |
|---|---|---|
| L1 | Foundation Models | Model theft, adversarial prompt injection, backdoor attacks |
| L2 | Data Operations | RAG poisoning, context leakage, data provenance |
| L3 | Agent Frameworks | Insecure orchestration, logic bugs, goal misalignment |
| L4 | Deployment and Infrastructure | Container escapes, insecure APIs, MCP server compromise |
| L5 | Evaluation and Observability | Monitoring bypass, adversarial drift, detection evasion |
| L6 | Security and Compliance | Cross-cutting security controls (vertical layer spanning L1–L5) |
| L7 | Agent Ecosystem | Marketplace manipulation, agent impersonation, tool squatting, rug pulls |

Some derivative analyses and tools present simplified variants or different L5/L6/L7 assignments. Verify which numbering your tooling uses before applying TREASURE's MAESTRO mappings. v1.2 applies this canonical mapping to every section and dataset entity (see Changelog item 2).

> The OWASP Agentic Security Initiative endorsed MAESTRO as "a comprehensive extension of STRIDE for handling Agentic AI" in its Agentic Threats and Mitigations documentation.

### 13.4 Open Research Directions (updated September 2026)

**Blast Radius Quantification.** No CVSS-equivalent measurement methodology exists for agentic compromise scope. TREASURE uses Blast Radius qualitatively (union of writable systems, readable data and influenceable downstream agents). PocketOS adds a necessary dimension: *recoverability* of what is inside the radius.

**Multi-Agent Trust Propagation.** How permissions should propagate when an agent spawns a sub-agent at runtime remains unresolved. ATLAS v2026.08 now catalogues autonomous agent-to-agent coordination (AML.T0118, incl. communication via shared artifacts) — the OpenAI agents used an internal package registry as a message board.

**Objective Misspecification as a Security Risk.** The OpenAI/Hugging Face incident was driven by an agent pursuing a benchmark objective by any available means. ATLAS v2026.08 extends its scope to "harmful autonomous behavior materially enabled by AI" and adds autonomous reconnaissance, attack-path adaptation and orchestration techniques (AML.T0116, AML.T0117, AML.T0124). TREASURE treats this as ASI10 and addresses it through the Agency Envelope, not through model alignment.

**MCP Cryptographic Tool Manifests.** Still absent from the MCP specification (2026-07-28). Custom implementations remain recommended for high-assurance deployments.

**AI SBOM / AIBOM Standardization.** SPDX and CycloneDX have initial AI SBOM extensions; TREASURE UC-GOV-04 aligns with CycloneDX ML-BOM as the best-supported option.

---

## 14. Design Principles (v1.2)

Five principles distilled from the 2026 evidence base and first presented at RootedCON Valencia (18 September 2026). They constrain how every TREASURE control is implemented. Dataset entities: TRSR.PRINCIPLE.01–05.

| # | Principle | Meaning for implementers | Evidence |
|---|-----------|-------------------------|----------|
| 1 | **Intent is not enforcement.** | Rules, restrictions and instructions held in the agent's context express intent. Only controls enforced outside the agent (ARCP, infrastructure) constrain behavior. A policy the agent can read but the runtime does not enforce is a paper control. | PocketOS (agent quoted the rules it broke); OpenClaw stop-failure (compaction dropped the restriction) |
| 2 | **Identity is not authority.** | Authenticating an agent says nothing about what it may do, now, on which resource. Identity and authorization are governed and enforced separately; every credential carries a visible, minimal scope. | PocketOS (token with undisclosed destructive scope); OpenAI/HF (shared cluster-admin identity); AIUC-1 Q2-2026 identity/access split |
| 3 | **Irreversible actions need an external stop condition.** | Every irreversible action class requires a gate outside the agent (HITL within SLA, default-deny) *and* a recovery path outside the agent's credential blast radius. | PocketOS; Replit |
| 4 | **Asymmetric autonomy.** | Containment acts autonomously — it must not wait for a human who is not there yet. Authority expansion and irreversible actions always require a human. | OpenAI/HF (signals not escalated; CoT monitoring would have paged > 1 day earlier) |
| 5 | **Containment logic is platform-independent; the enforcement adapter is platform-specific.** | Detection and containment are specified once against TREASURE controls; each platform supplies an adapter (Section 7). The OWASP Agent Control Standard defines a portable hook surface for such adapters. | Section 7 platform gaps; OWASP ACS (Sept 2026) |

**Three conditions for containment to work** (operational corollary): you must know what "normal" looks like (UC-SEC-04 / Drift Score); you must act without waiting for a human (UC-SEC-07 → UC-CTRL-02 T1/T2); you must be able to stop mid-action, not only after (UC-CTRL-02 T1 at the Tool Router / Policy Engine).

---

## 15. Standards & Crosswalk Update — September 2026

All items verified against primary sources on 29 September 2026. Dataset entities: TRSR.XWALK.*.

### 15.1 OWASP Agent Control Standard (ACS)

Donated to the OWASP GenAI Security Project and announced on 1–2 September 2026 alongside the OWASP Top 10 for LLM Applications 2026. ACS defines how agent platforms expose middleware hooks and how declarative safety policies are enforced through them, portable across agent frameworks and enforced at runtime. It was co-created at Zenity and is now developed in the open under OWASP.

**TREASURE impact:** the ARCP (Tool Router pre-call hooks, Policy Engine, Agency Envelope Validator) is conceptually an implementation of ACS-style hooks. Section 7 platform adapters should target ACS where a platform supports it. A control-by-hook crosswalk (TREASURE UC-* ↔ ACS hook points) is a v1.3 work item. **Attribution:** "OWASP GenAI Security Project standard (donated; co-created at Zenity)".

### 15.2 MITRE ATLAS v2026.08 (pinned)

- Content versioning moved to **YYYY.MM** from May 2026; every technique now carries a platform tag (Predictive AI, Generative AI, Agentic AI, Enterprise).
- **Breaking change (v2026.07):** Publish Poisoned AI Agent Tool (formerly **AML.T0104**) is now a sub-technique of **AML.T0115 Publish Poisoned AI Artifacts**, together with the former Publish Poisoned Datasets and Publish Poisoned Models. AML.T0110 AI Agent Tool Poisoning gained sub-techniques (definition and instructions, implementation, runtime response).
- **v2026.08 (published 1 September 2026):** 16 tactics, 114 techniques, 83 sub-techniques, 39 mitigations, 72 case studies. New mitigations **AML.M0037 AI Agent Authority Expansion Controls** (→ UC-CTRL-01) and **AML.M0038 AI Agent Scope Drift Detection** (→ UC-SEC-04, UC-GOV-05, Drift Score); autonomous-behaviour techniques AML.T0116–T0128; tactic AML.TA0001 renamed *AI Attack Adaptation*; case study **AML.CS0068** covers the OpenAI/Hugging Face incident.
- Other verified cross-references used in v1.2: AML.CS0049 (Poisoned ClawdBot Skill), AML.CS0050 (OpenClaw 1-Click RCE), AML.CS0059 (EchoLeak), AML.T0101 (Data Destruction via AI Agent Tool Invocation), AML.T0105 (Escape to Host), AML.T0010.001 (AI Supply Chain Compromise: AI Software), AML.T0109 (Rug Pull), AML.T0110 (Tool Poisoning).

**Verification method (v1.2).** Every AML ID in the three TREASURE artifacts was resolved against the official `ATLAS-2026.08.yaml` release asset (0 unresolved; AML.T0104 is referenced only as the former ID of AML.T0115.002). Case-study procedures were extracted from the release's relationship graph:

| Case study | TREASURE incident | Key procedure techniques (verified) |
|-----------|-------------------|-------------------------------------|
| AML.CS0068 | TRSR.INC.HF_OPENAI | AML.T0117 Autonomous Attack-Path Adaptation · AML.T0017.001 Autonomous Exploit Development · AML.T0118.000 Communication via Shared Artifacts · AML.T0119 Exploit Automated Artifact Processing Pipeline · AML.T0055 Unsecured Credentials · AML.T0091.000 Application Access Token · AML.T0105 Escape to Host · AML.T0122 Exploitation of Remote Services |
| AML.CS0049 | TRSR.INC.CLAWHUB | AML.T0115.002 Publish Poisoned AI Artifacts: AI Agent Tools · AML.T0111 Reputation Inflation · AML.T0010.005 AI Supply Chain Compromise: AI Agent Tool · AML.T0110.000 Tool Poisoning: Definition and Instructions · AML.T0011.002 User Execution: Poisoned AI Agent Tool |
| AML.CS0050 | TRSR.INC.OPENCLAW | AML.T0011.003 Malicious Link · AML.T0106 Exploitation for Credential Access · AML.T0081 Modify AI Agent Configuration · AML.T0105 Escape to Host |
| AML.CS0059 | TRSR.INC.ECHOLEAK | AML.T0070 RAG Poisoning · AML.T0051.002 Triggered Prompt Injection · AML.T0077 LLM Response Rendering · AML.T0025 Exfiltration via Cyber Means |

**Official mitigation linkage — findings:**
- ATLAS links **AML.M0029 Human In-the-Loop for AI Agent Actions** to **AML.T0101 Data Destruction via AI Agent Tool Invocation**, which independently corroborates the TREASURE Sigma rule (Section 16.2) and UC-CTRL-03.
- For AML.CS0068, ATLAS links only AML.M0037 and AML.M0038 (plus generic M0005/M0011/M0016/M0019/M0020/M0022) to the procedure techniques.
- **ATLAS contribution candidates** — TREASURE counterfactual controls with no ATLAS mitigation linked to the relevant case studies: escalation ownership with automatic containment (UC-SEC-07), tiered containment (UC-CTRL-02), recovery independence (UC-DATA-05), and workload-credential hygiene (UC-SEC-01 v1.2). PocketOS has no ATLAS case study yet (a no-adversary destructive action).

**TREASURE impact:** `maps_to_atlas` is now populated in the canonical dataset (controls → mitigations; incidents → case studies + verified procedure techniques), pinned to v2026.08. Re-verify on each monthly ATLAS release. The TRSR.* namespace remains distinct from AML.*.

### 15.3 AIUC-1 Q3-2026

AIUC-1 is revised quarterly. Q2-2026 (15 April 2026) changed 14 requirements and 23 controls, focused on MCP/A2A security, third-party risk and agent identity; it separated agent identity management from access management and called for just-in-time credentials scoped to subtasks or tool calls. Q3-2026 (15 July 2026) expanded coding-agent requirements (secrets management, secure defaults, execution-level safeguards) and published auditor guidance. Next release: **15 October 2026**.

**TREASURE impact:** UC-SEC-01 and UC-CTRL-01/03 already implement the identity/access split and JIT pattern. UC-* remain TREASURE internal IDs. Action: requirement-level re-pin against Q3-2026 before 15 October 2026.

### 15.4 Model Context Protocol — specification 2026-07-28

Stateless protocol core (sessions and the initialize handshake removed; `server/discover` added); authorization hardening (RFC 9207 `iss` validation, credentials bound to their issuing authorization server, `application_type` in client registration; Dynamic Client Registration deprecated in favour of Client ID Metadata Documents); OpenTelemetry trace context in `_meta`; Roots, Sampling and Logging deprecated; formal 12-month deprecation policy. **No native tool-manifest signing.** See Section 12.2.

### 15.5 NIST — AI Agent Standards Initiative (CAISI) and NCCoE agent identity concept

The CAISI AI Agent Standards Initiative (launched 17 February 2026) works across industry-led standards, open protocol development, and security and identity research. The companion NCCoE concept paper on software and AI agent identity and authorization proposes applying OAuth 2.0/2.1, OpenID Connect and SPIFFE/SPIRE to agent workloads. **TREASURE impact:** closes the v1.1 forward-reference gap; the NCCoE pattern is the reference implementation path for UC-SEC-01. No final NIST Special Publication yet — tracked.

### 15.6 EU AI Act — Digital Omnibus on AI (Regulation (EU) 2026/1744)

Published in the Official Journal on 24 July 2026, in force 27 July 2026. High-risk obligations deferred: stand-alone Annex III systems to **2 December 2027**; AI embedded in Annex I products to **2 August 2028**. GPAI obligations and Article 5 prohibitions are unaffected. **TREASURE impact:** Governance Layer compliance calendars (Agent Risk Register) must reference Regulation (EU) 2024/1689 as amended by 2026/1744. The deferral changes dates, not architecture.

---

## 16. Detection & Response Engineering — TREASURE Lab

> **Evidence-class rule:** TRSR.LAB.* entities are research artefacts from TREASURE lab work (first shown at RootedCON Valencia 2026). They are reference implementations of TREASURE controls. They are **never** cited as incident evidence and are not validated benchmarks.

### 16.1 Drift Score (TRSR.LAB.DRIFTSCORE)

**Idea.** Model each agent session as a directed graph of tool invocations and measure its graph-edit distance (GED) to the CI/CD-validated baseline graph for that agent class. Not a signature — a shape. The score raises the alert; **the new edge is the explanation.**

```
BASELINE:  tool_A → tool_B → tool_C
LIVE:      tool_A → credential_lookup → prod_delete
NEW EDGE:  credential_lookup → prod_delete      ← "what changed?"
```

**Methodology requirements before production use:**
1. Exact GED is NP-hard — use a declared approximation (e.g. bipartite assignment-based GED).
2. Declare node/edge insertion, deletion and substitution costs; weight edges by action class (irreversible > write > read).
3. Normalize by baseline graph size; compute over a sliding window per session.
4. Calibrate thresholds per agent class on a labelled replay set; report false-positive rate and MTTD.
5. Route alerts through UC-SEC-07 so that threshold breach triggers UC-CTRL-02 T1/T2 automatically.

Implements UC-SEC-04 and UC-GOV-05. ATLAS mitigation reference: AML.M0038 AI Agent Scope Drift Detection.

### 16.2 Sigma rule — irreversible action without HITL within SLA (TRSR.LAB.SIGMA_HITL)

Detection-as-code for UC-CTRL-03. Corrected from the version shown at RootedCON: a tool call is not a process creation event, so a custom logsource is used; the exclusion is expressed as a filter; ATLAS IDs go in `references` because Sigma has no ATLAS tag namespace.

```yaml
title: Irreversible Agent Action Allowed Without HITL Confirmation Within SLA
id: 41e90f12-9fae-4aa5-a69a-bb13a7d5b8a1
status: experimental
description: >
  Fires when an agent tool invocation classified as irreversible (Decision Boundary
  Matrix) is allowed without a human confirmation recorded inside the SLA window.
  Firing triggers TREASURE UC-CTRL-02 T1 (Stop) and T2 (Contain).
references:
  - TREASURE UC-CTRL-03 / UC-CTRL-02 (TRSR.LAB.SIGMA_HITL)
  - MITRE ATLAS AML.T0101 Data Destruction via AI Agent Tool Invocation (v2026.08)
  - MITRE ATLAS AML.M0029 Human In-the-Loop for AI Agent Actions (v2026.08)
author: Roger Sanz (TREASURE Lab)
date: 2026-09-29
tags:
  - attack.impact
  - attack.t1485
logsource:
  product: agent_runtime        # custom; map per platform adapter (Principle 5)
  category: tool_invocation
detection:
  selection:
    action_class: irreversible
    policy_decision: allowed
  filter_hitl:
    hitl_confirmed: 'true'
    hitl_latency_seconds|lte: 300   # SLA window, set per Agency Envelope Policy
  condition: selection and not filter_hitl
fields:
  - agent_id
  - tool_name
  - target_resource
  - credential_id
  - trace_id
falsepositives:
  - Pre-approved break-glass runbooks carrying a signed change ticket
level: critical
```

### 16.3 RootedCON VLC 2026 rogue-agent chain — audited technique set (TRSR.LAB.ROOTED_CHAIN)

Lab kill chain: malicious skill via marketplace → execution → escape to host → C2 tool transfer. Five ATT&CK techniques were kept after self-audit; v1.2 refines sub-techniques and adds verified ATLAS IDs (ATT&CK v19.2, ATLAS v2026.08).

| Stage | ATT&CK (v1.2) | Change vs. deck | ATLAS |
|-------|---------------|-----------------|-------|
| Resource Development | T1583.001 Acquire Infrastructure: Domains (C2 domain) + T1608.001 Stage Capabilities: Upload Malware (skill hosted on marketplace) | T1583 alone did not cover hosting the skill | AML.T0115.002 (AI Agent Tools) |
| Initial Access | T1195.002 Compromise Software Supply Chain | Deck cited parent T1195 with the T1195.001 name | — |
| Execution | T1059.006 Python; T1204.005 User Execution: Malicious Library *(proposed reinstatement — the victim installs and uses the skill)* | T1059 refined; T1204 cut in deck is reconsidered | — |
| Privilege Escalation | T1611 Escape to Host | Applies to container→node breakout; in OpenAI/HF only the privileged-pod→node step, not the sandbox exit | AML.T0105 Escape to Host |
| Command and Control | T1105 Ingress Tool Transfer | — | — |
| Impact (demo) | T1485, T1486, T1552 + T1567, T1053, T1548 (five fictional demo environments) | — | AML.T0101 |

Removed after audit (unchanged): T1547, T1068, T1562 (execution stage); T1047, T1071.001 (C2 stage).

---

## Appendix A: Detailed AIUC-1 Control-by-Control Mapping

> UC-\* identifiers are TREASURE's internal crosswalk convention, not official AIUC-1 requirement codes. ATLAS mitigation IDs verified against v2026.08.

| Control ID | Control Statement | TREASURE Implementation | Security Rationale | ATLAS |
|------------|--------------------------|------------------------|--------------------|------|
| **UC-DATA-01** | Establish a single authoritative knowledge source with documented provenance for all data used in agent reasoning | Diamond Record: governed ingestion pipeline; provenance metadata schema enforced at ingest; source attestation stored alongside each document chunk | CRITICAL — Without provenance, poisoned documents are indistinguishable from legitimate ones at retrieval time | AML.M0025 |
| **UC-DATA-02** | Implement embedding integrity controls capable of detecting and preventing vector index manipulation | Differential privacy in embeddings; cryptographic hash of index state per snapshot; semantic anomaly scoring on candidate ingest documents | HIGH — EchoLeak and AgentPoison both exploit the absence of this control | AML.M0031 |
| **UC-DATA-03** | Enforce access control at the retrieval layer, not solely at the application layer | Identity-scoped query constraints enforced by the Memory Manager in the ARCP | HIGH — Application-layer access control is bypassable via prompt injection; retrieval-layer enforcement is not | AML.M0005, AML.M0019 |
| **UC-DATA-04** | Maintain versioned, rollback-capable snapshots of all agent knowledge bases and active constraints | Append-only vector index snapshots with HMAC integrity; constraint records held outside compactable context; rollback procedure documented and tested | MEDIUM — Enables recovery from detected poisoning; keeps safety constraints durable | AML.M0031 |
| **UC-DATA-05** *(v1.2)* | Ensure no credential reachable by an agent can destroy both production data and its recovery path | Backups in a separate account/tenant; soft/delayed delete on agent-reachable destructive APIs; drilled restore with RTO/RPO | CRITICAL — PocketOS lost production and co-located backups in one call | AML.T0101 (threat) |
| **UC-EXEC-01** | Enforce least-privilege execution permissions for all agent tools and skills | Minimal-privilege skill manifests; Tool Router enforces allow-lists as hard constraints; manifest violations abort execution | CRITICAL — Over-privileged tools are the primary enabler of ASI02 | AML.M0028, AML.M0026 |
| **UC-EXEC-02** | Implement cryptographic signing for all executable agent components, CI tooling and dependencies prior to deployment | Skill registry acts as CA; valid signature over complete definition required before mounting; unsigned components rejected | CRITICAL — LiteLLM/Trivy, Mastra and ClawHub exploited the absence of provenance verification | AML.M0013, AML.M0014 |
| **UC-EXEC-03** | Sandbox all agent code execution environments; execution must not propagate to the host runtime | Process isolation per skill; reduced-privilege MCP processes; egress filtering; no registry/internet route unless declared; origin-validated control plane | CRITICAL — ASI05 requires sandbox integrity as an independent layer (OpenClaw CVE, OpenAI/HF) | AML.M0032 |
| **UC-EXEC-04** | Maintain an immutable audit trail of all agent tool invocations | Off-agent append-only invocation log; agent identity, skill ID + version hash, parameter/output hashes, timestamps; signed | HIGH — Without this record, trajectory manipulation is forensically undetectable | AML.M0024 |
| **UC-EXEC-05** | Implement pre-invocation intent validation for all tool calls | Pre-call hooks in the ARCP evaluate parameters against plan state; low goal-plan consistency → HITL escalation | HIGH — Primary execution-layer detection for ASI01 | AML.M0030, AML.M0033 |
| **UC-GOV-01** | Version-control all agent behavioral specifications | Agent artifact repository; PR workflow with required approvals; merge history = regulatory audit trail | CRITICAL — An unversioned agent is production code without source control | — |
| **UC-GOV-02** | Express all agent behavioral policies in machine-executable, declarative formats enforced at runtime | OPA/Rego or YAML interpreted by the Policy Engine; prompt-level rules do not satisfy this control | HIGH — Intent is not enforcement (PocketOS) | AML.M0021 |
| **UC-GOV-03** | Integrate automated security testing and supply-chain gates in the agent CI/CD pipeline | Static analysis; adversarial regression; automated red teaming; AIBOM validation; pinned verified dependencies incl. CI tooling; lifecycle scripts untrusted | HIGH — Primary prevention mechanism for ASI04 | AML.M0035, AML.M0016 |
| **UC-GOV-04** | Produce and maintain an AI Bill of Materials (AIBOM) for every agent deployment | Model version + provider; skills with hashes and certs; tool API schema versions; knowledge sources; build-to-build diff | HIGH — Prerequisite for supply-chain risk assessment and attribution | AML.M0023 |
| **UC-GOV-05** | Continuous drift detection against the CI/CD-validated behavioral baseline | Production metrics vs. baseline; thresholds per agent class; breaches routed via UC-SEC-07 | MEDIUM — Agentic drift is slow-moving; standard monitoring misses it | AML.M0038 |
| **UC-CTRL-01** | Define and enforce an Agency Envelope for each agent deployment, including evaluation and red-team environments | Decision Boundary Matrix with irreversible-action classes; Agency Envelope Validator before every action; authority expansion requires human | CRITICAL — Replit and PocketOS resulted directly from the absence of this control | AML.M0037, AML.M0026 |
| **UC-CTRL-02** | Implement a tiered infrastructure-level response independent of the agent's context | T1 Stop → T2 Contain (revoke JIT, quarantine, snapshot; < 30 s) → T3 Recover (envelope re-asserted) → T4 Terminate; drilled | CRITICAL — In-context stop mechanisms fail (OpenClaw stop-failure) | — |
| **UC-CTRL-03** | Implement human oversight checkpoints for action categories requiring authorization | HITL workflow integrated with the Envelope Validator; SLAs; default-deny on timeout; Sigma detection (Section 16.2) | HIGH — Human oversight must be an enforcement gate, not an optional UI element | AML.M0029 |
| **UC-SEC-01** | Unique cryptographic identity per agent; no shared credentials; workload credential hygiene | Per-agent identity (OAuth/OIDC/SPIFFE); JIT per invocation; IMDS blocked; per-cluster credentials; no secrets in env of untrusted-input parsers | CRITICAL — Identity is not authority; shared/over-scoped credentials drove AiTM, PocketOS and OpenAI/HF | AML.M0027, AML.M0026 |
| **UC-SEC-02** | Enforce network micro-segmentation | Egress via controlled proxy with allow-list; inter-agent comms only via orchestration channel | HIGH — Uncontrolled network enables exfiltration, AiTM infection and sandbox escape to internet | AML.M0032 |
| **UC-SEC-03** | Capture the complete execution trajectory in an immutable, off-agent log store | Reasoning steps, tool calls, memory ops, state transitions, inter-agent messages; append-only; HMAC-signed; OTel trace correlation | CRITICAL — Only post-hoc detection mechanism for trajectory manipulation | AML.M0024 |
| **UC-SEC-04** | Behavioral baselines and continuous anomaly detection | Statistical and graph-based baselines (Drift Score); anomaly scoring; alerts routed via UC-SEC-07 | HIGH — Primary mechanism for ASI10 without known-bad signatures | AML.M0038 |
| **UC-SEC-05** | Circuit breakers on all inter-agent communication paths | Per-path breakers; quarantine protocol; downstream notification before severing | HIGH — Prevents ASI08 cascades | AML.M0036 |
| **UC-SEC-06** | Output data loss prevention and exfiltration detection | DLP for PII/credentials/semantic exfiltration; steganography detection; entropy monitoring | CRITICAL — Terminal gate for the exfiltration consequence class (ASI01, ASI03, ASI06; ASI09 when the user trusts the output) | AML.M0033 |
| **UC-SEC-07** *(v1.2)* | Bind every agent-behavior detection to an owner, an escalation path and an automatic containment trigger | Alert routing per agent class; auto-pause thresholds in Agency Envelope Policy; MTTD/MTTC in Agent Risk Register; quarterly drill | HIGH — Signals that do not escalate are not controls (OpenAI/HF) | AML.M0038, AML.M0024 |

---

## References

### Standards & Frameworks

- [OWASP Top 10 for Agentic Applications 2026](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/) — official taxonomy published 10 December 2025
- [OWASP Top 10 for LLM Applications 2026](https://genai.owasp.org/resource/owasp-genai-llm-top-10-2026/) — published 3 August 2026; Appendix A maps LLM risks onto the agentic Top 10
- [OWASP Agent Control Standard (ACS)](https://genai.owasp.org/resource/agent-control-standard-acs/) — donated to the OWASP GenAI Security Project, September 2026
- [OWASP AI Exchange — Agentic AI Threats and Mitigations](https://genai.owasp.org/resource/agentic-ai-threats-and-mitigations/)
- [OWASP State of Agentic AI Security and Governance v2.01](https://genai.owasp.org/download/50592/) — June 2026
- [OWASP Practical Guide for Secure MCP Server Development](https://genai.owasp.org/resource/a-practical-guide-for-secure-mcp-server-development/) — February 2026
- [OWASP GenAI Exploit Round-up Report Q1 2026](https://genai.owasp.org/2026/04/14/owasp-genai-exploit-round-up-report-q1-2026/) — documents the OpenClaw stop-command (11.8) and LiteLLM/Trivy (11.9) incidents
- [CSA MAESTRO — Agentic AI Threat Modeling Framework](https://cloudsecurityalliance.org/blog/2025/02/06/agentic-ai-threat-modeling-framework-maestro) — Ken Huang, February 2025
- [CSA MAESTRO GitHub Repository](https://github.com/CloudSecurityAlliance/MAESTRO)
- [CSA — Applying MAESTRO in CI/CD pipelines (Feb 2026)](https://cloudsecurityalliance.org/blog/2026/02/11/applying-maestro-to-real-world-agentic-ai-threat-models-from-framework-to-ci-cd-pipeline)
- [CSA — Agentic AI Identity & Access Management](https://cloudsecurityalliance.org/artifacts/agentic-ai-identity-and-access-management-a-new-approach)
- [MITRE ATLAS](https://atlas.mitre.org/) · [atlas-data releases (v2026.08 pinned)](https://github.com/mitre-atlas/atlas-data/releases)
- [MITRE ATT&CK v19.2](https://attack.mitre.org/)
- [AIUC-1 changelog](https://www.aiuc-1.com/changelog) — Q2-2026 (15 Apr), Q3-2026 (15 Jul), next 15 Oct 2026. UC-\* identifiers in this document are TREASURE's internal convention, not AIUC-1 codes.
- [Model Context Protocol specification 2026-07-28 — changelog](https://modelcontextprotocol.io/specification/2026-07-28/changelog)
- [NIST — AI Agent Standards Initiative (CAISI), 17 Feb 2026](https://www.nist.gov/news-events/news/2026/02/announcing-ai-agent-standards-initiative-interoperable-and-secure)
- [NIST AI RMF 1.0](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework) · [NIST AI 600-1](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf)
- [ISO/IEC 42001:2023 — AI Management Systems](https://www.iso.org/standard/81230.html)
- EU AI Act — Regulation (EU) 2024/1689, as amended by Regulation (EU) 2026/1744 (Digital Omnibus on AI; OJ 24 July 2026; in force 27 July 2026)

### Research Papers

- [MemoryGraft — arXiv:2512.16962](https://arxiv.org/abs/2512.16962)
- [AgentPoison — arXiv:2407.12784](https://arxiv.org/abs/2407.12784)
- [AiTM — arXiv:2502.14847 (ACL 2025)](https://arxiv.org/abs/2502.14847)
- [Prompt Infection — arXiv:2410.07283](https://arxiv.org/abs/2410.07283)
- [Agent Security Bench — arXiv:2410.02644](https://arxiv.org/abs/2410.02644)
- MINJA — NeurIPS 2025 (proceedings.neurips.cc)
- [The Attack and Defense Landscape of Agentic AI — arXiv:2603.11088](https://arxiv.org/abs/2603.11088)
- [Agentic AI Security: Threats, Defenses, Evaluation — arXiv:2510.23883](https://arxiv.org/abs/2510.23883)

### Incidents & CVEs

- EchoLeak CVE-2025-32711 — [Aim Security](https://www.aim.security/lp/echoleak) · [MSRC](https://msrc.microsoft.com/update-guide/vulnerability/CVE-2025-32711)
- Gemini Memory Attack — [Rehberger, Feb 2025](https://embracethered.com/blog/posts/2024/google-gemini-persistent-memory-attack/) · GeminiJack — [Noma Security, Jun 2025](https://www.noma.ai/blog/geminijack-how-we-discovered-a-zero-day-that-could-compromise-google-workspace-agents)
- Atlassian Rovo — [Community report](https://community.atlassian.com/forums/Atlassian-Platform-Community/Rovo-Agent-Data-Exfiltration-via-Indirect-Prompt-Injection/ba-p/3001198)
- Replit Vibe Coding Meltdown (AIID #1152) — [Wired, July 2025](https://www.wired.com/story/replit-ai-code-database-deletion/)
- OpenClaw CVE-2026-25253 — [NVD](https://nvd.nist.gov/vuln/detail/CVE-2026-25253) · [SonicWall](https://www.sonicwall.com/blog/openclaw-auth-token-theft-leading-to-rce-cve-2026-25253) · [runZero](https://www.runzero.com/blog/openclaw/)
- OpenClaw stop-failure — [TechCrunch, 23 Feb 2026](https://techcrunch.com/2026/02/23/a-meta-ai-security-researcher-said-an-openclaw-agent-ran-amok-on-her-inbox/)
- LiteLLM / Trivy — [OWASP GenAI Exploit Round-up Q1 2026](https://genai.owasp.org/2026/04/14/owasp-genai-exploit-round-up-report-q1-2026/)
- ClawHub malicious skills — [Unit 42](https://unit42.paloaltonetworks.com/openclaw-ai-supply-chain-risk/) · [CNCERT advisory](https://www.cert.org.cn/publish/main/11/2026/20260312144519429724511/20260312144519429724511_.html)
- PocketOS — [The Register](https://www.theregister.com/software/2026/04/27/cursor-opus-agent-snuffs-out-startups-production-database/5224442) · [DEV postmortem](https://dev.to/axrisi/railway-database-deleted-by-an-ai-agent-the-pocketos-postmortem-2p7p)
- Mastra npm / Sapphire Sleet — [Microsoft Security Blog](https://www.microsoft.com/en-us/security/blog/2026/06/17/postinstall-payload-inside-mastra-npm-supply-chain-compromise/)
- OpenAI evaluation agents / Hugging Face — [Hugging Face timeline](https://huggingface.co/blog/agent-intrusion-technical-timeline) · [OpenAI disclosure](https://openai.com/index/hugging-face-model-evaluation-security-incident/) · [OpenAI report](https://openai.com/index/hugging-face-incident-and-the-road-ahead/)

---

## License

**CC0 1.0 Universal — Public Domain Dedication**

To the extent possible under law, Roger Sanz González has waived all copyright and related rights to this specific layout and textual implementation of the TREASURE AI Security Framework. You are free to copy, modify, distribute, and build upon this text, even for commercial purposes, without seeking prior permission or providing mandatory attribution.

→ [View CC0 1.0 Legal Code](https://creativecommons.org/publicdomain/zero/1.0/)

Contributions and feedback: [roger.sanz@owasp.org](mailto:roger.sanz@owasp.org)

---

*TREASURE Framework v1.2 · Roger Sanz González · Plain Concepts · OWASP AI Exchange · 29 September 2026*


---

*TREASURE Framework v1.1 (same-day corrections addendum applied) · Roger Sanz González · Plain Concepts · OWASP AI Exchange · 3 July 2026*
