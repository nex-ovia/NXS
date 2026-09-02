# Getting Started with NXS

**This guide helps you understand and use the Nexovia Standard for your first project.**

---

## 5-Minute Overview

NXS has **four outcomes** that matter: Resilience, Reusability, Ownership, Speed.

Every project should achieve these:

| Outcome | Means | How You Know It Worked |
|---------|-------|----------------------|
| **Resilience** | Project survives without you | Someone else ran it from docs alone in <2 hours |
| **Reusability** | Same logic works in 5+ places | You deployed to a new project without changing code |
| **Ownership** | Never locked into one tool | You swapped a tool in <4 hours |
| **Speed** | Build and iterate fast | Setup took 5 min, changes take 10 min |

---

## The Workflow (13 Steps)

### Phase 1: Discovery (30 min)

**Step 1: Answer 9 Questions**

Before writing code, write down:
1. What problem are we solving?
2. How will we know it worked?
3. What's IN scope, what's OUT?
4. Every external system we depend on
5. When does it need to ship?
6. What could go wrong?
7. Who needs to approve or know?
8. What are we assuming?
9. What are we NOT allowed to do?

This is Gate 1 (Declaration). It prevents surprises later.

**Step 2: Map Each Component to Outcomes**

For every piece of code or service, ask: "Which of the four outcomes does this serve?"

- Database → Resilience + Reusability
- Error handler → Resilience
- Configuration → Ownership + Speed
- Setup automation → Speed

Every component needs at least one outcome. This forces clear thinking.

### Phase 2: Build (Variable)

**Step 3: Build Logic Independent of Tools**

Write your core business logic without importing any external tool.

Bad: `import database; database.query()`  
Good: `def calculate_revenue(orders): return sum(order.amount for order in orders)`

Test your logic in isolation. If it works without the database or API, you've passed.

**Step 4: Put Configuration Outside Code**

Any value that changes across environments (URLs, passwords, API keys) goes in environment variables or config files.

Bad: `api_url = "https://production.example.com"`  
Good: `api_url = os.environ["API_URL"]`

Now your code runs the same locally and in production.

**Step 5: Document Every Dependency**

Create `DEPENDENCIES.md` listing:
- What external system (PostgreSQL, Redis, AWS)
- Why you need it
- What version
- What could replace it (fallback)
- How long it takes to swap

Example:
```
PostgreSQL | 14 | Relational queries and ACID guarantees | MySQL 8 | 3-4 hours to migrate schema
AWS Lambda | Latest | Serverless execution | Cloud Run | 2 hours to port code
```

**Step 6: Automate Setup**

Create `setup.sh` that new developers run once:

```bash
#!/bin/bash
git clone [repo]
cd [repo]
npm install
python -m pip install -r requirements.txt
./create_database.sh
pytest tests/
```

Anyone should be able to clone and run `./setup.sh` and have a working environment.

### Phase 3: Testing (2-4 hours)

**Step 7: Write Core Tests (70%+ coverage)**

Test your business logic:
```python
def test_calculate_revenue():
    orders = [Order(100), Order(200)]
    assert calculate_revenue(orders) == 300
```

Run: `pytest --cov=src/ --cov-min=70`

Core logic must have ≥70% coverage. Infrastructure code doesn't need 100%.

**Step 8: Write Integration Tests**

Test that your components work together:
```python
def test_order_to_payment_flow():
    order = create_order("item_123", 100)
    payment = process_payment(order)
    assert payment.status == "complete"
```

### Phase 4: Verification (1 hour)

**Step 9: Pass Gate 2 (Integrity Checks)**

Before saying "done," run these 9 checks:

1. ✅ No passwords or API keys in code
2. ✅ DEPENDENCIES.md exists and is complete
3. ✅ setup.sh runs without errors
4. ✅ Core tests pass (70%+ coverage)
5. ✅ Integration tests pass
6. ✅ RUNBOOK.md exists
7. ✅ Project manifest validates against schema
8. ✅ nxs-manifest.toml exists
9. ✅ No hardcoded URLs or localhost references

If any check fails, fix it and recheck.

**Step 10: Write RUNBOOK.md**

Pretend you're gone for 6 months. Write step-by-step instructions for:
- How to set up the environment
- How to run this
- What to do if something breaks
- How to monitor it
- How to respond to common incidents

Then **have someone else follow your RUNBOOK.md and actually run it.** If they get stuck, rewrite that section.

**Step 11: Document Why**

Write:
- Why you made each architectural choice
- What tradeoffs you made
- What problems you're NOT solving
- What future changes might be needed

Put this in `DECISIONS.md` or `ARCHITECTURE.md`.

### Phase 5: Sovereignty (1 hour)

**Step 12: Pass Gate 3 (Sovereignty Checks)**

Before shipping to production, verify:

1. ✅ Could we swap the database in 4 hours? (Not 4 weeks)
2. ✅ Can we export all our data in JSON or CSV?
3. ✅ Are we locked into a specific cloud provider? (No)
4. ✅ Is observability wired? (Logs, metrics, traces)
5. ✅ Did someone unfamiliar with the code follow RUNBOOK.md and succeed?
6. ✅ Is there any "only person_X knows how to do this"? (No)
7. ✅ Is everything in git with clean history?
8. ✅ Are README, RUNBOOK, DECISIONS, API docs all written and current?

If any check fails, fix it.

**Step 13: Ship**

Deploy to production with confidence.

---

## The Four Rules (Why They Matter)

These four rules make the four outcomes possible:

### Rule 1: Logic Separate from Tools
Your core business logic should work in Python, JavaScript, Go, or any language without changes.

**Test:** Can you test your core logic without the database or API?

### Rule 2: Configuration Never Hardcoded
Every value that changes lives in environment variables or config files, never in code.

**Test:** Can you deploy this to 5 different environments without editing code?

### Rule 3: Every Dependency Visible
You know exactly what you depend on, why, and what could replace it.

**Test:** Can someone list all dependencies without guessing?

### Rule 4: Runs Anywhere, for Anyone
The same setup process works on your laptop, CI/CD, and production. No secret manual steps.

**Test:** Does `./setup.sh` work on a fresh clone?

---

## Common Questions

**Q: Do I need to follow ALL 13 steps?**  
A: Yes. These aren't suggestions; they're gates. Missing steps create technical debt that kills resilience later.

**Q: What if my project is small?**  
A: Scale the effort, not the rigor. Gate 1 might take 15 min instead of 30. RUNBOOK.md might be 1 page instead of 5. But don't skip steps.

**Q: What if I'm using an LLM agent to build?**  
A: Agent loads `nxs_schema.toml` first, then reference the three TOML files (nxs_schema.toml, governance.toml, skill.toml) as needed. This keeps token usage efficient.

**Q: Can I modify the gates or policies?**  
A: No. NXS is a standard. If you need to modify it for your org, you're extending NXS, not using NXS. See GOVERNANCE.md "Extend for New Frameworks" if you want to customize.

**Q: How do I start?**  
A: Copy `nxs-manifest.toml` from MANIFEST-SPEC.md to your project root and answer each field. That's your project declaration.

---

## Next Steps

1. Read **README.md** — Understand what NXS is
2. Copy **nxs-manifest.toml** from MANIFEST-SPEC.md to your project
3. Answer the 9 questions in Step 1 above
4. Follow the 13-step workflow
5. Reference `governance.toml` and `skill.toml` when you need specific enforcement details

---

**NXS is simple because it answers one question at a time. Finish one phase before moving to the next.**
