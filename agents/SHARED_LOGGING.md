# Shared Agent Logging Standards

All agents MUST log their behavior. This file defines the common logging format.

## Log Location
`{PROJECT_ROOT}/agent_logs/{agent_name}_log.md`

## Log Format
```markdown
## [{timestamp}] {phase_or_mode}

**Actions:** {brief list}
**Decisions:** {key decisions + reasoning}
**Difficulties:** {issue}: {description} | Resolution: {how resolved}
**MCP Status:** {tool}: {working/failed/unavailable}
```

## Severity Levels
- **INFO**: Normal operations
- **WARN**: Workaround applied
- **ERROR**: Retry needed
- **CRITICAL**: User intervention needed

## What to Log
| Category | Examples |
|----------|----------|
| Actions | Agent spawned, output created, task completed |
| Decisions | Priority changes, scope adjustments |
| Difficulties | MCP failures, timeouts, parsing errors |
