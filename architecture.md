# SOWER Platform Architecture

> Full stack specification — v0.1 draft

---

## Overview

SOWER is a seven-layer federated media stack. Each layer is independently replaceable. No layer creates vendor lock-in. The stack is designed to run on commodity civic hardware — the same hardware already owned and operated by municipal institutions.

---

## Layer Stack

```
┌──────────────────────────────────────────────────────────────┐
│  LAYER 7 — UI                                                │
│  Minimal by default. No algorithmic feed. User-controlled.   │
├──────────────────────────────────────────────────────────────┤
│  LAYER 6 — AI API                                            │
│  Open. Any model. Claude, Gemini, local Ollama — all peers.  │
├──────────────────────────────────────────────────────────────┤
│  LAYER 5 — IDENTITY                                          │
│  Nostr-compatible. User owns private keys. No platform acct. │
├──────────────────────────────────────────────────────────────┤
│  LAYER 4 — FEDERATION                                        │
│  ActivityPub protocol. PeerTube-compatible. Node-to-node.    │
├──────────────────────────────────────────────────────────────┤
│  LAYER 3 — NODE                                              │
│  Municipal civic hardware. Libraries, schools, counties.     │
├──────────────────────────────────────────────────────────────┤
│  LAYER 2 — ENERGY                                            │
│  Per-node power metering. Public ledger. Real-time display.  │
├──────────────────────────────────────────────────────────────┤
│  LAYER 1 — STORAGE                                           │
│  IPFS content-addressed ZERA files. One file per artifact.   │
└──────────────────────────────────────────────────────────────┘
```

---

## Layer 1 — Storage

**Protocol:** IPFS (InterPlanetary File System)  
**Format:** ZERA universal latent container  
**Addressing:** Content hash (CID) — the file's identity is its content, not its location  
**Redundancy:** Handled by IPFS pinning across multiple nodes — no central copy  

Every piece of media is stored once as a ZERA file. The CID is permanent and globally resolvable. Nodes pin content they choose to serve. No node is required to pin everything.

---

## Layer 2 — Energy

**Purpose:** Radical transparency, not tokenization  
**Implementation:** Per-node power metering (smart PDU or software-based on dedicated hardware)  
**Publication:** Node publishes watt-hour consumption to an open ledger endpoint  
**User display:** Real-time watt-hour cost shown during every stream  

Energy data is never used for exchange or incentive economics. It is civic information — the same category as a utility meter reading.

---

## Layer 3 — Node

**Primary operators:** Libraries, schools, county IT departments, universities  
**Hardware baseline:** Any x86 machine capable of running Docker Compose  
**Reference implementation:** MESA platform (see github.com/paulstatchen10-ux/MESA)  
**Minimum viable node:** Docker Compose stack with IPFS, PeerTube, and energy metering agent  

Nodes do not require high-end hardware. A decommissioned workstation or a used mini PC is sufficient for a community-scale node. Bandwidth is the primary constraint, not compute.

---

## Layer 4 — Federation

**Protocol:** ActivityPub (same protocol as Mastodon, PeerTube)  
**Compatibility:** PeerTube federation out of the box  
**Node discovery:** DNS-based, no central registry  
**Content routing:** Federated — nodes share content metadata, not content itself  

A user on one SOWER node can follow, discover, and stream content from any other SOWER node. Content stays on its origin node. Metadata propagates across the federation.

---

## Layer 5 — Identity

**Protocol:** Nostr-compatible keypair identity  
**Key ownership:** User holds private key locally — no platform-controlled account  
**Portability:** Identity moves with the user across nodes  
**Privacy:** No required personally identifiable information  

Optional: users may remain fully anonymous, identified only by public key.

---

## Layer 6 — AI API

**Design principle:** AI systems are neighbors, not features  
**Interface:** Open REST API — same endpoints for human clients and AI agents  
**Model agnostic:** Claude, Gemini, GPT, local Ollama inference — all connect identically  
**ZERA integration:** AI agents may request raw latent data for generative operations  

No AI vendor receives preferential API access. The platform does not endorse or bundle any AI system.

---

## Layer 7 — UI

**Default state:** Search bar. Chronological feed from explicitly followed sources. Nothing else.  
**Algorithmic feed:** Not provided. Ever. Users who want recommendation logic install it locally as a plugin.  
**Customization:** Users define their own filter scripts. The platform executes them client-side.  
**Progressive complexity:** Every UI feature is opt-in. The minimum viable interface is permanent and always available.  

---

## Data Flow: Upload

```
User uploads source media
        ↓
ZERA encoder creates latent representation
        ↓
ZERA file content-addressed → IPFS CID generated
        ↓
CID published to origin node
        ↓
Federation layer propagates metadata to peer nodes
        ↓
Energy layer logs storage event watt-hours
```

---

## Data Flow: Stream

```
Client requests content by CID
        ↓
Nearest node with pin serves ZERA file
        ↓
Client-side decoder derives target resolution from latent
        ↓
Stream begins — no server-side transcoding
        ↓
Energy layer logs stream watt-hours → displayed to user
```

---

## Data Flow: AI Access

```
AI agent authenticates via open API
        ↓
Requests content by CID with latent flag
        ↓
Node serves raw ZERA latent representation
        ↓
AI operates directly on latent space
(no render required — AI-to-AI native format)
```

---

## Open Questions (Research Needed)

- [ ] ZERA encoder architecture — neural codec vs. wavelet vs. hybrid approach
- [ ] Latent space standardization — how do different AI models agree on a common latent format?
- [ ] Bandwidth incentive model without tokenization — reciprocal credit vs. pure civic participation
- [ ] Energy metering hardware requirements for municipal node operators
- [ ] Legal framework for municipal node operation under California public records law

---

*v0.1 — Paul Statchen, Santa Cruz CA, 2026*  
*AI Collaboration: Claude (Anthropic) assisted in drafting this document.*  
*"The worker is due their wages." — Luke 10:7*
