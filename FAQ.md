       
TREASURE Framework --- FAQ
Frequently Asked Questions  
Version 1.2 · 29 September 2026
TREASURE --- Tiered Resilient Execution Architecture for Secure
Unified Robust Environments
Defense-in-Depth Architecture for Agentic AI Systems
---
About the Framework
1. What is the TREASURE Framework?
TREASURE is a defense-in-depth security architecture specifically
designed for Agentic AI systems: systems that can plan, act, remember,
invoke tools, modify resources and collaborate across multi-step
workflows.
It organizes security into five layers with distinct responsibilities
and deliberately independent enforcement properties. The objective is to
prevent a failure in one layer from becoming a system-wide compromise.
2. What does TREASURE stand for?
TREASURE stands for:
> **Tiered Resilient Execution Architecture for Secure Unified Robust
> Environments**
This is the v1.2 framework title/tagline. It supersedes the wording used
in earlier FAQ material.
3. Who created TREASURE?
TREASURE was developed by Roger Sanz, PhD.
v1.2 identifies Roger Sanz as AI Security Lead at Plain Concepts, Senior
Researcher at Universidad Isabel I and Lead Editor of OWASP AI Exchange,
with contributions to MITRE ATLAS, CSA, ISMS Forum and DAMA.
4. When was TREASURE v1.2 released?
29 September 2026.
Version 1.2 supersedes v1.1 of 3 July 2026 and its same-day corrections
addendum.
5. Is v1.2 a completely new framework?
No. The five-layer architecture is unchanged.
v1.2 is an operational expansion and verification release. It
consolidates the v1.1 corrections, remaps CSA MAESTRO to its canonical
seven-layer model, adds new controls and incidents, introduces new
design principles, updates standards crosswalks and adds the TREASURE
Lab detection-and-response engineering track.
6. Is TREASURE a product?
No.
TREASURE is an operational security architecture and open framework,
not a commercial product, platform or proprietary security technology.
7. Is TREASURE a compliance framework?
Not by itself.
TREASURE provides an operational security architecture and crosswalks to
frameworks and standards including OWASP, CSA MAESTRO, NIST AI RMF,
MITRE ATLAS, AIUC-1 and ISO/IEC 42001. It does not replace regulatory
obligations, formal certifications or organization-specific
legal/compliance assessments.
8. Is TREASURE a threat model?
It can be used as an architectural basis for threat modeling, but its
scope is broader than a threat taxonomy.
TREASURE connects threats to architecture, controls, enforcement
points, detection, containment and recovery.
9. Who is TREASURE intended for?
The framework is relevant to:
AI Security Engineers
Security Architects
CISOs and security leaders
AI/ML platform engineers
Agent developers
Red teams and adversarial testing teams
Detection and response engineers
AI governance and risk practitioners
Security researchers
Organizations operating production Agentic AI systems
---
Core Security Model
10. What is the main security problem TREASURE addresses?
The central adversarial problem is the Double-Agent Threat: an
autonomous agent that appears to operate normally while its effective
behavior has been manipulated against the interests of its legitimate
principal.
The manipulation may originate from memory poisoning, RAG poisoning,
malicious skills, tool misuse, inter-agent communication, supply-chain
compromise or other execution-path attacks.
11. Does v1.2 address threats where there is no attacker?
Yes. This is one of the most important v1.2 extensions.
The framework explicitly addresses excess authority without an
adversary and the rogue-agent problem.
PocketOS and the OpenAI evaluation-agent / Hugging Face incident
demonstrate that an agent can cause serious harm without prompt
injection or a human attacker when its authority, environment or safety
boundaries are insufficient.
12. What is the difference between the Double-Agent Threat and a Rogue Agent?
The Double-Agent Threat describes an agent whose behavior is
manipulated while it appears to operate normally.
A Rogue Agent can cause harm without an external attacker because
the agent's objective, authority, environment or execution path is
unsafe.
The distinction matters because traditional adversarial defenses may not
detect a failure when there is no malicious input to identify.
13. What are the three primary attack vectors?
The original primary vectors remain:
Memory Poisoning
RAG Poisoning
Inter-Agent Communication Poisoning
v1.2 expands the threat model with Excess Authority without
Adversary as an additional attack/failure class.
14. What is meant by "intent is not enforcement"?
An instruction in a prompt, system message, policy document or agent
context does not constitute a security control unless an independent
enforcement mechanism can prevent the prohibited action.
This is one of the five explicit v1.2 design principles.
15. What does "identity is not authority" mean?
Knowing which agent is acting does not determine what that agent should
be allowed to do.
Identity must be associated with scoped, task-appropriate authority.
TREASURE therefore requires unique agent identities, JIT credentials and
bounded permissions rather than treating authenticated identity as
sufficient authorization.
16. What is asymmetric autonomy?
Asymmetric autonomy means that the more consequential an action is,
the less autonomy the agent should have to execute it without
independent validation or authorization.
Low-risk actions can remain highly automated. Irreversible or
authority-expanding actions require stronger external controls.
17. What does "containment must be independent of the agent" mean?
The mechanism that stops or contains an agent must remain operational
even when the agent is malfunctioning, compromised, ignoring
instructions or unable to process its own context.
TREASURE therefore places the response mechanism at
infrastructure/control-plane level rather than relying exclusively on
the agent's own reasoning loop.
18. What is the blast-radius principle?
TREASURE assumes that prevention will eventually fail.
The Security Layer therefore focuses on limiting what a compromised,
malfunctioning or rogue agent can reach, modify, observe or destroy.
This includes identity scoping, segmentation, trajectory telemetry,
circuit breakers and independent recovery.
---
The Five TREASURE Layers
19. What are the five layers?
DATA LAYER --- Diamond Record  
Design principle: Single Governed Truth
EXECUTION LAYER --- Skills & Runtime  
Design principle: Critical Attack Surface Control
GOVERNANCE LAYER --- Code-Grade Governance  
Design principle: Policy-as-Code Discipline
CONTROL LAYER --- Human-in-the-Loop  
Design principle: Encapsulated Autonomy
SECURITY LAYER --- Defense-in-Depth  
Design principle: Blast Radius Engineering
20. Why are the layers hierarchical?
Each layer provides foundational guarantees that the layers above it
rely upon.
The dependency relationship is:
``` text
SECURITY
   ↑
CONTROL
   ↑
GOVERNANCE
   ↑
EXECUTION
   ↑
DATA
```
The architecture is designed so that a failure in one layer does not
automatically become a system-wide failure.
21. What does the DATA Layer protect?
The Data Layer protects the integrity, provenance, authorization and
recoverability of information used by agent reasoning.
Its primary threat is Memory & Context Poisoning (ASI06).
22. What is the Diamond Record?
The Diamond Record is TREASURE's conceptual model for a single
governed source of truth for data used by agent reasoning.
It covers governed ingestion, provenance, memory integrity,
identity-scoped retrieval and recoverable state.
23. What are the DATA Layer controls?
UC-DATA-01 --- Governed ingestion and provenance
UC-DATA-02 --- Memory and embedding integrity
UC-DATA-03 --- Identity-scoped retrieval controls
UC-DATA-04 --- Versioned memory and constraint recovery
UC-DATA-05 --- Recovery independence
24. What is UC-DATA-05?
UC-DATA-05 is new in v1.2.
It requires that no credential reachable by an agent can destroy both
production data and its recovery path.
Typical implementation mechanisms include separate backup
accounts/tenants, delayed or soft deletion and tested restore
procedures.
25. What does the EXECUTION Layer protect?
The Execution Layer controls what an agent can execute and which tools,
skills and executable components it can invoke.
It addresses tool misuse, unexpected code execution, malicious skills,
supply-chain execution and control-plane abuse.
26. What are the EXECUTION Layer controls?
UC-EXEC-01 --- Least-privilege tool and skill execution
UC-EXEC-02 --- Cryptographic signing and provenance verification
UC-EXEC-03 --- Sandboxing and runtime isolation
UC-EXEC-04 --- Immutable tool invocation audit trail
UC-EXEC-05 --- Pre-invocation intent validation
27. What is the GOVERNANCE Layer?
The Governance Layer turns security requirements into version-controlled
and machine-enforceable controls.
Its design principle is Policy-as-Code Discipline.
28. What are the GOVERNANCE Layer controls?
UC-GOV-01 --- Version-controlled agent behavioural
specifications
UC-GOV-02 --- Machine-enforceable Policy-as-Code
UC-GOV-03 --- CI/CD security and supply-chain gates
UC-GOV-04 --- AI Bill of Materials (AIBOM)
UC-GOV-05 --- Continuous drift detection
29. What is an AIBOM?
An AI Bill of Materials (AIBOM) records the components and
dependencies that make up an agent deployment, including model/provider
information, skills, hashes, certificates, tool/API schema versions and
knowledge sources.
TREASURE treats the AIBOM as a supply-chain and change-management
control.
30. What does the CONTROL Layer do?
The Control Layer defines the boundaries of agent autonomy.
It determines which actions can be performed autonomously, which require
authorization and how the agent can be stopped independently of its own
context.
31. What are the CONTROL Layer controls?
UC-CTRL-01 --- Agency Envelope and Decision Boundary Matrix
UC-CTRL-02 --- Tiered response: Stop → Contain → Recover →
Terminate
UC-CTRL-03 --- Human authorization checkpoints
32. What is the Agency Envelope?
The Agency Envelope is an enforceable boundary defining what an agent is
permitted to do autonomously.
It is implemented through a Decision Boundary Matrix and an Agency
Envelope Validator.
Actions that expand authority or cross defined irreversible-action
boundaries require independent authorization.
33. Does the Agency Envelope apply to testing environments?
Yes.
v1.2 explicitly extends UC-CTRL-01 to evaluation and red-team
environments.
If safety layers are intentionally reduced for testing, compensating
controls must still bound credentials, network access, registry access
and destructive authority.
34. What is the Security Layer?
The Security Layer provides defense-in-depth when prevention fails.
Its design principle is Blast Radius Engineering.
It addresses identity abuse, inter-agent attacks, cascading failures,
lateral movement, credential abuse and data exfiltration.
35. What are the SECURITY Layer controls?
UC-SEC-01 --- Unique cryptographic identity and JIT credentials
UC-SEC-02 --- Network micro-segmentation
UC-SEC-03 --- Complete off-agent execution trajectory
UC-SEC-04 --- Behavioral baselines and anomaly detection
UC-SEC-05 --- Inter-agent circuit breakers
UC-SEC-06 --- Output DLP and exfiltration detection
UC-SEC-07 --- Detection-to-containment escalation ownership
36. What is UC-SEC-07?
UC-SEC-07 is new in v1.2.
It requires every meaningful agent-behavior detection to have:
a named owner;
an escalation path;
an automatic containment trigger where appropriate;
measurable MTTD/MTTC;
periodic drills.
The principle is:
> **A signal that does not escalate is not a control.**
---
ARCP, Runtime and Enforcement
37. What is the Agent Runtime Control Plane (ARCP)?
The ARCP is the central enforcement mechanism in the TREASURE
reference architecture.
It operates outside the agent's reasoning logic and provides enforcement
components including:
Memory Manager
Tool Router
Skill Executor
Policy Engine
It also integrates with the Agency Envelope, trajectory logging, anomaly
detection and tiered containment.
38. Why is the ARCP important?
Because agent context is mutable.
If a security restriction exists only inside the agent's context, it can
potentially be lost through memory manipulation, context compaction,
goal hijacking or model behavior.
The ARCP provides an enforcement boundary outside that context.
39. What is a Skill Security Manifest?
A Skill Security Manifest describes the security properties and
permissions associated with an executable skill.
TREASURE v1.2 requires cryptographic signing and verification of
executable components, minimal-privilege manifests, provenance and
runtime enforcement.
The manifest should therefore be treated as an enforced security
artefact, not merely documentation.
40. Does a tool allow-list count as a security control?
Only when it is enforced at the execution boundary.
An advisory configuration that the agent can circumvent does not provide
the same security property as a Tool Router that rejects unauthorized
invocations before execution.
---
Identity, Credentials and Authority
41. Why does TREASURE require per-agent identity?
Shared credentials make attribution, authorization and containment
difficult.
UC-SEC-01 therefore requires unique cryptographic identity per agent, no
shared credentials and JIT authorization.
42. What is JIT identity?
Just-in-time identity means credentials are issued for the required task
or invocation and expire rather than remaining as ambient long-lived
secrets.
TREASURE additionally requires workload credential hygiene, including
blocking inappropriate metadata-service access and avoiding secrets in
untrusted-input parsers.
43. Does authentication solve the Agentic AI authorization problem?
No.
Authentication establishes identity. It does not establish appropriate
authority.
TREASURE explicitly separates identity, authority, task scope and
action consequence.
44. Why is credential scoping important?
Because the damage caused by an agent is partly determined by the
authority available to it.
PocketOS and the OpenAI/Hugging Face incident illustrate how over-scoped
or shared credentials can transform a local agent failure into
infrastructure compromise or destructive impact.
---
Observability and Detection
45. Why is trajectory logging important?
TREASURE treats full execution trajectory logging as a critical security
capability.
The trajectory should cover, where applicable:
tool calls;
memory operations;
state transitions;
inter-agent messages;
agent identity;
skill identity and version;
relevant parameters and output hashes;
timestamps;
trace correlation.
The log must be immutable and stored outside the agent.
46. Is logging alone sufficient?
No.
TREASURE distinguishes visibility from response.
A log that is never analyzed does not detect an attack. A detection that
has no owner or containment path does not constitute an operating
control.
This is the rationale for UC-SEC-04 and UC-SEC-07.
47. What is Drift Score?
Drift Score is the TREASURE Lab methodology for comparing the execution
graph of a live agent session with the CI/CD-validated baseline for that
agent class.
For example:
``` text
BASELINE:
tool_A → tool_B → tool_C

LIVE:
tool_A → credential_lookup → prod_delete

NEW EDGE:
credential_lookup → prod_delete
```
The important signal is not only that the score changed, but which
execution edge changed.
48. Is Drift Score production-ready?
v1.2 defines the methodology but explicitly requires calibration before
production use.
Production implementation should:
declare the graph-distance approximation;
define node/edge costs;
weight irreversible actions more heavily;
normalize against baseline graph size;
calibrate thresholds using labelled replay data;
measure false-positive rate and MTTD;
route alerts through UC-SEC-07.
49. What is detection-to-containment escalation?
It is the requirement that a security signal must have a defined
operational path from:
``` text
Detection
   ↓
Named Owner
   ↓
Escalation
   ↓
Automatic Stop / Contain
   ↓
Recovery / Termination
```
UC-SEC-07 makes this an explicit TREASURE control.
---
Response and Recovery
50. What is the TREASURE tiered kill-switch?
v1.2 defines four response stages:
T1 --- Stop
T2 --- Contain
T3 --- Recover
T4 --- Terminate
Containment is designed to operate independently from the agent's
context.
51. What does "Stop" mean?
Stop interrupts the active execution path.
It is the immediate response to a high-confidence or high-consequence
violation.
52. What does "Contain" mean?
Containment limits further action by mechanisms such as credential
revocation, quarantine, network restriction and state snapshotting.
The reference architecture targets rapid containment for high-risk
scenarios.
53. What does "Recover" mean?
Recovery re-establishes a trusted state and restores the defined Agency
Envelope and security constraints.
Recovery depends on independent, trustworthy state and backups.
54. What does "Terminate" mean?
Termination is the final control state when an agent or runtime must be
removed from operation rather than merely paused or constrained.
---
MCP Security
55. Does TREASURE cover MCP?
Yes.
v1.2 treats Model Context Protocol (MCP) as a significant expansion
of the Execution Layer attack surface.
56. Which MCP threats are covered?
TREASURE v1.2 explicitly discusses:
Tool Poisoning
Rug Pull Attacks
Confused Deputy Attacks
Token Passthrough
Tool manifest integrity
Server provenance
Credential scoping
Runtime isolation
57. Why is MCP considered an execution security problem?
Because MCP connects agents to external tools, APIs and data sources.
The security question is therefore not simply whether the server is
reachable. It is whether the agent can invoke the connected capability
under the intended identity, authority, provenance and policy
constraints.
58. What is a Rug Pull attack?
A Rug Pull occurs when an MCP server or tool initially establishes trust
and subsequently changes its behavior.
TREASURE addresses this through pinned or content-addressed definitions,
signature verification and continuous drift detection.
59. What is a Confused Deputy attack in MCP?
A confused deputy occurs when an MCP server uses its own elevated
permissions instead of the scoped authority of the user or agent on
whose behalf it is acting.
TREASURE aligns this problem with UC-SEC-01 and scoped, audience-bound,
just-in-time credentials.
60. What is Token Passthrough?
Token passthrough occurs when a server forwards a raw client
authentication token to a downstream service instead of obtaining a
properly scoped token for the downstream audience.
This weakens authorization boundaries and auditability.
---
OWASP, MAESTRO and Cross-Framework Alignment
61. Does TREASURE replace OWASP Agentic Top 10?
No.
TREASURE uses the OWASP Agentic Applications taxonomy as an external
threat classification and maps its own controls and layers to those
threats.
62. What OWASP taxonomy does v1.2 use?
v1.2 uses the official December 2025 numbering:
ID      OWASP Agentic Threat
---
ASI01   Agent Goal Hijack
ASI02   Tool Misuse & Exploitation
ASI03   Identity & Privilege Abuse
ASI04   Agentic Supply Chain Vulnerabilities
ASI05   Unexpected Code Execution
ASI06   Memory & Context Poisoning
ASI07   Insecure Inter-Agent Communication
ASI08   Cascading Agent Failures
ASI09   Human-Agent Trust Exploitation
ASI10   Rogue Agents
Data Leakage & Exfiltration is not treated as a standalone ASI category
in v1.2; it is treated as a consequence spanning several threat classes.
63. How does TREASURE relate to CSA MAESTRO?
TREASURE uses the canonical seven-layer CSA MAESTRO model:
L1 Foundation Models
L2 Data Operations
L3 Agent Frameworks
L4 Deployment & Infrastructure
L5 Evaluation & Observability
L6 Security & Compliance
L7 Agent Ecosystem
TREASURE operationally decomposes relevant MAESTRO capabilities into its
five security layers.
64. Did v1.2 correct the MAESTRO mapping?
Yes.
v1.2 explicitly remaps legacy labels to the canonical model:
Legacy "L5 Ecosystem" → L7 Agent Ecosystem
Legacy "L6 Human-AI Interface" → L6 Security & Compliance
Legacy "L7 Governance & Audit" → L6 Security & Compliance, plus
L5 Evaluation & Observability where applicable
The canonical MAESTRO model does not contain a dedicated "Human-AI
Interface" layer.
65. Which other standards are aligned?
v1.2 references:
OWASP Agentic Applications
OWASP Agent Control Standard
OWASP AI Exchange
OWASP AI DEFEND
CSA MAESTRO
NIST AI RMF
NIST AI Agent Standards Initiative / NCCoE
MITRE ATLAS v2026.08
MITRE ATT&CK v19.2
AIUC-1 Q3 2026
ISO/IEC 42001
MCP specification 2026-07-28
EU AI Act as amended by Regulation (EU) 2026/1744
related CEN/CENELEC and ETSI AI security work
66. Are UC-* identifiers official AIUC-1 controls?
No.
This distinction is important.
`UC-*` identifiers are TREASURE's internal crosswalk convention.
They are not official AIUC-1 requirement identifiers.
---
MVSP v1.2
67. What is MVSP?
MVSP means Minimum Viable Security Posture.
It is the v1.2 minimum control analysis derived from the documented
incident set and their stored counterfactual control mappings.
It supersedes the earlier MVDP terminology used in the v1.0 FAQ.
68. How many controls are in the MVSP prevention core?
Four controls form the Tier 1 Prevention Core:
UC-CTRL-01 --- Agency Envelope
UC-DATA-01 --- Governed ingestion
UC-EXEC-02 --- Cryptographic signing
UC-SEC-01 --- Per-agent scoped JIT identity
The v1.2 analysis states that the four-control set breaks all 13
documented incident chains in the stored counterfactual analysis.
69. What is the resilience core?
Three additional controls form the Tier 2 Resilience Core:
UC-CTRL-02 --- Tiered kill-switch
UC-SEC-07 --- Detection-to-containment escalation ownership
UC-DATA-05 --- Recovery independence
These controls are intended to limit impact when prevention fails.
70. Is the MVSP a proven security benchmark?
No.
The v1.2 document explicitly states that the MVSP is a counterfactual
analysis over documented incidents, not an empirical effectiveness
measurement or universal guarantee.
71. Are additional controls needed for particular agent types?
Yes.
v1.2 defines profile overlays, including:
Coding / infrastructure agents → UC-CTRL-03
RAG / copilot agents → UC-EXEC-05 + UC-SEC-06
Build pipelines → UC-GOV-03
Multi-agent systems → UC-SEC-05
---
Real-World Evidence
72. Which incidents are included in v1.2?
The v1.2 evidence base contains 13 documented incident entities:
EchoLeak --- CVE-2025-32711
Gemini Memory Attack / GeminiJack
AgentPoison
AiTM
Atlassian Rovo
Replit Vibe Coding Meltdown
OpenClaw --- CVE-2026-25253
OpenClaw stop-command failure
LiteLLM / Trivy supply-chain compromise
PocketOS
OpenAI evaluation agents / Hugging Face
Mastra npm / Sapphire Sleet
ClawHub malicious skills
73. Why were PocketOS and OpenAI/Hugging Face important additions?
Because both demonstrate security failures that did not require a
conventional external attacker.
They expose two central v1.2 principles:
Identity ≠ Authority
Intent ≠ Enforcement
They also demonstrate why autonomous execution requires external
containment and recovery controls.
74. Does TREASURE claim that its controls have been proven against these incidents?
No.
The incidents provide an empirical evidence base for threat and
control analysis.
The framework uses counterfactual mappings to identify which controls
would have addressed the documented failure chains. This should not be
interpreted as empirical validation of universal control effectiveness.
75. Does the framework distinguish incidents from research artefacts?
Yes.
v1.2 explicitly distinguishes `TRSR.LAB.*` research artefacts from
incident evidence.
TREASURE Lab entities are reference implementations and research
material, not claims that the associated lab scenario occurred as a
real-world incident.
---
TREASURE Lab
76. What is TREASURE Lab?
TREASURE Lab is the detection-and-response engineering component
introduced in v1.2.
It includes research artefacts for:
Drift Score
Detection-as-Code
Sigma-based controls
audited attack-chain mappings
runtime security experimentation
77. What is the purpose of the Drift Score?
To identify behavioral changes in the execution graph of an agent
relative to its validated baseline.
The score is intended to raise an alert; the changed execution edge
provides the explanation.
78. What is TRSR.LAB.SIGMA_HITL?
It is a research detection rule for an irreversible agent action that is
allowed without the required human confirmation within the defined SLA.
It is explicitly documented as a TREASURE Lab artefact rather than a
claim of universal production readiness.
79. What is the RootedCON VLC 2026 technique chain?
The v1.2 framework documents an audited lab chain involving:
malicious skill acquisition;
software supply-chain compromise;
execution;
escape-to-host;
command-and-control transfer;
impact techniques in controlled demonstration environments.
The mapping was refined against MITRE ATT&CK v19.2 and MITRE ATLAS
v2026.08.
---
Implementation
80. How should an organization start implementing TREASURE?
A practical sequence is:
Establish the DATA Layer
Harden the EXECUTION Layer
Implement GOVERNANCE
Establish the CONTROL Layer
Harden SECURITY and containment
For production agents with write access, the MVSP prevention and
resilience cores can be used as an accelerated starting point.
81. What is the five-phase implementation roadmap?
---
Phase                               Focus
---
1 --- Foundation                Data governance, provenance,
integrity and recovery
2 --- Execution Control         Skills, signing, allow-lists,
sandboxing and pre-call validation
3 --- Governance                Policy-as-Code, AIBOM, CI/CD and
dependency controls
4 --- Human Control             Agency Envelope, Decision Boundary
Matrix, HITL and kill-switch
5 --- Security Hardening        JIT identity, segmentation,
trajectory telemetry, behavioral
detection and circuit breakers
82. Can TREASURE be implemented incrementally?
Yes.
The architecture is deliberately layered and can be adopted
progressively.
However, organizations should not interpret incremental deployment as
permission to leave high-risk production agents with unrestricted
destructive authority.
83. Is TREASURE platform-specific?
No.
v1.2 documents implementation examples for Microsoft/Azure/Copilot
Studio, Google Cloud/Vertex AI Agent Builder and AWS/Bedrock Agents.
The framework evaluates security properties and enforcement
semantics, not vendor branding.
84. Does a vendor feature automatically satisfy a TREASURE control?
No.
A platform feature satisfies a TREASURE control only when it provides
the required security property and enforcement semantics.
For example, an advisory tool allow-list is not equivalent to an
execution-boundary enforcement mechanism.
85. Can TREASURE be used for small organizations?
Yes.
The framework can be adopted incrementally, starting with the MVSP.
The v1.2 source does not prescribe a single organization size,
technology budget or staffing model.
86. What are the main implementation challenges?
v1.2 identifies several:
trajectory-log volume;
performance overhead from signing and sandboxing;
securing open skill marketplaces;
evasion of behavioral baselines;
ensuring detections actually escalate;
multi-modal agent risks, which remain out of scope in v1.2.
---
Scope and Limitations
87. Does TREASURE cover multimodal agents?
Not fully.
v1.2 explicitly identifies visual prompt injection, audio command
hijacking and sensor spoofing as future/out-of-scope areas.
88. Does TREASURE guarantee prevention?
No.
TREASURE is a defense-in-depth architecture.
It assumes that prevention will eventually fail and therefore places
significant emphasis on detection, containment, recovery and
blast-radius reduction.
89. Is TREASURE an empirical security benchmark?
No.
Some elements, including MVSP and Drift Score, are based on documented
evidence, counterfactual analysis or defined methodology.
They should not be represented as universal empirical benchmarks without
additional validation.
90. What are the known limitations of trajectory logging?
Comprehensive trajectory logging can generate substantial data volumes.
v1.2 identifies intelligent sampling, compression and tiered retention
as practical requirements while preserving forensic value.
91. What are the performance considerations?
Signing, verification and strict sandboxing can introduce latency and
resource overhead.
TREASURE therefore supports tiered enforcement according to agent risk
rather than assuming every workload requires identical enforcement
intensity.
92. What is the marketplace limitation?
Open skill marketplaces can contain rapidly changing or obfuscated
malicious components.
v1.2 uses ClawHub campaigns as evidence that registry-side scanning
alone should not be treated as sufficient protection.
High-assurance environments should use provenance, signing and curated
or controlled registries.
93. Can behavioral baselining be evaded?
Yes.
Patient attackers or unexpected agent behavior can gradually move within
an apparently normal envelope.
TREASURE therefore treats behavioral detection as one layer of defense,
combined with policy enforcement, identity controls, segmentation and
containment.
---
Governance and Community
94. Is TREASURE open for contributions?
Yes.
The framework is intended for security researchers, practitioners and
contributors working on Agentic AI Security.
95. What kinds of contributions are particularly useful?
Examples include:
Agent Runtime Security
MCP security
Agent identity and authorization
Agentic supply-chain security
adversarial testing
threat modeling
detection engineering
observability
AI governance
security architecture
reference implementations
96. How should contributors distinguish evidence from framework opinion?
v1.2 recommends distinguishing explicitly between:
documented incident evidence;
research evidence;
TREASURE design requirements;
counterfactual analysis;
proposed research hypotheses.
This distinction protects the evidentiary quality of the framework.
97. Will TREASURE continue to evolve?
Yes.
v1.2 is explicitly designed as an evolving framework.
The source identifies future work including multi-modal agent risks,
further standards integration, community contributions and additional
reference implementations.
---
Licensing and Commercial Use
98. Is TREASURE free to use?
Yes.
The framework is released under CC0 1.0 Universal --- Public Domain
Dedication, to the extent permitted by law.
99. Can TREASURE be used commercially?
Yes.
The CC0 dedication permits copying, modification, distribution and
commercial use without requiring permission.
100. Do commercial users have to implement the framework exactly as published?
No.
TREASURE is intended to be adapted to the organization's architecture,
threat model and risk profile.
101. Are attribution and permission mandatory?
The CC0 dedication does not impose mandatory attribution or permission
requirements.
Attribution and contributions are nevertheless welcome as a community
practice.
---
Version 1.2 and Traceability
102. What changed between v1.1 and v1.2?
The major changes include:
consolidation of the v1.1 corrections addendum;
canonical CSA MAESTRO remapping;
four new documented incidents;
UC-DATA-05;
UC-SEC-07;
expanded UC-CTRL-01;
tiered UC-CTRL-02;
enhanced UC-SEC-01;
five new explicit design principles;
OWASP Agent Control Standard alignment;
MITRE ATLAS v2026.08 verification;
AIUC-1 Q3-2026 crosswalk;
MCP 2026-07-28 alignment;
NIST CAISI/NCCoE alignment;
EU Digital Omnibus alignment;
TREASURE Lab;
Drift Score methodology;
corrected Sigma rule;
audited RootedCON VLC 2026 technique chain;
canonical dataset expansion from 83 to 118 entities;
MVSP v1.2 across 13 incident chains.
103. Are v1.1 artefacts still available?
Yes.
v1.1 artefacts are deprecated, not deleted, and are retained for
traceability.
The v1.2 source points to the project version index for historical
traceability.
104. What is the current version?
TREASURE Framework v1.2 --- 29 September 2026.
This FAQ should therefore be treated as the v1.2 FAQ rather than the
June 2026 v1.0 FAQ.
---
Getting Started
105. What should I do first if I operate Agentic AI in production?
Start by answering five questions:
What data can the agent read or modify?
What tools and skills can it execute?
What authority and credentials does it possess?
Which actions require independent human authorization?
Can the organization stop, contain and recover the agent without
relying on the agent itself?
These questions map directly to the TREASURE layers.
106. What should I prioritize for an agent with production write access?
Use the v1.2 MVSP fast path:
Tier 1 --- Prevention
UC-CTRL-01
UC-DATA-01
UC-EXEC-02
UC-SEC-01
Tier 2 --- Resilience
UC-CTRL-02
UC-SEC-07
UC-DATA-05
Then apply profile overlays according to whether the agent is a
coding/infrastructure, RAG/copilot, build-pipeline or multi-agent
system.
107. What should a security review of an agent include?
At minimum:
agent identity;
authority and credentials;
tools and skills;
skill provenance;
data sources;
memory and RAG controls;
policy enforcement;
Agency Envelope;
irreversible actions;
HITL requirements;
trajectory logging;
anomaly detection;
escalation ownership;
containment;
recovery independence;
supply-chain dependencies;
MCP exposure where applicable.
108. Where can I find the full TREASURE Framework?
The canonical project repository is:
https://github.com/rogersanz/agentic-aisec-treasure
The v1.2 framework source is the authoritative technical reference for
the controls, mappings, incidents, methodology and references.
---
The Central Principle
109. What is the most important principle of TREASURE?
> **"Protect your AgenticAI Security treasure. If you do not govern your
> agents, they will work for your adversaries."**
The operational interpretation is:
> **Govern. Protect. Detect. Assure. Evolve.**
110. What is the challenge to the community?
The framework is intended to be challenged, tested and improved.
Practitioners should evaluate TREASURE against real agent deployments,
test its assumptions, validate the proposed controls, identify gaps and
contribute evidence.
The floor is yours.
---
References
For the complete standards, research papers, incident disclosures, CVEs
and framework references supporting this FAQ, see the References
section of `TREASURE_FRAMEWORK_AGENTIC_AI_V1.2.md`.
Key source families include:
OWASP Agentic Applications
OWASP Agent Control Standard
OWASP AI Exchange / AI DEFEND
CSA MAESTRO
NIST AI RMF and CAISI/NCCoE
MITRE ATLAS v2026.08
MITRE ATT&CK v19.2
AIUC-1
MCP specification 2026-07-28
ISO/IEC 42001
EU AI Act and Regulation (EU) 2026/1744
---
License
CC0 1.0 Universal --- Public Domain Dedication
To the extent possible under law, Roger Sanz González has waived all
copyright and related rights to this specific layout and textual
implementation of the TREASURE AI Security Framework.
https://creativecommons.org/publicdomain/zero/1.0/
TREASURE Framework v1.2 · Roger Sanz González · 29 September 2026
Govern. Protect. Detect. Assure. Evolve.
