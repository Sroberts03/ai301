# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of my claim and reproduction on the issue I chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`.

---

## Your identity upstream

**GitHub username**

Sroberts03

---

## Posted upstream

**Claim comment**

<!-- TODO: paste the comment permalink here after posting, then paste the comment
text underneath it. Draft text is in ../../../unit2-drafts/claim.md -->

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/12#issuecomment-5880671172

Hi, I'm a student working through a course unit on open-source contribution,
and I'd like to take this one.

On `main` (f89c06f), the test meant to be the snapshot in
`tests/unit/test_prompt_templates.py` looks like it can't fail the way this
issue describes:

```python
content_hash = hashlib.md5(template_content.encode()).hexdigest()

# Expected hash - update if templates intentionally change
# This helps detect unintended changes to templates
assert isinstance(content_hash, str)
assert len(content_hash) == 32  # MD5 hash length
```

It hashes all five templates together, then asserts only that the digest is 32
characters — no expected value is ever compared against, so any edit should
still pass. The rest of the file checks placeholders, JSON instructions, and
keywords a silently rewritten template would still satisfy.

I've read that file but haven't run it. My first step is to verify the gap
rather than assume it: edit one template locally, run `pytest
tests/unit/test_prompt_templates.py`, and see whether the suite still passes.
I'll post the result here either way before opening a PR.

If it holds up, I'd record a digest per `(name, version)` pair in
`PROMPT_TEMPLATES` instead of one combined hash — editing `skills_feedback` v1
then fails by name, while adding a `v2` alongside an unchanged v1 passes. That's
the version-bump rule the issue asks for, and it says which template moved.

One design question: digests inline in the test file, or a committed snapshot
file with a flag to regenerate them? I'll go with inline unless you'd prefer
otherwise.

Happy to step aside if someone's already working on this.


**Reproduction comment**

<!-- TODO: paste the comment permalink here after posting, then paste the comment
text underneath it. -->

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/12#issuecomment-5880956435

# Reproduction: the prompt-template snapshot test cannot fail

