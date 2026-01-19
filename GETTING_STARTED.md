# Getting Started with The Agency

A comprehensive guide to setting up your multi-agent development environment.

**Time to complete:** ~15 minutes

---

## Prerequisites

### Required: Claude Subscription

| Requirement | Options |
|-------------|---------|
| **Account** | Claude.ai Pro ($20/mo), Max ($100-200/mo), or Team |
| **API Access** | Or Claude Console with pre-paid credits |

### Required: System Requirements

| Requirement | Details |
|-------------|---------|
| **OS** | macOS, Linux, or Windows (WSL recommended) |
| **Node.js** | Version 18+ |
| **Git** | For version control |
| **Shell** | bash or zsh |

### Required: Terminal Application

| Platform | Recommendation |
|----------|----------------|
| **macOS** | iTerm2 (for named tabs, notifications) |
| **Linux** | Any terminal with tab support |
| **Windows** | Windows Terminal |

### Recommended: CLI Tools (macOS)

The Agency works best with these tools installed:

```bash
# Essential (strongly recommended)
brew install jq gh tree

# Enhanced experience (optional)
brew install yq fzf bat ripgrep
```

| Tool | Purpose |
|------|---------|
| `jq` | Parse JSON (API responses, package.json) |
| `gh` | GitHub operations (PRs, issues, releases) |
| `tree` | Visualize project structure |
| `yq` | Edit YAML configs programmatically |
| `fzf` | Fuzzy search |
| `bat` | Syntax-highlighted file viewing |
| `rg` | Lightning-fast code search |

Or run after installation: `./tools/setup-mac --all`

---

## Step 1: Install Claude Code

### macOS / Linux

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

### Windows (PowerShell)

```powershell
irm https://claude.ai/install.ps1 | iex
```

### Verify Installation

```bash
claude --version
```

### PATH Setup (if needed)

If `claude` command not found, add to your shell profile (`~/.bashrc` or `~/.zshrc`):

```bash
export PATH="$HOME/.claude/bin:$PATH"
```

Then reload:

```bash
source ~/.zshrc  # or ~/.bashrc
```

---

## Step 2: Fork and Clone

```bash
# Fork on GitHub first, then:
git clone https://github.com/YOUR_USERNAME/the-agency-starter.git my-project
cd my-project

# Make tools executable
chmod +x tools/*
```

---

## Step 3: Configure Your Identity

Edit `claude/config/agency.yaml` to map your system username to your principal name:

```yaml
principals:
  # Map your system username to your principal name
  # Run `whoami` in terminal to get your system username
  your_username: YourName
  default: unknown

project:
  name: "My Project"
  timezone: "America/New_York"  # Your timezone
```

Test it:
```bash
./tools/principal
# Should output: YourName
```

---

## Step 4: Meet Your Housekeeping Agent

The captain is your guide. Launch it:

```bash
./tools/myclaude housekeeping captain
```

When it starts, it will:
1. Introduce itself
2. Ask what you're building
3. Help you set up your project structure

**Try saying:** "I'm building a Next.js web app. Help me set up The Agency for it."

---

## Step 5: Create Your First Workstream

Workstreams organize related work. Have housekeeping create one, or do it yourself:

```bash
./tools/create-workstream web "Web Application"
```

This creates:
```
claude/workstreams/web/
  KNOWLEDGE.md    # Shared knowledge for this workstream
```

---

## Step 6: Create Your First Agent

Agents are specialized Claude instances. Create one for your web work:

```bash
./tools/create-agent web web
```

This creates:
```
claude/agents/web/
  agent.md           # Agent identity and purpose
  KNOWLEDGE.md       # What this agent has learned
  WORKLOG.md         # Sprint-based work tracking
  ADHOC-WORKLOG.md   # Out-of-plan work
```

Edit `claude/agents/web/agent.md` to describe your agent's role:

