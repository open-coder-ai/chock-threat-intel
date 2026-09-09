<div align="center">

<img src=".github/logo.svg" alt="chock-threat-intel: a weekly digest of agentic-AI threats, each scored against an enforceable policy catalog — what a policy already enforces, what is only advisory, and what is still an open gap. The mark is chock's: a wheel held by a chock wedge." width="110">

# chock-threat-intel

**Weekly threat ledger the catalog's policies answer to.**

[the threat ledger →](reference/agentic-threat-ledger.md) ·
[weekly digests →](digests/) ·
[the framework →](https://github.com/open-coder-ai/chock) ·
[the policy catalog →](https://github.com/open-coder-ai/chock-catalog)

</div>

> **Unofficial compilation — verify at the source.** We are not an authoritative source for
> the frameworks cited here. Full disclaimer: [`docs/README.md`](docs/README.md).

## This week: [2026-09-04 digest](digests/2026-09-04.md)

MITRE ATLAS v2026.08 added 19 IDs; the two in scope for a repo-local coding-agent guard
are already covered:

| Entries | Catalog answer | Status |
| :--- | :--- | :--- |
| AML.T0118, .000–.001 (agent-to-agent comms) | `owasp-asi07-insecure-inter-agent-communication` | advisory |
| AML.T0016.004, T0017.002 (malicious agent tools) | `block-unpinned-agent-components` (hash-pinned `chock.lock` installs) | enforced (slice) |

## Coverage

Every new entry from this week's digest, mapped to a catalog policy where the digest names
one — never guessed:

| MITRE ATLAS v2026.08 entry | Catalog policy | Status |
| :--- | :--- | :--- |
| AML.T0118, T0118.000–.001 | `owasp-asi07-insecure-inter-agent-communication` | advisory |
| AML.T0016.004, T0017.002 | `block-unpinned-agent-components` | enforced (slice) |
| AML.T0116, T0117, T0119–T0128, T0016.003, T0017.001 (14 IDs) | — | out of scope — adversary tradecraft outside a repo-local coding-agent guard |

The full historical mapping lives in
[`reference/agentic-threat-ledger.md`](reference/agentic-threat-ledger.md), refreshed in
place by each sweep.

## How the ledger is updated

- **Weekly sweep.** An automated review checks the published threat frameworks (OWASP
  GenAI/ASI, MITRE ATLAS, NIST, CISA, CSA, vendor taxonomies) and the week's disclosed agent
  vulnerabilities, and drafts a delta digest against the running baseline.
- **Human review before publish.** Every digest lands as a pull request, read and approved
  by a maintainer before it merges. Nothing on `main` is unreviewed automation output.
- **Coverage honesty.** Each entry is tagged `enforced` (a gate blocks a slice of it),
  `advisory` (rule text an agent reads), or `policy wanted` (nothing covers it, linked to
  a contributor issue) — the catalog's own tiers.

More on reading a digest and contributing a policy: [`docs/README.md`](docs/README.md).

## Part of open-coder-ai

| | |
|---|---|
| [agentseam](https://github.com/open-coder-ai/agentseam) | the primitives — one handler API and a verified capability matrix across 16 agents |
| [chock](https://github.com/open-coder-ai/chock) | the compiler — one policy into git hooks, CI gates and native pre-tool hooks |
| [chock-catalog](https://github.com/open-coder-ai/chock-catalog) | the policies — 39, each labelled enforced or advisory, with replayed evals |
| [context-report](https://github.com/open-coder-ai/context-report) | the evidence — a signed report of whether an agent artifact actually works |
| [chock-threat-intel](https://github.com/open-coder-ai/chock-threat-intel) | the threat ledger the catalog's policies answer to |
| chock-{claude,cursor,copilot,codex}-plugins | the catalog, packaged for each agent's plugin format (generated) |
| chock-quickstart · chock-example | template repos: what `chock init` leaves behind, and a full adoption |

Other ways in, none of which need code:

- **Report a miss.** A published advisory or framework entry the ledger lacks: open an
  issue with the canonical link and the publisher's version and date, and the next weekly
  sweep picks it up.
- **Challenge a coverage tag.** `enforced` claims a gate blocks a slice of the threat. A
  case the gate lets through is a finding for the
  [catalog](https://github.com/open-coder-ai/chock-catalog/issues/new/choose), and the tag here follows the catalog.
- **Read a digest before it merges.** Every digest lands as a pull request. A review comment
  from someone who knows the source better than we do is what the human-review step is for.

Conventions for all of the above are in [CONTRIBUTING.md](CONTRIBUTING.md).

## Part of the open-coder-ai family

Everything under [open-coder-ai](https://github.com/open-coder-ai) is built on one rule: a claim must match a
mechanism. Where this repository sits among the others:

| Repository | What it is |
| :--- | :--- |
| [chock](https://github.com/open-coder-ai/chock) | The framework: write a policy once, enforce it on git hooks, CI, and every agent |
| [chock-catalog](https://github.com/open-coder-ai/chock-catalog) | The policies, each graded by what it actually enforces |
| [agentseam](https://github.com/open-coder-ai/agentseam) | The primitives layer under chock: one handler API over every agent's hooks, with a capability matrix that carries its provenance |
| [context-report](https://github.com/open-coder-ai/context-report) | A signed report format for whether a plugin, hook, skill or `AGENTS.md` actually works |
| [chock-claude-plugins](https://github.com/open-coder-ai/chock-claude-plugins) · [copilot](https://github.com/open-coder-ai/chock-copilot-plugins) · [cursor](https://github.com/open-coder-ai/chock-cursor-plugins) · [codex](https://github.com/open-coder-ai/chock-codex-plugins) | The catalog compiled into each client's native plugin format; generated only, rebuilt and diffed in CI |
| [chock-quickstart](https://github.com/open-coder-ai/chock-quickstart) · [chock-example](https://github.com/open-coder-ai/chock-example) | Template repositories: exactly what `chock init` leaves behind, and a working adoption with one policy per layer |

## License

Apache-2.0 — see [LICENSE](LICENSE). Threat framework names and identifiers belong to
their publishers (OWASP, MITRE, NIST, and others); each digest links its sources.
