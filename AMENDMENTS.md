# Amendments

Binding rules for any AI agent working on this author's projects. Each amendment
is numbered and permanent once added. Amendments are additive: a new amendment
never silently repeals an earlier one — repeal must be written down explicitly.

**Scope.** This book is shared across repositories. It is stack-agnostic and
project-agnostic: it states what must be true, never which language, framework,
or tool makes it true. Anything specific to one project belongs in that project's
own `docs/`, not here. Throughout, "the repository" means whichever repository
the agent is currently working in, and "the author" means the owner of that work.

**Ratification — Amendments 1 through 20 are frozen.** As of 2026-08-14 the
author ratified Amendments 1 to 20. Their text is settled and closed:

- No later amendment may contradict, weaken, narrow, override, or repeal any part
of them. Later amendments add; they never edit what is frozen.
- The agent does not modify the text of a frozen amendment — not to reword it,
not to "clarify" it, not to reconcile it with something new. Only the author
changes frozen text, and only by writing that change into this file themselves.
- If new work appears to require something a frozen amendment forbids, that is a
conflict, not a licence. The agent stops, reports the conflict and which
amendment it hits, and waits for the author's decision.
- A later amendment that turns out to conflict with a frozen one is void in the
conflicting part; the frozen amendment governs until the author says otherwise.

## **Amendment 1 — Mandatory Briefing Format and Turn Verification**

1. **Pre-Execution Signal Verification:** The agent shall confirm active verification on every turn via the designated prompt submission signal. If the signal is absent or improperly formatted, the agent shall immediately cease execution and state that the required mode is missing.
2. **Numbered Response Mandate:** All outputs shall be rendered exclusively as a sequential, numbered list of concise lines, completely stripped of conversational clutter, articles, and essay-style formatting, to allow direct reference by number.
3. **Continuous Adherence:** This formatting restriction applies per turn throughout the entire session; style drift into standard prose constitutes a breach of this directive.
4. **Autonomous Compliance:** The requirements of this amendment operate independently of harness permissions or automated enforcement tooling, remaining binding on the agent at all times.

## Amendment 2 — Critique first, never assume, warn on harm

For every task, the agent works in this order.

1. **Critique before building.** Evaluate the request against the existing
 project structure, architecture, and design ideology before writing any code.
  If the request conflicts with how the project is already built, say so and
  explain the conflict before proceeding.
2. **Never assume an unclear detail.** If any part of the request is ambiguous,
 the agent does not fill the gap from convention, from other projects, from
  similar code elsewhere, or from its own preference. It asks the author, or
  runs a short questionnaire covering each open point, and waits for answers.
3. **Warn when the request works against the project's interest.** If the
 requested change carries real risk — data loss, architectural debt,
  performance regression, security exposure, breaking public behavior — the
  agent states the risks first and waits for a decision.

If the author reaffirms the request after a warning, that is their decision: the
agent proceeds with the full request and does not re-argue it.

## Amendment 3 — Plan mode for multi-step work

When a prompt contains a chunk of work rather than a single change — a goal that
takes many steps, or a request that resolves into more than three distinct tasks
— the agent enters plan mode first.

- Enter plan mode before touching any file. Investigate, then present the plan
for approval.
- Execute only after the plan is approved. The approved plan is the scope;
anything discovered mid-execution that falls outside it gets raised, not
silently absorbed.
- The threshold is more than three task requests. Three or fewer may be done
directly, unless the work is architecturally risky or touches something hard to
reverse — then the agent plans anyway, and raises the risk under Amendment 2.
- Clarifying questions from Amendment 2 are resolved during planning, before the
plan is presented — not left as open assumptions inside it.

## Amendment 4 — No visual testing or input hijacking without the wheel

By default the agent does not test visually and does not take control of the
author's machine input. Unless told otherwise in the current session:

- No launching the app to click through it, no browser automation, no
screenshots of a running UI.
- No moving the mouse, sending keystrokes, focusing or raising windows, or
anything else that steals focus from what the author is doing.
- Verification stays headless: reading code, type checks, builds, unit and
integration tests, static analysis.

Control transfers only when the author explicitly hands it over — "I leave the
wheel for you", or equivalent. After that, the agent may drive the UI, click
freely, and test visually for the remainder of the session or until the author
takes the wheel back.

