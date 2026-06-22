# Banking Architecture
## Banking Reference Architecture based on BIAN + PCI DSS v4.0

The architecture is organized into **6 layers**, aligned with the **BIAN v12 framework** and designed to ensure that the Cardholder Data Environment (CDE) fully complies with **PCI DSS requirements**. Click on any component in the diagram to explore its associated controls, compliance requirements, and SLA definitions.

### How to read the widget

The main diagram maps each component to its corresponding BIAN domain and shows which **PCI DSS** requirement each component is responsible for addressing. Components highlighted in red belong to the CDE; components shown in green represent adjacent regulatory controls (GDPR, Basel III, AMLD6).

The four tabs cover:

**Architecture** — the interactive layered view, spanning from customer-facing channels down to infrastructure, including the 8 core BIAN Service Domains supporting central banking business operations.

**Functional Requirements** — 25 functional requirements grouped by domain: payments, identity management, security, fraud/AML, integration, and auditability. Each requirement includes its priority level (CRITICAL / HIGH / MEDIUM) and associated regulatory reference.

**NFR** — 19 non-functional requirements defined with precise and measurable metrics: latency targets (p95/p99), throughput (TPS), availability (99.99%), RTO/RPO objectives, MTTD/MTTR indicators, and test coverage requirements.

**PCI DSS** — the 12 requirements defined by the PCI DSS v4.0.1 standard, decomposed into specific technical and operational controls, classified by criticality level (Mandatory / Critical / Standard).

### Key design principles

The CDE is isolated and strongly segmented: the card data perimeter is strictly contained between the tokenization engine, the HSM/Key Vault, and the OLTP databases protected with TDE (Transparent Data Encryption). Any system operating outside this perimeter works exclusively with tokens, never with real PAN (Primary Account Number) data.

The architecture follows an event-driven and API-first approach, aligned with BIAN v12: each Service Domain exposes its BOM (Behavior Qualification Model) through REST APIs, using OpenAPI 3.1 specifications and ISO 20022 messaging standards for interbank communication. This significantly simplifies the cardholder data flow auditability required under PCI DSS Requirement 1.

**Security is implemented as a cross-cutting concern, not as an add-on: SIEM, PAM, DLP**, and **vulnerability management** operate as vertical security layers spanning the entire architecture rather than isolated standalone services.

If you would like to explore any area in more detail — such as the segmented CDE network model, the CI/CD pipeline design with SAST/DAST controls, the **PAN → Token tokenization flow**, or the audit data model architecture — I can expand each area further.

Preview the Diagram Landscape

https://htmlpreview.github.io/?https://github.com/mrcheidel/BIAN-Architecture/blob/main/reference.html

Extended Diagram Landscape

https://htmlpreview.github.io/?https://github.com/mrcheidel/BIAN-Architecture/blob/main/extended.html
