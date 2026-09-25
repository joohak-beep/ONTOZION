# ONTOZION — JARVIS Personal Intelligence OS

**JARVIS is a Windows-first, local-first personal intelligence operating system.**
It is designed to turn natural language into safe, verifiable computer work while
keeping the person's data, decisions, and long-term memory under personal control.

[Korean README](./README.md) · [Interactive blueprint](./jarvis-integrated-design-interactive.en.html) · [Architecture and memory design](./JARVIS_INTEGRATED_DESIGN_MEMORY_MODELS_2026-09-21.en.md)

**Brand structure:** `ONTOZION` is the project and operating-system brand; `JARVIS`
is the assistant/runtime identity that speaks, plans, and coordinates work inside it.
Filenames remain stable so existing links do not break.

> (Matrix metaphor: BOSS is Neo, local memory and reasoning are the Oracle, the optional cloud teacher is the Architect, the human-controlled harness is Zion, and Smith is a runaway self-expansion/privilege-escalation failure state.)

> Status: active design and engineering project. This repository is not a claim that
> general artificial intelligence, consciousness transfer, or a fully autonomous
> production system has already been achieved.
>
> Repository name: `ONTOZION`. Normal development and test work stays on `develop`;
> `main` is reserved for baseline and verified history.

## Why this project exists

The current economic transition is moving some human labor into software, model
inference, and token-based services. That can create enormous productivity, but it
can also concentrate memory, judgment, and productive power inside a small number of
platforms. A person may gain access to an impressive assistant while still not
owning the assistant's memory, policies, execution path, or future improvements.

JARVIS begins from a different premise:

> A personal AI should be useful enough to remove repetitive work, private enough
> to protect a family's data, and accountable enough that the human owner can
> understand, stop, correct, and inherit it.

The project focuses on the work people repeatedly postpone or dislike:
window and browser operations, file preparation, research, routine communication,
status checks, data organization, and other bounded tasks. The interface should be
simple: the BOSS speaks naturally, JARVIS interprets the request, a local harness
selects the smallest safe capability, and the result is shown through voice and
screen with evidence.

## ONTOZION's purpose: preserve and extend BOSS self-determination

ONTOZION exists to build a **BOSS-owned, distributed, mutually learning personal AGI
mesh** that preserves and extends the BOSS's ability to choose for himself. JARVIS
nodes on different computers can question, challenge, and teach one another, so
research, design, testing, and learning do not require the BOSS to answer every
intermediate question.

Freedom here does not mean that JARVIS may act without limits. It means that the BOSS
can understand alternatives, choose, refuse, and revoke. Approved nodes may share the
right to ask questions, but a question never grants execution power, administrator
access, or authority to rewrite the Constitution.

## Public scope and execution boundary

The only representative agent and operating runtime in this repository is
**ONTOZION/JARVIS**. No external general-purpose agent runtime is installed, executed,
or required. Every LLM, skill, MCP or ACP integration, tool, learning loop, and verifier
runs under the JARVIS harness. Multiple models on one computer are workers inside the
same JARVIS; multiple computers exchange only approved messages and evidence between
their own JARVIS nodes. A connected model or service never becomes the owner of
authority and cannot bypass the Constitution, authority broker, or verifier.

## The ultimate purpose: a family knowledge and values inheritance system

Human life is finite. The deepest reason for completing JARVIS is not merely to
build a convenient assistant or to win a benchmark. It is to give a spouse and
children a durable way to receive the creator's thinking, values, philosophy,
stories, decisions, and lessons after the creator is gone.

The long-term vision is a **personal intelligence inheritance system**:

1. Record the creator's reasoning, choices, mistakes, principles, stories, and
   working methods while life is being lived.
2. Preserve each record with provenance, date, context, confidence, and the
   creator's own words where possible.
3. Let the family search and question that archive in ordinary language.
4. Show evidence and uncertainty instead of pretending that a generated answer is
   the creator's exact voice or an unquestionable command.
5. Allow each child to keep, challenge, extend, or fork the knowledge according
   to their own life and consent.

