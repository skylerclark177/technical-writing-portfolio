# API Integration Guide: Secure Data Endpoint

## Overview
This guide outlines the authentication sequence, endpoint wiring, and error-handling schema for interacting with the decentralized data service. 

---

## 1. Authentication
All requests require a cryptographically signed header token. Plain-text API keys are deprecated to ensure transport-layer security and client anonymity.

* **Header Field:** `X-Signature-Auth`
* **Format:** Ed25519 public-key signature paired with a current UTC Unix timestamp.

### Example Request Header (cURL)
```bash
curl -X POST [https://api.secure-node.internal/v1/sync](https://api.secure-node.internal/v1/sync) \
  -H "Content-Type: application/json" \
  -H "X-Signature-Auth: 0x47c...f31a" \
  -d '{"payload": "encrypted_stream_block"}'
