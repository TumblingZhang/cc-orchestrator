# CC Orchestrator - Complete Setup Guide

Autonomous Multi-Agent Software Development System for Claude Code

## Table of Contents
1. [Overview](#overview)
2. [Installation](#installation)
3. [Usage](#usage)
4. [Multi-Version Mode](#multi-version-mode)
5. [How It Works](#how-it-works)
6. [Configuration](#configuration)
7. [Troubleshooting](#troubleshooting)

---

## Overview

CC Orchestrator transforms Claude Code into a fully autonomous software development team. You provide a single request, approve the approach, and receive a complete, tested project. Now with **Multi-Version Mode** to explore multiple implementation approaches in parallel.

### Key Features
- 🤖 **8 Specialized Agents**: Manager, Direction Dreamer, Dreamer, Critic, PM, TechLead, Developers, QA
- 🔄 **Single User Interaction**: Approve once, receive complete delivery
- 📝 **Test-First Development**: QA writes tests before any code
- ⚡ **Parallel Development**: Multiple developers work simultaneously
- 🔀 **Multi-Version Mode**: Generate N completely different implementations in parallel
- 🔒 **Integrity Checks**: Checksummed tests prevent tampering
- 📊 **Full Traceability**: Every decision documented
- 👁️ **Visual Verification**: QA uses Playwright MCP to visually verify frontend (optional)
- 🔧 **Developer Debugging**: Chrome DevTools MCP for real-time frontend debugging (optional)

---

## Installation

### Quick Start (Easiest - Just Copy & Paste!)

**Paste this into Claude Code:**

```
Fetch https://github.com/TumblingZhang/cc-orchestrator and use @cc-orchestrator/agents/MANAGER.md to build 3 versions of a example personal portfolio website
```

Just describe what you want - even vague ideas work! The orchestrator will generate multiple production-ready implementations for you to choose from:
- `build 3 versions of task management system - explore different approaches`
- `build a habit tracker - give me 5 versions to compare`

---

### Option 1: Copy to Claude Code Skills Directory (Recommended for Offline Use)

```bash
# Clone or download the cc-orchestrator folder
# Then copy to your Claude Code skills location:

# For user-level skills:
cp -r cc-orchestrator ~/.claude/skills/

# Or for project-level:
cp -r cc-orchestrator ./your-project/.claude/skills/
```

### Option 2: Use Directly from Any Location

You can reference the agents from any location using absolute or relative paths:

```bash
# In Claude Code:
@/path/to/cc-orchestrator/agents/MANAGER.md Build a todo app
```

### Option 3: Add to CLAUDE.md (Project Instructions)

Add to your project's `CLAUDE.md` file:

```markdown
## Multi-Agent Orchestration

When I ask you to "orchestrate" a project or say "use the orchestrator", 
load and follow the instructions in:
- @cc-orchestrator/agents/MANAGER.md for orchestration
- Use Task() to spawn sub-agents as described in MANAGER.md
```

---

## Usage

### Basic Usage

1. **Start Claude Code** in your desired directory:
   ```bash
   cd ~/projects
   claude
   ```

2. **Invoke the orchestrator**:
   ```
   @cc-orchestrator/agents/MANAGER.md Build a REST API for managing tasks with user authentication
   ```

3. **Approve the proposed approach** when Manager asks:
   ```
   approve
   ```

4. **Wait for delivery** - no further input needed!

### With Custom Configuration

Override defaults by specifying in your request:

```
@cc-orchestrator/agents/MANAGER.md [dreamer_critic_rounds=2, max_developers=3] 
Create a CLI tool for file conversion
```

### Complex Projects

For complex projects, provide more detail:

```
@cc-orchestrator/agents/MANAGER.md Create a real-time dashboard with:
- WebSocket data streaming
- User authentication via OAuth
- PostgreSQL backend
- React frontend with charts
- Export to CSV/PDF
```

---

## Multi-Version Mode

When you want to explore multiple implementation approaches, use Multi-Version Mode. This generates N completely different versions of your project in parallel.

### Activating Multi-Version Mode

**Explicit configuration:**
```
@cc-orchestrator/agents/MANAGER.md [multi_version=true, version_count=3]
Build a task management application
```

**Natural language triggers:**
```
# Any of these phrases activate multi-version mode:
@cc-orchestrator/agents/MANAGER.md Build a blog - give me 3 versions
@cc-orchestrator/agents/MANAGER.md Create an e-commerce site - explore different approaches
@cc-orchestrator/agents/MANAGER.md Design a dashboard - multiple versions please
@cc-orchestrator/agents/MANAGER.md Build a CLI tool - compare alternatives
```

### How Multi-Version Mode Works

1. **Direction Dreamer** generates N strategically different directions
2. **N parallel workflows** execute (each with full Dreamer→Critic→PM→TechLead→QA→Dev→QA)
3. **Comparison report** summarizes all versions
4. **User receives N complete implementations** to choose from

```
User Request → Direction Dreamer → N Distinct Directions
                                          ↓
                    ┌─────────────────────┼─────────────────────┐
                    ↓                     ↓                     ↓
               Version 1             Version 2             Version N
            "The Minimalist"      "The Enterprise"      "The Innovator"
           ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
           │ Dreamer↔Critic  │  │ Dreamer↔Critic  │  │ Dreamer↔Critic  │
           │ PM→TechLead     │  │ PM→TechLead     │  │ PM→TechLead     │
           │ Architecture    │  │ Architecture    │  │ Architecture    │
           │ QA→Dev→QA       │  │ QA→Dev→QA       │  │ QA→Dev→QA       │
           └─────────────────┘  └─────────────────┘  └─────────────────┘
                    ↓                     ↓                     ↓
                    └─────────────────────┼─────────────────────┘
                                          ↓
                              Comparison & Delivery
                              (N complete versions)
```

### Example Direction Output

For "Build a task management app", Direction Dreamer might generate:

| Direction | Philosophy | Key Characteristics |
|-----------|------------|---------------------|
| **The Minimalist** | "Less is more" | CLI-based, plain text storage, zero dependencies |
| **The Collaborator** | "Teams first" | Web app, real-time sync, team features, integrations |
| **The Power User** | "Efficiency is everything" | Desktop app, vim keybindings, scriptable API |

### Multi-Version Project Structure

```
your_project/
├── .orchestrator/
│   └── state.json                    # Tracks all versions
├── requirements/
│   └── directions.md                 # Direction Dreamer output
├── versions/
│   ├── v1_minimalist/                # Complete Version 1
│   │   ├── requirements/
│   │   ├── specs/
│   │   ├── architecture/
│   │   ├── src/
│   │   └── tests/
│   ├── v2_collaborator/              # Complete Version 2
│   │   └── ...
│   └── v3_power_user/                # Complete Version 3
│       └── ...
└── comparison/
    ├── summary.md                    # Quick comparison
    └── detailed_comparison.md        # Feature-by-feature
```

### Choosing Your Version

After delivery, you can:
1. **Pick one version** that best fits your needs
2. **Combine elements** from multiple versions
3. **Use comparison report** to understand trade-offs

---

## How It Works

### Phase Flow

```
┌─────────────────────────────────────────────────────────────────┐
│ Phase 0: INITIALIZATION                                          │
│ • Manager analyzes request                                       │
│ • Proposes team configuration                                    │
│ • User approves (ONLY USER INTERACTION)                         │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│ Phase 1: REQUIREMENTS (Dreamer ↔ Critic, 3 rounds)              │
│ • Dreamer: Creative ideation, maximize value                    │
│ • Critic: Alignment check, scope control                        │
│ • Output: requirements/final_requirements.md                    │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│ Phase 2: SPECIFICATIONS (PM → TechLead, 2 rounds)               │
│ • PM: User stories, acceptance criteria                         │
│ • TechLead: Feasibility assessment                              │
│ • Output: specs/user_stories.md, specs/acceptance_criteria.md   │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│ Phase 3: ARCHITECTURE (TechLead)                                │
│ • System design                                                  │
│ • API contracts                                                  │
│ • Developer assignments                                          │
│ • Output: architecture/*.md                                      │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│ Phase 4: TEST PLANNING (QA) - BEFORE DEVELOPMENT!               │
│ • Write all tests before any code                               │
│ • Generate checksums for integrity                              │
│ • Output: tests/test_*.py, tests/.checksums                     │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│ Phase 5: DEVELOPMENT (Developers in PARALLEL)                   │
│ • Multiple developers work simultaneously                       │
│ • Each implements assigned components                           │
│ • TechLead reviews each submission                              │
│ • Output: src/**/*                                              │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│ Phase 6: VERIFICATION (QA)                                      │
│ • Verify test file integrity (checksums)                        │
│ • Run all tests                                                  │
│ • Verify acceptance criteria                                     │
│ • Output: tests/verification_report.md                          │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│ Phase 7: DELIVERY (Manager → User)                              │
│ • Compile final report                                           │
│ • Present to user                                                │
└─────────────────────────────────────────────────────────────────┘
```

### Task Tool Usage

The Manager uses Claude Code's native `Task()` tool to spawn agents:

```python
# Manager spawns Dreamer
dreamer_result = Task("""
    You are the DREAMER agent.
    
    PROJECT_ROOT: ./my_project_20250115
    USER_REQUEST: Build a todo app
    ROUND: 1 of 3
    
    Read DREAMER.md and generate ideas.
    Output to: requirements/ideas_round_1.md
""")

# Manager spawns Critic to review
critic_result = Task("""
    You are the CRITIC agent.
    
    DREAMER_OUTPUT: requirements/ideas_round_1.md
    ...
""")
```

---

## Configuration

### Default Settings

| Setting | Default | Description |
|---------|---------|-------------|
| `dreamer_critic_rounds` | 3 | Requirements refinement iterations |
| `pm_techlead_rounds` | 2 | Specification iterations |
| `dev_review_rounds` | 3 | Max development-review cycles |
| `max_developers` | 5 | Maximum parallel developers |
| `multi_version_mode` | false | Enable parallel version development |
| `version_count` | 3 | Number of versions to generate (2-5) |

### MCP Configuration (For Frontend Projects)

For projects with frontend/UI components, configure these MCPs to enable visual debugging and verification:

#### Playwright MCP (Primary for QA, Secondary for Developers)
Official Microsoft Playwright MCP for browser automation, visual verification, screenshots, and E2E testing.

```json
// In your Claude Code settings or .mcp.json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["-y", "@playwright/mcp@latest"]
    }
  }
}
```

**QA Agent uses this as PRIMARY tool for:**
- Automated E2E visual verification
- Taking screenshots of all pages/states (desktop + mobile)
- Testing user flows end-to-end
- Verifying responsive layouts

**Developer Agent uses this as SECONDARY tool for:**
- Quick smoke tests after fixing issues
- Capturing screenshots for documentation

#### Chrome DevTools MCP (Primary for Developers, Secondary for QA)
Official Chrome DevTools MCP for real-time browser debugging.

```json
{
  "mcpServers": {
    "chrome-devtools": {
      "command": "npx",
      "args": ["-y", "chrome-devtools-mcp@latest"]
    }
  }
}
```

**Developer Agent uses this as PRIMARY tool for:**
- Real-time debugging during development
- Checking console for errors/warnings
- Monitoring network requests and responses
- Inspecting DOM structure
- Running JavaScript to query state

**QA Agent uses this as SECONDARY tool for:**
- Debugging when Playwright tests fail
- Investigating console errors
- Analyzing failed network requests
- Understanding why something doesn't work

#### When to Enable MCPs

| Project Type | Playwright MCP | Chrome DevTools MCP |
|--------------|----------------|---------------------|
| Full-stack web app | ✅ Required | ✅ Recommended |
| React/Vue/Svelte SPA | ✅ Required | ✅ Recommended |
| Backend API only | ❌ Skip | ❌ Skip |
| CLI tool | ❌ Skip | ❌ Skip |
| Desktop app (Electron) | ✅ Optional | ✅ Recommended |
| Mobile web | ✅ Required | ✅ Recommended |

### Override Examples

```
# Faster iteration (less refinement)
@MANAGER.md [dreamer_critic_rounds=1, pm_techlead_rounds=1] Quick prototype

# More thorough (enterprise project)
@MANAGER.md [dreamer_critic_rounds=5, pm_techlead_rounds=3] Enterprise system

# Small team
@MANAGER.md [max_developers=2] Simple utility
```

---

## Troubleshooting

### Common Issues

#### "Task() not available"
Claude Code's Task tool may need to be enabled. Check your Claude Code settings.

#### "Agent not responding correctly"
Ensure the agent prompt files are accessible and the paths are correct.

#### "Infinite loop in Dreamer ↔ Critic"
This can happen if they can't reach consensus. The Manager should cap rounds and proceed with best available requirements.

#### "Tests failing after development"
Check `tests/verification_report.md` for details. The Manager will loop back to development for fixes.

#### "Checksum mismatch"
Test files were modified during development. This is caught intentionally to ensure test integrity.

### Debug Mode

Add to your request for verbose output:

```
@MANAGER.md [debug=true] Build my app
```

#### MCP-Related Issues

**"Playwright MCP not responding"**
- Ensure npx is available in your PATH
- Try: `npx @playwright/mcp@latest --help`
- Check that a browser can be launched (may need Playwright dependencies)
- Install browsers if needed: `npx playwright install chromium`

**"Chrome DevTools MCP connection failed"**
- Chrome/Chromium must be installed
- Check if remote debugging port is available (default: 9222)
- Try: `npx chrome-devtools-mcp@latest --help`
- For sandboxed environments, use `--browser-url` option

**"MCP tools not found"**
- Verify the MCP server names match your config: `playwright`, `chrome-devtools`
- Tools are called as `mcp__playwright__browser_navigate`, `mcp__chrome-devtools__navigate_page`
- Check that the MCPs are properly configured in your Claude Code settings

**"Screenshots not saving"**
- Check write permissions in project directory
- Ensure `screenshots/` directory exists or can be created
- Verify disk space available
- Screenshots from Playwright are base64 - they need to be decoded and saved

**"Visual verification skipped"**
- This is expected for backend-only projects
- For frontend projects, ensure dev server is running before QA verification
- Check that `localhost` URL is accessible
- Verify MCP tools are responding (try a simple navigate command)

---

## File Structure Reference

```
cc-orchestrator/
├── SKILL.md                        # Skill documentation
├── README.md                       # This file
├── agents/
│   ├── MANAGER.md                  # Orchestration controller
│   ├── DIRECTION_DREAMER.md        # Multi-version strategic directions
│   ├── DREAMER.md                  # Creative ideation
│   ├── CRITIC.md                   # Alignment verification
│   ├── PM.md                       # Product specifications
│   ├── TECHLEAD.md                 # Architecture & review
│   ├── DEVELOPER.md                # Implementation
│   └── QA.md                       # Testing & verification
├── templates/
│   ├── state.json                  # State template (single-version)
│   └── state_multi_version.json    # State template (multi-version)
└── scripts/
    └── init_project.sh             # Project initialization
```

---

## Support

For issues or improvements:
1. Check the troubleshooting section above
2. Review agent prompts for expected behavior
3. Examine `.orchestrator/state.json` for current state
4. Check `errors` array in state.json for logged issues

---

## License

MIT License - Use freely, modify as needed.