The phrase **“spirit genome project”** is a metaphor for this accumulating,
human-readable body of values and lived knowledge. It does not claim that a
machine can literally copy a person's consciousness, soul, or identity. The goal
is an honest, evolving record that can help descendants live better without
turning the deceased person's archive into an unaccountable authority.

### Inheritance is knowledge, not unrestricted power

The inheritance mode must never silently transfer passwords, bank authority,
administrator rights, or the ability to make irreversible decisions. A future
family member may receive:

- stories, principles, preferences, and explanations;
- curated lessons and decision records;
- source documents and citations;
- a read-only or simulated JARVIS experience;
- clearly marked suggestions that can be accepted, rejected, or corrected.

Execution authority remains separately scoped, revocable, and legally reviewed.
The family should inherit a conversation with the creator's documented thinking,
not an invisible machine that can control their accounts.

## What JARVIS is

JARVIS is a harness around several model roles and deterministic tools:

- **BOSS** — the single human owner who sets values, approves high-risk scope,
  and can revoke or shut down the system.
- **Constitution** — versioned rules for privacy, authority, evidence, safety,
  learning, and inheritance.
- **Authority broker** — a small, fast enforcement layer that checks a scoped
  capability before any tool runs. It is not a second boss and cannot grant
  itself permission.
- **JARVIS orchestrator** — interprets requests, retrieves context, chooses a
  fast or deep execution lane, delegates bounded work, and reports what happened.
- **Local open-weight model** — private continuity, routine dialogue, retrieval,
  and offline operation.
- **Personal SLLM** — a compact model trained for the user's procedures, style,
  schemas, and routing, using approved and redacted traces.
- **Cloud teacher** — an optional high-capability model used for difficult cases,
  critique, and distillation targets; it is not the owner and does not receive
  private data by default.
- **Memory fabric** — short-term, medium-term, long-term, and fact-ledger memory
  with lexical, semantic, temporal, graph, procedure, and provenance indexes.
- **Device tools** — typed adapters for browser, files, shell, windows, screen,
  camera, phone, and approved external services.
- **Verifier and ledger** — post-condition checks, receipts, rollback metadata,
  privacy filtering, and an account of what was proposed, executed, and proven.

## Core architecture

~~~text
                         BOSS / human owner
                                  |
                           Constitution
                                  |
                           Authority broker
                                  |
                         Agent Supervisor
                                  |
        +--------------------- JARVIS ---------------------+
        |                 chief orchestrator               |
        |       intent · context · plan · delegation       |
        +------------------+----------------+---------------+
                           |                |
                    Memory + indexes   Model pool
                           |          local · SLLM · teacher
                           v                |
                    Typed device tools <----+
                           |
                    Verify · report · ledger
                           |
                  Learn only from approved traces
~~~

The model may propose. The harness decides whether a proposal is allowed. A tool
may execute. The verifier decides whether the intended post-condition is true.
The ledger records evidence. This separation is the main protection against a
fluent model gradually becoming an invisible administrator.

### Agent Supervisor: the harness control plane

The Agent Supervisor is integrated into the JARVIS harness but runs as a separate
protected process. It is not another conversational agent. It starts and stops
workers, enforces CPU/GPU/memory and time limits, renews heartbeats, isolates crashes,
and closes risky work when the authority broker or ledger is unhealthy.
The Authority Broker and Supervisor are sibling control-plane components, not a new
authority hierarchy. The Supervisor never creates or mints capabilities; only the
Authority Broker can issue them.

One computer runs one Supervisor and one JARVIS Orchestrator. The Supervisor manages
the model gateway, Agent Bus, MCP host, and worker agents. The Orchestrator makes plans;
the Supervisor manages execution lifecycle; only the Authority Broker can issue a
capability for a side effect. An agent's question or agreement never becomes authority.

Local MCP servers use child-process `stdio` where possible. Remote MCP connections use
authenticated HTTP. Internal agent messages use typed JSON over a local pipe or socket,
not free-form natural language. A failed worker is restarted or retired without taking
down the entire harness.

## The ontology harness: why the harness is the JARVIS OS

