# NXS v2.0 at a Glance

## The Nexovia Standard in 5 Minutes

### What Is It?
A delivery standard for the AI era grounded in **delivery sovereignty**: the team that pays for a solution retains full understanding, control, and portability forever.

### Why It Matters
Solutions don't fail because they're built slow. They fail because:
- Nobody can explain how they work (tribal knowledge)
- Swapping tools requires rebuilding from scratch
- Original builder leaves and everything breaks
- Same solution duplicated across 5 projects

NXS makes these failures structurally impossible.

---

## The Four Business Outcomes

Every NXS project enables one or more of these:

| Outcome | Business Meaning | How You Know You've Succeeded |
|---------|-----------------|-----|
| **Resilience** | Project survives without original builder | Handoff < 2 hours; system runs 1 week unchanged |
| **Reusability** | Same logic works in 5+ different contexts | Deployed to 2+ projects; adaptation < 2 hours |
| **Ownership** | Business is not locked into tools | Tool swap < 4 hours; fallback works automatically |
| **Speed** | Ship 40% faster; iterate 6x faster | Setup 5 min; iteration < 10 min; decisions reused |

---

## The Four Rules (And What They Enable)

| Rule | Meaning | Enables |
|------|---------|---------|
| **Logic separate from tools** | Business decisions live independently from implementation | Ownership · Reusability · Resilience |
| **Config externalised** | No hardcoded values in code; everything comes from environment | Speed · Reusability · Resilience |
| **Dependencies visible** | Every external system is named and documented | Ownership · Resilience · Speed |
| **Runs anywhere, for anyone** | No tribal knowledge; new person can run it without asking | Resilience · Speed · Reusability |

---

## Definition of Done (7 Checkboxes)

A solution is complete when:

- [ ] Purpose documented (anyone understands what it does)
- [ ] Logic identifiable (business rules are clear and separate)
- [ ] Dependencies listed (every external system is named)
- [ ] Configuration externalised (nothing hardcoded)
- [ ] Runs anywhere (new person can run it on any machine)
- [ ] Health verifiable (defined way to check if it's working)
- [ ] Stable under load (tested at real-world volume)

---

## How to Measure Quality

| Metric | Target | Outcome(s) |
|--------|--------|-----------|
| Time to Understand | < 2 hours | Resilience |
| Dependency Swap Time | < 4 hours | Ownership |
| Time to First Version | 40% faster than baseline | Speed |
| Maintenance Overhead | < 10% of team time | Speed · Resilience |

---

## Three Governance Gates (All Must Pass)

1. **Declaration Gate:** No implementation until intent is in the manifest
2. **Integrity Gate:** Physical project matches declared topology
3. **Sovereignty Gate:** All dependencies declared; no hidden lock-in

---

## The Outcome-First Paradigm (v2.0)

**Old:** "Follow these rules; check these boxes"

**New:** "Achieve these outcomes; tests prove it"

- Start with outcome you care about (resilience, speed, ownership, reusability)
- Rules and gates exist to enable that outcome
- Tests measure success objectively (timers, pass/fail)
- Leaders measure outcomes; developers build toward them

---

## For Different Roles

### Project Leaders
- Measure your projects against the four outcomes
- Use the four metrics + outcome-specific tests as accountability
- You don't need to read code; read the manifest and decision log

### Developers
- Build toward the four outcomes, not just the rules
- Follow the Definition of Done checklist
- Reference manifests + decision audit trails
- Outcome tests tell you when you're done

### AI Tools & Agents
- Classify every session (simple, moderate, complex)
- Run diagnostic gateway for complex sessions
- Detect drift; correct course
- Apply the right rigour to the right situation

### Teams
- Use GOVERNANCE.md as your constitution
- Define "done" by outcomes, not hours or features
- Track time waste; optimize it
- Audit decisions; replay them when needed

---

## Quick Reference: Where to Find What

| Need | Go To |
|------|-------|
| Understand NXS philosophy | README.md |
| See business outcomes clearly | README.md "The Four Business Outcomes" |
| Learn the four rules in detail | README.md "The Four Rules of NXS" |
| Understand how to execute NXS | GOVERNANCE.md |
| Set up a project structure | MANIFEST-SPEC.md |
| Configure AI tools for NXS | SYSTEM-PROMPT.md |
| Understand session discipline | GOVERNANCE.md Section 7 |
| Know how documents relate | INDEX.md |

---

## The One-Sentence Summary

**NXS is a standard that makes solutions portable, reusable, and independent of any single person or tool by making outcomes measurable and gating all work on four principles: clear intent, externalized configuration, visible dependencies, and documented operation.**

---

## Visual: How Outcomes Connect

```
Build with Intent
  (declare what you're doing)
       ↓
     [Enables RESILIENCE]
       ↓
  Separate Logic from Tools
    (parameterize business rules)
       ↓
     [Enables REUSABILITY]
       ↓
  Externalize Configuration
    (no hardcoded environment-specific values)
       ↓
     [Enables SPEED]
       ↓
  Document Dependencies & Fallbacks
    (know what you're locked into; plan B exists)
       ↓
   [Enables OWNERSHIP]
       ↓
   Solution Achieves All Four Outcomes
   ↓
   Future-Proof. Portable. Unmissable.
```

---

## Common Questions

**Q: Do I have to follow all four rules?**  
A: All four rules protect delivery sovereignty. Skip one and you lose an outcome. But if your project legitimately can't meet a rule, document the exception and its risk.

**Q: What if I'm building something throwaway?**  
A: NXS applies to "production-grade" solutions. Quick prototypes, proofs of concept, experiments: use common sense. Once it's business-critical, apply NXS.

**Q: Does this slow down development?**  
A: No. It accelerates it. Setup automation, decision reuse, and clear intent save 10x the time you spend on structure.

**Q: Who enforces NXS?**  
A: You do. The gates are there to prompt; whether you follow them is a choice. But if you skip them, you'll pay the price later when solutions become unmaintainable.

**Q: Can I use NXS with AI-generated code?**  
A: Yes. That's the whole point of v2.0. AI generates code. You write intent (what should happen). NXS captures intent separately, making solutions portable across tools and LLMs.

---

## Next Steps

1. **If you're new to NXS:** Read README.md end-to-end
2. **If you're building something:** Use INDEX.md to find your read order
3. **If you're implementing NXS:** Read GOVERNANCE.md; use it as your operating system
4. **If something is unclear:** Reference GOVERNANCE.md Section 7 (Gaining Clarity)

---

_The Nexovia Standard: because a solution built once should work, grow, and last._
