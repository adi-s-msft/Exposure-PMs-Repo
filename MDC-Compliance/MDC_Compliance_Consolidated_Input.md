# MDC Regulatory Compliance Context - Consolidated for Knowledge Brain

## Product Area
Microsoft Defender for Cloud (MDC)

## Knowledge Type
- Regulatory Requirements & Compliance Framework
- Product Architecture & Design Decisions
- Stakeholder Landscape & Ownership

---

## 1. Compliance Frameworks & Regulations

### Global Core Frameworks (Table Stakes - Explicitly Supported)
- GDPR (EU Data Privacy)
- SOC 2 (Security & Operations)
- ISO 27001 / 27002 / 27017 (Information Security)
- NIST CSF, 800-53, 800-171 (US Federal)
- PCI DSS (Payment Card Industry)
- CIS Benchmarks (Center for Internet Security)
- HITRUST, SWIFT, SOX

### Emerging High-Growth Regulatory Areas
#### AI Regulation
- **EU AI Act** - Explicitly added to MDC compliance framework
  - Customers view as "GDPR of AI"
  - Requirements: transparency, data locality, auditability, evidence collection
  - Status: Active customer demand for support

#### Regional & Sovereignty Regulations
- **NIS2 (EU 2022/2555)** - Network security directive
- **DORA (Digital Operational Resilience Act)** - Financial sector
- **k-ISMS-P (Korea)** - Regional security standard
- **LGPD (Brazil)** - Data privacy regulation

#### Financial & Operational Resilience
- DORA explicitly added to MDC framework
- Extends compliance beyond security → operational governance

---

## 2. MDC Compliance Architecture (How It Works)

### Core Model: Standards → Controls → Recommendations

**Flow:**
```
Standards (GDPR, CIS, ISO, etc.)
  ↓
Controls (industry concepts mapped to each standard)
  ↓
Recommendations (existing MDC recommendations reused)
  ↓
Compliance View (projection/pivot of recommendations by standard)
```

**Key Design Principle:** 
- Recommendations are mapped TO standards, not created FOR standards
- Compliance is a derived layer, not a separate product

### Standards Management
- Standards are implemented as **Azure Policy initiatives**
- Policies define controls and assessment logic
- Violations generate recommendations + remediation guidance
- Standards apply **across Azure, AWS, GCP** (multi-cloud)

### Assessment Model
- **Continuous assessment**: MDC continuously evaluates resources against mapped controls
- **Compliance dashboard**: Real-time posture tracking by standard
- **Microsoft Cloud Security Benchmark (MCSB)**: Baseline mapped to multiple frameworks (CIS, NIST, PCI)

---

## 3. Critical Control & Audit Requirements

### Evidence & Audit Readiness (HIGH PRIORITY)
- **Customer demand:** Build audit-ready reporting with compliance evidence
- **Gap:** Current system lacks defensible audit artifacts
- **Requirements:**
  - Evidence collection for each control
  - Exemption workflows with audit trail
  - Compliance-ready export/reporting
  - Mapping clarity: Resource → Control → Standard → Regulation

