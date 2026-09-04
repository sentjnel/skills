---
name: manage-manual-review-interventions
description: "Maintain staged human-review interventions for mathematical or technical manuscripts, including authoritative numbered opinion logs, read-only discussion, confirmed logic changes, ordered unified merges, validation, version freezing, and task handoffs. Use when Codex resumes a review from handoff/opinion/main files, the user says 写入修改意见 or 统一合并, gives a definite simple correction to record without confirmation, discusses a proof or source issue that should be recorded only after confirmation, or requires a handoff before context compaction."
---

# Manage Manual Review Interventions

Use a staged workflow that separates discussion, the auditable opinion record, and the authoritative manuscript. Preserve provenance and never let a tentative discussion silently become a manuscript edit.

## Establish the review state

1. Identify the authoritative handoff document, current opinion document, main manuscript, current version, and frozen archives.
2. Read the files completely in this order unless the project explicitly gives another order:
   1. handoff document;
   2. current opinion document;
   3. current main manuscript.
3. Read version indexes or source reports after those three when they affect the request.
4. Treat archived opinions as history. Do not repeat, copy back, or re-execute already merged items.
5. Default to read-only review. Do not edit the main manuscript, PDF, research progress files, lemma files, version index, or frozen archives without the corresponding authorization.
6. State only that the review is ready when the user requested an orientation-only response.

## Classify each user message

Classify the request before editing anything.

### Definite simple correction

Treat a local, mechanical instruction in definite language as authorization to append a new opinion directly to the current opinion document. Do not ask for confirmation.

Typical cases include:

- renaming or deleting one symbol;
- replacing a notation everywhere in a bounded proof;
- spelling out one definition or equality;
- changing one phrase without altering the proof strategy;
- adding an already specified pointwise estimate or domain qualifier.

Apply this rule only when an authoritative opinion document has already been established for the review. Record the instruction; do not modify the main manuscript unless the user also explicitly authorizes a unified merge.

### Logical, mathematical, organizational, or source issue

Discuss and analyze the issue read-only first. Do not record an open question, tentative diagnosis, or unresolved alternative as an agreed modification.

Write a new opinion only after the resolution is confirmed. Count any of the following as confirmation:

- the user explicitly says to write or record the agreed modification;
- the user selects one of the discussed resolutions;
- the user gives a fully specified directive after the consequences have already been discussed.

Do not treat a bare question such as “how is this obtained?” or “can this be simplified?” as confirmation. If a direct substantive directive changes theorem scope, source attribution, dependency order, or proof strategy and its consequences have not been established, explain the consequences before recording it.

### Read-only question

Answer from the authoritative manuscript and current opinion state. Localize the exact logical bridge requested. Do not broaden the edit, update the opinion log, or change files unless the user authorizes it.

### Unified merge

Modify the main manuscript only after an explicit instruction such as “统一合并”, “统一合并进 TeX”, or an equally clear authorization to apply the pending opinions to the main document.

## Maintain the opinion document

1. Locate the current version-specific opinion document. Do not create a competing list when one already exists.
2. Determine the next number from the actual headings in the file, not from memory or a stale handoff summary.
3. Keep the document header and status paragraph current. After appending an opinion, update the pending range or count and the next opinion number; never leave “no pending items” above a nonempty pending list.
4. Append only genuinely new opinions. Preserve earlier items as an audit trail.
5. Give each opinion:
   - a concise title;
   - an exact location by theorem, equation, paragraph, or stable text;
   - the agreed change;
   - any required formula, quantifier, domain, or dependency;
   - a statement of what remains unchanged when scope could be misunderstood.
6. Record a later correction as a new opinion instead of silently rewriting an earlier one. State which earlier item it supersedes when necessary.
7. Give later opinions higher priority when two pending items conflict.
8. Keep the main manuscript and generated PDF unchanged while only maintaining opinions.
9. After a successful unified merge, archive the complete pre-reset opinion document. Then reset the working opinion document to the new version baseline and follow the project convention for restarting or continuing numbering.

Read [document-templates.md](references/document-templates.md) when creating, resetting, or repairing an opinion document.

## Perform a unified merge

### Preflight

