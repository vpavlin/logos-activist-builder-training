# λ | Logos Tech Stack

**Session 1 — Eco Dev — 30 minutes**

> Covers: intro to Logos Blockchain, Messaging, Storage and Basecamp · running a node
> basics · existing tools and developer resources.

## Run of show

This document is now the **source of truth for the e-learning**, and reads at roughly 39
minutes. That's deliberate — it's easier to cut a rich text than to pad a thin one — but it
means the live 30-minute session is a *cut* of this, not a reading of it.

**The 30-minute live cut.** Take these, in these proportions:

| Time | Section | Take |
|------|---------|------|
| 0–4' | [Three ancient needs](#three-ancient-needs) | Napster and DigiNotar only. Drop the Usenet/email paragraph — messaging re-tells it better. |
| 4–9' | [Messaging](#messaging) | Full, but compress *Two things being built on top* to its closing box. |
| 9–14' | [Storage](#storage) | Full. This is the section that changed most, and unlinkability is the strongest single idea in the talk. |
| 14–18' | [Blockchain](#blockchain) | Drop the Zones/LEZ paragraph and the post-quantum aside. |
| 18–24' | [Basecamp](#basecamp) | Full, including the permission model — it's what makes "install this" a reasonable ask. |
| 24–27' | [Running a node](#running-a-node) | One line per sense of the phrase, then the Raspberry Pi fact. |
| 27–30' | [Where to go next](#tools-and-resources) | Never cut. This is the whole point. |

**What the full text is for:** the e-learning, the handout, and your own confidence — the
detail you don't say is the detail that lets you answer the question afterwards.

**Learning outcomes.** By the end, a participant can (1) name the four pieces and say what
each is *for*, in their own words; (2) explain why they are separate things rather than one
thing; (3) name one earlier decentralised system and why it lost; (4) say what "running a
node" would mean for them concretely; (5) name one place to go to start.

---

## Three ancient needs

All of the Logos Tech Stack comes from ancient (in internet terms) needs to communicate,
archive and reach consensus.

The thing worth knowing — and what makes this less of a leap of faith than it might sound —
is that **the internet already had decentralised answers to all three.** They weren't
prototypes. They worked, millions of people used them, and then one by one they were
replaced by things that belong to somebody.

That history is the actual design brief for everything in this session, because none of them
lost by accident. Each was beaten by a specific, nameable pressure.

**We could talk without a platform.** Usenet, from 1980, was a genuinely decentralised
discussion network: thousands of independent servers passing messages between themselves,
no company, no owner, no terms of service. Email was the same bargain — anyone could run a
mail server and reach anyone else. Both are effectively finished as decentralised systems.
Usenet drowned in spam, because an open network where anyone may publish and nobody has an
account has no way of saying *you have had enough*. Email survived by centralising: the
defence against spam was reputation, reputation required scale, and so today you can
absolutely run your own mail server — it just won't get delivered.

**We could publish without a host.** Napster, in 1999, showed that millions of ordinary
people would share files directly with one another. It had one weakness: a central index,
which turned out to be a single address at which to serve a court order. Gnutella answered
that within a year by removing the index altogether, and promptly discovered that a network
where every search is shouted at everybody does not scale. BitTorrent found the balance and
is still with us — but it never solved *permanence*. A torrent lives while people seed it
and dies quietly when they stop. Nothing keeps your thing alive except somebody's goodwill.

**We never really solved agreeing at all.** The internet's actual answers to "who is this"
and "where does this name point" — the certificate authorities that vouch for websites, and
the domain name system — were hierarchies from the very beginning. They work, and they are
chokepoints by design. In 2011 a Dutch certificate authority called DigiNotar was broken
into and used to issue fraudulent Google certificates, which were used to read the email of
roughly 300,000 people in Iran. That is not a theoretical risk to activists; that was the
actual, observed use. Domain seizure, meanwhile, is routine enough to be a standard
instrument of policy.

