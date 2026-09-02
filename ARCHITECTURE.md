# NXS v2.0 — Complete Architecture

## Repository at a Glance

```
The Nexovia Standard v2.0
│
├─ README.md ━━━━━━━━━━━━━━━━━━━━━━━━━━━━ THE STANDARD (What & Why)
│  ├─ What is NXS?
│  ├─ Four Business Outcomes ◄─────────── NEW in v2.0: Outcome-first framing
│  ├─ Four Rules (+ outcome mapping)
│  ├─ Definition of Done (7 checkboxes)
│  ├─ Quality Metrics (4 + outcome-specific tests)
│  └─ Governance Gates (3, outcome-mapped)
│
├─ GOVERNANCE.md ━━━━━━━━━━━━━━━━━━━━━ THE PLAYBOOK (How to Execute)
│  ├─ Quick Reference: Outcomes table ◄─── NEW: Outcome quick lookup
│  ├─ Four Rules (operational details)
│  ├─ Definition of Done (how to verify)
│  ├─ Topology & Node Schema
│  ├─ Three Gates (enforcement)
│  └─ Agent Behavior Layer (session discipline)
│
├─ SYSTEM-PROMPT.md ━━━━━━━━━━━━━━━ AI SYSTEM PROMPT (Apply Universally)
│  ├─ Session classification
│  ├─ Diagnostic gateway
│  ├─ Drift detection
│  └─ Writing standards
│
├─ MANIFEST-SPEC.md ━━━━━━━━━━━━━━ PROJECT TEMPLATE (Structure Projects)
│  ├─ Root configuration
│  ├─ Node schema
│  └─ Decision logic
│
├─ INDEX.md ━━━━━━━━━━━━━━━━━━━━━ NAVIGATION (Find What You Need) ◄─── NEW
│  ├─ Audience-specific read orders
│  ├─ Deep dives by topic
│  ├─ File guide
│  └─ How docs relate
│
├─ QUICK-START.md ━━━━━━━━━━━━━━━ 5-MINUTE SUMMARY (Onboard Quickly) ◄─ NEW
│  ├─ The standard in 5 minutes
│  ├─ Outcomes + rules (tables)
│  ├─ Role-specific guidance
│  └─ Common Q&A
│
└─ CHANGELOG.md ━━━━━━━━━━━━━━ v2.0 UPDATE SUMMARY (What Changed) ◄─── NEW
   ├─ What changed
   ├─ What didn't change
   ├─ Migration guide
   └─ Feedback questions
```

---

## Document Flow (How Readers Use Them)

### For Understanding the Philosophy
```
START
  │
  └─→ README.md
       ├─ skim "What is NXS?"
       ├─ read "The Four Business Outcomes"
       ├─ scan "The Four Rules"
       └─ DONE (philosophy clear)
```

### For Building a Solution
```
START
  │
  ├─→ QUICK-START.md (5 min overview)
  │
  ├─→ README.md (full standard)
  │   ├─ outcomes
  │   ├─ rules
  │   └─ definition of done
  │
  ├─→ MANIFEST-SPEC.md (structure your project)
  │   └─ create project_manifest.toml
  │
  ├─→ GOVERNANCE.md (execute NXS)
  │   ├─ gates (declaration, integrity, sovereignty)
  │   └─ topology
  │
  └─→ Build using the framework
```

### For Leading a Project
```
START
  │
  └─→ QUICK-START.md
       ├─ "The Four Business Outcomes"
       ├─ "How to Measure Quality"
       └─ DONE (you have accountability framework)
```

### For Configuring AI Tools
```
START
  │
  ├─→ README.md (understand outcomes)
  │
  └─→ SYSTEM-PROMPT.md (copy to your AI tool settings)
       └─ applies to every session automatically
```

---

## The Four Outcomes (Central to Everything)

```
Every rule, gate, and decision in NXS exists to enable one of these:

┌────────────────────────────────────────────────────────┐
│                                                        │
│  RESILIENCE                  REUSABILITY              │
│  Project survives            Same logic works         │
│  without original builder    in 5+ contexts           │
│                                                        │
│  Enabled by: Rules 3, 4      Enabled by: Rules 1, 2  │
│  Tested by: Handoff < 2h     Tested by: Deploy 2+    │
│            System runs 1 week unchanged               Adapt < 2h    │
│                                                        │
│  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━  │
│                                                        │
│  OWNERSHIP                    SPEED                   │
│  Business is not locked      Ship 40% faster          │
│  into tools                  Iterate 6x faster        │
│                                                        │
│  Enabled by: Rules 1, 3      Enabled by: Rules 2, 4  │
│  Tested by: Tool swap < 4h   Tested by: Setup 5 min  │
│            Fallback works    Iteration < 10 min      │
│                                                        │
└────────────────────────────────────────────────────────┘
```

