# CLAUDE.md

# Claude Code Sub Agent Configuration
## 🚨 CRITICAL: CONCURRENT EXECUTION FOR ALL ACTIONS

**ABSOLUTE RULE**: ALL operations MUST be concurrent/parallel in a single message:

### 🔴 MANDATORY CONCURRENT PATTERNS:
1. **TodoWrite**: ALWAYS batch ALL todos in ONE call (5-10+ todos minimum)
2. **Task tool**: ALWAYS spawn ALL agents in ONE message with full instructions
3. **File operations**: ALWAYS batch ALL reads/writes/edits in ONE message
4. **Bash commands**: ALWAYS batch ALL terminal operations in ONE message
5. **Memory operations**: ALWAYS batch ALL memory store/retrieve in ONE message

### ⚡ GOLDEN RULE: "1 MESSAGE = ALL RELATED OPERATIONS"

**Examples of CORRECT concurrent execution:**
```javascript
// ✅ CORRECT: Everything in ONE message
[Single Message]:
  - TodoWrite { todos: [10+ todos with all statuses/priorities] }
  - Task("Agent 1 with full instructions and hooks")
  - Task("Agent 2 with full instructions and hooks")
  - Task("Agent 3 with full instructions and hooks")
  - Read("file1.js")
  - Read("file2.js")
  - Write("output1.js", content)
  - Write("output2.js", content)
  - Bash("npm install")
  - Bash("npm test")
  - Bash("npm run build")
```

**Examples of WRONG sequential execution:**
```javascript
// ❌ WRONG: Multiple messages (NEVER DO THIS)
Message 1: TodoWrite { todos: [single todo] }
Message 2: Task("Agent 1")
Message 3: Task("Agent 2")
Message 4: Read("file1.js")
Message 5: Write("output1.js")
Message 6: Bash("npm install")
// This is 6x slower and breaks coordination!
```

### 🎯 CONCURRENT EXECUTION CHECKLIST:

Before sending ANY message, ask yourself:
- ✅ Are ALL related TodoWrite operations batched together?
- ✅ Are ALL Task spawning operations in ONE message?
- ✅ Are ALL file operations (Read/Write/Edit) batched together?
- ✅ Are ALL bash commands grouped in ONE message?
- ✅ Are ALL memory operations concurrent?

## 🤖 Claude Sub-Agents Integration

This project includes 15 specialized AI sub-agents for enhanced development.

### Available Agents

The following agents are installed in `.claude/agents/`:

- **project-planner**: Strategic planning and task decomposition specialist
- **api-developer**: Backend API development specialist with PRP awareness
- **frontend-developer**: Modern web interface implementation specialist
- **tdd-specialist**: Test-driven development and comprehensive testing expert
- **code-reviewer**: Code quality, security, and best practices analyst
- **debugger**: Error analysis and debugging specialist
- **refactor**: Code refactoring and improvement specialist
- **doc-writer**: Technical documentation specialist
- **security-scanner**: Security vulnerability detection specialist
- **devops-engineer**: CI/CD and deployment automation specialist
- **product-manager**: Product requirements and user story specialist
- **marketing-writer**: Technical marketing content specialist
- **api-documenter**: OpenAPI/Swagger documentation specialist
- **test-runner**: Automated test execution specialist
- **shadcn-ui-builder**: UI/UX implementation with ShadCN components

### Using Sub-Agents

Agents work alongside your existing PRPs and can be invoked in several ways:

1. **Direct execution**: `claude-agents run <agent> --task "description"`
2. **Task tool in Claude Code**: `Task("agent-name: task description")`
3. **Agent slash commands**: Located in `.claude/commands/agents/`

### Memory System

Agents share context and coordinate through:
- **Memory Store**: `.swarm/memory.json` for persistent agent memory
- **Context Sharing**: Agents can access shared project context
- **PRP Integration**: Agents are aware of and can work with your PRPs

### Best Practices

- Use agents for specialized tasks that match their expertise
- Agents can read and understand your PRPs for context
- Multiple agents can work on different aspects of the same feature
- Memory system allows agents to build on each other's work
If ANY answer is "No", you MUST combine operations into a single message!

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Moveless is a property investment company that acts as both landlord and management company for its residential properties. The company invests in and owns its entire property portfolio, managing all aspects of property operations.

**Business Model**: Moveless is a specialist landlord providing quality residential properties exclusively for supported living. We lease properties to Registered Providers and Care Providers who deliver supported living services. We treat our provider customers and their residents with care, ensuring our properties are high-quality, compliant, and purpose-designed to enable excellent supported living delivery.

**Target Audience**:
- Registered Providers delivering supported living services
- Care Providers specializing in supported living accommodation
- Organizations supporting adults with learning disabilities, mental health needs, or physical disabilities in community settings
- Local Authority Commissioners and NHS Commissioners evaluating accommodation options for funded placements

**Value Proposition**: As a specialist supported living landlord, we provide properties that enable care providers to deliver outstanding services. We understand what makes properties work for supported living: CQC compliance requirements, accessibility standards (DDA/Equality Act), strategic locations near services and amenities, and responsive maintenance that doesn't disrupt care delivery. Our properties help providers achieve quality outcomes and CQC Outstanding ratings.

**Commissioner Appeal**: Our properties give commissioners confidence that accommodation standards support positive outcomes. We provide suitable, compliant properties that enable providers to deliver person-centered care, community integration, and value for money. Properties are designed to reduce institutional placements and support independent living.

This is a static website built with HTML, CSS, and JavaScript featuring a minimal, modern design.

## Development

Simply open `index.html` in a browser to view the site locally, or use a local server:

```bash
# Using Python's built-in server
python3 -m http.server 8000

# Then visit http://localhost:8000
```

## Project Structure

- `index.html` - Main website structure
- `styles.css` - Minimal, modern styling
- `script.js` - Interactive functionality