The harness is not a thin approval wrapper around a model. It is the operating
system made from an **ontology kernel, memory projections, action contracts, and
a verification/ledger bus**. The ontology gives people, devices, tasks, memories,
permissions, and evidence one shared language for relationships and time.

Every semantic memory tier follows that contract:

- **Short-term:** current BOSS, session, goal, target, approval, and tool state;
- **Medium-term:** projects, open tasks, decisions, failures, and recurring procedures;
- **Long-term:** stable people, devices, preferences, procedures, and values;
- **Fact ledger:** atomic claims, evidence, rebuttals, validity, and succession policy.

Every record has at least `stable_id`, `subject`, `predicate`, `object`, time,
source, confidence, sensitivity, owner, consent, evidence, and contradiction
fields. Vector, lexical, and graph indexes are searchable projections of the
canonical store, not the truth source.

The ontology path is:

~~~text
natural language → entity and relationship normalization → situation frame
→ memory, state, and evidence retrieval → Constitution and authority query
→ plan and capability token → device execution
→ observed event and outcome → projection refresh → report
~~~

This lets JARVIS answer more than “which text looks similar?” It can reason about
who did what, when, under which authority, and with which evidence. Ontology does
not require a large LLM on every request: hot session relations use RAM and
compiled queries, while embeddings, deduplication, and graph projections update
asynchronously so the fast lane remains fast.

## Audit ledger and optional blockchain sealing

Blockchain is not JARVIS's real-time execution engine. It is an optional external
seal that helps prove, after a task, that its record was not silently rewritten.
The hot path finishes locally; blockchain anchoring runs asynchronously in the
background.

- **Ledger:** an encrypted local store keeps proposed, approved, executed, observed, verified, and recovered events.
- **Seal:** the BOSS signature, Constitution version, policy version, plan fingerprint, and result fingerprint are recorded.
- **Anchor:** events can be batched into a Merkle root (one fingerprint for many records) and anchored to an external chain only when useful.
- **Privacy:** voice, embeddings, passwords, API keys, and raw memories never go on-chain; they remain encrypted locally.
- **Succession:** the system can prove when a BOSS-approved JARVIS version and succession policy existed, without silently granting execution authority to an heir.

If the chain is unavailable, JARVIS continues normal work. The sealing queue stays
local and retries later. A single personal computer may need only a signed
append-only ledger and encrypted backups; an external blockchain anchor is an
optional witness for cross-owner collaboration or inheritance evidence.

### Domains worth considering for blockchain anchoring

The test is not merely “is this record important?” It is: **must independent
parties verify the same record, and would a later rewrite cause loss or dispute?**

| Domain | Record | Why anchor it |
|---|---|---|
| Finance and securities | Order plan, BOSS approval, and fill fingerprints | Post-trade audit and dispute evidence |
| Constitution and succession | JARVIS version, policy change, and approval time | Prove which version was intended for heirs |
| Model and skill supply chain | Model hash, test results, and release version | Verify which model actually ran |
| Multiple JARVIS nodes | Node signatures, questions, answers, and result fingerprints | Compare records across machines |
| Consent and authority | Consent version, revocation time, and scope | Prove when a capability was allowed |

Personal notes, voice, embeddings, passwords, and raw financial records stay off
chain. Blockchain anchoring also does not replace a legal will, a notary, or a
financial institution's official records.

## CodePlan and local model roles

Having an LLM write a human paragraph and then making code parse that paragraph
adds latency and failure modes. In JARVIS, **the local model is the CodePlan
designer** and **the harness is the validator, compiler, and executor**.

- **Reflex lane:** a small local SLLM classifies intent and entities and selects a tested `skill_id`.
- **Design lane:** a stronger local open-weight model creates complex code, refactoring, and test plans.
- **Teacher lane:** only when local confidence is low or tests repeatedly fail, a cloud model critiques a redacted plan.

A CodePlan is a typed plan containing the repository, branch, files, symbols,
reason for change, tests, constraints, and capability. The harness permits only
tools such as `repo.search/read/patch/test/diff/rollback`; it never reinterprets
free text as an arbitrary shell command.