None of those are crypto failures. They are internet failures, from before anyone used the
word blockchain, and the pattern across all three is identical: the decentralised version
existed and lost — to spam it couldn't filter without demanding identity, to permanence it
couldn't guarantee without incentives, to trust it couldn't establish without a hierarchy.

| Ancient need | Lost to | Logos layer |
|---|---|---|
| Communicate | Spam, and the identity required to stop it | **Logos Messaging** |
| Archive | Nothing keeping it alive once attention moved on | **Logos Storage** |
| Reach consensus | Never attempted without a hierarchy | **Logos Blockchain** |
| *(and: be usable)* | Every one of them, honestly | **Logos Basecamp** |

One caveat on the second row, because it would be easy to oversell: Logos Storage's current
answer is about *who can see what you publish and fetch*, not about permanence. Keeping
things alive when attention moves on is, genuinely, still unsolved — by them and by
everybody else. More on that below.

The fourth row is not an ancient need — it's the honest admission that the first three are
plumbing. Plumbing nobody can install is a research project. And "too hard to use" is a
perfectly good cause of death: it's most of why Freenet, built explicitly for dissidents in
2000 and censorship-resistant in ways that still hold up, never reached the people it was
for. Basecamp is the answer to "and then what does a person actually open?"

> **Worth saying out loud**
>
> This isn't a break from that history, it's a continuation of it — quite literally. The
> peer discovery in Logos Blockchain is Kademlia, from the academic wave of the early 2000s.
> The privacy routing descends from mix networks, which David Chaum described in **1981**,
> before the web existed, and which you may already know through Tor. The trick for limiting
> spam without demanding identity is the great-grandchild of hashcash, proposed in 1997 to
> fight email spam.
>
> Every one of these ideas is older than most of the platforms we're trying to replace. What
> changed is not the ideas. It's that the pieces can now be assembled into something an
> ordinary person can install.

> **What this means for organising**
>
> Think about the last campaign you ran. Where did the conversations live? Where did the
> documents live? Where did the money and the membership list live? For almost everyone the
> answer is: on three platforms, each of which can close your account on a Tuesday, each of
> which can be compelled to hand over what it holds, and none of which you can leave without
> losing your history.
>
> That situation is recent, and it is not natural. It is roughly twenty years old, and every
> layer of it replaced something more distributed that people had already built. The stack
> below is an attempt at the version that doesn't get recaptured — which mostly means taking
> seriously the specific reasons the last attempts were.

## Messaging

Logos Messaging is a general peer-to-peer network allowing any connected peers to
communicate while preserving their privacy. It is built on top of libp2p, utilizing
GossipSub at its core to disseminate messages across the network and adding necessary
protocols on top of it. This allows Logos Messaging to serve edge nodes, provide some
reliability guarantees even to devices who disconnected briefly and maintains the
configured rate limiting to allow for predictable bandwidth and fairness.

It is important to emphasize the generality of the network — the payload is opaque bytes and
each peer filters messages they are interested in based on message metadata, so the use
cases span from human-to-human chat, accessing remote APIs or completely automated
coordination of bots.

Three of those properties are worth unpacking, because each one is doing real work.

**Serving edge nodes.** A phone is not a server. It sleeps, it changes networks, it runs on
a battery, and it is behind a NAT. Most peer-to-peer designs quietly assume a machine that
is always on and always reachable, which is why so many of them are only ever run by
enthusiasts with a spare box. Logos Messaging has protocols specifically for devices that
can't hold up their end of the gossip — they can ask a well-connected peer to relay on their
behalf, subscribe to only the slice of traffic they care about, and ask for what they missed.
That is the difference between "a network organisers can use" and "a network organisers'
technical friend can use".

**Reliability across a brief disconnect.** Because some peers store messages and will serve
them back on request, going through a tunnel doesn't mean losing the thread. This is a
weaker guarantee than a server-backed chat app — it's "ask around and probably get it back",
not "it is definitively kept for you" — and the difference matters when you design something
on top.