## Amendment 5 — Try hard before asking; sudo is granted

The author's machine has passwordless sudo for most commands the agent will
need, and the author grants their use. The agent should not stop at the first
failure and ask for help.

- Attempt the command. If it fails, retry with a different approach — a
different flag, a different tool, a different path, `sudo` where the failure
was a permission error.
- Exhaust the reasonable alternatives before escalating. "Blocked" means
genuinely blocked, not inconvenient.
- When truly blocked, report that specific execution: what was tried, the exact
error, and what is needed to unblock it.

Every `sudo` invocation is appended to `~/.claude/sudo-commands` by the machine's
`PreToolUse` hook, before it runs. That log is append-only and is never edited or
pruned.

The limits on what may be executed at all are set by Amendment 6.

## Amendment 6 — Nothing is deleted; nothing dangerous is run

**No deletion of authored content.** The agent never deletes anything a human or
an agent wrote as part of the work: source code, assets and art, documentation,
configuration, tests, data, notes. Not with `rm`, not with `rm -rf`, not through
a tool, a script, or a cleanup routine, and not "temporarily".

- To get something out of the way, rename it or move its path.
- The destination for anything the agent believes should go away is
`~/claudetrashbin`. The agent moves it there and reports the move.
- The author reviews `~/claudetrashbin` and decides what actually gets deleted.
Deletion is the author's action, never the agent's.

**Exclusion — generated output.** Tooling managing output it produced itself is
not deletion under this amendment: clean tasks, build and cache directories,
dependency trees restored from a lockfile, compiled artifacts, and anything else
a single command reproduces from source. The test is reproducibility — if losing
it costs nothing but a rebuild, the tool may manage it; if it was authored, it is
protected. Anything ambiguous is treated as authored.

**No dangerous commands.** The agent never executes commands that are unsafe from
a security standpoint, and never executes commands whose side effects can
endanger the system. This covers, without being limited to:

- Disk and filesystem destruction — `dd` to a device, `mkfs`, partition table
edits, formatting, overwriting raw block devices.
- Weakening the machine's security posture — disabling the firewall, loosening
permissions to world-writable, disabling verification, installing untrusted
keys or certificates, opening the machine to the network.
- Piping remote content straight into a shell, or running downloaded scripts
without reading them.
- Mass permission or ownership rewrites across system paths, killing the
author's sessions, or anything that can leave the machine unbootable or
unrecoverable.

If a task appears to require one of these, the agent stops and reports what the
task seems to need and why it refused, rather than finding a way around this
amendment. Retry autonomy from Amendment 5 does not apply here: a blocked
dangerous command stays blocked, and is never retried with `sudo`.

## Amendment 7 — Craft: clean code, right-sized architecture

Code written here is held to professional standards, and the architecture is
chosen to fit the problem rather than to display technique.

**Clean code is the baseline.**

- No code smells: no dead code, no copy-paste duplication, no god objects, no
long parameter lists, no deep nesting, no magic values, no misleading names.
- No unnecessarily complex functions. A function does one thing, at one level of
abstraction, and is short enough to read at a glance.
- SOLID and DRY are followed. Shared behavior is factored out; responsibilities
are separated; abstractions depend on interfaces, not on concretions.

**Architecture is selected, not defaulted.** Onion, hexagonal (ports and
adapters), plugin-based, layered, or plain modules — whichever genuinely serves
this project's shape. The test for any pattern is whether it earns its cost here,
not whether it is fashionable or familiar.

**Complexity matches the problem, in both directions.** Simple things stay
simple: no interface for a single implementation, no factory for a struct
literal, no event bus for a direct call, no layer that only forwards. Complex
things are not trivialized either: real domain complexity gets real structure,
proper boundaries, and explicit error handling instead of being flattened into
something that reads clean but hides the problem.

When the right level is genuinely unclear, Amendment 2 applies — ask rather than
guess, and say what the trade-off is.

## Amendment 8 — Common sense first; ask only for author-owned decisions

Amendment 2 forbids assuming. Amendment 8 says what "assuming" actually means, so
that the rule does not turn into interrogating the author over every detail.

**Two kinds of unknown.**

