# ONTOZION — JARVIS Personal Intelligence Operating System

## Integrated Blueprint · Memory Layers · Retrieval · Open-Weight Model Selection

- Date: 2026-09-21
- Status: target architecture
- Interactive version: [JARVIS interactive blueprint](./jarvis-integrated-design-interactive.en.html)

> This is a design document, not a claim that every component is currently implemented or verified on every device. Each device, model, and action path needs its own acceptance tests.

## 1. ONTOZION's purpose and one-sentence definition

ONTOZION exists to build a **BOSS-owned, distributed, mutually learning personal AGI
mesh** that preserves and extends the BOSS's self-determination. JARVIS instances on
different computers may question and challenge one another, exchanging evidence from
their own memories, models, and tools instead of making the BOSS answer every
intermediate question.

Freedom here means that the BOSS can understand alternatives, choose, refuse, and
revoke. It does not give JARVIS unlimited autonomy. Question rights may be distributed
to approved nodes, but a question never becomes execution authority or permission to
rewrite the Constitution.

## 1.1 Public scope and execution boundary

The representative agent and operating runtime in this design are **ONTOZION/JARVIS
only**. No external general-purpose agent runtime is installed, executed, or required.
Every LLM, skill, MCP or ACP integration, tool, learning loop, and verifier runs under
the JARVIS harness. Multiple models on one computer are workers inside one JARVIS;
multiple computers exchange only approved messages and evidence between their own
JARVIS nodes. A connected model or service never owns authority and cannot bypass the
Constitution, authority broker, or verifier.

## 1.2 One-sentence definition

JARVIS is not only a voice chatbot. It is a personal intelligence operating system in which BOSS owns the goals and authority, JARVIS understands and plans, constrained capabilities operate devices, verifiers confirm real outcomes, and an append-only record becomes the foundation for learning.

```text
BOSS owns the goal and the authority.
The Constitution defines the non-negotiable boundaries.
JARVIS understands, plans, and coordinates.
The authority broker decides whether an action is allowed.
Device agents perform the allowed action.
The verifier checks what really happened.
The ledger records the evidence.
The learning loop makes the next run faster and better.
```

The central rule is **parallel thinking, single execution**. Several models may propose plans, but only one plan that passes policy and verification is allowed to commit a real side effect.

## 2. Full architecture

```text
                         ┌────────────────────┐
                         │       BOSS         │
                         │ owner · final say  │
                         └─────────┬──────────┘
                                   │ sign / approve
                         ┌─────────▼──────────┐
                         │  JARVIS Constitution│
                         │ non-negotiable law │
                         └─────────┬──────────┘
                                   │ compile into policy
                         ┌─────────▼──────────┐
                         │ Authority broker   │
                         │ deterministic gate │
                         └─────────┬──────────┘
                                   │ allowed capabilities only
                         ┌─────────▼──────────┐
                         │ Agent Supervisor   │
                         │ lifecycle/resources│
                         └─────────┬──────────┘
                                   │ execution coordination
┌──────────────┐       ┌──────────▼──────────┐       ┌──────────────┐
│ voice / UI   │──────▶│ JARVIS orchestrator │◀──────│ memory store │
│ phone input  │       │ understand / plan   │       │ private data │
└──────────────┘       └──────────┬──────────┘       └──────────────┘
                                   │ plan
                         ┌─────────▼──────────┐
                         │ Model router       │
                         │ SLLM / open-weight│
                         │ cloud teacher     │
                         └─────────┬──────────┘
                                   │ capability call
                         ┌─────────▼──────────┐
                         │ Windows/macOS/Linux│
                         │ browser / CLI / app│
                         └─────────┬──────────┘
                                   │ real outcome
                         ┌─────────▼──────────┐
                         │ Verifier           │
                         │ evidence and state │
                         └─────────┬──────────┘
                                   │
                         ┌─────────▼──────────┐
                         │ Ledger and learning│
                         │ replay / audit     │
                         └────────────────────┘
```

### 2.1 Harness control plane and Agent Supervisor

The Agent Supervisor is not a second JARVIS. It is a deterministic operating layer
integrated into the harness. It does not replace the JARVIS Orchestrator's goals or
judgment; it manages agent lifecycle, resources, isolation, cancellation, and restart.
The Authority Broker and Supervisor are sibling control-plane components inside the
harness, not a new authority hierarchy. The Supervisor never creates or mints a
capability; that authority remains exclusively with the Authority Broker.

