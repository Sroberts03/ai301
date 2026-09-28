# Voice guide: how I talk upstream

The version numbers, file names, and repo details in the wrong/right
pairs below are placeholders in the shape of real lines. Swap them for
my issue's actual specifics as I go; the rule each pair demonstrates
does not change.

## Who I am in threads

I'm a student working through a course unit on open-source
contribution, and I say so in the first line rather than letting
someone guess. I'm new to this repo and I don't pretend otherwise, but
I show up with something I actually ran, not with enthusiasm. What a
maintainer can expect from me: a short comment, the evidence attached,
an honest account of what I did and didn't verify, and no follow-up
pressure.

## Rules I write by

### Rule: claim exactly as far as I ran

Every confidence word has to be cashable against an artifact in the
same comment. If the strongest thing I have is one run on one machine,
that is what the sentence says. "Reproduced" means the output is right
there; a cause is a hypothesis until a run demonstrates it.

- Wrong: "I've fully reproduced this and tracked down the root cause:
  the debounced save is definitely being cancelled by the switch
  handler."
- Right: "Reproduced on 3.9.6 (output below). The timing makes me
  suspect the debounced save is cancelled before it fires, but I
  haven't instrumented that yet."

### Rule: name what I didn't do

Scope is part of the claim. I state which case I tested, which I
skipped, and what differed from the report's conditions, in the same
breath as the result. A cannot-reproduce is a real finding when I say
plainly that I ran the thing and it didn't happen.

- Wrong: "Confirmed, this reproduces on my setup."
- Right: "Scenario 2 reproduces on my setup (below). I didn't test
  scenario 1, and my environment differs from the report's on shell
  and OS, both noted in the report."

### Rule: one line of context, then the evidence

Warmth is fine; buying goodwill with it is not. I get one plain
sentence of who I am and what I'm doing, then the run. No praise for
the project, no emoji, no exclamation points doing work my evidence
should do.

- Wrong: "Hello maintainers! Amazing project, I use it every day and
  I'd love to help out with this awesome repo 🙏 This issue looks
  perfect for me!"
- Right: "Hi, I'm a student making a first contribution here. I
  reproduced the missing header on 3.2.4; report below."

### Rule: ask with evidence, never with a date

I may ask for the issue, but only in a comment that already contains
the reproduction, and only in a form the maintainer can decline. I
never name a delivery date, and I never ask anyone to hold or reserve
an issue for me.

- Wrong: "Kindly assign this to me, I will fix it within 2 days
  guaranteed. Please keep it reserved for me."
- Right: "Reproduction is above. I'd like to take this if it's not
  already spoken for; my next step is reading how `set_names` wraps
  scalar names. Happy to step aside if someone's further along."

### Rule: disclose the assistant, tool and extent

I disclose AI assistance in every comment I post, whatever the repo's
policy requires, naming the tool and how far its help went, and I only
post prose I've read and would defend as my own. The disclosure is one
sentence, not an apology.

- Wrong: (no mention at all, in a comment that was drafted with an
  assistant)
- Right: "Disclosure: I used Claude Code to help organize this report.
  I ran every step myself and I understand what I'm reporting."

## Things I never post

- **A date or a deadline.** No "by Friday", no "within 2 days", no
  estimate of when a fix lands. I don't control my week or the review
  queue.
- **Certainty I didn't earn from a run.** No "definitely",
  "guaranteed", "100%", "confirmed root cause" unless a shown artifact
  says it. A hypothesis gets called a hypothesis.
- **Flattery, emoji, or hype.** No "amazing project", no 🙏, no
  exclamation-point enthusiasm spent to make a maintainer like me. The
  evidence is the goodwill.
- **"+1", "same here", or a nudge for updates.** If I have nothing new
  to add, I don't post. Asking "any updates on this?" adds nothing and
  costs someone a notification.
- **Words I didn't write.** Nothing an assistant drafted goes up
  unread or unedited, and nothing goes up undisclosed.
