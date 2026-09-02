# The Nexovia Standard — Complete Index

**Version:** 2.0  
**Last Updated:** September 2026

---

## Start Here

- **README.md** — The complete standard in one document
  - What is NXS?
  - The four business outcomes (Resilience, Reusability, Ownership, Speed)
  - The four rules
  - Definition of Done (7 checkboxes)
  - How to measure quality (4 metrics + outcome-specific tests)
  - Governance gates

---

## For Different Audiences

### For Business Leaders & Project Sponsors
Read in this order:
1. README.md — "The Four Business Outcomes" section
2. README.md — "How to Measure Delivery Quality" section
3. Skip the rules and gates; they're for technical teams

**Key takeaway:** Measure your projects against the four outcomes using timers and concrete tests. That's your accountability framework.

### For Developers & Software Architects
Read in this order:
1. README.md — Full document
2. GOVERNANCE.md — Sections 1-6 (rules, topology, gates)
3. MANIFEST-SPEC.md — How to structure project manifests

**Key takeaway:** Build toward the four outcomes. Tests tell you when you've succeeded.

### For AI Tools & Agents
Read in this order:
1. README.md — The four outcomes (understand what you're enabling)
2. SYSTEM-PROMPT.md — Universal session framework
3. GOVERNANCE.md — Sections 7-8 (agent behavior, drift detection, writing style)

**Key takeaway:** Classify sessions. Run diagnostic gateway. Apply rigour accordingly. Check outcomes, not just rules.

### For Teams Using NXS
Read in this order:
1. README.md — Full document
2. GOVERNANCE.md — Full document (your operational constitution)
3. Use MANIFEST-SPEC.md as your project structure template

**Key takeaway:** This is your single source of truth. Reference it when decisions conflict.

---

## Deep Dives by Topic

### Understanding Outcomes
- README.md — "The Four Business Outcomes" section
- GOVERNANCE.md — "Quick Reference: The Four Outcomes" table

### Building Solutions That Achieve Outcomes
- README.md — "The Four Rules of NXS" section
- README.md — "Measuring the Four Outcomes" section (outcome-specific tests)

### Project Topology & Structure
- GOVERNANCE.md — "Section 4: The Topology"
- MANIFEST-SPEC.md — Full specification

### Delivery Gates & Compliance
- GOVERNANCE.md — "Section 5: The Three Delivery Gates"
- GOVERNANCE.md — "Section 1: The Four Rules"

### Session Discipline (For Agents & Teams)
- GOVERNANCE.md — "Section 7: The Agent Behaviour Layer"
  - Session classification
  - Diagnostic gateway
  - Drift detection
  - Session close

### Writing Standards
- GOVERNANCE.md — "Section 8: Writing Style Standard"
- SYSTEM-PROMPT.md — "Writing Style" section

### Universal System Prompt
- SYSTEM-PROMPT.md — Complete file
  - Set this once in your AI tool
  - Applies to every session automatically

---

## File Guide

| File | Purpose | Read When |
|------|---------|-----------|
| **README.md** | The Nexovia Standard explained: outcomes, rules, metrics, gates | Starting NXS; understanding the philosophy |
| **GOVERNANCE.md** | Operational playbook: how to execute NXS; session discipline; gates | Building under NXS; need detailed guidance |
| **SYSTEM-PROMPT.md** | Universal AI system prompt; set once, applies everywhere | Configuring AI tools; want consistent behavior |
| **MANIFEST-SPEC.md** | Project manifest format (project_manifest.toml structure) | Creating new projects; defining topology |
| **INDEX.md** | This file; navigation guide | Finding what you need |

---

## The Core Principle (Delivery Sovereignty)

Every document serves delivery sovereignty:

> The team that commissions a solution retains full understanding, full control, and full portability of what was built. This is true regardless of what tool built it, what AI generated it, or who on the team originally delivered it.

A sovereign solution can be:
- Understood without reading the code
- Reused without rebuilding
- Extended without breaking things
- Packaged as a reusable module
- Maintained without depending on original builder

---

## How Documents Relate

```
README.md (What & Why)
  ├─ What is NXS? Outcome-first definition
  ├─ The four business outcomes
  ├─ The four rules (and what they enable)
  ├─ Definition of Done (7 checkboxes)
  └─ How to measure quality
       │
       ├─ Enables GOVERNANCE.md (How)
       │    ├─ How to execute rules
       │    ├─ Topology & schema
       │    ├─ Three gates
       │    ├─ Agent behavior layer
       │    └─ Session discipline
       │         │
       │         └─ Enabled by SYSTEM-PROMPT.md
       │              └─ Universal system prompt for AI tools
       │
       └─ Enabled by MANIFEST-SPEC.md
            └─ Project structure template
```

---

## Key Concepts by Outcome

### Resilience (Project Survives Without Original Builder)
- How: Declare intent separately; document decisions; make handoff testable
- Where: README.md "Resilience" outcome; GOVERNANCE.md Declaration Gate
- Test: Handoff < 2 hours; system runs 1 week without builder

### Reusability (Same Logic, Multiple Contexts)
- How: Parameterize logic; externalize config; separate concerns
- Where: README.md "Reusability" outcome; GOVERNANCE.md Integrity Gate
- Test: Deploy to 2+ projects; adaptation < 2 hours

### Ownership (Not Locked Into Tools)
- How: Separate logic from tools; document fallbacks; audit lock-in
- Where: README.md "Ownership" outcome; GOVERNANCE.md Sovereignty Gate
- Test: Tool swap < 4 hours; fallback works automatically

### Speed (Ship Faster, Iterate Faster)
- How: Automate setup; reuse decisions; track time waste
- Where: README.md "Speed" outcome; GOVERNANCE.md all gates
- Test: Setup 5 min; iteration < 10 min; decisions reused across projects

---

## Versioning

**NXS v2.0** is the current version.

**What changed in v2.0:**
- Added four business outcomes as the foundation
- Mapped each rule to outcomes it enables
- Added outcome-specific tests
- Integrated AI-era thinking (intent-centric, not implementation-centric)
- Restructured documentation for clarity

**Future versions** will maintain backward compatibility with v2.0 while adding new patterns.

Declare your compliance version in your manifest:
```toml
[project]
nxs_version = "2.0"
```

---

## Quick Links

- GitHub: https://github.com/nex-ovia/NXS
- Website: https://www.nex-ovia.com
- Report gaps or suggest patterns: Open a discussion on GitHub

---

## How to Use This Index

- **Lost?** Find your audience above; follow the read order
- **Looking for X?** Check "Deep Dives by Topic"
- **Understanding how documents relate?** See "How Documents Relate"
- **Need the manifest spec?** Open MANIFEST-SPEC.md directly
- **Setting up AI tools?** Copy SYSTEM-PROMPT.md to your tool's settings

---

_The Nexovia Standard: because a solution built once should work, grow, and last._