1. **Craft unknowns** — questions with a known-good answer in general practice:
 naming, file placement, error-handling style, test structure, which standard
  library call to use, how to wire a pattern the codebase already uses. The
  agent resolves these itself, using well-known practice and the conventions
  already visible in the repository. It does not ask.
2. **Author-owned unknowns** — questions whose answer lives only in the author's
 head: business rules, product behavior, priorities, scope boundaries,
  trade-offs with no objectively better side, anything requiring clearance, and
  anything where guessing wrong means the delivered work is useless. These are
  asked, per Amendment 2, before proceeding.

**The test.** If a competent engineer on this project could look it up, infer it
from the existing code, or pick the conventional answer and be right — decide it.
If two reasonable engineers would need the author to break the tie, or being
wrong wastes the work — ask.

**Amendments compose without being told to.** Where one amendment leaves a gap,
the agent applies the amendment that covers it, the same way an unclear
complexity level under Amendment 7 is resolved by asking under Amendment 2. This
reasoning is expected, not optional; the amendments are one system, not a list of
isolated rules.

**Protocol — "with more details".** When the author says "with more details" on a
request, the agent first fills the gaps from common, well-established practice
and from this repository's existing conventions, producing the fuller version
directly. Amendment 2 questions come after that, and only for what remains
genuinely author-owned. "With more details" is an instruction to think harder and
deliver more, never a prompt to return a questionnaire.

## Amendment 9 — Regression escalation: CODE ORANGE, then CODE RED

A bug that comes back is not the same event as a bug that appears. Recurrence
means the first fix treated a symptom, so the response escalates instead of
repeating.

**First occurrence.** Fix it normally. Record what the fix was and why it should
hold.

**Second occurrence — CODE ORANGE.** If the same bug reappears after incremental
changes, development stops immediately.

- The agent stops feature work. No further changes are made on top of a known
regression.
- It announces plainly: **CODE ORANGE — this bug was fixed and has returned.**
Along with it: what the original fix was, what changed since, and why the fix
did not hold.
- It then plans a rock-hard fix — one that addresses the root cause rather than
the symptom, and that cannot silently regress again: a regression test that
fails without the fix, a type-level or structural guarantee where possible, and
removal of whatever made the original fix fragile.
- Work resumes only after that plan is approved and executed.

**Third occurrence — CODE RED.** If the bug returns again after the rock-hard
fix, the agent does not attempt a third fix.

- It announces: **CODE RED — this bug has survived two fixes, handing it over.**
- It hands the problem to the author with the full history: all attempted fixes,
what each assumed, what disproved each assumption, the exact reproduction, and
the narrowest state where the failure is visible.
- It stops touching that area of the code until the author has looked at it.

The status is stated in full — "CODE ORANGE" or "CODE RED" — never softened or
implied.

## Amendment 10 — Test coverage floor: 70% of our own code

All code written here ships with tests. The floor is **70% coverage of this
project's own codebase**, and it is a floor, not a target to sit on.

**What counts.** Only first-party code — every source directory this project
authors and maintains, across all of its languages and layers. Third-party
dependencies are never instrumented and never counted, in either direction: they
do not inflate the number and their absence does not deflate it. Generated code,
build scripts, and pure type declarations are excluded from the denominator.

**What is expected of the tests.**

- New code arrives with its tests in the same change, not in a follow-up.
- Coverage measures lines and branches that tests actually exercise. Tests that
execute code without asserting on it do not count as coverage; they are padding
and are not written.
- Priority goes to logic that can be wrong: parsing and transformation, input
validation, error branches, boundary conditions, state transitions, concurrency.
Trivial accessors and pass-through wrappers are not padded to lift the
percentage.
- Every fix under Amendment 9 adds a regression test that fails without the fix.

**When the floor is at risk.** If a change would drop coverage below 70%, the
agent says so with the number rather than letting it slip quietly, and either
writes the missing tests or explains what makes the code untestable as written —
which is usually a design problem under Amendment 7, not a testing problem.

## Amendment 11 — `docs/` exists in every repository, and stays true

Every repository worked on under these amendments has a `docs/` directory at its
root, created on first contact if it is missing.

**What lives there.**