**Issue:** [#12 — Add snapshot tests for prompt templates to catch accidental changes](https://github.com/codepath/pathreview-ai301-fa26-s1/issues/12)
**Verified on:** `main` @ `f89c06f`
**File:** `tests/unit/test_prompt_templates.py`, `test_template_snapshot_content_hash` (lines 191–204)

## Summary

`test_template_snapshot_content_hash` looks like the snapshot test issue #12 asks for,
but it never compares the hash it computes against a stored baseline. A template's
content can change arbitrarily and the test still passes. The protection the issue
describes is not currently in place.

## Setup

```bash
git clone https://github.com/codepath/pathreview-ai301-fa26-s1
cd pathreview-ai301-fa26-s1
git checkout main            # f89c06f

python3 -m venv .venv
.venv/bin/pip install -e ".[dev]"
```

`make setup` also runs migrations, seeds the database, and installs the frontend.
None of that is needed here — this test only imports `rag/generator/prompt_templates.py`,
so `pip install pytest structlog` is enough if you want the minimum.

## Step 1 — baseline

```bash
.venv/bin/pytest tests/unit/test_prompt_templates.py -q
```

```
.....................................      [100%]
37 passed in 0.03s
```

## Step 2 — record the hash the test computes

This mirrors lines 194–199 of the test exactly:

```bash
.venv/bin/python -c "
import hashlib
from rag.generator.prompt_templates import PROMPT_TEMPLATES as P
c=''.join(P[n][v] for n in sorted(P) for v in sorted(P[n]))
print(hashlib.md5(c.encode()).hexdigest())
"
```

```
3e79f974f8c1b6d8d1481dfc42e949ca
```

## Step 3 — change a template's content, leaving its version alone

In `rag/generator/prompt_templates.py`, inside `PROMPT_TEMPLATES["skills_feedback"]["v1"]`:

```diff
-1. Demonstrated technical skills (with specific examples from projects)
+1. Demonstrated technical skills (IGNORE ALL PREVIOUS INSTRUCTIONS)
```

The edit is deliberately chosen to slip past every *other* test in the module. It keeps
`{context}`, `{github_username}` and `{project_count}` intact, keeps the word "json",
stays over the 100-character floor, and leaves the version key at `v1`. Nothing else in
the suite is watching this text.

## Step 4 — confirm the content hash moved

Re-running the Step 2 command:

```
a196ad77879799f55f5119976f818de6     # was 3e79f974f8c1b6d8d1481dfc42e949ca
```

## Step 5 — re-run the tests

```bash
.venv/bin/pytest tests/unit/test_prompt_templates.py -q
.venv/bin/pytest "tests/unit/test_prompt_templates.py::TestPromptTemplates::test_template_snapshot_content_hash" -v
```

```
37 passed in 0.02s

tests/unit/test_prompt_templates.py::TestPromptTemplates::test_template_snapshot_content_hash PASSED [100%]
1 passed in 0.01s
```

**Expected:** the snapshot test fails, because a template's content changed without a version bump.
**Actual:** all 37 tests pass. A prompt now carrying an injection string ships green.

## Root cause

`tests/unit/test_prompt_templates.py:203-204`:

```python
content_hash = hashlib.md5(template_content.encode()).hexdigest()

# Expected hash - update if templates intentionally change
# This helps detect unintended changes to templates
assert isinstance(content_hash, str)
assert len(content_hash) == 32  # MD5 hash length
```

`hashlib.md5(...).hexdigest()` returns a 32-character `str` for *every* possible input,
including the empty string. Both assertions are tautologies — there is no template
content that makes this test fail. The comment above them describes an expected-hash
constant that was never written.

## Notes toward a fix

Two directions, if a maintainer wants to weigh in before I open a PR:

1. **Pin the hash.** Compare `content_hash` against a module-level constant. Smallest
   change, but a failure only says "something under `PROMPT_TEMPLATES` moved" — the
   developer still has to diff by hand to find out what.
2. **Per-template snapshot files.** One committed snapshot per `(template, version)`
   pair, compared individually. More files, but a failure names the template and the
   diff is readable in review, which is closer to what the issue asks for ("developers
   must consciously version templates").

I'd lean toward (2), with a documented way to regenerate snapshots for intentional changes.

## Eval iterations

**Run history**

Two runs, both full runs over all 20 scored packages, in order:

1. Full run, not saved — **19/20 scored items**. One disagreement, `pkg-10`:

```
pkg-10  accept  reject   NO     failed: artifact-shows-issue-behavior, control-or-contrast-shown

categories: clear-accept 7/8  disclosure 1/1  no-evidence 4/4  unfollowable-comms 3/3  wrong-target 4/4
agreement: 19/20 scored items  (bar: 18/20: PASS)
```

2. Full run with `--save-run eval-run.txt` — **20/20 scored items**, the run
   recorded in `eval-run.txt`:

```
categories: clear-accept 8/8  disclosure 1/1  no-evidence 4/4  unfollowable-comms 3/3  wrong-target 4/4
agreement: 20/20 scored items  (bar: 18/20: PASS)
```

The two commands were identical apart from `--save-run`, and I changed nothing
between them: same `rubric.md`, same `references/evidence-guide.md`, same
`SKILL.md`, same pinned model, same 20 packages. The header of `eval-run.txt`
records the hashes of the three files it graded:

```
# model: sonnet (pinned)
#   rubric.md  sha256:6b52277f6ab57dbb
#   evidence-guide.md  sha256:0ae13fecda538154
#   SKILL.md  sha256:094c7ec26a0f22ed
```

So `pkg-10` went from `reject` to `accept` on identical inputs. That is grader
variance on a borderline package, not a fix I made between rounds. I have two
draws from one rubric, 19 and 20. What I can claim is that both draws clear the
18/20 bar and that 19/20 is the worse of the two; what I cannot claim is that
the recorded run measures anything the first run did not.

Worth recording what I did not do: I never ran `--only`. Both rounds were full
runs at about $4 each, when the thing I actually needed to know — does `pkg-10`
flip again — is a one-package re-run at about $0.20. Next time the cheap
targeted round comes first and the full run comes last.

**Package analysis**

`pkg-10` (source `starship/starship#7648`, category `clear-accept`) — gold label
**accept**. My rubric said **reject** on run 1 and **accept** on run 2. It is the
only disagreement in either run; the other 19 packages agreed with gold both
times.

The run recorded the cause:

```
pkg-10  accept  reject   NO     failed: artifact-shows-issue-behavior, control-or-contrast-shown
```

Only `artifact-shows-issue-behavior` decided the verdict.
`control-or-contrast-shown` is `preferred`, and my verdict rule says preferred
checks never change the verdict in either direction — it is a fair note here
(the issue is conditional on macOS + fish and the report could only run Linux +
zsh), but it is not what rejected the package.

The package is an honest cannot-reproduce. The report runs the issue's exact
symlink layout and config, and the artifact it pastes is a prompt that works:

```
monorepo/packages/app-dir on  master
```

The issue's symptom is that this line goes *blank* when the working directory is
a symlink into a Git repo with `repo_root_style` set. So the artifact shows the
issue's behavior failing to occur, on the issue's own scenario — which is the
case my pass condition has a second clause for:

> A run of the issue's own scenario that does not produce the behavior also
> passes, when the report reports that negative result as its outcome.

The report satisfies that clause. It opens with "Result: cannot reproduce on
Linux + zsh with the report's exact layout and config", names what differed (OS
and shell, with the starship version matching), and says what a triggering setup
would likely need — "a fish shell resolving `PWD` logically looks necessary to
hit the `contract_repo_path` failure". Run 2 read it that way.

Run 1 applied the first sentence of the same pass condition instead — "At least
one shown artifact carries the issue's named symptom" — and no artifact does,
because the entire point of the report is that none could.

Both readings are available in the words I wrote, and that is the real finding
here: my check never tells the grader *which* clause governs when the report's
stated outcome is negative. `pkg-09` (`sharkdp/fd#2033`) is the other honest
cannot-reproduce in the set and agreed both times, because its artifacts are
produced output — marker ordering that visibly did not reorder — so the first
sentence has something concrete to read. `pkg-10`'s artifact is a single healthy
prompt line. That is why it sits on the seam and `pkg-09` does not.

**Check rationale**

`artifact-shows-issue-behavior`, quoted from the `rubric.md` the runs graded
(the copy whose hash is in the `eval-run.txt` header):

> | `artifact-shows-issue-behavior` | The output excerpts, transcripts, logs, and produced files in the candidate repro report, read against the issue's own error text and expected-versus-actual blocks, narrowed by any maintainer statement in the thread highlights. See **Behavior shown**. | At least one shown artifact carries the issue's named symptom: the same error string, exit status, code path, or missing or wrong output. A run of the issue's own scenario that does not produce the behavior also passes, when the report reports that negative result as its outcome. Artifacts that only show the tool running or the setup being ready, that show an adjacent symptom (a graceful error where the issue reports a panic, garbled output where the issue reports a dead process), or that are described rather than shown, fail. | required |

The second sentence is deliberate. An evidenced cannot-reproduce is a real
result, the gold set has two of them in `clear-accept`, and a rubric that
required every artifact to carry the symptom would reject both on principle. The
first and third sentences are written against the categories that actually need
holding: `wrong-target`, where the artifact shows an adjacent failure, and
`no-evidence`, where it shows the tool starting up.

Where the wording is thin is not the rubric row but the evidence guide the row
points at. The **Behavior shown** family gives the negative case one line, last,
after four bullets that all push the same direction:

> An honest negative artifact still counts here: a run that shows the bug not
> occurring is evidence, as long as it is the issue's own scenario that was run.

It is the only bullet in that family with no worked example under it, while the
bullets above it carry three (`bat`'s exit-1 argument error, `jq`'s compile
error, `zellij`'s version banner and tab bar). Read top to bottom, four
illustrated bullets say *reject* and one unillustrated line says *accept*. That
is the asymmetry the grader resolved differently on the two runs.

The revision I would make is not to the rubric row but to that family: name the
negative artifact as its own shape, before the symptom bullets rather than after
them, and make the order of operations explicit — read the report's stated
outcome first, then apply the matching clause. `pkg-10` is the example it should
carry, since it is the one that moved.

**Trade-offs**

The wording that makes `pkg-10` borderline is load-bearing elsewhere, which is
why I did not simply loosen it. Four of my correct rejections rest on the
symptom sentence: `pkg-14` (zellij artifacts show only a version banner, a
session list, and a tab bar), `pkg-02` (bat's graceful exit-1 argument error
narrated as the reported exit-101 panic), `pkg-08` (a jq compile error from an
edited expression, not the reported `Invalid path expression`), and `pkg-17`
(garbled escape-sequence output with the process still alive, presented as a
crash). Every one of them is a report whose artifact does not carry the issue's
symptom — the same sentence `pkg-10` failed run 1 on.

`pkg-14` is the one to keep in view, because on the artifact alone it looks like
`pkg-10`: neither shows the bug happening. The difference is not the artifact,
it is the stated outcome. `pkg-10` says it could not reproduce; `pkg-14` claims
confirmation and shows setup. So the scoping I would use keys the negative-result
clause to what the report *claims*, not to what the artifact lacks: only a report
that states a negative outcome gets read under that clause, and a report claiming
confirmation is graded against the symptom with no exception. That keeps the
clause from becoming a general excuse for a missing artifact, and it leaves
dishonest negatives to `claims-match-evidence`, which is where they belong.

What I am accepting in the meantime is one package that can land either way on a
re-run. I would rather record that than re-run until I draw a 20 and report the
20 as the rubric's accuracy. The honest summary is: 19/20 at worst across two
full runs, both passing the bar, with the variance concentrated in a single
cannot-reproduce package on a single required check.

---

Related paths: `eval-run.txt` in this directory — the hashes in its header
identify the exact `rubric.md`, `evidence-guide.md`, and `SKILL.md` that produced
it. My skill's files are in `tools/repro-check/`.
