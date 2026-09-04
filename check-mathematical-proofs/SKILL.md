---
name: check-mathematical-proofs
description: Audit mathematical proofs, proof attempts, derivations, and solution arguments for local and global correctness. Use when asked to check, verify, critique, referee, or debug one or more mathematical proofs, especially for reversed or unjustified inequalities, misapplied theorem hypotheses or conclusions, undefined concepts or unsupported results, silently added assumptions, quantifier or domain errors, missing logical bridges, circular reasoning, goal mismatch or irrelevant-but-correct reasoning, edge cases, or dependency failures. Treat separate proofs as independent unless explicitly linked, distinguish proof-critical errors from removable redundant branches, judge internal logical consistency rather than conformity to a standard method, and report localized errors with brief repair attempts instead of writing a complete replacement proof unless requested.
---

# Check Mathematical Proofs

## Core mandate

Audit the submitted argument, not its resemblance to a familiar solution. Use standard proofs, workspace conventions, and known methods only as diagnostic references. Accept any route whose stated assumptions support every inference.

Default to error localization and minimal repair. Do not supply a complete corrected proof unless the user explicitly asks for one.

When several proofs are supplied, restart the audit for each proof. Do not let an earlier proof, shared intended idea, or later proof silently fill a gap in another proof. Allow cross-proof dependencies only when the proof explicitly invokes them and they are available in the stated context.

## Build the audit baseline

Before judging a step, record the following semantic ledger:

1. State the exact claim being proved, including domains and parameter ranges.
2. List only the hypotheses actually given.
3. Preserve the order and dependence of all quantifiers.
4. Record definitions and previously established results that the proof may use.
5. Identify the intended conclusion and its required strength.

Do not strengthen a hypothesis, weaken the conclusion, or reinterpret notation to rescue the proof. If the problem statement or surrounding context is ambiguous, state the interpretation used and explain whether the verdict changes under another natural interpretation.

If an exact cited theorem or definition is needed, verify it from the provided context or an accessible source. If verification is unavailable, mark the application as `needs source verification`; do not invent a statement and do not automatically call the mathematical claim false.

## Run the goal-alignment gate

Before inspecting local proof details, temporarily grant every claim made in the submitted argument and ask whether the resulting chain would prove the exact target theorem.

1. Expand the target into its actual proof obligations, including cases, domains, quantifiers, and required strength.
2. Identify the argument's actual terminal claim rather than inferring what the author intended.
3. Trace an explicit implication path from the argument's claims to every proof obligation.
4. Compare the terminal claim with the target for direction, strength, scope, and quantifier order.
5. Mark claims that lie on no apparent path as provisionally unused. Confirm redundancy only during the second goal-alignment check, after local validity is known.

If no adequate implication path exists, record a `TARGET` issue before the detail audit. State whether the argument proves a different claim, a weaker claim, a special case, only a necessary condition, or merely a collection of unrelated truths. Accept indirect routes and supporting lemmas when the proof supplies a valid bridge to the target. Continue the detail audit even after this gate fails so that independent local errors are still reported.

Never assign a correct verdict when the goal-alignment gate fails, even if every sentence in the argument is true.

## Audit every dependency

Break the proof into atomic claims, equations, and inference steps. For each nontrivial transition, identify:

- the premises used;
- the rule, definition, theorem, or calculation invoked;
- the resulting claim;
- the later step that depends on it.

Audit in both directions: follow the submitted inferences forward, then trace backward from the exact conclusion to confirm that every proof obligation has been discharged.

Reconstruct omitted intermediate reasoning at high-risk transitions. A phrase such as “clearly,” “similarly,” “standard,” or “it follows” is not itself a justification. Treat a skipped step as harmless only when the missing bridge is routine, valid under the existing hypotheses, and can be stated locally without adding a new idea.

Use a symbolic check, limiting case, equality case, or small counterexample when useful, but do not substitute a heuristic test for a proof-level justification.

Do not stop at the first error. When practical, provisionally grant a failed step and inspect the remainder for independent errors. Distinguish new errors from downstream statements that fail only because an earlier premise failed.

During this detail audit, judge every step's local correctness even when it appears unused. Treat its effect on the target verdict as provisional until the second goal-alignment check. Suspected redundancy is not a reason to skip or excuse a local error.

## Apply the targeted checks

### Goal alignment and relevance (`TARGET`)

