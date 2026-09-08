# chock-threat-intel docs

Prose moved here from the root `README.md`, verbatim, so the landing page can stay to one
screen.

## Disclaimer

This repository is an independent, unofficial compilation. We are **not** an
authoritative or authorized source for any of the frameworks, taxonomies, or
advisories referenced here. All threat data originates from the third-party
publications cited inline (OWASP, MITRE, NIST, CISA, and the other named
publishers); we aggregate and summarize it for the convenience of mapping catalog
policies against it. Errors, omissions, and staleness are possible — **always
fact-check against the cited canonical source before relying on any entry**, and
treat the publisher's version as the one that governs. Framework names, entry IDs,
and trademarks belong to their respective owners; their use here is referential and
implies no affiliation or endorsement. This content is provided as-is, without
warranty of any kind, and is not security, legal, or compliance advice.

## Reading a digest

One file per week in [`../digests/`](../digests/), newest first. Entries reference the OWASP
Agentic Threats spine (T1–T17) and MITRE ATLAS technique IDs, so the same threat is
traceable across frameworks and across weeks.

## Contributing a policy from a `policy wanted` entry

1. Open the linked issue and claim it.
2. `chock init` a scratch repo and ask your agent to run the `policy-init` skill — it
   scaffolds a conformant policy folder.
3. Follow the catalog's
   [contributing guide](https://github.com/open-coder-ai/chock-catalog/blob/main/CONTRIBUTING.md):
   a policy claims only what it can do, and evals are the argument.

Corrections are contributions too — including "this entry overstates the threat" and
"this coverage tag claims too much". Especially those.
