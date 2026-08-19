# Coverage crosswalk — what the ledger enumerates vs. what Chock implements

The [ledger](agentic-threat-ledger.md) lists everything the published frameworks warn
about. This file answers the other question: for each entry, what does the
[chock-catalog](https://github.com/open-coder-ai/chock-catalog) actually do about it
today? Statuses use the catalog's own honesty tiers, plus one this file adds:

- **enforced (slice)** — a deterministic gate or guard blocks a concrete slice of the
  threat. Never the whole threat; the named slice only.
- **advisory** — committed rule text every agent reads. Real influence, no mechanism.
- **`policy wanted`** — in scope, nothing covers it; linked to a contributor issue.
- **out of scope** — not addressable by a repo-local tool governing coding agents, and
  declared so rather than silently omitted.

## Scope statement, first

Chock governs **coding agents working in a git repository**. Its reach is what a repo
can carry: pre-tool-use guards, git hooks, a CI gate, committed instruction files.
Threats that live in training pipelines, model weights, RAG/vector infrastructure,
inference platforms, or organization-level identity systems are out of scope by
architecture — a repo cannot enforce there. They are listed anyway, because a coverage
report that omits what it cannot do is the failure mode this project exists to avoid.

## OWASP Agentic Top 10 (ASI01–10)

| ID | Risk | Catalog answer | Status |
| :--- | :--- | :--- | :--- |
| ASI01 | Agent Goal Hijack | `owasp-asi01-agent-goal-hijack`, `injection-defense`; slice: `block-invisible-unicode` (Trojan-Source-class hidden text) | enforced (slice) |
| ASI02 | Tool Misuse & Exploitation | `owasp-asi02-tool-misuse`; slice: `block-destructive-commands` | enforced (slice) |
| ASI03 | Identity & Privilege Abuse | `owasp-asi03-identity-privilege-abuse`; slices: `block-wildcard-iam`, `block-wildcard-agent-permissions` | enforced (slice) |
| ASI04 | Agentic Supply Chain | `owasp-asi04-…`; slices: `block-unpinned-agent-components`, `verify-dependency-exists`, `scan-secrets` | enforced (slice) |
| ASI05 | Unexpected Code Execution | `owasp-asi05-…`; slice: `block-unsafe-code-execution` | enforced (slice) |
| ASI06 | Memory & Context Poisoning | `owasp-asi06-memory-context-poisoning`, `memory-discipline` | advisory |
| ASI07 | Insecure Inter-Agent Communication | `owasp-asi07-insecure-inter-agent-communication` | advisory |
| ASI08 | Cascading Failures | `owasp-asi08-cascading-failures`; slice: `verify-dependency-exists` | enforced (slice) |
| ASI09 | Human-Agent Trust Exploitation | `owasp-asi09-human-agent-trust` | advisory |
| ASI10 | Rogue Agents | `owasp-asi10-rogue-agents` | advisory |

## OWASP Agentic Threats T1–T17

Maintained as the spine of every weekly digest — current scoring in
[digests/2026-08-16-baseline.md](../digests/2026-08-16-baseline.md): 6 enforced in
slice, 9 advisory, T4 (resource overload) and T8-as-a-policy open. The framework
roadmap items for both gaps are public: rate-limit/budget gate kind and the
tamper-evident gate log ([chock#33](https://github.com/open-coder-ai/chock/issues/33)).

## OWASP GenAI LLM Top 10 (2026)

| ID | Risk | Catalog answer | Status |
| :--- | :--- | :--- | :--- |
| LLM01 | Prompt Injection | `injection-defense`; slice: `block-invisible-unicode` | enforced (slice) |
| LLM02 | Sensitive Information Disclosure | slices: `scan-secrets` (staged credentials), `protect-commit-privacy` (process leakage into history) | enforced (slice) |
| LLM03 | Excessive Agency | slices: `block-no-verify`, `block-destructive-commands`, `protect-agent-config`, `protect-main-branch` — the guard family exists to bound agency | enforced (slice) |
| LLM04 | Supply Chain | as ASI04 | enforced (slice) |
| LLM05 | Data & Model Poisoning | training-time; a repo tool cannot reach it | out of scope |
| LLM06 | Unbounded Consumption | needs the budget gate kind ([chock#33](https://github.com/open-coder-ai/chock/issues/33)) | `policy wanted` |
| LLM07 | Misinformation | `agent-discipline` | advisory |
| LLM08 | Hidden Context Exposure | slice: `protect-agent-config` (agent config/context files are protected paths); `scan-secrets` for credentials in them | enforced (slice) |
| LLM09 | Vector & Embedding Weaknesses | RAG infrastructure | out of scope |
| LLM10 | Improper Output Handling | downstream consumers; partial influence via `agent-discipline` only | out of scope (advisory edge) |

## MITRE ATLAS — coding-agent-relevant techniques

| Technique | Name | Catalog answer | Status |
| :--- | :--- | :--- | :--- |
| AML.T0051 | LLM Prompt Injection | `injection-defense`; slice: `block-invisible-unicode` | enforced (slice) |
| AML.T0080 | Agent Context Poisoning | `memory-discipline`, `owasp-asi06-…` | advisory |
| AML.T0081 | Modify Agent Configuration | `protect-agent-config` (approval-marker guard over agent config paths) | enforced (slice) |
| AML.T0083 | Credentials from Agent Configuration | `scan-secrets` | enforced (slice) |
| AML.T0086 | Exfiltration via Tool Invocation | [`block-unapproved-egress`](https://github.com/open-coder-ai/chock-catalog/issues/2) | `policy wanted` |
| AML.T0098 | Agent Tool Credential Harvesting | `scan-secrets` slice; broader harvesting | advisory |
| AML.T0101 | Data Destruction via Tool Invocation | `block-destructive-commands` | enforced (slice) |
| AML.T0105 | Escape to Host | sandboxing concern; guards raise the default-path floor only | out of scope (declared honestly in every guard's prose) |
| AML.T0109 | Supply-Chain Rug Pull | `block-unpinned-agent-components`; hash-pinned catalog installs (`chock.lock`) | enforced (slice) |
| AML.T0110 | Agent Tool Poisoning (incl. MCP) | [`verify-mcp-allowlist`](https://github.com/open-coder-ai/chock-catalog/issues/1) | `policy wanted` |
| AML.T0112 | Machine Compromise via Local Agent | `block-unsafe-code-execution`, `block-destructive-commands` slices | enforced (slice) |

## The rest of the ledger, honestly

- **OWASP Data Security (DSGAI01–21)** — mostly platform/data-pipeline scope. In
  reach: DSGAI02 (credential exposure → `scan-secrets`, `protect-agent-config`),
  DSGAI06 (tool exchange boundaries → the guard family). The other nineteen are out of
  scope for a repo-local tool.
- **OWASP AI Exchange, NIST AI 100-2/600-1, ENISA** — taxonomy/control matrices; the
  builtin compliance frameworks in `chock check` report against NIST AI RMF and EU AI
  Act claims per policy. Model/training attack classes: out of scope.
- **AIVSS** — a scoring system, not a threat list; useful vocabulary for policy prose.
- **Microsoft Failure Modes, Google SAIF, CSA, Unit 42** — map onto the T-spine above;
  the digest tracks them through it rather than duplicating rows.
- **MIT Risk Repository, AVID, AI Incident Database** — aggregators; the weekly sweep
  reads them for new coding-agent incidents.

## The honest totals

Of the ledger's 400+ entries, the slice a repo-local governance tool can
deterministically enforce is small — today: **12 enforced policies covering slices of
~14 framework entries, ~20 advisory policies, 3 open `policy wanted` items, everything
else declared out of scope**. That statement is the product working as designed: the
alternative — a matrix of green checkmarks across all 22 frameworks — is exactly the
overclaim this repo exists to refuse. Want a gap closed? The
[`policy wanted` issues](https://github.com/open-coder-ai/chock-catalog/issues) are
the front door.
