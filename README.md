# .deut Open Asset Format

**Status:** Beta 1.0
**Maintainer:** Deut.li Engineering Team
**License:** MIT

## Overview
The `.deut` format is a structured JSON-based container for visual art assets. Unlike simple prompt text files, a `.deut` file acts as a "Digital Negative," storing the raw intent (`input_dna`), the system parameters, and a cryptographic proof of integrity.

The format ensures:
1. **Non-Destructive Editing:** Original user inputs are preserved separately from the LLM-generated prompt.
2. **Provenance & Integrity:** A built-in fingerprint mechanism prevents silent tampering.
3. **Platform Agnostic:** While designed for Deut.li, the schema is open for any tool to implement.

## File Structure

The file must be a valid JSON object with MIME-type `application/vnd.deut`.

```json
{
  "meta": { ... },       // Versioning and ownership
  "input_dna": { ... },  // The "Source Code" of the image (User Intent)
  "llm_output": { ... }, // The compiled result (can be regenerated)
  "fingerprint": "..."   // SHA-256 Hash for verification
}
```

## Fingerprint Generation Protocol
To verify the integrity of a `.deut` file, independent validators must reconstruct the hash using the following algorithm.

### 1. Normalization
All text values within `input_dna` are converted to **lowercase** and **trimmed** of leading/trailing whitespace.

### 2. Concatenation
Fields are joined into a single string using the pipe symbol `|` as a separator in the exact order below:

`userId | user_subject | user_action | user_environment | user_atmosphere | mediaCategory | mediaStyle | lighting | framing | focus | film | aspectRatio | avoid | seed`

> **Note:** If a field is empty or missing, it is treated as an empty string.

### 3. Hashing
Apply **SHA-256** to the concatenated string.
The resulting hexadecimal string must match the `fingerprint` field in the file.

## Validation
Developers can validate `.deut` files using the `schema.json` provided in this repository.

```bash
# Example validation using a generic JSON schema validator
ajv validate -s schema.json -d my-art.deut
```
