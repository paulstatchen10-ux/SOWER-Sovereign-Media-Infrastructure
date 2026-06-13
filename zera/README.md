# ZERA Research Directory

This directory contains research notes, prototype code, and experimental implementations related to the ZERA universal latent container format.

See [`docs/ZERA_format_spec.md`](../docs/ZERA_format_spec.md) for the full specification.

---

## Current Status

**Phase: Pre-prototype research**

No production code yet. This directory is the staging ground for the first ZERA encoder/decoder prototype.

---

## Immediate Research Priorities

### 1. Encoder Candidate Evaluation
Compare AV1 SVC, neural codec, and wavelet hybrid approaches on:
- Compression ratio vs. current multi-copy storage
- Client-side decode compute requirements on mobile hardware
- AI-native latent interoperability

### 2. Latent Space Standardization
How do we define a common latent format that different encoder models can produce compatibly? This is the hardest unsolved problem in the ZERA spec.

### 3. Energy Cost Benchmarking
Measure actual watt-hours consumed per minute of video encoded under each candidate approach. This feeds directly into the platform energy transparency layer.

---

## How to Contribute Here

Drop research notes as markdown files. Name them descriptively:
- `encoder-candidate-av1-svc-notes.md`
- `latent-standardization-research.md`
- `energy-benchmark-results.md`

Prototype code goes in subdirectories named by approach:
- `zera/av1-svc/`
- `zera/neural-codec/`
- `zera/wavelet/`

---

*v0.1 — Paul Statchen, Santa Cruz CA, 2026*  
*AI Collaboration: Claude (Anthropic) assisted in drafting this document.*
