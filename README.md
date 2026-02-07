# FPF Engineering Standards

Structured reasoning discipline for software development with Claude Code.

Provides confidence tracking (L0/L1/L2), stage-aware decision calibration, weakest-link analysis, and hypothesis-based reasoning — as a set of reusable skills and a CLAUDE.md configuration.

## Installation

### Plugin (global, persistent)

```bash
# Add the marketplace source
claude plugin marketplace add m0n0x41d/fpf-swe-discipline-skillpack

# Install the plugin
claude plugin install fpf-swe-discipline@fpf-swe-discipline-skillpack
```

This installs five skills that Claude invokes automatically based on context:

| Skill | Purpose |
|-------|---------|
| `adi-reasoning` | Hypothesis-based reasoning for architecture and debugging |
| `confidence-scope` | Confidence level and scope marking for assertions |
| `wlnk-mono` | Weakest link and MONO analysis for reliability |
| `temporal-check` | Plan vs reality checks for debugging discrepancies |
| `bounded-context` | Term translation across service/domain boundaries |

### Plugin (local, single session)

```bash
claude --plugin-dir /path/to/fpf-swe-discipline-skillpack
```

### CLAUDE.md (engineering standards)

Copy `CLAUDE.md` to your global or project-level config:

```bash
# Global — applies to all projects
cp CLAUDE.md ~/.claude/CLAUDE.md

# Project — applies to one project
cp CLAUDE.md /path/to/your/project/CLAUDE.md
```

### Project docs scaffold

Copy the `template/docs/` directory to bootstrap project knowledge management:

```bash
cp -r template/docs /path/to/your/project/docs
```

This creates:

```
docs/
├── decisions/        # Architecture Decision Records
│   └── _template.md  # FPF-enhanced ADR template
├── context/
│   ├── stack.md      # Technologies, versions, rationale
│   ├── commands.md   # Build, test, deploy commands
│   ├── constraints.md # Known limitations, gotchas
│   ├── patterns.md   # Debugging patterns, resolved issues
│   └── integrations.md # External APIs, contracts
└── active-context.md # Session handoff state
```

## What's in the box

**CLAUDE.md** — Engineering standards covering modularity, contracts, correctness, complexity control, testing philosophy, communication style, and a decision framework with stage-aware calibration.

**Skills** — Five self-contained reasoning tools following the [Agent Skills](https://agentskills.io) open standard. Each provides a structured process and output format for a specific type of engineering problem.

**Template** — Project documentation scaffold with ADR template, context files, and session handoff format.

## Attribution

Built on the [First Principles Framework (FPF)](https://github.com/ailev/FPF) by [Anatoly Levenchuk](https://github.com/ailev). This skillpack adapts FPF's epistemic discipline — confidence levels, weakest-link analysis, hypothesis-based reasoning — for software engineering workflows with Claude Code.

## Key concepts

- **L0/L1/L2** — Confidence levels: untested guess, logically derived, empirically verified
- **Stages** — Explore, Shape, Evidence, Operate — determines required rigor
- **WLNK** — System reliability = min(component reliabilities), never average
- **MONO** — More complexity can decrease reliability; additions must justify new failure points
- **Transformer** — Always identify who/what performs the change
