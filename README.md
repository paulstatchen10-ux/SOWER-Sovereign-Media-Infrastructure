# SOWER
### Sovereign Federated Media Infrastructure

> *"A sower went out to sow."* — Matthew 13:3  
> The infrastructure belongs to the neighbors.

---

SOWER is an open-source, federated media platform designed to replace centralized video and media infrastructure with a municipal-node backbone, zero tokenization, radical energy transparency, and a novel universal container format called **ZERA**.

Where existing platforms optimize for engagement, advertising revenue, and proprietary lock-in — SOWER optimizes for **sovereignty, legibility, and long-term civic resilience.**

---

## Core Design Constraints

These are architectural commitments, not preferences. Locked before implementation begins.

| Constraint | Commitment |
|---|---|
| **No tokenization. Ever.** | No convertible currency layer. No exchange-listed token. Energy accounting is for transparency only — never for exchange. |
| **Energy transparency** | Every node publishes actual power draw. Every stream shows watt-hour cost to the user in real time. |
| **Municipal node backbone** | Primary infrastructure is civic hardware — libraries, schools, county facilities, university nodes. |
| **Minimal by default** | Zero algorithmic feed. No engagement optimization. User adds complexity. Platform never does. |
| **AI-agnostic open API** | Any AI system connects as a peer neighbor. Human clients and AI agents are equivalent interface clients. |

---

## The ZERA Format

**ZERA** (from the Hebrew *zera*, זֶרַע — meaning *seed*) is the native media container format for SOWER.

Instead of storing 6–8 discrete quality copies of every media file, ZERA stores a single latent-space representation — a mathematical seed — from which any resolution, format, or bitrate is derived on demand at playback time.

- **Stream down** — derive 480p from the latent for a low-bandwidth mobile client
- **Generate up** — AI systems read the latent directly to extend, remix, or derive new formats
- **One file per piece of content** — content-addressed on IPFS, no redundant copies

See [`docs/ZERA_format_spec.md`](docs/ZERA_format_spec.md) for the full specification.

---

## Platform Architecture

```
┌─────────────────────────────────────────────────────┐
│                    SOWER STACK                      │
├─────────────────────────────────────────────────────┤
│  UI Layer        │ Minimal by default. No algo feed  │
│  AI API Layer    │ Open. Any model. Human = AI peer  │
│  Identity Layer  │ Nostr-compatible. User owns keys  │
│  Federation      │ ActivityPub / PeerTube protocol   │
│  Node Layer      │ Municipal civic hardware backbone │
│  Energy Layer    │ Per-node metering. Public ledger  │
│  Storage Layer   │ IPFS content-addressed ZERA files │
└─────────────────────────────────────────────────────┘
```

---

## Reference Implementation

The municipal node infrastructure reference is **MESA** (Municipal Enterprise Service Architecture):

👉 [github.com/paulstatchen10-ux/MESA---Municipal-Enterprise-Service-Architecture](https://github.com/paulstatchen10-ux/MESA---Municipal-Enterprise-Service-Architecture)

---

## Repository Structure

```
SOWER/
├── README.md
├── LICENSE
├── CONTRIBUTING.md
├── docs/
│   ├── architecture.md
│   └── ZERA_format_spec.md
├── zera/
│   └── README.md
├── node/
│   └── docker-compose.yml
└── ui/
    └── README.md
```

---

## License

Apache 2.0 — Copyright 2026 Paul Statchen

---

## AI Collaboration Attribution

Developed in collaborative dialogue with **Claude (Anthropic)**.  
Vision, design constraints, naming (SOWER / ZERA), and civic philosophy are original work by **Paul Statchen**.  
Claude assisted with technical articulation, specification language, and document structure.

> *"The worker is due their wages."* — Luke 10:7
