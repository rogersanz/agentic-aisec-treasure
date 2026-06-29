████████╗██████╗ ███████╗ █████╗ ███████╗██╗   ██╗██████╗ ███████╗
╚══██╔══╝██╔══██╗██╔════╝██╔══██╗██╔════╝██║   ██║██╔══██╗██╔════╝
   ██║   ██████╔╝█████╗  ███████║███████╗██║   ██║██████╔╝█████╗
   ██║   ██╔══██╗██╔══╝  ██╔══██║╚════██║██║   ██║██╔══██╗██╔══╝
   ██║   ██║  ██║███████╗██║  ██║███████║╚██████╔╝██║  ██║███████╗
   ╚═╝   ╚═╝  ╚═╝╚══════╝╚═╝  ╚═╝╚══════╝ ╚═════╝ ╚═╝  ╚═╝╚══════╝

        
# TREASURE Framework - FAQ (Frequently Asked Questions)

**Version 1.0** | June 2026

**TREASURE** — *Tiered Resilient Execution Agentic Security Unified Robust Ecosystem*

Defense-in-Depth Architecture for Agentic AI Systems

---

### **1. What is the TREASURE Framework?**

TREASURE is a **defense-in-depth security framework** designed specifically for **Agentic AI** systems (autonomous agents that plan, use tools, remember, and act independently). It organizes protections into five independent layers to limit the impact of breaches.

---

### **2. What does TREASURE stand for?**

**Tiered Resilient Execution Agentic Security Unified Robust Ecosystem**

---

### **3. Why was the TREASURE Framework created?**

Traditional security controls were built for stateless generative AI. Agentic systems introduce persistent memory, tool usage, and long-running autonomy, creating new attack surfaces. TREASURE provides a structured operational architecture to secure these advanced systems in production.

---

### **4. What are the five layers of the TREASURE Framework?**

1. **Data Layer** – Diamond Record (Single Governed Truth)  
2. **Execution Layer** – Skills & Runtime (Critical Attack Surface)  
3. **Governance Layer** – Code-Grade Governance  
4. **Control Layer** – Human-in-the-Loop (Encapsulated Autonomy)  
5. **Security Layer** – Defense-in-Depth (Blast Radius Engineering)

---

### **5. What is the main threat TREASURE addresses?**

The **Double Agent threat**: an autonomous agent that appears to operate normally while secretly working against its owners through memory poisoning, RAG attacks, or inter-agent manipulation.

---

### **6. Does TREASURE replace existing standards like OWASP or NIST?**

No. TREASURE is an **implementation overlay**. It maps to and works alongside OWASP ASI, CSA MAESTRO, NIST AI RMF, AIUC-1, ISO 42001, and MITRE ATLAS.

---

### **7. Is the framework free to use?**

Yes. It is released under **CC0 1.0 (Public Domain)**. You can freely copy, modify, distribute, and use it commercially with no restrictions.

---

### **8. Who is TREASURE intended for?**

- AI Security Engineers and Red Teams  
- CISOs and Security Architects  
- Developers building production-grade agentic systems  
- Researchers focused on Agentic AI safety

---

### **9. What are the three primary attack vectors TREASURE focuses on?**

1. Memory Poisoning  
2. RAG Poisoning  
3. Inter-Agent Communication Poisoning

---

### **10. Which real-world incidents influenced the framework?**

EchoLeak (CVE-2025-32711), OpenClaw (CVE-2026-25253), Replit Meltdown, GeminiJack, and research attacks such as AgentPoison, MemoryGraft, and AiTM.

---

### **11. What is the Agent Runtime Control Plane (ARCP)?**

The ARCP is the central enforcement engine of TREASURE. It operates at the infrastructure layer and enforces critical controls (Memory Manager, Tool Router, Skill Executor, Policy Engine) that the agent cannot bypass through prompt manipulation.

---

### **12. What is the Agency Envelope?**

A formal, enforceable boundary that defines exactly what actions an agent is allowed to perform autonomously. Actions outside this envelope require human approval.

---

### **13. What is a Skill Security Manifest?**

A signed YAML file that declares a skill’s permissions, allowed tools, risk level, sandbox requirements, and dependencies. It is enforced by the runtime before execution.

---

### **14. How important is trajectory logging?**

Critical. Full trajectory logging is one of the few reliable ways to detect and investigate memory poisoning and goal hijacking attacks after they occur.

---

### **15. What are the main implementation challenges?**

- High data volume from trajectory logging  
- Performance overhead from signing and sandboxing  
- Securing open skill marketplaces  
- Sophisticated evasion of behavioral baselining

---

### **16. Is TREASURE suitable for startups and small teams?**

Yes. It includes a **Minimum Viable Defense Posture (MVDP)** with 7–8 essential controls that can be implemented incrementally.

---

### **17. Does TREASURE address multi-agent systems?**

Yes. The Security Layer includes specific controls for inter-agent trust, message signing, circuit breakers, and zero-trust communication.

---

### **18. Will there be future versions of TREASURE?**

Yes. The roadmap includes community feedback incorporation, multi-modal agent support, and reference code implementations.

---

### **19. Can I use TREASURE in commercial products?**

Absolutely. The CC0 license gives you full freedom to use it in any commercial or internal project.

---

### **20. What is the most important principle of the framework?**

**“Protect your AgenticAI Security treasure. If you do not govern your agents, they will work for your adversaries.”**

---

### **21. Where can I download the full document?**

[Download TREASURE Framework v1.0](TREASURE_FRAMEWORK_AGENTIC_AI_V1.docx)

---

### **22. How mature is the framework today?**

It is a solid **Version 1.0** — comprehensive and production-oriented, but still evolving. It provides a strong foundation that organizations can adapt to their specific risk profiles.

---

### **23. How can organizations get started with TREASURE?**

Start with the **Minimum Viable Defense Posture (MVDP)** and the **Implementation Roadmap**. Begin with the Data Layer, then progressively implement the upper layers.

---

### **24. What makes TREASURE different from other AI security frameworks?**

It focuses on **operational architecture** rather than just lists of controls. It emphasizes structural independence between layers and real-world attack patterns from 2025–2026 incidents.

---

### **25. The debate is open — what should I do next?**

Download the framework, evaluate it against your current agent deployments, share your feedback, and help improve it.  
**The floor is yours.**

---

**Contributions and discussions are highly welcome!**


```
