       
 TREASURE Framework — FAQ
Version 1.2 | 29 September 2026
TREASURE — Tiered Resilient Execution Architecture for Secure Unified Robust Environments  
Defense-in-Depth Architecture for Agentic AI Systems
---
1. What is the TREASURE Framework?
TREASURE is a defense-in-depth security architecture designed for Agentic AI systems that plan, act, remember, use tools and collaborate across multi-step workflows. It organizes security controls into five independent layers.
2. What does TREASURE stand for?
Tiered Resilient Execution Architecture for Secure Unified Robust Environments.
3. Why was TREASURE created?
Agentic AI introduces persistent memory, tool execution, autonomous decision-making, inter-agent communication and long-running workflows. Traditional perimeter controls and prompt/output guardrails do not cover the complete execution trajectory.
4. Who is TREASURE for?
TREASURE is intended for AI Security Engineers, CISOs, security architects, developers, red teams, researchers and teams responsible for deploying or governing Agentic AI systems.
5. Is TREASURE a product?
No. TREASURE is an open security architecture and implementation framework. It is not a product, policy template or checklist.
6. Does TREASURE replace other security frameworks?
No. TREASURE is an implementation overlay. It is designed to complement frameworks and standards including OWASP Agentic Applications, CSA MAESTRO, NIST AI RMF, AIUC-1, ISO/IEC 42001 and MITRE ATLAS.
7. What is the central threat addressed by TREASURE?
The primary adversarial problem is the Double-Agent threat: an autonomous agent appears to operate normally while its effective behaviour has been manipulated against the interests of its legitimate principals.
8. What is the Double-Agent threat based on?
The v1.2 threat model focuses particularly on memory poisoning, RAG poisoning and manipulation of inter-agent communication. These mechanisms can corrupt the agent's effective context or objective while leaving normal-looking interactions visible to users.
9. Does TREASURE address rogue agents?
Yes. v1.2 explicitly expands the model to include the unattacked rogue agent: an agent can cause serious harm without an external attacker when its authority exceeds what its task requires. PocketOS and the OpenAI/Hugging Face evaluation-agent incident are used as evidence for this class.
10. What are the primary attack vectors covered by TREASURE?
The core vectors are Memory Poisoning, RAG Poisoning, Inter-Agent Communication Poisoning, and, in v1.2, Excess Authority without Adversary.
---
11. What are the five TREASURE layers?
Data Layer — Diamond Record
Execution Layer — Skills & Runtime
Governance Layer — Code-Grade Governance
Control Layer — Human-in-the-Loop
Security Layer — Defense-in-Depth
They form a dependency hierarchy while remaining structurally independent so that failure of one layer does not automatically become system-wide failure.
12. What is the Data Layer?
The Data Layer establishes a Single Governed Truth for agent memory, retrieval and persistent state. It addresses provenance, memory integrity, identity-scoped retrieval, versioned recovery and recovery independence.
13. What is the Diamond Record?
The Diamond Record is the TREASURE concept for governed agent data and memory. It provides a controlled source of truth with provenance, integrity, access constraints, versioning and recovery properties.
14. What is the Execution Layer?
The Execution Layer controls the agent's skills, tools and runtime. Its design principle is Critical Attack Surface Control, covering least privilege, signing, sandboxing, invocation auditing and pre-invocation validation.
15. What is the Governance Layer?
The Governance Layer applies Code-Grade Governance. It turns agent behaviour, security requirements and supply-chain constraints into version-controlled and machine-enforceable policies.
16. What is the Control Layer?
The Control Layer implements Encapsulated Autonomy. It defines where an agent may act autonomously, where human authorization is required and how the system stops, contains, recovers or terminates an unsafe execution.
17. What is the Security Layer?
The Security Layer provides Blast Radius Engineering. It covers workload identity, network segmentation, trajectory telemetry, behavioural detection, inter-agent circuit breakers and output exfiltration controls.
18. Why are the layers independent?
Agentic failures can cross technical boundaries. TREASURE therefore avoids relying on a single control point or on the agent itself to enforce its own restrictions. Independent layers provide additional prevention, detection, containment and recovery paths.
---
19. What is ARCP?
ARCP — Agent Runtime Control Plane is the external enforcement architecture described by TREASURE. It contains components such as the Memory Manager, Tool Router, Skill Executor and Policy Engine and sits outside the agent's reasoning loop.
20. Why is ARCP outside the agent's reasoning loop?
Because an agent cannot be the sole enforcement point for restrictions that apply to its own behaviour. TREASURE distinguishes between what the agent intends and what the surrounding runtime actually permits.
21. What is the Agency Envelope?
The Agency Envelope is the enforceable boundary defining what an agent may do autonomously. Actions outside that boundary can require human authorization or independent containment.
22. What is the Decision Boundary Matrix?
It defines classes of agent actions and their required authorization or control level. It is particularly important for irreversible or high-impact operations.
23. Why does TREASURE separate identity from authority?
Because authenticating an agent does not determine what that agent is allowed to do. TREASURE requires identity and authorization to be governed separately, with credentials scoped to the minimum required task or tool invocation.
24. Why does TREASURE require external stop conditions?
An agent may misinterpret its objective, lose a restriction from context or behave outside its intended boundary. Irreversible actions therefore require an enforcement condition outside the agent, such as a human authorization gate or independent runtime control.
25. What does “Intent is not enforcement” mean?
Instructions, policies and restrictions stored in an agent's context express intent. They are not security controls unless an external runtime or infrastructure mechanism actually enforces them.
26. What does “Asymmetric autonomy” mean?
Containment must be able to act autonomously, while authority expansion and irreversible actions require stronger authorization. A security response should not wait for a human who has not yet responded.
27. Why must containment be platform-independent?
Detection and containment logic should be defined against security requirements rather than tied to one vendor. TREASURE allows platform-specific adapters while keeping the underlying security semantics consistent.
---
28. What is the TREASURE MVSP?
MVSP — Minimum Viable Security Posture is the minimum control set derived in v1.2 from counterfactual analysis of 13 documented incident chains.
29. What is the MVSP prevention core?
The Tier 1 prevention core contains four controls:
UC-CTRL-01 — Agency Envelope
UC-DATA-01 — Governed ingestion
UC-EXEC-02 — Cryptographic signing
UC-SEC-01 — Per-agent scoped JIT identity
30. What is the MVSP resilience core?
Tier 2 contains:
UC-CTRL-02 — Tiered response: Stop → Contain → Recover → Terminate
UC-SEC-07 — Detection-to-Containment Escalation Ownership
UC-DATA-05 — Recovery Independence
These controls limit impact when prevention fails.
31. Does the MVSP guarantee security?
No. The v1.2 MVSP result is a counterfactual analysis over documented incidents, not an empirical effectiveness benchmark or a security guarantee.
32. Does every Agentic AI system need exactly the same controls?
No. TREASURE defines a common foundation and profile overlays. For example, coding and infrastructure agents add UC-CTRL-03; RAG/copilot systems add UC-EXEC-05 and UC-SEC-06; build pipelines add UC-GOV-03; multi-agent systems add UC-SEC-05.
33. Can TREASURE be implemented incrementally?
Yes. The implementation roadmap progresses from data governance and provenance, through execution controls and governance, to human control and security hardening.
---
34. How does TREASURE address MCP?
TREASURE treats Model Context Protocol (MCP) as a significant Execution Layer attack surface. It addresses tool permissions, OAuth 2.1 delegation, credential scoping, sandboxing, input/output validation, invocation auditing and tool provenance.
35. Does MCP natively provide signed tool manifests?
Not in the MCP 2026-07-28 specification. TREASURE therefore treats cryptographic tool-manifest signing as custom infrastructure when implementing UC-EXEC-02 for MCP, with compensating controls such as curated registries, static approval and behavioural monitoring.
36. How does TREASURE address supply-chain attacks?
The Execution and Governance layers combine cryptographic signing, provenance verification, AIBOM controls, dependency and CI/CD gates, curated registries and runtime restrictions.
37. How does TREASURE address multi-agent systems?
The Security Layer applies zero-trust principles to inter-agent communication, including per-agent identity, scoped authority, message integrity and inter-agent circuit breakers. TREASURE also maps these controls to the OWASP ASI07 and ASI08 threat classes where applicable.
38. How does TREASURE address data exfiltration?
Data exfiltration is treated as a consequence that can arise from multiple agentic attack classes rather than as a standalone OWASP Agentic Top 10 entry. TREASURE uses identity-scoped retrieval, trajectory monitoring, output DLP and execution controls to reduce this risk.
---
39. How does TREASURE map to OWASP?
TREASURE maps its layers and controls to the official OWASP Top 10 for Agentic Applications taxonomy. The v1.2 baseline uses the December 2025 numbering, including ASI04 Agentic Supply Chain Vulnerabilities, ASI07 Insecure Inter-Agent Communication, ASI08 Cascading Agent Failures, ASI09 Human-Agent Trust Exploitation and ASI10 Rogue Agents.
40. How does TREASURE map to CSA MAESTRO?
TREASURE uses the canonical seven MAESTRO layers: L1 Foundation Models, L2 Data Operations, L3 Agent Frameworks, L4 Deployment & Infrastructure, L5 Evaluation & Observability, L6 Security & Compliance and L7 Agent Ecosystem. TREASURE decomposes these concerns across its five operational layers.
41. How does TREASURE relate to MITRE ATLAS?
TREASURE uses MITRE ATLAS as a threat and mitigation crosswalk. The v1.2 dataset pins ATLAS references to release v2026.08 and maps documented incidents and controls to verified techniques and mitigations.
42. How does TREASURE relate to AIUC-1?
AIUC-1 provides auditable AI security control requirements that TREASURE maps into its operational architecture. UC-* identifiers are TREASURE's internal control identifiers; they are not AIUC-1 control codes.
---
43. What evidence supports TREASURE v1.2?
The v1.2 evidence base contains 13 documented incidents or incident entities, including EchoLeak, Gemini Memory Attack/GeminiJack, AgentPoison, AiTM, Atlassian Rovo, Replit, OpenClaw, LiteLLM/Trivy, PocketOS, OpenAI/Hugging Face, Mastra and ClawHub.
44. Are TREASURE Lab experiments the same as incident evidence?
No. `TRSR.LAB.*` entities are research artefacts or reference implementations. They must not be presented as real-world incident evidence or validated benchmarks.
45. What is TREASURE Lab?
TREASURE Lab is the Detection & Response Engineering component introduced in v1.2. It develops and tests mechanisms such as behavioural baselines, Drift Score, detection-as-code and audited attack-chain mappings.
46. What is the Drift Score?
The Drift Score models an agent session as a directed graph of tool invocations and compares the observed trajectory with a CI/CD-validated baseline. The objective is to identify changed execution paths and provide an explainable signal for detection and response.
47. Is Drift Score already a validated benchmark?
No. v1.2 describes it as a research methodology. Production implementation requires defined graph-distance approximations, weighting and costs, baseline normalization, threshold calibration using labelled replay, and measurement of false-positive rate and MTTD.
48. What are the main limitations of TREASURE?
v1.2 does not fully cover multimodal agent threats such as visual prompt injection, audio command hijacking or sensor spoofing. Other limitations include trajectory-log volume, signing and sandboxing overhead, marketplace risk and potential behavioural-baseline evasion.
---
49. What is the current TREASURE version?
The current baseline is TREASURE Framework v1.2, dated 29 September 2026. It supersedes v1.1 and consolidates the updated threat model, controls, standards mappings, evidence base, MVSP and TREASURE Lab work.
50. How can I use or contribute to TREASURE?
TREASURE is released under CC0 1.0 Universal. The framework can be copied, adapted, implemented and extended. Contributions should preserve the distinction between documented evidence, counterfactual analysis and research artefacts.
---
Central Principle
> **Protect your AgenticAI Security treasure. If you do not govern your agents, they will work for your adversaries.**
Govern. Protect. Detect. Assure. Evolve.
Repository: https://github.com/rogersanz/agentic-aisec-treasure
