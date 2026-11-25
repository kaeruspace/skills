---
name: doubt
description: Isolated adversarial review before committing or finalizing non-trivial changes. Use when changing branching logic or boundaries, asserting concurrency or ordering invariants, making irreversible changes, editing unfamiliar code, or claiming a non-obvious property.
---

# Doubt

Run an isolated adversarial review to disprove claims on non-trivial decisions before committing or finalizing changes.

## When to use

Use Doubt when a decision meets any of these conditions:

- It adds or changes branching logic or state transitions.
- It crosses module, service, network, or storage boundaries.
- It asserts an invariant the compiler or type system cannot check, such as concurrency, ordering, or idempotence.
- Its impact is irreversible, such as a schema migration, a public API change, or a production deploy.
- The author edits code without full understanding.
- The author claims a non-obvious property, such as safety, scale, or spec compliance.

Skip routine edits, renames, formatting, file reads, and test runs.

Run Doubt from the main session so Step 3 can spawn an isolated reviewer. Inside a subagent that cannot spawn another, escalate to the user or run a self-review of the artifact and contract and mark it degraded.

## The review cycle

### 1. State the claim

Write the decision and its failure risk in two lines:

```text
CLAIM: Expected behavior and scope.
RISK: Concrete failure mode if the claim is wrong.
```

If you cannot state the claim in two lines, clarify the decision before proceeding.

This step is complete when the claim and failure risk fit in two lines.

### 2. Extract artifact and contract

Isolate the review unit into two parts:

- **Artifact.** The isolated diff, function, or proposal. Keep it small enough to read in one pass. Decompose larger changes before review.
- **Contract.** Explicit constraints, requirements, and invariants the artifact must satisfy.

Include contradicting evidence such as callers, guards, or failing tests. Strip your own reasoning and history so the reviewer evaluates the artifact without bias.

This step is complete when the isolated unit contains only the artifact, the contract, and relevant evidence.

### 3. Run adversarial doubt

Invoke an isolated reviewer subagent or open a clean session. Pass only the artifact and the contract. Keep the claim and your rationale out of the prompt so the reviewer forms an independent judgment.

Use this prompt verbatim so it overrides any balanced summary default:

```text
Adversarial review. Find every flaw, unhandled edge case, and false assumption in this artifact under the contract.
Assume the author is overconfident. Look for:
- Unstated assumptions that fail
- Unhandled edge cases and boundary conditions
- Hidden coupling, shared state, or side effects
- Direct contract violations
- Broken conventions
- Failure modes under unexpected input or heavy load

Report concrete issues only, or state that thorough inspection found none. Do not summarize or validate strengths.

Artifact:
<paste artifact>

Contract:
<paste contract>
```

This step is complete when the reviewer returns an issues-only report or confirms that thorough inspection found no issues.

### 4. Reconcile findings

Treat reviewer output as raw data, not a final verdict. Re-read the artifact and check the codebase against each finding before deciding.

Classify every finding in this precedence order:

1. **Contract misread.** The reviewer flagged an issue because the contract was incomplete or ambiguous. Update the contract and re-run Step 3.
2. **Actionable defect.** The finding identifies a real flaw. Fix the artifact and repeat the cycle from Step 1.
3. **Conscious trade-off.** The finding is accurate, but fixing it costs more than accepting the limitation. Document the trade-off for the user.
4. **Noise.** The finding is false because the reviewer lacked context. Verify against the codebase, discard the finding, and check whether adding that context to the contract would prevent the false finding.

This step is complete when every finding has a verified classification and any actionable defect is fixed.

### 5. Stop conditions

End the loop when any of these conditions occurs:

- The reviewer returns only noise or trivial findings.
- Two or more cycles produce real findings with zero classified as actionable. Stop and escalate to the user.
- Three cycles finish without resolution. Stop and escalate the remaining issues to the user. If the artifact is too large for three cycles, return to Step 2 and decompose the artifact instead of running a fourth.
- The user accepts the artifact.