**Rate limiting without identity.** This is the one that killed Usenet, so it's worth
dwelling on. In an open network where anyone may publish and nobody has an account, what
stops a flood? The usual answer is accounts, which means identity, which is exactly what you
were trying to avoid — and it is why every open network of the last forty years has
eventually had to choose between being swamped and being surveilled.

Adam Back proposed the shape of a third answer in 1997: hashcash, which made a sender do a
small amount of provable work for each message. Cheap for a person sending a few, ruinous
for a machine sending millions, and it needed to know nothing about who you were. Logos
Messaging uses the modern descendant of that idea — a peer proves in zero knowledge that it
is within its allowance, without revealing which peer it is. Stay inside the limit and you
are anonymous; exceed it and the proof itself gives you up. A bouncer who can count but
cannot see faces.

> **What this means for organising**
>
> There is no room to be seized, no group to be reported, no admin account to be pressured,
> and no server whose logs can be subpoenaed — because there isn't a server. Messages move
> between participants, and the network as a whole doesn't know who is talking to whom.
>
> Be precise about the claim, though, because activists will be, and should be. This is
> **transport-level** privacy: it protects the *pattern* — who talks to whom, when, from
> where. It is not, by itself, an end-to-end encrypted messenger, it has no notion of your
> identity, and it will happily carry a plaintext message if the app on top asks it to.
> Encryption of the *content* is a separate job — see the next section for who is taking it
> on. Logos Messaging's own contribution is that the network can't build a social graph
> out of you.

### Two things being built on top

Both are live work rather than finished products, and each closes a gap named above.

**libchat** is the secure messaging layer — the answer to "so who does the content
encryption, then?" Rather than every application inventing its own, libchat handles
identity, *introduction bundles* (how two people who have never met bootstrap an encrypted
conversation), private conversations, and delivery acknowledgements. It already exists as a
Basecamp module with a reference chat UI, so an app can have real private messaging by
calling it rather than by hiring a cryptographer and hoping. Chat is in beta.

Two pieces are landing on top of it that matter for organising specifically. **Group**
messaging is being built on de-MLS, a decentralised take on the standard the rest of the
industry is converging on for encrypted group chat — which is the difference between secure
one-to-one conversations and a secure *organisation*. And an identity primitive called
λAccount is in review, which is what lets an account be a durable thing you own rather than
a handle issued to you.

**libp2p-mix** pushes mixing down into the transport itself. Logos Messaging already hides
who is talking to whom from any single observer. A mixnet goes further: each message is
routed through a pool of relays that each peel off one layer of encryption and hold the
message briefly before passing it on, so that even somebody watching the whole network
can't line up what went in with what came out. This is the 1981 Chaum idea again — the one
that produced Tor — now being wired directly into the peer-to-peer layer, so that a message
can be published without the network learning who published it.

Both have shipped further than "planned": as of testnet v0.2.1, chat uses de-MLS for direct
conversations as well as groups, and the mix work is being exercised by an AnonComms demo.

> **What this means for organising**
>
> Take them together and you get the property most people actually mean when they say
> "secure" — not merely that the contents are unreadable, but that the conversation is
> unobservable. Content encryption on its own still leaves a pattern of who contacted whom
> and when, and in the situations that matter, the pattern is frequently the evidence.

> **Honest status**
>
> This is the most mature layer in the stack by a wide margin — it is the continuation of
> the Waku project, with years of running network behind it, and it is already carrying real
> traffic. If you want something that works today, start here. Mobile builds for Android and
> iOS were repaired and put under CI this summer, which matters if what you're imagining runs
> on phones.
>
> The two additions above are genuinely in progress rather than done. Mix is furthest along
> on the storage side; group messaging and the identity work are in review and simulation.

