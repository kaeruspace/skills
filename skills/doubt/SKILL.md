---
name: doubt
description: Adversarial review for non-trivial decisions, plans, and code. Disproves assumptions using an isolated reviewer before changes take effect.
---

# Doubt

Context turns assumptions into accepted facts over long sessions. High confidence does not guarantee correctness. Doubt runs an in-flight adversarial review to disprove claims before non-trivial changes take effect.

## When to use

Use Doubt when a decision is non-trivial:
- Branching logic or state transitions change.
- Code crosses module, network, or storage boundaries.
- Logic asserts invariants that compilers cannot check, such as concurrency, ordering, or idempotence.
- Blast radius is irreversible, such as schema migrations, public API updates, or production deployments.
- The author edits code without full understanding.

Skip Doubt for routine operations:
- File renames, formatting, or moves.
- Straightforward edits following clear user instructions.
- File inspections and summaries.
- Low-risk edits verified by direct tests.

## The review cycle

### 1. State the claim
Write the decision and its operational risk in two lines:
CLAIM: Expected behavior and scope.
RISK: Concrete failure mode if this claim is wrong.

If you cannot state the claim in two lines, clarify the decision before proceeding.

### 2. Extract artifact and contract
Isolate the work into two components:
- Artifact. The isolated diff, function, or proposal. Keep the size small enough to read in one pass. Decompose larger changes before review.
- Contract. Explicit constraints, requirements, and invariants the artifact must satisfy.

Strip all personal reasoning, history, and justification. Author rationalizations bias the reviewer toward agreement.

### 3. Run adversarial doubt
Invoke an isolated reviewer subagent or open a clean session.

Pass only the artifact and the contract. Never pass the claim or internal rationale. The reviewer must evaluate the material independently.

Use this prompt:

```
Adversarial review. Find every flaw, unhandled edge case, and false assumption in this artifact under the contract.
Assume the author is overconfident. Look for:
- Unstated assumptions that fail
- Unhandled edge cases and boundary conditions
- Hidden coupling, shared state, or side effects
- Direct contract violations
- Broken conventions
- Failure modes under heavy load or invalid input

Do not summarize. Do not validate strengths. Report concrete issues only, or state that thorough inspection found none.

Artifact:
<paste artifact>

Contract:
<paste contract>
```

### 4. Reconcile findings
Reviewer feedback is raw data, not a final verdict. The reviewer lacks broader context. Re-read the artifact against each finding before deciding.

Classify every finding in this precedence order:
1. Contract misread. The reviewer flagged an issue because the contract was incomplete or ambiguous. Update the contract and re-evaluate.
2. Actionable defect. The finding identifies a real flaw. Fix the artifact and repeat the cycle.
3. Conscious trade-off. The finding is accurate, but fixing it costs more than accepting the limitation. Document the trade-off explicitly for the user.
4. Noise. The finding is incorrect because the reviewer lacked relevant context. Verify the codebase, then discard the finding.

### 5. Stop conditions
End the loop when any of these conditions occurs:
- The reviewer returns only noise or trivial findings.
- Three cycles finish without resolution. Stop and escalate the remaining issues to the user. Do not run a fourth cycle alone. Three unresolved cycles indicate the artifact is defective or too large.
- The user accepts the artifact.

## Operational traps

- Leaking the claim. Sending the claim or author rationale to the reviewer primes it to agree.
- Doubt theater. Completing two or more cycles with real findings without marking any finding as actionable.
- Rubber-stamping. Accepting reviewer findings without verification against the codebase.
- Post-hoc doubt. Running review after committing code. Doubt is an in-flight check, not a pull request gate.
- Over-reviewing. Running Doubt on trivial edits. Reviewing routine edits wastes time and slows delivery.
