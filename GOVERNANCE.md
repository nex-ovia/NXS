# GOVERNANCE.md — How to Execute NXS

**For:** Teams implementing NXS; need clear operational details  
**See also:** README.md (philosophy and rules)

---

## The Three Governance Gates

Every project must pass these gates before implementation starts.

### Gate 1: Declaration Gate
**Before** you write any code, declare your intent in a manifest.

- [ ] Is the problem clear?
- [ ] Is the solution approach documented?
- [ ] Do all stakeholders agree on what we're building?

If NO: Define it first.  
If YES: Proceed to Gate 2.

### Gate 2: Integrity Gate
**After** you've built it, verify the physical project matches your declaration.

- [ ] Does the actual project structure match the manifest?
- [ ] Are there files/components not in the manifest?
- [ ] Are there manifest items not in the actual code?

If NO: Align them.  
If YES: Proceed to Gate 3.

### Gate 3: Sovereignty Gate
**Before** shipping, audit dependencies and ensure no lock-in.

- [ ] Is every external dependency listed?
- [ ] Does a fallback exist if the primary tool fails?
- [ ] Can we survive if a vendor disappears?

If NO: Add fallbacks or exit strategy.  
If YES: Ready to ship.

---

## Project Structure

Use this topology to organize your project:

### Five Layers
- **Governance:** Manifests, policies, decisions (top-level)
- **Orchestration:** Entry points, routers, how things connect
- **Execution:** Business logic, actual work
- **Persistence:** Databases, state, memory
- **Surface:** APIs, UIs, external interfaces

### Node Types
- **manifest** → Your project declaration (project_manifest.toml)
- **logic** → Business rules and algorithms
- **entrypoint** → Where execution starts
- **agent** → AI or automated agents
- **adapter** → Connections to external systems
- **ui** → User interfaces
- **manual** → Human steps

### Node Properties
Every node should have:
- **layer** → Which of the 5 layers
- **type** → What kind of node (logic, adapter, etc.)
- **path** → Where it lives (file or documentation)
- **dependencies** → What it depends on
- **criticality** → high/medium/low

---

## Project Manifest Template

Create a `project_manifest.toml` in your project root:

```toml
[project]
name = "your-project-name"
version = "0.1.0"
standard = "https://github.com/nex-ovia/NXS"
nxs_version = "2.0"

[governance]
purpose = "What this project does in one sentence"
completion_criteria = "How we know this is done"

# Node 1: Entry point
[[nodes]]
id = "main"
layer = "orchestration"
type = "entrypoint"
path = "src/main.py"
criticality = "high"
description = "Where execution starts"

# Node 2: Core logic
[[nodes]]
id = "business-logic"
layer = "execution"
type = "logic"
path = "src/logic.py"
criticality = "high"
dependencies = []
description = "The core business rules"

# Add more nodes as needed...
```

---

## Definition of Done Checklist

Before shipping, verify:

- [ ] Purpose is documented (anyone can read what it does)
- [ ] Logic is identifiable (business rules are clear)
- [ ] Dependencies are listed (every external service is named)
- [ ] Configuration is externalized (nothing hardcoded)
- [ ] It runs anywhere (new person can run it without asking)
- [ ] Health is verifiable (way to confirm it's working)
- [ ] It's stable under load (tested at real volume)

---

## Metrics to Track

Measure your project against these:

| Metric | Measures | Target |
|--------|----------|--------|
| **Time to Understand** | How long for new person to grasp it | < 2 hours |
| **Dependency Swap Time** | How long to replace one tool | < 4 hours |
| **Time to First Version** | Speed from idea to working solution | 40% faster than baseline |
| **Maintenance Overhead** | Time spent on fixes/support per week | < 10% of team time |

---

## Common Patterns

### Fallback Chain (For Resilience & Ownership)
```
When primary_tool fails:
  → Try fallback_tool
  → If fallback fails:
    → Try another_fallback
    → If all fail:
      → Alert operator, stop and wait
```

### Configuration Externalization (For Speed & Reusability)
```
Do NOT:
  TIMEOUT = 30
  API_KEY = "secret123"
  
Do:
  TIMEOUT = os.getenv("SERVICE_TIMEOUT", "30")
  API_KEY = os.getenv("API_KEY")
```

### Dependency Documentation (For Ownership & Resilience)
```
[dependencies]
- PostgreSQL (stores state; could migrate to MySQL)
- Redis (caching; could replace with local cache)
- Claude API (primary agent; fallback to Ollama)
```

---

## Session Discipline (For Teams & AI Tools)

When working on this project:

### Before Starting
1. **Clarify the goal:** What are we doing?
2. **Define success:** How will we know it's done?
3. **Check gates:** Do we pass Declaration Gate?

### During
1. **Stay focused:** If scope changes, acknowledge it
2. **Document as you go:** Don't wait until the end
3. **Check progress:** Are we moving toward the goal?

### After
1. **Verify completion:** Did we meet success criteria?
2. **Check gates:** Do we pass Integrity & Sovereignty Gates?
3. **Update manifest:** Record any decisions made

---

## Decision Log

Document major decisions with:
- **What:** The decision
- **Why:** Rationale and context
- **When:** Date
- **Impact:** What changes as a result

Example:
```
Decision: Use Claude API as primary agent
Date: 2026-09-01
Why: Speed critical; accuracy important; internet connectivity guaranteed
Fallback: OpenCode (fewer features, works in more environments)
Impact: Setup requires ANTHROPIC_API_KEY
```

---

## When Things Go Wrong

### Project fails a gate
**Declaration Gate:** Declare intent before proceeding  
**Integrity Gate:** Align code with manifest  
**Sovereignty Gate:** Add fallbacks or document risk  

### Stakeholders disagree
Go back to the manifest. The manifest is the source of truth.

### Requirements change mid-project
Document the change in the manifest. Re-run gates if scope is big.

### You discover something critical late
Stop, update the manifest, re-run gates, then proceed.

---

## Key Principles

**Manifest first, code second.** Always.

**Written down beats tribal knowledge.** Always.

**Gates are checkpoints, not obstacles.** They save time by preventing rework.

**Decisions matter more than code.** Document decisions; code is implementation.

**Simpler is better.** If it's hard to explain, it's too complex.

---

_Read README.md for the philosophy. Use this for the how-to._
