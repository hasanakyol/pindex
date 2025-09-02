# Pindex

A universal, architecture-agnostic framework for building software through structured specifications, optimized for AI-powered development tools. Works with any language, any architecture pattern, new or existing codebases.

```
 ██████╗  ██╗ ███╗   ██╗ ██████╗  ███████╗ ██╗  ██╗
 ██╔══██╗ ██║ ████╗  ██║ ██╔══██╗ ██╔════╝ ╚██╗██╔╝
 ██████╔╝ ██║ ██╔██╗ ██║ ██║  ██║ █████╗    ╚███╔╝
 ██╔═══╝  ██║ ██║╚██╗██║ ██║  ██║ ██╔══╝    ██╔██╗
 ██║      ██║ ██║ ╚████║ ██████╔╝ ███████╗ ██╔╝ ██╗
 ╚═╝      ╚═╝ ╚═╝  ╚═══╝ ╚═════╝  ╚══════╝ ╚═╝  ╚═╝
 by @hasanakyol
```
## 📋 Prerequisites

- **Claude Code** - This framework is designed to work with [Claude Code](https://claude.ai/code), Anthropic's official CLI for Claude
- A project directory where you want to build software

## 🛠️ Installation

```bash
# Option 1: Using gitpick (recommended) - directly clone framework to your project
npx gitpick hasanakyol/pindex/tree/main/.claude
npx gitpick hasanakyol/pindex/blob/main/CLAUDE.md  # Also get the quick reference

# Option 2: Manual installation
git clone https://github.com/hasanakyol/pindex.git
cd pindex
cp -r .claude CLAUDE.md /path/to/your/project/
```

**Follow the workflow**: Plan → Requirements → Design → Tasks → Align → Execute

## 🎯 The 6-Phase Workflow

```
1. /pin:plan [description]     → Feature Breakdown      → [Approval Gate]
2. /pin:requirements [feature] → Feature Specifications → [Approval Gate]
3. /pin:design [feature]       → Technical Design       → [Approval Gate]
4. /pin:tasks [feature]        → Task Breakdown         → [Approval Gate]
5. /pin:align [feature]        → Alignment Check        → [Approval Gate]
6. /pin:execute [feature]      → Working Code           → [Testing & Deploy]
```

### Phase 1️⃣: Planning (`/pin:plan`)
Break down a project goal into manageable features through interactive discussion.
- **Input**: Project description (+ optional "--all" flag for draft requirements)
- **Output**: Feature directories with template requirements (or draft EARS requirements if "--all" flag used)
- **Gate**: "Ready to detail requirements for the first feature?"

### Phase 2️⃣: Requirements (`/pin:requirements`)
Define WHAT needs to be built using EARS format.
- **Input**: Feature name
- **Output**: Detailed `requirements.md` with testable specifications
- **Gate**: "Requirements complete. Ready for design phase?"

### Phase 3️⃣: Design (`/pin:design`)
Define HOW it will be built with technical specifications.
- **Input**: Approved requirements
- **Output**: `design.md` with architecture, APIs, and data models
- **Gate**: "Technical design complete. Ready for task breakdown?"

### Phase 4️⃣: Tasks (`/pin:tasks`)
Break down design into TDD implementation steps.
- **Input**: Approved design
- **Output**: `tasks.md` with Red-Green-Refactor cycles
- **Gate**: "Task breakdown complete. Ready to validate?"

### Phase 5️⃣: Alignment (`/pin:align`)
Ensure alignment between all specifications.
- **Input**: Requirements, design, and tasks
- **Output**: Validation report and fixes if needed
- **Gate**: "Specifications aligned. Ready to implement?"

### Phase 6️⃣: Implementation (`/pin:execute`)
Execute the implementation plan using TDD.
- **Input**: Validated specifications
- **Output**: Working, tested code
- **Approaches**: TDD, Standard, Collaborative, or Self-implementation

## 📋 Commands Reference

| Phase | Command | Purpose |
|-------|---------|---------|
| 1️⃣ | `/pin:plan [description] [--all]` | Interactive discussion → features ("--all" = draft EARS requirements) |
| 2️⃣ | `/pin:requirements [feature]` | Create EARS requirements |
| 3️⃣ | `/pin:design [feature]` | Generate technical design |
| 4️⃣ | `/pin:tasks [feature]` | Create TDD implementation plan |
| 5️⃣ | `/pin:align [feature]` | Validate alignment & consistency |
| 6️⃣ | `/pin:execute [feature]` | Execute implementation |
| 📋 | `/pin:list` | List all features |
| 📊 | `/pin:status` | Show implementation status |
| ❓ | `/pin:help` | Command help |

## 🔧 Key Concepts

### EARS Requirements Format
Structured, testable requirements using standardized patterns:

| Pattern | Format |
|---------|--------|
| **Ubiquitous** | "The system SHALL [requirement]" |
| **Event-Driven** | "WHEN [trigger] THEN the system SHALL [response]" |
| **State-Driven** | "WHILE [state] the system SHALL [requirement]" |
| **Conditional** | "IF [condition] THEN the system SHALL [requirement]" |

**Example**: "WHEN a user enters incorrect credentials three times THEN the system SHALL lock the account for 15 minutes."

### Test-Driven Development (TDD)
Every implementation follows the Red-Green-Refactor-Validate cycle:
1. **🔴 Red**: Write failing test
2. **🟢 Green**: Write minimal code to pass
3. **🔄 Refactor**: Improve code structure
4. **✅ Validate**: Re-run tests to ensure refactoring didn't break functionality
5. **🔗 Integration**: Test interactions between completed tasks

### Quality Gates
- ✅ **Requirements**: Testable, specific, EARS-formatted
- ✅ **Design**: Addresses all requirements, technically sound, security-aware
- ✅ **Tasks**: Granular, actionable, includes test scenarios
- ✅ **Security**: OWASP 2025 compliance, AI/LLM threats addressed

## 📁 Project Structure

```
your-project/
├── .claude/
│   ├── CLAUDE.md                 # Complete methodology
│   ├── commands/pin/             # Concise slash commands (~85% smaller)
│   │   ├── plan.md
│   │   ├── requirements.md
│   │   ├── design.md
│   │   ├── tasks.md
│   │   ├── execute.md
│   │   ├── align.md
│   │   ├── feature.md
│   │   ├── list.md
│   │   ├── status.md
│   │   └── help.md
│   ├── core/                     # Reusable logic (NEW)
│   │   ├── feature-selection.md # Feature selection logic
│   │   ├── validation-rules.md  # Prerequisites & validation
│   │   ├── standards-table.md   # Quality standards
│   │   ├── tdd-process.md      # TDD cycle definition
│   │   ├── output-formats.md    # Output messages
│   │   └── shared-logic.md     # Index of core logic
│   ├── templates/                # Document templates
│   │   ├── requirements.md
│   │   ├── design.md
│   │   ├── tasks.md
│   │   └── tldr.md
│   ├── ARCHITECTURE.md           # Project architecture
│   ├── CONVENTIONS.md            # Coding standards
│   └── SECURITY.md               # OWASP 2025 checklist
└── features/                     # Generated specifications
    └── [feature-name]/
        ├── requirements.md       # EARS requirements
        ├── design.md            # Technical design
        ├── tasks.md             # TDD task breakdown
        └── tldr.md              # Implementation summary
```

## 💡 Why This Works

**Problems Solved:**
- ❌ Context overload → ✅ Focused commands
- ❌ Reliability issues → ✅ Smaller, reliable operations
- ❌ Poor iteration → ✅ Independent phase modification
- ❌ Vague requirements → ✅ EARS precision

**Benefits:**
- **Human Control**: Explicit approval gates
- **Quality Assurance**: Built-in testing via TDD
- **Security-First**: OWASP 2025 & AI/LLM security built-in
- **Token Efficient**: 85% reduction through modular architecture
- **Maintainable**: DRY principle, shared logic in one place
- **Iterative**: Easy to refine individual phases
- **Scalable**: Works for simple features to complex systems

## 🤝 Contributing

We welcome contributions! Please see our [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on how to make this project better.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

Made with ❤️ by [Hasan Akyol](https://github.com/hasanakyol)