Independent reads, searches, and tests run in parallel, while writes to the same
file are serialized. Small repeated work is handled by the SLLM or a codemod;
new architecture, low confidence, or repeated failure is escalated to the
stronger local model or a selective cloud teacher. No model receives direct
administrator, financial, or unrestricted file authority.

## Constitution and safety principles

1. Human authority is explicit, scoped, revocable, and never inferred from silence.
2. Irreversible actions require a fresh approval token or a narrow pre-approved rule.
3. Credentials are vault references, never prompt text or ordinary log content.
4. Private data stays local by default; cloud transfer is a separate visible decision.
5. Tools use least privilege, typed inputs, bounded retries, and idempotency where possible.
6. Uncertainty becomes a pause, a smaller action, or a question—not invented permission.
7. Every mutation has a post-condition check; an exit code is not proof of success.
8. Failures are contained, reversible where possible, and recorded without hiding partial work.
9. Learning may improve routing and suggestions, but cannot rewrite the constitution.
10. Human override, shutdown, correction, export, and deletion remain available.

## Proactive housekeeping and financial safety

JARVIS may proactively find unused subscriptions, expiring coupons or points,
dormant accounts, and investment candidates, then **alert BOSS and prepare the work**.
Account closure, withdrawals, transfers, and securities orders remain behind a fresh
review and BOSS policy because they move money or may be hard to reverse. The goal is
not to ask about every click; it is to reduce questions inside a boundary BOSS has
written in advance.

Passwords and passkeys belong to the operating-system authenticator or local credential
store, not to the LLM context. JARVIS receives an account alias and a short capability
token instead of the raw secret. Finance tools separate read, draft, and execute verbs.
CAPTCHA, MFA, and identity checks are never bypassed.

The constitution is implemented as machine-checkable schemas, risk classes,
allow-lists, expiry rules, and verification tests. It is not left only in a
system prompt that a model might forget.

## Memory and retrieval

JARVIS uses the smallest useful context for each task:

| Tier | Purpose | Default lifetime |
|---|---|---|
| Short-term | Current turn, wake session, active tool state, interruption state | RAM and automatic expiry |
| Medium-term | Current project, open tasks, recent decisions, temporary goals | TTL and user-editable summaries |
| Long-term | Stable preferences, procedures, people, places, and lessons | Provenance and promotion review |
| Fact ledger | Atomic facts with source, confidence, sensitivity, expiry, and contradiction links | Explicit record lifecycle |

Parallel indexes provide fast recall:

- lexical search for exact commands and names;
- semantic search for paraphrases;
- temporal search for recent or “as-of” questions;
- graph search for people, projects, devices, and dependencies;
- procedure search for proven tool recipes and rollback steps;
- provenance and permission search for source, consent, and sensitivity.

No memory item becomes truth merely because a model generated it. The ledger
keeps source and uncertainty attached to the item.

## Local model, SLLM, and cloud-teacher loop

The project intentionally combines two local learning paths:

1. An open-weight local model provides general capability and privacy.
2. A personal SLLM learns stable procedures, user vocabulary, tool schemas, and
   routing from approved, redacted examples.

When a frontier cloud model is used, it acts as a teacher or critic:

approved trace → redact secrets and personal content → teacher critique →
distillation or SLLM training → offline replay tests → canary deployment →
BOSS approval for promotion

The cloud model is never allowed to silently become the memory owner. Model
weights, tokenizer licenses, dataset terms, and acceptable-use restrictions are
reviewed separately for every selected model. Quantization is accepted only after
measuring tool reliability, Korean and English quality, latency, and memory use on
the real JARVIS workload.

For open-weight models from any region, including China, “uncensored” is not
treated as a synonym for honest. Selection includes reproducible probes for
factual stability, omissions, uncertainty, multilingual parity, refusal behavior,
data leakage, and license obligations. The result is documented as a measured
limitation, not a political slogan.

## Privacy and data classes

| Class | Default route | Example |
|---|---|---|
| D0 public | Local or cloud | Public documentation |
| D1 personal | Local first | Preferences and project notes |
| D2 sensitive | Local only unless explicitly approved | Screen, mail, family records |
| D3 secret | Vault reference only | Passwords, tokens, private keys |

