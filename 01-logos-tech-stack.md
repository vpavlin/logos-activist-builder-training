# λ | Logos Tech Stack

**Session 1 — Eco Dev — 30 minutes**

> Covers: intro to Logos Blockchain, Messaging, Storage and Basecamp · running a node
> basics · existing tools and developer resources.

## Run of show

| Time | Section | Notes |
|------|---------|-------|
| 0–4' | [Three ancient needs](#three-ancient-needs) | The framing. Do not rush this — everything else hangs off it. |
| 4–9' | [Messaging](#messaging) | |
| 9–13' | [Storage](#storage) | |
| 13–19' | [Blockchain](#blockchain) | Densest section. *(Zones/LEZ detail cuts first.)* |
| 19–24' | [Basecamp](#basecamp) | The "where a human touches it" answer. |
| 24–27' | [Running a node](#running-a-node) | Shape, not steps. *(cut to 1' if needed)* |
| 27–30' | [Where to go next](#tools-and-resources) | Never cut. This is the whole point. |

**Learning outcomes.** By the end, a participant can (1) name the four pieces and say what
each is *for*, in their own words; (2) explain why they are separate things rather than one
thing; (3) say what "running a node" would mean for them concretely; (4) name one place to
go to start.

---

## Three ancient needs

All of the Logos Tech Stack comes from ancient (in internet terms) needs to communicate,
archive and reach consensus. There have been attempts to solve this — see the original
Ethereum whitepaper and the early "Ethereum, Whisper, Swarm" trinity — which never came to
fruition though.

That trinity is worth a moment, because it explains the shape of what follows. The idea was
that a full decentralised application needs three separate things: a way for people and
programs to *talk* (Whisper), a way to *keep* things (Swarm), and a way to *agree* on
something (Ethereum itself). Only the third one ever really shipped. So for a decade the
industry has been building applications where the "agree" part is beautifully
decentralised, and the talking and the keeping quietly run on Amazon.

Logos is a bet that you have to build all three, together, and that the interesting part is
what happens when they are actually available at the same time.

| Ancient need | Logos layer | One-line |
|---|---|---|
| Communicate | **Logos Messaging** | Get a message to someone without anyone owning the route. |
| Archive | **Logos Storage** | Keep something so it stays available and nobody can quietly delete it. |
| Reach consensus | **Logos Blockchain** | Agree on a shared record nobody has to be trusted to maintain. |
| *(and: be usable)* | **Logos Basecamp** | The place where an actual human touches all of the above. |

The fourth row is not an ancient need — it's the honest admission that the first three are
plumbing. Plumbing that nobody can install is a research project. Basecamp is the answer to
"and then what does a person open?"

> **What this means for organising**
>
> Think about the last campaign you ran. Where did the conversations live? Where did the
> documents live? Where did the money and the membership list live? For almost everyone the
> answer is: on three platforms, each of which can close your account on a Tuesday, each of
> which can be compelled to hand over what it holds, and none of which you can move off
> without losing your history.
>
> The stack below is an attempt to give a movement its own answer to those three questions —
> one that doesn't get better or worse depending on who is currently in office.

---

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

**Rate limiting without identity.** The hard problem in an open, anonymous network is spam:
if anyone can publish and nobody has an account, what stops a flood? The usual answer is
accounts, which means identity, which is exactly what you were trying to avoid. Logos
Messaging instead uses zero-knowledge rate limiting — a peer proves it is within its
allowance without revealing who it is. Exceed the allowance and the proof itself exposes
you. It's a bouncer who can count but can't see faces.

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
> Encryption of the *content* is the application's job. Logos Messaging's contribution is
> that the network can't build a social graph out of you.

> **Honest status**
>
> This is the most mature layer in the stack by a wide margin — it is the continuation of
> the Waku project, with years of running network behind it, and it is already carrying real
> traffic. If you want something that works today, start here.

