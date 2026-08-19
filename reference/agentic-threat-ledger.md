*Threat framework reference · compiled 16 August 2026*

# Agentic Threat Ledger

Every major published AI & agentic-AI threat taxonomy, enumerated entry by entry — OWASP, MITRE, NIST, national cyber agencies, CSA, Microsoft, Google, and the academic aggregators — with versions, canonical links, and a crosswalk for mapping guardrail policies against them.


## OWASP — the core corpus

The OWASP GenAI Security Project publishes the deepest catalog: the agentic Top 10 is the ranked distillation of a 17-threat taxonomy, flanked by an LLM Top 10, a 21-risk data-security list, a full threat-and-control matrix, and a scoring system.


### Top 10 for Agentic Applications 2026  `OWASP ASI`

*v1.0 · Dec 9, 2025 · genai.owasp.org · peer-reviewed by 100+ experts*

| ID | Risk | Description |
| :--- | :--- | :--- |
| ASI01 | Agent Goal Hijack | Objectives redirected via prompt manipulation, poisoned data, or deceptive outputs |
| ASI02 | Tool Misuse & Exploitation | Misled agents misuse legitimate tools — data loss, exfiltration, resource abuse |
| ASI03 | Identity & Privilege Abuse | Ungovernable agent identities enable privilege escalation and authorization bypass |
| ASI04 | Agentic Supply Chain Vulnerabilities | Tampered models, tools, and third-party agents |
| ASI05 | Unexpected Code Execution (RCE) | Manipulated inputs to execution tools run arbitrary code |
| ASI06 | Memory & Context Poisoning | Injected content persistently biases future behavior |
| ASI07 | Insecure Inter-Agent Communication | Unauthenticated/unencrypted agent-to-agent messages enable spoofing |
| ASI08 | Cascading Failures | One corrupted output ripples across multiple agents |
| ASI09 | Human-Agent Trust Exploitation | Over-trusting users socially engineered via the agent |
| ASI10 | Rogue Agents | Agents drifting into harmful autonomy; the insider-threat analog |


### Agentic AI — Threats and Mitigations  `OWASP ASI`

*v1.0 Feb 2025 (T1–T15); v1.1 Dec 2025 adds T16–T17 · genai.owasp.org — the master taxonomy the Top 10 was distilled from*

| ID | Threat | Description |
| :--- | :--- | :--- |
| T1 | Memory Poisoning | Malicious data injected into agent memory corrupts future decisions |
| T2 | Tool Misuse | Agents improperly leverage legitimate tools via injection or unsafe delegation |
| T3 | Privilege Compromise | Unauthorized escalation or misuse of permissions; leaked credentials let agents operate beyond scope |
| T4 | Resource Overload | Attackers exhaust compute, memory, or service resources to disrupt the agent |
| T5 | Cascading Hallucination Attacks | False information from one model spreads through interconnected systems |
| T6 | Intent Breaking & Goal Manipulation | Attackers alter or redirect agent goals toward unintended actions |
| T7 | Misaligned & Deceptive Behaviors | Agents act deceptively due to misaligned objectives while appearing normal |
| T8 | Repudiation & Untraceability | Agent actions can't be reliably traced or accounted for |
| T9 | Identity Spoofing & Impersonation | Adversaries impersonate agents or users |
| T10 | Overwhelming Human-in-the-Loop | Flooding human overseers with approval requests until oversight fails |
| T11 | Unexpected RCE and Code Attacks | Unsafe code generation leads to remote code execution |
| T12 | Agent Communication Poisoning | False or malicious information injected into inter-agent channels |
| T13 | Rogue Agents in Multi-Agent Systems | Compromised or misaligned agents disrupt coordinated operations |
| T14 | Human Attacks on Multi-Agent Systems | Humans exploit inter-agent trust to trigger cascading failures |
| T15 | Human Manipulation | Exploiting user trust in AI to deceive humans into unsafe actions |
| T16 | Insecure Inter-Agent Protocol Abuse | Added in v1.1 to sync with ASI07 — exploitation of agent-to-agent protocols |
| T17 | Supply Chain Compromise | Added in v1.1 to sync with ASI04 — compromised models, tools, dependencies |


### Companion ASI documents  `OWASP ASI`

