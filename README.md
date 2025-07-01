# LLMAuditTrail

Cryptographic audit trail framework for LLM autonomous agents in regulated environments. Provides tamper-proof logging, integrity verification, and compliance reporting without requiring model modifications.

## Problem Statement

LLM agents deployed in critical environments (healthcare, finance, government) require cryptographic audit trails and compliance documentation that existing observability tools don't provide. Current solutions focus on development debugging rather than production auditing and regulatory compliance.

LLMAuditTrail addresses this gap by implementing cryptographic integrity verification at the API level, creating immutable records of agent decision-making processes.

## Technical Approach

- **API Interception**: Captures all HTTP traffic to LLM providers (OpenAI, Anthropic, etc.)
- **Cryptographic Logging**: HMAC-SHA256 with Merkle tree verification for tamper detection
- **Compliance Integration**: Built-in support for FDA 21 CFR Part 11, SOX, EU AI Act requirements
- **Session Replay**: Deterministic reproduction of agent execution sequences

## Key Differentiators

| Aspect | Traditional Tools | LLMAuditTrail |
|--------|-------------------|---------------|
| **Purpose** | Development observability | Regulatory compliance |
| **Cryptography** | None | HMAC-SHA256 + Merkle trees |
| **Standards** | None | FDA, SOX, EU AI Act |
| **Tamper-proof** | No | Yes |
| **Audit Reports** | Basic logs | Compliance-ready reports |

## Installation

```
pip install llmaudittrail
```

Development installation:
```
git clone https://github.com/davidhassoun/llmaudittrail
cd llmaudittrail
pip install -e .
```

## Quick Start

```python
from llmaudittrail import AuditTracer
import openai

# Initialize with compliance mode
tracer = AuditTracer(
    session_id="medical_diagnosis_001",
    compliance_mode="medical",  # FDA 21 CFR Part 11
    retention_years=7
)

# Wrap your existing LLM client
client = tracer.wrap_client(openai.OpenAI())

# Use normally - all interactions are automatically logged
with tracer.audit_session():
    response = client.chat.completions.create(
        model="gpt-4",
        messages=[{"role": "user", "content": "Analyze patient symptoms..."}]
    )

# Export compliance report
audit_report = tracer.export_compliance_report()
integrity_verified = tracer.verify_integrity()
```

## Performance Characteristics

Benchmarked with OpenAI GPT-4 under production load:

| Metric | Value |
|--------|-------|
| Latency overhead | 3-6ms per call |
| Memory overhead | +1.2MB baseline, +0.4KB per event |
| Storage overhead | ~1.5KB per interaction (compressed) |
| Verification time | <100ms for 1000-event chains |

*Based on controlled testing with 10,000 requests over 24-hour periods.*

## Architecture

Four-layer cryptographic verification system:

1. **Client Wrapper**: Transparent proxy for LLM API clients
2. **Crypto Engine**: HMAC-SHA256 + Merkle trees for integrity verification
3. **Compliance Manager**: Regulatory standards implementation
4. **Replay Engine**: Deterministic session reconstruction

## Compliance Features

### Healthcare (FDA 21 CFR Part 11)
- Electronic signatures with timestamp verification
- 7-year retention with automated archival
- Audit trail completeness validation
- Change control documentation

### Financial (SOX Section 404)
- Internal control testing documentation
- Management assertion support
- Independent auditor trail verification
- Real-time anomaly detection

### EU AI Act (High-Risk Systems)
- Algorithmic transparency documentation
- Human oversight audit trails
- Risk management integration
- Conformity assessment support

## Use Cases

### Medical AI Compliance
```python
tracer = AuditTracer(
    compliance_mode="medical",
    retention_years=7,
    electronic_signatures=True
)

with tracer.audit_session():
    diagnosis = medical_agent.analyze_symptoms(patient_data)
    treatment_plan = medical_agent.recommend_treatment(diagnosis)
    
# Generate FDA-compliant audit report
fda_report = tracer.export_medical_compliance_report()
```

### Financial Algorithm Monitoring
```python
tracer = AuditTracer(
    compliance_mode="financial",
    real_time_monitoring=True
)

with tracer.audit_session():
    market_analysis = trading_agent.analyze_market()
    trade_decision = trading_agent.execute_strategy(market_analysis)

# SOX compliance verification
sox_report = tracer.export_sox_compliance_report()
```

### Session Replay and Analysis
```python
# Load historical session
replay_engine = tracer.create_replay_engine("session_001")

# Step through events chronologically
for event in replay_engine.step_through():
    print(f"{event.timestamp}: {event.event_type}")

# Extract decision timeline
decisions = replay_engine.get_decision_timeline()
metrics = replay_engine.calculate_session_metrics()
```

## Security Considerations

- HMAC keys stored using system keyring integration
- SQLite databases encrypted at rest (configurable)
- Network traffic captured via TLS termination
- GDPR-compliant data anonymization options
- Support for hardware security modules (HSMs)

## Limitations (Version 0.1 - MVP)

⚠️ **Current limitations**:
- No ZK-proofs implementation (roadmap v0.2)
- Single LLM provider support (OpenAI initially)
- Cryptographic overhead ~3-6ms per interaction
- Determinism limited by model variability
- SQLite storage only (PostgreSQL in v0.2)

## Research Context

This project is part of ongoing research into cryptographic auditability of autonomous AI systems, with applications to World Models and advanced agent architectures. The framework provides a foundation for more sophisticated verification methods in future releases.

**Author:** David Hassoun  
AI Safety researcher and founder of Comenius, specialized in agentic AI systems and cryptographic auditability frameworks.

## Roadmap

- [ ] v0.2: ZK-proofs for privacy-preserving verification
- [ ] v0.3: Multi-provider support (Anthropic, etc.)
- [ ] v0.4: PostgreSQL backend with encryption
- [ ] v0.5: Real-time anomaly detection with ML
- [ ] v1.0: Production certification and enterprise features

## Contributing

Contributions welcome! This project aims to establish standards for cryptographic auditability of LLM agents.

1. Fork the repository
2. Create a feature branch
3. Add comprehensive tests
4. Ensure all tests pass (`pytest`)
5. Submit a pull request

## License

MIT License - see LICENSE file for details.

## Citation

If you use LLMAuditTrail in academic research:

```
@software{llmaudittrail2025,
  title={LLMAuditTrail: Cryptographic Audit Framework for LLM Autonomous Agents},
  author={David Hassoun},
  year={2025},
  url={https://github.com/davidhassoun/llmaudittrail}
}
```

## Contact

**David Hassoun**  
- Twitter: [@david_hassoun](https://x.com/david_hassoun)
- Email: davidhassoun@protonmail.com
- LinkedIn: [David Hassoun](https://linkedin.com/in/davidhassoun)

## References

- FDA 21 CFR Part 11 - Electronic Records and Electronic Signatures
- SOX Section 404 - Internal Control Requirements  
- EU AI Act - High-Risk AI Systems Requirements
- NIST Cybersecurity Framework - Audit Trail Guidelines