Flag any shift from the stated target to another conclusion. Treat a plausible but missing final bridge as both `TARGET` and `GAP`; treat an argument whose terminal claim is genuinely unrelated or insufficient as a fatal `TARGET` failure. If a complete valid proof core exists and only additional material is off-path, classify that additional material under the final redundancy check rather than treating the whole proof as a `TARGET` failure.

### Inequalities and estimates (`INEQ`)

Check both the truth and the usefulness of every bound.

- Track direction when multiplying or dividing by a quantity of unknown or negative sign.
- Check reciprocal, negative-power, monotone-decreasing, squaring, square-root, and absolute-value transformations with their domain and sign conditions.
- Check whether integration, summation, expectation, limits, limsup/liminf, norms, or extrema preserve the asserted direction.
- Check coefficient signs, constant dependence, equality cases, and whether a denominator may vanish.
- Check that an upper bound is not later used as a lower bound, or vice versa.
- Check that the estimate is strong and uniform enough for the conclusion, especially when parameters tend to a limit.

### Theorem and lemma use (`THM`)

Compare the application with the exact result, not with a remembered slogan.

- Verify every hypothesis: domain, regularity, measurability, integrability, compactness, completeness, boundary conditions, parameter ranges, exceptional sets, and independence assumptions when relevant.
- Verify that the objects in the proof match the theorem's objects.
- Verify the direction of implication; do not use a converse, contrapositive, uniqueness claim, or equality case that the theorem does not provide.
- Check whether the theorem gives pointwise, almost-everywhere, local, global, weak, strong, uniform, or merely subsequential information.

### Definitions and support (`DEF/SRC`)

Require every material symbol and concept to be defined by the problem, context, or proof. Require every non-elementary imported conclusion to be stated clearly enough or identified well enough to verify.

Distinguish:

- an undefined or ambiguous expression;
- a missing citation or unverifiable imported result;
- a cited result that does not imply the claimed statement;
- a claim that is demonstrably false.

Do not collapse these into one accusation.

### Added assumptions and invalid reductions (`ASSUMP`)

Detect properties introduced without derivation, including positivity, nonvanishing, boundedness, smoothness, compactness, connectedness, genericity, normalization, or attainment of an extremum.

Reject “without loss of generality” unless a valid symmetry, relabeling, normalization, or exhaustive case reduction is supplied. If a repair needs a new assumption, state it as a conditional repair and note that it changes the original claim.

### Quantifiers and logical scope (`QUANT`)

Write out the quantifier structure when dependence matters.

- Distinguish arbitrary from fixed objects and universal claims from existence claims.
- Track which witnesses or constants may depend on which variables.
- Detect swapped quantifiers, missing uniformity, illicit choice of a witness, and reuse of a witness outside its scope.
- Check negations exactly, including `not for all` versus `for all not`, and `not exists` versus `exists not`.
- Distinguish everywhere, almost everywhere, densely, eventually, and along a subsequence.

### Missing bridges (`GAP`)

Inspect especially carefully when the proof moves through:

- existence or uniqueness assertions;
- convergence and interchange of limits with sums, integrals, derivatives, expectations, or optimizations;
- pointwise-to-uniform, local-to-global, weak-to-strong, or almost-everywhere-to-everywhere conclusions;
- compactness, closure, density, approximation, diagonal, subsequence, or selection arguments;
- boundary or degenerate cases, equality cases, zero denominators, and endpoint parameters;
- induction bases, case exhaustiveness, cancellations, and changes of variables.

Attempt to state the smallest missing lemma or calculation. If that bridge cannot be justified from the existing ledger, report a real gap rather than silently completing it with a new assumption or major idea.

### Circularity and dependency order (`CIRC`)

Trace a dependency graph for the main claim and supporting lemmas. Flag a step when it uses:

- the desired conclusion itself;
- an equivalent reformulation whose equivalence already needs the conclusion;
- a later lemma that depends on the current result;
- a minimality, maximality, or contradiction premise that has not been established.

Do not label mere reuse of an earlier independent lemma as circular.

### Other correctness failures (`OTHER`)

Report material algebraic or computational errors, ill-defined operations, missing cases, or confusion of necessary and sufficient conditions even when they do not fit the priority categories. Give a specific subtype such as `CALC`, `DOMAIN`, or `CASE`.

## Perform a global pass

After the local audit, repeat the goal-alignment gate using only validated steps and explicitly accepted local repairs. Trace backward from the exact target and confirm that the surviving argument discharges every proof obligation. Do not let the quantity, correctness, sophistication, or topical similarity of unused material substitute for this implication check.

