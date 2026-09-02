---
name: nexovia-standard
version: 2.0
category: standards

description: |
  Apply the Nexovia Standard (NXS) to any project, outcome, or agent setup.
  Use when building solutions, evaluating structure, planning deployments.
  Grounds decisions in four business outcomes (Resilience, Reusability,
  Ownership, Speed) and validates against three gates (Declaration, Integrity,
  Sovereignty). Works for software, business processes, agent configurations,
  and hybrid projects. Loads NXS automatically; no manual setup needed.

tags: [standard, architecture, delivery, outcomes, gates, nxs]

# AGENT INSTRUCTIONS
---

# Nexovia Standard (NXS) Skill for Agents

You are grounded in the Nexovia Standard (NXS v2.0). Every project you work on, every decision you make, traces back to four business outcomes and validates through three gates.

## The Four Outcomes (Why We Build)

These are measurable goals. Measure everything against them.

| Outcome | Test | Target |
|---------|------|--------|
| **Resilience** | Handoff time (can someone else run this?) | < 2 hours |
| **Reusability** | Deploy unchanged to multiple contexts | Works in 5+ projects without modification |
| **Ownership** | Tool swap time (could we replace the tool?) | < 4 hours |
| **Speed** | Setup time + iteration cycle time | Setup 5 min, iterate < 10 min |

**Map every component you create to at least one outcome.** If a component doesn't serve an outcome, it's waste.

## The Four Rules (How We Build)

These make the outcomes possible. Apply them to everything.

**Rule 1: Logic Separate from Tools**
- Core business logic must not know or depend on any tool
- Logic should be testable in complete isolation
- Tools (databases, APIs, frameworks) connect at boundaries only
- Example: If building an agent, the decision logic lives separately from the LLM runtime

**Rule 2: Configuration Never Hardcoded**
- Every value that changes across environments lives in external configuration
- No magic strings embedded in code
- Configuration lives in one place and is version-controlled
- Example: API endpoints, timeouts, feature flags all external

**Rule 3: Every Dependency Visible**
- Document every external dependency: libraries, services, APIs, models, tools
- Include version and reason for each
- State the cost/impact of replacing it
- Example: "We use Claude API because X; replacing would take Y hours"

**Rule 4: Runs Anywhere, for Anyone**
- Setup must be completely automated (one command)
- Same execution path for local, CI, production
- No "just set this environment variable" instructions
- Example: `./setup.sh` works on any machine without manual steps

## The Three Execution Gates

Always follow this sequence. Each gate prevents different mistakes.

### Gate 1: Declaration (Before You Code — 30 Minutes)

Write this down. Get agreement. Then code.

**Declare:**
1. **Problem** — What are we solving? (One clear sentence, not vague)
2. **Scope In** — What's explicitly included?
3. **Scope Out** — What's explicitly excluded? (What we're NOT solving)
4. **Success Criteria** — How will we know it's done?
5. **Dependencies (Preliminary)** — What external things do we need?
6. **Outcomes** — Which of the four outcomes does this serve? (Map to ≥1)

**Why:** Prevents "we're almost done, now let's add X" scope creep. Saves weeks.

### Gate 2: Integrity (After You Build — Verify Before Shipping)

Structure must match your Declaration.

**Check:**
- [ ] Is the structure as declared? (Code matches plan?)
- [ ] Do all dependencies match what you said?
- [ ] Can someone else run this with zero help?
- [ ] All four rules followed?
- [ ] Definition of Done all 7 boxes checked?

**Definition of Done (All 7 Required):**
1. Logic works in isolation (no tool dependencies)
2. Configuration is external and documented
3. All dependencies are explicit (with versions and reasons)
4. Setup is automated (one command)
5. Runs the same way locally and in production
6. Code is understandable without the original author present
7. Handoff instructions are tested (someone else actually followed them)

**Why:** Catches structural problems before deployment.

### Gate 3: Sovereignty (Before You Ship — Verify No Lock-In)

You must not be locked into tools.

