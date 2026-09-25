# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/12

**Verdict output**

I'll load the issue-select skill, since that's exactly what this asks for.

⏺ Skill(issue-select)
Successfully loaded skill

  Read 3 files

Live mode, and all three URLs are in the scoped repo. Let me gather evidence.

  Ran 9 shell commands

All three issues are in the scoped repo (codepath/pathreview-ai301-fa26-s1). Graded each independently against rubric.md.

Repo-level evidence (shared by all three, today = 2026-09-25):
- Last default-branch commit 2026-09-16 by Aburke225 (human) — 9 days ago ✅
- Not archived; last push 2026-09-16; 3 stars; no releases
- Maintainer first-response sample: of 16 commented issues, only #43 and #52 got a maintainer reply (both 6 days) → 2/16, under half ❌ (preferred)
- docs/CONTRIBUTING.md exists, says nothing about AI-assisted work → passes (silence passes)
- Only one PR exists in the whole repo (#74 → closes #60), so none of these three has a linked or mentioned PR

Ranked read-out — all three accepted, and they tie on every preferred check (same maintainer-in-thread pass, same release/adoption/latency fails). scope.md's fit profile is still the placeholder (Write a few sentences here.), so I have nothing to rank on — fill that in and I can order them properly. Listed below by the issues' own effort estimates, which is my read, not the rubric's:

1. #73 — README vs .env.example disagree on the LLM API key. Two files, docs-only, 1–2 h, opened by a COLLABORATOR, zero comments, zero claims.
2. #18 — repo analyzer never gets file_structure. 2–4 h across two Python files. One claim comment from ColonelToad (author_association NONE, 2026-09-24) — under the Path Review house rule a classmate's claim does not block, so the check passes; expect company on it.
3. #12 — snapshot tests for prompt templates. 3–5 h, single test file, no comments or claims.

One tension worth naming: the latency check fails repo-wide because staff have barely replied to the student threads opened this week. It's a preferred check, so it can't sink anything, but it is the one real signal that PRs here may sit.

[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73",
    "checks": [
      {"name": "commit on the default branch", "grade": "pass", "evidence": "newest default-branch commit 2026-09-16 (9 days before 2026-09-25)"},
      {"name": "Who is committing", "grade": "pass", "evidence": "all 5 most recent commits authored by Aburke225, a human account"},
      {"name": "Issue response latency", "grade": "fail", "evidence": "only 2 of 16 commented issues (#43, #52) got any maintainer reply; the other 14 have none"},
      {"name": "Maintainer activity in this thread", "grade": "pass", "evidence": "opened by Aburke225, author_association COLLABORATOR"},
      {"name": "Release recency", "grade": "fail", "evidence": "GET /releases returns an empty list; repo has never published a release"},
      {"name": "Last push", "grade": "pass", "evidence": "pushed_at 2026-09-16T21:48:27Z, 9 days ago"},
      {"name": "Archived flag", "grade": "pass", "evidence": "\"archived\": false on the repo record"},
      {"name": "Adoption scale", "grade": "fail", "evidence": "stargazers_count 3, no Used-by counter (not a published library)"},
      {"name": "Bounded scope", "grade": "pass", "evidence": "\"Make the two files agree\" — README.md and .env.example, estimated effort 1-2 hours, no umbrella list and no debate"},
      {"name": "Real, endorsed request", "grade": "pass", "evidence": "opener Aburke225 is a human COLLABORATOR, not a [bot] account"},
      {"name": "Contribution, not support", "grade": "pass", "evidence": "asks for a docs change to two named files, not for help using the project"},
      {"name": "Age and failed attempts", "grade": "pass", "evidence": "opened 2026-09-16, 9 days old; no closed unmerged PRs reference it"},
      {"name": "Assignee", "grade": "pass", "evidence": "\"assignees\": [] on the issue record"},
      {"name": "Linked PRs", "grade": "pass", "evidence": "repo has exactly one PR (#74, closes #60); nothing links or mentions #73"},
      {"name": "Claim comments", "grade": "pass", "evidence": "comment count 0; no claim of any kind on the thread"},
      {"name": "Label freshness", "grade": "pass", "evidence": "good-first-issue label present on an issue opened 2026-09-16, 9 days ago"},
      {"name": "Contribution policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md covers branches, CI and xfail markers; no mention of AI-generated or AI-assisted contributions"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/18",
    "checks": [
      {"name": "commit on the default branch", "grade": "pass", "evidence": "newest default-branch commit 2026-09-16 (9 days before 2026-09-25)"},
      {"name": "Who is committing", "grade": "pass", "evidence": "all 5 most recent commits authored by Aburke225, a human account"},
      {"name": "Issue response latency", "grade": "fail", "evidence": "only 2 of 16 commented issues (#43, #52) got any maintainer reply; the other 14 have none"},
      {"name": "Maintainer activity in this thread", "grade": "pass", "evidence": "opened by Aburke225, author_association COLLABORATOR"},
      {"name": "Release recency", "grade": "fail", "evidence": "GET /releases returns an empty list; repo has never published a release"},
      {"name": "Last push", "grade": "pass", "evidence": "pushed_at 2026-09-16T21:48:27Z, 9 days ago"},
      {"name": "Archived flag", "grade": "pass", "evidence": "\"archived\": false on the repo record"},
      {"name": "Adoption scale", "grade": "fail", "evidence": "stargazers_count 3, no Used-by counter (not a published library)"},
      {"name": "Bounded scope", "grade": "pass", "evidence": "maintainer-written body names the cause and the fix across github_tool.py and repo_analyzer.py, 2-4 hours; no umbrella, no unsettled debate, no core-internals warning"},
      {"name": "Real, endorsed request", "grade": "pass", "evidence": "opener Aburke225 is a human COLLABORATOR, not a [bot] account"},
      {"name": "Contribution, not support", "grade": "pass", "evidence": "bug report asking for a code fix, not a usage question"},
      {"name": "Age and failed attempts", "grade": "pass", "evidence": "opened 2026-09-10, 15 days old; no closed unmerged PRs reference it"},
      {"name": "Assignee", "grade": "pass", "evidence": "\"assignees\": [] on the issue record"},
      {"name": "Linked PRs", "grade": "pass", "evidence": "repo has exactly one PR (#74, closes #60); nothing links or mentions #18"},
      {"name": "Claim comments", "grade": "pass", "evidence": "ColonelToad claimed it 2026-09-24 with author_association NONE, i.e. a classmate; scope.md's Path Review house rule says student claims do not block"},
      {"name": "Label freshness", "grade": "pass", "evidence": "good-first-issue label present on an issue opened 2026-09-10, 15 days ago"},
      {"name": "Contribution policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md covers branches, CI and xfail markers; no mention of AI-generated or AI-assisted contributions"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/12",
    "checks": [
      {"name": "commit on the default branch", "grade": "pass", "evidence": "newest default-branch commit 2026-09-16 (9 days before 2026-09-25)"},
      {"name": "Who is committing", "grade": "pass", "evidence": "all 5 most recent commits authored by Aburke225, a human account"},
      {"name": "Issue response latency", "grade": "fail", "evidence": "only 2 of 16 commented issues (#43, #52) got any maintainer reply; the other 14 have none"},
      {"name": "Maintainer activity in this thread", "grade": "pass", "evidence": "opened by Aburke225, author_association COLLABORATOR"},
      {"name": "Release recency", "grade": "fail", "evidence": "GET /releases returns an empty list; repo has never published a release"},
      {"name": "Last push", "grade": "pass", "evidence": "pushed_at 2026-09-16T21:48:27Z, 9 days ago"},
      {"name": "Archived flag", "grade": "pass", "evidence": "\"archived\": false on the repo record"},
      {"name": "Adoption scale", "grade": "fail", "evidence": "stargazers_count 3, no Used-by counter (not a published library)"},
      {"name": "Bounded scope", "grade": "pass", "evidence": "one deliverable in tests/unit/test_prompt_templates.py, estimated effort 3-5 hours; no umbrella list, no debate in the thread"},
      {"name": "Real, endorsed request", "grade": "pass", "evidence": "opener Aburke225 is a human COLLABORATOR, not a [bot] account"},
      {"name": "Contribution, not support", "grade": "pass", "evidence": "asks for new snapshot tests to be added, not for help using the project"},
      {"name": "Age and failed attempts", "grade": "pass", "evidence": "opened 2026-09-10, 15 days old; no closed unmerged PRs reference it"},
      {"name": "Assignee", "grade": "pass", "evidence": "\"assignees\": [] on the issue record"},
      {"name": "Linked PRs", "grade": "pass", "evidence": "repo has exactly one PR (#74, closes #60); nothing links or mentions #12"},
      {"name": "Claim comments", "grade": "pass", "evidence": "comment count 0; no claim of any kind on the thread"},
      {"name": "Label freshness", "grade": "pass", "evidence": "good-first-issue label present on an issue opened 2026-09-10, 15 days ago"},
      {"name": "Contribution policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md covers branches, CI and xfail markers; no mention of AI-generated or AI-assisted contributions"}
    ],
    "verdict": "accept"
  }
]

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

{
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/12",
    "checks": [
      {"name": "commit on the default branch", "grade": "pass", "evidence": "newest default-branch commit 2026-09-16 (9 days before 2026-09-25)"},
      {"name": "Who is committing", "grade": "pass", "evidence": "all 5 most recent commits authored by Aburke225, a human account"},
      {"name": "Issue response latency", "grade": "fail", "evidence": "only 2 of 16 commented issues (#43, #52) got any maintainer reply; the other 14 have none"},
      {"name": "Maintainer activity in this thread", "grade": "pass", "evidence": "opened by Aburke225, author_association COLLABORATOR"},
      {"name": "Release recency", "grade": "fail", "evidence": "GET /releases returns an empty list; repo has never published a release"},
      {"name": "Last push", "grade": "pass", "evidence": "pushed_at 2026-09-16T21:48:27Z, 9 days ago"},
      {"name": "Archived flag", "grade": "pass", "evidence": "\"archived\": false on the repo record"},
      {"name": "Adoption scale", "grade": "fail", "evidence": "stargazers_count 3, no Used-by counter (not a published library)"},
      {"name": "Bounded scope", "grade": "pass", "evidence": "one deliverable in tests/unit/test_prompt_templates.py, estimated effort 3-5 hours; no umbrella list, no debate in the thread"},
      {"name": "Real, endorsed request", "grade": "pass", "evidence": "opener Aburke225 is a human COLLABORATOR, not a [bot] account"},
      {"name": "Contribution, not support", "grade": "pass", "evidence": "asks for new snapshot tests to be added, not for help using the project"},
      {"name": "Age and failed attempts", "grade": "pass", "evidence": "opened 2026-09-10, 15 days old; no closed unmerged PRs reference it"},
      {"name": "Assignee", "grade": "pass", "evidence": "\"assignees\": [] on the issue record"},
      {"name": "Linked PRs", "grade": "pass", "evidence": "repo has exactly one PR (#74, closes #60); nothing links or mentions #12"},
      {"name": "Claim comments", "grade": "pass", "evidence": "comment count 0; no claim of any kind on the thread"},
      {"name": "Label freshness", "grade": "pass", "evidence": "good-first-issue label present on an issue opened 2026-09-10, 15 days ago"},
      {"name": "Contribution policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md covers branches, CI and xfail markers; no mention of AI-generated or AI-assisted contributions"}
    ],
    "verdict": "accept"
  }

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

Five runs, in order: 5/20 → 10/20 → 12/20 → 18/20 → 19/20.

The final run is the one recorded in `eval-run.txt` in this directory:

```
agreement: 19/20 scored items  (bar: 18/20: PASS)
```

**Issue analysis**

`issue-04` (source `zxcalc/zxlive#555`) — my rubric said **reject**, the gold label is
**accept**. It is the only disagreement in my final run.

The run recorded the cause:

```
issue-04  accept  reject   NO     failed: Issue response latency (preferred), Release recency (preferred), Bounded scope
```

Only `Bounded scope` matters, because it is the one required check of the three, and my
verdict rule is "Accept if every required check passes."

The whole issue body is one sentence:

> Including remove identity, fuse spiders, remove self loops, etc.

under the title "Missing several basic rule previews (#555)". My `Bounded scope` check
fails an issue that is "a list of sub-items meant to be split into separate issues or
PRs," and that sentence is literally a list of three items with an open-ended `etc.` on
the end. That is what the grader matched on, so the check failed and the issue was
rejected.

It should have passed. The same check says "Short is not unscoped: a terse body ... can
still pass, especially when the opener is a maintainer or the issue has a
good-first-issue label," and both of those escape hatches apply here:

> opened by RazinShaikh (COLLABORATOR) on 2026-08-04, state open, labels: Type: bug, good first issue, Category: Proof mode, Priority: Medium

The gold note agrees — "small active repo, maintainer-filed bounded bug, unclaimed". The
three rule previews are three small additions in the same place, not three separate
issues. My check read the *shape* of the sentence (a list) instead of the *size* of the
work (one bounded change), which is exactly the failure mode the check's own last line
warns against: "Grade the size of the work asked for, not the polish of the writeup."

**Check rationale**

The `Bounded scope` check, quoted as it currently stands in
`tools/issue-select/issue-select/skill/rubric.md`:

> | Bounded scope | the issue body, its labels, and the comment thread (especially maintainer comments) | fail if any of these hold: (a) the issue is explicitly an umbrella or tracking issue, a list of sub-items meant to be split into separate issues or PRs (a long, detailed spec for one deliverable, such as one new docs page plus pointers to it from existing pages, is not an umbrella); (b) the thread shows the design still being debated with no maintainer having settled it (an issue opened by a maintainer that lays out the causes, the fix, or a list of suggestions counts as settled, not debated); (c) a maintainer says outright that the fix touches core internals (e.g. "this needs changes to the parser"). Otherwise pass. Short is not unscoped: a terse body, an acceptance-criteria checklist, or a bug report without repro steps can still pass, especially when the opener is a maintainer or the issue has a good-first-issue label. Grade the size of the work asked for, not the polish of the writeup | required |

It reads that way because of how my scores moved. My first runs were 5/20 and 10/20, and
the problem then was the opposite of the one I have now: the check was a one-liner about
whether the issue "is a reasonable size," so the grader used its own taste and rejected
almost everything. The three lettered conditions exist to replace that taste with a test
someone else could apply and get my answer — an umbrella, an unsettled design debate, or
a maintainer saying the fix reaches core internals. Everything else passes by default.

The two sentences after the conditions were added between 12/20 and 18/20, and they are
the ones that moved the score most. I kept rejecting terse maintainer-filed bugs because
they *looked* unfinished, so I wrote down that short is not the same as unscoped and that
the thing being graded is the size of the work, not the quality of the writeup. The
parentheticals in (a) and (b) are the same fix applied to specific misses: a detailed
one-deliverable spec kept reading as an umbrella, and a maintainer listing suggestions
kept reading as an unsettled debate.

**Trade-offs**

`issue-04` is the case I accept it will miss, and I am keeping the check as written
rather than chasing it.

Condition (a) has to fire on something that reads like a list of sub-items, because that
is what an umbrella issue looks like from the outside — there is no other signal in the
text. A one-sentence list of three rule previews with an `etc.` on the end is genuinely
ambiguous: on the evidence in the bundle it could be one small change or the opening of
an open-ended pile of them. The only edits that would rescue it are ones that cost me
more than they earn. Loosening (a) to require an explicit "tracking issue" marker would
let `issue-05` through, the sympy codebase-wide type-annotation umbrella that wears a
good-first-issue label and is exactly what this check exists to catch. Letting the
good-first-issue label override (a) outright would do the same, since `issue-05` carries
that label too.

Nothing else regressed, and the run shows it:

```
categories: claimed 4/4  clear-accept 7/8  dead-repo 3/3  policy 1/1  scope 4/4
```

The scope category — the four issues this check is built for — is 4/4. The one miss sits
in clear-accept (7/8). So the check pays for one false reject in exchange for catching
every scope trap in the set, and the 19/20 clears the 18/20 bar. Trading a correct
rejection of a codebase-wide umbrella for a correct acceptance of one terse bug is a bad
trade for a first issue: the cost of wrongly skipping a good issue is that I pick a
different one, and the cost of wrongly taking an umbrella is weeks of wasted work.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

**1. Fit to my interests and the time available.**

I picked #12 because I want practice writing tests, and this is a test-only issue — the
whole deliverable lives in `tests/unit/test_prompt_templates.py`. It also sits in the
part of the codebase I actually want to understand, the prompt templates the RAG
generator uses, so I get to read that code closely without being responsible for
changing it. Touching no product code matters for a first PR: I can't break a running
feature, and if my snapshot tests are wrong the blast radius is the test file.

On time, 3–5 hours is tight but doable for me. It is the longest of the three issues I
graded, and I went in knowing that. #73 was a 1–2 hour docs fix and #18 was 2–4 hours,
so I am deliberately spending my whole budget rather than taking the easy one.

**2. What the verdict identified correctly, and what I weighed that the rubric could not.**

The verdict was right about the things I would not have checked carefully by hand. It
confirmed the repo is alive (a human commit nine days ago, not archived), that #12 has
no assignee, no linked PR, and no claim comments at all, and that `docs/CONTRIBUTING.md`
says nothing that would rule out AI-assisted work. It also correctly flagged what is
weak here: no releases, 3 stars, and a maintainer first-response rate of 2 out of 16
commented issues. Those are preferred checks, so they could not sink the issue, but they
told me something true — a PR here may sit for a while.

What the rubric could not weigh is that all three candidates tied on every preferred
check, so the ranking it gave me was not really a ranking. It listed #73 first purely on
the effort estimates, which is a proxy for "shortest," not for "best for me." I broke the
tie on what I want out of the unit rather than on what finishes fastest. The rubric also
cannot see that #18 already had a classmate on it; the house rule correctly says a
classmate's claim doesn't block me, but I would rather spend my one PR somewhere I am
not duplicating someone else's work. And it cannot judge that snapshot tests are a good
thing for *me* to learn right now.

**3. Anticipated difficulty in claiming it.**

Low. #12 is wide open — zero comments, no assignee, no linked PR, and the good-first-issue
label has been on it since the issue was opened on 2026-09-10. Nothing has to be cleared
before I comment.

The two real risks are both about other people, not about the issue. One is timing:
it is a tier-1 good-first-issue in a class this size, and several other issues picked up
claim comments in the last few days, so someone else may claim it between now and when I
post. The house rule says that costs me nothing since credit attaches to the PR I open,
but I would rather be first. The other is that I should not expect a reply confirming my
claim — of the 16 issues in this repo with comments, only two ever drew a maintainer
response. So I plan to write the claim comment, state what I intend to do, and start
work without waiting for an acknowledgement.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
