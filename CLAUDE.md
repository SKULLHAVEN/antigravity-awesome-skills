# CLAUDE.md - Guide for AI Assistants & Developers

Welcome to the **antigravity-awesome-skills** repository! This guide is designed to help AI assistants, human developers, and repository maintainers understand the codebase, contribute effectively, and maintain quality standards.

---

## 📋 Table of Contents

1. [Quick Start](#quick-start)
2. [Repository Structure](#repository-structure)
3. [Skill Anatomy & Standards](#skill-anatomy--standards)
4. [Development Workflows](#development-workflows)
5. [Key Scripts & Commands](#key-scripts--commands)
6. [Quality Standards & Conventions](#quality-standards--conventions)
7. [Git & Contribution Workflow](#git--contribution-workflow)
8. [Data Files & Registries](#data-files--registries)
9. [CI/CD Pipeline & Automation](#cicd-pipeline--automation)
10. [Common Issues & Troubleshooting](#common-issues--troubleshooting)
11. [Guidelines for AI Assistants](#guidelines-for-ai-assistants)
12. [Additional Resources](#additional-resources)

---

## Quick Start

### What is This Repository?

**antigravity-awesome-skills** is a curated, validated collection of **930+ agentic skills** for AI coding assistants like Claude Code, Gemini CLI, Cursor, Antigravity, and others.

Each skill is a focused, reusable instruction set that tells AI assistants how to solve specific problems, follow best practices, or use tools effectively.

**Key Stats:**
- **930+ skills** organized in `/skills/` directory
- **6.2.0** current version (following semantic versioning)
- **MIT License** - Open source and community-driven
- **Automated validation** - All skills pass quality checks before merge

### Most Common Tasks

| Task | Command | Purpose |
|------|---------|---------|
| **Validate all skills** | `npm run validate` | Check if all SKILL.md files are valid |
| **Strict validation** | `npm run validate:strict` | CI-level validation (what gets merged) |
| **Generate index** | `npm run index` | Regenerate skills registry |
| **Update README** | `npm run readme` | Regenerate README with skill list |
| **Full pipeline** | `npm run chain` | Run validate → index → readme (recommended) |
| **Build catalog** | `npm run catalog` | Build full JSON catalog |
| **Run all tests** | `npm run test` | Execute all test suites |
| **Complete build** | `npm run build` | Run chain + catalog (final step) |

### Before You Start

1. ✅ **Node.js** - Required for package management and building
2. ✅ **Python 3** - Required for validation and index generation
3. ✅ Run `npm ci` - Install Node dependencies
4. ✅ Run `pip install -r requirements.txt` - Install Python dependencies (if you have requirements.txt)

---

## Repository Structure

### Directory Overview

```
antigravity-awesome-skills/
├── skills/                 # 930+ skill definitions (THE CORE)
├── docs/                   # User and maintainer documentation
├── scripts/                # Build, validation, and utility scripts
├── data/                   # Generated JSON registries (DO NOT EDIT)
├── bin/                    # CLI entry points
├── lib/                    # Shared utilities
├── .github/                # CI/CD workflows and templates
├── web-app/                # Web interface (out of scope for this guide)
└── README.md, CHANGELOG.md # Project-level documentation
```

### Core Directories Explained

#### `/skills/` - The Heart of the Repository

Contains 930+ skill folders, each with a required `SKILL.md` file.

```
skills/
├── brainstorming/
│   └── SKILL.md                    [REQUIRED]
├── git-pushing/
│   ├── SKILL.md                    [REQUIRED]
│   ├── examples/                   [OPTIONAL]
│   │   ├── example1.sh
│   │   └── example2.sh
│   ├── scripts/                    [OPTIONAL]
│   ├── templates/                  [OPTIONAL]
│   └── references/                 [OPTIONAL]
└── [928+ more skills with similar structure...]
```

**Important Rules:**
- Each skill has its own folder named in `kebab-case` (lowercase-with-hyphens)
- Only `SKILL.md` is required; everything else is optional
- Folder name MUST exactly match the `name:` field in SKILL.md frontmatter
- All 930 skills must pass validation before being merged

#### `/docs/` - Comprehensive Documentation

Human-readable guides for understanding and contributing to the project.

**Key files:**
- `SKILL_ANATOMY.md` - How to structure and write SKILL.md files
- `QUALITY_BAR.md` - Quality standards and validation requirements
- `GETTING_STARTED.md` - User onboarding guide
- `CONTRIBUTING.md` - Step-by-step contribution guide (root level)
- `QUALITY.md` - Detailed quality standards
- `BUNDLES.md` - How skills are grouped into curated collections
- `WORKFLOWS.md` - Workflow definitions and chaining
- And 10+ more files in English, plus Vietnamese translations

#### `/scripts/` - Automation & Validation

Python and Node.js scripts that maintain the repository.

**Core scripts:**
- `validate_skills.py` - **CRITICAL** - Validates all SKILL.md files
- `generate_index.py` - Generates `skills_index.json` registry
- `update_readme.py` - Updates README.md with current skill list
- `build-catalog.js` - Builds `catalog.json` (full catalog)
- `sync_microsoft_skills.py` - Syncs Microsoft-contributed skills
- `skills_manager.py` - Utility for skill management

**Test scripts (in `/scripts/tests/`):**
- `validate_skills_headings.test.js` - Node test for skill validation
- `test_validate_skills_headings.py` - Python test for skill headings
- `test_comprehensive_coverage.py` - Coverage testing
- `inspect_microsoft_repo.py` - Microsoft repo inspection

#### `/data/` - Generated Registries

**⚠️ DO NOT EDIT THESE FILES DIRECTLY** - They are regenerated automatically by scripts.

```
data/
├── skills_index.json      # Main registry of 930 skills
├── catalog.json           # Full detailed catalog (569KB)
├── bundles.json           # Curated skill collections
├── aliases.json           # Skill name aliases
└── workflows.json         # Workflow definitions
```

These files are regenerated by:
- `npm run index` → regenerates `skills_index.json`
- `npm run catalog` → regenerates `catalog.json`
- CI/CD pipeline → regenerates all on main branch

#### `/bin/` - CLI Entry Points

- `install.js` - Main entry point for the NPM package
- `skill-utils.js` - Command-line utilities for skill operations

#### `/lib/` - Shared Utilities

- `skill-utils.js` - Shared utility functions used by scripts and CLI

#### `/.github/` - CI/CD Configuration

- `workflows/ci.yml` - Main CI pipeline (validation, building, testing)
- `workflows/publish-npm.yml` - NPM publishing pipeline
- `ISSUE_TEMPLATE/` - GitHub issue templates
- `PULL_REQUEST_TEMPLATE.md` - PR template for contributors

---

## Skill Anatomy & Standards

### SKILL.md File Structure

Every skill consists of two parts: **Frontmatter** (metadata) and **Content** (instructions).

#### Part 1: Frontmatter (YAML)

Located at the top of SKILL.md, wrapped in `---`:

```markdown
---
name: my-skill-name
description: "Brief, clear description of what this skill does"
---
```

**Required Fields:**

| Field | Format | Rules | Example |
|-------|--------|-------|---------|
| `name` | kebab-case string | Must match folder name exactly | `git-pushing`, `react-debugging` |
| `description` | String (quoted) | Max 200 characters, clear value prop | `"Push changes to git with conventional commit messages"` |

**Optional Fields:**

| Field | Values | Purpose | Example |
|-------|--------|---------|---------|
| `risk` | `none`, `safe`, `critical`, `offensive`, `unknown` | Safety classification | `risk: "safe"` |
| `source` | URL or `"self"` | Original source reference | `source: "https://example.com/original"` |
| `tags` | Array of strings | Categorization | `tags: ["git", "devops"]` |

**Risk Level Guide:**
- 🟢 **none** - Pure reasoning/text (e.g., brainstorming, writing)
- 🔵 **safe** - Reads files, runs read-only commands (e.g., linting)
- 🟠 **critical** - Modifies state, deletes files, pushes to production
- 🔴 **offensive** - Pentesting/red team tools (requires "Authorized Use Only" warning)

#### Part 2: Content Structure

After frontmatter, use clear Markdown sections to organize instructions.

**Recommended Structure:**

```markdown
# Skill Title

## Overview
2-3 sentences explaining what this skill does and why it matters.

## When to Use This Skill
- Use when [scenario 1]
- Use when [scenario 2]
- Use when the user asks about [topic]

## How It Works
### Step 1: [First Action]
Detailed instructions...

### Step 2: [Second Action]
More instructions...

## Examples
### Example 1: [Use Case]
\`\`\`language
code example
\`\`\`

### Example 2: [Another Use Case]
\`\`\`language
code example
\`\`\`

## Best Practices
- ✅ Do this
- ✅ Also do this
- ❌ Don't do this

## Limitations
- Does not work on [platform]
- Cannot handle [scenario]

## Related Skills
- `@other-skill` - When to use instead
- `@complementary-skill` - How to chain together
```

**Key Rules:**
- **"When to Use" section is mandatory** - Validation requires it
- **Clear action verbs** - Use "Create the file", not "The file should be created"
- **Copy-paste ready examples** - At least one example users can immediately use
- **Explicit limitations** - Document what the skill cannot do
- **Related skills** - Use `@skill-name` format for cross-references

### Optional Skill Components

#### Examples Directory
```
examples/
├── basic-usage.js
├── advanced-pattern.ts
└── full-implementation/
    ├── index.js
    └── config.json
```
Referenced in SKILL.md for users to study.

#### Scripts Directory
```
scripts/
├── setup.sh
├── validate.py
└── generate.js
```
Helper scripts that automate parts of the skill.

#### Templates Directory
```
templates/
├── component.tsx
├── test.spec.ts
└── config.json
```
Reusable code templates referenced in SKILL.md.

#### References Directory
```
references/
├── api-docs.md
├── best-practices.md
└── troubleshooting.md
```
External documentation or detailed references.

---

## Development Workflows

### Adding a New Skill

**Step 1: Create the folder**
```bash
mkdir skills/my-new-skill
cd skills/my-new-skill
```

**Step 2: Create SKILL.md with template**
```bash
cat > SKILL.md << 'EOF'
---
name: my-new-skill
description: "Clear description of what this skill does"
---

# My New Skill

## Overview
Explain what this skill does and why it matters.

## When to Use This Skill
- Use when [scenario]

## How It Works
Step-by-step instructions...

## Examples
\`\`\`
code example
\`\`\`

## Best Practices
- ✅ Do this
- ❌ Don't do this
EOF
```

**Step 3: Validate locally**
```bash
npm run validate        # Warnings only
npm run validate:strict # CI-level checks
```

**Step 4: Optional - Add supporting files**
- Create `examples/` for example code
- Create `scripts/` for automation
- Create `templates/` for code templates
- Create `references/` for documentation

**Step 5: Commit and push**
```bash
git add skills/my-new-skill/
git commit -m "feat: add my-new-skill"
git push origin branch-name
```

### Modifying an Existing Skill

1. Navigate to the skill: `cd skills/skill-name/`
2. Edit `SKILL.md` to improve instructions, examples, or metadata
3. Run validation: `npm run validate:strict`
4. Commit changes: `git commit -m "docs: improve skill-name"`
5. Push to your branch

### Running Validation

**Soft mode** (warnings only - for local development):
```bash
npm run validate
```

**Strict mode** (enforces all checks - what CI runs):
```bash
npm run validate:strict
```

**What validation checks:**
1. ✅ SKILL.md exists in each skill folder
2. ✅ Frontmatter is valid YAML
3. ✅ `name` and `description` fields present
4. ✅ Name matches folder name (kebab-case)
5. ✅ Description under 200 characters
6. ✅ "When to use" section exists
7. ✅ Has at least one code example
8. ✅ Risk level is valid (if specified)

### Generating Indexes

The repository maintains generated JSON files that track all skills.

**Generate index registry:**
```bash
npm run index
```
Updates `skills_index.json` (main registry of 930 skills)

**Update README with skill list:**
```bash
npm run readme
```
Updates README.md with current skill count and list

**Build full catalog:**
```bash
npm run catalog
```
Builds `catalog.json` (detailed information on all skills)

### Full Build Pipeline

**Run the complete validation chain** (recommended before committing):
```bash
npm run chain
```

This runs:
1. `npm run validate` - Validate all skills
2. `npm run index` - Generate skills index
3. `npm run readme` - Update README

Then optionally:
```bash
npm run catalog
```
Builds the full catalog

**Or in one command:**
```bash
npm run build
```
Runs `chain` + `catalog` (everything)

---

## Key Scripts & Commands

### NPM Scripts Reference

| Script | Command | Purpose | When to Use |
|--------|---------|---------|------------|
| `validate` | `python3 scripts/validate_skills.py` | Soft validation | Local development |
| `validate:strict` | `python3 scripts/validate_skills.py --strict` | CI-level validation | Before pushing |
| `index` | `python3 scripts/generate_index.py` | Generate skills index | Part of build pipeline |
| `readme` | `python3 scripts/update_readme.py` | Update README | Part of build pipeline |
| `chain` | `validate && index && readme` | Full validation chain | After modifying skills |
| `catalog` | `node scripts/build-catalog.js` | Build full catalog | After validation chain |
| `build` | `chain && catalog` | Complete build | Final step before push |
| `test` | Multiple test runners | Run all tests | Before major changes |
| `sync:microsoft` | `python3 scripts/sync_microsoft_skills.py` | Sync Microsoft skills | Maintenance only |
| `sync:all-official` | `sync:microsoft && chain` | Sync + update | Maintenance only |

### Running Tests

```bash
npm run test
```

Runs all test suites:
- Node.js validation tests (`validate_skills_headings.test.js`)
- Python validation tests (`test_validate_skills_headings.py`)
- Microsoft repo inspection (`inspect_microsoft_repo.py`)
- Comprehensive coverage tests (`test_comprehensive_coverage.py`)

### Syncing Official Skills

For maintainers only:
```bash
npm run sync:microsoft
npm run sync:all-official
```

---

## Quality Standards & Conventions

### The Quality Bar (V4 Standard)

Every skill submission must pass **5 quality checks**:

#### 1. **Metadata Integrity**
- Frontmatter is valid YAML
- `name` field is kebab-case and matches folder name
- `description` is present and under 200 characters
- `risk` field is one of: `none`, `safe`, `critical`, `offensive`, `unknown`

#### 2. **Clear Triggers (When to Use)**
- Must have section explicitly stating when to use the skill
- Accepted section headings:
  - `## When to Use This Skill`
  - `## When to Use`
  - `## Use this skill when`
- Must answer: "What problem does this solve?" and "When should it be triggered?"

#### 3. **Safety & Risk Classification**
- Each skill declares a risk level
- **critical** or **offensive** skills must have "Authorized Use Only" warnings
- No harmful commands without proper labeling

#### 4. **Copy-Pasteable Examples**
- At least one code block or interaction example
- Example must be realistic and immediately usable
- Users should be able to copy/paste and get results

#### 5. **Explicit Limitations**
- Document known edge cases or scenarios where the skill doesn't work
- Examples: "Does not work on Windows without WSL", "Cannot handle files over 1GB"

### Naming Conventions

**Skills (folder names & SKILL.md name field):**
- Format: `kebab-case` (lowercase-with-hyphens)
- ✅ Good: `react-debugging`, `git-pushing`, `stripe-integration`
- ❌ Bad: `ReactDebugging`, `gitPushing`, `Stripe_Integration`

**Commit messages:**
- Use prefix: `feat:`, `fix:`, `docs:`, `refactor:`, `test:`, `chore:`
- Example: `feat: add kubernetes-deployment skill`
- Example: `docs: improve quality bar documentation`

**Branch names:**
- Follow pattern: `claude/add-{feature}-{sessionID}`
- Example: `claude/add-claude-documentation-qKpU7`

### File Naming Conventions

- SKILL.md files use ALL CAPS: `SKILL.md` (not `skill.md`)
- Examples use language suffixes: `example.js`, `example.py`, `example.ts`
- Utilities use kebab-case: `my-helper.js`, `my-utility.py`
- Configuration files: `config.json`, `config.yml`

### Documentation Standards

- Use clear, direct language (no hedging: "might consider" → "do this")
- Use action verbs ("Create", "Run", "Check") not passive voice
- Keep instructions specific, not vague
- Write for both AI assistants and human developers
- Include practical examples wherever possible

---

## Git & Contribution Workflow

### Branch Strategy

**Development branches:**
- Name format: `claude/add-{feature}-{sessionID}`
- Example: `claude/add-claude-documentation-qKpU7`
- Push to: `origin {branch-name}`

**Merge branches:**
- Main branch: `main` (production-ready)
- Feature branches start with `claude/` or `feat/`

### Commit Workflow

**Before committing:**
1. Run validation: `npm run validate:strict`
2. Run tests: `npm run test`
3. Run full build: `npm run build`
4. Check for uncommitted changes: `git status`

**Committing changes:**
```bash
git add skills/my-skill/
git commit -m "feat: add my-skill"
git push -u origin claude/add-my-skill-sessionID
```

**Commit message format:**
```
{type}: {description}

Optional longer explanation...

{url to session/issue if applicable}
```

**Commit types:**
- `feat:` - New skill or major feature
- `fix:` - Bug fixes in existing skills
- `docs:` - Documentation improvements
- `refactor:` - Code reorganization without changing function
- `test:` - Adding or updating tests
- `chore:` - Maintenance, dependency updates

### Pull Request Process

1. Create feature branch: `git checkout -b claude/add-feature-sessionID`
2. Make changes and commit: `git commit -m "feat: description"`
3. Push to origin: `git push -u origin branch-name`
4. Create PR via GitHub UI
5. CI/CD pipeline validates automatically
6. Address any validation failures
7. Merge when green ✅

### CI/CD Auto-Actions

When you push to `main` branch, CI/CD automatically:
1. ✅ Validates all skills
2. ✅ Regenerates index and README
3. ✅ Builds catalog
4. ✅ Runs all tests
5. ✅ Auto-commits generated files (if changes detected)
6. ✅ Detects and reports any drift

---

## Data Files & Registries

### skills_index.json

**Location:** `/data/skills_index.json` or root level

**Purpose:** Master registry of all 930 skills

**Structure:**
```json
{
  "skills": [
    {
      "name": "brainstorming",
      "folder": "brainstorming",
      "description": "Help turn ideas into fully formed designs",
      "risk": "none",
      "tags": ["ideation", "planning"]
    },
    ...
  ],
  "total": 930
}
```

**Generated by:** `npm run index`

**⚠️ DO NOT EDIT** - Always regenerate with `npm run index`

### catalog.json

**Location:** `/data/catalog.json`

**Purpose:** Full, detailed catalog with complete skill information

**Size:** ~569KB (large file)

**Content:** Complete metadata for all 930 skills including descriptions, examples, risk levels

**Generated by:** `npm run catalog`

**⚠️ DO NOT EDIT** - Always regenerate with `npm run catalog`

### bundles.json

**Location:** `/data/bundles.json`

**Purpose:** Curated collections of related skills

**Example:**
```json
{
  "bundles": [
    {
      "name": "react-development",
      "description": "Essential React skills",
      "skills": ["react-best-practices", "react-debugging", "component-design"]
    }
  ]
}
```

**Generated by:** Part of `npm run build` pipeline

### aliases.json

**Location:** `/data/aliases.json`

**Purpose:** Alternate names/shortcuts for skills

**Example:**
```json
{
  "aliases": {
    "git-push": "git-pushing",
    "debug": "systematic-debugging"
  }
}
```

### workflows.json

**Location:** `/data/workflows.json`

**Purpose:** Predefined skill chains for common workflows

**⚠️ Key Rule:** Always regenerate data files, never edit manually. They're overwritten by CI/CD.

---

## CI/CD Pipeline & Automation

### Pipeline Stages

The GitHub Actions workflow in `.github/workflows/ci.yml` runs:

**Stage 1: Validation**
- Set up Python 3.10 environment
- Run `python3 scripts/validate_skills.py` (soft mode)
- Checks all SKILL.md files against quality standards

**Stage 2: Index Generation**
- Run `python3 scripts/generate_index.py`
- Generates `skills_index.json` with all 930 skills

**Stage 3: README Update**
- Run `python3 scripts/update_readme.py`
- Updates README.md with current skill count and list

**Stage 4: Testing**
- Set up Node.js (LTS)
- Run `npm ci` (clean install)
- Run `npm audit --audit-level=high` (dependency security check)
- Run `npm run test` (all test suites)

**Stage 5: Catalog Building**
- Run `npm run catalog`
- Builds complete `catalog.json` file

**Stage 6: Auto-Commit (main branch only)**
- If changes detected in generated files
- Auto-commits with message: "chore: sync generated registry files [ci skip]"
- Auto-pushes to origin/main

**Stage 7: Drift Detection**
- Checks if any uncommitted changes remain
- Fails if drift detected (prevents out-of-sync builds)

### When CI Runs

- ✅ On push to `main` or `feat/*` branches
- ✅ On pull requests to `main`
- ✅ On manual workflow dispatch (Actions tab)

### Common CI Failures & Fixes

**Validation fails:**
```bash
npm run validate:strict
# Fix validation errors in SKILL.md
git add .
git commit -m "fix: address validation errors"
git push
```

**Index generation fails:**
- Check for invalid YAML in SKILL.md frontmatter
- Ensure all `name` fields match folder names
- Run `npm run index` locally to debug

**Drift detected:**
```bash
npm run chain && npm run catalog
git add README.md skills_index.json data/
git commit -m "chore: sync generated registry files"
git push
```

**NPM audit fails:**
- Update vulnerable packages: `npm audit fix`
- Or manually: `npm update {package-name}`
- Commit updates to `package-lock.json`

---

## Common Issues & Troubleshooting

### Skill Validation Issues

**Problem:** "name does not match folder name"
```
Error: Skill 'my-new-skill' in 'my_new_skill' folder
```

**Solution:**
- Ensure folder name is exactly `my-new-skill` (kebab-case)
- Ensure `name:` field in SKILL.md frontmatter matches exactly
- Both must use lowercase-with-hyphens format

**Problem:** "description exceeds 200 characters"
```
Error: description is 215 chars, max 200
```

**Solution:**
- Count characters in the `description:` field (excluding quotes)
- Shorten description to be more concise
- Keep only the essential "what" and "when to use"

**Problem:** "missing When to Use section"
```
Error: Skill must have 'When to Use' section
```

**Solution:**
- Add a section to SKILL.md with one of these headings:
  - `## When to Use This Skill`
  - `## When to Use`
  - `## Use this skill when`
- Include 2-3 scenarios where this skill applies

**Problem:** "invalid frontmatter YAML"
```
Error: Invalid YAML in frontmatter
```

**Solution:**
- Check that `description:` value is quoted
- Check for proper indentation (2 spaces, not tabs)
- Verify all required fields are present
- Validate YAML syntax at [yamllint.com](https://www.yamllint.com/)

**Problem:** "no examples found"
```
Error: Skill must have copy-pasteable examples
```

**Solution:**
- Add an `## Examples` section
- Include at least one code block with language specified
- Make examples realistic and immediately usable

### Script Execution Issues

**Problem:** Python script not found
```
Error: command not found: python3
```

**Solution:**
- Install Python 3: `apt-get install python3` (Ubuntu/Debian)
- Or use system package manager for your OS
- Verify: `python3 --version`

**Problem:** pip dependencies missing
```
Error: No module named 'yaml'
```

**Solution:**
- Install dependencies: `pip install -r requirements.txt`
- Or manually: `pip install pyyaml`

**Problem:** Node modules not installed
```
Error: Cannot find module 'yaml'
```

**Solution:**
```bash
npm ci  # Clean install (preferred)
# or
npm install
```

### Build Pipeline Issues

**Problem:** `npm run chain` fails partway through
```
Error during index generation
```

**Solution:**
1. Run each step individually to isolate the issue:
   ```bash
   npm run validate:strict  # Check validation first
   npm run index           # Then index generation
   npm run readme          # Then README update
   ```
2. Fix the issue identified
3. Re-run the full chain

**Problem:** Generated files not updating
```
Changes not reflected in README or index
```

**Solution:**
- Ensure you're running the full chain: `npm run build`
- Not just `npm run validate`
- Generated files only update via: `npm run index`, `npm run readme`, `npm run catalog`

---

## Guidelines for AI Assistants

### When to Run Validation

**Always run before committing:**
```bash
npm run validate:strict  # CI-level checks
```

**Run locally before pushing:**
```bash
npm run build  # Full build including tests
```

**Run after modifying SKILL.md files:**
```bash
npm run validate:strict
npm run chain      # Update index/readme
npm run catalog    # Rebuild catalog
```

### Handling Generated Files

**❌ NEVER manually edit:**
- `/data/skills_index.json`
- `/data/catalog.json`
- `/data/bundles.json`
- `/data/aliases.json`
- `/data/workflows.json`
- `README.md` (except for documentation sections)
- `CATALOG.md`

**✅ ALWAYS regenerate via scripts:**
```bash
npm run index    # Regenerate skills_index.json
npm run catalog  # Regenerate catalog.json
npm run readme   # Update README
npm run build    # Regenerate everything
```

### Best Practices for Batch Operations

**Adding multiple skills:**
1. Create all skill folders with SKILL.md files
2. Run full validation once: `npm run validate:strict`
3. Fix any issues across all skills
4. Run full build: `npm run build`
5. Commit all changes together

**Modifying multiple skills:**
1. Edit all SKILL.md files
2. Run validation to check all changes: `npm run validate:strict`
3. Run build to update indexes: `npm run build`
4. Commit all changes together

**Syncing external skills:**
1. Run: `npm run sync:microsoft` (or appropriate sync command)
2. Run: `npm run chain` to validate and update indexes
3. Commit all changes

### Error Handling & Recovery

**If a script fails:**
1. Read the error message carefully
2. Check that prerequisites are installed (Node.js, Python 3)
3. Run the failing step again
4. If still failing, run the step before it to check inputs
5. Fix the root cause, not the symptom

**If you make a mistake:**
1. Don't delete files directly
2. Use `git status` to see what changed
3. Use `git restore {file}` to undo local changes
4. Use `git reset HEAD {file}` to unstage changes
5. Use `git revert` for committed mistakes

**If indexes become out-of-sync:**
1. Don't manually edit `/data/` files
2. Run: `npm run build` to regenerate everything
3. Verify outputs: `git diff`
4. Commit the regenerated files

### Development Flow for AI Assistants

**Standard workflow:**
```bash
# 1. Start fresh
git pull origin main
git checkout -b claude/add-feature-sessionID

# 2. Make changes
# (edit SKILL.md files, add new skills, etc.)

# 3. Validate locally
npm run validate:strict

# 4. Run full build
npm run build

# 5. Check status
git status

# 6. Commit changes
git add skills/
git commit -m "feat: add new skills"

# 7. Push to feature branch
git push -u origin claude/add-feature-sessionID
```

---

## Additional Resources

### Key Documentation Files

| File | Location | Purpose |
|------|----------|---------|
| **SKILL_ANATOMY.md** | `/docs/SKILL_ANATOMY.md` | How to write effective SKILL.md files |
| **QUALITY_BAR.md** | `/docs/QUALITY_BAR.md` | Quality standards and validation rules |
| **CONTRIBUTING.md** | `/CONTRIBUTING.md` | Contribution guidelines and setup |
| **GETTING_STARTED.md** | `/docs/GETTING_STARTED.md` | User onboarding guide |
| **BUNDLES.md** | `/docs/BUNDLES.md` | Curated skill collections |
| **WORKFLOWS.md** | `/docs/WORKFLOWS.md` | Workflow chaining |
| **SECURITY_GUARDRAILS.md** | `/docs/SECURITY_GUARDRAILS.md` | Safety policies |
| **CHANGELOG.md** | `/CHANGELOG.md` | Version history |

### Related Skills (if using as agentic skill)

- `@brainstorming` - For designing new skills
- `@systematic-debugging` - For troubleshooting issues
- `@git-workflow` - For advanced git operations
- `@test-driven-development` - For skill validation

### External Resources

- **GitHub Repository:** https://github.com/sickn33/antigravity-awesome-skills
- **Issue Tracker:** https://github.com/sickn33/antigravity-awesome-skills/issues
- **Discussions:** https://github.com/sickn33/antigravity-awesome-skills/discussions

### CLI Installation

Install locally as an NPM package:
```bash
npm install -g antigravity-awesome-skills
```

Or use directly from repository:
```bash
npx antigravity-awesome-skills
```

---

## Summary

This repository is a living collection of AI-optimized skills built by the community. As an AI assistant or developer working here, remember:

✅ **DO:**
- Validate before committing (`npm run validate:strict`)
- Run full build before pushing (`npm run build`)
- Write clear SKILL.md files with examples
- Follow the quality bar standards
- Reference existing documentation
- Regenerate data files via scripts
- Commit with clear messages

❌ **DON'T:**
- Edit `/data/` files manually
- Commit without validation
- Merge without passing CI/CD
- Use unclear skill descriptions
- Skip the "When to Use" section
- Assume skill names without checking
- Modify generated files directly

**For questions or issues:**
- Check `/docs/` for comprehensive guides
- Review `/CONTRIBUTING.md` for contribution process
- Open an issue on GitHub
- Check existing issues for similar problems

Welcome to the community! 🚀

---

**Last Updated:** March 2026
**Repository Version:** 6.2.0
**Total Skills:** 930+
