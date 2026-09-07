# λ | Logos Tech Stack — slides outline

Session 1, 30 minutes, ~17 slides. Bullets are what goes *on* the slide.
Italics are the point to land, not text to display.

Full script: [`01-logos-tech-stack.md`](01-logos-tech-stack.md)

---

**1 · Title** — 0'

- λ | Logos Tech Stack
- Activist Builder Training

---

**2 · Three ancient needs** — 1'

- Communicate
- Archive
- Agree

*Everything in the stack comes from these.*

---

**3 · We already had answers** — 2'

- Usenet, email — 1980s
- Napster → Gnutella → BitTorrent — 1999
- Bank, platform, trusted treasurer

*Decentralised versions existed. Millions used them.*

---

**4 · What we lost** — 4'

- Usenet: spam → needed identity
- BitTorrent: swarm is public → the letter
- Ledgers: solved 2008 → permanently readable

*Same casualty every time: privacy.*

---

**5 · Standing on giants** — 6'

- Ouroboros · Solana model · RISC Zero · libp2p
- Foundations borrowed on purpose
- New work: privacy, unlinkability, anonymity, self-sovereignty, scale

*Not reinventing. Concentrating the new work in one place.*

---

**6 · Messaging** — 8'

- Peer-to-peer, built on libp2p
- Payload is opaque bytes
- Serves phones, not just servers
- Rate limiting without identity

*The network can't build a social graph out of you.*

---

**7 · Messaging — being added** — 10'

- libchat — encrypted conversations, groups
- libp2p-mix — hides who sent it

*Content encryption alone still leaves a pattern.*

---

**8 · Storage** — 12'

- Publish and fetch, no server
- Content addressed
- Availability follows interest

*Durability comes later. Not a vault yet.*

---

**9 · Storage — the real property** — 14'

- Publisher unlinkability
- Downloader unlinkability
- Caching nodes can deny knowing

*The dangerous act is often reading, not publishing.*

---

**10 · Blockchain** — 16'

- Bedrock (base) + Zones (apps run here)
- Cryptarchia — private leadership election
- Blend — hides who proposed

*Helping secure the network shouldn't announce that you are.*

---

**11 · Blockchain — LEZ** — 18'

- Public and private accounts, one address space
- Program written once, works across both
- Protocol enforces privacy, not the developer

---

**12 · Basecamp** — 20'

- The thing you actually open
- Hosts modules, installs more
- Like a browser in shape

*Plumbing nobody can install is a research project.*

---

**13 · Basecamp — not the browser's trust model** — 21'

- Web app: served by someone who sees you fetch it
- Can serve you different code than the auditor saw
- Basecamp: installed, signed, verified locally, repos you choose

---

**14 · Basecamp — what stops an app misbehaving** — 23'

- Modules ask; people approve
- Apps talk only along declared lines
- Packages signed

*No store. Nobody decides what you may install.*

---

**15 · Running a node** — 25'

- Take part in consensus
- Carry others' traffic
- Your own always-on peer
- One tool: `logosctl`

---

**16 · Raspberry Pi 5, 64 GB** — 27'

- Not a datacenter
- A box on a shelf

*A network that needs a datacenter recentralises the moment it matters.*

---

**17 · Where to go next** — 28'

- docs.logos.co
- roadmap.logos.co — weekly, candid
- Basecamp releases — download it
- Session 2: how to actually build

*None of this is finished. That's why you're being shown it.*
