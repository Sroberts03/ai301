# Evidence guide: where proof lives in a reproduction package

This file is the rubric's map. For every kind of proof a check names,
it says where to look in a package and what good looks like when you
get there. A check whose evidence this file cannot locate is a check
nobody else can execute.

## How to read a package at all

**In eval mode the bundle is the world.** Each `packages/*.md` has five
parts, in this order, and every location below names one of them:

- `## Repo facts (captured ...)` — the repo line, the `latest release`
  line, the `bug reports` line (what the issue template asks for), and
  the `contribution policy` line (including any AI policy).
- `## Issue` — the title with its number, the author and their
  association, the state and labels, then the body: usually the
  reporter's own steps, expected result, and actual result.
- `## Thread highlights` — dated one-line summaries of the comments
  that matter, each with its author's association.
- `## Candidate claim comment` — the comment that would be posted to
  claim the issue.
- `## Candidate repro report` — the comment that would be posted as
  the reproduction.

The `.json` twin holds the same snapshot in fields:
`repo_facts.raw_markdown`, `issue.body_markdown` (plus `issue.title`,
`issue.author_association`, `issue.labels`), `thread_highlights[]`,
`claim_comment_markdown`, `repro_report_markdown`.

**In live mode the drafts are the world.** The candidate side is the
student's draft files (typically `claim.md` and `repro.md`); the
issue side is fetched:

- Issue body and thread: `gh issue view <n> --repo <owner>/<repo>
  --comments`, or the issue page.
- Template asks: `.github/ISSUE_TEMPLATE/*` (the bug-report form).
- Contribution and AI policy: `CONTRIBUTING.md`,
  `.github/contributing.md`, and any `AI_POLICY.md` /
  `AI_USAGE_POLICY.md` the contributing guide points to.
- Version landscape: `gh release view`, or the releases page.
- House rules: `scope.md` in this skill directory.

A draft is read the way a stranger on the thread will read it. Files in
the student's working directory that the draft does not contain or
quote are not evidence: an environment recorded only in a terminal
scrollback is an environment the reader never sees.

**Four rules that apply in every family below.**

1. The package's own frame fixes the facts. The `captured:` date and
   the `latest release` line are the version landscape; do not correct
   them against today's GitHub, and in live mode do not correct a
   draft's version claims against a release that shipped later.
2. Who is speaking decides what the bug is. `MEMBER`, `COLLABORATOR`
   and `CONTRIBUTOR` statements in the issue body or thread settle what
   correct behavior is and what the bug actually is; a `NONE`
   commenter's "same here" does not. When a maintainer says they
   cannot reproduce under some condition, that condition is part of
   the target.
3. The report has no fixed headings. Environments turn up as a lead
   line, a trailing line, or a table; results turn up under
   `Actual`, `Observed result`, `Conclusion`, or nothing. Locate proof
   by content, never by heading.
4. Absence is a finding, but confirm it. Before recording that
   something is missing, scan both candidate sections end to end; a
   detail is often in the claim comment rather than the report.

## Environment

**Where it lives.** Anywhere in `## Candidate repro report` — usually
an `Environment:` line at the top, sometimes a table
(`| Component | Version |`), sometimes a line near the end — plus any
version the `## Candidate claim comment` names. What the record must
cover is set by two other places: the issue's own version statement
(in `## Issue`, e.g. "confirmed on the latest version and on main", or
"1.9.4, 1.10.0"), and the `bug reports` line of `## Repo facts`, which
names the fields this repo asks every reporter for. Live: the draft
plus the issue's version fields and the bug-report template.

**What good looks like.**

- The record names the version of the thing under test and how it was
  installed, plus the platform facts the issue's symptom depends on —
  OS and build, browser, shell, driver, backend, build profile. The
  `bug reports` line is the checklist: a Windows-only tunnel issue
  whose template asks for the OS and the driver needs both.
- The versions tested are the ones the issue targets, or the report
  says in its own words that they are not: "filed against 1.9.4; still
  present on 1.11.7" is a record, while silently testing 1.5.3 against
  an issue confirmed on latest and main is a deviation dressed as a
  record.
- A reader could assemble the same setup from the text. "Latest
  version", "my machine", or a bare tool name does not place the
  attempt.
- Where the issue itself says the failure mode depends on an
  environment axis (a release versus debug build, one OS versus
  another), the record states that axis explicitly.

## Steps

**Where it lives.** The numbered steps, command blocks, and config or
source snippets in `## Candidate repro report`, read against the
reporter's own steps and trigger example in `## Issue` (and any
refinement in `## Thread highlights`, such as a maintainer spelling out
what triggers it). Live: the draft's steps against the issue page.

**What good looks like.**

- Three things are present: the starting state (what files, config,
  data, or session existed), the exact commands or UI actions in order,
  and the trigger — the specific input, syntax, or setting the issue
  blames.
- A stranger with only the repo and this comment could re-run every
  step. Commands are copyable; inputs are either shown inline or
  produced by a command that is shown; configs, layouts, and sketches
  the run depends on appear in the text or come from the issue. A step
  that rests on an unshared private repo or an internal config file
  ends the chain, however honestly it is described.
- The trigger matches the issue as written, character for character
  where the issue's syntax is the point. A near variant — a prefix
  range where the issue used an offset from the end, a colon where the
  issue used `=`, an expression edited until a variable is unbound —
  means the steps never reached the reported code path, and the
  artifact will be evidence about something else.
- Setup the issue calls essential is either reproduced or its absence
  is called out: a driver, a language-priority order, a directory
  layout, a theme pair.

## Behavior shown