**Where to go next:** [`logos-messaging/logos-delivery`](https://github.com/logos-messaging/logos-delivery)
is the node implementation. Inside Basecamp it appears as the **Delivery module**, which
apps call rather than speaking the protocol themselves.

---

## Storage

Logos Storage is the archive layer — the answer to "and where does the thing actually live?"
It is the continuation of the Codex project, and it does something more specific than
"decentralised Dropbox".

When you put a file in, it isn't handed to one machine to look after. It's split into pieces
with **erasure coding**, which means redundancy that is cleverer than making copies: a file
is expanded into a set of fragments such that any sufficiently large subset can rebuild the
whole thing. Lose a third of the fragments and the file is still perfectly intact. Spread
those fragments across unrelated machines in unrelated jurisdictions and there is no single
door for anyone to knock on.

The second property is **content addressing**. A file's name is derived from its contents, so
asking for it is asking for exactly those bytes and nothing else. You can't be served a
quietly-edited version — the address wouldn't match. For an archive, this is the whole ball
game: it makes the record tamper-evident by construction rather than by trust.

The third is **proofs of durability**. Storage providers are periodically challenged to
demonstrate they still hold what they claimed to hold, and can't pass the challenge by
having deleted it. This is what makes the network's promise checkable instead of aspirational.

> **What this means for organising**
>
> Two use cases, and they're different.
>
> *Publishing that can't be quietly pulled.* A report, a dataset, a piece of evidence, a
> testimony. Once it's addressed by its content and spread across the network, taking it
> down is not a phone call to a hosting company — and any attempt to substitute a doctored
> version produces a different address, visibly.
>
> *An archive that outlives the organisation.* Movements fragment, funding stops, the person
> with the Google Drive password moves on. Content-addressed storage separates "does this
> still exist" from "does this particular group still exist".
>
> The discipline this demands: **encrypt before you upload.** Censorship resistance and
> confidentiality are different properties, and the first one is the one you're being handed.
> Something that can't be deleted also can't be un-published if you put the wrong thing in it.

> **Honest status**
>
> The storage network exists and the Basecamp module exists. Persistence is ultimately an
> economic question — data survives because providers are incentivised to keep it — and those
> incentives are still being worked out on testnet. Treat it today as a capable system to
> build against, not yet as somewhere to put the only copy of something irreplaceable.

**Where to go next:** [`logos-storage/logos-storage-nim`](https://github.com/logos-storage/logos-storage-nim)
for the network; [`logos-co/logos-storage-module`](https://github.com/logos-co/logos-storage-module)
for the Basecamp module apps call.

---

## Blockchain

Logos Blockchain — the continuation of Nomos — is the consensus layer: the shared record
that everyone can verify and nobody has to be trusted to maintain. Three things distinguish
it, and the third is the one that matters most to this room.

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
through the network, so you can't identify a proposer by watching where the block first
appeared. Proposer anonymity is worthless if the network layer gives you away, so both are
needed.

> **What this means for organising**
>
> Start with what a shared ledger is *for* in a movement: a membership roll, a treasury,
> a vote, a decision record. Today these live with a bank, a platform, or a trusted
> individual — every one of which is a chokepoint and a liability.
>
> But the standard blockchain answer has always been a bad trade for activists specifically.
> A public ledger is a permanent, globally-readable, perfectly-correlatable record of who
> funded what and who voted how. For a lot of the world that isn't a privacy nuisance, it's
> a target list. Plenty of movements have correctly looked at public-ledger governance tools
> and concluded the surveillance cost outweighs the censorship-resistance benefit.
>
> The privacy work above is aimed squarely at that trade. Proposer anonymity means helping
> secure the network doesn't announce that you're doing it, or how much you hold.
> Private transfers mean supporting something financially isn't a public act. That's the
> pitch: the resilience of a shared ledger without the ledger becoming evidence.

> **Honest status**
>
> This is the least mature layer and the fastest-moving. It is on **testnet v0.1** — real
> software, real running nodes, no real money, and things break. Documentation is explicitly
> in draft. It is a great place to experiment and a bad place to put anything that matters
> yet. Say this plainly; the credibility you spend overselling here is spent for good.

**Where to go next:** [`logos-blockchain/logos-blockchain`](https://github.com/logos-blockchain/logos-blockchain)
for the node, [`logos-blockchain/logos-execution-zone`](https://github.com/logos-blockchain/logos-execution-zone)
for the zone where apps run, and [roadmap.logos.co/testnets/v01](https://roadmap.logos.co/testnets/v01)
for what testnet v0.1 actually contains. Anyone who wants to write a program for LEZ should
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
under a runtime called `logoscore`. One implementation, two front ends, no drift between
what the app does and what the always-on node does.

Modules also *use each other*. A chat app doesn't implement peer-to-peer networking; it
declares a dependency on the Delivery module and calls it. A file-sharing app doesn't
implement erasure coding; it calls the Storage module. And the Package Manager module is how
new modules arrive — a catalogue you browse and install from inside Basecamp, the way you'd
install an app on a phone.

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

"Run a node" is one phrase covering three quite different acts, and conflating them is the
single most common source of confusion. Separate them explicitly.

**1. Run a blockchain node.** You are participating in consensus — helping produce and
validate the shared record. The shape of it: download the node binary and the
zero-knowledge circuit files it needs, run `init` with a couple of bootstrap peers to
generate your keys and config, then start the node pointed at that config. Ask the testnet
faucet for tokens, and watch it sync.

The number worth saying out loud: the target hardware is a **Raspberry Pi 5 with about
64 GB of storage**. Not a datacenter, not a rented server with someone's name on the
contract. A device on a shelf in a flat, on a normal connection. That is a deliberate design
goal and it is the most politically significant fact in this session — a network that needs
a datacenter to participate in is a network that recentralises the moment it matters.

**2. Run messaging or storage infrastructure.** You are not producing blocks; you're
carrying other people's traffic or holding other people's data. This is the neighbourly
version: a group that runs a well-connected messaging node is directly making the network
usable for everyone nearby on a phone. It's the lowest-barrier way to contribute
infrastructure, and it's underrated.

**3. Run your own always-on peer.** Not for the network — for *you*. Basecamp's modules
running headless under `logoscore` on a machine that never sleeps, so your group's shared
state is reachable when the laptops are shut. This is what makes a collaborative tool
actually work in practice rather than only when two people happen to be online at once.

> **What this means for organising**
>
> Node operation is the most concrete way to be part of this that doesn't require writing
> code. A group that runs a node is not a user of the infrastructure — it *is* the
> infrastructure. And unlike most infrastructure contributions, it's legible: you can point
> at the box.
>
> The thing to be candid about is that operating a node is a **commitment**, not a weekend:
> it wants uptime, updates, a bit of attention when things break, and someone who cares.
> Better to have five groups who actually maintain a node than fifty who set one up at a
> workshop and forget it.

> **Honest status**
>
> The blockchain node quickstart is published but carries an explicit "early draft, may be
> incomplete or incorrect" banner. The headless-mode guide is more placeholder than guide
> right now. Anyone going down this path today should expect to ask questions in Discord
> rather than follow a document start to finish — and those questions are genuinely wanted,
> because they're what turns the draft into a guide. Frame it as contributing, not as
> struggling.

---

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
for the desktop app; the [blockchain releases page](https://github.com/logos-blockchain/logos-blockchain/releases)
for the node binary and its bootstrap peers.

**If you have an idea and no one to build it with:** that is Session 2, and it's genuinely
the more important half. Come back for it.

> **Closing line, if you want one**
>
> None of this is finished, and you're not being shown it because it's finished. You're
> being shown it because the questions of what gets built on it — and who it's built for —
> are still open, and they're being answered right now by whoever turns up.
