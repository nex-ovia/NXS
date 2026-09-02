# The Nexovia Standard (NXS v2.0)

**A delivery standard that makes solutions portable, reusable, and independent of any single person or tool.**

---

## What Is NXS?

Good solutions are built **once**, reused **many times**, extended **without friction**, and maintained **without becoming a burden**.

NXS defines what every finished solution must be true of, so that it can be:
- Understood by anyone without reading code
- Extended by anyone without breaking what works
- Reused across projects without rebuilding
- Maintained for years without the original builder

It doesn't tell you what language to use, what tools to pick, or how to write code. It tells you what "done" looks like.

---

## The Four Business Outcomes

Every solution built to NXS achieves one or more of these outcomes:

### 1. **Resilience** — Project survives without the original builder
- New person understands the system in < 2 hours
- System runs unchanged when builder is gone for weeks
- All decisions are documented with clear rationale

**How you know:** Handoff takes < 2 hours, no tribal knowledge needed

### 2. **Reusability** — Same logic works in 5+ different contexts
- Business logic doesn't assume one specific environment or tool
- Same code runs in Project A, B, C with only configuration differing
- Reuse takes hours, not weeks

**How you know:** Deploy to 2+ projects unchanged; adaptation < 2 hours

### 3. **Ownership** — Business is never locked into tools
- Swapping tools (Claude → OpenCode) takes < 4 hours with no logic rewrite
- If a tool disappears, you can move to an alternative automatically
- Fallback chains exist so primary tool failure doesn't break everything

**How you know:** Tool swap < 4 hours; fallbacks work automatically

### 4. **Speed** — Ship 40% faster; iterate 6x faster
- New device setup takes 5 minutes, not 2 hours (automation, not manuals)
- Changing a parameter takes < 10 minutes (change → test → deploy)
- Decisions are reused, not remade every project
- Time waste is visible and tracked

**How you know:** Setup 5 min, iteration < 10 min, decisions reused across projects

---

## The Four Rules

Every NXS solution follows these non-negotiable rules:

### Rule 1: Logic Separate From Tools
The business logic (decisions, rules, algorithms) must be independent of the tools used to deliver it.

If your database changes or your platform is replaced, the logic stays the same. Only the connection changes.

**Example:**
```
✗ WRONG: "Use Claude Code to orchestrate agents"
✓ RIGHT: "When primary agent fails, use fallback agent. Claude Code is one option; OpenCode is another."
```

### Rule 2: Configuration Never Hardcoded
Every value that changes between environments (API keys, URLs, timeouts, feature flags) must live outside the code.

Same solution runs locally, in staging, in production — no modifications needed.

**Example:**
```
✗ WRONG: API_URL = "https://prod.myvendor.com/v1"
✓ RIGHT: API_URL = os.getenv("VENDOR_API_URL")
```

### Rule 3: Every External Dependency Is Visible
Document every service, tool, API, database, or platform your solution depends on.

Document: what it is, why it's there, what it provides, what would change if replaced.

**Example:**
```
✗ WRONG: Solution silently depends on Ollama; nobody knows until it breaks
✓ RIGHT: [Dependencies] section lists: Ollama (local LLM), Claude API (cloud fallback), PostgreSQL (state)
```

### Rule 4: Runs Anywhere, For Anyone
New person on any machine can run your solution by following only what's written down.

No tribal knowledge. No "magic" setup steps. No local-only files.

---

## Definition of Done (7 Checkboxes)

A solution is complete when all of these are true:

- [ ] **Purpose documented** — Anyone can read what this does and why, without reading code
- [ ] **Logic identifiable** — Business rules live somewhere clear, readable, and separate from tools
- [ ] **Dependencies listed** — Every external system is named with its purpose documented
- [ ] **Configuration externalised** — Nothing environment-specific is hardcoded
- [ ] **Runs anywhere** — New person can run it on any machine by following written steps
- [ ] **Health verifiable** — Defined way to confirm the solution is running correctly
- [ ] **Stable under load** — Tested to work correctly at expected real-world volume

---

## How to Measure Success

Use these four metrics to measure whether your solution achieves NXS outcomes:

| Metric | What It Measures | Target | Outcome |
|--------|------------------|--------|---------|
| **Time to Understand** | How long new person takes to grasp an unfamiliar solution | < 2 hours | Resilience |
| **Dependency Swap Time** | How long to replace one tool/vendor with another | < 4 hours | Ownership |
| **Time to First Version** | Speed from brief to working, deployable solution | 40% faster than baseline | Speed |
| **Maintenance Overhead** | Hours per week on fixes, firefighting, support | < 10% of team time | Speed + Resilience |

---

## The Three Governance Gates

All must pass before implementation starts:

### Gate 1: Declaration Gate
Intent must be defined in the project manifest before code starts.
- Question: Is it clear what we're building and why?
- Answer: Yes → proceed; No → define it first

### Gate 2: Integrity Gate
Physical project structure must match what's declared.
- Question: Does the code match the plan?
- Answer: Yes → proceed; No → align them

### Gate 3: Sovereignty Gate
All dependencies are audited; no hidden lock-in.
- Question: Can we survive if a vendor disappears?
- Answer: Yes → proceed; No → add fallbacks

---

## NXS Is NOT

**Not a language/framework choice.** Python, Rust, JavaScript, no-code tools — all can follow NXS.

**Not a constraint on creativity.** NXS defines the structure; what you build inside it is yours.

**Not a compliance exercise.** Every rule exists to protect your business ownership of what was built.

**Not a library.** There's nothing to install. NXS is applied to projects, not added as a dependency.

---

## How to Use This Standard

### For Leaders
Read: "The Four Business Outcomes" and "How to Measure Success"  
Action: Measure your projects against the four metrics  
Time: 5 minutes

### For Developers
Read: Full page + GOVERNANCE.md (operational details)  
Action: Follow the four rules + Definition of Done checklist  
Time: 2 hours to understand; apply ongoing

### For AI Tools/Agents
Read: SYSTEM-PROMPT.md  
Action: Copy to your AI tool settings; applies to every session  
Time: 5 minutes

### For New Team Members
Read: QUICK-START.md (5-minute summary)  
Action: Use INDEX.md when you need specifics  
Time: 5 minutes to get productive; 30 minutes to understand fully

---

## Related Files

- **GOVERNANCE.md** — Operational details: how to execute NXS, session discipline, gates
- **SYSTEM-PROMPT.md** — AI system prompt; copy to your AI tool
- **QUICK-START.md** — 5-minute summary with visual tables
- **INDEX.md** — Navigation guide; find what you need
- **MANIFEST-SPEC.md** — Project structure template
- **ARCHITECTURE.md** — How all documentation fits together

---

## Core Principle: Delivery Sovereignty

Delivery sovereignty means the team that commissions a solution retains full understanding, control, and portability forever.

A sovereign solution can be:
- **Understood** without reading code
- **Reused** without rebuilding
- **Extended** without breaking things
- **Packaged** as a reusable module
- **Maintained** without depending on the original builder

If a solution can't do all five, it hasn't truly been built — it's been assembled for one moment in time.

---

## Versioning

**NXS v2.0** is the current version.

v2.0 is fully backward compatible with v1.0. Existing projects don't need changes; they remain compliant.

---

## Quick Links

- **Main Repository:** https://github.com/nex-ovia/NXS
- **For Details:** GOVERNANCE.md
- **For Quick Summary:** QUICK-START.md
- **For Navigation:** INDEX.md

---

_The Nexovia Standard: because a solution built once should work, grow, and last._
