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
## 🛠️ Installation

```bash
# Clone and copy to your project
git clone https://github.com/hasanakyol/pindex.git
cd pindex
cp -r .claude architecture.md conventions.md /path/to/your/project/
```

**Follow the workflow**: Plan → Requirements → Design → Tasks → Execute

## 🎯 The 6-Phase Workflow

```
1. /spec:plan [description]     → Feature List     → [Approval Gate]
2. /spec:requirements [feature] → requirements.md  → [Approval Gate]
3. /spec:design [feature]       → design.md        → [Approval Gate]
4. /spec:tasks [feature]        → tasks.md         → [Approval Gate]
5. /spec:validate [feature]     → Alignment Check  → [Approval Gate]
6. /spec:execute [feature]      → Working Code     → [Testing & Deploy]
```

### Phase 1️⃣: Planning (`/spec:plan`)
Break down a project goal into manageable features through interactive discussion.
- **Input**: Project description (+ optional "all" flag for draft requirements)
- **Output**: Feature directories with template requirements (or draft EARS requirements if "all" flag used)
- **Gate**: "Ready to detail requirements for the first feature?"

### Phase 2️⃣: Requirements (`/spec:requirements`)
Define WHAT needs to be built using EARS format.
- **Input**: Feature name
- **Output**: Detailed `requirements.md` with testable specifications
- **Gate**: "Requirements complete. Ready for design phase?"

### Phase 3️⃣: Design (`/spec:design`)
Define HOW it will be built with technical specifications.
- **Input**: Approved requirements
- **Output**: `design.md` with architecture, APIs, and data models
- **Gate**: "Technical design complete. Ready for task breakdown?"

### Phase 4️⃣: Tasks (`/spec:tasks`)
Break down design into TDD implementation steps.
- **Input**: Approved design
- **Output**: `tasks.md` with Red-Green-Refactor cycles
- **Gate**: "Task breakdown complete. Ready to validate?"

### Phase 5️⃣: Validation (`/spec:validate`)
Ensure alignment between all specifications.
- **Input**: Requirements, design, and tasks
- **Output**: Validation report and fixes if needed
- **Gate**: "Specifications aligned. Ready to implement?"

### Phase 6️⃣: Implementation (`/spec:execute`)
Execute the implementation plan using TDD.
- **Input**: Validated specifications
- **Output**: Working, tested code
- **Approaches**: TDD, Standard, Collaborative, or Self-implementation

## 📋 Commands Reference

| Phase | Command | Purpose |
|-------|---------|---------|
| 1️⃣ | `/spec:plan [description] [all]` | Interactive discussion → features ("all" = draft EARS requirements) |
| 2️⃣ | `/spec:requirements [feature]` | Create EARS requirements |
| 3️⃣ | `/spec:design [feature]` | Generate technical design |
| 4️⃣ | `/spec:tasks [feature]` | Create TDD implementation plan |
| 5️⃣ | `/spec:validate [feature]` | Validate alignment & consistency |
| 6️⃣ | `/spec:execute [feature]` | Execute implementation |
| ✅ | `/spec:check` | Framework health check & validation |
| 🎯 | `/spec:advanced` | Enterprise-grade analysis (STRIDE, risk) |
| 📋 | `/spec:list` | List all features |
| 📊 | `/spec:status` | Show implementation status |
| ❓ | `/spec:help` | Command help |

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
Every implementation follows the Red-Green-Refactor cycle:
1. **🔴 Red**: Write failing test
2. **🟢 Green**: Write minimal code to pass
3. **🔄 Refactor**: Improve code while keeping tests green

### Quality Gates
- ✅ **Requirements**: Testable, specific, EARS-formatted
- ✅ **Design**: Addresses all requirements, technically sound
- ✅ **Tasks**: Granular, actionable, includes test scenarios

## 📁 Project Structure

```
your-project/
├── .claude/
│   ├── CLAUDE.md                 # Complete methodology
│   ├── commands/spec/            # Slash commands
│   │   ├── plan.md, requirements.md, design.md
│   │   ├── tasks.md, execute.md, advanced.md
│   │   ├── list.md, status.md, help.md
│   └── templates/                # Reference templates
│       ├── requirements.md
│       ├── design.md
│       ├── tasks.md
│       └── tldr.md
└── features/                     # Generated specifications
    └── [feature-name]/
        ├── requirements.md       # EARS requirements
        ├── design.md            # Technical design
        ├── tasks.md             # TDD task breakdown
        └── tldr.md  # Completion summaries
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
- **Iterative**: Easy to refine individual phases
- **Scalable**: Works for simple features to complex systems

## 🤝 Contributing

We welcome contributions! Please see our [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on how to make this project better.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

Made with ❤️ by [Hasan Akyol](https://github.com/hasanakyol) 

