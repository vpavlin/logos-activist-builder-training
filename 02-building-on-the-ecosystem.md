# λ | Building on the Ecosystem

**Session 2 — Eco Dev — 30 minutes**

> Covers: open-source collaboration · builder workflows · documentation · working with
> Eco Dev and other contributors · turning successful pilots into reusable infrastructure.

## Run of show

| Time | Section | Notes |
|------|---------|-------|
| 0–3' | [The premise](#the-premise) | Reframes the session. Short, but do it. |
| 3–9' | [Open-source collaboration](#open-source-collaboration) | The bazaar, and permission to be confused. |
| 9–16' | [Builder workflows](#builder-workflows) | Idea → PoC → what happens next. The decision tree. |
| 16–20' | [Documentation](#documentation) | *(cut to 2' if needed — but don't cut entirely)* |
| 20–26' | [Working with Eco Dev](#working-with-eco-dev-and-other-contributors) | Who to talk to, and how. |
| 26–30' | [From pilot to infrastructure](#turning-pilots-into-reusable-infrastructure) | The payoff. Never cut. |

**Learning outcomes.** By the end, a participant can (1) name three ways to contribute that
aren't writing production code; (2) describe what happens to an idea after they propose it,
and who decides; (3) name the specific channel where they'd raise something; (4) explain
what makes a one-off pilot become something other groups can reuse.

---

## The premise

Session 1 was about the technology. This one is about the part that actually determines
whether any of it matters: **who builds on it, and how they find each other.**

Here's the uncomfortable version. A stack like this has been built before, more or less. The
reason those attempts are footnotes is almost never that the cryptography was wrong. It's
that the distance between "a protocol exists" and "an organiser in a difficult place has a
tool that helps them" was never crossed, because nobody's job was to cross it and nobody
built the road.

Eco Dev is the team whose entire job is that road. And the thing worth understanding is that
you are not being invited to *use* the road. You're being invited to help build it, and the
bar for doing so is much lower than people assume.

---

## Open-source collaboration

The model Logos works to is Eric Raymond's, from *The Cathedral and the Bazaar*. In the
cathedral, software is built by a closed priesthood and revealed when it's ready. In the
bazaar, it's built in public, messily, by whoever turns up — and Linus's Law applies:
**given enough eyeballs, all bugs are shallow.**

The practical consequence is that code is released to the public at the same moment it goes
to the internal team. There is no gated preview tier, no partner-only build. When something
ships, you have exactly the same access as the people whose job this is.

