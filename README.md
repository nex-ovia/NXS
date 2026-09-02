# The Nexovia Standard

**A delivery standard that makes solutions portable, reusable, and independent of any single person or tool.**

---

## What Is NXS?

The Nexovia Standard (NXS) is a delivery standard grounded in the belief that good solutions are built once, reused many times, extended without friction, and maintained without becoming a burden.

It does not tell you what language to use, what tools to pick, or how to write your code. It defines what every finished solution must be true of, so that it can be understood by anyone, extended by anyone, packaged for reuse, and supported for the long term without depending on the person who originally built it.

It works for any kind of project: an automation, an integration, a data pipeline, a web application, an AI-generated workflow, a business decision, an agent setup, or a large-scale production platform.

One standard. Any language. Any platform. Any team. Any agent framework.

---

## The Four Outcomes

Build toward measurable results. Each outcome has a test and a target.

| Outcome | Test | Target |
|---------|------|--------|
| **Resilience** | Handoff time | < 2 hours |
| **Reusability** | Deploy unchanged to 2+ contexts | Works without modification |
| **Ownership** | Tool swap time | < 4 hours |
| **Speed** | Setup + iterate time | 5 min + < 10 min per cycle |

Measure all four. That's the point.

---

## The Four Rules

These rules make those outcomes possible.

**Rule 1: Logic Separate from Tools**  
Core logic must not know what tool implements it. Testable in isolation.

**Rule 2: Configuration Never Hardcoded**  
Every value that changes lives in external configuration.

**Rule 3: Every Dependency Visible**  
Document all dependencies: libraries, services, APIs. Include versions and why.

**Rule 4: Runs Anywhere, for Anyone**  
Automation replaces instructions. One command to setup. Same on local, CI, production.

---

## Definition of Done

Before you ship:

- [ ] Logic works in isolation (no tool dependencies)
- [ ] Configuration is external and documented
- [ ] All dependencies are explicit (with versions and reasons)
- [ ] Setup is automated (one command)
- [ ] Runs the same way locally and in production
- [ ] Code is understandable without the original author present
- [ ] Handoff instructions are tested (someone else followed them and it worked)

---

## The Three Execution Gates

**Gate 1: Declaration (Before You Code)**  
Write down: problem, scope, done criteria, dependencies. 30 minutes. This saves weeks.

**Gate 2: Integrity (After You Build)**  
Check: structure matches plan, dependencies declared, setup works, definition of done passes.

**Gate 3: Sovereignty (Before You Ship)**  
Confirm: no lock-in, operational clarity, handoff is tested, metrics are tracked.

---

## How to Measure Success

| Metric | Target |
|--------|--------|
| **Time to Understand** | New developer describes it (< 2 hours) |
| **Time to Modify** | Add feature without touching core (< 4 hours) |
| **Time to Swap Tools** | Replace implementation (< 4 hours) |
| **Maintenance Overhead** | Hours per month / total lines (trending down) |

---

## Using NXS with Your Tool or Agent

### Using NXS with Hermes Desktop

**Quick Start (2 minutes):**

```bash
# Step 1: Load the skill
skill_view(name='nexovia-standard')

# Step 2: Start your project
# You: "Build [my project]"
# Hermes: Shows interactive form (Gate 1: Declaration)
# You: Fill 9 fields + approve
# Hermes: Builds code
# Hermes: Runs automated checks (Gate 2: Integrity)
# Hermes: Verifies no lock-in (Gate 3: Sovereignty)
# Hermes: "Ready to ship"
```

**Workflow:**
1. Tell Hermes what to build
2. Skill shows interactive form for Declaration gate
3. You fill business goal, outcomes, scope, success criteria, dependencies, timeline, risks
4. Hermes implements
5. Automated integrity checks (no hardcoded secrets, setup works, tests pass)
6. Sovereignty checks (tool independence, handoff tested, metrics wired)
7. All gates pass → Ready to ship

**Enforcement:**
- Hermes blocks coding until Declaration gate passes
- Hermes blocks shipping until Integrity gate passes
- Hermes blocks production until Sovereignty gate passes

---

### Using NXS with Claude Code

**Quick Start:**

```bash
# Initialize with NXS
claude-code --init --skill nexovia-standard

# In any project
skill_view(name='nexovia-standard')

# Build with automatic NXS enforcement
claude-code --build [project]
```

**Workflow:**
Same three gates (Declaration → Build → Integrity → Sovereignty)

