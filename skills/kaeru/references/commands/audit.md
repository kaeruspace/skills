# Kaeru Command: `audit`

Codebase & context health audit, drift detection, and dead-weight pruning.  
Triggered via `/kaeru audit`.

---

## 1. Audit Workflow
1. **Map vs. Reality**: Compare `git ls-files` and manifests against `SYSTEM.md`. Flag unmapped files or ghost entries.
2. **Subtractive Scan**: Review Section 5 (Reusable Primitives). Detect duplicate helpers and dead weight.
3. **Audit Report**:
   ```markdown
   ### KAERU AUDIT REPORT
   - Context Health: [SYNCED | DRIFT DETECTED] (<unmapped> / <ghosts>)
   - Bloat Score: [LEAN | MODERATE BLOAT | SEVERE ACCRETION]
   - Dead Weight Candidates: <paths to prune>
   - Decision Invariants: [All active | <stale count> flagged]
   ```
4. **Emit Prune Prompt**: If dead weight exists, emit single-task prompt directly into chat.

---

## 2. Single-Task Prompt: `audit: prune` (Emitted Directly into Chat)

```markdown
# TASK: audit: prune — Dead Code & Accretion Elimination
[Target Files]: [relative paths of files to be pruned or consolidated]
[Subtractive Anchor]: Delete <deprecated paths>; Consolidate <duplicated helpers>
[Net LOC Budget]: Net LOC < 0 (Negative delta strictly required, verify via git diff --stat)
[Not-Doing]: Zero new feature logic or styling changes allowed.

[Assigned Skills]:
- Primary: @ponytail-audit
- Guard: @doubt-driven-development
- Invariant: @full-output-enforcement (zero stubs, complete drop-in deletion)

Read: SYSTEM.md, DECISIONS.md, AGENTS.md rules.
Objective: Prune dead weight and eliminate duplicate code with zero regression.

Protocol (Follow AGENTS.md strictly):
1. INSPECT & REALITY CHECK: Verify target code is unreferenced. Run tests before editing. Emit [REALITY CHECK: CLEAN] or [REALITY CHECK: PIVOT].
2. BLUEPRINT: Print 5-line [BLUEPRINT] to chat and execute immediately.
3. EXECUTE: Remove targeted dead code. Update call sites to canonical primitives. FORBIDDEN: Net positive LOC, leaving dead imports or orphan types.
4. VERIFY & COMMIT: Verify Net LOC < 0 via `git diff --stat`. Prune deleted files from SYSTEM.md. Commit: audit(prune): <summary>. Escalate only on FAIL or PAUSE.
```
