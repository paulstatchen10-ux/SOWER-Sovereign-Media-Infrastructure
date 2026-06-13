# SOWER UI Specification

> Minimal by default. Always.

---

## Design Philosophy

The SOWER UI is not a product. It is a civic utility.

It does not optimize for engagement, session time, or return visits. It optimizes for the user finding what they came for and leaving satisfied. These are opposite design goals from every major platform currently operating.

The default state of the SOWER UI contains exactly three elements:
1. A search bar
2. A chronological feed of content from explicitly followed sources
3. An energy display showing the watt-hour cost of the current session

Nothing else is present by default. Everything else is opt-in.

---

## Core UI Constraints

These are locked alongside the platform design constraints:

- **No algorithmic feed** — ever, as a platform default
- **No autoplay** — the user initiates every piece of content
- **No engagement metrics displayed** — no view counts, no like counts, no trending sections
- **No notifications by default** — user enables if desired
- **No dark patterns** — no infinite scroll, no variable reward loops, no urgency manufactured by the interface
- **Energy display always visible** — watt-hours consumed this session, this stream

---

## Default Interface Layout

```
┌─────────────────────────────────────────────┐
│  SOWER          [search bar]        ⚡ 0.3Wh │
├─────────────────────────────────────────────┤
│                                             │
│  Following — chronological                  │
│                                             │
│  [Content from sources user follows,        │
│   newest first, no ranking applied]         │
│                                             │
│  [Load more]                                │
│                                             │
└─────────────────────────────────────────────┘
```

That is the complete default UI. No sidebar. No recommendations. No trending. No promoted content.

---

## Progressive Complexity Model

Users who want more functionality add it themselves. The platform provides:

- A local plugin API for client-side filter scripts
- A preference store (local, never server-side by default)
- Documentation for writing your own recommendation logic

Example user plugins (community-developed, not platform defaults):
- "Show me content from my region first"
- "Filter by energy cost under X watt-hours per hour"
- "Surface content my followed accounts have commented on"

---

## Energy Display

The energy display is a first-class UI element, always visible, never dismissible.

It shows:
- Watt-hours consumed this session
- Watt-hours consumed by the current stream
- Node location serving the current stream
- A simple comparison: "equivalent to running a 60W bulb for X minutes"

This is civic education, not a deterrent. Users who understand the real cost of media infrastructure make better decisions. That is the point.

---

## AI Interface

The AI query interface is a clean text input, available from any screen. It connects to whatever AI system the user has configured — local Ollama, Claude, Gemini, or any open API endpoint. The platform does not provide or prefer any AI system.

The AI interface can:
- Search and summarize content
- Describe what a ZERA file contains without rendering it
- Help the user write filter scripts for their personal recommendation layer
- Operate directly on ZERA latents for users who want generative features

---

## Accessibility

SOWER UI targets WCAG 2.1 AA compliance as a baseline. Civic infrastructure must be accessible to all community members.

---

## Implementation Notes

- Target: Progressive Web App (PWA) — works on any device, no app store required
- Framework: Preference for lightweight, dependency-minimal implementations
- Offline capability: Cached content playable without network connection
- Mobile first: Designed for the lowest-power device in the community first

---

## Contributing to UI Design

UI contributions are welcome. Before proposing any feature, answer this question:

> Does this feature serve the user's intent, or does it serve the platform's engagement metrics?

If the answer is engagement metrics — do not submit it.

---

*v0.1 — Paul Statchen, Santa Cruz CA, 2026*  
*AI Collaboration: Claude (Anthropic) assisted in drafting this document.*  
*"The worker is due their wages." — Luke 10:7*
