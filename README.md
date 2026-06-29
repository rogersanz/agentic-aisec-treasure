████████╗██████╗ ███████╗ █████╗ ███████╗██╗   ██╗██████╗ ███████╗
╚══██╔══╝██╔══██╗██╔════╝██╔══██╗██╔════╝██║   ██║██╔══██╗██╔════╝
   ██║   ██████╔╝█████╗  ███████║███████╗██║   ██║██████╔╝█████╗
   ██║   ██╔══██╗██╔══╝  ██╔══██║╚════██║██║   ██║██╔══██╗██╔══╝
   ██║   ██║  ██║███████╗██║  ██║███████║╚██████╔╝██║  ██║███████╗
   ╚═╝   ╚═╝  ╚═╝╚══════╝╚═╝  ╚═╝╚══════╝ ╚═════╝ ╚═╝  ╚═╝╚══════╝
 

Editor's Notice
The TREASURE AI Security Framework is an innovative security framework developed by Roger Sanz, PhD, explicitly designed to address the complex vulnerabilities and risk vectors of Agentic AI systems.

This framework is open to every contributor and practitioner with a clear focus on security research, testing, or interest in the Agentic AI Security scenario evolution. This initial version provides the starting point of the framework's evolution and should be used in a tailored manner depending on the specific organization's scenario. It is intended to complement — not substitute — other frameworks, and takes into account future integrations based on community development.

Central principle: Protect your AgenticAI Security treasure. If you do not govern your agents, they will work for your adversaries.

Licensing & Rights Notice (CC0 1.0): To the extent possible under law, the author has waived all copyright and related rights to this specific layout and textual implementation. You are free to copy, modify, distribute, and build upon this text, even for commercial purposes, without seeking prior permission. → View CC0 1.0 Legal Code

Executive Summary
Enterprise organizations are deploying autonomous AI agents at an accelerating pace. Unlike traditional generative AI systems that respond to prompts in isolation, agentic systems plan, act, remember, and collaborate across multi-step workflows — invoking APIs, modifying databases, communicating with other agents, and operating continuously with minimal human oversight. This qualitative leap in capability introduces a qualitative leap in attack surface that no single perimeter control, guardrail, or content filter is architecturally capable of addressing.

The TREASURE Framework responds with a five-layer defense-in-depth architecture specifically engineered for the threat model of agentic AI. Each layer addresses a distinct attack class while maintaining structural independence so that the failure of any single layer does not cascade into a system-wide breach. The framework is not a product, a policy template, or a checklist: it is an operational architecture grounded in the adversarial evidence base of 2025–2026.

The core adversarial problem this document addresses is the double-agent threat: an autonomous agent that, through memory poisoning, RAG poisoning, or inter-agent communication manipulation, operates against the interests of its legitimate principals while appearing to function normally. Three documented incidents — EchoLeak (CVE-2025-32711), OpenClaw (CVE-2026-25253), and the Replit Meltdown (Incident #1152, July 2025) — demonstrate that this threat class is not theoretical.