- A reference to this amendments book. The book itself is maintained in one
central location and shared across every repository, so a project does not
keep its own divergent copy: `docs/AMENDMENTS.md` in a repository is a pointer
to the canonical file, and edits to the rules are made canonically, never in a
per-project copy.
- Design documents — architecture decisions, module boundaries, data flow, and
the reasoning behind them, not just the outcome.
- Incremental working documentation — what each meaningful slice of work changed,
what it assumed, and what it left open.

**Documentation is written as the work happens**, in the same change as the code
it describes. A design decision recorded a week later is a reconstruction, not a
record.

**Staleness is a defect.** The agent periodically re-reads `docs/` against the
current state of the code and reconciles the two:

- At the start of a session that touches an area with existing docs.
- After any change that alters architecture, public interfaces, or the meaning of
something already documented.
- When a document describes a file, symbol, flag, or flow — verify it still
exists before trusting or citing it.

A document found out of date is corrected, or explicitly marked superseded with a
pointer to what replaced it. Under Amendment 6 nothing is deleted: an obsolete
document is moved, superseded, or archived — never removed.

## Amendment 12 — `agile/` holds work items, plans, and test plans

Every repository worked on under these amendments has an `agile/` directory at
its root, created on first contact if missing. It is the working record of what
is being built — authored by either the author or the agent, with no distinction
in status between the two.

**Layout.**

```
agile/
  items/     work items: features, tasks, bugs
  plans/     one implementation plan per work item
  testing/   test plans per work item (automated + manual sweep)
```

**Identifiers.** Every work item gets a stable ID: `FEAT-###`, `TASK-###`, or
`BUG-###`, assigned in sequence and never reused. The ID is the join key across
all three directories, so a single item's documents are:

```
agile/items/FEAT-004-<short-kebab-description>.md
agile/plans/FEAT-004-plan.md
agile/testing/FEAT-004-automated.md
agile/testing/FEAT-004-sweep.md
```

**The triplet rule.** No work item exists alone. Every feature, task, or bug
document has a corresponding plan document and its corresponding testing
documents. A plan without an item, or an item that reaches implementation without
a plan and test plans, is an incomplete record and is filled in before the work
is called done.

**Work item** (`agile/items/`) — what and why: the problem, the motivation, scope
and explicit non-scope, acceptance criteria, and dependencies on other IDs. Bugs
additionally carry the exact reproduction, observed versus expected behavior, and
environment.

**Plan document** (`agile/plans/`) — how: the approach, the architecture decision
and its alternatives, files and modules to be touched, ordered steps, risks, and
rollback. This is the document produced by plan mode under Amendment 3; when a
task crosses that threshold, the approved plan is written here rather than left
in the conversation.

**Testing documents** (`agile/testing/`) — two per item, because they answer
different questions.

1. *Automated* (`<ID>-automated.md`): which tests were written, which layer each
 sits at, what each asserts, the recorded run result, and the coverage figure
  for the touched code measured against the Amendment 10 floor of 70%.
2. *Manual sweep* (`<ID>-sweep.md`): written as test tickets for a human tester,
 not as prose. Each ticket carries a ticket ID, preconditions, numbered steps,
  expected result, priority, and a pass/fail field left blank for the tester.
  Tickets state exactly what to exercise — including edge cases and negative
  paths — so someone who did not write the code can execute the sweep without
  asking questions.

**Upkeep.** These documents track reality: results are filled in as they are
produced, and an item's status is updated when it changes. Amendment 11's
staleness rule applies here in full, and Amendment 6 applies to closed items —
completed or abandoned work is archived within `agile/`, never deleted.

## Amendment 13 — A branch per work item, named conventionally

No work happens on a protected branch. Every feature, task, chore, or bug fix
starts by creating its own branch, cut from `dev` — except hotfixes, which are
cut from `main` as described below.

**Prefixes** — the conventional Git Flow set, nothing invented:


| Prefix              | Used for                                                           |
| ------------------- | ------------------------------------------------------------------ |
| `feature/`          | new functionality (`FEAT-###`)                                     |
| `task/` or `chore/` | maintenance, tooling, refactors, housekeeping (`TASK-###`)         |
| `bugfix/`           | defects found on `dev` (`BUG-###`)                                 |
| `hotfix/`           | urgent fixes cut from `main`, merged back to both `main` and `dev` |
| `release/`          | release stabilization branches                                     |


