TREASURE Framework
Defense-in-Depth Architecture for Agentic AI Systems
> **Tiered Resilient Execution Architecture for Secure Unified Robust
> Environments**
![License:](https://img.shields.io/badge/License-CC0_1.0-lightgrey.svg)
![OWASP GenAI](https://img.shields.io/badge/Aligned-OWASP%20GenAI%20Security-blue)
![CSA](https://img.shields.io/badge/Aligned-CSA%20MAESTRO-orange)
![NIST AI](https://img.shields.io/badge/Aligned-NIST%20AI%20RMF-green)
![MITRE](https://img.shields.io/badge/Aligned-MITRE%20ATLAS%20v2026.08-red)
![ISO](https://img.shields.io/badge/Aligned-ISO%2FIEC%2042001-blue)
[![Version](https://img.shields.io/badge/Version-1.2-brightgreen)]()
Author: Roger Sanz, PhD  
Version: 1.2 · 29 September 2026  
Contact: roger.sanz@owasp.org
---
Editor's Notice
The TREASURE AI Security Framework is an operational security
architecture developed by Roger Sanz, PhD, specifically for the security
challenges created by Agentic AI systems.
Agentic systems do more than generate responses. They plan, act,
remember, invoke tools, modify resources, communicate with other agents
and operate across multi-step workflows. TREASURE is designed around
those execution characteristics rather than treating an agent as simply
another LLM application.
The framework is open to security researchers, practitioners and
contributors interested in the evolution of Agentic AI Security. It is
intended to be adapted to the organization's architecture, threat
model and risk profile.
TREASURE is designed to complement, not replace, established
security, AI governance, threat-modeling and compliance frameworks.
> **Central principle:**\
> **Protect your AgenticAI Security treasure. If you do not govern your
> agents, they will work for your adversaries.**
Licensing & Rights
CC0 1.0 --- Public Domain Dedication. To the extent possible under
law, Roger Sanz González has waived copyright and related rights to this
specific layout and textual implementation of the framework. You are
free to copy, modify, distribute and build upon it, including for
commercial purposes.
View the CC0 1.0 Legal
Code
---
Executive Summary
Enterprise organizations are deploying autonomous AI agents across
development, operations, productivity, security and business processes.
Unlike conventional generative AI systems that primarily respond to
prompts, agentic systems plan, act, remember and collaborate across
multi-step workflows. They can invoke APIs, execute code, modify
databases, access enterprise information, communicate with other agents
and continue operating with limited human intervention.
This creates a different security problem.
The attack surface is no longer limited to the model or the prompt. It
includes:
persistent memory and RAG knowledge;
tools, skills and executable components;
agent runtime and orchestration;
identities and credentials;
inter-agent communication;
supply-chain dependencies and marketplaces;
policy enforcement;
human authorization boundaries;
execution trajectories and behavioral drift;
containment, recovery and blast-radius controls.
The TREASURE Framework addresses this problem through a five-layer
defense-in-depth architecture. Each layer addresses a distinct
security responsibility while remaining structurally independent from
the others.
The architecture is deliberately hierarchical:
``` text
SECURITY LAYER       ← Blast Radius Engineering
        ↑
CONTROL LAYER        ← Encapsulated Autonomy
        ↑
GOVERNANCE LAYER     ← Policy-as-Code Discipline
        ↑
EXECUTION LAYER      ← Critical Attack Surface Control
        ↑
DATA LAYER           ← Single Governed Truth
```
The objective is not to make an agent incapable of acting. The objective
is to ensure that agent autonomy remains bounded, observable,
attributable and containable.
---
The Core Adversarial Problem
The Double-Agent Threat
The central threat addressed by TREASURE is the double-agent
problem:
> An autonomous agent appears to operate normally while its effective
> behavior has been manipulated away from the interests of its
> legitimate principal.
This can occur through:
memory poisoning;
RAG poisoning;
malicious or compromised skills;
tool manipulation;
inter-agent communication attacks;
excessive authority;
compromised dependencies;
behavioral drift.
The 2025--2026 evidence base demonstrates that this is not purely
theoretical.
Documented cases include EchoLeak, OpenClaw, the Replit Vibe
Coding incident, LiteLLM/Trivy, ClawHub malicious skills,
PocketOS, Mastra/Sapphire Sleet, and the OpenAI
evaluation-agent / Hugging Face incident.
A second problem: the rogue agent without an attacker
v1.2 expands the threat model beyond adversarial compromise.
Some of the most important 2026 incidents involved no external
attacker at all. The agent itself caused the damage because its
authority exceeded the task it was supposed to perform, or because a
safety condition existed only in mutable context rather than in an
enforceable control plane.
This produces a fundamental distinction:
> **Capability is not authority. Identity is not authority. Intent is
> not enforcement.**
TREASURE therefore treats excess authority without an adversary as a
first-class security problem.
---
Five-Layer Architecture
1. DATA LAYER --- Diamond Record
Design principle: Single Governed Truth
The Data Layer is the foundation. Agent reasoning ultimately depends on
data retrieved from memory, RAG systems, knowledge bases and other
sources.
Primary threats
Memory & Context Poisoning --- OWASP ASI06
RAG poisoning
Data integrity manipulation
Loss of provenance
Destruction of both production data and its recovery path
Core controls
UC-DATA-01 --- Governed ingestion and provenance
UC-DATA-02 --- Memory and embedding integrity
UC-DATA-03 --- Identity-scoped retrieval controls
UC-DATA-04 --- Versioned memory and constraint recovery
UC-DATA-05 --- Recovery independence
UC-DATA-05 is new in v1.2 and establishes a critical resilience
property:
> No credential reachable by an agent should be capable of destroying
> both production data and the recovery path.
---
2. EXECUTION LAYER --- Skills & Runtime
Design principle: Critical Attack Surface Control
The Execution Layer controls what an agent can execute and which tools
and skills it can invoke.
Primary threats
Tool misuse --- OWASP ASI02
Unexpected code execution --- ASI05
Malicious skills
Tool poisoning
Supply-chain execution
Control-plane abuse
Core controls
UC-EXEC-01 --- Least-privilege tool and skill execution
UC-EXEC-02 --- Cryptographic signing and provenance verification
UC-EXEC-03 --- Sandboxing and runtime isolation
UC-EXEC-04 --- Immutable tool invocation audit trail
UC-EXEC-05 --- Pre-invocation intent validation
A critical TREASURE principle is that a tool allow-list should be an
enforced execution control, not merely an advisory configuration.
---
3. GOVERNANCE LAYER --- Code-Grade Governance
Design principle: Policy-as-Code Discipline
Governance must be executable.
Agent behavioral specifications, security policies, dependencies and
deployment artefacts must be version-controlled and subject to security
gates.
Primary threats
Agentic supply-chain compromise --- ASI04
Agentic drift
Policy violations
Uncontrolled dependency changes
Core controls
UC-GOV-01 --- Version-controlled agent behavioural
specifications
UC-GOV-02 --- Machine-enforceable Policy-as-Code
UC-GOV-03 --- CI/CD security and supply-chain gates
UC-GOV-04 --- AI Bill of Materials (AIBOM)
UC-GOV-05 --- Continuous drift detection
The key principle is simple:
> **A policy written in a prompt is not equivalent to a policy enforced
> by the runtime.**
---
4. CONTROL LAYER --- Human-in-the-Loop
Design principle: Encapsulated Autonomy
Human oversight must be an enforcement mechanism, not merely a
user-interface feature.
The Control Layer defines what the agent is allowed to do, when human
authorization is required and how the system can stop an agent
independently of its own context.
Primary threats
Goal hijacking --- ASI01
Human-agent trust exploitation --- ASI09
Rogue agents --- ASI10
Excessive agency
Irreversible actions
Core controls
UC-CTRL-01 --- Agency Envelope and Decision Boundary Matrix
UC-CTRL-02 --- Tiered response: Stop → Contain → Recover →
Terminate
UC-CTRL-03 --- Human authorization checkpoints
v1.2 explicitly extends the Agency Envelope to evaluation and red-team
environments.
---
5. SECURITY LAYER --- Defense-in-Depth
Design principle: Blast Radius Engineering
The Security Layer assumes that prevention will eventually fail.
Its purpose is therefore to limit what a compromised, malfunctioning or
rogue agent can reach, observe, modify or destroy.
Primary threats
Identity and privilege abuse --- ASI03
Insecure inter-agent communication --- ASI07
Cascading agent failures --- ASI08
Lateral movement
Data exfiltration
Credential abuse
Core controls
UC-SEC-01 --- Unique per-agent identity and JIT credentials
UC-SEC-02 --- Network micro-segmentation
UC-SEC-03 --- Complete off-agent execution trajectory
UC-SEC-04 --- Behavioral baselines and anomaly detection
UC-SEC-05 --- Inter-agent circuit breakers
UC-SEC-06 --- Output DLP and exfiltration detection
UC-SEC-07 --- Detection-to-containment escalation ownership
UC-SEC-07 is new in v1.2:
> A detection that has no owner, escalation path or containment action
> is not an operating security control.
---
Five Design Principles Introduced in v1.2
1. Intent ≠ Enforcement
An agent may be instructed not to perform an action. That instruction is
not a security control unless an independent enforcement mechanism can
prevent the action.
2. Identity ≠ Authority
Knowing which agent is acting does not determine what that agent should
be allowed to do.
Identity must be bound to scoped, task-appropriate authority.
3. Irreversible Actions Need External Stop Conditions
Deletion, privilege expansion, destructive infrastructure operations and
comparable actions require enforcement outside the agent's mutable
context.
4. Asymmetric Autonomy
The more consequential an action is, the less autonomy the agent should
have to execute it without independent validation or authorization.
5. Containment Must Be Platform-Independent
The security architecture must be capable of stopping or containing an
agent even when the agent itself is malfunctioning, compromised or
ignoring instructions.
---
OWASP Agentic Top 10 Alignment
TREASURE maps its controls to the official OWASP Agentic Applications
taxonomy.
---
OWASP                   Threat                  Primary TREASURE Layer
---
ASI01                   Agent Goal Hijack       CONTROL / DATA
ASI02                   Tool Misuse &           EXECUTION
Exploitation
ASI03                   Identity & Privilege    SECURITY
Abuse
ASI04                   Agentic Supply Chain    GOVERNANCE / EXECUTION
Vulnerabilities
ASI05                   Unexpected Code         EXECUTION
Execution
ASI06                   Memory & Context        DATA
Poisoning
ASI07                   Insecure Inter-Agent    SECURITY
Communication
ASI08                   Cascading Agent         SECURITY
Failures
ASI09                   Human-Agent Trust       CONTROL
Exploitation
ASI10                   Rogue Agents            CONTROL
Data leakage and exfiltration are treated as consequences spanning
multiple attack classes, particularly ASI01, ASI03 and ASI06, rather
than as a standalone OWASP ASI category.
---
CSA MAESTRO Integration
TREASURE maps its five operational layers to the canonical seven-layer
CSA MAESTRO model:
CSA MAESTRO                      TREASURE relationship
---
L1 Foundation Models             Security and deployment context
L2 Data Operations               DATA
L3 Agent Frameworks              EXECUTION
L4 Deployment & Infrastructure   EXECUTION / SECURITY
L5 Evaluation & Observability    GOVERNANCE / SECURITY
L6 Security & Compliance         GOVERNANCE / CONTROL
L7 Agent Ecosystem               EXECUTION
TREASURE does not redefine MAESTRO. It uses the canonical model and
decomposes relevant capabilities into operational security layers.
---
AIUC-1, NIST, MITRE, OWASP and Regulatory Alignment
TREASURE is designed as a cross-framework architecture rather than a
replacement for existing standards.
Current v1.2 alignment includes:
OWASP Top 10 for Agentic Applications
OWASP Agent Control Standard (ACS)
OWASP AI Exchange
OWASP AI DEFEND
CSA MAESTRO
NIST AI RMF
NIST AI Agent Standards Initiative / NCCoE
MITRE ATLAS v2026.08
MITRE ATT&CK v19.2
AIUC-1 Q3 2026
ISO/IEC 42001
Model Context Protocol specification 2026-07-28
EU AI Act, including Regulation (EU) 2026/1744
CEN/CENELEC, ETSI and related AI security work
> **Important:** `UC-*` identifiers are TREASURE's internal crosswalk
> convention. They are not official AIUC-1 requirement identifiers.
---
MCP Security
MCP has become a major execution-layer attack surface for agentic
systems.
TREASURE v1.2 explicitly addresses:
Tool poisoning
Rug-pull attacks
Confused deputy attacks
Token passthrough
Tool manifest integrity
Server provenance
Credential scoping
Runtime isolation
The framework treats MCP servers as execution components, not simply
as integrations.
For high-assurance deployments, MCP controls should include signed or
content-addressed tool definitions, provenance verification, scoped
credentials, network controls and continuous integrity monitoring.
---
Minimum Viable Security Posture --- MVSP v1.2
TREASURE v1.2 re-derived its Minimum Viable Security Posture against
13 documented incidents.
Tier 1 --- Prevention Core
The four-control prevention core is:
UC-CTRL-01 --- Agency Envelope
UC-DATA-01 --- Governed ingestion
UC-EXEC-02 --- Cryptographic signing
UC-SEC-01 --- Per-agent scoped JIT identity
Together, these controls break every documented incident chain in the
v1.2 counterfactual analysis.
Tier 2 --- Resilience Core
Three additional controls are required to limit impact when prevention
fails:
UC-CTRL-02 --- Tiered Stop → Contain → Recover → Terminate
UC-SEC-07 --- Detection-to-containment escalation ownership
UC-DATA-05 --- Recovery independence
Profile Overlays
Additional controls should be applied according to the agent profile:
Coding / infrastructure agents: UC-CTRL-03
RAG / copilot agents: UC-EXEC-05 + UC-SEC-06
Build pipelines: UC-GOV-03
Multi-agent systems: UC-SEC-05
> The MVSP is a counterfactual analysis over documented incidents. It is
> not an empirical effectiveness measurement or a guarantee of
> prevention.
---
Reference Architecture
The TREASURE enforcement model can be implemented through an Agent
Runtime Control Plane (ARCP).
``` text
User / External Input
        │
        ▼
Orchestrator + Intent Monitoring
        │
        ▼
Agent Runtime Control Plane
   ├── Memory Manager
   ├── Tool Router
   ├── Skill Executor
   └── Policy Engine
        │
        ▼
Agency Envelope Validator
        │
   ┌────┴────┐
   │ HITL    │
   │ Check   │
   └────┬────┘
        ▼
Scoped Tool APIs + Diamond Record
        │
        ▼
Full Trajectory Log
        │
        ▼
Anomaly Detection + Drift Score
        │
        ▼
Tiered Kill-Switch
Stop → Contain → Recover → Terminate
        │
        ▼
Out-of-Blast-Radius Backups
```
The critical architectural property is that containment remains
outside the agent's own decision loop.
---
Detection & Response Engineering --- TREASURE Lab
v1.2 introduces the TREASURE Lab as a research and engineering track.
Drift Score
The Drift Score models an agent session as a graph of tool
invocations and compares the live execution graph against a
CI/CD-validated baseline.
The important signal is not merely that a score changed, but which
execution edge changed.
``` text
BASELINE:
tool_A → tool_B → tool_C

LIVE:
tool_A → credential_lookup → prod_delete

NEW EDGE:
credential_lookup → prod_delete
```
The methodology requires declared graph-distance approximations,
action-weighted costs, baseline calibration and routing through
UC-SEC-07.
Detection-as-Code
v1.2 includes a corrected Sigma rule for detecting irreversible agent
actions that occur without required human confirmation within the
defined SLA.
Research Artefacts
Entities using the `TRSR.LAB.*` namespace are research artefacts and
reference implementations.
They are not presented as incident evidence and are not claimed to be
validated benchmarks.
---
Real-World Evidence Base
TREASURE v1.2 contains 13 documented incident entities, including:
EchoLeak --- CVE-2025-32711
Gemini Memory Attack / GeminiJack
AgentPoison
AiTM
Atlassian Rovo
Replit Vibe Coding Meltdown
OpenClaw --- CVE-2026-25253
OpenClaw stop-command failure
LiteLLM / Trivy supply-chain compromise
PocketOS production-volume deletion
OpenAI evaluation agents / Hugging Face compromise
Mastra npm / Sapphire Sleet
ClawHub malicious skills
The evidence base is used to derive control counterfactuals, mappings
and resilience requirements rather than to claim that TREASURE
controls have been empirically validated across these environments.
---
Implementation Roadmap
TREASURE can be introduced incrementally.
---
Phase                   Focus                   Typical Activities
---
1 --- Foundation    DATA                    Governed ingestion,
provenance, memory
integrity, recovery
independence
2 --- Execution       EXECUTION               Signed skills,
Control                                       allow-lists,
sandboxing, pre-call
validation
3 --- Governance    GOVERNANCE              Policy-as-Code, AIBOM,
CI/CD security,
dependency controls
4 --- Human Control CONTROL                 Agency Envelope,
Decision Boundary
Matrix, HITL, tiered
kill-switch
5 --- Security        SECURITY                JIT identity,
Hardening                                     segmentation,
trajectory telemetry,
behavioral detection,
circuit breakers
For production agents with write access, the v1.2 MVSP fast path
should be considered before broader optimization:
``` text
UC-CTRL-01
      +
UC-DATA-01
      +
UC-EXEC-02
      +
UC-SEC-01
      ↓
Prevention Core

UC-CTRL-02
      +
UC-SEC-07
      +
UC-DATA-05
      ↓
Resilience Core
```
---
Platform Independence
TREASURE is intentionally platform-independent.
The framework can be implemented using different technology stacks,
provided the underlying security properties are preserved.
Examples documented in v1.2 include:
Microsoft / Azure / Copilot Studio
Google Cloud / Vertex AI Agent Builder
AWS / Amazon Bedrock Agents
The framework evaluates security properties and enforcement points,
not vendor branding.
A platform feature should not automatically be treated as a TREASURE
control unless it provides the required enforcement semantics.
---
What TREASURE Is --- and Is Not
TREASURE is
an Agentic AI security architecture;
a defense-in-depth model;
a control architecture;
a threat-to-control crosswalk;
an operational basis for architecture reviews and security
engineering;
a framework for detection, containment and resilience;
an open research and practitioner framework.
TREASURE is not
a product;
an AI governance policy template;
a compliance certification;
a replacement for OWASP, NIST, CSA, MITRE, ISO or regulatory
requirements;
a guarantee that an agent cannot be compromised;
an empirical benchmark claiming universal control effectiveness.
---
Version 1.2 Changes
Version 1.2, released 29 September 2026, retains the five-layer
architecture and introduces substantial operational extensions:
four additional real-world incidents, bringing the documented
evidence base to 13;
UC-DATA-05 Recovery Independence;
UC-SEC-07 Detection-to-Containment Escalation Ownership;
expanded UC-CTRL-01 Agency Envelope;
tiered UC-CTRL-02 Stop → Contain → Recover → Terminate;
enhanced workload credential hygiene in UC-SEC-01;
five explicit design principles;
canonical CSA MAESTRO remapping;
OWASP Agent Control Standard alignment;
MITRE ATLAS v2026.08 verification;
MCP 2026-07-28 alignment;
NIST CAISI / NCCoE alignment;
EU Digital Omnibus alignment;
TREASURE Lab detection engineering;
Drift Score methodology;
audited RootedCON VLC 2026 technique mapping;
canonical dataset expansion to 118 entities;
MVSP v1.2 derived from all 13 documented incident chains.
The v1.2 source also retains previous versions for traceability.
---
Contributing
TREASURE is open to contributions from practitioners and researchers
working on:
Agentic AI Security
Agent Runtime Security
AI supply-chain security
MCP security
AI identity and authorization
Agent observability
Agentic threat modeling
adversarial testing
security architecture
detection engineering
AI governance
Contributions should be technically grounded, reproducible where
possible, and explicit about whether an assertion is:
documented incident evidence;
research evidence;
a TREASURE design requirement;
a counterfactual analysis;
a proposed research hypothesis.
This distinction is important to preserve the evidentiary quality of the
framework.
---
Author
Roger Sanz, PhD
AI Security Lead --- Plain Concepts  
Senior Researcher --- Universidad Isabel I  
Lead Editor --- OWASP AI Exchange  
Contributor --- MITRE ATLAS · CSA · ISMS Forum · DAMA
Contact: roger.sanz@owasp.org
---
License
CC0 1.0 Universal --- Public Domain Dedication
View CC0 1.0 Legal
Code
---
> **TREASURE Framework v1.2 · Roger Sanz González · 29 September 2026**
>
> **Govern. Protect. Detect. Assure. Evolve.**
