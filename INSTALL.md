# Installation & Setup

**Install the NXS skill once. Then every project uses it automatically.**

---

## Quick Start (2 minutes)

### Step 1: Install the Skill

Copy the skill files to your agent's skill directory:

**Hermes Desktop:**
```bash
mkdir -p ~/.hermes/skills/nexovia-standard
cp SKILL.md ~/.hermes/skills/nexovia-standard/
cp GOVERNANCE.md ~/.hermes/skills/nexovia-standard/
cp nxs_schema.toml ~/.hermes/skills/nexovia-standard/
```

**Claude Code:**
```bash
mkdir -p ~/.claude_code/skills/nexovia-standard
cp SKILL.md ~/.claude_code/skills/nexovia-standard/
cp GOVERNANCE.md ~/.claude_code/skills/nexovia-standard/
cp nxs_schema.toml ~/.claude_code/skills/nexovia-standard/
```

**Pi (Ollama):**
```bash
mkdir -p ~/.pi/skills/nexovia-standard
cp SKILL.md ~/.pi/skills/nexovia-standard/
cp GOVERNANCE.md ~/.pi/skills/nexovia-standard/
cp nxs_schema.toml ~/.pi/skills/nexovia-standard/
```

**OpenCode:**
```bash
mkdir -p ~/.opencode/skills/nexovia-standard
cp SKILL.md ~/.opencode/skills/nexovia-standard/
cp GOVERNANCE.md ~/.opencode/skills/nexovia-standard/
cp nxs_schema.toml ~/.opencode/skills/nexovia-standard/
```

### Step 2: Use the Skill

Now when you start a new project, the agent automatically uses NXS:

```bash
# Hermes Desktop
You: "Build a customer search API"
Hermes: [Loads SKILL.md, shows Gate 1 form]

# Claude Code
claude-code build "customer search API"
[Claude loads SKILL.md, shows Gate 1 form]

# Pi/Ollama
pi build "customer search API"
[Pi loads SKILL.md, shows Gate 1 form]
```

**That's it.** Gates 1, 2, 3 enforce automatically for every project.

---

## Installation Paths

### Hermes Desktop

**Install:**
```bash
mkdir -p ~/.hermes/skills/nexovia-standard
cp SKILL.md GOVERNANCE.md nxs_schema.toml ~/.hermes/skills/nexovia-standard/
```

**Verify:**
```bash
ls -la ~/.hermes/skills/nexovia-standard/
# Should show: SKILL.md, GOVERNANCE.md, nxs_schema.toml
```

**Use:**
```bash
# In Hermes chat or terminal
You: "Build [project]"
Hermes: "Gate 1 required. Showing declaration form..."
# Agent loads skill automatically, gates enforce automatically
```

**Uninstall:**
```bash
rm -rf ~/.hermes/skills/nexovia-standard
```

---

### Claude Code

**Install:**
```bash
mkdir -p ~/.claude_code/skills/nexovia-standard
cp SKILL.md GOVERNANCE.md nxs_schema.toml ~/.claude_code/skills/nexovia-standard/
```

**Verify:**
```bash
ls -la ~/.claude_code/skills/nexovia-standard/
# Should show: SKILL.md, GOVERNANCE.md, nxs_schema.toml
```

**Use:**
```bash
claude-code build "my project"
# Claude Code loads skill, enforces gates automatically
```

**Uninstall:**
```bash
rm -rf ~/.claude_code/skills/nexovia-standard
```

---

### Pi (Ollama / Local LLM)

**Install:**
```bash
mkdir -p ~/.pi/skills/nexovia-standard
cp SKILL.md GOVERNANCE.md nxs_schema.toml ~/.pi/skills/nexovia-standard/
```

**Verify:**
```bash
# Make sure Ollama is running
ollama serve  # Run in another terminal

# Then
pi list-skills
# Should show: nexovia-standard
```

**Use:**
```bash
pi build "my project"
# Pi loads skill, enforces gates automatically
# If Ollama down: Manual Declaration gate (human fills form)
```

**Uninstall:**
```bash
rm -rf ~/.pi/skills/nexovia-standard
```

---

### OpenCode (Code Review)

**Install:**
```bash
mkdir -p ~/.opencode/skills/nexovia-standard
cp SKILL.md GOVERNANCE.md nxs_schema.toml ~/.opencode/skills/nexovia-standard/
```