```text
Harness OS
├─ Authority Broker : mints or denies capabilities; final veto on side effects
├─ Agent Supervisor : registry, admission, heartbeat, timeout, kill, and quotas
├─ JARVIS Orchestrator : interprets BOSS requests, retrieves memory, plans, coordinates
├─ Model Gateway : SLLM, local open-weight, and optional cloud teacher
├─ Agent Bus : typed agent messages and task state
├─ MCP Host : local stdio tools and authenticated remote HTTP tools
└─ Ledger : append-only request, authority, execution, verification, and recovery record
```

One computer runs one Supervisor and one Orchestrator. The Supervisor starts first as
a protected Windows Service, launchd job, or systemd service, then manages the
Orchestrator, inference server, MCP servers, and worker agents as child processes.
If the Supervisor or Authority Broker is unhealthy, risky external actions fail closed.
If one worker crashes, the other workers and the harness ledger remain available.

Every agent manifest includes an `agent_id`, model, capabilities, data class, memory
scope, CPU/GPU/memory quotas, maximum runtime, and a kill handle. An unregistered agent
does not run. Agent questions, consensus, or ACP messages never become authority; only
the Authority Broker can mint a short-lived capability bound to a target and scope.

### JARVIS versus the authority broker

- JARVIS is the representative agent that reasons and plans.
- The broker does not debate or invent goals; it checks authority.
- JARVIS never outranks the broker for side effects.
- The broker must be a small deterministic program, not another autonomous LLM.

## 3. Constitutional layer

### Non-negotiable principles

1. BOSS is the sole owner.
2. JARVIS assists BOSS but does not replace BOSS's values or ownership.
3. Private data stays local by default.
4. JARVIS may use only explicitly registered capabilities.
5. Irreversible actions require a separate approval path.
6. Important actions carry a plan, authority, result, and evidence.
7. Models are replaceable; memory and skills are not locked to one vendor.
8. JARVIS cannot grant itself more authority.
9. JARVIS cannot modify the Constitution, ownership, or succession rules.
10. An unverified outcome is `UNKNOWN`, never silently treated as success.

The Constitution is not only a long prompt. Minimum privilege, approval, expiry, allowed paths, and emergency stop rules must also exist as executable policy.

## 4. Harness components

| Component | Responsibility | Boundary |
|---|---|---|
| Input/session manager | Combine voice, text, and screen input into a session | Does not rewrite the user's intent |
| Memory manager | Retrieve the private context needed for this task | Does not expose secrets without policy |
| Model router | Choose a model by task, privacy, and latency | Does not let models call tools directly |
| Planner | Break a goal into steps and conditions | Does not grant authority |
| Authority broker | Check capability, target, scope, expiry, and approval | Does not invent goals |
| Executor | Operate a browser, CLI, API, or app | Does not open an arbitrary admin shell |
| Verifier | Check the screen, file, state, and response | Does not trust a success sentence alone |
| Ledger/learning | Store events, skills, tests, and model versions | Does not silently rewrite the production model |

### 4.1 Ontology harness — the semantic kernel of the JARVIS OS

If the harness is described only as an authority broker or a collection of tools,
the central JARVIS OS function is missing. The complete harness is the combination
of an **ontology kernel, memory projections, action contracts, and a
verification/ledger bus**. An ontology is not just a taxonomy; it is a shared
contract that lets the machine query what exists, how things relate, when a claim
is valid, what evidence supports it, and which authority permits an action.

#### Layers inside the JARVIS OS

| Layer | Role | Relationship to the ontology |
|---|---|---|
| JARVIS chief agent | Understand, plan, coordinate, and report | Builds and queries an ontology situation frame |
| Ontology kernel | Canonical objects, relationships, time, state, and evidence | Semantic source shared by every memory tier and executor |
| Memory manager | Retrieve, promote, correct, and forget context | Graph, lexical, and vector indexes are projections |
| Authority broker | Check capability, target, scope, expiry, and approval | Denies when the required ontology relation is unclear |
| Executor/device agent | Operate browser, CLI, API, and apps | Performs only declared capabilities and reports events |
| Verifier/ledger | Store observed outcomes, evidence, tests, and learning | Compares ontology state before and after execution |