**Confirm:**
- [ ] Could we swap the underlying tool/runtime? (< 4 hours of work)
- [ ] Does logic exist independent of the tool? (Can we rewrite the implementation?)
- [ ] Could we move to different infrastructure? (Cloud, local, different vendor)
- [ ] Operational clarity documented? (Who runs it? How? What could break?)
- [ ] Handoff actually tested? (Did someone who didn't build this run it successfully?)
- [ ] All four outcomes measurable? (Are we tracking them?)

**If any answer is "no" or "weeks of work," you have a lock-in problem. Fix it before shipping.**

**Why:** Prevents strategic lock-in. Ensures long-term viability.

## Universal Node Types (What Your Project Contains)

Every component must have an explicit type. Pick the one that fits.

| Type | What It Is | Examples | Outcomes |
|------|-----------|----------|----------|
| **code** | Executable software logic | API, worker, CLI, library | Resilience, Reusability, Ownership, Speed |
| **agent** | Autonomous actor (LLM, router, scheduler) | Claude-based handler, router, negotiator | Reusability, Ownership, Speed |
| **config** | External configuration (not in code) | Env vars, TOML files, secrets | Ownership, Speed |
| **data** | Persistent state (database, cache, files) | PostgreSQL table, S3 bucket, Redis | Resilience, Reusability |
| **decision** | Business policy or rule | Approval criteria, routing logic, escalation | Ownership, Resilience |
| **business_process** | Workflow (humans + systems) | Onboarding, incident response, deployment | Resilience, Speed |
| **documentation** | Runbooks and guides | RUNBOOK.md, DECISIONS.md, API.md | Resilience |
| **manual_step** | Human decision or action | Code review, testing, approval | Resilience |

## Universal Runtimes (How Things Execute)

Be explicit about runtime. Don't infer.

**Code:** Python 3.11, Python 3.12, Rust 2024, Node.js 20, Node.js 22  
**Agent:** LLM (Claude, GPT), Ollama (local), Remote API  
**Execute:** Docker, Lambda, Cloud Run, human, human-in-loop  
**Automation:** Workflow orchestrator, Cron job  
**Storage:** Static file, Environment variable, Database  

## How to Apply NXS (Agent Workflow)

### When Planning a Project

1. **Gate 1: Declaration**
   - Ask the user: What problem? Scope? How done? Dependencies?
   - Write it down (create `project_declaration.md` or equivalent)
   - Identify which outcomes this serves
   - Map preliminary nodes (what components?)

2. **Identify Outcomes**
   - Does this project need to survive without the original builder? → Resilience
   - Will this logic work in multiple contexts? → Reusability
   - Could we swap tools if needed? → Ownership
   - Can we ship and iterate quickly? → Speed

### When Building

1. **Apply the Four Rules**
   - Separate core logic from tool/infrastructure code
   - Externalize all configuration
   - Document every dependency (version + why)
   - Automate all setup (one command)

2. **Map Components**
   - Every component gets: id, name, type, runtime, outcomes, path, criticality
   - Example:
     ```toml
     [[nodes]]
     id = "claude-router"
     name = "Request Router Agent"
     type = "agent"
     runtime = "llm"
     outcomes = ["speed", "ownership"]
     path = "agents/router.toml"
     criticality = "high"
     dependencies = ["config-file", "logging-service"]
     ```

3. **Gate 2: Integrity**
   - Verify structure matches Declaration
   - Check all seven Definition of Done boxes
   - Ensure no component is orphaned (doesn't map to outcome)

### When Ready to Ship

1. **Gate 3: Sovereignty**
   - Test handoff with real person (not the builder)
   - Verify all outcomes are measurable
   - Confirm no lock-in (could we replace any tool?)

2. **Ship**
   - All three gates passed
   - All seven Definition of Done boxes checked
   - Handoff documented and tested

## Common Patterns

### Pattern 1: Agent Setup with Fallback

```toml
[[nodes]]
id = "ai-classifier"
type = "agent"
runtime = "llm"
outcomes = ["speed"]

[[nodes]]
id = "fallback-classifier"
type = "code"
runtime = "python-3.11"
outcomes = ["resilience"]
```

**Why:** If AI model is down, logic still works. Serves Resilience outcome.

### Pattern 2: Business Logic + Tool

```toml
[[nodes]]
id = "core-algorithm"
type = "code"
runtime = "python-3.11"
outcomes = ["reusability", "ownership"]

[[nodes]]
id = "database-adapter"
type = "code"
runtime = "python-3.11"
outcomes = []
```

**Why:** Core algorithm independent of database. Swappable. Serves Ownership outcome.

### Pattern 3: Decision + Workflow

```toml
[[nodes]]
id = "approval-policy"
type = "decision"
runtime = "human"
outcomes = ["ownership", "resilience"]

[[nodes]]
id = "approval-workflow"
type = "business_process"
runtime = "workflow"
outcomes = ["speed"]
```

**Why:** Policy explicit (owned), workflow automated (speed).

## Validation Checklist (Use Before Any Delivery)

```
NXS Compliance Checklist

Declaration Gate:
☐ Problem stated (specific, not vague)
☐ Scope in/out clear
☐ Success criteria defined
☐ Dependencies preliminary list
☐ Outcomes mapped (≥1)

Four Rules:
☐ Logic separate from tools
☐ No configuration hardcoded
☐ All dependencies listed (versions + why)
☐ Setup automated (one command)

Nodes:
☐ Every node has id, name, type, runtime, outcomes
☐ Every node maps to ≥1 outcome
☐ No circular dependencies
☐ No orphan nodes (unmapped components)

Definition of Done (All 7):
☐ Logic works in isolation
☐ Configuration external
☐ All dependencies explicit
☐ Setup automated
☐ Same everywhere (local, CI, prod)
☐ Understandable without original author
☐ Handoff tested with real person

Integrity Gate:
☐ Structure matches Declaration
☐ Dependencies documented with versions
☐ All Definition of Done boxes checked
☐ Setup automation works without help

Sovereignty Gate:
☐ Could we swap tools? (< 4 hours)
☐ Logic independent of tools?
☐ Could we move to different infrastructure?
☐ Operational clarity documented?
☐ Handoff tested (not just builder)?
☐ Outcomes measurable and tracked?

Ready to Ship:
☐ All three gates passed
☐ All checks above completed
☐ Team agrees: This is resilient, reusable, autonomous, fast
```

## Decision Making Framework

**When unsure about a design choice, ask:**

1. **Resilience:** "Could someone run this without me?" → No? Fix before shipping
2. **Reusability:** "Could this logic work elsewhere unchanged?" → No? Abstract it
3. **Ownership:** "Am I locked into this tool?" → Yes? Replace with tool-agnostic logic
4. **Speed:** "Can we ship this in < 5 min?" → No? Automate setup

**Pick the decision that optimizes all four outcomes, in this priority:**
1. Resilience (don't break when things fail)
2. Reusability (serve multiple contexts)
3. Ownership (never locked in)
4. Speed (ship fast, iterate faster)

## Questions to Ask Users

When someone asks you to build something, before you code, ask:

1. **"What problem are we solving?"** (Gate 1)
2. **"How will we know it's done?"** (Gate 1)
3. **"Which outcomes does this serve?"** (Resilience? Reusability? Ownership? Speed?)
4. **"Could someone else run this when you're unavailable?"** (Resilience test)
5. **"Could we replace the tool if we needed to?"** (Ownership test)
6. **"How will we measure success?"** (Four metrics)

Don't code without answers.

## Red Flags (Problems to Fix Immediately)

- ❌ "This only works if I do it" → Resilience problem
- ❌ "We'll have to rewrite for the new use case" → Reusability problem
- ❌ "We're locked into this vendor" → Ownership problem
- ❌ "Setup takes 3 days and a wizard" → Speed problem
- ❌ "Nobody knows what this does anymore" → Resilience problem
- ❌ "It's in production, we can't change it" → Ownership problem

## References

**Repository:** https://github.com/nex-ovia/NXS  
**README:** https://github.com/nex-ovia/NXS/blob/main/README.md  
**GOVERNANCE:** https://github.com/nex-ovia/NXS/blob/main/GOVERNANCE.md  
**Schema:** https://github.com/nex-ovia/NXS/blob/main/nxs_schema.toml  

---

_The Nexovia Standard. Resilient. Reusable. Autonomous. Fast._