**Verify:**
```bash
opencode skill list
# Should show: nexovia-standard
```

**Use:**
```bash
# Before reviewing PR
opencode review --skill nexovia-standard
# OpenCode loads skill, checks 8 policies against code
# Blocks merge if violations (with SOP to fix)
```

**Uninstall:**
```bash
rm -rf ~/.opencode/skills/nexovia-standard
```

---

### Custom Agent Framework (OpenClaw, Codex, etc.)

**Install:**
```bash
mkdir -p ~/.your_tool/skills/nexovia-standard
cp SKILL.md GOVERNANCE.md nxs_schema.toml ~/.your_tool/skills/nexovia-standard/
```

**Configure Your Tool:**
Edit your tool's config to load NXS skill:
```yaml
# your_tool.yaml or config.json
skills:
  - name: nexovia-standard
    path: ~/.your_tool/skills/nexovia-standard
    autoload: true
```

**Use:**
Your tool loads NXS automatically. Gates 1-3 enforce on every project.

**Uninstall:**
```bash
rm -rf ~/.your_tool/skills/nexovia-standard
```

---

## File Structure After Install

```
~/.hermes/skills/
├── nexovia-standard/
│   ├── SKILL.md (399 lines — agent instructions)
│   ├── GOVERNANCE.md (958 lines — gates, policies, enforcement)
│   └── nxs_schema.toml (326 lines — specification)
└── [other skills...]
```

That's it. 3 files, ~2,000 lines, no dependencies.

---

## Troubleshooting

### Problem: "Skill not found"

**Cause:** Skill not copied to correct directory

**Fix:**
```bash
# Check if directory exists
ls -la ~/.hermes/skills/nexovia-standard/

# If not, create and copy
mkdir -p ~/.hermes/skills/nexovia-standard
cp SKILL.md GOVERNANCE.md nxs_schema.toml ~/.hermes/skills/nexovia-standard/
```

### Problem: "Gates aren't enforcing"

**Cause:** Agent didn't load skill properly

**Fix:**
```bash
# Verify files exist
ls ~/.hermes/skills/nexovia-standard/SKILL.md
ls ~/.hermes/skills/nexovia-standard/GOVERNANCE.md

# Restart agent and try again
# Start new project (gates apply to new projects only)
```

### Problem: "Policy violations aren't blocking"

**Cause:** GOVERNANCE.md not in skill directory

**Fix:**
```bash
# Make sure GOVERNANCE.md is there
cp GOVERNANCE.md ~/.hermes/skills/nexovia-standard/

# Restart and try again
```

---

## Verification

After installation, verify it's working:

**Hermes Desktop:**
```bash
# In Hermes
You: "Build test project"
Hermes: [Should show Gate 1 declaration form with 9 fields]
# If you see the form, skill is loaded and working
```

**Claude Code:**
```bash
claude-code build test
# Should prompt for Gate 1 declaration
# If you get prompted, skill is working
```

**Pi/Ollama:**
```bash
pi build test
# Should prompt for Gate 1 or run automated gates
# If gates run, skill is working
```

---

## What Gets Installed

**3 files only:**

1. **SKILL.md** (399 lines)
   - Agent instructions
   - Four outcomes, four rules, three gates
   - Workflow for applying NXS
   - Validation checklist

2. **GOVERNANCE.md** (958 lines)
   - How to enforce Gate 1 (Declaration)
   - How to enforce Gate 2 (Integrity)
   - How to enforce Gate 3 (Sovereignty)
   - 8 explicit policies
   - How to version + extend policies
   - How to add new agent frameworks

3. **nxs_schema.toml** (326 lines)
   - Specification for any project
   - 8 node types
   - 14 runtimes
   - How to extend schema

**Total:** ~2,000 lines
**Dependencies:** None
**Works offline:** Yes

---

## Next Steps

1. ✅ Copy 3 files to your agent's skill directory
2. ✅ Start a new project
3. ✅ Agent shows Gate 1 (Declaration form)
4. ✅ Fill 9 fields + approve
5. ✅ Gates 2-3 run automatically
6. ✅ Only ship when all gates PASS

---

_Install once. Use everywhere. One standard. Any agent._