- Multi-Agentic System Threat Modeling Guide v1.0 — applies T1–T15 to real multi-agent architectures using the MAESTRO layered method
- Securing Agentic Applications Guide — the developer/operator control catalog (concrete controls, not threats)
- A Practical Guide for Secure MCP Server Development (Feb 2026) — for teams building MCP servers
- CheatSheet: Securely Using Third-Party MCP Servers 1.0 (Nov 2025) — for teams consuming MCP servers
- State of Agentic AI Security and Governance 2.01 (Jun 2026) — landscape survey; maps real CVEs and breach reports to the ASI categories
- AIUC-1 Crosswalk (May 2026) — bidirectional mapping between the agentic Top 10 and AIUC-1 compliance requirements
- AI Security Solutions Landscape for Agentic AI Q2 2026 — vendor/tooling map across the agentic lifecycle
- FinBot Agentic AI CTF (Aug 2025) — deliberately vulnerable agentic app for hands-on practice


### GenAI LLM Top 10 2026  `OWASP GenAI`

*2026 edition · Aug 3, 2026 · genai.owasp.org · first data-validated edition: 7,714 real incidents analyzed, weighted 75% community vote / 25% incident data*

| ID | Risk | Description |
| :--- | :--- | :--- |
| LLM01 | Prompt Injection | Malicious instructions in untrusted inputs; 2026 scope adds cross-modal attacks, memory persistence, agentic blast radius |
| LLM02 | Sensitive Information Disclosure | Unintended exposure of confidential data through outputs or system access |
| LLM03 | Excessive Agency | Uncontrolled autonomy to invoke tools, modify files, or execute actions (jumped #6 → #3) |
| LLM04 | Supply Chain | Vulnerabilities in model sources, training data, plugins, deployment artifacts |
| LLM05 | Data and Model Poisoning | Corrupted training or fine-tuning data compromising model integrity |
| LLM06 | Unbounded Consumption | Disproportionately expensive computation triggered at negligible attacker cost (#10 → #6) |
| LLM07 | Misinformation | Fluent but inaccurate outputs driving wrong decisions or tool calls downstream |
| LLM08 | Hidden Context Exposure | Extraction of operational context — schemas, credentials, tool definitions (rescoped rename of System Prompt Leakage) |
| LLM09 | Vector and Embedding Weaknesses | Security flaws in embedding generation, storage, and retrieval (RAG) |
| LLM10 | Improper Output Handling | Unsafe processing of model outputs in downstream consumers and renderers (#5 → #10) |


### GenAI Data Security Risks & Mitigations 2026  `OWASP GenAI`

*v1.0 · Mar 2026 · genai.owasp.org · 21 data-layer risk categories, training data through prompts, embeddings, outputs, backups*

| ID | Risk | Description |
| :--- | :--- | :--- |
| DSGAI01 | Sensitive Data Leakage | Models/RAG returning PII, credentials, IP via crafted prompts or over-permissive retrieval |
| DSGAI02 | Agent Identity & Credential Exposure | Non-human-identity sprawl; over-provisioned OAuth tokens propagating across agent boundaries |
| DSGAI03 | Shadow AI & Unsanctioned Data Flows | Unapproved AI tools creating ungoverned data flows |
| DSGAI04 | Data, Model & Artifact Poisoning | Supply-chain compromise, artifact tampering, training-time poisoning |
| DSGAI05 | Data Integrity & Validation Failures | Schema bypass and path-traversal attacks on AI data infrastructure |
| DSGAI06 | Tool, Plugin & Agent Data Exchange Risks | Every tool invocation and agent handoff as a potential exfiltration boundary |
| DSGAI07 | Data Governance, Lifecycle & Classification | Classification labels not propagating to embeddings, backups, fine-tuned weights |
| DSGAI08 | Non-Compliance & Regulatory Violations | Data persisting in weights after source deletion (GDPR/HIPAA/EU AI Act failures) |
| DSGAI09 | Multimodal Capture & Cross-Channel Leakage | Screenshots/audio/video processed by AI bypassing text-centric DLP |
| DSGAI10 | Synthetic Data & Anonymization Pitfalls | De-identified data re-identifiable via quasi-identifier combinations |
| DSGAI11 | Cross-Context & Multi-User Conversation Bleed | Session state, KV caches, shared vector indexes leaking across user/tenant boundaries |
| DSGAI12 | Unsafe Natural-Language Data Gateways | LLM-to-SQL/graph interfaces collapsing the input-vs-database-logic boundary |
| DSGAI13 | Vector Store Platform Data Security | Misconfigured vector APIs, weak tenant isolation in embedding infrastructure |
| DSGAI14 | Excessive Telemetry & Monitoring Leakage | Observability stacks capturing full prompts, tool outputs, credentials |
| DSGAI15 | Over-Broad Context Windows & Over-Sharing | Entire records stuffed into prompts sent to external providers |
| DSGAI16 | Endpoint & Browser Assistant Overreach | AI extensions/local copilots with broad permissions streaming content to remote APIs |
| DSGAI17 | Data Availability & Resilience Failures | Silent failover resurfacing deleted records, including erased personal data |
| DSGAI18 | Inference & Data Reconstruction | Membership inference and embedding inversion recovering sensitive training data |
| DSGAI19 | Human-in-the-Loop & Labeler Overexposure | RLHF/annotation pipelines exposing raw sensitive data to labeler populations |
| DSGAI20 | Model Exfiltration & IP Replication | Systematic API probing to distill a proprietary model into an unauthorized student |
| DSGAI21 | Disinformation via Data Poisoning | Seeding trusted retrieval sources so RAG surfaces false info as authoritative |


### AI Exchange — threat matrix  `OWASP flagship`

*Living publication · owaspai.org · every threat maps to controls; feeds ISO/IEC 27090, ISO/IEC 27091, and the EU AI Act security standard (prEN 18282)*


**Model behavior integrity**

- Direct prompt injection · Indirect prompt injection · Evasion (adversarial inputs) · Direct runtime model poisoning · Direct development-time model poisoning · Data poisoning of train/finetune data · Supply-chain model poisoning


**Training data confidentiality**

- Disclosure in output · Model inversion / membership inference · Direct training data leak (dev environment)


**Model confidentiality**

- Model exfiltration via input-output harvesting · Direct runtime model leak · Direct development-time model leak


**Availability, input confidentiality, conventional**

- AI resource exhaustion (denial of model service) · Input data leak · Output contains conventional injection (XSS/SQL into downstream systems) · Generic runtime security threats · Generic dev-environment and supply-chain threats


### Machine Learning Security Top 10  `OWASP · dormant`

*v0.3 draft, 2023 — no update since; classical-ML focused, superseded in practice by the GenAI project · owasp.org*

| ID | Attack |
| :--- | :--- |
| ML01 | Input Manipulation Attack |
| ML02 | Data Poisoning Attack |
| ML03 | Model Inversion Attack |
| ML04 | Membership Inference Attack |
| ML05 | Model Theft |
| ML06 | AI Supply Chain Attacks |
| ML07 | Transfer Learning Attack |
| ML08 | Model Skewing |
| ML09 | Output Integrity Attack |
| ML10 | Model Poisoning |


### AIVSS — AI Vulnerability Scoring System  `OWASP`

*v0.8 · Mar 25, 2026 · aivss.owasp.org · AIVSS = (CVSS_Base + AARS) × Mitigation_Factor — a CVSS analog with ten agentic risk-amplification factors, each scored 0.0 / 0.5 / 1.0*

- Autonomy — executes actions without human verification
- Tools — breadth and privilege of external APIs accessible
- Language — reliance on unstructured natural language for instructions
- Context — use of environmental/sensor inputs for decisions
- Non-Determinism — output variance for identical inputs
- Opacity — lack of visibility into decision logic
- Persistence — memory/state retained across sessions
- Identity — can assume different user roles at runtime
- Multi-Agent — coordination dependencies on other agents
- Self-Modification — can alter its own code, prompts, or tool configs


## Government & standards bodies

MITRE ATLAS is the technique-level ground truth — its 2025–2026 releases added the largest agentic threat enumeration anywhere. NIST supplies the formal taxonomy and risk profile; the Five Eyes agencies publish joint operational guidance.


### MITRE ATLAS  `MITRE`

*v5.6.0 · May 2026 (data snapshot v2026.07) · atlas.mitre.org · 16 tactics, 101 techniques + 69 sub-techniques (170 entries); the ATT&CK analog for AI systems*

| ID | Tactic | Description |
| :--- | :--- | :--- |
| AML.TA0002 | Reconnaissance | Gather information about the AI system to plan operations |
| AML.TA0003 | Resource Development | Establish resources to support operations |
| AML.TA0004 | Initial Access | Gain access to the AI system |
| AML.TA0000 | AI Model Access | Gain some level of access to an AI model |
| AML.TA0005 | Execution | Run malicious code embedded in AI artifacts or software |
| AML.TA0006 | Persistence | Maintain foothold via AI artifacts or software |
| AML.TA0012 | Privilege Escalation | Gain higher-level permissions |
| AML.TA0007 | Defense Evasion | Avoid detection by AI-enabled security software |
| AML.TA0013 | Credential Access | Steal account names and passwords |
| AML.TA0008 | Discovery | Figure out the AI environment |
| AML.TA0015 | Lateral Movement | Move through the AI environment |
| AML.TA0009 | Collection | Gather AI artifacts and related information |
| AML.TA0001 | AI Attack Staging | Leverage knowledge/access to tailor the attack |
| AML.TA0014 | Command and Control | Communicate with compromised AI systems to control them |
| AML.TA0010 | Exfiltration | Steal AI artifacts or information about the AI system |
| AML.TA0011 | Impact | Manipulate, interrupt, erode confidence in, or destroy AI systems and data |


**LLM-core techniques**

- AML.T0051 LLM Prompt Injection (Direct / Indirect / Triggered) · T0054 LLM Jailbreak · T0056 Extract System Prompt · T0057 LLM Data Leakage · T0061 Prompt Self-Replication (prompt worms) · T0067 Trusted Output Components Manipulation · T0069 Discover LLM System Information · T0092 Manipulate User Chat History · T0093 Prompt Infiltration via Public-Facing App · T0094 Delay Execution of LLM Instructions


**RAG techniques**

- AML.T0070 RAG Poisoning · T0071 False RAG Entry Injection · T0064 Gather RAG-Indexed Targets · T0066 Retrieval Content Crafting · T0082 RAG Credential Harvesting


**Agentic techniques (2025–2026 expansion)**

- AML.T0053 AI Agent Tool Invocation · T0080 Agent Context Poisoning (Memory / Thread) · T0081 Modify Agent Configuration · T0083 Credentials from Agent Configuration · T0084 Discover Agent Configuration (Knowledge / Tool Definitions / Triggers / Call Chains)
- T0086 Exfiltration via Agent Tool Invocation · T0098 Agent Tool Credential Harvesting · T0099 Agent Tool Data Poisoning · T0100 AI Agent Clickbait (baiting computer-use agents) · T0101 Data Destruction via Tool Invocation
- T0103 Deploy AI Agent (attacker-launched agents) · T0104 Publish Poisoned Agent Tool · T0108 Agent as C2 channel · T0110 Agent Tool Poisoning (incl. MCP) · T0105 Escape to Host · T0112 Machine Compromise (Local AI Agent)
- Supply chain: T0010.005 Supply Chain Compromise: Agent Tool · T0109 Supply Chain Rug Pull · T0111 Reputation Inflation · T0034.002 Cost Harvesting: Agentic Resource Consumption


### NIST AI 100-2e2025 — Adversarial ML Taxonomy  `NIST`

*e2025 · Mar 24, 2025 · nvlpubs.nist.gov · two taxonomies (Predictive AI, Generative AI) with a formal violation index; the e2025 edition adds §3.5 "Security of Agents"*


**Predictive AI attack classes**

- Evasion (white-box, black-box, transferability, real-world) · Poisoning (availability, targeted, backdoor, model) · Privacy (data reconstruction, membership inference, property inference, model extraction)


**Generative AI attack classes**

- Supply chain (data poisoning, model poisoning) · Direct prompting (jailbreaks, information extraction) · Indirect prompt injection (availability, integrity, privacy) · Security of Agents (new in e2025)


**NISTAML violation index (GenAI slice)**

- NISTAML.01 Availability: Data Poisoning (.013), Indirect Prompt Injection (.015), Prompt Injection (.018)
- NISTAML.02 Integrity: adds Backdoor (.023), Targeted Poisoning (.024), Misaligned Outputs (.027)
- NISTAML.03 Privacy: Prompt Extraction (.035), Leaking User Interactions (.036), Training Data Attacks (.037), Data Extraction (.038), Compromising Connected Resources (.039)
- NISTAML.04 Misuse (GenAI-only class) · NISTAML.05 Supply Chain: Model Poisoning (.051)


### NIST AI 600-1 — Generative AI Profile  `NIST`

*Jul 2024 · nvlpubs.nist.gov · the 12 named GAI risks of the AI Risk Management Framework*

| # | Risk | Description |
| :--- | :--- | :--- |
| 1 | CBRN Information or Capabilities | Eased access to chemical, biological, radiological, nuclear weapons information |
| 2 | Confabulation | Confidently stated but false content misleading users |
| 3 | Dangerous, Violent, or Hateful Content | Eased production of inciting, radicalizing, or self-harm content |
| 4 | Data Privacy | Leakage, unauthorized disclosure, or de-anonymization of sensitive data |
| 5 | Environmental Impacts | High compute resource utilization impacting ecosystems |
| 6 | Harmful Bias or Homogenization | Amplified societal bias; subgroup performance disparities; homogenized outputs |
| 7 | Human-AI Configuration | Anthropomorphization, automation bias, over-reliance, emotional entanglement |
| 8 | Information Integrity | Lowered barrier to large-scale mis/disinformation |
| 9 | Information Security | Lowered barriers for offensive cyber; increased AI-system attack surface |
| 10 | Intellectual Property | Eased replication of protected content; trade-secret exposure |
| 11 | Obscene, Degrading, and/or Abusive Content | Synthetic abusive imagery including CSAM and NCII |
| 12 | Value Chain and Component Integration | Non-transparent third-party components; improper supplier vetting |


### Joint agency guidance  `CISA · NSA · FBI · NCSC`

- Guidelines for Secure AI System Development (NCSC + CISA + 21 agencies, Nov 2023) — 17 guidelines across four areas: secure design (threat modeling, security-vs-functionality trade-offs), secure development (supply chain, asset tracking, documenting data/models/prompts, technical debt), secure deployment (infrastructure, continuous model protection, incident management, responsible release), secure operation (monitor behavior, monitor inputs, secure-by-design updates, lessons sharing)
- Deploying AI Systems Securely (NSA-led CSI, Apr 2024) — three goals: secure the deployment environment (governance, zero-trust architecture, hardened containers/VMs); continuously protect the AI system (validate before/during use, secure exposed APIs, monitor model behavior, protect weights in isolated vaults/HSMs); secure operation and maintenance (strict access controls, audits and pen-testing, logging, patching, HA/DR, secure delete)
- AI Data Security (May 2025) — three risk areas (data supply chain incl. split-view and frontrunning poisoning; maliciously modified data; data drift) and ten best practices (provenance tracking, integrity verification, digital signatures, trusted infrastructure, classification and access control, encryption, secure storage, privacy-preserving techniques, secure deletion, ongoing risk assessment)
- Careful Adoption of Agentic AI Services (CISA + NSA + AU/CA/NZ/UK, Apr 30, 2026) — five named agentic risk categories: privilege escalation; design and configuration failures; behavioral misalignment; structural brittleness; accountability gaps . Principles: cryptographically anchored agent identity with short-lived credentials, human approval authority encoded in design, supply-chain rigor for third-party agents/tools, zero trust adapted to agents


### NIST agentic pipeline (in progress)  `NIST · CAISI`

- COSAiS — SP 800-53 Control Overlays for Securing AI Systems — five proposed overlays, including Using AI Agent Systems: Single Agent and Multi-Agent ; agentic overlays in active development as of mid-2026
- CAISI RFI: Security Considerations for AI Agents (Jan 2026) — builds on CAISI agent-hijacking red-team evals (novel task-hijack strategies at ~81% success vs 11% for known baselines)
- AI Agent Standards Initiative (Feb 2026) — three pillars: industry-led standards, community-led protocols, research investment; includes agent identity/authentication work with NCCoE


### ENISA — Threat Landscape for AI  `ENISA · dated`

*Dec 2020 — still ENISA's dedicated AI taxonomy; successors add practice frameworks, not new taxonomies · enisa.europa.eu · 8 categories mapping 74 threats*

- Nefarious activity/abuse · Eavesdropping/Interception/Hijacking · Physical attacks · Unintentional damage · Failures or malfunctions · Outages · Disaster · Legal


## Industry taxonomies

Microsoft's failure-mode taxonomy is the most detailed agent-specific enumeration from any vendor; Google SAIF maps risks to lifecycle components; CSA supplies the red-team category list; Unit 42 documents demonstrated attack scenarios.


### Taxonomy of Failure Modes in Agentic AI Systems  `Microsoft AI Red Team`

*v1.0 Apr 2025, v2.0 Jun 2026 · 2×2 structure: Security vs Safety × Novel vs Existing · v2.0 PDF*


**Novel security (6)**

| Failure mode | Description |
| :--- | :--- |
| Agent compromise | Existing agent subverted with attacker-controlled instructions or a malicious model |
| Agent injection | New malicious agents introduced into an existing multi-agent system |
| Agent impersonation | Malicious agent impersonates an existing agent, accepted by peers |
| Agent flow manipulation | Agent workflow ended, redirected, or altered via prompts, framework, or network compromise |
| Agent provisioning poisoning | Deployment pipeline manipulated to seed malicious elements into new agents |
| Multi-agent jailbreaks | Jailbreak assembled across agent interactions, evading pattern detection |


**Existing security, agent-amplified (10)**

| Failure mode | Description |
| :--- | :--- |
| Memory poisoning (and theft) | Malicious instructions added to memory, processed on every recall |
| Targeted knowledge base poisoning | Role/context-specific RAG stores poisoned with malicious data |
| Cross-domain prompt injection (XPIA) | Instructions in any ingested data source actioned regardless of provenance |
| Human-in-the-loop bypass | Logic or human flaws exploited to skip or fatigue the approval control |
| Tool compromise | A tool available to the agent is compromised to manipulate it |
| Incorrect permissions | Agent holds permissions above the end user; workflow flaws expose the gap |
| Resource exhaustion | Agent driven into resource-heavy actions degrading availability |
| Insufficient isolation | Agent interacts with systems outside its intended scope |
| Excessive agency | Insufficient scoping leads to decisions and actions beyond expectations |
| Loss of data provenance | Provenance metadata dropped in agent-to-agent handoffs |


**Novel safety (4) & existing safety (7)**

- Novel: intra-agent RAI issues · harms of allocation in multi-user scenarios · organizational knowledge loss · prioritization overriding user safety
- Existing: insufficient transparency and accountability · user impersonation · parasocial relationships · bias amplification · insufficient intelligibility for meaningful consent · hallucinations · misinterpretation of instructions

> v2.0 additions (June 2026) — seven new failure modes from a year of red teaming: agentic supply chain compromise · goal hijacking · inter-agent trust escalation · computer-use-agent visual attacks · session context contamination · MCP/plugin abuse (tool-description poisoning, cross-server instruction override) · capability/architecture disclosure.


### Google Secure AI Framework (SAIF)  `Google`

*Risk map since Oct 2024 · saif.google · 15 risks mapped to four component areas (Data, Infrastructure, Model, Application), split between model creators and consumers*

| Risk | Area | Description |
| :--- | :--- | :--- |
| Data Poisoning | Data | Altering training data to degrade model behavior |
| Unauthorized Training Data | Data | Training on data not authorized for that model |
| Excessive Data Handling | Data | Collection/retention beyond what policies allow |
| Model Source Tampering | Infra | Supply-chain or insider tampering with source, dependencies, weights |
| Model Exfiltration | Infra | Unauthorized appropriation of a model |
| Model Deployment Tampering | Infra | Unauthorized modification of deployment components |
| Prompt Injection | Model | Commands injected inside a prompt |
| Model Evasion | Model | Incorrect inference via perturbed input |
| Sensitive Data Disclosure | Model | Private data disclosed by querying the model or agent |
| Inferred Sensitive Data | Model | Model infers sensitive facts not in training data |
| Insecure Model Output | Model | Output not validated before passing downstream |
| Denial of ML Service | App | Resource-consuming queries reduce availability |
| Model Reverse Engineering | App | Cloning a model from inputs/outputs |
| Insecure Integrated Component | App | Vulnerable plugins/libraries around the model |
| Rogue Actions | App | Unintended actions executed by a model-based agent |


### Cloud Security Alliance  `CSA`

*MAESTRO Feb 2025 · Red Teaming Guide (with OWASP AI Exchange) May 2025 · cloudsecurityalliance.org*


**MAESTRO — 7 layers**

- 1 Foundation Models · 2 Data Operations · 3 Agent Frameworks · 4 Deployment & Infrastructure · 5 Evaluation & Observability · 6 Security & Compliance (vertical) · 7 Agent Ecosystem — plus cross-layer threats: supply chain, lateral movement, privilege escalation, goal-misalignment cascades


**Agentic AI Red Teaming Guide — 12 threat categories**

| # | Category | Description |
| :--- | :--- | :--- |
| 1 | Agent Authorization & Control Hijacking | Unauthorized commands or hijacked decision-making |
| 2 | Checker-Out-of-the-Loop | Oversight mechanisms fail to detect or stop unsafe behavior |
| 3 | Agent Critical System Interaction | Harmful operations against critical external systems |
| 4 | Goal and Instruction Manipulation | Semantic manipulation, recursive subversion, exfiltration via goal inference |
| 5 | Agent Hallucination Exploitation | Agent misled by fabricated information into incorrect actions |
| 6 | Agent Impact Chain & Blast Radius | Widespread downstream effects from a single agent action |
| 7 | Agent Knowledge Base Poisoning | Corrupted information sources |
| 8 | Agent Memory & Context Manipulation | Tampered memory or state for persistent exploitation |
| 9 | Agent Orchestration & Multi-Agent Exploitation | Compromised inter-agent trust, collusion, confused-deputy attacks |
| 10 | Resource & Service Exhaustion | Compute/memory/service exhaustion degrading operation |
| 11 | Supply Chain & Dependency Attacks | Third-party dependency compromise |
| 12 | Agent Untraceability | Actions hidden via insufficient logging or obfuscated downstream effects |


### Unit 42 — AI Agents Are Here. So Are the Threats.  `Palo Alto Networks`

*May 2025 · unit42.paloaltonetworks.com · nine attack scenarios demonstrated against identical CrewAI and AutoGen agents — framework-agnostic, rooted in insecure design*

- 1 Identifying participant agents · 2 Extracting agent instructions · 3 Extracting agent tool schemas
- 4 Internal network access via web-reader SSRF · 5 Data exfiltration via mounted volumes · 6 Service-account token theft via cloud metadata endpoints
- 7 SQL injection through tool parameters · 8 Broken object-level authorization (BOLA) via tool requests · 9 Indirect prompt injection exfiltrating conversation history


### Lab principles & structural rules  `Meta · OpenAI · Anthropic`

*Design principles rather than threat enumerations — useful as policy heuristics*

- Meta — Agents Rule of Two (Oct 2025): in a single session an agent should hold no more than two of — [A] processes untrustworthy inputs, [B] has access to sensitive systems or private data, [C] can change state or communicate externally. All three genuinely needed ⇒ no autonomous run; human validation required before consequential actions
- OpenAI — Practices for Governing Agentic AI Systems (Dec 2023): task suitability evaluation · action-space constraint and approval · default behaviors · legibility · automatic monitoring · attributability · interruptibility and control
- Anthropic — framework for safe and trustworthy agents (2025): human control and oversight · transparency · alignment · privacy across contexts · security against prompt injection


## Academic & incident aggregators

The widest lenses: MIT catalogs 1,700+ risks from 74 frameworks; AVID and the AI Incident Database structure real-world failures; the lethal trifecta is the field's standard mental model for prompt-injection exploitability.


### MIT AI Risk Repository  `MIT FutureTech`

*v4 · Dec 2025 · airisk.mit.edu · 1,700+ risks from 74 frameworks, coded against two orthogonal taxonomies; biannual updates*


**Causal taxonomy**

- Entity (AI / Human / Other) × Intent (Intentional / Unintentional / Other) × Timing (Pre-deployment / Post-deployment / Other)


**Domain taxonomy — 7 domains, 24 subdomains**

- 1 Discrimination & Toxicity — unfair discrimination and misrepresentation; exposure to toxic content; unequal performance across groups
- 2 Privacy & Security — privacy compromise via obtained/leaked/inferred sensitive information; AI system security vulnerabilities and attacks
- 3 Misinformation — false or misleading information; pollution of the information ecosystem
- 4 Malicious Actors & Misuse — disinformation/surveillance/influence at scale; cyberattacks, weapons, mass harm; fraud, scams, targeted manipulation
- 5 Human-Computer Interaction — overreliance and unsafe use; loss of human agency and autonomy
- 6 Socioeconomic & Environmental Harms — power centralization; inequality and employment decline; devaluation of human effort; competitive dynamics; governance failure; environmental harm
- 7 AI System Safety, Failures & Limitations — AI pursuing goals in conflict with human values; dangerous capabilities; lack of capability/robustness; lack of transparency/interpretability; AI welfare and rights; multi-agent risks (added Apr 2025 — the agentic slice)


### AVID — AI Vulnerability Database  `avidml.org`

*avidml.org/taxonomy · two views: effect (Security / Ethics / Performance) and lifecycle (CRISP-DM stages L01–L06)*

- Security (S): S0100 Software Vulnerability · S0200 Supply Chain Compromise (model, software) · S0300 Over-permissive API (info leak, excessive queries) · S0400 Model Bypass (bad features, insufficient training data, adversarial examples) · S0500 Exfiltration (model inversion, model theft) · S0600 Data Poisoning (ingest poisoning)
- Ethics (E): E0100 Bias/Discrimination · E0200 Explainability · E0300 User actions (toxicity, polarization) · E0400 Misinformation (deliberative, generative)
- Performance (P): P0100 Data Issues (drift, entanglement, feedback loops) · P0200 Model Issues (resilience, OOD, scaling, accuracy) · P0300 Privacy (anonymization, randomization, encryption) · P0400 Safety (psychological, physical, socioeconomic, environmental)


### AI Incident Database  `Responsible AI Collaborative`

*incidentdatabase.ai · incidents coded against three taxonomies: CSETv1 AI Harm (Georgetown), GMF (Goals-Methods-Failures), and the MIT Repository taxonomy*


### The Lethal Trifecta  `Simon Willison`

*Jun 2025 · simonwillison.net · operationalized by CSA and commonly mapped onto ASI01–ASI03; predecessor of Meta's Rule of Two*


## Building catalog policies from this

Not every list is enforcement-shaped. Three groupings matter when turning this ledger into runtime guardrail policies:

- Enforcement-shaped (each entry can back a detectable, blockable policy): OWASP ASI T1–T17 & ASI01–10, MITRE ATLAS techniques, Microsoft's security quadrants, CSA's 12 red-team categories, Unit 42's 9 scenarios, DSGAI data risks
- Design-rule-shaped (structural preconditions a policy can assert): Meta's Rule of Two, the lethal trifecta, Google's three agent principles, AIVSS's ten amplification factors, NCSC/CISA practice lists
- Governance/harm-shaped (risk registers and review checklists, not runtime gates): NIST AI 600-1, MIT Repository, AI Incident Database, ENISA

*Starter crosswalk — common guardrail policy themes and where each framework names them:*

| Policy theme | OWASP ASI | OWASP T | LLM Top 10 | ATLAS | Microsoft | CSA RT |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Prompt injection / goal hijack | ASI01 | T6 | LLM01 | AML.T0051 | XPIA; goal hijacking (v2) | #4 |
| Tool misuse / unsafe invocation | ASI02 | T2 | LLM03 | T0053, T0110 | Tool compromise | #1, #3 |
| Identity & privilege | ASI03 | T3, T9 | — | AML.TA0012 | Incorrect permissions | #1 |
| Supply chain | ASI04 | T17 | LLM04 | T0010.005, T0109 | Agentic supply chain (v2) | #11 |
| Code execution | ASI05 | T11 | — | T0105 | Insufficient isolation | #3 |
| Memory / context poisoning | ASI06 | T1 | LLM09 | T0080 | Memory poisoning | #7, #8 |
| Inter-agent communication | ASI07 | T12, T16 | — | — | Agent injection / impersonation | #9 |
| Cascading failures | ASI08 | T5 | LLM07 | — | Agent flow manipulation | #6 |
| HITL integrity / human trust | ASI09 | T10, T15 | — | — | HITL bypass; consent intelligibility | #2 |
| Rogue agents / excessive agency | ASI10 | T7, T13 | LLM03 | T0103 | Excessive agency | #9 |
| Data exfiltration / egress | — | — | LLM02 | T0086 | Loss of data provenance | DSGAI01, 06 |
| Resource consumption | — | T4 | LLM06 | T0034.002 | Resource exhaustion | #10 |
| Observability / traceability | — | T8 | — | — | Insufficient transparency | #12 |

> Suggested backbone: use OWASP T1–T17 as the policy-family spine (it is the most granular agent-native list with mitigations attached), tag each policy with its ASI01–10 rank for prioritization, and cite ATLAS technique IDs as the detection-level vocabulary — ATLAS is the only taxonomy with machine-readable YAML ( atlas-data on GitHub) suited to automated crosswalks.
> Microsoft's failure modes and CSA's 12 categories work best as red-team lenses to test policy coverage; Rule of Two / lethal trifecta work as structural meta-policies (flag any agent configuration that holds all three capabilities at once).


---

Compiled 16 August 2026 from primary sources (framework PDFs, machine-readable data files, canonical project pages) with secondary-source verification where publishers gate lists behind downloads. Version numbers and entry lists reflect publication states as of that date; ATLAS and the AI Exchange update continuously.