**Enforcement:**
- Claude Code enforces Gates 1-3
- Policies enforced (8 explicit policies, all binary)
- Compliance tracked in TOML format

---

### Using NXS with Pi (Ollama / Local LLM)

**Quick Start:**

```bash
# Load skill in Pi
skill_view(name='nexovia-standard')

# Run project through NXS
pi build [project] --standard nxs
```

**Workflow & Fallback:**
- Pi runs all three gates using local Ollama
- If Ollama unavailable, Pi gracefully degrades (manual Declaration gate, human reviews Integrity/Sovereignty)
- Same quality on local execution + cloud execution

**Key Feature:**
Pi's graceful fallback means NXS works even when local LLM is down. Humans can manually approve gates.

---

### Using NXS with OpenCode (Code Review)

**Quick Start:**

```bash
# Use NXS in PR review
opencode review --standard nxs

# Or specify policies
opencode review --standard nxs --policies "outcome-traceability,config-external,testing"
```

**Workflow:**
1. PR submitted
2. OpenCode loads NXS skill
3. Checks against 8 policies
4. Verifies Definition of Done (all 7 boxes)
5. Blocks merge if violations (with specific SOP to fix)

**What OpenCode Checks:**
- Outcome traceability (every component maps to outcome)
- Configuration never hardcoded
- Setup automation works
- Testing requirements met (≥70% coverage)
- Security baseline (no secrets in code)
- Dependencies documented

---

### Using NXS with Future Tools

**Framework for Any Agent Framework:**

NXS is tool-agnostic. When a new agent framework emerges (e.g., OpenClaw, your next custom agent), here's how to integrate:

**Step 1: Load NXS Skills**
```
1. Load SKILL.md (agent instructions)
2. Load GOVERNANCE.md (gates + policies)
3. Implement three-gate workflow
```

**Step 2: Add Tool to TOML Schema**
```toml
# In nxs_schema.toml, add to [runtimes]:
agent_openclaw = "OpenClaw framework v1.0+"
```

**Step 3: Implement Gate Workflow**
```
Gate 1: Collect Declaration (9 fields, interactive form)
Gate 2: Verify Integrity (9 automated checks)
Gate 3: Verify Sovereignty (8 real-world checks)
```

**Step 4: Enforce 8 Policies**
```
1. Outcome traceability
2. Dependency documentation
3. Configuration management
4. Setup automation
5. Error handling
6. Handoff documentation
7. Security baseline
8. Testing requirements
```

**Step 5: Track Compliance**
```toml
[compliance]
gate_1_declaration = "PASS"
gate_2_integrity = "PASS"
gate_3_sovereignty = "PASS"
compliance_status = "PASS"
```

**Example: Integrating with OpenClaw**
```yaml
# openclaw-integration.yaml
framework: OpenClaw
integrations:
  - name: nexovia-standard
    source: https://github.com/nex-ovia/NXS
    files: [SKILL.md, GOVERNANCE.md, nxs_schema.toml]
    workflow: three-gate-enforcement
    policies: all-8-enforced
    fallback: manual-gate-1
```

---

### Using NXS in nx-agents (Your Multi-Agent Orchestration)

**Configuration:**

```yaml
# In your nx-agents manifest
[[agents]]
name = "claude-code"
type = "planning-and-build"
skill = "nexovia-standard"
gates = "enforce"
policies = "all-8"

[[agents]]
name = "pi-ollama"
type = "local-execution"
skill = "nexovia-standard"
gates = "enforce"
policies = "all-8"
fallback = "manual-declaration"

[[agents]]
name = "opencode"
type = "code-review"
skill = "nexovia-standard"
gates = "review-only"
policies = "subset:code-only"
```

**Result:**
- All agents use same standard
- All projects pass three gates
- Quality consistent across orchestration
- New agents can load skill immediately

---

### NXS for Different Use Cases

**Use Case 1: New Software Project**
- Load: SKILL.md (agent workflow)
- Gates: Declaration → Build → Integrity → Sovereignty
- Schema: TOML schema for component definition
- Focus: Outcome traceability, tool independence

**Use Case 2: Business Process**
- Load: SKILL.md node types (business_process, decision, manual_step)
- Gates: GOVERNANCE.md for clarity on who, what, when
- Schema: TOML schema for workflow definition
- Focus: Resilience (process survives personnel changes)