```markdown
# Web Agent

**Workstream:** web
**Purpose:** Build and maintain the web application frontend

## Expertise
- Next.js 15
- React
- TypeScript
- Tailwind CSS

## Responsibilities
- Implement UI components
- Handle client-side state
- Optimize performance
```

---

## Step 7: Launch Your Agent

```bash
./tools/myclaude web web
```

Your agent will:
1. Read its identity from `agent.md`
2. Check for any active instructions
3. Ask what you want to work on

---

## Essential Tools

### The `!` Shortcut

In Claude Code, prefix any command with `!` to run it in bash mode:

```
> !git status
> !./tools/now
> !ls -la
```

### Agency Tools

| Tool | What It Does |
|------|--------------|
| `./tools/now` | Current timestamp |
| `./tools/whoami` | Your principal identity |
| `./tools/agentname` | Current agent name |
| `./tools/workstream` | Current workstream |

### Session Management

| Tool | What It Does |
|------|--------------|
| `./tools/hello` | Start session, get context |
| `./tools/welcomeback` | Resume after break |
| `./tools/backup-session` | Save session state |
| `./tools/restore` | Restore agent context |

### Quality & Deployment

| Tool | What It Does |
|------|--------------|
| `./tools/pre-commit-check` | Run all quality checks |
| `./tools/run-unit-tests` | Run test suite |
| `./tools/code-review` | AI code review |
| `./tools/sync` | Push to remote |

### Collaboration

| Tool | What It Does |
|------|--------------|
| `./tools/collaborate` | Request help from another agent |
| `./tools/post-news` | Broadcast to all agents |
| `./tools/read-news` | Read broadcasts |
| `./tools/add-nit` | Log a small issue for later |

### Discovery

| Tool | What It Does |
|------|--------------|
| `./tools/list-tools` | List all available tools |
| `./tools/find-tool "keyword"` | Search for a tool |

---

## Claude Code Basics

### Keyboard Shortcuts

| Shortcut | What It Does |
|----------|--------------|
| `!` | Bash mode prefix |
| `@` | Mention files/folders |
| `#` | Add to CLAUDE.md |
| `Esc` | Interrupt Claude |
| `Esc + Esc` | Rewind to checkpoint |
| `/` | Access slash commands |
| `Tab` | Command completion |
| `↑` | Previous command |

### Essential Slash Commands

| Command | What It Does |
|---------|--------------|
| `/help` | Show all commands |
| `/clear` | Clear conversation (use often!) |
| `/model` | Change AI model |
| `/compact` | Summarize long conversation |
| `/rewind` | Undo changes |
| `/permissions` | Manage tool permissions |

### Models

| Model | When to Use |
|-------|-------------|
| Opus | Complex architecture, security |
| Sonnet | Implementation, refactoring (default) |
| Haiku | Quick searches, simple edits |

Switch with: `/model opus`, `/model sonnet`, `/model haiku`

---

## What You Get With The Agency

### Named Terminal Tabs

Each agent session runs in a clearly labeled tab:

```
┌──────────────────┬──────────────────┬──────────────────┐
│ housekeeping     │ web              │ api              │
│ (housekeeping)   │ (web)            │ (api)            │
└──────────────────┴──────────────────┴──────────────────┘
```

### Persistent Agent Identity

```bash
$ ./tools/whoami
YourName

$ ./tools/agentname
housekeeping

$ ./tools/workstream
housekeeping
```

### Session State

Your agent knows:
- What it was working on (ADHOC-WORKLOG.md)
- Active instructions from principals
- Collaboration requests from other agents
- Recent news and updates

### Structured Work Tracking

```
claude/
├── agents/
│   └── housekeeping/
│       ├── agent.md          # Agent definition
│       ├── WORKLOG.md         # Sprint work
│       ├── ADHOC-WORKLOG.md   # Ad-hoc tracking
│       └── KNOWLEDGE.md       # Learned context
├── principals/
│   └── YourName/
│       ├── instructions/      # Tasks from principal
│       └── artifacts/         # Deliverables
└── workstreams/
    └── web/
        └── KNOWLEDGE.md       # Shared knowledge
```

