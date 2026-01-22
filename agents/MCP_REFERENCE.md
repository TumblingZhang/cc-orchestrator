# MCP Reference & Reliability Patterns

This document provides consistent MCP (Model Context Protocol) notation, usage patterns, and reliability strategies across all agents.

## Available MCP Servers

| MCP Server | Purpose | Available To |
|------------|---------|--------------|
| **Context7** | Up-to-date library/framework documentation | Dreamer, TechLead, Developer |
| **Exa** | Web search, code search, technical research | Dreamer, TechLead |
| **MarkItDown** | Read PDFs, Office docs, images as markdown | Dreamer |
| **Playwright** | Browser automation for E2E testing | QA (primary), Developer (secondary) |
| **Chrome DevTools** | Console/network/DOM debugging | Developer (primary), QA (secondary) |

---

## Standardized MCP Function Notation

### Context7 MCP (Library Documentation)

```python
# Step 1: Resolve library to get Context7-compatible ID
mcp__context7__resolve(libraryName="react")
# Returns: {"libraries": [{"id": "/facebook/react", ...}]}

# Step 2: Get documentation for specific topic
mcp__context7__get_library_docs(
    context7CompatibleLibraryID="/facebook/react",
    topic="hooks"
)
```

**Common Libraries:**
| Library | Resolve Name | Example ID |
|---------|--------------|------------|
| React | `react` | `/facebook/react` |
| Express | `express` | `/expressjs/express` |
| FastAPI | `fastapi` | `/tiangolo/fastapi` |
| pytest | `pytest` | `/pytest-dev/pytest` |

### Exa MCP (Web Search & Research)

```python
# Basic web search
mcp__exa__web_search_exa(query="best practices React 2024")

# Deep research with AI summaries
mcp__exa__deep_search_exa(query="microservices architecture patterns")

# Find code examples
mcp__exa__get_code_context_exa(query="OAuth2 implementation Node.js")
```

**Search Query Patterns:**
| Goal | Query Pattern |
|------|---------------|
| Find competitors | `"best [domain] apps 2024 comparison"` |
| User complaints | `"[product] user complaints reddit"` |
| Best practices | `"[topic] best practices 2024"` |
| Innovations | `"innovative [domain] startups"` |

### MarkItDown MCP (Document Conversion)

```python
# Convert documents to markdown
mcp__markitdown__convert_to_markdown(uri="file:///path/to/document.pdf")
mcp__markitdown__convert_to_markdown(uri="file:///path/to/spreadsheet.xlsx")
mcp__markitdown__convert_to_markdown(uri="file:///path/to/presentation.pptx")
```

**Supported Formats:** PDF, DOCX, XLSX, PPTX, Images (OCR)

### Playwright MCP (Browser Automation)

```python
# Navigation
mcp__playwright__browser_navigate(url="http://localhost:3000")
mcp__playwright__browser_navigate_back()

# Page inspection
mcp__playwright__browser_snapshot()  # Gets accessibility tree + element refs
mcp__playwright__browser_take_screenshot()  # Returns base64 PNG

# Interactions (use refs from browser_snapshot)
mcp__playwright__browser_click(element="Login button", ref="e1")
mcp__playwright__browser_type(element="Email input", text="test@example.com", ref="e2")
mcp__playwright__browser_select_option(element="Dropdown", values=["option1"], ref="e3")
mcp__playwright__browser_press_key(key="Enter")

# Responsive testing
mcp__playwright__browser_resize(width=375, height=667)   # Mobile
mcp__playwright__browser_resize(width=1920, height=1080) # Desktop

# Utilities
mcp__playwright__browser_wait_for(time=2000)  # Wait in ms
mcp__playwright__browser_network_requests()
mcp__playwright__browser_tabs()
```

### Chrome DevTools MCP (Debugging)

```python
# Navigation
mcp__chrome-devtools__navigate_page(url="http://localhost:3000")

# Console inspection
mcp__chrome-devtools__list_console_messages()

# Network inspection
mcp__chrome-devtools__list_network_requests()
mcp__chrome-devtools__get_network_request(request_id="...")

# DOM inspection
mcp__chrome-devtools__take_snapshot()
mcp__chrome-devtools__take_screenshot()

# Element interaction
mcp__chrome-devtools__click(selector="#my-button")
mcp__chrome-devtools__fill(selector="#email-input", value="test@example.com")

# JavaScript execution
mcp__chrome-devtools__evaluate_script(script="document.querySelector('.error')?.textContent")
mcp__chrome-devtools__evaluate_script(script="window.localStorage")
```

---

## Reliability Patterns

### Pattern 1: Graceful Degradation

When an MCP is unavailable, fall back to alternative approaches:

```
MCP Call Attempt
    ↓
[Success] → Use result
    ↓
[Failure] → Try fallback
    ↓
[Fallback Success] → Use result + log warning
    ↓
[Fallback Failure] → Log error + proceed with limitations
```

