# Standard Operating Procedure (SOP): Structured Data Sanitization

## 1. Purpose & Scope
This SOP defines the standardized pipeline for sanitizing, parsing, and verifying structured text data prior to downstream ingestion into decentralized storage clusters.

## 2. Prerequisites
* Python 3.10+ execution environment
* `pandas` and `jsonschema` verification libraries
* Local read/write permissions for the target staging directory

---

## 3. Step-by-Step Procedure

<Steps>
  <Step title="Acquisition & Ingestion" subtitle="Step 1">
    Fetch raw batch payloads from the staging drop directory. Validate file integrity via SHA-256 checksum comparison against the manifest file.
  </Step>
  <Step title="Sanitization & Stripping" subtitle="Step 2">
    Execute the normalization script to strip trailing whitespace, normalize UTF-8 character encoding, and remove malicious injection vectors or null-byte characters.
  </Step>
  <Step title="Schema Validation" subtitle="Step 3">
    Run the validation script against the current JSON schema definition to ensure compliance.
    ```bash
    python3 validate_schema.py --input staged_payload.json --schema v2_spec.json
    ```
  </Step>
  <Step title="Staging & Handoff" subtitle="Step 4">
    Move verified outputs to the production export queue and archive raw source logs.
  </Step>
</Steps>

---

## 4. Troubleshooting & Exception Handling
* **Checksum Mismatch:** Discard the payload, log the discrepancy in `error_audit.log`, and flag the source node operator.
* **Schema Validation Failure:** Review the stderr output for missing keys and reject the batch until corrected by the upstream producer.