### Quality Gates

Pre-commit checks run automatically:
1. Formatting
2. Linting
3. Type checking
4. Unit tests
5. Code review

### Versus Going Solo

| Capability | Vanilla Claude Code | The Agency |
|------------|---------------------|------------|
| Terminal naming | Manual | Automatic |
| Agent identity | None | Built-in |
| Session persistence | Basic `/resume` | Full state restoration |
| Work tracking | None | WORKLOG, ADHOC, instructions |
| Quality gates | Manual | Automated 5-step |
| Collaboration | None | Full agent-to-agent |
| Principal instructions | None | Structured system |

---

## What's Next?

### Add More Agents

As your project grows, add specialized agents:
- `api` - Backend/API development
- `infra` - Infrastructure and DevOps
- `data` - Database and migrations
- `test` - Testing and QA

### Use Epics and Sprints

For larger initiatives:
```bash
./tools/create-epic 1          # Create epic001
./tools/create-sprint web 1 1  # Create web/epic001/sprint001
```

### Check the Docs

- `CLAUDE.md` - The constitution (agents read this)
- `claude/docs/CONCEPTS.md` - Deep dive on all concepts
- `claude/docs/guides/` - Specific workflows

---

## Quick Reference

### Common Commands

```bash
# Launch an agent
./tools/myclaude {workstream} {agent}

# Create things
./tools/create-workstream {name} "{description}"
./tools/create-agent {workstream} {name}
./tools/capture-instruction -t "Title" "Content"

# Collaboration
./tools/collaborate {target-agent} "Subject" "Request"
./tools/post-news "Update message"
./tools/read-news

# Quality
./tools/pre-commit-check
./tools/sync

# Discovery
./tools/find-tool -l          # List all tools
./tools/find-tool "keyword"   # Search tools
```

### Directory Structure

```
claude/
  agents/{name}/        # Agent definitions
  workstreams/{name}/   # Work organization
  principals/{name}/    # Human stakeholders
  docs/                 # Guides and reference
  config/agency.yaml    # Project configuration
tools/                  # CLI tools
source/                 # Apps, services, packages
```

### Naming Conventions

| Entity | Format | Example |
|--------|--------|---------|
| Agent | lowercase-hyphen | `web`, `agent-manager` |
| Workstream | lowercase | `web`, `agents` |
| Instruction | INSTR-XXXX | `INSTR-0001-alice-web-frontend-dark-mode.md` |
| Artifact | ART-XXXX | `ART-0001-alice-web-frontend-2026-01-01-report.md` |

---

## Troubleshooting

### "claude: command not found"

Add to PATH:
```bash
export PATH="$HOME/.claude/bin:$PATH"
source ~/.zshrc
```

### "Permission denied" on tools

```bash
chmod +x tools/*
```

### Agent not picking up context

```bash
./tools/restore
```

### Agent doesn't see my instruction

- Check the instruction's **To:** field matches `{workstream}/{agent}`
- Run `./tools/show-instructions` to verify

### Terminal tab not renaming

Ensure you're using iTerm2 (macOS) or a terminal that supports escape sequences for tab naming.

### Git push fails

- Use `./tools/sync` instead of `git push` directly
- Check for merge conflicts: `git status`

---

## Getting Help

### Ask the Captain

The captain knows The Agency inside and out:
```bash
./tools/myclaude housekeeping captain "How do I...?"
```

### Check Documentation

- `CLAUDE.md` - Quick reference
- `claude/docs/CONCEPTS.md` - All concepts explained
- `claude/docs/guides/` - Specific workflows

### Report Issues

https://github.com/the-agency-ai/the-agency-starter/issues

---

## Sources

- [Claude Code Product Page](https://claude.com/product/claude-code)
- [Claude Code Best Practices](https://www.anthropic.com/engineering/claude-code-best-practices)
- [Claude Code Documentation](https://code.claude.com/docs/en/overview)

---

*Welcome to The Agency. Build something amazing.*
