# Doubt

Language models agree with user proposals by default and validate flawed premises with polite praise. **Doubt** does the opposite. It runs an in-flight adversarial review biased to disprove claims before non-trivial changes take effect.

## When to Use

- **Non-trivial architecture, state transitions, or boundary crossings.**
- **Invariants compilers cannot verify**, such as concurrency, ordering, or idempotence.
- **Irreversible changes**, such as schema migrations, public APIs, or production deployments.
- **Any confident assertion** cheaper to cross-examine now than to debug later.

## The Review Cycle

Run `@doubt` on any non-trivial proposal, plan, or code diff.

1. **State the claim**: Define the expected behavior and concrete operational risk in two lines (`CLAIM` & `RISK`).
2. **Extract artifact and contract**: Separate the isolated diff or proposal from its explicit constraints, stripping all author rationalizations.
3. **Run adversarial doubt**: Prompt an isolated reviewer to find flaws under the contract without seeing the author's claim or reasoning.
4. **Reconcile findings**: Classify findings strictly by precedence order (`Contract misread` → `Actionable defect` → `Conscious trade-off` → `Noise`).
5. **Stop**: Finish on clean findings, user approval, or three bounded cycles maximum before escalating to the user.

### Install Doubt

```bash
npx skills add kaeruspace/skills -y
```
