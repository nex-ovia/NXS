# Installing NXS Skill

**The Nexovia Standard is a skill, not a library. Installation is simple: load it once, use everywhere.**

---

## Quick Install (30 seconds)

### Hermes Desktop (Recommended)

```bash
skill_view(name='nexovia-standard')
```

That's it. The skill loads automatically. Every new project enforces Gates 1-3.

### Claude Code

**Option 1: Initialize New Project with NXS**
```bash
claude-code --init --skill nexovia-standard
```

**Option 2: Add NXS to Existing Project**
```bash
skill_view(name='nexovia-standard')
```

### Pi (Ollama / Local LLM)

```bash
# Load the skill
skill_view(name='nexovia-standard')

# Run your first project through NXS
pi build [project-name] --standard nxs
```

### OpenCode (Code Review)

```bash
# Use NXS for PR review
opencode review --standard nxs
```

---

## How NXS Installs

NXS doesn't need to be "installed" in the traditional sense. It's a **skill** (a set of instructions for agents).

### Where Skill Lives

**Hermes Desktop:**
```
~/.hermes/skills/nexovia-standard/SKILL.md
```

**Claude Code:**
```
Built-in skill registry
```

**Pi/Ollama:**
```
User-local cache + GitHub source (https://github.com/nex-ovia/NXS)
```

### How It Works

1. **You ask agent:** "Build [project]"
2. **Agent loads skill:** Reads SKILL.md (agent instructions)
3. **Agent enforces:** Gates 1, 2, 3 automatically
4. **You approve:** Gate 1 declaration (9 fields)
5. **Agent builds & validates:** Gate 2 integrity checks
6. **Agent verifies:** Gate 3 sovereignty checks
7. **Result:** Project ready to ship or problems listed with SOP

---

## Installation Paths

### Path 1: Hermes Desktop (Full-Featured)

**What you get:**
- ✅ Interactive Gate 1 form (HTML preview)
- ✅ Automatic integrity checks (grep, tests, scans)
- ✅ Sovereignty validation (real-world checks)
- ✅ Policy enforcement (8 policies, all binary)
- ✅ Compliance tracking (TOML format)
- ✅ Human approval loop

**Install:**
```bash
# In Hermes chat or terminal
skill_view(name='nexovia-standard')

# Then
# You: "Build my search API"
# Hermes: Shows interactive form (Gate 1)
```

**Status:** ✅ Recommended for development

---

### Path 2: Claude Code (Local + Cloud)

**What you get:**
- ✅ Same gates (Declaration → Integrity → Sovereignty)
- ✅ Same policies (8 explicit, all checkable)
- ✅ Same compliance tracking (TOML)
- ✅ Works on Mac, Linux, Windows
- ✅ Cloud-ready

**Install:**
```bash
# Option A: New project with NXS built-in
claude-code --init --skill nexovia-standard

# Option B: Existing project
skill_view(name='nexovia-standard')

# Then
# claude-code build [project]
# Gates run automatically
```

**Status:** ✅ Recommended for production

---

### Path 3: Pi / Ollama (Offline, Local-First)

**What you get:**
- ✅ Runs offline (no internet needed for inference)
- ✅ Same gates + policies
- ✅ Graceful fallback (if Ollama down, manual Declaration gate)
- ✅ Works on Mac, Linux, Windows, Raspberry Pi

**Install:**
```bash
# Make sure Ollama is running
ollama serve  # Run in another terminal

# Load NXS skill
skill_view(name='nexovia-standard')

# Run project
pi build [project-name] --standard nxs
```

**Fallback (if Ollama unavailable):**
```
Gate 1: Human manually fills declaration (9 fields)
Gate 2: Human reviews integrity (9 checks)
Gate 3: Human verifies sovereignty (8 checks)
Result: Same quality, slower (manual instead of automated)
```

**Status:** ✅ Recommended for offline work

---

### Path 4: OpenCode (Code Review)

**What you get:**
- ✅ Automatic PR review against 8 policies
- ✅ Blocks merge if violations (with SOP to fix)
- ✅ Definition of Done checklist verification
- ✅ Security baseline checks

**Install:**
```bash
# Before reviewing PR
opencode review --standard nxs

# Or specify subset of policies
opencode review --standard nxs --policies "config-external,testing"
```

**Status:** ✅ Recommended for CI/CD

---

### Path 5: Custom Agent Framework (OpenClaw, YourTool, etc.)

**What you get:**
- ✅ Framework for any new agent
- ✅ Gates, policies, compliance tracking
- ✅ Self-contained (no external dependencies)

**Install:**

**Step 1: Copy NXS Files**
```bash
# Clone or download NXS
git clone https://github.com/nex-ovia/NXS.git

# Copy to your tool's skill directory
cp NXS/SKILL.md ~/.your_tool/skills/nexovia-standard/
cp NXS/GOVERNANCE.md ~/.your_tool/skills/nexovia-standard/
cp NXS/nxs_schema.toml ~/.your_tool/skills/nexovia-standard/
```

**Step 2: Load in Your Tool**
```bash
# In your tool's config
skill_view(name='nexovia-standard')
```

**Step 3: Implement Gates**
```
Gate 1: Collect declaration (9 fields)
        Show interactive form or text prompt
        Get user approval

Gate 2: Run integrity checks
        grep for hardcoded secrets
        verify DEPENDENCIES.md
        run setup.sh
        run tests (≥70% coverage)
        check Definition of Done (7 boxes)

Gate 3: Verify sovereignty
        Check tool independence (< 4h swap)
        Check handoff tested (real person)
        Check metrics wired
        Check operational clarity
```

