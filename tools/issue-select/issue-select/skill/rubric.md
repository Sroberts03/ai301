# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

Every recency threshold below is measured against the bundle's capture
date in eval mode, and against today in live mode.

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| commit on the default branch | live: the repo's front page: the line above the file list shows the newest commit and its date; click the commit count next to it to see the recent history. Bundle: "last 5 default-branch commits" under Repo facts | a commit on the default branch within the last 30 days | required |
| Who is committing | live: the author of each commit in the default-branch history; open a bot commit to see whose PR it merged. Bundle: commit author names in "last 5 default-branch commits" under Repo facts | at least one of the last 5 default-branch commits is authored by a human (username not ending in `[bot]`), or is a bot commit merging a human's pull request | required |
| Issue response latency | live: a few recently updated issues (Issues tab, sort by recently updated), time from opening to the first reply by an Owner, Member, or Collaborator. Bundle: "maintainer first-response sample" under Repo facts | in at least half of the sampled issues, a maintainer (Owner/Member/Collaborator) first replied within 14 days | preferred |
| Maintainer activity in this thread | live: the Owner/Member/Collaborator badges next to commenters in this issue's thread. Bundle: author_association on each comment in the Comments section | the issue was opened by, or has at least one comment from, an OWNER, MEMBER, or COLLABORATOR | preferred |
| Release recency | live: the Releases box in the right sidebar of the repo front page: the latest release and its date. Bundle: "latest release" under Repo facts | latest release is no older than 30 days | preferred |
| Last push | live: the newest commit date on the front page and the Branches page. Bundle: "last push to any branch" under Repo facts | a push to any branch within the last 90 days | preferred |
| Archived flag | live: an archived repo shows a "This repository has been archived" banner across the top and is read-only: hard dead. Bundle: "archived:" on the repo line | The repo should not be archived | required |
| Adoption scale | live: the star count at the top of the repo page; for libraries, the "Used by" counter in the right sidebar. Bundle: stars on the repo line | Should have a several stars or used by number greater than 20 | preferred |
| Bounded scope | the issue body, its labels, and the comment thread (especially maintainer comments) | fail if any of these hold: (a) the issue is explicitly an umbrella or tracking issue, a list of sub-items meant to be split into separate issues or PRs (a long, detailed spec for one deliverable, such as one new docs page plus pointers to it from existing pages, is not an umbrella); (b) the thread shows the design still being debated with no maintainer having settled it (an issue opened by a maintainer that lays out the causes, the fix, or a list of suggestions counts as settled, not debated); (c) a maintainer says outright that the fix touches core internals (e.g. "this needs changes to the parser"). Otherwise pass. Short is not unscoped: a terse body, an acceptance-criteria checklist, or a bug report without repro steps can still pass, especially when the opener is a maintainer or the issue has a good-first-issue label. Grade the size of the work asked for, not the polish of the writeup | required |
| Real, endorsed request | the issue's opener and author_association, its labels, and the comment thread | fail if the opener is a bot account (username ending in `[bot]`) and no maintainer (OWNER, MEMBER, COLLABORATOR) has endorsed it by commenting or labeling it; pass otherwise | required |
| Contribution, not support | the issue body and title | fail if the issue is a pure usage question ("how do I get this to work?") asking for help rather than a change to the code or docs; pass otherwise | required |
| Age and failed attempts | the issue's open date and the linked/referenced PRs in its timeline | fail if the issue has been open 2+ years and has 2 or more closed, unmerged PRs that attempted it; pass otherwise | preferred |
| Assignee | live: the Assignees box in the issue's right sidebar. Bundle: "this issue: assignees:" under Repo facts | the issue has no assignee, or a maintainer comment dated after the assignment says the issue is free again | required |
| Linked PRs | live: the Development box in the issue's right sidebar, plus PRs mentioned in the comment thread. Bundle: "linked PRs:" with state per PR, plus any PRs mentioned in the Comments section. When the sidebar and the thread disagree, believe the thread | no open PR, linked or mentioned in the thread, is attempting this issue. Closed unmerged PRs do not fail this check (see Age and failed attempts) | required |
| Claim comments | the comment thread: comments like "I'll take this", "can I work on this", "working on this", with their dates and any maintainer reply | no one has claimed the issue in the last 60 days, unless the claimer or a maintainer later said the claim is dropped | required |
| Label freshness | live: the grey event line showing when the good-first-issue label was added. Bundle: issue open date vs capture date | the good-first-issue label was added (in the bundle: the issue was opened) within the last 365 days | preferred |
| Contribution policy | live: `CONTRIBUTING.md` in the repo root or `.github/` and the docs it links to, AI policy files like `AI_POLICY.md` or `AI_USAGE_POLICY.md`, and PR/issue templates. Bundle: the "contribution policy" line under Repo facts | fail only on an outright ban on AI-generated or AI-assisted contributions. Conditions (disclose AI use, understand and test every change, human review) pass, and so does a repo that says nothing. An `AGENTS.md` file is a sign AI tools are welcome | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->

Accept if every required check passes; preferred checks never change the verdict, they rank accepted issues; unclear counts as fail.