# LLMAuditTrail: Cryptographic Audit Framework for Autonomous LLM Agents

> **Trace. Verify. Comply.**
> A cryptographic audit trail system designed for high-stakes deployment of autonomous LLM agents in regulated environments.

---

## 🔒 Core Problem

LLM agents operating in critical domains (healthcare, finance, government) lack verifiable logging and compliance tools. Most observability solutions today are built for development debugging not for regulatory-grade auditability or tamper-proof documentation.

---

## 🚀 What LLMAuditTrail Does

LLMAuditTrail enables **immutable, verifiable, and regulation-compliant logging** of agent interactions, without modifying the LLM model itself.

### ✅ Key Features

* **API Interception**: Transparent capture of all LLM API calls (e.g., OpenAI, Anthropic).
* **Cryptographic Logging**: HMAC-SHA256 + Merkle tree-based event signing.
* **Compliance Modules**: Native support for FDA 21 CFR Part 11, SOX 404, EU AI Act.
* **Session Replay**: Full deterministic reconstruction of agent decision processes.
* **Real-Time Monitoring** (beta): Live anomaly detection and control validation.

---

## 🧱 Architecture Overview

| Layer                 | Description                                                      |
| --------------------- | ---------------------------------------------------------------- |
| **API Hooking Layer** | Intercepts HTTP requests to LLM providers.                       |
| **Audit Engine**      | Signs and hashes events, builds Merkle chains.                   |
| **Compliance Layer**  | Generates certified reports for FDA, SOX, EU AI Act.             |
| **Replay Module**     | Enables full, deterministic session analysis and reconstruction. |

---

## 🆚 Why Not Traditional Tools?

| Feature                      | Traditional Tools | LLMAuditTrail         |
| ---------------------------- | ----------------- | --------------------- |
| Target                       | Debugging         | Regulatory compliance |
| Cryptographic guarantees     | ❌ None            | ✅ HMAC + Merkle Trees |
| Regulatory standards support | ❌ No              | ✅ FDA, SOX, EU AI Act |
| Tamper detection             | ❌ No              | ✅ Yes                 |
| Auditability                 | 🟡 Partial        | ✅ Full-chain logging  |

---

## ⚙️ Installation

### Quick Install

```bash
pip install llmaudittrail
```

### Dev Install

```bash
git clone https://github.com/davidhassoun/llmaudittrail
cd llmaudittrail
pip install -e .
```

---

## 🚀 Quick Start

```python
from llmaudittrail import AuditTracer
import openai

tracer = AuditTracer(
    session_id="session_001",
    compliance_mode="medical",
    retention_years=7
)

client = tracer.wrap_client(openai.OpenAI())

with tracer.audit_session():
    response = client.chat.completions.create(
        model="gpt-4",
        messages=[{"role": "user", "content": "Analyze patient symptoms..."}]
    )

report = tracer.export_compliance_report()
verified = tracer.verify_integrity()
```

---

## 📊 Performance

| Metric            | Value                   |
| ----------------- | ----------------------- |
| Latency overhead  | 3–6ms per call          |
| Memory overhead   | 1.2MB + 0.4KB/event     |
| Storage overhead  | 1.5KB per interaction   |
| Verification time | \~100ms for 1000 events |

---

## 📁 Use Cases

### 🏥 Medical Compliance (FDA)

```python
tracer = AuditTracer(compliance_mode="medical", electronic_signatures=True)
```

* Full support for **21 CFR Part 11** (timestamped e-signatures, 7-year retention, traceability)

---

### 💰 Financial Compliance (SOX)

```python
tracer = AuditTracer(compliance_mode="financial", real_time_monitoring=True)
```

* Internal controls validation, change logs, and external auditor trace access

---

### 🔁 Session Replay

```python
replay_engine = tracer.create_replay_engine("session_001")

for event in replay_engine.step_through():
    print(f"{event.timestamp}: {event.event_type}")

timeline = replay_engine.get_decision_timeline()
```

---

## 🔐 Security Architecture

* Encrypted SQLite at rest
* HMAC key storage via system keyrings
* GDPR-compliant anonymization options
* TLS-level capture via secure proxy
* **Upcoming**: HSM integration

---

## ⚠️ Current Limitations

* ZK-Proofs not implemented yet (v0.2)
* OpenAI-only support (multi-provider in v0.3)
* SQLite backend (PostgreSQL in v0.4)
* Limited determinism with non-reproducible models

---

## 🔬 Research Context

LLMAuditTrail is part of a broader research initiative into **verifiable agent architectures** and **World Model auditing**. It lays the foundation for agent-level accountability, traceable decision chains, and future-proof compliance frameworks.

---

## 🧪 Roadmap

| Version | Major Feature                                       |
| ------- | --------------------------------------------------- |
| v0.2    | Zero-Knowledge Proofs (ZK) for privacy verification |
| v0.3    | Anthropic & Google LLM support                      |
| v0.4    | PostgreSQL encrypted backend                        |
| v0.5    | ML-based anomaly detection                          |
| v1.0    | Production-grade certification                      |

---

## 🤝 Contributing

I welcome contributions focused on security, compliance, and auditing performance. Please follow my contribution guidelines and respect the cryptographic standards of the framework.

---

## 📄 License

MIT License.

---

## 📚 Citation

```bibtex
@software{llmaudittrail2025,
  title={LLMAuditTrail: Cryptographic Audit Framework for LLM Autonomous Agents},
  author={David Hassoun},
  year={2025},
  url={https://github.com/davidhassoun/llmaudittrail}
}
```

---

## 📞 Contact

* **Author**: David Hassoun
* **Email**: [davidhassoun@protonmail.com](mailto:davidhassoun@protonmail.com)
* **Twitter**: [@david\_hassoun](https://twitter.com/david_hassoun)
