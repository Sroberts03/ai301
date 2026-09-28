# Rubric: is this reproduction package ready to post?

Six required checks, one per way a package gets posted before it should
have been, plus two preferred checks that describe quality without
gating it. Every pass condition judges the thing itself: what the
artifacts show, what the words claim, what the repo asks for. None of
them counts steps, measures length, or looks for headings.

`references/evidence-guide.md` holds the map each Evidence cell points
at; its family headings are named below in **bold**.

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| `env-recorded` | The environment record wherever it appears in the candidate repro report (lead line, trailing line, or table) plus any version named in the candidate claim comment, read against the issue's own version statement and the axes the issue or thread calls relevant. See **Environment**. | The record names the version of the thing under test and every platform fact the issue's symptom turns on (OS and build, shell, browser, driver, backend, build profile), AND the versions tested are the ones the issue targets or the report itself states the difference. A record that is absent, or that silently tests a version the issue does not target, fails. | required |
| `steps-rerunnable` | The numbered steps, command blocks, and input or config snippets in the candidate repro report, read against the reporter's steps and trigger example in the issue. See **Steps**. | A stranger with only the repo and this comment could re-run the attempt: the starting state is recoverable from the text (shown inline, produced by a shown command, taken from the issue, or described specifically enough to rebuild), the commands or actions are given in order, and the issue's trigger appears as the issue writes it. Steps that depend on an unshared repo or config, omit setup the issue names as essential, or substitute a near variant for the trigger fail. | required |
| `artifact-shows-issue-behavior` | The output excerpts, transcripts, logs, and produced files in the candidate repro report, read against the issue's own error text and expected-versus-actual blocks, narrowed by any maintainer statement in the thread highlights. See **Behavior shown**. | At least one shown artifact carries the issue's named symptom: the same error string, exit status, code path, or missing or wrong output. A run of the issue's own scenario that does not produce the behavior also passes, when the report reports that negative result as its outcome. Artifacts that only show the tool running or the setup being ready, that show an adjacent symptom (a graceful error where the issue reports a panic, garbled output where the issue reports a dead process), or that are described rather than shown, fail. | required |
| `claims-match-evidence` | The confidence words in the candidate claim comment and in the report's summary or conclusion, set against the artifact lines; the report's own expected, actual, and result statements; and any sentence naming a deviation or scoping what was not tested. See **Honesty**. | Every reproduction claim and causal conclusion traces to a shown artifact line, the stated result describes what the run produced rather than what the issue predicted, the wording's reach matches the run's reach, and every deviation from the issue's conditions is named by the report itself. A diagnosis asserted without a shown measurement, a conclusion generalized past the one run, a result stated backwards, or an unmentioned deviation fails. An evidenced cannot-reproduce passes. | required |
| `claim-comment-specific` | The candidate claim comment read against the issue and the thread highlights, and against the house rules in `scope.md` in live mode. See **Comms**. | The comment names specifics of this issue that make it unpastable elsewhere (the symptom in the author's words, the version reproduced on, a detail from the thread), states one concrete next step tied to this code, and promises nothing it cannot back. A delivery date, a guarantee, a demand to reserve or assign, or interchangeable enthusiasm with no stated intent fails. | required |
| `ai-policy-respected` | The contribution-policy line of the repo-facts block, read for its scope (issue comments, pull requests, or any contribution) and its force (required, permitted, or silent), against both candidate comments. Live: `CONTRIBUTING.md` and any `AI_POLICY.md` or `AI_USAGE_POLICY.md`. See **Comms**, disclosure. | Treat the package as AI-assisted work. If the policy requires disclosing AI use for comments of this kind, the comment discloses it, naming the tool and the extent; if the policy requires the human to understand and own the work, the comment says so plainly. If the policy is silent, permissive without a disclosure ask, or explicitly exempts issue comments, the check passes whether or not a disclosure line is present. A policy requiring human-written comments passes on a comment written in the author's own words about their own run. | required |
| `control-or-contrast-shown` | The artifact blocks in the candidate repro report, read against the condition the issue names as necessary. See **Behavior shown**, control run. | Where the issue is conditional, a run with that condition removed is shown as its own artifact, so the contrast is visible rather than asserted. Passes trivially where the issue names no such condition. | preferred |
| `template-asks-covered` | The bug-reports line of the repo-facts block, read against both candidate comments. Live: `.github/ISSUE_TEMPLATE/`. See **Comms**. | Every field this repo's bug-report template asks a reporter for is supplied somewhere in the package, including the ones the symptom does not turn on. | preferred |

## Verdict rule

Accept when every required check passes. A single required fail is a
reject: each of the six names a way a package misleads the thread, and
none of them is offset by strength elsewhere, which is why an excellent
reproduction under a disclosure-requiring policy that does not disclose
is still held.

`unclear` on a required check counts as a fail. Proof I cannot verify
is proof that is not ready to post, and the honest move is to say what
is missing rather than to assume it exists somewhere off the page.

The two preferred checks never change the verdict in either direction.
They are reported so the summary can say what would make a passing
package stronger, and a package can be accepted with both failing.

In live mode on a claim-only draft, only `claim-comment-specific` and
`ai-policy-respected` are graded; the other six report `unclear` with
evidence `not yet applicable: claim-only draft` and are left out of the
verdict, so the verdict answers only whether the claim comment is ready
to post.
