# ZERA Format Specification

> Universal Latent Media Container — v0.1 Draft  
> *zera* (זֶרַע) — Hebrew: seed, offspring, that which is planted and grows

---

## Concept

ZERA is a universal media container format designed for sovereign, federated media infrastructure. It stores a single latent-space mathematical representation of any media artifact — audio, video, image, 3D geometry, or future formats — from which any target resolution, format, or bitrate can be derived on demand.

**One upload. One file. Infinite derived outputs.**

---

## Design Principles

1. **Single source of truth** — one ZERA file per media artifact, forever
2. **Bidirectional derivation** — derive downward for streaming, derive upward for AI generation
3. **Format agnostic** — audio, video, image, 3D, and future media types in one container spec
4. **AI-native** — latent representation is directly usable by AI systems without rendering
5. **Energy efficient** — eliminates server-side transcoding and multi-copy storage overhead
6. **Open standard** — no royalties, no proprietary encoding, Apache 2.0

---

## The Problem ZERA Solves

Current platform storage model for a single 4K video upload:

| Quality Tier | Approx Size |
|---|---|
| 4K (2160p) | ~20 GB/hr |
| 1440p | ~10 GB/hr |
| 1080p | ~5 GB/hr |
| 720p | ~2.5 GB/hr |
| 480p | ~1 GB/hr |
| 360p | ~500 MB/hr |
| **Total stored** | **~39 GB/hr of source content** |

Multiply by billions of uploads. This is the primary driver of datacenter scale energy consumption globally.

**ZERA target:** One latent file at approximately the size of the highest quality tier. All other resolutions derived mathematically at playback time. Estimated storage reduction: 70–85% per media artifact.

---

## Theoretical Foundation

ZERA builds on three established principles:

### 1. Nyquist-Shannon Sampling Theory
Capture at the information ceiling of the source. Any lower-fidelity representation is mathematically derivable from the ceiling capture. This is how FLAC works for audio — one lossless master, any lossy output derived from it.

### 2. Scalable Vector Representation
SVG stores mathematical descriptions, not pixel grids. Resolution becomes irrelevant — the math renders correctly at any scale. ZERA applies this principle to time-based media through latent space encoding.

### 3. Neural Latent Space Compression
Modern generative AI models (video, audio, image) do not operate on pixels or samples — they operate on compressed latent representations. These latents are compact, mathematically rich, and contain enough information to reconstruct the original or generate related content. ZERA proposes storing these latents directly as the canonical format.

---

## File Structure (Proposed)

```
ZERA FILE
├── Header
│   ├── Magic bytes: ZERA
│   ├── Version: uint8
│   ├── Media type: enum (video, audio, image, geometry, mixed)
│   ├── Source resolution metadata
│   ├── Encoder model identifier
│   └── Content hash (for IPFS CID verification)
│
├── Latent Block
│   ├── Compressed latent tensor
│   ├── Encoder architecture reference
│   └── Quantization parameters
│
├── Metadata Block
│   ├── Title, description, author
│   ├── Nostr public key (creator identity)
│   ├── Timestamp
│   ├── License
│   └── Energy cost of encoding (watt-hours)
│
└── Index Block
    ├── Keyframe index (for video seeking)
    └── Derived format manifest (optional pre-computed lower-res caches)
```

---

## Derivation Modes

### Downward Derivation (Streaming)
Client requests stream → specifies target resolution and bitrate → client-side decoder derives output from latent in real time.

No server-side transcoding. No quality ladder stored on node. Compute cost moves to the client where it belongs.

### Upward Derivation (AI Generative)
AI agent requests raw latent → operates directly in latent space → extends, remixes, or generates new content without rendering intermediate human-facing output.

AI-to-AI content exchange skips the render layer entirely. Latents pass directly between models.

### Cross-Format Derivation (Future)
A ZERA file containing video latent → AI derives sheet music, 3D scene, text description, or audio-only extract from the same source latent.

This is the generative seed concept. One file. Many worlds.

---

## Encoder Architecture (Research Phase)

Three candidate approaches under consideration:

### Option A — Neural Codec (Preferred)
Train a codec model similar to architectures used in video generation (VQ-VAE, or similar). Encoder compresses source to latent. Decoder reconstructs at any resolution. Latent is the canonical format.

**Pros:** True single-file, AI-native, highest compression potential  
**Cons:** Requires training a new open model, client decoder complexity

### Option B — AV1 SVC (Near-term Practical)
Use AV1 Scalable Video Coding — an existing open standard with layered encoding. Not a true single latent, but a significant improvement over current multi-file approach.

**Pros:** Exists today, open royalty-free, hardware decode support growing  
**Cons:** Not true latent space, limited AI-native interoperability

### Option C — Wavelet Hybrid
Motion JPEG 2000 derivative with neural upscaling layer. Wavelet coefficients serve as the latent proxy.

**Pros:** Mathematically clean, progressive by design  
**Cons:** Legacy ecosystem, limited hardware support

**Current recommendation:** Prototype with Option B (AV1 SVC) for near-term demo. Research Option A as the target architecture.

---

## Open Research Questions

- [ ] What is the minimum viable neural encoder architecture for real-time client-side decoding on mobile hardware?
- [ ] How do we standardize the latent space so encoders from different models produce ZERA-compatible files?
- [ ] What is the actual compression ratio achievable vs. current multi-copy storage?
- [ ] How do we handle encoder model versioning as codec models improve over time?
- [ ] What are the compute requirements for upward derivation on consumer hardware?

---

## Energy Accounting Integration

Every ZERA encode operation logs:
- Watt-hours consumed during encoding
- Encoder hardware used
- Timestamp and node ID

This data is embedded in the ZERA metadata block and published to the node's energy ledger. Users see the true energy cost of their upload — not as a deterrent, as civic information.

---

## Relation to Existing Standards

| Standard | Relation to ZERA |
|---|---|
| FLAC | Conceptual ancestor — lossless master, derived lossy outputs |
| SVG | Conceptual ancestor — mathematical description, resolution-agnostic |
| AV1 SVC | Near-term implementation candidate |
| IPFS CID | ZERA files are content-addressed via IPFS |
| Motion JPEG 2000 | Historical reference — wavelet approach |
| HLS / DASH | Replaced by client-side derivation from ZERA latent |

---

## Contributing to ZERA Research

ZERA is the highest research priority in the SOWER project. If you work in:
- Neural video compression
- Codec design
- Latent space representation
- Distributed storage systems

...your contribution is directly needed. Open an Issue labeled `zera-research`.

---

*v0.1 — Paul Statchen, Santa Cruz CA, 2026*  
*AI Collaboration: Claude (Anthropic) assisted in drafting this document.*  
*"The worker is due their wages." — Luke 10:7*
