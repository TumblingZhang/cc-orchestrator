# CC Orchestrator: Autonomous Multi-Agent System

A fully autonomous software development orchestration system for Claude Code. One user approval → complete project delivery. Now with **Multi-Version Mode** for parallel alternative development.

## Quick Start

```bash
# 1. Copy this folder to your Claude Code project or ~/.claude/skills/
cp -r cc-orchestrator ~/.claude/skills/

# 2. In Claude Code, start a new project:
claude

# 3. Invoke the orchestrator:
@cc-orchestrator/agents/MANAGER.md Build a REST API for managing todo items with user authentication

# 4. Or request multiple versions:
@cc-orchestrator/agents/MANAGER.md [multi_version=true, version_count=3] Build a task management app - give me 3 different approaches
```

## How It Works

### Single-Version Mode (Default)

The Manager agent orchestrates 6 specialized agents through Claude Code's native `Task` tool:

```
User Request → Manager → [Dreamer ↔ Critic] → [PM → TechLead] → [QA] → [Developers] → [QA] → Delivery
                 │              │                    │             │         │           │
                 │         Requirements           Specs      Test Plan   Code      Verify
                 │                                                   (parallel)
                 └─────────────────────── ONLY user interaction: initial approval
```

### Multi-Version Mode

When user requests multiple versions, the system generates N parallel development workflows:

```
User Request → Manager → Direction Dreamer → N Strategic Directions
                              ↓
               ┌──────────────┼──────────────┐
               ↓              ↓              ↓
           Version 1      Version 2      Version N
           [Full Workflow] [Full Workflow] [Full Workflow]
               ↓              ↓              ↓
               └──────────────┼──────────────┘
                              ↓
                    Comparison & Delivery
                    (N complete versions)
```

## Agent Roles

| Agent | Purpose | Output |
|-------|---------|--------|
| **Manager** | Orchestration, user communication | `state.json`, final delivery |
| **Direction Dreamer** | Generate N distinct strategic directions | `requirements/directions.md` |
| **Dreamer** | Creative ideation, maximize value | `requirements/ideas_round_N.md` |
| **Critic** | Alignment check, scope control | `requirements/critique_round_N.md` |
| **PM** | User stories, acceptance criteria | `specs/user_stories.md` |
| **TechLead** | Architecture, feasibility, code review | `architecture/*.md` |
| **Developer** | Implementation | `src/**/*` |
| **QA** | Test-first development, verification | `tests/**/*` |

## Configuration

Default settings (can be modified in Manager prompt):

```json
{
  "dreamer_critic_rounds": 3,
  "pm_techlead_rounds": 2,
  "dev_qa_rounds": 3,
  "max_developers": 5,
  "multi_version_mode": false,
  "version_count": 3
}
```

## Project Structure Created

### Single-Version Mode

```
your_project/
├── .orchestrator/
│   └── state.json           # Progress tracking
├── requirements/
│   ├── ideas_round_*.md     # Dreamer outputs
│   ├── critique_round_*.md  # Critic outputs
│   └── final_requirements.md
├── specs/
│   ├── user_stories.md
│   ├── acceptance_criteria.md
│   └── technical_constraints.md
├── architecture/
│   ├── system_design.md
│   ├── api_contracts.md
│   └── component_breakdown.md
├── src/                     # Implementation
├── tests/
│   ├── test_plan.md
│   ├── test_*.py
│   ├── .checksums           # Integrity verification
│   └── verification_report.md
└── docs/
```

### Multi-Version Mode

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
│   ├── v2_enterprise/                # Complete Version 2
│   │   └── ...
│   └── v3_innovative/                # Complete Version N
│       └── ...
└── comparison/
    ├── summary.md                    # High-level comparison
    └── detailed_comparison.md        # Feature-by-feature
```

## Files in This Skill

- `agents/MANAGER.md` - Entry point, orchestration logic
- `agents/DIRECTION_DREAMER.md` - Multi-version strategic direction generation
- `agents/DREAMER.md` - Creative ideation
- `agents/CRITIC.md` - Alignment verification
- `agents/PM.md` - Product specifications
- `agents/TECHLEAD.md` - Architecture & code review
- `agents/DEVELOPER.md` - Implementation
- `agents/QA.md` - Testing & verification
- `templates/state.json` - Initial state template (single-version)
- `templates/state_multi_version.json` - State template for multi-version mode
- `scripts/init_project.sh` - Project initialization helper

## Usage Examples

### Simple Project (Single Version)
```
@cc-orchestrator/agents/MANAGER.md Create a CLI tool for converting CSV to JSON
```

### Complex Project (Single Version)
```
@cc-orchestrator/agents/MANAGER.md Build a real-time chat application with:
- WebSocket support
- User authentication
- Message history
- File sharing
```

### With Custom Config
```
@cc-orchestrator/agents/MANAGER.md [dreamer_critic_rounds=2, max_developers=3]
Build a REST API for inventory management
```

### Multi-Version Mode (3 versions, default)
```
@cc-orchestrator/agents/MANAGER.md Build a task management app - give me multiple versions to compare
```

### Multi-Version Mode (explicit count)
```
@cc-orchestrator/agents/MANAGER.md [multi_version=true, version_count=4]
Create a personal finance tracker - I want 4 different approaches
```

### Multi-Version with Trigger Phrases
Any of these phrases will activate multi-version mode:
```
# Natural language triggers:
@cc-orchestrator/agents/MANAGER.md Build an e-commerce site - explore different approaches
@cc-orchestrator/agents/MANAGER.md Create a blog platform - give me 3 versions
@cc-orchestrator/agents/MANAGER.md Design a dashboard - compare multiple alternatives
```

## Multi-Version Mode Details

When activated, the system:

1. **Direction Dreamer** generates N distinct strategic directions (e.g., "Minimalist", "Enterprise", "Innovative")
2. **N parallel workflows** execute concurrently, each following one direction
3. Each workflow runs the complete pipeline: Dreamer → Critic → PM → TechLead → QA → Developers → QA
4. **Comparison report** summarizes all versions with recommendations
5. **User receives N complete implementations** to choose from or combine

### Example Directions Generated

For "Build a task management app", Direction Dreamer might generate:

| Direction | Philosophy | Approach |
|-----------|------------|----------|
| **The Minimalist** | "Less is more" | CLI-based, plain text, zero dependencies |
| **The Collaborator** | "Teams first" | Real-time web app, sharing, integrations |
| **The Power User** | "Keyboard is king" | Desktop app, vim-like bindings, scriptable |

## Important Notes

1. **Single Interaction**: After initial approval, NO user input needed until delivery
2. **Test-First**: QA writes tests BEFORE developers start coding
3. **Parallel Development**: Multiple developers work simultaneously per version
4. **Parallel Versions**: In multi-version mode, all N versions develop concurrently
5. **Integrity Checks**: Test files are checksummed to prevent tampering
6. **Autonomous Recovery**: Manager handles errors and retries automatically
7. **Version Independence**: Each version is a complete, standalone implementation