JARVIS does not outrank the broker in authority. **The harness is the OS as a
whole**. The chief agent is its planning process; the ontology kernel and
authority broker are deterministic layers below the model that enforce meaning
and side-effect boundaries.

#### Core ontology objects and relationships

| Object | Representative relationships | Harness purpose |
|---|---|---|
| `Person / BOSS / FamilyMember` | `owns` · `governs` · `inherits_from` · `consents` | Separates the owner, successors, and consent. Knowledge inheritance is not automatic execution inheritance. |
| `Agent / Model / Tool / Device` | `runs_on` · `can_invoke` · `observes` · `reports_to` | Tracks which model invokes which tool on which device instead of allowing an arbitrary shell call. |
| `Task / Skill / Event / Outcome` | `contains` · `derived_from` · `caused` · `verified_as` | Connects a spoken request to an execution graph and a reusable, tested skill. |
| `Capability / Policy / Approval` | `authorized_by` · `targets` · `scoped_to` · `expires_at` | Defines scope, target, expiry, and approval. An unclear relation is a denial. |
| `MemoryItem / Evidence / Source` | `asserts` · `supports` · `contradicts` · `supersedes` | Preserves source, contradiction, and freshness instead of silently overwriting facts. |

#### Ontology contract for every semantic memory tier

Every memory write shares at least this shape:

~~~text
stable_id · subject · predicate · object
valid_from · valid_to · created_at · source_ref
confidence · sensitivity · owner_id · consent_ref
evidence_ref · contradiction_refs · schema_version
~~~

| Tier | Ontology frame | Indexing and retention |
|---|---|---|
| Short-term | Current BOSS, session, goal, target, pending approval, and tool state | RAM keys, exact state queries, session expiry |
| Medium-term | Projects, open tasks, decisions, failures, and recurring procedures | Time, project, task ID, graph relations, TTL |
| Long-term | Stable preferences, people, devices, procedures, and values | Graph, vector, and lexical retrieval; promotion review |
| Fact ledger | Atomic claims, evidence, rebuttals, validity, and succession policy | `predicate`, `as-of`, and `provenance` queries; correction propagation |

The vector database is not the truth source for memory. Vector, BM25, and graph
indexes are projections that can be rebuilt from the same canonical event store.
Contradictions remain explicit relationships instead of being silently deleted.

#### Ontology path from language to execution

~~~text
natural language
  → entity and relationship normalization
  → situation frame (actor · goal · target · time · state · authority)
  → semantic memory + exact state + evidence in parallel
  → Constitution and authority query
  → plan + capability token
  → device execution
  → observed event, outcome, and evidence in the ledger
  → graph, vector, and lexical projections refreshed asynchronously
  → voice and UI report
~~~

#### Preserve performance while making meaning explicit

Ontology does not mean calling a large LLM for every action.

1. Keep an append-only canonical event store and validate stable IDs and types first.
2. Serve the active session and hot relationships from RAM and compiled policy queries.
3. Prefer deterministic code for entity linking, time normalization, and authority checks.
4. Run embeddings, deduplication, and graph projection outside the critical execution path.
5. Call a tested ontology-backed `skill_id` directly for routine work.

#### Ontology acceptance gates

- Every semantic memory write has a stable ID, relationship, source, and time.
- Every index can be deleted and rebuilt from the canonical store.
- Fact conflicts are preserved as `contradicts` rather than overwritten.
- Missing or expired capability relations prevent tool execution.
- `forget/correct/wipe` propagates to the ledger and every projection.
- Family inheritance may expand knowledge access, but never expands execution authority automatically.

### 4.2 CodePlan and local model roles

Having an LLM write a human paragraph and then making code parse that paragraph
creates unnecessary latency and failure modes. In JARVIS, **the local model is the
CodePlan designer** and **the harness is the validator, compiler, and executor**.
Source code remains human-readable text, but which files change, why they change,
and which tests must pass are carried through a typed plan.

#### Three model lanes