### Pattern 2: Retry with Backoff

For transient failures (rate limits, timeouts):

```
Attempt 1 → Wait 0s
    ↓ [Fail]
Attempt 2 → Wait 30s
    ↓ [Fail]
Attempt 3 → Wait 60s
    ↓ [Fail]
Log error and proceed with fallback
```

### Pattern 3: MCP Health Check

Before heavy MCP usage, perform a quick health check:

```python
# Quick test to verify MCP is responding
try:
    # Context7: Simple resolve
    mcp__context7__resolve(libraryName="react")
    # Exa: Simple search
    mcp__exa__web_search_exa(query="test")
    # Playwright: Navigate to blank
    mcp__playwright__browser_navigate(url="about:blank")
except:
    # Log MCP unavailable, switch to fallback mode
```

---

## Fallback Strategies by MCP

### Context7 Unavailable

| Fallback | When to Use |
|----------|-------------|
| Use official documentation URLs | Always |
| Search for code examples with Exa | If Exa available |
| Use cached/known API patterns | For common libraries |
| Note uncertainty in output | Always |

**Example:**
```
WARN: Context7 unavailable | Resolution: Used official React docs at react.dev
```

### Exa Unavailable

| Fallback | When to Use |
|----------|-------------|
| Use known industry patterns | For common domains |
| Reference established best practices | Always |
| Note limited research in output | Always |
| Proceed with conservative proposals | If Dreamer |

**Example:**
```
WARN: Exa unavailable | Resolution: Proceeded with known industry standards, noted limited research
```

### MarkItDown Unavailable

| Fallback | When to Use |
|----------|-------------|
| Ask user for document summary | Complex documents |
| Request plain text version | Simple documents |
| Extract text manually if possible | Images/PDFs |

**Example:**
```
WARN: MarkItDown unavailable | Resolution: Requested user to provide document summary
```

### Playwright Unavailable

| Fallback | When to Use |
|----------|-------------|
| Use Chrome DevTools MCP | For visual inspection |
| Document manual testing needed | Always |
| Rely on unit/integration tests | Code verification |

**Example:**
```
WARN: Playwright unavailable | Resolution: Visual verification deferred, documented for manual testing
```

### Chrome DevTools Unavailable

| Fallback | When to Use |
|----------|-------------|
| Use Playwright MCP | For basic inspection |
| Add console.log debugging | Development |
| Use network tab in manual testing | Debugging |

**Example:**
```
WARN: Chrome DevTools unavailable | Resolution: Used Playwright for basic inspection
```

---

## Rate Limit Handling

### Exa Rate Limits

Exa may rate limit after many searches. Strategy:

1. **Batch queries intelligently** - Combine related searches
2. **Cache results** - Don't re-search same query
3. **Wait and retry** - 60 second pause usually sufficient
4. **Prioritize queries** - Most important searches first

### Context7 Rate Limits

Less common, but if encountered:

1. **Cache library IDs** - Don't re-resolve same libraries
2. **Batch doc requests** - Get multiple topics at once
3. **Use official docs as backup** - Direct URL access

---

## Logging MCP Issues

All agents must log MCP status in their log files:

```markdown
## [{timestamp}] Session

**MCP Tool Status:**
- Context7: {working/failed/unavailable/rate-limited}
- Exa: {working/failed/unavailable/rate-limited}
- MarkItDown: {working/failed/not-needed}
- Playwright: {working/failed/unavailable}
- Chrome DevTools: {working/failed/not-needed}

**MCP Issues Encountered:**
- {MCP name}: {issue description} | Resolution: {how handled}
```

### Severity Levels

| Level | Meaning | Example |
|-------|---------|---------|
| INFO | Expected, normal | "Exa search returned 5 results" |
| WARN | Degraded, but proceeding | "Context7 slow, used cached docs" |
| ERROR | MCP failed, fallback used | "Playwright unavailable, documented manual testing" |
| BLOCKED | Cannot proceed without MCP | "OAuth requires user credentials" |

---

## Agent-Specific MCP Usage

### Dreamer
- **Primary**: Exa (research), Context7 (verify features)
- **Minimum**: 5-10 Exa searches before proposing features
- **Fallback**: If Exa unavailable, note limited research

### TechLead
- **Primary**: Context7 (API verification), Exa (architecture patterns)
- **Usage**: Verify library capabilities before recommending
- **Fallback**: Note uncertainty in technical constraints

### Developer
- **Primary**: Context7 (coding reference), Chrome DevTools (debugging)
- **Secondary**: Playwright (smoke tests)
- **Fallback**: Manual testing + official docs

### QA
- **Primary**: Playwright (E2E testing), Chrome DevTools (debugging)
- **Usage**: Full visual verification for frontend projects
- **Fallback**: Document manual verification requirements