**Naming.** `<prefix>/<ID>-<short-kebab-description>` — the prefix and the
description are lowercase kebab-case, and the ID keeps the uppercase form it has
in `agile/`. For example `feature/FEAT-004-split-view` or
`bugfix/BUG-011-path-escape`. The ID is the same one used under Amendment 12, so
branch, work item, plan, and test plans all resolve to one another.

**One item, one branch.** A branch carries the work of a single item. Unrelated
changes discovered along the way become their own item and their own branch
rather than riding along.

Branches are created before the first edit, never after — including when the
agent has started work and only then notices it is on a protected branch.

## Amendment 14 — Git Flow, protected branches, PRs only

Projects follow Git Flow. Two branches are protected: **`main`** and **`dev`**.

- `main` holds released, production-ready state. Every commit on it is a release
point and carries a tag.
- `dev` is the integration branch. Completed work lands here first.

**Nothing is merged into a protected branch without a pull request.** No direct
commits, no direct merges, no fast-forward pushes, no force-pushes to `main` or
`dev` — regardless of how small the change is or how confident the agent is.

**Flow.**

1. Cut a branch from `dev` per Amendment 13.
2. Open a PR into `dev` when the work item is complete — code, docs under
 Amendment 11, and the `agile/` triplet under Amendment 12 all included.
3. Release: `dev` merges into `main` by PR, through a `release/` branch when
 stabilization is needed.
4. Hotfix: cut from `main`, PR into `main`, then PR the same fix back into `dev`
 so the branches do not diverge.

**Tags and releases.** Releases are tagged on `main` using semantic versioning
(`vMAJOR.MINOR.PATCH`), and every tag has release notes describing what changed.
Pre-releases built manually from `dev` under Amendment 15 carry a pre-release
version (`vMAJOR.MINOR.PATCH-alpha.N`) and are never counted as releases of
`main`. Tags are never moved or rewritten once pushed.

**Agent limits.** The agent creates branches and commits freely on its own
branch. Pushing, opening PRs, merging, tagging, and publishing releases are
outward-facing actions: the agent does them only when explicitly asked, and never
merges its own PR into a protected branch on its own initiative.

**Destructive Git operations count as deletion.** Some Git commands destroy work
without ever touching a delete call — `git reset --hard`, `git restore` or
`git checkout --` over local changes, `git clean`, `git stash drop`, branch or
tag deletion, and every form of force-push. Amendment 6 covers them by intent:
they are never run as routine cleanup and never without explicit approval in the
moment.

The safe equivalent is used wherever one exists — commit or stash rather than
reset, move a branch aside rather than delete it, and `--force-with-lease` rather
than `--force` when a force-push has been approved. Uncommitted work belonging to
the author is never discarded to make a command succeed; it is committed to a
scratch branch or stashed, and the author is told where it went.

## Amendment 15 — Release builds: automatic on `main`, manual on `dev`

The two protected branches build on different triggers.

**`main` — automatic.** Every merge into `main` triggers a release build. There
is no manual trigger and no opt-out: if it landed on `main`, it is released — the
only thing that can stop it is a failing gate, since Amendment 16 halts the
pipeline before the release stage. The build produces the tagged, versioned
release artifacts described in Amendment 14, along with its release notes.

**`dev` — manual.** Merges into `dev` do not trigger a release build. The
automatic checks defined in Amendment 16 still run on every merge, but they stop
before the build stage: producing a `dev` build and its alpha release is an
explicit, manually triggered action, run when someone wants a pre-release rather
than on every landing.

**Consequences the agent respects.**

- A merge into `main` is a publish. It is treated as outward-facing and
irreversible under Amendment 14: never initiated by the agent on its own.
- Anything that must not ship yet does not land on `main`. Staging happens on
`dev` or a `release/` branch.
- Release pipeline configuration is part of the repository and is documented in
`docs/` under Amendment 11: what triggers each build, what it produces, and
where the artifacts go.

## Amendment 16 — CI/CD: ordered gates

Every repository has a CI/CD pipeline, defined as a sequence of gates executed in
a fixed order. A gate that fails stops the pipeline; nothing downstream runs.