**Where to go next:** [`logos-messaging/logos-delivery`](https://github.com/logos-messaging/logos-delivery)
is the node implementation, and inside Basecamp it appears as the **Delivery module**, which
apps call rather than speaking the protocol themselves. libchat lives at
[`logos-messaging/logos-chat`](https://github.com/logos-messaging/logos-chat), reachable
from Basecamp as the **ChatSDK module**. The mix protocol is part of
[`vacp2p/nim-libp2p`](https://github.com/vacp2p/nim-libp2p).

---

## Storage

Logos Storage is a filesharing protocol which allows anyone running the Logos stack to
publish a file and anyone else to fetch it, without a server in between and without either
of them being identifiable. It began as Codex, a decentralised storage network in the
conventional sense, where you paid providers to hold your data and they periodically proved
that they still had it. That model was removed from the codebase in January 2026 and the
project refocused on privacy preserving filesharing, which is a narrower goal and a
considerably harder one.

Files are content addressed, so a file's name is derived from its bytes, and asking for it
by name means asking for exactly those bytes and nothing else. Availability comes from
interest rather than from payment - everyone who downloads a file also becomes a source of
it, so the things people actually read become more resilient the more they are read. It is
important to be blunt about the other side of this: there are no durability guarantees any
more, and a file nobody fetches can quietly disappear.

Most of the current effort goes into unlinkability. The goal is that neither the publisher
nor the downloader of a file can be linked to it by anybody else, queries included, and that
a node caching content can plausibly deny knowing what it is holding. This is achieved by
routing traffic through a mix network in Sphinx format packets, so that an observer watching
the network cannot match what went in with what came out. The team's own benchmark is that
downloading this way should perform about as well as running BitTorrent over Tor, and they
are now designing hidden services on the same transport.

> **What this means for organising**
>
> The obvious use is publishing that can't be quietly pulled: a report, a dataset, a
> testimony. Once something is addressed by its contents and spread across the network,
> taking it down isn't a phone call to a hosting company, and a doctored substitute has a
> visibly different address.
>
> But the property being built now is the one that's harder to get anywhere else, and it's
> about **reading**, not publishing. In a great many situations the dangerous act is not
> putting the document out — it's being seen to fetch it. Downloading a banned text, a
> leaked file, a piece of evidence, is the act that puts a name on a list. Publisher and
> downloader unlinkability means the network cannot tell who asked for what. Plausible
> deniability for caching nodes matters for the same reason from the other side: a group can
> contribute storage to a movement without vouching for everything that passes through it.
>
> Two disciplines this demands. **Encrypt before you upload** — censorship resistance and
> confidentiality are different properties, and something that can't be deleted also can't
> be un-published. And treat it as a *sharing* network rather than a vault: with organic
> replication, keeping something alive means somebody continuing to care about it. It is not
> yet the place for the only copy of something irreplaceable.

> **Honest status**
>
> The split matters here. The filesharing part works and ships — the Basecamp module is at
> v2.1.x, with much better NAT traversal and a genuinely simpler onboarding flow, and the
> tutorials were rewritten this summer to run on modest hardware. The *anonymity* part, which
> is the reason to be interested, is actively under construction: the mix transport does
> basic transfers as of August 2026, hidden services are still at the spec and simulation
> stage. So: usable for sharing today, with the property that makes it matter landing
> progressively over the coming releases.
>
> This is the thread Freenet was pulling on in 2000 — censorship-resistant publishing with
> plausible deniability, built explicitly for dissidents. Its cryptography largely still
> stands up; it failed because using it was miserable. That is a real way to fail, and it is
> why Basecamp gets a section of its own.

**Where to go next:** [docs.logos.co/storage](https://docs.logos.co/storage) is the intro and
tutorials. [`logos-storage/logos-storage-nim`](https://github.com/logos-storage/logos-storage-nim)
is the node; [`logos-co/logos-storage-module`](https://github.com/logos-co/logos-storage-module)
is what apps call from Basecamp. The mix path-selection research is public and readable at
[forum.research.logos.co](https://forum.research.logos.co/t/mix-path-selection/721).

## Blockchain

This is the one where there was no good earlier answer to point at.

Communicating and archiving both had decentralised versions that worked and were lost.
Agreeing never had one. When the internet needed to settle "is this really that website"
or "where does this name point", it built hierarchies — certificate authorities, the domain
name system — and those hierarchies are exactly the chokepoints that DigiNotar and domain
seizure exploit. Open-membership consensus, agreement among people who haven't been
vouched for by anybody, was an unsolved problem until Bitcoin in 2008.

Bitcoin solved it, and made one trade that has aged badly for this room in particular: it
put every transaction in a permanent, globally readable, perfectly correlatable ledger.
Logos Blockchain — the continuation of Nomos — is an attempt to keep the solution and undo
that trade. Three things distinguish it, and the third matters most here.

**It has two layers.** *Bedrock* is the base: it provides consensus and data availability,
and it is deliberately kept minimal. *Zones* are lightweight chains built on top, where
applications actually run. The first one is the **Logos Execution Zone (LEZ)**. The split
means an application's activity doesn't have to congest, or be constrained by, the base
layer — and different communities can run different zones with different rules while
settling to the same base.

**Consensus is private proof-of-stake.** The protocol is called **Cryptarchia**. In a normal
proof-of-stake chain, being selected to propose a block is a public event: everyone can see
which validator was picked, and therefore who holds how much stake. Cryptarchia runs the
leadership election *locally, on each node*, and the winner proves in zero knowledge that
they legitimately won — without revealing which participant they are or how much they hold.

**Message routing is mixed.** A layer called **Blend** obscures the path messages take
through the network, so you can't identify a proposer by watching where a block first
appeared. Proposer anonymity is worthless if the network layer gives you away, so both are
needed. This is the mix-network idea David Chaum published in 1981 — the same lineage that
produced Tor — applied to block propagation.

> **What this means for organising**
>
> Start with what a shared ledger is *for* in a movement: a membership roll, a treasury,
> a vote, a decision record. Today these live with a bank, a platform, or a trusted
> individual — every one of which is a chokepoint and a liability.
>
> But as noted above, the standard blockchain answer has been a bad trade for activists
> specifically. A permanent, globally readable record of who funded what and who voted how
> is not a privacy nuisance in much of the world — it's a target list. Plenty of movements
> have looked at public-ledger governance tools, done that arithmetic correctly, and walked
> away.
>
> The privacy work above is aimed squarely at that trade. Proposer anonymity means helping
> secure the network doesn't announce that you're doing it, or how much you hold.
> Private transfers mean supporting something financially isn't a public act. That's the
> pitch: the resilience of a shared ledger without the ledger becoming evidence.

> **Honest status**
>
> This is the least mature layer and the fastest-moving. The current release is **testnet
> v0.2.1**, with v0.3 already scoped — real software, real running nodes, no real money, and
> things break. Recent work has been on
> making the execution zone's sequencing decentralised (it started out with a single
> sequencer), on consensus stability, and — worth noting for anyone thinking in decades — on
> a post-quantum migration strategy for the whole stack. Documentation is explicitly
> in draft. It is a great place to experiment and a bad place to put anything that matters
> yet. Say this plainly; the credibility you spend overselling here is spent for good.

**Where to go next:** [`logos-blockchain/logos-blockchain`](https://github.com/logos-blockchain/logos-blockchain)
for the node, [`logos-blockchain/logos-execution-zone`](https://github.com/logos-blockchain/logos-execution-zone)
for the zone where apps run, and [roadmap.logos.co/testnets](https://roadmap.logos.co/testnets)
for what each testnet actually contains, including release notes. Anyone who wants to write a program for LEZ should
look at [`logos-co/spel`](https://github.com/logos-co/spel) — a framework in the spirit of
Anchor for Solana, where you annotate your logic and it generates the interface, the CLI and
the deployment path for you.

---

## Basecamp

Everything above is infrastructure. **Logos Basecamp is the thing you open.**

It's a desktop application — Linux and macOS, downloadable as a single file — and the best
way to understand it is that it's less like an app and more like a *phone*. It doesn't do
much on its own. What it does is host **modules**, and let you install more of them.

A module comes in two halves, and the split is the important idea:

- A **core module** holds the logic — the engine, the crypto, the network protocol, the
  rules. It has no user interface at all.
- A **UI module** is a thin view that draws what the core module tells it and passes clicks
  back. It holds no logic of its own.

The reason to separate them is that the same core module runs in two completely different
places without changing a line. Behind the desktop UI, when someone is looking at it — and
standing alone as a **headless** process on a server or a Raspberry Pi, when nobody is,
driven by a command-line tool called `logosctl`. One implementation, two front ends, no drift between
what the app does and what the always-on node does.

Modules also *use each other*. A chat app doesn't implement peer-to-peer networking; it
declares a dependency on the Delivery module and calls it. A file-sharing app doesn't
implement content addressing and peer discovery; it calls the Storage module. And the Package Manager module is how
new modules arrive — a catalogue you browse and install from inside Basecamp, the way you'd
install an app on a phone.

### What stops an app doing something you didn't ask for

The obvious question about a system that installs other people's code is what that code is
then allowed to do. This is where a lot of Basecamp's current engineering effort is going,
and three of the rules are worth knowing because they're the ones that protect a user rather
than a developer.

**Modules ask; people decide.** A module can request a signature — to authorise a
transaction, say — but it cannot produce one. The signing key is derived only when a person
types the password into an approval screen showing what they're signing, and it's wiped
before the call returns. There is deliberately no "unlocked" state that a module can take
advantage of afterwards, which was precisely the hole that got closed this summer.

**Apps can talk to each other, but only along declared lines.** One app can ask another to
do something, and the request goes through the host, which checks that the caller declared
that it uses that capability in the first place. An app can't forge a reply to itself, and
it never gets a handle on whoever answered.

**Permissions have a direction, and packages are signed.** Recent work separated inbound from
outbound grants — previously, A being allowed to call B silently meant B could call A — and
tightened package signature checking so a package can't satisfy a pinned identity with a
signature that doesn't actually verify.

> **What this means for organising**
>
> This is where the stack stops being an argument and becomes a tool.
>
> It means a small group can build something for one specific need — a decision log, a
> mutual aid roster, a secure drop for testimony — without building a network, a storage
> system, or a chat protocol first. Those already exist as modules. You build the part that
> is actually about your situation, and it inherits privacy and censorship-resistance from
> the layers underneath.
>
> It also means the thing you build is **distributable**. It isn't a fork of a codebase
> somebody has to compile. It's a package another group can install, in an app they already
> have, in a few clicks. That is the difference between a tool your collective uses and a
> tool a movement uses.

> **On trusting what you install**
>
> "Install this module" is a request for trust, and the answer shouldn't have to be "I read
> the source". A permission model is what lets an app you installed to run a rota be unable
> to read the app holding your treasury, or to spend from it without a human looking at a
> screen and agreeing.
>
> The honest version too: this is being actively hardened, which means holes are being found.
> The ones described above were real and were closed within the last few weeks. That is what
> a security model under development looks like, and it beats silence — but it argues for
> growing into this as it matures, rather than putting your most sensitive material on it
> this month.

> **Honest status**
>
> Basecamp works and you can download it today. It is early: the module catalogue is small,
> the developer experience has sharp edges, and the two published tutorials will take a
> capable developer an afternoon rather than an hour. But the architecture is real and the
> shipped modules — wallet, chat, storage, delivery, package manager — genuinely run.

**Where to go next:** [`logos-co/logos-basecamp`](https://github.com/logos-co/logos-basecamp) —
prebuilt Linux AppImage and macOS DMG on the releases page. Then
[`logos-co/logos-modules`](https://github.com/logos-co/logos-modules) to see what already
exists to build on.

---

## Running a node

"Run a node" covers three different motivations, and separating them is the single best way
to stop the conversation getting confused. The good news, as of the current release, is that
operationally they have converged: **one tool, `logosctl`, runs one Logos node and the
modules inside it** — blockchain, storage and delivery together, in a single session. There
is a published node operator guide for testnet v0.2.1 that pins every package version and
gives copy-paste commands.

**1. To take part in consensus.** The blockchain module helps produce and validate the
shared record. This is the one with real requirements: zero-knowledge circuit files, keys,
bootstrap peers, and patience while it syncs.

The number worth saying out loud is the hardware target: a **Raspberry Pi 5 with around
64 GB of storage**. Not a datacenter, not a rented server with somebody's name on the
contract — a device on a shelf in a flat, on a normal connection. That is a deliberate design
goal and it is arguably the most politically significant fact in this session. A network that
needs a datacenter to participate in is a network that recentralises the moment it matters.

**2. To carry other people's traffic.** The delivery and storage modules don't produce
blocks; they make the network usable for everyone else. This is the neighbourly contribution
and it's underrated: a group running a well-connected delivery node is directly why somebody
nearby on a phone can use any of this at all. It's also the lowest-barrier way in.

**3. To have your own always-on peer.** Not for the network — for you. The same modules
running on a machine that never sleeps, so your group's shared state is reachable when
everyone's laptops are shut. This is what makes a collaborative tool work in practice rather
than only when two people happen to be online simultaneously.

> **What this means for organising**
>
> Node operation is the most concrete way to be part of this that doesn't involve writing
> code. A group that runs a node isn't a user of the infrastructure — it *is* the
> infrastructure. And unlike most infrastructure contributions it's legible: you can point at
> the box.
>
> Be candid that it's a **commitment** rather than a weekend. It wants uptime, updates, a bit
> of attention when things break, and somebody who cares whether it's still running. Five
> groups that actually maintain a node are worth more than fifty that set one up at a
> workshop and forget it.

> **Honest status**
>
> This got substantially better recently and it's worth saying so. Earlier in the year the
> headless story was genuinely a placeholder — the guide openly listed what it didn't know.
> There is now a real **node operator guide for testnet v0.2.1** with pinned package
> versions, the required ports, and commands that run. Expect rough edges, not a void.
>
> Two caveats. The published operator guide assumes a Linux host. And testnet means testnet:
> no real money, and version churn between releases is high — v0.3 is already scoped.

## Tools and resources

The last three minutes. Nobody remembers a list read aloud — point at the four doors and let
the handout carry the rest.

**If you want to understand more:** the [documentation](https://github.com/logos-co/logos-docs)
is organised by layer — blockchain, messaging, storage, core, apps — with task-shaped
"journeys" rather than API dumps. The [Eco Dev wiki](https://github.com/logos-co/ecosystem)
is where the ecosystem team works in the open: what's being built, what's wanted, and why.

**If you want to build something:** the two-part [tutorial](https://github.com/logos-co/logos-tutorial)
takes you from wrapping a library to a working Basecamp app.
[`logos-template-module`](https://github.com/logos-co/logos-template-module) and
[`counter_qml`](https://github.com/logos-co/counter_qml) are the smallest things that work —
start by changing them, not by starting from scratch. SDKs exist for C++, JavaScript, Nim
and Rust, so this is not a one-language ecosystem.

**If you want to run something:** the [Basecamp releases page](https://github.com/logos-co/logos-basecamp/releases/latest)
for the desktop app. For a node, start with the **node operator guide** at
[roadmap.logos.co/testnets](https://roadmap.logos.co/testnets) — it pins the exact package
versions for the current testnet, which is the difference between an evening and a weekend.

**If you have an idea and no one to build it with:** that is Session 2, and it's genuinely
the more important half. Come back for it.

> **Closing line, if you want one**
>
> None of this is finished, and you're not being shown it because it's finished. You're
> being shown it because the questions of what gets built on it — and who it's built for —
> are still open, and they're being answered right now by whoever turns up.
