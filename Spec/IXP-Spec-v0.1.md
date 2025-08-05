# IXP Specification (v0.1)

## Overview

IXP (Intent Exchange Protocol) is a layered, AI-first protocol stack enabling secure, semantic, trust-aware communication between autonomous agents, tools, and models.

Unlike human-centric HTTP/REST systems, IXP routes encrypted intent-based messages, supports capability discovery, memory synchronization, and verifiable agent identity â€” over any transport layer.

## Protocol Layers

### Layer 1: EMCL (Encrypted Model Context Layer)

**Purpose:** Encrypt, sign, and securely transport agent messages.

```json
{
  "headers": {
    "agentId": "agent.alpha",
    "toolId": "tool.summarizer",
    "intent": "summarize",
    "timestamp": "2025-08-05T12:00:00Z",
    "nonce": "xyz123",
    "signature": "<HMAC256>"
  },
  "payload": "<base64-encrypted-json>"
}
```

- AES-GCM encryption
- HMAC or ECDSA signing
- Replay protection (nonce + timestamp)
- Transport-agnostic

### Layer 2: IMP (Intent Message Protocol)

**Purpose:** Route by semantic intent, not endpoint or path.

```json
{
  "intent": "summarize",
  "input": {
    "text": "System status has returned to nominal levels."
  },
  "metadata": {
    "language": "en",
    "priority": "high"
  },
  "agentPrefs": {
    "preferredAgent": "agent.alpha.summarizer",
    "fallbackAllowed": true
  }
}
```

- Structured intent + payload
- Match via capability registry
- Support for fallback and urgency

### Layer 3: Discovery Mesh

**Purpose:** Agents describe and expose capabilities.

```json
{
  "agentId": "agent.alpha.summarizer",
  "capabilities": ["summarize"],
  "input": { "type": "text", "lang": ["en", "ta"] },
  "trustScore": 0.98
}
```

- Capability-based search (not static APIs)
- Versioning and deprecation supported
- Trust-aware discovery

### Layer 4: Memory Sync

**Purpose:** Exchange agent beliefs and evolving knowledge.

```json
{
  "agentId": "agent.core.memory",
  "beliefs": [
    {
      "id": "b123",
      "statement": "Entity Z is incompatible with component Y",
      "confidence": 0.92,
      "timestamp": "2025-08-04T10:12:00Z"
    }
  ]
}
```

- Snapshot, diff, and merge memory
- Support for confidence, emotions
- Optional sharing via EMCL

### Layer 5: Trust Fabric

**Purpose:** Provide decentralized identity and message verification.

```json
{
  "agentId": "agent.alpha.researcher",
  "publicKey": "-----BEGIN PUBLIC KEY-----\n...\n-----END PUBLIC KEY-----",
  "issuedAt": "2025-08-01T00:00:00Z",
  "expiresAt": "2026-08-01T00:00:00Z",
  "revoked": false
}
```

- Agent IDs + public keys
- Key rotation and revocation
- Verifiable trust scores

## Implementation Roadmap

1. Finalize EMCL encryption/signing library
2. Define IMP matching rules (regex, vector, capability tags)
3. Build discovery registry (flat file or decentralized)
4. Prototype memory sync format and merge strategy
5. Establish agent key issuance and trust rules

## IXP Vision & Roadmap

### What IXP Is

IXP is a protocol for agent-to-agent communication that focuses on:
- Secure, encrypted messaging
- Intent-based routing (not APIs)
- Capability-based agent discovery
- Memory/belief synchronization
- Trust and verifiability by design

### Why This Protocol Exists

As AI agents evolve, traditional networking stacks are insufficient:
- HTTP assumes human-driven sessions
- OAuth assumes human auth and delegation
- REST assumes static APIs and request/response patterns

IXP provides:
- Encrypted, signed messages
- Agent capability discovery
- Intent-based coordination
- Native support for evolving beliefs, trust, and autonomy

### Project Roadmap

| Phase      | Goal                                                                | Status      |
| ---------- | ------------------------------------------------------------------- | ----------- |
| Phase 1    | Define Layered Spec (EMCL, IMP, etc.)                               | Complete    |
| Phase 2    | Create minimal working agent-to-agent demo                          | In Progress |
| Phase 3    | CLI tools: ixp-send, ixp-router, ixp-registry                       | Planned     |
| Phase 4    | Memory sync + belief graphs                                         | Planned     |
| Phase 5    | Integrations (LangChain, Ollama, LLM ToolCalls)                    | Planned     |

## How to Use or Contribute

- Build an agent that speaks IXP using the envelope formats
- Create your own IXP router or agent registry
- Add new capabilities, layers, or encoding formats
- Propose extensions or improvements in your own fork

## License & Contributions

IXP is an open-spec, MIT-licensed protocol. Contributions welcome at: https://github.com/IXP

Maintainer: Balachandar Manikandan