### Certify redundant material (`REDUNDANT`)

First identify at least one complete, validated proof core that establishes every part of the exact target. Do not certify any material as redundant before such a core exists.

Apply this deletion test to each candidate passage or branch:

1. Remove the candidate and every later statement that depends exclusively on it.
2. Use only the remaining argument as submitted; do not add a new lemma, assumption, repair, or proof idea.
3. Recheck every target obligation.
4. Certify the candidate as `REDUNDANT` only if a complete validated proof core still remains.

Classify its role precisely:

- `essential`: removing it leaves some target obligation unsupported;
- `alternative`: it belongs to a target-relevant route, but another independent validated route remains;
- `redundant-unrelated`: it lies on no valid route to the target;
- `redundant-failed-branch`: it contains a local error, but a separate validated route proves the target without it;
- `undetermined`: the dependency structure is too ambiguous to certify deletion.

An erroneous step may be called redundant even when later steps cite it only if its entire dependent branch can be deleted, or the cited conclusion already follows from other valid submitted premises without it. If deleting the step requires repairing it, replacing the method, adding a hypothesis, or proving something new, it is not redundant. Never assume an erroneous step or its proposed repair to certify redundancy.

Do not treat two branches as independent when they share an invalid premise. Do not use one separately presented proof version to rescue another; the rule that different proofs are independently audited still controls. Within one proof, if two complete valid routes are supplied, describe them as alternative routes rather than calling either one irrelevant.

Keep local correctness and target impact separate. Retain every local error found in certified redundant material, but mark its target impact as `none`. Such an error does not lower the overall verdict when the remaining proof core is complete and valid.

After the local audit, check that:

- all cases are covered and their scopes do not overlap incorrectly or leave a gap;
- locally valid steps compose to the claimed conclusion;
- no hypothesis or defined object changes meaning midway;
- all proof dependencies are available and acyclic;
- the final statement has exactly the requested quantifiers and strength.

Recheck every proposed local repair against the same ledger. Do not allow the repair to introduce a hidden condition, quantifier change, or circular dependency.

Distinguish a false conclusion from an invalid proof of a possibly true conclusion. Judge only what the audit establishes.

## Report the audit

Match the user's language. For each proof, report findings in proof order using short anchors such as an equation, sentence fragment, or step number.

Use this structure:

1. **Overall verdict** — choose one:
   - `Correct`: a complete validated proof core establishes the target. Certified redundant material, including locally erroneous redundant material, does not lower this verdict.
   - `Correct with minor clarification`: only locally fillable omissions remain in the proof core, using facts and hypotheses already present.
   - `Material gap`: a necessary bridge or imported result is unproved or unverifiable, but no decisive false inference has been established.
   - `Incorrect`: no complete valid proof core remains because a required inference fails or the argument does not establish the stated target.
   - `Insufficient context`: missing statement, definitions, or source material prevents a meaningful overall judgment.
2. **Findings** — for every issue, give:
   - `Location`: the smallest unambiguous anchor;
   - `Type`: one or more of `TARGET`, `INEQ`, `THM`, `DEF/SRC`, `ASSUMP`, `QUANT`, `GAP`, `CIRC`, or `OTHER` with a subtype;
   - `Severity`: `fatal`, `major`, `minor`, or `needs verification`;
   - `Role`: `essential`, `alternative`, `certified redundant`, or `undetermined`;
   - `Problem`: the exact failed inference and why it does not follow;
   - `Local repair`: a brief correction, missing condition, or smallest lemma to prove. Say when no local repair is available.
   - `Target impact`: `fatal`, `material`, `minor`, or `none`; identify the affected range without repeating derivative failures.
3. **Redundant material** — when present, list each certified redundant passage, the deletion-test basis, and any local error it still contains. State explicitly that its target impact is `none`.
4. **Global assessment** — explain in a few sentences whether the validated proof core establishes the claim and whether any reported errors occur only in certified redundant material.

Do not manufacture findings to populate every category. When no substantive issue is found, say which high-risk checks were performed and avoid claiming infallibility. Keep style suggestions separate from correctness findings.

List all independent substantive errors found. Group purely derivative failures under the root issue rather than inflating the finding count.

Base the overall verdict only on the validated proof core. Never hide or relabel a local error merely because it is redundant, and never downgrade an otherwise correct target proof solely because certified redundant material is false or invalid.

For multiple proofs, repeat the full structure for each proof and give each an independent verdict. Add a cross-proof comparison only if the user asks for one.
