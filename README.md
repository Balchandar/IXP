# IXP — Intent Exchange Protocol

**IXP (Intent Exchange Protocol)** is a layered, open protocol stack for secure, semantic, agent-to-agent communication in AI-first systems.

IXP enables encrypted message exchange, intent-based routing, trust-aware identity, decentralized capability discovery, and memory synchronization — all without relying on traditional APIs, endpoints, or OAuth.

> 🔒 Secure by design  
> 🧠 Semantic, intent-driven communication  
> ⚙️ Pluggable transport (WebSocket, QUIC, NATS, etc.)

---

## 🔍 Why IXP?

As autonomous agents evolve beyond LLM prompts and REST APIs, they need their own native communication infrastructure — one that speaks in **intent**, not endpoints.

IXP enables:
- **Encrypted transport** with agent identity and signatures (via EMCL)
- **Intent-based routing** (IMP) instead of static API contracts
- **Capability discovery** between agents and tools
- **Trust and reputation** in decentralized agent ecosystems
- **Memory and belief sync** to coordinate evolving knowledge

---

## 📚 Layers

| Layer | Name                      | Purpose |
|-------|---------------------------|---------|
| L1    | EMCL (Encrypted Model Context Layer) | Secure transport of messages |
| L2    | IMP (Intent Message Protocol)        | Routing based on `intent` values |
| L3    | Discovery Mesh            | Register and find agent capabilities |
| L4    | Memory Sync               | Exchange belief/context snapshots |
| L5    | Trust Fabric              | Agent identity, signing, and scoring |

See full spec → [`IXP-Spec.md`](./IXP-Spec.md)

---

## 🛠 Roadmap

| Phase      | Goal                                                                | Status      |
| ---------- | ------------------------------------------------------------------- | ----------- |
| ✅ Phase 1  | Define Layered Spec (EMCL, IMP, etc.)                               | Drafted     |
| 🟡 Phase 2 | Create minimal demo: agent A sends signed intent → agent B responds | In Progress |
| 🔜 Phase 3 | CLI tools: `ixp-send`, `ixp-agent`, `ixp-discovery`                 | Planned     |
| 🔜 Phase 4 | Cross-agent registry (discovery + trust scoring)                    | Planned     |
| 🔜 Phase 5 | Developer SDKs and LangChain integrations                           | Planned     |

---

## 🚀 Getting Started

### Build Your First IXP Agent

```json
{
  "protocol": "IXP/1.0",
  "intent": "summarize",
  "input": {
    "text": "System status has returned to nominal levels."
  },
  "agentPrefs": {
    "preferredAgent": "agent.alpha.summarizer"
  }
}