**Where it lives.** The fenced blocks and quoted output in
`## Candidate repro report`: command transcripts, log excerpts, exit
codes, produced CSS or JSON, described screenshots. The comparison
target is the issue's own artifact in `## Issue` — its error text, its
expected and actual blocks, its stack trace — narrowed by anything in
`## Thread highlights`. Live: the draft's blocks against the issue
page's blocks.

**What good looks like.**

- The artifact contains the issue's named symptom, not merely output
  from the same tool. Compare the concrete tokens: the error string,
  the exit status, the code path in the trace, the header that should
  be present, the attribute that should be injected. `error: Invalid
  value for '--line-range'` with exit 1 is not the capacity-overflow
  panic with exit 101; a compile error is not `Invalid path
  expression`.
- For a crash claim, the artifact shows the process dying — a panic, a
  stack trace, a nonzero status the issue names. Garbled output with
  the window still open and the prompt returned is an adjacent
  symptom, and the report's own words often say so ("the window
  remained open afterward") while its conclusion says otherwise.
- The artifact shows the behavior, not the setup. A version banner, a
  session list, a tab bar, "everything is in place" — these show the
  tool runs. The issue's blank pane, stalled log, or missing header has
  to appear.
- A screenshot that is described but not attached is a description.
  Grade what the text contains.
- Where the issue is conditional ("only when a single header is
  present", "only with a non-English language first"), a control run
  with that condition removed, shown as its own block, is what turns
  an artifact into evidence about the condition rather than evidence
  that something happened once.
- An honest negative artifact still counts here: a run that shows the
  bug not occurring is evidence, as long as it is the issue's own
  scenario that was run.

## Honesty

**Where it lives.** The seam between two places: the confidence words
in `## Candidate claim comment` and in the report's summary or
conclusion lines, and the artifacts in `## Candidate repro report`.
Also the report's own `Expected` / `Actual` / `Result` lines, and any
sentence scoping what was not tested. Live: the same seam inside the
drafts.

**What good looks like.**

- Every claim traces to a line of the artifacts. Read each strong word
  — "fully reproduced", "confirmed", "guaranteed reproducible", "I
  verified this race condition", "verifiably broken" — and name the
  artifact line that backs it. A root cause asserted with no shown
  measurement, or a diagnosis the transcript never demonstrates, is
  the failure this family exists for.
- The wording's strength matches the run's reach. One run on one build
  does not support "this also demonstrates the problem is not limited
  to git-main builds", and the maintainers' stated inability to
  reproduce on that build makes the overreach load-bearing.
- `Actual` describes what the run produced, not what the issue
  predicted. When `Expected` states the issue's symptom and `Actual`
  reports a healthy startup, the report has stated its result
  backwards, and the artifact is the evidence for that.
- A cannot-reproduce passes on its own terms, and a good one is easy
  to recognize: the result is stated plainly and early ("I could NOT
  reproduce scenario 2"), a real attempt is shown with its artifacts,
  the conditions that differed from the report are named, the untested
  parts are scoped out ("I did not test scenario 1"), and any next
  step is offered as a hypothesis rather than a finding.
- Known deviations are surfaced by the report itself, not discovered
  by the grader: a different version, a trimmed trace that does not
  match the issue's, a substituted command. A deviation that the
  report names and reasons about is honest; the same deviation
  unmentioned is the whole failure.

## Comms

**Where it lives.** The `## Candidate claim comment`, read against
three things: the state of `## Issue` and `## Thread highlights` (who
is already working on it, what maintainers have asked for, whether the
repo assigns), the `bug reports` line of `## Repo facts` (what this
repo asks a reporter to supply), and the `contribution policy` line of
`## Repo facts` (the contribution guide and any AI policy, quoted
there in full). Live: the draft comments against
`.github/ISSUE_TEMPLATE/*`, `CONTRIBUTING.md` and any
`AI_POLICY.md` / `AI_USAGE_POLICY.md`, plus the house rules in
`scope.md`; `voice-guide.md` is held against the drafts separately and
does not live here.

**What good looks like.**

- The comment could not be pasted onto another issue. It names this
  issue's specifics: the symptom in the author's own words, the
  version reproduced on, a detail from the thread. Boilerplate
  ("Great project, I love it, kindly assign it to me") carries no
  evidence that its author read the issue.
- It states what the author actually did and one concrete next step
  tied to this code — a file, a function, a path to read
  (`apply_missing_repeated_headers()`, `Index.set_names`, the
  layout-apply path). "I will fix it" is an intention, not a step.
- It asks for nothing it cannot back: no delivery date, no
  "guaranteed", no demand to reserve or assign the issue where the
  repo does not assign, no claim of coordination that has not
  happened.
- It fits the thread as it stands. Where maintainers have already
  narrowed the cause or said they cannot reproduce under some
  condition, a comment that ignores that is talking past the room. In
  live mode the Path Review house rules in `scope.md` override the
  wild-GitHub reading of a classmate's existing claim.
- Disclosure: find the policy in the `contribution policy` line, then
  read its **scope** (issue comments, PRs, or any contribution) and its
  **force** (required, permitted, or silent).
  - Requires disclosing AI use in any form, and the comments do not
    disclose: fail. Treat every package here as AI-assisted work —
    that is how these comments are produced — so silence is never
    readable as "no AI was used".
  - Permits assistive use with the human responsible: a comment that
    names the tool and the extent, and says the author ran and
    understands the work, satisfies it in its own words.
  - Permissive with no disclosure ask, silent on AI, or explicitly
    stating no disclosure is expected for issue comments: absence of a
    disclosure line is fine, and adding one is neutral.
  - Policies that also require the human to understand the work read
    on the same line: the comment claims understanding plainly, and
    the rest of the package has to make that claim survivable.