It goes further than access to code. **Every team publishes a weekly update, in public, at
[roadmap.logos.co](https://roadmap.logos.co)** — and they are unusually candid ones. They
name the bug that was found, the design that was abandoned, the assumption that turned out
wrong. Recent entries include a team removing a large part of their own codebase because
they'd changed their mind about the direction, and another describing a security hole in
their own signing code in detail, along with how it was closed.

That is worth pausing on, because it's rare and it's useful to you. You can read what every
part of this stack did last week, before deciding where to put your effort — and the tone of
those updates tells you what kind of collaboration is expected.

That's the structure. The part worth actually dwelling on is the culture, and specifically
three permissions that the Eco Dev team writes down explicitly for itself — and which extend
to you, because you are doing the same job from outside.

**Permission to break it.** Misusing software, stressing it, and finding the edges is the
work, not a nuisance alongside the work. Finding an issue is a *success*, explicitly. There
is a no-blame norm around it, written down, because teams that quietly punish bug reports
stop receiving them and then ship broken things confidently.

**Permission to be confused.** This is the one to sit with. The team's own principle is: *if
an experienced developer doesn't understand it, the community won't either.* Your confusion
is not a gap in you to be hidden until you've caught up. It is **data about the product**,
and it is data that only exists while you're still new. Someone who has used a tool for six
months has permanently lost the ability to see what's confusing about it. You have that
ability right now and it expires.

**Permission to say no.** To look at a piece of software and report that it is not ready —
for you, for your group, for the people you work with. That verdict is a legitimate,
requested output, not a failure to try hard enough.

> **What this means for you**
>
> The lowest-effort useful contribution to Logos is not code. It's an honest account of
> where you got stuck.
>
> "I followed the quickstart and it failed at step four and I don't know why" is a complete,
> valuable contribution. It goes in as a GitHub issue and it is exactly the raw material the
> team is asking for. You do not need to diagnose it, propose a fix, or apologise for it.
>
> The success condition the team has set for itself is telling: they want community
> contributions to eventually *exceed* Eco Dev's own — for the red team to become
> unnecessary because the bazaar has grown. That's not a slogan, it's the stated metric.
> Turning up is the contribution.

---

## Builder workflows

So you have an idea. Something your group needs, or something you can see a movement needing.
What actually happens to it?

### The shape of the path

The honest answer is that it goes through a triage, and the useful thing is knowing what the
triage is actually asking, because it tells you how to present an idea well.

First: **is this feasible?** The answer comes from building a small, ugly proof of concept —
not a product. A PoC exists to answer one question: can this be done on this stack at all,
and what breaks when you try? PoCs are allowed to be bad. Their output is knowledge, plus a
pile of issues filed against the parts of the stack that made it hard.

Then a genuinely open question: **does something already do this?** If an external project
already solves it, the sensible move is integration rather than building a second one. Not
every good idea should become new code, and a proposal that has already checked this is a
much stronger proposal.

Then: **who should build it?** This is where it forks, and the fork is worth knowing:

- **Built internally** — for things that are critical, or that nobody else will pick up.
- **RFP** — outsourcing the development effort while keeping tight control of the output.
  Used when the requirements are known and the work needs doing.
- **Lambda Prize (ꟛPrize)** — for genuinely hard, ambitious problems where *the solution
  isn't dictated*. A category of problem is named and a price is put on solving it; whoever
  takes it on defines the product requirements and the approach themselves.
- **A partner integrates it** — when someone external is already most of the way there.

> **What this means for you**
>
> Two things follow, and they're both actionable.
>
> First, the distinction between an RFP and a Lambda Prize is the distinction between "we
> know what we want, build it" and "we know what's broken, surprise us". If you have a hard
> problem from the field that no one has solved — the second category is *specifically for
> you*, and it doesn't require you to already know the answer.
>
> Second, and more immediately: **ideas enter this process from Logos circles and from the
> community, not only from inside the team.** The stated intent is that priorities should be
> set by what the ecosystem actually needs. That only works if the needs arrive. An idea that
> stays in the room where it was mentioned is an idea that will never be built.

### What makes a proposal land

Not a business plan. A few things that let someone else evaluate it:

- **The situation, not the feature.** "Our members are exposed when they donate" tells
  someone far more than "we want a private payments module". The first invites a solution;
  the second pre-commits to one that may be wrong.
- **Who specifically needs it, and how many.** One group's inconvenience and a pattern
  across thirty groups are different objects.
- **What you do today instead**, and what it costs you. This is the strongest section of any
  proposal and the most commonly omitted.
- **What "working" would look like** — how you'd know it had succeeded.

That's it. Write it as an issue on [`logos-co/ecosystem`](https://github.com/logos-co/ecosystem/issues)
and it is in the process. Not politely received — *in the process*, where the prioritisation
actually happens.

---

## Documentation

Documentation is treated as a first-class deliverable here, with its own team, its own
pipeline, and its own definition of done. That definition is worth quoting because it sets a
high bar: turning internal knowledge into documentation that a user can **execute correctly
on the first attempt.**

The pipeline runs in five stages. The engineers who built a thing hand over a "doc packet" —
raw knowledge, not prose. Writers turn that into a draft. The draft becomes *runnable*, with
its unknowns and assumptions written down explicitly rather than papered over. Then it gets
validated in parallel by the engineers, for technical correctness, **and by the red team,
who actually try to follow it end to end.** Only then is it published.

That fourth stage is the interesting one, because it's a job you can do.

> **What this means for you**
>
> Following a guide and reporting where it broke is a formal, requested step in this
> process. It has a name and a place in the workflow. It is not you failing to keep up with
> a document — it is the validation the document requires before it can ship.
>
> And the guides genuinely need it. Several still carry an explicit "this is an early draft
> and may be incomplete or incorrect" banner. Those banners are not embarrassment; they're an
> invitation with the door left open.
>
> They also get closed. The headless-node guide was, until recently, closer to a placeholder
> — it openly listed what it didn't yet know. There is now a real node operator guide with
> pinned versions and commands that run. Storage rewrote all of its tutorials this summer,
> explicitly so they'd work on modest hardware, after a user described theirs as a "potato
> PC". That is the loop working: somebody said it was too hard, and it got easier.
>
> There is also a specific, slightly odd contribution that matters more than it sounds:
> documentation is explicitly written to be **readable by AI assistants**, because a large
> share of people now approach a new stack by asking a model. Docs that a model reads
> correctly are docs that work for everyone downstream. If you notice that an assistant
> confidently told you something the docs actually contradict, that is a documentation bug
> worth filing.

**Where to go:** [`logos-co/logos-docs`](https://github.com/logos-co/logos-docs). Issues and
pull requests both welcome; fixing an unclear sentence is a real contribution and a
completely normal first one.

---

## Working with Eco Dev and other contributors

Eco Dev's mandate is a two-way valve: carry the ecosystem's needs *into* the technology
stack, and carry what the stack can do *out* to the people who might use it. Both directions
matter, and the inbound one is the one that's usually starved.

The team splits into streams, and knowing which one you're talking to saves everyone time:

| Stream | What they do | Come to them when |
|---|---|---|
| **Red Team / Solution** | Dogfooding, PoCs, builder support, mentorship | You're stuck building something, or you found something broken |
| **DevKit / DappFoundry** | Tooling, SDKs, scaffolding, template apps | The tooling is the obstacle, or you want a starting point |
| **Integration** | Ecosystem map, requirements, delivery strategy | You have a need to get onto the roadmap |
| **Lambda Prize & RFP advisory** | Scoping, technical review, supporting candidates | You're considering applying for one |

Notice that "builder support (mentorship, technical assistance, solution engineering)" is a
listed output of the Red Team, not a favour they do when they have time. If you are building
on Logos, supporting you is somebody's actual job.

### Knowing what to ask about

Before reaching for a person, [roadmap.logos.co](https://roadmap.logos.co) will usually tell
you whether the thing you need is being worked on, was abandoned, or has never been
considered — and those three get very different conversations. Each team has its own stream
of weekly updates, and the deeper research arguments happen in the open at
[forum.research.logos.co](https://forum.research.logos.co).

It's also the honest answer to "is this project alive?", which is a fair question to ask of
any young stack and an awkward one to ask a person.

### How to reach them

- **Discord `#ecodev`** — the main channel. Lightweight questions are fine, and there are
  per-team channels for deeper protocol questions.
- **GitHub issues** — on [`logos-co/ecosystem`](https://github.com/logos-co/ecosystem/issues)
  for needs and ideas; on the specific repo for bugs. Issues raised from ecosystem work carry
  a `from-eco-dev` label so they're traceable as coming from real use.
- **Office hours** — a recurring, scheduled slot for direct questions. Use it; that is what
  it's for.
- **Vibe coding sessions** — live, unedited sessions of someone building on the stack in
  public, including the parts where it doesn't work. Deliberately honest about developer
  experience. Both a good way to learn and a good format to *ask for* on your use case.

### On working with other contributors

Two things are worth saying to a room of organisers specifically.

**Your problem is almost certainly not unique.** The Eco Dev wiki maintains a list of desired
projects — private DAOs, local peer-to-peer marketplaces, activity hubs, community CMS,
multisig, forums. Read it before proposing. Not to be discouraged if yours is there, but the
opposite: if it's already on the list, you're not asking for a favour, you're adding weight
to something already wanted. And there may be someone already working on it.

**Circles are the on-ramp.** Logos circles are the grassroots layer of this — local groups
where ideas surface and route into the process described above. If you want a path from
"my group has a problem" to "something got built", that's usually it, and it doesn't require
you to be technical at all.

---

## Turning pilots into reusable infrastructure

This is the closing idea, and it's the one that makes the difference between a movement with
tools and a movement with a toolkit.

The pattern that fails is familiar. A group has a need, someone builds something that works,
and it dies with the campaign — because it lived on one laptop, with no documentation, with
one person who understood it. Every subsequent group starts from zero. This isn't a failure
of skill; it's a failure of *packaging*, and it's the default outcome unless something is
deliberately done about it.

The stack makes the technical half easier — a Basecamp module is a package another group
installs, not a codebase they compile. But the packaging half is a discipline, and Logos has
written it down as the definition of a shipped sample app:

- **Code in a public repo with an open licence.** Non-negotiable. Not reusable otherwise.
- **FURPS+** — a written statement of what it does and doesn't do: functionality, usability,
  reliability, performance, and explicitly privacy, anonymity and censorship-resistance. The
  "+" is where a tool for activists is honest about what it actually protects against.
- **Architecture Decision Records** — *why* the design is the way it is. This is what lets
  the next group adapt it instead of guessing, and it's what preserves the reasoning after
  the person who did the reasoning has moved on.
- **Declared dependencies** — which parts of the stack it needs, so someone can tell what
  they're taking on.

Meet that bar and the trajectory is: **pilot → sample app → template → ecosystem
infrastructure.** Sample apps are explicitly intended to become templates that other people
take to production. Something that starts as one group's answer to one situation becomes the
starting point for the next thirty.

> **What this means for organising**
>
> Concretely: if your group builds something and it works, the difference between a useful
> afternoon and a contribution to the movement's shared capacity is a public repo, a
> readme that says what it protects, and a note explaining why you built it that way.
> That's a day's work at the end, and it's the highest-leverage day in the project.
>
> The FURPS+ point deserves emphasis for this room. Writing down precisely what a tool
> protects against — and what it doesn't — is not bureaucracy. Someone will eventually make
> a decision about their safety based on your tool. The document that tells them what it
> actually does is part of the tool.

> **Closing line, if you want one**
>
> The stack in Session 1 exists so that this is possible. This session is the part that
> makes it happen. The infrastructure a movement gets is the infrastructure its people
> bothered to package — and right now, early, with the roadmap still open, what gets
> packaged is decided by who shows up with a real problem and doesn't leave.