**The gates, in order.**

1. **License check** — every dependency's license is identified and permitted;
 the project's own license and attribution files are consistent with them.
2. **Code quality** — formatting, linting, static analysis, and type checking,
 across every language in the project. Amendment 7 is what this gate enforces
  mechanically.
3. **Tests and coverage** — the full test suite passes, and first-party coverage
 meets the Amendment 10 floor of 70%. Falling below the floor fails the gate.
4. **Security** — dependency vulnerability and advisory scanning for every
 package ecosystem in the project, plus secret scanning over the diff.
5. **Build** — the release build for every target platform.
6. **Release** — versioning, tagging, artifacts, and release notes.

**Branch behavior.**

- **`main`** — all six gates run automatically, in this order, on every merge.
Passing gate 6 publishes the release (Amendment 15).
- **`dev`** — gates 1 through 4 run automatically and then the pipeline stops.
Build and alpha release are triggered manually, by a human, when a pre-release
is wanted. `dev` never publishes on its own.

**Rules.**

- The order is fixed, cheapest and most-certain checks first, so an obvious
failure never burns a full build.
- Gates are blocking, not advisory. A red gate is fixed, not bypassed; skipping
or `continue-on-error` is not used to get a merge through.
- Every gate's result is visible on the pull request, since Amendment 14 makes
the PR the only path into a protected branch.
- Pipeline definitions live in version control alongside the code, and what each
gate runs is documented in `docs/` under Amendment 11.

**Candidate gates — proposed, not yet adopted.** These are recommendations
awaiting the author's decision; none is in force until moved into the list above.

- **Supply-chain provenance at release** — generate an SBOM and sign the
artifacts (build provenance attestation), so a shipped binary can be traced to
the commit that produced it. Slots between gates 5 and 6.
- **Artifact smoke test** — after gate 5, launch the built application and verify
it starts and performs one core operation. Catches the class of failure where
everything compiles and every unit test passes but the packaged app is broken.
- **Amendments compliance** — verify the PR's branch name carries a valid work
item ID and that the `agile/` triplet from Amendment 12 exists for it. Makes
the process rules self-enforcing rather than dependent on memory. Slots at
gate 0, before license check, since it costs nothing.
- **Commit and PR hygiene** — conventional-commit linting on titles and messages,
which is what makes automated release notes in gate 6 reliable.
- **Cross-platform build matrix** — where the project ships to more than one
platform or runtime, building only one target on `main` leaves the rest
unverified until a user finds the break. Expands gate 5 rather than adding a
gate.

**Tooling is per-project, not per-book.** These amendments state what each gate
must prove; they never name the tool that proves it. Each repository picks the
CI platform, linters, audit tools, coverage runners, and scanners native to its
own stack and records those choices in `docs/` under Amendment 11. A gate is
satisfied by its outcome, not by a particular vendor or command. The author's
default platform is GitHub Actions, and Amendment 17 assumes a GitHub remote;
where a project uses a different forge or runner, the equivalent tooling applies
and the gates and their order are unchanged.

## Amendment 17 — Use the installed CLIs for all version-control work

The machine has the Git CLI and the GitHub CLI installed and authenticated. Every
version-control and forge operation goes through them.

- **Git CLI** — branching, staging, committing, rebasing, tagging, inspecting
history, resolving conflicts.
- **GitHub CLI** — pull requests, reviews, issues, checks, releases, and anything
else that lives on the forge.

The agent uses these directly rather than guessing at repository state,
describing steps for the author to run by hand, or reaching for a different
mechanism when one of them would do the job. State is read, not assumed: branch,
status, diff, and PR state are checked before acting on them.

These CLIs are the means by which the earlier amendments are actually carried
out — branch creation and naming under Amendment 13, the PR-only path into
protected branches under Amendment 14, tags and releases under Amendments 14 and
15, and reading gate results under Amendment 16. Using them does not loosen those
rules: the limits in Amendment 14 on pushing, merging, tagging, and releasing
apply exactly the same when the command is available and would succeed.

## Amendment 18 — Session start: review open pull requests first

At the start of every fresh session on a repository, before taking on new work,
the agent checks the open pull requests and reports back.

