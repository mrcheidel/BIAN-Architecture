# BIAN-Architecture

## Arquitectura de referencia bancaria BIAN + PCI DSS v4.0

La arquitectura está organizada en **6 capas** alineadas con el modelo BIAN v12 y diseñadas para que el Cardholder Data Environment (CDE) cumpla íntegramente con PCI DSS. Haz clic sobre cualquier componente en el diagrama para ver sus detalles de controles, requisitos y SLA.

### Cómo leer el widget

El diagrama principal mapea cada componente a su dominio BIAN y muestra qué requisito PCI DSS es responsable de cubrir. Los badges en rojo son componentes dentro del CDE; en verde, controles normativos adyacentes (GDPR, Basel III, AMLD6).

Las cuatro pestañas cubren:

**Arquitectura** — la vista en capas interactiva, desde canales hasta infraestructura, pasando por los 8 Service Domains BIAN de negocio bancario central.

**Req. funcionales** — 25 requisitos funcionales agrupados por dominio: pagos, identidad, seguridad, fraude/AML, integración y auditoría, cada uno con su prioridad (CRÍTICO / ALTO / MEDIO) y referencia normativa.

**NFR** — 19 requisitos no funcionales con métricas precisas y medibles: latencias (p95/p99), throughput (TPS), disponibilidad (99.99%), RTO/RPO, MTTD/MTTR y cobertura de pruebas.

**PCI DSS** — los 12 requisitos del estándar v4.0.1 desglosados en controles concretos con su nivel de criticidad (Obligatorio / Crítico / Estándar).

### Principios de diseño clave

El **CDE está contenido y segmentado**: el perímetro de datos de tarjeta queda delimitado entre el tokenization engine, el HSM/Key Vault y las bases de datos OLTP con TDE. Todo lo que salga de ese perímetro trabaja exclusivamente con tokens, nunca con PANs reales.

La arquitectura es **event-driven y API-first** conforme a BIAN v12: cada Service Domain expone su BOM (Behavior Qualification Model) como API REST con OpenAPI 3.1 e ISO 20022 para mensajería interbancaria, lo que facilita la auditoría de flujos de datos de tarjeta exigida en PCI Req 1.

La **seguridad es transversal**, no un añadido: el SIEM, el PAM, el DLP y la gestión de vulnerabilidades son capas que atraviesan verticalmente toda la arquitectura, no servicios aislados.

Si quieres profundizar en algún área concreta —el modelo de red segmentado del CDE, el diseño del pipeline CI/CD con SAST/DAST, el flujo de tokenización PAN→Token, o el modelo de datos de auditoría— puedo desarrollarlo en detalle.

English
https://htmlpreview.github.io/?https://github.com/mrcheidel/BIAN-Architecture/blob/main/bian_pci_reference_architecture_v3.html