1. Re-read the complete opinion document and current main manuscript.
2. Identify unrelated user changes and preserve them.
3. Build a resolution map from every pending opinion to its target text and expected verification evidence.
4. Resolve overlaps by giving later opinions higher priority.
5. Preserve frozen versions. Never edit an existing frozen archive.
6. Keep source interfaces marked open unless direct verification actually closes them.

### Apply changes in the required order

Apply all pending changes in this order, even if the opinion numbers are interleaved:

1. proof logic details;
2. article organization;
3. symbols and notation.

Within each stage, apply later opinions before relying on superseded wording.

For proof logic details:

- verify exact hypotheses, domains, quantifiers, signs, scaling, and dependency order;
- distinguish a local clarification from a change in theorem strength;
- use the mathematical proof-audit skill when available and relevant;
- keep external-source attribution honest and separately identify independently derived conclusions.

For article organization:

- move, combine, split, or delete results only after the proof chain is stable;
- update prose dependencies and cross-references by content rather than old equation numbers;
- delete labels and references made obsolete by the reorganization.

For symbols and notation:

- perform mechanical renaming only after logical and structural edits settle;
- preserve symbols explicitly reserved elsewhere;
- search the final manuscript for stale aliases and mixed notation.

Use `apply_patch` for manuscript and review-document edits. Do not mutate unrelated Progress, Lemma, source-report, or archive files unless the user explicitly put them in scope.

### Audit the merged manuscript

1. Perform a forward audit from every opinion to the final text.
2. Perform a reverse audit using only the final manuscript, checking that:
   - no pending instruction was missed;
   - no superseded wording remains;
   - no deleted label, section, or symbol survives;
   - no new proof dependency became circular or undefined.
3. Check duplicate labels, undefined references, undefined citations, and stale tokens mechanically where possible.
4. Re-read proof-critical transitions independently of the opinion wording.

### Validate and freeze

For a LaTeX manuscript, after the last manuscript edit:

1. identify the authoritative independent compilation entry; if the target is only a fragment, report the limitation and never present a temporary wrapper build as the final manuscript build;
2. run pdfLaTeX twice in sequence on the authoritative entry;
3. inspect the final log for errors, warnings, overfull or underfull boxes, undefined references, and undefined citations;
4. extract the complete PDF text and check key additions, placeholders, and stale status text;
5. render every page and visually inspect every page for clipping, overlap, missing glyphs, and uncompiled formulas;
6. compute hashes after all final edits;
7. create a new version archive only when the request or established project convention authorizes it;
8. copy the exact merged opinion record and updated handoff into the new archive;
9. verify the root TeX and PDF are byte-identical to the archived copies;
10. update the version index without rewriting prior frozen versions.

Do not count exploratory or pre-final builds as the required final two builds.

## Hand off before a second context compaction

Treat an automatic conversation summary or context compaction as a compression event. Track the count for the current logical task.

After detecting the first compaction, perform a handoff checkpoint at the next safe boundary before substantial further work. This guarantees that the task is handed off before a second compaction. If the count is uncertain, assume one compaction has already occurred and hand off early.

At the checkpoint:

1. stop mutations at a recoverable state;
2. do not mark unfinished work complete;
3. write or update the authoritative handoff document;
4. record the exact current task objective, authoritative paths, read order, version and hashes when known, completed work, pending work, accepted decisions, unresolved issues, source boundaries, files changed, validation already run, validation still required, restrictions, and the exact next action;
5. record the next opinion number and whether pending opinions have been merged;
6. include a self-contained prompt that a new task can use without relying on hidden conversation context;
7. end the user-facing response with a directly copyable prompt in a fenced `text` block.

If the task finishes safely before a handoff is needed, complete it normally. If the user requests a handoff earlier, perform it immediately.

Read [document-templates.md](references/document-templates.md) before creating or substantially rewriting a handoff document.

## Preserve the user-facing compatibility rule

Until the user explicitly revokes it, apply these rules to page replies and copyable prompts:

- do not use Markdown bold or italic emphasis;
- avoid formatting that renders user-facing prose as emphasized text;
- place every mathematical formula on its own display line;
- do not use inline TeX delimiters in page replies;
- keep the final response self-contained because commentary may be collapsed.

Apply these compatibility rules to user-facing messages, not automatically to the manuscript's own typesetting conventions.