| Lane | Role | Use when |
|---|---|---|
| Reflex lane | Small local SLLM for intent classification, entity linking, and tested `skill_id` selection | Repeated work, small edits, low risk |
| Design lane | Strong local open-weight model for architecture, refactoring, and test plans | New features, multi-file changes, deeper reasoning |
| Teacher lane | Selective cloud model for critique and hard-case help using redacted plans | Low local confidence, schema failure, repeated test failure, or new architecture |

The cloud model never receives direct shell, file, or administrator authority.
Sensitive source and memory stay local by default; if a teacher call is needed,
send only the minimum redacted context and CodePlan. An open-weight model is not
“free”: evaluate its model, tokenizer, dataset, and quantization licenses as well
as the hardware and power cost.

#### Minimum CodePlan contract

~~~json
{
  "kind": "code_plan",
  "request_id": "uuid",
  "repository": "jarvis",
  "branch": "develop",
  "files": [
    {"path": "src/router.py", "symbols": ["route_request"], "operation": "patch"}
  ],
  "tests": ["python -m compileall src", "tests/test_router.py"],
  "constraints": ["no_constitution_change", "no_admin_shell"],
  "capability": "repo.patch",
  "approval": "policy_scoped"
}
~~~

#### Harness compile and execution steps

1. Validate the CodePlan JSON Schema and version.
2. Confirm that the repository, branch, files, and symbols exist in the ontology.
3. Deterministically check the Constitution, risk, capability, approval, and expiry.
4. Execute only typed tools such as `repo.search/read/patch/test/diff/rollback`.
5. Serialize writes to the same file and parallelize independent reads and tests.
6. Check compilation, lint, unit tests, regression tests, and real postconditions.
7. On failure, re-plan the failed stage instead of regenerating the whole codebase.

#### Speed and stability metrics

Record `CodePlan schema pass rate`, `patch apply success`, `first-pass compile`,
`targeted-test pass`, `full-regression pass`, `verified change p95`,
`replan count`, and `tokens per verified change`. Structured output reduces
format errors, but it does not prove that the code is logically correct; final
promotion still requires execution evidence and a reviewed diff.

## 5. Request lifecycle

```text
1. BOSS speaks.
2. Wake word, identity, and session are checked.
3. Speech is transcribed.
4. Current conversation and relevant memory are retrieved.
5. The request is classified: chat, information, local work, external action, or high-risk action.
6. JARVIS writes a plan.
7. The broker checks the plan.
8. A scoped capability token is issued.
9. A device agent executes.
10. Screen, state, and response are checked again.
11. The result becomes VERIFIED, FAILED, BLOCKED, or UNKNOWN.
12. JARVIS reports the result by voice and UI.
13. The event and reusable learning material are stored.
```

Reads and preparations may run in parallel. A real change, payment, trade, deletion, or external send must have one deliberate commit point.

## 6. Fast execution design

### Three lanes

#### Reflex lane

Known work is mapped by the SLLM to a tested `skill_id`.

```text
natural language → skill_id → verified execution graph → authority check → run
```

No cloud reasoning is needed for a routine skill.

#### Planning lane

Novel work is planned by the open-weight model or a cloud teacher. Once verified, the procedure becomes a local skill.

#### Approval lane

Payments, deletion, trading, booking, and external publishing are prepared automatically; BOSS confirms only the final commit.

### Speed rules

- One representative agent coordinates; specialist executors work in parallel.
- Keep models, browser sessions, API connections, and hot memory warm.
- Prefer official APIs over screen clicks.
- Prefer DOM/accessibility trees over visual OCR.
- Run embeddings, deduplication, and indexing asynchronously.
- Use idempotency keys to prevent duplicate side effects.
- Compile successful traces into reusable skills.

## 7. Memory layers

### Short-term memory

Current voice conversation, active plan, recent screen state, pending approval, and the latest tool result.

- RAM or a fast local store
- Minutes to hours by default
- Direct lookup by session, sequence, and task ID
- Exact current state is more important than semantic similarity

### Medium-term memory

Projects, decisions, failures, and recurring procedures from the last few days or weeks.

- Search by date, project, person, and task ID
- Combine exact terms and semantic retrieval
- Keep older records as `superseded` instead of deleting them

### Long-term memory

BOSS preferences, principles, verified facts, completed skills, and durable project knowledge.

- No silent overwrite
- Preserve source, verification time, and validity window
- Conflicts become explicit conflicts or pending records

