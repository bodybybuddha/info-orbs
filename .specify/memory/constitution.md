<!--
Sync Impact Report
- Version change: 2.1.1 → 2.2.0
- Modified principles:
	- (new) "Device Reliability" added as Principle I
	- (new) "Reproducible Builds & Config Safety" added as Principle II
	- (new) "Test-First Evidence" added as Principle III (clarified TDD expectations)
	- (new) "Observability & Privacy" added as Principle IV
	- (new) "Modularity & Simplicity" added as Principle V
- Added sections:
	- "Constraints & Compliance" (Section 2)
	- "Development Workflow" (Section 3)
- Removed sections: none
- Templates requiring updates:
	- `.specify/templates/plan-template.md` ✅ updated
	- `.specify/templates/spec-template.md` ⚠ pending (review for mandatory sections alignment)
	- `.specify/templates/tasks-template.md` ⚠ pending (review task categories vs new principles)
- Follow-up TODOs:
	- TODO(RATIFICATION_DATE): original ratification date not found; please supply
	- Manual review: agent-specific references in templates (e.g., CLAUDE/copilot) may need generic wording
-->

# Info Orbs Constitution

## Core Principles

### Device Reliability (I)

Every firmware release MUST prioritize user safety, device stability, and predictable
behaviour in constrained environments. Rules: firmware MUST fail-safe on errors,
recoverable configuration MUST be supported (factory-reset path), and runtime
resource usage (memory, CPU) MUST be bounded and documented for each widget.
Rationale: physical devices interact with users and power/hardware; reliability is
non-negotiable and testable through watchdogs, integration tests and manual smoke
tests.

### Reproducible Builds & Config Safety (II)

Builds MUST be reproducible and configuration entry points MUST be explicit.
Rules: the repository MUST provide `config.h.template`; building MUST not depend on
untracked local files. All release artifacts MUST include build metadata (PlatformIO
env, commit SHA, date). Rationale: reproducible builds reduce debugging time and
support reproducible bug reports from users.

### Test-First Evidence (III)

Critical behavior MUST be captured by automated tests before code implementation
where practical. Rules: unit tests for pure logic, contract tests for I/O formats,
and integration tests (including hardware-in-the-loop where available) for device
flows. Tests MUST be executable in CI and MUST fail before implementation tasks
are merged. Rationale: TDD reduces regressions and documents expected behaviour.

### Observability & Privacy (IV)

Firmware and companion tools MUST provide structured logs (levels: ERROR/WARN/INFO/DEBUG)
and runtime diagnostics accessible to developers. Telemetry is allowed only when
opt-in and MUST comply with licensing and privacy requirements (AGPLv3 compliance
and user consent). Rationale: observability enables faster diagnosis while
protecting user privacy and legal compliance.

### Modularity & Simplicity (V)

Design MUST favour small, well-documented modules (widgets, drivers, utilities)
over large monoliths. Rules: new functionality SHOULD be implemented as a
separable module with clear public API, assets (images/fonts) MUST include source
or license records. Keep interfaces minimal (YAGNI) and prefer readability over cleverness.
Rationale: modularity improves maintainability and enables community contributions.

## Constraints & Compliance

The project is an embedded firmware project built with PlatformIO and distributed
under the GNU Affero General Public License v3.0 (AGPLv3). Rules:

- All releases MUST include a copy of `LICENSE.txt` and attribution for bundled fonts/images.
- Platform constraints: memory and CPU usage for widgets MUST be documented in the
  widget README and enforced by CI checks where possible.
- Configuration and secret handling: no secrets (API keys, passwords) MUST be
  committed to the repository. CI and release processes MUST validate this.

## Development Workflow

Branching & Reviews:

- Primary branches: `main` (stable), `dev` (active development). Feature work
  SHOULD be performed on descriptive feature branches and submitted as PRs.
- PRs MUST include a short description, testing steps, and link to related spec/plan.
  Code Quality & CI:
- Automated checks (build, unit tests, lint) MUST pass on PRs before merge.
- Tests required: unit tests for logic, integration/contract tests for widgets and
  data flows. Hardware-specific integration tests SHOULD be documented and run
  manually or in a hardware lab when CI is not available.

## Governance

Amendments:

- Changes to this constitution MUST be proposed as a PR against `.specify/memory/constitution.md`.
- A major governance change (removal or redefinition of a principle) MUST be
  approved by the project maintainers and document a migration plan. Approval
  requires at least two maintainer reviews or explicit owner approval.

Versioning & Releases:

- The constitution follows semantic versioning `MAJOR.MINOR.PATCH` for governance
  text. Bump rules:
  - MAJOR: Backward-incompatible governance change (principle removals or redefinition).
  - MINOR: Add or materially expand principles or sections (this change: 2.1.1 → 2.2.0).
  - PATCH: Clarifications, typos, or non-semantic refinements.

Compliance Reviews:

- PRs that modify behaviour constrained by this constitution (tests, licensing,
  reproducible builds) MUST include a short compliance checklist in the PR body.

**Version**: 2.2.0 | **Ratified**: TODO(RATIFICATION_DATE): original ratification date unknown | **Last Amended**: 2025-09-20
