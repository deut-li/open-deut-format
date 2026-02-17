# .deut Open Asset Format

![Status](https://img.shields.io/badge/Status-Beta_1.0-black?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-yellow?style=flat-square)
![Standard](https://img.shields.io/badge/Standard-Open_Asset-blue?style=flat-square)

> **"Don't type. Snap it in."** — The Digital Negative for Generative Arts.

---

## 🏛 The Manifesto: Order from Chaos

Professional generative workflow is currently broken. Designers are stuck in a loop of "prompt roulette"—tweaking keywords and losing track of iterations.
* **PNGs** are black boxes; metadata is lost on compression or conversion.
* **Txt files** are unstructured and disjointed.
* **Intent** is mixed with **Implementation**.

**We are establishing the .deut format as a new industry standard.**
It is a structured container designed not just to *store* prompts, but to *engineer* them. It treats your prompts like blueprints, enabling version control, non-destructive editing, and enterprise-grade collaboration.

---

## 💎 The Architecture

Unlike simple text files, a `.deut` file separates the **Human Intent** from the **Machine Parameters**.

### Core Principles
1.  **Non-Destructive Editing:** Change the lighting or camera angle without rewriting the entire prompt logic. The format preserves the original user inputs separately from the LLM-compiled string.
2.  **Provenance & Integrity:** A built-in SHA-256 fingerprint mechanism acts as a seal of authenticity, preventing silent tampering of assets.
3.  **Platform Agnostic:** While designed for the *Deut.li* ecosystem, the schema is open. It creates a universal language between different models and tools.

---

## 🧬 File Structure (The DNA)

A `.deut` file is a rigid JSON object.

```json
{
  "meta": {
    "version": "1.0",
    "created_at": "2023-10-27T10:00:00Z",
    "author_hash": "..." 
  },
  "input_dna": {
    "description": "User's high-level concept",
    "subject": "concrete monolith",
    "action": "hovering",
    "environment": "dense pine forest",
    "lighting": "overcast dusk",
    "composition": "rule of thirds"
  },
  "system_params": {
    "model_hash": "e6415c4892",
    "sampler": "DPM++ 2M Karras",
    "steps": 30,
    "seed": 382985710478200
  },
  "fingerprint": "a1b2c3d4..." // Proof of Integrity
}
```

### 🔐 Fingerprint Protocol (Security)
To verify the integrity of a `.deut` file, the system reconstructs the hash from the `input_dna` fields. This ensures that the file you load creates exactly what the author intended.

**Algorithm:**
1.  **Normalize**: Lowercase and trim all text values.
2.  **Concatenate**: Join fields via `|` separator in strict order (`userId | subject | action | ...`).
3.  **Hash**: Apply SHA-256 to generate the immutable signature.

---

## 🛠 Utilities: Migration Tools

We provide tools to help professionals migrate their legacy libraries into the new standard.

### Local Batch Parser (Web)
A client-side utility to extract metadata from existing A1111/Stable Diffusion PNG libraries and convert them into structured `.deut` sidecars.

*   **Zero Uploads:** Runs entirely in the browser via File System Access API.
*   **Batch Processing:** Converts thousands of images in minutes.

![Batch Parser Demo](assets/demo.gif)

[**👉 Access the Migration Tool**](https://deut.li)

---

## 🤝 Roadmap

*   **v1.0 (Current):** Schema Definition & Migration Parsers.
*   **v2.0:** Visual Editor Support (Node-based prompt engineering).
*   **v3.0:** Enterprise Team Sync & Cloud Libraries.

---

**Maintainer:** Deut.li Engineering Team
