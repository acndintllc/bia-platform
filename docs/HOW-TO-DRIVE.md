# How to drive this

Written for the owner, not for a developer. You do not need to know the
commands. You need to know what to ask for.

---

## The short version

**Describe the outcome. Claude picks the tools.**

> "Build the login system so members sign in once and it works across all
> five apps."

That sentence is enough. Behind it, Claude routes to the planner to break
it down, the TDD agent to write tests first, the code reviewer to check
quality, and the security reviewer because it touches authentication. You
did not name any of them.

The commands below exist for developers who want manual control. They are
optional.

---

## What you actually control

Three things, and none of them are technical.

**1. The goal.** What should be true when this is done? Not how — what.

**2. The constraint.** What must not change? Budget, deadline, an existing
decision, a brand rule.

**3. The verdict.** Claude verifies its own work, but you decide whether
it is what you wanted. "That's not it" is a complete and useful sentence.

---

## How to ask well

| Weak | Strong |
|---|---|
| "Work on Blackflix" | "Let a filmmaker upload a film and have it show as pending review" |
| "Make it secure" | "Someone who isn't logged in must never reach another member's data" |
| "Fix the site" | "The logo is a black box on the light page — it should be transparent" |

The pattern: **describe the finished state**, not the activity. If you can
say how you would check it yourself, that is a good ask.

---

## When to interrupt

- It is building the wrong thing → say so immediately, not at the end
- You do not understand what it just said → "explain that in plain English"
- It asks a question you cannot answer → "you decide, here's what matters to me"
- It claims done → "show me" is always fair

---

## The commands, in plain English

You will rarely need these. Kept here so the vocabulary is not a mystery.

| Command | What it does | When you'd want it |
|---|---|---|
| `/plan` | Writes a step-by-step plan and waits for approval before touching code | Before anything big, when you want to see the shape first |
| `/tdd` | Writes the tests before the code, so correctness is provable | Any feature where being wrong is expensive |
| `/code-review` | Reviews changes for bugs and quality | Before anything ships |
| `/verify` | Runs every check against the current state | "Is this actually working?" |
| `/e2e` | Drives the real app like a user would and reports what breaks | Before a launch |
| `/build-fix` | Fixes build errors one at a time | When something stops compiling |
| `/refactor-clean` | Finds and removes dead code safely | Periodic cleanup |
| `/test-coverage` | Finds untested code and writes the missing tests | When coverage has drifted |
| `/checkpoint` | Saves a known-good state you can return to | Before a risky change |
| `/update-docs` | Syncs documentation to match the code | After a change that outdates the docs |
| `/update-codemaps` | Regenerates the architecture map | After structural change |
| `/learn` | Extracts reusable patterns from the session into new skills | After solving something you'll hit again |
| `/orchestrate` | Chains several agents in order for one complex job | A large feature, end to end |
| `/eval` | Sets measurable pass criteria and tests against them | When "done" needs to be objective |
| `/setup-pm` | Picks the package manager | Once, at project setup |

---

## The nine agents

Specialists Claude delegates to. You will not normally name them.

| Agent | Role |
|---|---|
| `planner` | Breaks a request into buildable pieces |
| `architect` | System design and structural decisions |
| `tdd-guide` | Enforces tests before implementation |
| `code-reviewer` | Quality and correctness |
| `security-reviewer` | Vulnerabilities, auth, data exposure |
| `build-error-resolver` | Gets a broken build green again |
| `e2e-runner` | Tests real user journeys in a browser |
| `refactor-cleaner` | Removes dead code |
| `doc-updater` | Keeps documentation true |

To force one: *"use the security reviewer on the payment code."*

---

## What is always on

**`CLAUDE.md`** is injected into every session. It is why work here gets
verified rather than asserted, and why the spec is treated as law. You do
not invoke it; it is the environment.

**Hooks** run automatically on tool use — blocking dev servers outside
tmux, keeping documentation in the knowledge base, saving session state.

Everything else is on demand.

---

## The honest boundary

Claude can plan, build, test, review and document. It cannot decide what
the business should be. Pricing, brand, what to cut, what matters — those
stay yours, and it should ask rather than guess.

If it guesses at something that was yours to decide, tell it. That is a
bug in how it is working, not a preference.
