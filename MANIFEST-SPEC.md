# NXS Project Manifest Template

Every NXS project should have a `nxs-manifest.toml` file in the project root that answers the 9 Declaration questions.

---

## Template: nxs-manifest.toml

```toml
[project]
name = "My Project"
description = "Brief description of what this project does"
version = "0.1.0"

[declaration]
# Gate 1: These 9 fields are mandatory before coding starts

goal = "What problem are we solving?"
success_metrics = "How will we know it worked?"
scope_boundary = "What is IN scope, what is OUT?"
dependencies = "Every external system we depend on"
timeline = "When does it need to ship?"
known_risks = "What could go wrong?"
stakeholders = "Who needs to approve or know?"
assumptions = "What are we assuming to be true?"
constraints = "What are we NOT allowed to do?"

[outcomes]
# Map this project to NXS outcomes

resilience = "How does this project help systems survive change?"
reusability = "How can this be used in other projects unchanged?"
ownership = "How does this avoid tool lock-in?"
speed = "How does this enable fast setup and iteration?"

[structure]
# Reference key files required by NXS

nxs_standard = "https://github.com/nex-ovia/NXS"
manifest = "nxs-manifest.toml"
dependencies_file = "DEPENDENCIES.md"
runbook_file = "RUNBOOK.md"
setup_script = "setup.sh"

[gates]
# Track gate passage

gate_1_declaration = false  # Set to true after Gate 1 passes
gate_2_integrity = false    # Set to true after Gate 2 passes
gate_3_sovereignty = false  # Set to true after Gate 3 passes
```

---

## How to Use This Template

1. **Copy** `nxs-manifest.toml` to your project root
2. **Fill in** the 9 Declaration fields (Gate 1)
3. **Update outcomes** to show how your project serves the standard
4. **Reference** your required files (DEPENDENCIES.md, RUNBOOK.md, setup.sh)
5. **Mark gates as true** as you pass Gate 2 and Gate 3

---

## What Each Section Means

**`[project]`**: Basic metadata about your project

**`[declaration]`**: The 9 mandatory questions from Gate 1 (before coding)

**`[outcomes]`**: How this project aligns with NXS outcomes (Resilience, Reusability, Ownership, Speed)

**`[structure]`**: References to required files and the standard

**`[gates]`**: Tracks which gates you've passed

---

## Minimal Example

```toml
[project]
name = "Customer API"
version = "1.0.0"

[declaration]
goal = "Provide REST API for customer queries"
success_metrics = "API responds in <100ms, 99.9% uptime"
scope_boundary = "Read-only queries only, no updates"
dependencies = "PostgreSQL 14, Redis 7, AWS Lambda"
timeline = "Ship by end of sprint"
known_risks = "Database migration could cause downtime"
stakeholders = "Platform team, Support team"
assumptions = "Customer data is already in PostgreSQL"
constraints = "Must work offline with cache"

[outcomes]
resilience = "Runbook ensures support can operate without original author"
reusability = "Logic works in other services unchanged"
ownership = "No vendor lock-in (can swap PostgreSQL)"
speed = "setup.sh brings new dev to working state in 5 min"

[gates]
gate_1_declaration = true
gate_2_integrity = false
gate_3_sovereignty = false
```

That's it. Use `nxs-manifest.toml` as your declaration and tracking file.