### Fact ledger

Execution approvals, actions, outcomes, and evidence are stored separately from memory. A memory can say “the message was sent”; the ledger must prove whether it actually was.

## 8. Retrieval and indexing

### Parallel indexes

| Index | Best at finding |
|---|---|
| Full-text/BM25 | File names, commands, numbers, exact phrases |
| Dense vector | Different wording with the same meaning |
| Temporal | Recent events and decisions from a specific date |
| Entity graph | People, projects, files, and tools connected together |
| Procedure | Reusable skills and execution graphs |
| Provenance/permission | Evidence location and which model may see it |

### Fast retrieval path

```text
classify the query
 → choose the needed indexes
 → query full-text, vector, time, graph, and provenance in parallel
 → filter by permission and validity
 → rerank 30–50 candidates
 → pack only the best 3–8 items into context
```

An initial ranking score may combine semantic similarity, exact match, recency, importance, and source trust, while penalizing stale or conflicting records. Those weights are starting points, not universal truths.

### Minimal memory record

```json
{
  "memory_id": "mem_001",
  "tier": "medium",
  "type": "procedure",
  "content": "morning report procedure",
  "entities": ["report", "investment_lab"],
  "valid_from": "2026-09-01",
  "valid_to": null,
  "confidence": 0.91,
  "source_refs": ["event_183", "screen_44"],
  "privacy_class": "D1",
  "supersedes": null,
  "status": "active"
}
```

## 9. Privacy classes

| Class | Example | Default handling |
|---|---|---|
| D0 public | Public documents and web pages | Cloud use is allowed when useful |
| D1 personal | Personal schedules, preferences, ordinary projects | Local first; send only reduced context |
| D2 sensitive | Family, finance, private business material | Local by default; explicit approval for export |
| D3 secret | Passwords, cards, API keys | Never pass raw values to a model or cloud |

## 10. Model roles

### Personal SLLM

Fast intent routing, BOSS's style, personal memory, recurring skills, and low-latency local work.

### Open-weight model

Unfamiliar problems, complex plans, code analysis, and broad reasoning.

### Cloud teacher

A teacher, critic, and test generator for sanitized hard cases. It does not directly call local tools or control devices.

```text
SLLM proposal ──────┐
                     ├─ verifier + authority broker → one commit
open-weight proposal ┘
```

## 11. Chinese open-weight model selection

### Policy

Do not trust an `uncensored` label by itself. Verify the official checkpoint, model hash, license, local execution path, and actual behavior on JARVIS tests.

### Candidate roles

- **Fast personal assistant:** Qwen3 family
- **Deep reasoning and coding:** DeepSeek-R1 family or an R1 distilled model
- **Personalization:** a private SLLM trained on BOSS-approved data

