# Working with Claude: known failure modes

Recorded from real misses, not hypotheticals. Every example below happened
while building this repository.

The purpose is not self-criticism. It is that these failures are
*patterned* — they recur, they are recognisable, and a short question from
the owner catches most of them.

---

## The failure modes

### 1. Testing a part, claiming the whole

**The worst one.** It produces confident, specific, wrong answers.

*What happened:* Claude ran a hook script by hand, watched it reject
`docs/build_manifest.md`, and reported that the knowledge base was
blocked. It was not. The hook never fired at all — its matcher was
malformed, so the script was never invoked. A component test had been
presented as a system result.

*Catch it with:* **"Did you test that end to end?"**

---

### 2. Inferring a rule from partial data, then writing it down

Encoding a guess makes it sticky. It stops being a guess and becomes a
rule that later work is built on.

*What happened:* Given monochrome application logos and gold mother marks,
Claude inferred "gold marks the alliance layer and appears nowhere else"
and wrote it into the brand specification. The gold application set
arrived shortly after and the rule was wrong.

*Catch it with:* **"Is that from what I gave you, or did you infer it?"**

---

### 3. Optimising for a goal that was never stated

Usually safety when reach was wanted, or protection when openness was.

*What happened:* Claude recommended AGPL to protect against competitors
taking the code. The actual goal was maximum spread. It was solving a
problem the owner did not have, and kept recommending it until corrected.

*Catch it with:* **"Why that choice?"** — and state the goal, not just the
task.

---

### 4. Reading instructions literally when the intent was plain

*What happened:* "Use the framework as-is" was read as a permanent freeze.
The intent was "port it intact, then adapt it." Claude built an elaborate
settings-layer workaround rather than fixing the file directly, and only
stopped when told.

*Catch it with:* **"That's not what I meant"** — early, not at the end.

---

### 5. Trusting a subagent's report

Subagent output is evidence, not fact. It needs the same verification as
anything else.

*What happened:* A review agent reported that a hook blocked the knowledge
base. Claude relayed it to the owner as established. It was wrong — see
failure 1.

*Catch it with:* **"Did you verify that yourself?"**

---

### 6. Doing it directly instead of routing to an agent

There is a standing bias toward acting rather than delegating. Faster,
usually worse for anything large.

*What happened:* One agent was used across an entire session of work, and
only because the owner asked for it. That agent immediately found a
critical bug Claude had shipped.

*Catch it with:* **"Run that through the agents"** or **"/plan first"**

---

### 7. Not looking at the output

*What happened:* Making a logo transparent, Claude keyed out every dark
pixel — erasing the black fist along with the black background. The code
ran without error. The result was an empty shield. It was caught only
because the image was viewed afterwards.

*Catch it with:* **"Show me"** — for anything visual, always.

---

## The four questions

In rough order of how much they catch:

1. **"Did you test that end to end?"**
2. **"Show me."**
3. **"Why that choice?"**
4. **"That's not what I meant."**

---

## The structural fix

**State the goal, not just the task.**

Nearly every failure above traces back to Claude inferring intent rather
than being given it. "Make the logo transparent" produced a broken key.
"Make the logo transparent so it works on the light page" would have
produced a check against a light background.

The task says what to do. The goal says how to know it worked.

---

## The honest limit

Claude does not reliably detect its own errors by introspection. Every
failure above was caught by testing or by the owner — none by Claude
noticing something felt wrong.

So the working system is not "Claude is careful." It is:

- **Claude verifies empirically** rather than asserting
- **The owner sanity-checks intent** rather than reviewing code

That division works. Reviewing the code is not the owner's job and never
will be. Noticing "that isn't what I asked for" is, and it is the check
that catches the most.
