# GOVERNANCE.md — How to Execute NXS

This guide tells you how to actually build to the Nexovia Standard. Use it alongside README.md.

---

## Before You Start: Gate 1 — Declaration

Spend 30 minutes writing this down. Not in your head. Written.

**Create a file called `project_declaration.md` in your repo root:**

```markdown
# Project Declaration

## What problem are we solving?
[One clear sentence. Not "improve systems" — be specific.]

## What's in scope?
- 
- 

## What's out of scope?
- 
- 

## How will we know it's done?
[The definition of done checklist — what needs to be true before we ship?]

## Dependencies (preliminary)
- [Database choice and why]
- [External APIs and why]
- [Languages/frameworks and why]
- [Infrastructure and why]

## Handoff target
[Who will need to run this? Describe them.]
```

Stop here. Get agreement. Then code.

---

## Rule 1: Logic Separate from Tools

Your business logic is the part that solves the actual problem. Everything else is just plumbing.

**Here's what separation looks like:**

```
/project
  /core                    ← Business logic (testable, tool-agnostic)
    logic.py
    models.py
    handlers.py
  /infrastructure          ← Tool-specific code
    database.py
    api.py
    config.py
```

**Test your core logic without any tools:**

```python
# In /core/logic.py — no imports from /infrastructure
def calculate_recommendation(user_history, context):
    return apply_algorithm(user_history, context)

# Test it standalone
assert calculate_recommendation([1,2,3], "context") == expected
```

**The /infrastructure layer wires tools to core logic:**

```python
# In /infrastructure/database.py
from core.logic import calculate_recommendation

def get_recommendation(user_id):
    history = db.query(user_id)
    context = cache.get('context')
    result = calculate_recommendation(history, context)  # Call core logic
    return result
```

**Why this matters:** You can test core logic without standing up a database. You can replace your database later without rewriting logic.

---

## Rule 2: Configuration Never Hardcoded

If it's a string that changes between environments, it goes in configuration.

**Create one configuration file:**

```toml
# config.toml (or .env, or config.yaml — pick one)

[database]
host = "${DB_HOST}"          # From environment
port = "${DB_PORT}"
name = "myapp_prod"           # Can differ per env

[api]
timeout = 30                  # Value, never hardcoded in code
retries = 3

[feature_flags]
new_algorithm = true          # Can be toggled without code change
debug_logging = false
```

**In your code, read it once at startup:**

```python
import config

def main():
    db_host = config.database.host
    timeout = config.api.timeout
    # Use it
```

**Your `config.toml` file goes in version control. Your `.env` file (with secrets) does not.**

Document what each setting does:

```toml
# DATABASE
# The host and port of your database.
# Can be overridden by DB_HOST and DB_PORT environment variables.
# If not set, defaults to localhost:5432
host = "${DB_HOST:localhost}"
```

**Why this matters:** You can deploy the same binary to staging and production by changing configuration, not code.

---

## Rule 3: Every Dependency Visible

Create a single file that lists everything your project depends on.

**Create `DEPENDENCIES.md`:**

```markdown
# Project Dependencies

## Required
- Python 3.11+
  - Why: Async context managers
  - How to replace: Python 3.10 with compatibility shim, or rewrite async code
  
## External Services
- PostgreSQL 13+
  - Why: Main data store
  - How to replace: Swap database layer (< 4 hours, core logic unchanged)
  - When to upgrade: When support ends (2026)

- Redis
  - Why: Caching user sessions
  - How to replace: In-memory cache + database (performance hit, but possible)
  
## Libraries (Python)
- fastapi==0.104.1
  - Why: HTTP server, modern async
  - How to replace: Switch to Flask (API layer only, 2-3 hours)
  
- sqlalchemy==2.0.0
  - Why: Database ORM
  - How to replace: Raw SQL queries (tedious, but possible)

- pydantic==2.0
  - Why: Data validation
  - How to replace: Manual validation (slow to write, easy to break)

## CI/CD
- GitHub Actions
  - Why: Free for public repos, integrates with GitHub
  - How to replace: GitLab CI or Jenkins (CI config only)

- Docker
  - Why: Reproducible environments
  - How to replace: Manual server setup (not recommended; very fragile)

## Threat: What could break us?
- PostgreSQL goes away → Very unlikely, but rewrite would take 2 weeks
- Redis becomes paid → We could go in-memory tomorrow
- fastapi unmaintained → Switch to Flask or Django (infrastructure layer only)
```

**Why this matters:** When someone asks "can we replace this?", you already know the answer and how long it takes.

---

## Rule 4: Runs Anywhere, for Anyone

Setup should be one command. Not three commands, not "just run these manual steps first." One command.

**Create a setup script:**

```bash
#!/bin/bash
# setup.sh

set -e

echo "Setting up NXS example project..."

# Check dependencies
if ! command -v python3 &> /dev/null; then
    echo "❌ Python 3 not found"
    exit 1
fi

if ! command -v docker &> /dev/null; then
    echo "❌ Docker not found"
    exit 1
fi

# Install Python dependencies
pip install -r requirements.txt

# Start Docker services
docker-compose up -d

# Wait for services to be ready
sleep 5

# Initialize database
python scripts/init_db.py

echo "✅ Setup complete"
echo "Run: python main.py"
```