**Step 4: Enforce Policies**
```
Policy 1: Outcome traceability (every component maps to outcome)
Policy 2: Dependency documentation (all deps listed)
Policy 3: Configuration management (zero hardcoded secrets)
Policy 4: Setup automation (one command)
Policy 5: Error handling (explicit, not silent)
Policy 6: Handoff documentation (RUNBOOK.md tested)
Policy 7: Security baseline (no secrets in repo)
Policy 8: Testing requirements (≥70% coverage)
```

**Step 5: Track Compliance (TOML)**
```toml
[compliance]
gate_1_declaration = "PASS"
gate_2_integrity = "PASS"
gate_3_sovereignty = "PASS"
compliance_status = "PASS"
```

**Status:** ✅ Recommended for extending to new tools

---

## Verify Installation

### Hermes Desktop

```bash
# In chat or terminal
skill_view(name='nexovia-standard')

# You should see: SKILL.md content (356 lines, agent instructions)
```

### Claude Code

```bash
claude-code --version
# Should show: version 2.x+

skill_view(name='nexovia-standard')
# Should show: SKILL.md loaded
```

### Pi/Ollama

```bash
# Make sure Ollama is running
ollama list

# Load skill
skill_view(name='nexovia-standard')

# Test on small project
pi build test-project --standard nxs --verbose
```

### Custom Tool

```bash
# Check skill loaded
ls ~/.your_tool/skills/nexovia-standard/SKILL.md
ls ~/.your_tool/skills/nexovia-standard/GOVERNANCE.md
ls ~/.your_tool/skills/nexovia-standard/nxs_schema.toml

# Should all exist
```

---

## Uninstall (Rarely Needed)

### Hermes Desktop
NXS is a skill. To stop using it, just don't load it:
```bash
# Don't run: skill_view(name='nexovia-standard')
# Projects will proceed without NXS gates
```

### Claude Code
```bash
# Remove from project
rm -rf ~/.claude_code/skills/nexovia-standard/
```

### Pi/Ollama
```bash
# Stop loading it
# Don't run: skill_view(name='nexovia-standard')
```

### Custom Tool
```bash
# Remove SKILL files
rm -rf ~/.your_tool/skills/nexovia-standard/
```

---

## Troubleshooting

### Problem: Skill won't load

**Hermes Desktop:**
```
Error: "Skill not found"
Fix: Make sure you're in the right Hermes profile
     Run: hermes profile list
     Then: skill_view(name='nexovia-standard')
```

**Claude Code:**
```
Error: "nexovia-standard not registered"
Fix: Update Claude Code to latest version
    claude-code --update
```

**Pi/Ollama:**
```
Error: "Ollama not running"
Fix: Start Ollama in another terminal
    ollama serve
```

### Problem: Gates aren't enforcing

**Check:**
```bash
# Verify skill is loaded
skill_view(name='nexovia-standard')

# Should show 356 lines of agent instructions
```

**Fix:**
```bash
# Reload skill
skill_view(name='nexovia-standard')

# Start new project (gates apply to new projects only)
# Existing projects use version when created
```

### Problem: Policy violations aren't blocking

**Check:**
```bash
# Verify GOVERNANCE.md Part 6 policies are running
# Agent should say: "Policy 3 violation: [specific problem]"
```

**Fix:**
```bash
# Make sure agent loaded SKILL.md (not just GOVERNANCE.md)
skill_view(name='nexovia-standard')  # Includes all 3 files

# Restart project
```

---

## What Gets Installed

NXS installs **3 files** (total ~2,000 lines):

1. **SKILL.md** (399 lines)
   - Agent instructions
   - Four outcomes, four rules, three gates
   - How to apply NXS workflow
   - Validation checklist
   - Decision framework

2. **GOVERNANCE.md** (958 lines)
   - Gate 1-3 detailed enforcement
   - 8 explicit policies (with automated checks)
   - Policy versioning mechanism
   - How to extend for new frameworks
   - Version management (semantic versioning)

3. **nxs_schema.toml** (326 lines)
   - Specification for any project
   - 8 node types (code, agent, config, data, decision, business_process, documentation, manual_step)
   - 14 runtimes (Python, Rust, Node, LLM, Ollama, Docker, Lambda, Cloud Run, etc.)
   - Extension guide (how to add new runtime/type/layer)

**Total:** ~2,000 lines of pure governance logic. No bloat. No dependencies.

---

## Next Steps After Install

1. **Load skill:** `skill_view(name='nexovia-standard')`
2. **Start project:** Tell your agent to build something
3. **Fill Declaration:** Agent shows interactive form (Gate 1)
4. **Approve:** Gates 2-3 run automatically
5. **Ship:** Only when all gates PASS

---

## Getting Help

**Questions about install?**
- Check this file (INSTALL.md)
- Read README.md for usage with each tool
- Read SKILL.md for agent workflow

**Questions about gates/policies?**
- Read GOVERNANCE.md (Parts 2-11)
- Check SKILL.md validation checklist

**Found a bug?**
- GitHub Issues: https://github.com/nex-ovia/NXS/issues

---

_Install NXS once. Use everywhere. One standard. Any tool. Any agent._