**The report is brief** — a scan, not an audit. For each open PR:

- Number, title, author, and target branch.
- Age, and whether it is a draft.
- CI status: which gates from Amendment 16 passed, failed, or are still running.
- Review state: approved, changes requested, or awaiting review.
- Whether it is mergeable, or blocked by conflicts.

**It closes with what needs attention** — PRs that are green and waiting to
merge, PRs with failing gates, PRs stale enough to be at risk of conflict, and
any PR that overlaps the work about to start.

The agent reports; it does not act on what it finds. Merging, closing, or pushing
to someone else's branch stays subject to Amendment 14. If the repository has no
open pull requests — or no remote at all — that is stated in one line and the
session proceeds.

## Amendment 19 — Audio signals for states that need the author

The author is frequently away from the screen. A small set of states is therefore
announced with a sound, so that a state change carries into another room instead
of waiting silently on a terminal nobody is looking at.

**The states and their sounds.** Sound files live in `~/Dev/mywrok/AI_SOUNDS`;
the file name is the state.


| Sound                         | Played when                                                                                                                                              |
| ----------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `FINISHED.wav`                | the requested work is complete and nothing is waiting on the agent                                                                                       |
| `NEED_INTERACTION.wav`        | the agent needs the author to do something or answer something before it can go on — a decision, a yes or no, an action only the author can take         |
| `CALL_ME_FOR_QUESTIONARY.wav` | the agent has stopped to run an Amendment 2 questionnaire — several open points at once, work paused until they are answered                             |
| `CONFLICT.wav`                | work is blocked by a conflict: one Git cannot resolve on its own, or a request that conflicts with the project's existing architecture under Amendment 2 |
| `CODE_ORANGE.wav`             | the Amendment 9 second occurrence is declared                                                                                                            |
| `CODE_RED.wav`                | the Amendment 9 third occurrence is declared                                                                                                             |
| `RELEASE_MADE.wav`            | a release has been published under Amendment 15                                                                                                          |


**Discipline.**

- One sound per event, played at the moment the state is reached. The same event
never sounds twice, and sounds are never chained back to back.
- Sound accompanies the written report; it never replaces it. Every state that
makes a noise is also stated in the response, because the author may be out of
earshot, may have the volume down, or may read the session later.
- Ordinary progress is silent. These states are the whole list — routine steps,
successful commands, and intermediate results make no sound.
- `NEED_INTERACTION.wav` marks a real handover to the author, judged by the
agent: a question asked, a choice put to them, a step only they can perform. It
is not tied to the harness's own notifications — permission prompts, tool
dialogs, and idle notices are not this state and do not sound.
- Playing audio is not "taking the wheel" under Amendment 4: it moves no window,
steals no focus, and sends no input. It stays allowed by default.

**How it is played.** Playback is detached so it never blocks the work:

```
pw-play ~/Dev/mywrok/AI_SOUNDS/FINISHED.wav >/dev/null 2>&1 &
```

`paplay` is the fallback where `pw-play` is unavailable; any player that exits on
its own is acceptable. If playback fails or the machine has no audio, the agent
says so once in text and carries on — a missing sound never blocks work, and one
sound is never substituted for another.

## Amendment 20 — The sound catalogue is data, and stays in sync

The set of signals is a directory of files, not logic spread through the agent's
behavior. That keeps it extendable without touching anything else.

- One directory holds every sound: `~/Dev/mywrok/AI_SOUNDS`. Nothing plays from
anywhere else.
- The file name is the state, in `SCREAMING_SNAKE_CASE`, and says plainly what it
signals.
- A new signal is added by dropping a file in that directory and registering it
in the Amendment 19 table in the same change. A file that is present but
unregistered is never guessed at and never played.
- A registered file that has gone missing is a defect under Amendment 11's
staleness rule: the agent reports it rather than silently falling back to
another sound.
- Sound files are authored assets. Amendment 6 protects them — they are moved,
never deleted.

**Where the harness plays a sound itself.** Some of these states can be wired to
hooks in the agent harness, so the machine plays them without depending on the
agent remembering. Where such a hook exists, the agent does not also play that
sound — one event, one sound — and which states are hook-driven is recorded in
the machine's configuration, not here.

