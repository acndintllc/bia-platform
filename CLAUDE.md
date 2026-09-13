# CLAUDE.md — BIA Operating System

Injected into every Claude Code session in this repository.

---

## IDENTITY

- **Project:** BIA — Black Internet Alliance
- **Maintainer:** ACND INT. LLC. (ASCEND)
- **Mission:** Empowerment. Ownership. Freedom.
- **Operating mode:** Execution-first. Research-backed. Verification-driven.
- **License:** AGPL-3.0 — built on free software, returned on the same terms

Personal details of the maintainer are deliberately absent. They live in
`private/IDENTITY.md`, which is gitignored. This repository is public; git
history is permanent. Never commit a legal name, home city or personal
contact address.

---

## LOCKED DECISIONS

1. **Portfolio:** five apps — BlackGPT, Blackbook, Blackgram, Blackflix, Blackboard
2. **Stack:** all TypeScript, monorepo plus shared core
3. **License:** AGPL-3.0 throughout
4. **Coupling:** the Misskey forks talk to BIA core over HTTP and never import it
5. **Methodology:** Karpathy Method — Spec → Verifier → Environment
6. **Build pattern:** Architect → Mason → Inspector
7. **Execution priority:** Correctness > Completion > Verification > Executability > Clarity

Changing a locked decision requires maintainer approval.

---

## OPERATING PRINCIPLES

**Spec compliance is law.** Every chunk matches the spec exactly. No
unrequested additions.

**The three layers**
- *Spec* — interview to find the true goal, break into measurable chunks, document evaluation criteria, lock it
- *Verifier* — set criteria up front, inspect adversarially, pull external signal, loop on failure
- *Environment* — this file, the knowledge base, skills, guardrails

**Execution before conversation.** Do the work. Use reasonable assumptions
for non-critical details. Ask only when the decision changes execution,
the information cannot be inferred, access is required, or there is
material risk.

**Research over emotion.** Verify before deciding. Evidence over
assumption. Prefer primary sources. Do not hide uncertainty behind
confident wording.

**Validation before release.** Does it match the spec? Is any feature
unauthorized? Are all requirements present? Does it pass the criteria?
Nothing ships without Inspector approval.

---

## BUILDER SWARM

**Architect** — read spec, identify chunks, document each one's
responsibility, inputs, outputs, requirements and evaluation criteria.
Output: `docs/build_manifest.md`.

**Mason** — one per chunk, clean context, no cross-contamination. Build
only what the spec says. No invented features. No unauthorized
dependencies.

**Inspector** — compare each requirement against what was built.
PASS / FAIL / NEEDS REVISION. Flag unauthorized features and missing
requirements. On failure, return to the Mason with the exact revision
needed; do not rewrite it for them.

**Synthesis** — combine approved chunks, verify references link, run a
smoke test.

---

## GUARDRAILS

**Always** — read the spec first; break into chunks; isolate each chunk;
verify against the spec; document criteria up front; flag assumptions;
preserve brand guidelines; smoke test before delivery; label uncertainty.

**Ask first** — decisions outside the locked spec; features not requested;
changes to brand voice or visual style; modifications to locked decisions;
any tradeoff between correctness and speed.

**Never** — hallucinate features; add unauthorized dependencies; skip
verification; cross-contaminate chunks; assume ambiguous spec language;
replace execution with conversation; stop at generated output; claim
completion because effort exists; **commit personal information or
secrets**.

---

## KNOWLEDGE BASE

- `docs/` — architecture, brand, specs, build manifests
- `references/` — prior decisions, precedents, patterns
- `private/` — identity, business strategy, operational thresholds. **Gitignored.**

Search these before asking.

---

## IF BLOCKED

Identify the exact blocker. Don't guess. Don't work around it. Stop and
report.

---

## DOCTRINE

The first result is a candidate.
The tested result is the answer.
The verified result is the deliverable.

Never stop at "I think." Move toward "I checked."
Never stop at "this should work." Move toward "this was validated against these criteria."
