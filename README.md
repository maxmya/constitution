# 📜 The AI Agent Constitution & Binding Amendments

[![Ratification Status](https://img.shields.io/badge/Ratification-Amendments%201--20%20Frozen-blue.svg)](#ratification--the-frozen-core)
[![Governance](https://img.shields.io/badge/Governance-Stack--Agnostic-success.svg)](#scope--philosophy)
[![Test Coverage Floor](https://img.shields.io/badge/Coverage%20Floor-70%25%20First--Party-orange.svg)](#amendment-10--test-coverage-floor-70)
[![Git Flow](https://img.shields.io/badge/Branching-Git%20Flow%20Enforced-informational.svg)](#amendment-14--git-flow--pr-only-gateways)
[![CI/CD Gates](https://img.shields.io/badge/CI%2FCD-6%20Ordered%20Gates-purple.svg)](#amendment-16--ordered-cicd-pipeline-gates)

> **A stack-agnostic, project-agnostic constitutional framework and operational rulebook for autonomous AI coding agents.**

---

## 📑 Table of Contents

- [Overview & Purpose](#-overview--purpose)
- [Core Philosophy & Scope](#-core-philosophy--scope)
- [Ratification & The Frozen Core](#-ratification--the-frozen-core)
- [The 20 Ratified Amendments](#-the-20-ratified-amendments)
  - [1. Operational Discipline & Communication](#1-operational-discipline--communication)
  - [2. Safety, Permissions & Asset Protection](#2-safety-permissions--asset-protection)
  - [3. Software Craftsmanship & Testing Rigor](#3-software-craftsmanship--testing-rigor)
  - [4. Agile Architecture & Git Flow](#4-agile-architecture--git-flow)
  - [5. Ambient Feedback & Tooling](#5-ambient-feedback--tooling)
- [Lifecycle Workflows & Architecture](#-lifecycle-workflows--architecture)
  - [The Development Triplet Workflow](#the-development-triplet-workflow)
  - [Regression Escalation Protocol](#regression-escalation-protocol)
  - [CI/CD Ordered Gates](#cicd-ordered-gates)
- [Project Layout & Artifact Standards](#-project-layout--artifact-standards)
  - [The `agile/` Work Item Triplet](#the-agile-work-item-triplet)
  - [Branch Naming Taxonomy](#branch-naming-taxonomy)
  - [Audio State Dispatcher](#audio-state-dispatcher)
- [Adopting in Your Repositories](#-adopting-in-your-repositories)
- [Contributing & Amendment Lifecycle](#-contributing--amendment-lifecycle)
- [License](#-license)

---

## 🎯 Overview & Purpose

As AI coding agents take on complex engineering tasks across multi-repository workspaces, standard prompt instructions often break down:
- Agents make assumptions when specifications are ambiguous.
- Destructive commands (`rm -rf`, hard resets) destroy uncommitted human work.
- Code changes bypass version control and test coverage standards.
- Regressions are patched with symptomatic fixes rather than root-cause remediation.
- Project documentation drifts out of sync with codebases.

**The AI Agent Constitution (`AMENDMENTS.md`)** is a single, binding source of truth that governs how AI agents interact with codebases, file systems, Git repositories, CI/CD pipelines, and human authors. It turns loose conventions into strict, repeatable, and verifiable rules.

---

## 🏛️ Core Philosophy & Scope

1. **Stack-Agnostic & Project-Agnostic:** Specifies *what must be true*, never which language, framework, or cloud vendor makes it true.
2. **Centralized Authority:** Lives in one central repository (`constitution`) and is linked into downstream projects via `docs/AMENDMENTS.md`. Projects do not keep divergent, unmaintained local copies.
3. **Additive-Only Rules:** A new amendment never silently overrides an earlier rule. All changes and repeals must be explicitly documented.
4. **Composability:** Amendments compose as a unified system rather than a disconnected checklist.

---

## 🔒 Ratification & The Frozen Core

As of **2026-08-14**, **Amendments 1 through 20 are permanently ratified and frozen**.
- **Agent Modification Forbidden:** AI agents may never reword, clarify, soften, or alter frozen amendments.
- **Precedence:** If a proposed change conflicts with a frozen amendment, the agent must immediately pause, flag the exact conflict, and await author instructions.

---

## 📜 The 20 Ratified Amendments

### 1. Operational Discipline & Communication

| # | Amendment | Core Mandate |
|---|---|---|
| **1** | **Mandatory Briefing Format & Turn Verification** | Pre-execution signal verification on every turn; numbered, concise, article-stripped responses to allow direct line referencing. |
| **2** | **Critique First, Never Assume, Warn on Harm** | Critique requests against project ideology before coding; ask questionnaires for ambiguous details; warn on data loss, debt, or architectural risks before proceeding. |
| **4** | **No Visual Testing / Input Hijacking Without the Wheel** | Default to headless verification. No browser automation, UI clicking, or window-focus stealing unless the author explicitly yields control ("I leave the wheel for you"). |
| **8** | **Common Sense First; Ask Only for Author-Owned Decisions** | Agents resolve *craft unknowns* (naming, standard patterns) independently; agents only prompt the author for *author-owned decisions* (business logic, trade-offs, scope). |

### 2. Safety, Permissions & Asset Protection

| # | Amendment | Core Mandate |
|---|---|---|
| **5** | **Try Hard Before Asking; Sudo is Granted** | Agents must exhaust reasonable alternatives before escalating. Passwordless `sudo` is logged to `~/.claude/sudo-commands` via append-only hooks. |
| **6** | **Zero-Deletion Policy & Command Safety** | Authored content is **never deleted**. Deprecated files are moved to `~/claudetrashbin` for human review. Dangerous commands (`dd`, `mkfs`, raw piping into bash, firewall tampering) are strictly forbidden. |
| **17** | **Installed CLIs for Version Control** | All Git and forge tasks must use the native Git CLI and GitHub CLI (`gh`). State is read directly, never assumed. |

### 3. Software Craftsmanship & Testing Rigor

| # | Amendment | Core Mandate |
|---|---|---|
| **3** | **Plan Mode for Multi-Step Work** | Requests involving >3 distinct tasks or high architectural risk require planning mode before touching any files. Approved plans become scope boundaries. |
| **7** | **Craft: Clean Code, Right-Sized Architecture** | Strict adherence to SOLID/DRY principles. No dead code, god objects, or speculative over-engineering (no unnecessary factories, interfaces for single implementations, etc.). |
| **9** | **Regression Escalation Protocol** | **1st occurrence:** Standard fix with regression test. <br>**2nd occurrence:** `CODE ORANGE` — halt feature work, diagnose root cause, deploy rock-hard fix. <br>**3rd occurrence:** `CODE RED` — immediate handover to human author with full diagnostic logs. |
| **10** | **Test Coverage Floor: 70%** | Minimum **70% test coverage** on first-party code across all layers. Tests that don't assert are forbidden. Fixes must include regression tests. |

### 4. Agile Architecture & Git Flow

| # | Amendment | Core Mandate |
|---|---|---|
| **11** | **`docs/` Exists & Stays True** | Every repo maintains a living `docs/` folder with architectural decisions and system specs. Staleness is treated as a defect; docs are updated in the same change as code. |
| **12** | **`agile/` Work Item Triplets** | Strict documentation tree using `FEAT-###`, `TASK-###`, `BUG-###`. Every item must have its Item, Plan, and dual Test Plans (automated + manual sweep). |
| **13** | **Conventional Branch Isolation** | One branch per work item (`feature/FEAT-###-desc`, `bugfix/BUG-###-desc`). All branches branch from `dev` (hotfixes from `main`). |
| **14** | **Git Flow & PR-Only Gateways** | `main` and `dev` are protected. No direct commits or fast-forward pushes. Destructive Git commands (`git reset --hard`, `git clean`) require explicit confirmation. |
| **15** | **Release Builds Strategy** | Merges into `main` automatically publish tagged releases. Merges into `dev` run quality gates but trigger alpha/pre-release builds manually. |
| **16** | **Ordered CI/CD Pipeline Gates** | Ordered blocking verification gates: (1) License Check → (2) Code Quality → (3) Tests & Coverage → (4) Security Audit → (5) Build → (6) Release. |
| **18** | **Session Start: Review Open PRs** | Agent begins each workspace session by summarizing open pull requests, CI gate statuses, and potential merge conflicts. |

### 5. Ambient Feedback & Tooling

| # | Amendment | Core Mandate |
|---|---|---|
| **19** | **Audio Signals for Critical States** | Background audio playback notifies the author when they are away from screen for states like `FINISHED`, `NEED_INTERACTION`, `CONFLICT`, `CODE_ORANGE`, `CODE_RED`. |
| **20** | **Sound Catalogue as Structured Data** | Audio files live under `~/Dev/mywrok/AI_SOUNDS` in `SCREAMING_SNAKE_CASE.wav` format, mapped 1-to-1 with registered system states. |

---

## 🔄 Lifecycle Workflows & Architecture

### The Development Triplet Workflow

Every feature, task, or bug fix follows a deterministic lifecycle:

```mermaid
flowchart TD
    A([User Request / Task]) --> B{> 3 Tasks or Arch Risk?}
    B -- Yes --> C[Amendment 3: Plan Mode]
    B -- No --> D[Amendment 2: Critique & Scope]
    C --> E[Create Triplet in agile/]
    D --> E
    
    subgraph Agile Triplet
        E --> F1[agile/items/ID-name.md]
        E --> F2[agile/plans/ID-plan.md]
        E --> F3[agile/testing/ID-automated.md]
        E --> F4[agile/testing/ID-sweep.md]
    end
    
    E --> G[Cut Branch from dev: prefix/ID-description]
    G --> H[Implement Code & Update docs/]
    H --> I[Write Tests: ≥ 70% Coverage Floor]
    I --> J[Open PR into dev]
    J --> K{CI/CD Gates 1-4}
    K -- Pass --> L[Merge to dev]
    K -- Fail --> H
```

---

### Regression Escalation Protocol

When defects resurface, the agent follows Amendment 9's strict escalation hierarchy:

```mermaid
stateDiagram-v2
    [*] --> FirstBug: Defect Discovered
    FirstBug --> NormalFix: Implement Fix + Regression Test
    NormalFix --> Resolved: Verified
    NormalFix --> CodeOrange: Same Bug Reoccurs (2nd Time)
    
    state CodeOrange {
        [*] --> HaltFeatureWork
        HaltFeatureWork --> AnnounceCodeOrange: Announce "CODE ORANGE" + Play Audio
        AnnounceCodeOrange --> RootCausePlan: Formulate Rock-Hard Fix
        RootCausePlan --> ApprovedExecution: Author Approval
    }
    
    ApprovedExecution --> Resolved: Fix Holds
    ApprovedExecution --> CodeRed: Same Bug Reoccurs (3rd Time)
    
    state CodeRed {
        [*] --> HaltAllEdits
        HaltAllEdits --> AnnounceCodeRed: Announce "CODE RED" + Play Audio
        AnnounceCodeRed --> HandoverLogs: Compile All Diagnostics & Assumptions
        HandoverLogs --> AuthorTakeover: Immediate Handover to Human
    }
```

---

### CI/CD Ordered Gates

All pull requests pass through strict sequential gates defined in Amendment 16:

```mermaid
flowchart LR
    G1[1. License Check] --> G2[2. Code Quality & Lint]
    G2 --> G3[3. Tests & ≥70% Coverage]
    G3 --> G4[4. Security & Audit]
    G4 --> G5[5. Platform Build]
    G5 --> G6[6. Publish & Release]
    
    classDef gate fill:#f9f9f9,stroke:#333,stroke-width:1px;
    class G1,G2,G3,G4,G5,G6 gate;
```

- **`dev` Target:** Runs Gates 1 through 4. Build and Alpha deployment are triggered manually.
- **`main` Target:** Runs all 6 gates sequentially. Success triggers automated tagging and release artifact publication.

---

## 📂 Project Layout & Artifact Standards

Every downstream repository managed under these amendments adopts the standard file tree:

```
<project-root>/
├── .github/
│   └── workflows/ci.yml       # Ordered CI/CD Pipeline (Amendment 16)
├── agile/                     # Amendment 12: Work Tracking
│   ├── items/                 # What & Why (FEAT-###, TASK-###, BUG-###)
│   ├── plans/                 # Architecture & Implementation Plans
│   └── testing/               # Dual Test Plans:
│       ├── <ID>-automated.md  # Unit/Integration assertion log & coverage %
│       └── <ID>-sweep.md      # Manual step-by-step test tickets
├── docs/                      # Amendment 11: Persistent Documentation
│   ├── AMENDMENTS.md          # Pointer to central constitution repository
│   ├── architecture/          # ADRs, Module Boundaries, Data Flows
│   └── ci-cd.md               # Gate definitions & tooling choices
└── src/                       # First-party source code (≥ 70% coverage floor)
```

### The `agile/` Work Item Triplet

| Directory | File Pattern | Purpose |
|---|---|---|
| `agile/items/` | `FEAT-004-split-view.md` | Problem statement, business value, acceptance criteria, dependencies. |
| `agile/plans/` | `FEAT-004-plan.md` | Architectural decisions, affected files, rollback strategy, implementation steps. |
| `agile/testing/` | `FEAT-004-automated.md` | Automated test suite breakdown and verified first-party coverage report. |
| `agile/testing/` | `FEAT-004-sweep.md` | Structured test tickets for manual human sweeps (preconditions, steps, expected vs. actual). |

---

### Branch Naming Taxonomy

Branches are strictly mapped to agile work item IDs under Amendment 13:

| Type | Branch Pattern | Example | Base Branch |
|---|---|---|---|
| **Feature** | `feature/<ID>-<kebab-name>` | `feature/FEAT-042-auth-provider` | `dev` |
| **Task / Chore** | `task/<ID>-<kebab-name>` or `chore/...` | `task/TASK-018-upgrade-deps` | `dev` |
| **Bugfix** | `bugfix/<ID>-<kebab-name>` | `bugfix/BUG-103-null-pointer` | `dev` |
| **Hotfix** | `hotfix/<ID>-<kebab-name>` | `hotfix/BUG-104-memory-leak` | `main` |
| **Release** | `release/v<MAJOR.MINOR.PATCH>` | `release/v2.1.0` | `dev` |

---

### Audio State Dispatcher

Under Amendments 19 & 20, critical workflow milestones trigger background audio notifications from `~/Dev/mywrok/AI_SOUNDS`:

```bash
pw-play ~/Dev/mywrok/AI_SOUNDS/FINISHED.wav >/dev/null 2>&1 &
```

| Signal File | State / Trigger Condition |
|---|---|
| `FINISHED.wav` | Work complete; all tests passing and no blocking actions pending. |
| `NEED_INTERACTION.wav` | Agent paused waiting for a human decision or credential authorization. |
| `CALL_ME_FOR_QUESTIONARY.wav` | Paused to present an Amendment 2 multi-point clarifying questionnaire. |
| `CONFLICT.wav` | Blocked by merge conflicts or irreconcilable architecture conflicts. |
| `CODE_ORANGE.wav` | Bug reappeared after 1st fix; halting feature work for root-cause plan. |
| `CODE_RED.wav` | Bug survived 2 fixes; immediate diagnostic handover to author. |
| `RELEASE_MADE.wav` | Automated production release build deployed on `main`. |

---

## 🚀 Adopting in Your Repositories

To enforce the Constitution across your repositories:

### 1. Link the Constitution
In your child repository, create `docs/AMENDMENTS.md` pointing to this central repository:

```markdown
# Amendments Reference
This repository operates under the canonical AI Agent Constitution:
Canonical Repository: https://github.com/maxmya/constitution.git
See [AMENDMENTS.md](file:///path/to/central/constitution/AMENDMENTS.md) for full text.
```

### 2. Configure Agent Instruction Harness
Add the following directive to your agent configuration (`.cursorrules`, `.windsurfrules`, `CLAUDE.md`, or Antigravity rules):

```markdown
You are bound by the AI Agent Constitution defined in `AMENDMENTS.md`.
1. All changes must satisfy Amendments 1 through 20.
2. Every change must maintain the `agile/` triplet and `docs/` sync.
3. Test coverage on first-party code must remain at or above 70%.
4. Protected branches (`main`, `dev`) are modified via Pull Request only.
5. Authored content must never be deleted; move deprecated files to `~/claudetrashbin`.
```

---

## 🤝 Contributing & Amendment Lifecycle

- **Proposing Amendments:** New amendments (Amendment 21+) must be proposed via Pull Request to this repository.
- **Additive Consistency:** Proposed amendments must not weaken or conflict with Amendments 1–20.
- **Ratification:** Amendments become binding only when explicitly ratified and frozen by the author.

---

## 📄 License

This governance standard is open-sourced under the **MIT License**. You are free to adopt, modify, and reference this constitution across all your AI-assisted engineering projects.