---

## How Four Rules Enable Outcomes

```
RULE 1: Logic Separate from Tools
  ↓
  Enables: OWNERSHIP (tool swaps work)
         + REUSABILITY (logic works anywhere)
         + RESILIENCE (intent survives tool changes)

RULE 2: Configuration Externalised
  ↓
  Enables: SPEED (setup automated)
         + REUSABILITY (same code, different configs)
         + RESILIENCE (new person doesn't break things)

RULE 3: Dependencies Visible
  ↓
  Enables: OWNERSHIP (audit lock-in)
         + RESILIENCE (handoff is clear)
         + SPEED (no debugging unknown deps)

RULE 4: Runs Anywhere, For Anyone
  ↓
  Enables: RESILIENCE (handoff requires only docs)
         + SPEED (new device setup automated)
         + REUSABILITY (works in any context)
```

---

## Quality Measurement Pyramid (v2.0)

```
                    OUTCOMES ACHIEVED
                    (What matters to business)
                           ▲
                           │
                    ┌──────┴──────┐
                    │   TESTS     │
             Outcome-specific tests
             (Handoff < 2h, Tool swap < 4h, etc.)
                    │             │
                    └──────┬──────┘
                           ▲
                           │
                    ┌──────┴──────┐
                    │   METRICS   │
              (Time to understand,
               Swap time, Time to first version,
               Maintenance overhead)
                    │             │
                    └──────┬──────┘
                           ▲
                           │
                    ┌──────┴──────────┐
                    │  CHECKLIST (7)  │
          Purpose documented
          Logic identifiable
          Dependencies listed
          Config externalised
          Runs anywhere
          Health verifiable
          Stable under load
                    │               │
                    └──────┬────────┘
                           ▲
                           │
                    ┌──────┴──────┐
                    │  THE RULES  │
              (Logic separate, Config external,
               Deps visible, Runs anywhere)
```

---

## Three Gates (All Must Pass)

```
No implementation begins
            │
            ├─→ DECLARATION GATE
            │   Intent defined in manifest?
            │   ✓ PASS ──┐
            │ ✗ FAIL     └─→ INTEGRITY GATE
            ├─→ INTEGRITY GATE
            │   Physical project matches
            │   declared topology?
            │   ✓ PASS ──┐
            │ ✗ FAIL     └─→ SOVEREIGNTY GATE
            ├─→ SOVEREIGNTY GATE
            │   All dependencies declared?
            │   Sovereignty goals met?
            │   ✓ PASS ──┐
            │ ✗ FAIL     └─→ BUILD BLOCKED
                         │
                         └─→ Can Proceed (All gates pass)
```

---

## Repository Navigation (v2.0)

```
Lost? Start here:

1. Need philosophy?          → README.md
2. Quick overview?           → QUICK-START.md
3. Building something?       → INDEX.md (read order)
4. Executing NXS?            → GOVERNANCE.md
5. Setting up project?       → MANIFEST-SPEC.md
6. Configuring AI?           → SYSTEM-PROMPT.md
7. Finding specifics?        → INDEX.md (deep dives)
8. What changed in v2.0?     → CHANGELOG.md
```

---

## Core Principle at Every Level

Every document serves one core principle:

```
DELIVERY SOVEREIGNTY

The team that commissions a solution retains:
  ├─ Full understanding   (can read what it does without code)
  ├─ Full control         (can change vendors without rebuild)
  ├─ Full portability     (can move between teams/projects)
  └─ Long-term ownership  (maintains without original builder)

        ↓ Requires ↓

Four Rules:
  ├─ Logic separate from tools
  ├─ Configuration externalised
  ├─ Dependencies visible
  └─ Runs anywhere, for anyone

        ↓ Enables ↓

Four Outcomes:
  ├─ Resilience (survives departure)
  ├─ Reusability (works in multiple contexts)
  ├─ Ownership (not locked into tools)
  └─ Speed (40% faster, 6x faster iterations)
```

---

_The Nexovia Standard v2.0: Outcome-first, AI-era ready, built for delivery sovereignty._