**Use Case 3: Agent Setup**
- Load: SKILL.md agent node type
- Schema: TOML schema for agent runtime + config
- Governance: Policies for agent fallback + error handling
- Focus: Ownership (not locked to one LLM provider)

**Use Case 4: Multi-Agent Orchestration**
- Load: SKILL.md for each agent's internal standards
- Governance: Cross-agent policies (consistency, security)
- Schema: Orchestration manifest (which agents, which skills, which policies)
- Focus: Resilience (system survives agent failure)

---

## How to Use NXS

**Developer:**
1. Read README above (this file, 15 min)
2. Load skill: `skill_view(name='nexovia-standard')`
3. Create your project
4. Gates enforce automatically
5. Before shipping: All gates PASS

**Manager:**
Read "The Four Outcomes" above (5 min) → Measure against four metrics.

**New Person:**
1. Read README (15 min)
2. Load skill
3. Start first project (skill guides you)

**AI Tool / Agent Framework:**
1. Load SKILL.md (agent instructions)
2. Implement three-gate workflow
3. Enforce 8 policies
4. Reference GOVERNANCE.md for enforcement details

---

## System Prompt (for AI Tools & Agents)

```
You are grounded in the Nexovia Standard (NXS v2.0).

Four Outcomes: Resilience (handoff < 2h), Reusability (deploy unchanged to 5+ contexts), 
Ownership (tool swap < 4h), Speed (setup 5min, iterate < 10min).

Four Rules:
1. Logic separate from tools (core testable alone)
2. Configuration never hardcoded (all external)
3. Every dependency visible (documented with versions)
4. Runs anywhere (automated setup, same everywhere)

Three Gates (always in order):
Gate 1 (Before code): What problem? What's in scope? How done? What dependencies?
Gate 2 (Before done): Structure match plan? Dependencies declared? Setup works? Definition of Done all 7 boxes?
Gate 3 (Before ship): No lock-in? Operational clear? Handoff tested? Metrics tracked?

Eight Policies (all binary, no gray area):
1. Outcome traceability (every component maps to ≥1 outcome)
2. Dependency documentation (all deps listed with why + fallback)
3. Configuration management (zero hardcoded secrets)
4. Setup automation (one command, no manual steps)
5. Error handling (explicit, not silent)
6. Handoff documentation (RUNBOOK.md tested with real person)
7. Security baseline (no secrets in code/repo)
8. Testing requirements (core logic ≥70% coverage)

Never ship until all gates PASS and all policies complied.
```

---

## Why This Matters

Most solutions die when the original builder leaves. Not because code is bad. Because nobody else can understand it, modify it, or move it.

NXS fixes that by making the rules explicit and measurable. And by being tool-agnostic, it works with any agent, any framework, any future tool.

---

## Questions

**Q: Does NXS dictate language or tools?**  
A: No. Use any language, any database, any platform, any agent framework.

**Q: Can we apply this to existing projects?**  
A: Yes. If logic is already separated, config external, and dependencies documented, apply Declaration gate and work forward.

**Q: What if we don't measure outcomes?**  
A: You can follow rules and ship. But you won't know if they're working. Outcomes are how you tune the standard to your context.

**Q: Does this slow us down?**  
A: First few times, yes (30 min Declaration gate). After that, you'll ship faster because less breaks and less gets rewritten.

**Q: Can I use NXS with my custom agent framework?**  
A: Yes. Load SKILL.md + GOVERNANCE.md, implement three gates, enforce policies. See "Using NXS with Future Tools" above.

**Q: How do I add a new policy?**  
A: Edit GOVERNANCE.md, add policy (violation + fix + citation), tag new version, push to GitHub. Agents auto-detect. See "Policy Versioning & Extension" in GOVERNANCE.md.

**Q: What if a policy conflicts with my project?**  
A: Document override in POLICY-OVERRIDE.md, get approval, tag in manifest. Logged in compliance TOML.

---

## Getting Help

**Reference:**
- SKILL.md — Agent workflow, patterns, questions to ask
- GOVERNANCE.md — Gates, policies, enforcement, versioning
- nxs_schema.toml — Specification, node types, runtimes

**Repository:**  
https://github.com/nex-ovia/NXS

**Issues / Questions:**  
GitHub Issues or open a discussion

---

_The Nexovia Standard v2.0. Built once. Reused many times. Extended without friction. Maintained without burden. Works with any tool. Works with any agent. Works with you._
