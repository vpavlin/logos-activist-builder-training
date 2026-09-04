# λ | Pointers & Glossary

Companion handout for both sessions. Written to be given out, not read aloud.

---

## Start here, depending on what you want

**"I just want to see it."**
Download Logos Basecamp — [releases page](https://github.com/logos-co/logos-basecamp/releases/latest),
Linux AppImage or macOS DMG. Open it, look at the Package Manager, install a module.

**"I want to understand the ideas."**
[logos.co/manifesto](https://logos.co/manifesto) for the why ·
[Farewell to Westphalia](https://logos.co/farewell-to-westphalia) for the political argument ·
[Why proposer anonymity](https://press.logos.co/article/why-proposer-anonymity) for one
concrete example of the privacy engineering.

**"I want to build something."**
[`logos-tutorial`](https://github.com/logos-co/logos-tutorial) — two parts, wrapping a
library then building a UI. Then [`logos-template-module`](https://github.com/logos-co/logos-template-module)
or [`counter_qml`](https://github.com/logos-co/counter_qml) — the smallest working things.
Change one of those rather than starting from an empty directory.

**"I want to run infrastructure."**
[Blockchain node releases](https://github.com/logos-blockchain/logos-blockchain/releases) —
binary, ZK circuits, and the current bootstrap peers are all in the release notes.
Quickstart guide is in [`logos-docs`](https://github.com/logos-co/logos-docs) under
`docs/blockchain/`. Expect to ask questions.

**"I have a need, not a project."**
Open an issue on [`logos-co/ecosystem`](https://github.com/logos-co/ecosystem/issues), or
raise it through a Logos circle. Describe the situation, not the feature.

---

## Naming: things have been renamed

Older material, blog posts and search results use the previous names. This trips people up
constantly.

| You'll see | It's now | What it is |
|---|---|---|
| Waku | **Logos Messaging** | Peer-to-peer messaging network |
| Codex | **Logos Storage** | Decentralised, durable storage |
| Nomos | **Logos Blockchain** | Consensus layer (Bedrock + Zones) |
| Logos App | **Logos Basecamp** | The desktop app that hosts modules |

One that is *not* a rename, and catches people out: **NSSA** is a legacy prefix still used
inside the Logos Execution Zone code (the `nssa_core` crate, the `NSSA_WALLET_HOME_DIR`
environment variable). It isn't a separate product and it isn't the old name for LEZ — it's
just what some of the internals are still called.

---

## Glossary

**Bedrock** — the base layer of Logos Blockchain. Consensus and data availability, kept
deliberately minimal.

**Blend** — the routing layer that mixes messages so you can't identify who sent one by
watching the network.

**Circle** — a local Logos group. The grassroots on-ramp; ideas surface here and route into
the ecosystem process.

**Core module** — a Basecamp module that holds logic and has no UI. Runs behind the desktop
app *and* headless on a server, unchanged.

**Cryptarchia** — Logos Blockchain's Private Proof of Stake consensus. Leadership election
runs locally on each node; the winner proves in zero knowledge that they won, without
revealing who they are or what they hold.

**Eco Dev** — Ecosystem Development. The team connecting the technology to the people who
might use it, in both directions.

**Erasure coding** — redundancy cleverer than copying: a file becomes fragments such that
any sufficiently large subset rebuilds the whole. Lose a third, lose nothing.

**FURPS+** — the shape of a requirements document here: Functionality, Usability,
Reliability, Performance, Supportability — plus privacy, anonymity and censorship-resistance.

**GossipSub** — the libp2p protocol that spreads messages peer to peer, at the core of
Logos Messaging.

**Lambda Prize (ꟛPrize)** — a prize for hard, ambitious problems where the *solution isn't
dictated*. You define the approach.

**libchat** — the secure messaging layer built on Logos Messaging: identity,
introduction bundles, private one-to-one conversations, delivery acknowledgements.
Reachable in Basecamp as the ChatSDK module. Content encryption, so every app doesn't
have to invent its own.

**libp2p-mix** — mixnet routing being wired into the peer-to-peer layer. Messages hop
through a pool of relays that each peel one layer of encryption and hold the message
briefly, so a network-wide observer can't match what went in to what came out. Chaum's
1981 idea, same lineage as Tor.

**LEE** — Logos Execution Environment. The machinery inside LEZ that provides the
public/private account split. You'll see LEE and LEZ used close together: roughly, LEE is
the capability, LEZ is the chain that offers it.

**LEZ** — Logos Execution Zone. The first Zone; where applications and smart contracts run.
Its distinguishing feature is that public and private accounts are handled uniformly — a
program is written once and works across both, with privacy enforced by the protocol rather
than by the developer remembering to ask for it.

**libp2p** — the peer-to-peer networking toolkit underneath both the messaging network and
the blockchain.

**logoscore** — the runtime that runs Basecamp modules headless, with no UI. How you get an
always-on peer.

**Module** — a Basecamp component. Core modules hold logic; UI modules draw. Modules declare
dependencies on each other and are installed via the Package Manager.

**Red Team** — Eco Dev's stress-testing role. Permission to break it, permission to be
confused, permission to say it isn't ready.

**RFP** — Request for Proposals. Outsourced development where the requirements are already
known.

**SPEL** — the framework for writing programs for LEZ. Annotate your logic; get the
interface, CLI and deployment generated.

**Zone** — a lightweight chain on top of Bedrock, where applications actually run.

---

## Repositories

### The four layers

| | Repo |
|---|---|
| Messaging | [`logos-messaging/logos-delivery`](https://github.com/logos-messaging/logos-delivery) |
| Messaging — secure chat layer (libchat) | [`logos-messaging/logos-chat`](https://github.com/logos-messaging/logos-chat) |
| Messaging — mix protocol (libp2p-mix) | [`vacp2p/nim-libp2p`](https://github.com/vacp2p/nim-libp2p) |
| Storage | [`logos-storage/logos-storage-nim`](https://github.com/logos-storage/logos-storage-nim) |
| Blockchain | [`logos-blockchain/logos-blockchain`](https://github.com/logos-blockchain/logos-blockchain) |
| Execution Zone | [`logos-blockchain/logos-execution-zone`](https://github.com/logos-blockchain/logos-execution-zone) |
| Basecamp | [`logos-co/logos-basecamp`](https://github.com/logos-co/logos-basecamp) |

### Building on it

| | Repo |
|---|---|
| Tutorial (start here) | [`logos-co/logos-tutorial`](https://github.com/logos-co/logos-tutorial) |
| Module template | [`logos-co/logos-template-module`](https://github.com/logos-co/logos-template-module) |
| Simplest UI example | [`logos-co/counter_qml`](https://github.com/logos-co/counter_qml) |
| Existing modules (catalogue) | [`logos-co/logos-modules`](https://github.com/logos-co/logos-modules) |
| Dev CLI / local dev environment | [`logos-co/logos-scaffold`](https://github.com/logos-co/logos-scaffold) |
| Multi-repo dev environment | [`logos-co/logos-workspace`](https://github.com/logos-co/logos-workspace) |
| Smart contract framework (LEZ) | [`logos-co/spel`](https://github.com/logos-co/spel) |
| UI design system | [`logos-co/logos-design-system`](https://github.com/logos-co/logos-design-system) |

**SDKs** — not a one-language ecosystem:
[C++](https://github.com/logos-co/logos-cpp-sdk) ·
[JavaScript](https://github.com/logos-co/logos-js-sdk) ·
[Nim](https://github.com/logos-co/logos-nim-sdk) ·
[Rust](https://github.com/logos-co/logos-rust-sdk)

### Process, docs and planning

| | Where |
|---|---|
| Documentation | [`logos-co/logos-docs`](https://github.com/logos-co/logos-docs) |
| Eco Dev wiki (open working notes) | [`logos-co/ecosystem`](https://github.com/logos-co/ecosystem) · [ecosystem.logos.co](https://ecosystem.logos.co) |
| Ideas, needs, desired projects | [ecosystem issues](https://github.com/logos-co/ecosystem/issues) |
| Testnet v0.1 scope | [roadmap.logos.co/testnets/v01](https://roadmap.logos.co/testnets/v01) |
| RFPs | [`logos-co/rfp`](https://github.com/logos-co/rfp) |

---

## The ancestors

Every idea in Session 1 has a lineage, and all of it predates the word "blockchain". Useful
for anyone who wants to check that this is a continuation of internet history rather than a
departure from it — and genuinely good reading in its own right.

| Year | Thing | Why it matters here |
|---|---|---|
| 1980 | **Usenet** | Decentralised discussion at scale, no owner. Drowned in spam, because an open network with no accounts couldn't say "enough". |
| 1981 | **Chaum's mix networks** | The original idea that you can hide *who is talking to whom*, not just what they said. Ancestor of Tor, and of Blend. |
| 1982 | **SMTP / email** | The great decentralised success — and the cautionary tale. Still open by design; centralised in practice by the economics of spam defence. |
| 1984 | **FidoNet** | Store-and-forward between dial-up BBSs. Solved intermittent connectivity forty years before anyone said "edge node". |
| 1997 | **Hashcash** | Rate limiting without identity, invented for email spam. Direct ancestor of how Logos Messaging limits flooding. |
| 1997 | **The Cathedral and the Bazaar** | Eric Raymond's essay. The collaboration model Session 2 describes. |
| 1999 | **Napster** | Proved people would share peer-to-peer. Died because a central index is a single address for a court order. |
| 2000 | **Gnutella** | Removed the index in response — and discovered fully naive decentralisation doesn't scale. |
| 2000 | **Freenet** | Censorship-resistant publishing built explicitly for dissidents. Cryptography held up; usability didn't. |
| 2001 | **BitTorrent** | Got the balance right, still with us. Never solved permanence — files die when seeding stops. |
| 2002 | **Kademlia** | The distributed hash table that survived the academic wave. It's the peer discovery in Logos Blockchain today. |
| 2002 | **Tor** | Chaum's mix networks, shipped and actually used by the people who needed them. Two Logos efforts descend from the same idea: libp2p-mix in Messaging, and Blend in the blockchain. |
| 2008 | **Bitcoin** | Solved open-membership consensus. Made one trade — a permanently public ledger — that Logos Blockchain is trying to undo. |
| 2011 | **DigiNotar** | A compromised certificate authority used to read ~300,000 Iranians' email. What a trust hierarchy fails like, with activists as the victims. |

The point to carry out of this table: **the ideas aren't new and they weren't wrong.** What
has changed is that the pieces can now be assembled into something a person can install.

---

## Maturity, honestly

Useful to hand over, because it stops people bouncing off the wrong entry point.

| Layer | Where it's at |
|---|---|
| **Messaging** | Most mature by a distance. Years of running network behind it. Start here if you want something that works today. |
| **Storage** | Network and module both real. Long-term persistence economics still being settled on testnet. |
| **Basecamp** | Works, downloadable, genuinely runs. Early: small catalogue, sharp edges in developer experience. |
| **Blockchain** | Testnet v0.1. Real software, no real money, fast-moving, docs in draft. Great to experiment on, not to depend on. |
| **Docs** | Actively being built. Several guides carry explicit "early draft" banners; the headless-node guide is closer to a placeholder. Following one and reporting where it broke is a requested contribution. |

---

## Getting help

- **Discord `#ecodev`** — main channel for ecosystem questions. Per-team channels exist for
  deeper protocol questions.
- **Office hours** — recurring scheduled slot for direct questions.
- **GitHub issues** — bugs on the specific repo; needs and ideas on
  [`logos-co/ecosystem`](https://github.com/logos-co/ecosystem/issues).

Three things worth repeating from Session 2, because people don't believe them the first
time:

1. Getting stuck and saying so **is** the contribution. You don't need to diagnose it.
2. Supporting people building on Logos is a listed responsibility of the Red Team, not a
   favour.
3. Your confusion is only visible to you while you're new. It's the most perishable thing
   you have to offer.
