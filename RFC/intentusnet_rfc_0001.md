---
title: IntentusNet Protocol Specification (RFC 0001)
author: Balachandar Manikandan
date: 2025-08-06
status: Draft
version: 0.1.0
---

# IntentusNet Protocol — RFC 0001 (Draft)

## 1. Overview
IntentusNet is a protocol for intent-driven, agent-oriented, secure communication between autonomous components in distributed AI or software systems. It replaces traditional API-based architectures with dynamic, semantically routed intent exchanges, using encrypted payloads and agent-based routing.

## 2. Core Principles
- **No REST, no RPC** — only intents
- **Tool and intent-based routing**
- **End-to-end encrypted, signed messages (EMCL)**
- **Agent discovery, fallback, and hot-reload supported**
- **Pluggable transports: HTTP, WebSocket, ZeroMQ, etc.**

## 3. Message Envelope (EMCL)
Each message must conform to the EMCL format:

```json
{
  "tool": "Summarizer",
  "intent": "summarizeReport",
  "params": { "text": "..." },
  "context": {
    "agentId": "client-001",
    "timestamp": "2025-08-06T10:00:00Z",
    "nonce": "b8f8...",
    "signature": "sha256-hmac"
  }
}
```

## 4. Encryption & Signing
- **Encryption**: AES-256-CBC
- **Signing**: HMAC-SHA256 over `iv + ciphertext`
- **Envelope Structure**:

```json
{
  "iv": "base64",
  "payload": "base64(aes_encrypted_json)",
  "signature": "hmac_sha256"
}
```

## 5. Intent Routing
Routing is based on:
- `tool:intent`
- Agents must register their capabilities
- IXP routes to first-available or preferred agent
- Fallback list supported

## 6. Agent Registration
Agents must register themselves with:
```json
{
  "agentId": "summarizer-001",
  "tool": "Summarizer",
  "intents": ["summarizeReport"],
  "address": "localhost:5571"
}
```
Broadcast is typically over ZeroMQ PUB or HTTP POST to registry service.

## 7. Transports
Supported transports:
- ZeroMQ (REQ/REP, PUB/SUB)
- HTTP (for external clients)
- WebSocket (optional, duplex intent stream)
- UNIX socket (internal agent communication)

## 8. Fallback and Retry
- Registry supports multiple agents per intent
- Fallback policy:
  - Try primary → if error → try next
  - Configurable at router level

## 9. Logging
IXP must log:
- Received intent
- Source agentId
- Routed target
- Duration
- Status (ok/error)

## 10. Key Rotation
- Keys managed by Key Manager
- Rotation can be manual or via `intent:rotateKey`
- Rotation must update all connected nodes securely

## 11. Security Considerations
- No plaintext transport unless on localhost
- All messages must be signed and timestamped
- Clock drift allowed: ±30s default

## 12. Future Extensions
- Vectorized memory model per agent
- Federation between IXPs
- Semantic type validation

## 13. License
MIT License © 2025 Balachandar Manikandan