**Now setup is:**

```bash
$ ./setup.sh
```

**Not:**

```
1. Install Docker
2. Install Python
3. pip install -r requirements.txt
4. Run docker-compose up -d
5. Wait 30 seconds
6. python scripts/init_db.py
7. If that fails, check that Redis is running
```

**Why this matters:** New developer runs one command. It works. They're productive in minutes, not hours.

---

## After You Build: Gate 2 — Integrity

Before you call it done, check these boxes:

**Structure Check:**
- [ ] Core logic has no tool imports (python: no db, no HTTP, no file I/O)
- [ ] Configuration is external (all values in config file or env vars)
- [ ] Dependencies are documented (DEPENDENCIES.md exists and is complete)
- [ ] Setup is automated (one command that works)

**Code Check:**
- [ ] Logic is testable in isolation (test core without tools)
- [ ] Error handling is explicit (failures are named, not silent)
- [ ] Logging tells the story (can I follow what happened from logs alone?)

**Operations Check:**
- [ ] Can someone else run this? (Actually let them, unsupervised)
- [ ] Does it fail gracefully? (Errors are clear, not mysterious)
- [ ] Can you see what's happening? (Metrics, logs, health checks)

---

## Before You Ship: Gate 3 — Sovereignty

This gate confirms you're not locked in.

**Lock-in check:**
- [ ] Could we swap the database? (1-2 days of work max)
- [ ] Could we move to different cloud? (Infrastructure layer changes, logic untouched)
- [ ] Could we rewrite in a different language? (Logic is independent, just rewrite infrastructure)

**If you answer "no" or "weeks of work," you have a lock-in problem. Go fix it before shipping.**

**Operational clarity:**
- [ ] Who runs this in production? (Name them)
- [ ] How do they run it? (Step by step in RUNBOOK.md)
- [ ] What could go wrong? (List it. How would they fix it?)

**Handoff is real:**
- [ ] Did someone who didn't build this actually run the setup script? (Not "I ran it and it worked." Actually let them do it.)
- [ ] Did they understand the code? (Ask them to describe one piece)

**Metrics wired:**
- [ ] Can you see each outcome? (Time to handoff? Deployment time? Error rates?)
- [ ] Is it tracked somewhere? (Dashboard, monitoring, or spreadsheet — somewhere)

---

## Common Pattern: External Dependencies

When your code needs to call external services, use a pattern like this:

```python
# /core/logic.py — This doesn't know or care about external services
def recommend_product(user_history):
    # Pure logic, testable without anything external
    return algorithm(user_history)

# /infrastructure/api_client.py — External service isolation
class ExternalRecommendationAPI:
    def __init__(self, url, timeout):
        self.url = url
        self.timeout = timeout
    
    def fetch_recommendation(self, user_id):
        # If this service is down, the error stays here
        return self.call(f"{self.url}/recommendation/{user_id}")

# /infrastructure/handler.py — Wire them together
def get_recommendation_for_user(user_id):
    # Try external first (faster)
    try:
        return ExternalRecommendationAPI().fetch_recommendation(user_id)
    except ServiceUnavailable:
        # Fall back to local logic if external is down
        history = database.get_user_history(user_id)
        return recommend_product(history)
```

This way, if the external service is down, your app still works. If you need to replace it, you change one file.

---

## Decision Logging

When you make a decision that affects the standard, log it.

**Create `DECISIONS.md`:**

```markdown
# Decisions

## Decision: Use PostgreSQL instead of MongoDB
Date: 2025-09-01
Reasoning: We need ACID guarantees. MongoDB lost that tradeoff.
Impact: Schema migrations required, joins are now possible
Revert path: 2 days of work (if needed)

## Decision: Move logic to /core package
Date: 2025-09-05
Reasoning: Core logic was scattered. Moving makes it testable without tools.
Impact: New developers must respect core/infrastructure boundary
Revert path: Can split back out, but not recommended

## Decision: Use environment variables for all config
Date: 2025-09-08
Reasoning: Simpler than config files, works in containers
Impact: No more project-specific config files in repo
Revert path: Easy (parse env vars to config file instead)
```

When someone asks "why did you do this?", you have an answer.

---

## Check Your Work

When you think you're done, run this checklist:

```
NXS Compliance Checklist
=======================

Definition of Done (all 7):
☐ Logic works in isolation
☐ Configuration is external
☐ All dependencies explicit
☐ Setup is automated
☐ Runs same way everywhere
☐ Understandable without original author
☐ Handoff tested with real person

The Four Rules:
☐ Rule 1: Logic separate from tools
☐ Rule 2: Configuration never hardcoded
☐ Rule 3: Every dependency visible
☐ Rule 4: Runs anywhere, for anyone

The Three Gates:
☐ Gate 1: Declaration (done before coding)
☐ Gate 2: Integrity (done after building)
☐ Gate 3: Sovereignty (done before shipping)

The Four Outcomes (measurable):
☐ Resilience: Handoff < 2 hours (tested)
☐ Reusability: Logic works elsewhere unchanged
☐ Ownership: Tool swap < 4 hours (or proven impossible)
☐ Speed: Setup < 5 min, iterate < 10 min
```

If you check all these boxes, you're compliant.

---

_That's how you execute the Nexovia Standard. One project at a time._