### Control Coverage & Freshness (MEDIUM-HIGH PRIORITY)
- **Gap:** Customers missing latest CIS, ISO, NIST versions
- **Requirement:** Full coverage of latest benchmark versions
- **Challenge:** Standards lifecycle management (when standard updates, mappings don't auto-update)
- **Workaround needed:** Mechanism to handle standard updates without forcing manual re-selection

### Control Explainability & Mapping (MEDIUM PRIORITY)
- **Gap:** Mapping between control and standard not clear enough to users
- **Requirement:** Explicit, transparent mapping for compliance officer review
- **Feature needed:** Better reporting and visualization of control-to-standard relationships

### Multi-Cloud Compliance
- Standards apply across Azure, AWS, GCP
- Control mapping must work consistently across clouds
- Regional restrictions and data sovereignty considerations apply

---

## 4. AI-Specific Compliance Controls (Emerging)

### New Control Categories
- **Transparency controls:** Model behavior visibility, decision explainability
- **Human oversight controls:** Human-in-the-loop for critical decisions
- **Data minimization controls:** Minimize data collection/retention for AI systems
- **Auditability controls:** Logging, change tracking for AI model decisions

### Timeline
- Effective: July 1, 2026 (new AI telemetry requirement)
- Note: These require NEW control types, not just reuse of existing security controls

---

## 5. Product Design Direction & Key Decisions

### UX Strategic Shift: Recommendations-First Model

**Prior approach:** "Enable standards" → separate compliance surface
**New direction:** 
- Keep users in **existing recommendations view** 
- Add filtering/pivoting **by standard** (e.g., CIS, GDPR)
- Derived compliance view over recommendations
- Avoid separate compliance UI

**Rationale:** Simplify mental model + reduce UI complexity

### Standards Activation Flow
- **Previous:** "Enable frameworks" → select which standards to track
- **New:** Select recommendations (which are already mapped to standards)
- **Outcome:** Compliance automatically derived from recommendation selections
- **Benefit:** Single mental model (recommendations), not dual (standards + recs)

### Data Source Migration
- **From:** Ibiza-based configuration system
- **To:** New posture-based system (ASC - Azure Security Center)
- **Impact:** Standards lifecycle + control mapping must work in new infrastructure

---

## 6. Key Tensions & Tradeoffs

### Compliance vs. Security Risk Prioritization
- **Tension:** MCSB explicitly tries to reduce "over-reliance on compliance-only signals"
- **Issue:** Compliance-driven controls may not align with actual risk priority
- **Implication:** Need mechanism to balance compliance requirements with real risk

### Standards as Direct Config vs. Derived Property
- **Tension:** Should standards be directly configurable, or derived from recommendations?
- **Current decision:** Derived (to simplify UX)
- **Customer expectation:** Explicit standard activation (enterprise compliance officers)
- **Resolution:** Hybrid approach (standard filtering surface over recommendations)

### Standard Freshness vs. User Continuity
- **Problem:** When standard updates (e.g., CIS v2 → v3):
  - New recommendations added
  - Existing mappings may change
  - Users won't auto-get new coverage
- **Current workaround:** Manual re-selection required
- **Long-term requirement:** Automated delta handling

### Control Reuse vs. Standard-Specific Controls
- **Decision:** Maximize reuse (one recommendation can map to multiple standards)
- **Benefit:** Efficient, avoids duplication
- **Risk:** May miss standard-specific nuances

---

## 7. Regulatory Deadlines & Timeline Signals

### Known External Deadlines
- **July 31, 2026:** GDPR-related compliance task completion target
- **August 2026:** External audit
- **September 2026:** EU launch
- **July 1, 2026:** AI telemetry requirement (new effective date)

### MDC Feature Timeline (Inferred from roadmap)
- **Q2/Q3 2026:** Core compliance framework (standards, controls, assessment)
- **Q3/Q4 2026:** Multi-cloud compliance support (AWS/GCP)
- **2027:** Advanced features (custom standards, versioning, analytics)

---

## 8. Implementation Gaps & Priorities

### High Priority (Blocking)
1. **Standard updates handling** - Delta recommendations when standards evolve
2. **Audit evidence system** - Capture defensible compliance artifacts
3. **Control mapping clarity** - Make resource→control→standard→regulation explicit
4. **UX activation flow** - Reduce clicks in standard enablement (customer pain point)

### Medium Priority (Enabling)
1. Standards freshness - Keep CIS, ISO, NIST versions current
2. Multi-cloud consistency - Ensure controls work across Azure/AWS/GCP
3. Compliance reporting - Export/visualization for compliance officers
4. AI control definitions - New control types for EU AI Act, DORA

### Future/Research
1. Custom standards framework - Allow customers to define own standards
2. Compliance automation - Auto-remediation workflows
3. Continuous compliance analytics - Trend analysis, predictive posture

---

## 9. Stakeholders & Ownership

### Internal Teams
- **Product Management:** Feature prioritization, roadmap, compliance strategy
- **Engineering:** Control mapping, assessment engine, multi-cloud integration
- **UX/Design:** Standards activation flow, compliance dashboard
- **Compliance & Legal:** Regulatory interpretation, audit requirements
- **Security Architecture:** Control design, standards mapping, risk alignment
- **Customer Success:** Customer demand signals, adoption support

### External Stakeholders
- **Customers:** Compliance officers, security teams, audit teams
- **Regulators:** EU, national bodies (implicit, via legal/compliance)
- **Auditors:** External audit firms validating compliance
- **Competitors:** AWS Security Hub, Google Cloud Security posture, etc.

---

## 10. Customer Demand Signals

### Top Feature Requests
1. **Audit-ready reporting** - Evidence collection, compliance export
2. **AI Act compliance support** - Transparency, governance controls
3. **CIS benchmarks expansion** - SQL, AKS, DB services out-of-the-box
4. **Control mapping improvement** - Better explainability
5. **Activation simplification** - Fewer clicks, clearer flow

### Pain Points
- Too many clicks to enable standards
- Missing latest benchmark versions
- Lack of audit evidence
- Unclear control-to-standard mapping
- Limited transparency into why a control matters

---

## 11. Open Questions & Decisions Pending

1. **MVP scope:** Which standards/controls in v1? (EU-focus vs. global?)
2. **Regulatory deadlines:** What's the binding timeline for AI Act support?
3. **Success metrics:** How do we measure compliance adoption success?
4. **Business model:** Compliance as paid add-on or core feature?
5. **Architecture:** How to handle custom standards without explosion?
6. **Audit requirements:** What audit evidence must we capture?
7. **Technical ownership:** Who owns standards lifecycle + updates?
8. **Compliance vs. risk:** How to balance regulatory requirements with actual risk?

---

## Evidence & Sources

### Emails & Announcements
- 31 regulatory standards announcement (June 2026)
- Four new standards announcement (EU AI Act, DORA, k-ISMS-P, CIS)
- MDC Compliance Feature Requests Unified Report (customer demand)
- Field advisory on regulatory pressure and board expectations

### Meetings (Transcripts Available)
- Regulatory Compliance Follow-up (June 8, 2026) - Design decisions, UX direction
- Regulatory Compliance Deep Dive (June 1, 2026) - Architecture, model alignment
- Standardizing MDC & MSEM Preview Process (June 5, 2026) - Feature rollout process

### Documentation
- Microsoft Cloud Security Benchmark (MCSB) reference
- Azure Defender for Cloud regulatory compliance documentation
- Control mapping schemas and standards definitions

---

## Notes for Knowledge Brain

This document consolidates:
1. **What** regulations/frameworks apply to MDC
2. **Why** they matter (customer demand, market pressure, deadlines)
3. **How** MDC implements compliance (standards→controls→recommendations)
4. **Where** gaps exist (evidence, standards freshness, UX)
5. **Who** owns what (stakeholders, dependencies)
6. **When** deliverables are needed (timelines, regulatory deadlines)

Ready for:
- Knowledge base consolidation into persistent pages
- Cross-linking with MDC roadmap items
- Integration with compliance requirements tracking
- Sharing with compliance/legal stakeholders