Raw audio, screenshots, credentials, exact locations, and private family records
are not ordinary Git artifacts. Public examples must be synthetic or redacted.

## What is implemented and what is still a goal

This repository contains active Windows-first engineering, design documents, and
interactive architecture material. Some capabilities remain design targets or
require physical-device validation:

- natural full-duplex voice, echo cancellation, and barge-in;
- long-stream continuity and provider failover;
- privacy-bounded screen and camera observation;
- cross-device Linux/macOS integration;
- inheritance workflows, succession rules, and family-facing UX;
- long-horizon learning without data leakage or value drift.

Claims about readiness must be backed by tests, logs, post-condition evidence,
and real-device acceptance gates. Fluent conversation alone is not proof of an
AGI system.

## Repository entry points

- Interactive English blueprint: `jarvis-integrated-design-interactive.en.html`
- Integrated design and memory document:
  `JARVIS_INTEGRATED_DESIGN_MEMORY_MODELS_2026-09-21.en.md`
- Korean project README: `README.md`
- Implementation audit: `INTEGRATED_DESIGN_AUDIT.md`
- Voice and memory contract: `VOICE_MEMORY_INTEGRATION.md`
- Voice service: `jarvis-wake-service/`
- Windows audio harness: `jarvis-audio-harness/`
- Learning cockpit: `jarvis-learning-os/`
- Windows packaging tools: `windows-package/`

To explore the design without installing a runtime, open the interactive HTML
file in a browser. It is self-contained and uses no external JavaScript bundle.

## Development and contribution rules

- Keep normal development and test work on the `develop` branch; preserve
  `main` for baseline or verified history.
- Never commit API keys, passwords, raw audio, screen pixels, exact coordinates,
  or unredacted family data.
- Treat provider output, model claims, and benchmark numbers as evidence-bearing
  statements. Label estimates and open limits.
- Add a regression test and a post-condition check for every new mutating tool.
- Keep model adapters replaceable; the memory and policy contracts are the stable
  project assets.
- Do not add automatic financial, legal, account, or destructive actions without
  an explicit risk policy and a human approval path.

## Open-source and license policy

Original source code and documentation in this repository are released under
the Apache License 2.0; see [LICENSE](./LICENSE). Apache-2.0 is used here because
it includes an explicit patent grant while keeping the project broadly reusable.
Before a public release, the copyright-holder line and any organization-specific
notices should be reviewed.

Third-party code, libraries, datasets, fonts, services, and model weights are
**not automatically relicensed** by this repository. Each component keeps its
upstream license and notice requirements. In particular:

- review the license of every open-weight model and tokenizer before download,
  redistribution, or commercial use;
- keep required attribution and NOTICE files;
- do not bundle model weights or private datasets unless their terms allow it;
- do not copy cloud-provider prompts, SDK assets, or proprietary documentation
  into this repository;
- publish only synthetic, redacted, or explicitly consented examples;
- if a file has a more specific license, that file's license controls.

The repository license grants software rights; it does not grant rights to a
person's likeness, voice, private memories, family records, or financial accounts.

## Ethical inheritance commitment

The family-inheritance goal is designed to preserve agency, not to create a
posthumous ruler. A descendant must be able to inspect sources, disagree with
the archive, correct it, export it, and stop using it. Any legal succession,
financial authority, account access, or estate decision belongs in a separate
human and legal process. JARVIS can help explain the creator's documented
thinking; it cannot prove that it is the creator.

## Disclaimer

JARVIS is experimental software. It can misunderstand speech, misread a screen,
produce an incorrect plan, or fail during a tool action. Do not use it for
unattended financial trading, medical decisions, legal decisions, or destructive
system administration without independent safeguards and human review.

## License

Copyright 2026 JARVIS Project Owner.

Licensed under the Apache License, Version 2.0. See [LICENSE](./LICENSE).
You may obtain a copy of the License at:
<https://www.apache.org/licenses/LICENSE-2.0>