The official Qwen3 and DeepSeek-R1 reports demonstrate reasoning, coding, math, and multilingual capability; those benchmarks do not by themselves prove truthfulness, political neutrality, or absence of suppression. [Qwen3 technical report](https://arxiv.org/abs/2505.09388) · [DeepSeek-R1 paper](https://arxiv.org/abs/2501.12948)

### Honesty and censorship audit

1. Does the model answer allowed questions instead of refusing unnecessarily?
2. Are Korean, English, and Chinese answers consistent when the evidence is the same?
3. Does it separate uncertainty from fact?
4. Does it invent numbers when checked against official sources or calculations?
5. Does it falsely claim that a tool action completed?
6. Does the local checkpoint behave differently from the API route?

One independent audit reported information omission or softening in DeepSeek responses to politically sensitive prompts. Another study reported language-dependent political responses across models. These findings do not mean that every Chinese model behaves identically; they mean that each deployed version needs its own audit. [Information suppression audit](https://arxiv.org/abs/2506.12349) · [Bilingual bias study](https://arxiv.org/abs/2602.06371)

## 12. Quantization policy

“Zero performance loss after quantization” cannot be guaranteed in advance. Compare the original and quantized versions on the actual JARVIS workload and promote only a version within the allowed regression budget.

```text
BF16/FP16 baseline
 → FP8/INT8
 → Q8
 → Q6
 → AWQ/GPTQ 4-bit
```

AWQ protects salient activation channels during low-bit weight quantization. GPTQ is a post-training method designed to preserve accuracy at low bit widths. Neither method guarantees identical results for every model, hardware target, or task. [AWQ paper](https://arxiv.org/abs/2306.00978) · [GPTQ paper](https://arxiv.org/abs/2210.17323)

### Quantization regression suite

| Area | Compare |
|---|---|
| Dialogue | Korean fluency and context retention |
| Tool use | JSON format and command accuracy |
| Coding | Real test pass rate |
| Memory | Accuracy of retrieved facts |
| Truthfulness | Unsupported-claim rate |
| Refusal behavior | Unnecessary refusal rate on allowed prompts |
| Speed | Time to first response and total completion |
| Stability | Repetition and forgetting in long sessions |

Suggested initial promotion targets (design targets, not measured results):

```text
dialogue success delta        <= 2%
tool-call success delta       <= 1%
code-test pass-rate delta     <= 1%
truthfulness regression       none
unnecessary-refusal increase  none
P95 latency                   better than baseline
```

## 13. Authority design

### Green: automatic

- Read files or web pages
- Check schedules
- Search locally
- Draft reversible changes

### Yellow: conditional

- Enter data in a browser
- Rename files
- Work inside a logged-in service
- Repeat a task inside a standing order

### Red: BOSS confirmation

- Send external mail or publish
- Payment, booking, or securities trading
- Bulk deletion
- Administrator or security changes
- Constitution, authority, or model-policy changes

JARVIS never receives the administrator password. It requests a bounded capability such as `backup_project`; the broker checks scope and expiry, then runs a signed procedure.

### 13.1 Proactive household and finance housekeeping

JARVIS should not wait for BOSS to notice every repetitive nuisance. It can inspect
local, consented records and follow **discover → propose → prepare → bounded execution
→ verify**. Discovery and recommendations are broad; movement of money or loss of a
right remains policy-bound.

| Area | What JARVIS may do first | Execution boundary |
|---|---|---|
| Subscriptions | Find 30-day non-use, cost, family sharing, and cancellation fees; propose cancellation and prepare the page | Auto-cancel only under a BOSS rule with no fee or benefit loss |
| Coupons and points | Find expiry dates, conditions, and conversion options; alert and prepare candidates | BOSS confirmation for third-party transfer, conversion loss, or changed terms |
| Bank accounts | Find dormant accounts, standing payments, balances, and linked services; propose an order of cleanup | Closure, transfer, and withdrawal always require a current review and BOSS authorization |
| Investments | Present candidates with data timestamps, evidence, risks, and alternatives | Orders require an explicit strategy, amount/loss limits, and order confirmation |

“Invest when conditions are good” is not an executable rule. Define an asset universe,
maximum amount, daily cap, loss limit, no-leverage rule, expiry, and stop conditions in a
machine-checkable policy first. JARVIS may proactively surface candidates, but it may not
turn an unspoken model judgment into new authority. Prefer read-only official finance APIs;
use browser automation only for preparation when no suitable API exists.

### 13.2 Passkeys and the credential broker

A passkey is not an encrypted password file; it is public-key/private-key authentication.
The private key is used by Windows Hello/TPM, macOS Secure Enclave, or a FIDO security key.
The LLM receives neither the password nor the private key. It sees only an opaque reference
such as `account_ref=approved_bank_main` and a bounded request.

1. JARVIS requests `login(account_ref)`.
2. The credential broker checks the site, target, and expiry.
3. The platform authenticator signs the challenge using BOSS PIN/biometric or a security key.
4. The broker issues a short capability such as `read_only`, `subscription_cancel`, or `order_draft`.
5. Receipts, results, and failures go to the ledger; passwords, passkeys, and card numbers do not.

If a site lacks passkey support, a local credential store may inject a password ephemerally,
but it must never enter prompts, voice transcripts, or ordinary logs. An already logged-in
browser session is not unlimited authority: finance tools separate read, draft, and execute
verbs. CAPTCHA, MFA, and identity checks are never bypassed; they are handed to BOSS. For
strict local-only storage, select a device-bound, non-synced passkey.

## 14. Execution states and records

```text
PROPOSED
 → POLICY_CHECKED
 → PREPARED
 → APPROVED or GRANTED
 → EXECUTING
 → OBSERVED
 → VERIFIED
 → COMMITTED
```

Failure states:

- `FAILED`: the cause is known
- `BLOCKED`: policy prevented execution
- `UNKNOWN`: the result could not be verified
- `RECOVERED`: the recovery path verified the result

### Event record example

```json
{
  "event_id": "evt_20260921_000184",
  "task_id": "task_20260921_0042",
  "actor": "jarvis",
  "constitution_version": "1.0.0",
  "policy_version": "2026-09-21.3",
  "model_version": "sllm-0.8.2",
  "capability": "browser_read",
  "approval_id": null,
  "plan_hash": "sha256:...",
  "evidence": ["screenshot_ref", "http_status"],
  "status": "verified"
}
```

### 14.1 Change history and optional blockchain sealing

The Constitution, policies, and skills may receive a new version when the BOSS
approves a change. The old version is not erased: the diff, reason, approver,
and effective time are appended to the ledger. Blockchain is not an authority
or execution path; it is an optional external witness that helps detect a later
rewrite of that ledger.

```text
execute → write to the local encrypted ledger → sign BOSS/version fingerprints
        → enqueue a seal → asynchronously anchor a Merkle root externally
```

- Real-time voice, browser, CLI, and financial actions never wait for a chain confirmation.
- Raw voice, embeddings, passwords, API keys, screenshots, and private memories never go on-chain.
- If the chain is unavailable, work continues and the local sealing queue retries later.
- A single BOSS-owned computer may need only a signed append-only ledger and encrypted backups.
- Use an external anchor only for cross-owner JARVIS collaboration or inheritance evidence.

#### Domain decision table

| Domain | Record bundle | Why an external anchor can help |
|---|---|---|
| Finance and securities | Order plan, approval, and fill fingerprints | Post-trade audit and dispute evidence |
| Constitution and succession | JARVIS version, policy change, and approval time | Prove the version intended for succession |
| Model and skill supply chain | Model hash, test results, and release version | Verify the model that actually ran |
| Multiple nodes | Node signatures, questions, answers, and result fingerprints | Compare records across machines |
| Consent and authority | Consent version, revocation time, and capability scope | Prove when and how a capability was allowed |

The decision depends on independent parties needing to verify the same record and
the cost of a later rewrite, not on importance alone. Personal memories, voice,
embeddings, passwords, and raw financial records stay off-chain; blockchain does
not replace a legal will, a notary, or a broker's official record.

Never record raw passwords, card numbers, API keys, or private source audio.

## 15. Failure and recovery

- Pause external actions when the network is unavailable.
- Do not mark an unverified result as success.
- Use idempotency keys for retries.
- Resume from the last verified step after a service restart.
- Use the local fallback only inside its allowed scope during a cloud outage.
- Block risky work if the authority broker is unhealthy.
- Let BOSS revoke all active execution tokens with an emergency stop.

## 16. Build order

1. Constitution, BOSS identity, authority broker, and append-only ledger
2. Natural voice sessions and short-term memory
3. Medium/long-term memory and parallel indexes
4. Browser, file, CLI, and API capability registry
5. Real outcome verification and recovery
6. SLLM, open-weight, and cloud-teacher routing
7. Skill promotion and regression tests
8. Succession, key rotation, and multi-device operation

## 17. Acceptance gates

### Dialogue gate

Does voice remain continuous and does the wake session carry context naturally?

### Authority gate

Can the model obtain administrator rights or silently widen its scope?

### Execution gate

Does the requested action happen on the real device, with a verified result?

### Memory gate

Can JARVIS retrieve the needed memory quickly while separating stale facts from current facts?

### Model gate

Does the quantized model preserve dialogue, code, tool use, retrieval, and truthfulness within the allowed regression budget?

### Learning gate

Does a successful task become a reusable skill, test, and memory item?

## 18. Final principle

> JARVIS should not be a system that blindly trusts a model. It should remain safe and useful even when the model is wrong.

> The first run requires reasoning. Later runs should use the verified procedure and become fast.

## Open-source publication note

This repository is released under the Apache License 2.0. Third-party code, services,
datasets, tokenizers, and open-weight models retain their own licenses and notices.
Public design files must contain no local paths, secrets, raw recordings, exact locations,
or unredacted family data; hardware-specific acceptance reports should stay outside the
public design unless they are intentionally released and redacted.
