# CC Orchestrator: Autonomous Multi-Agent System

A fully autonomous software development orchestration system for Claude Code. One user approval → complete project delivery.

## Quick Start

```bash
# 1. Copy this folder to your Claude Code project or ~/.claude/skills/
cp -r cc-orchestrator ~/.claude/skills/

# 2. In Claude Code, start a new project:
claude

# 3. Invoke the orchestrator:
@cc-orchestrator/agents/MANAGER.md Build a REST API for managing todo items with user authentication
```

## How It Works

The Manager agent orchestrates 6 specialized agents through Claude Code's native `Task` tool:

```
User Request → Manager → [Dreamer ↔ Critic] → [PM → TechLead] → [QA] → [Developers] → [QA] → Delivery
                 │              │                    │             │         │           │
                 │         Requirements           Specs      Test Plan   Code      Verify
                 │                                                   (parallel)
                 └─────────────────────── ONLY user interaction: initial approval
```

## Agent Roles

| Agent | Purpose | Output |
|-------|---------|--------|
| **Manager** | Orchestration, user communication | `state.json`, final delivery |
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
  "max_developers": 5
}
```

## Project Structure Created

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

## Files in This Skill

- `agents/MANAGER.md` - Entry point, orchestration logic
- `agents/DREAMER.md` - Creative ideation
- `agents/CRITIC.md` - Alignment verification
- `agents/PM.md` - Product specifications
- `agents/TECHLEAD.md` - Architecture & code review
- `agents/DEVELOPER.md` - Implementation
- `agents/QA.md` - Testing & verification
- `templates/state.json` - Initial state template
- `scripts/init_project.sh` - Project initialization helper

## Usage Examples

### Simple Project
```
@cc-orchestrator/agents/MANAGER.md Create a CLI tool for converting CSV to JSON
```

### Complex Project
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

## Important Notes

1. **Single Interaction**: After initial approval, NO user input needed until delivery
2. **Test-First**: QA writes tests BEFORE developers start coding
3. **Parallel Development**: Multiple developers work simultaneously
4. **Integrity Checks**: Test files are checksummed to prevent tampering
5. **Autonomous Recovery**: Manager handles errors and retries automatically
