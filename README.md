# ServiceNow IRM — Saudi Regulatory GRC Implementation

A full end-to-end ServiceNow Integrated Risk Management (IRM) implementation scoped to the Saudi Arabian regulatory and international compliance landscape, built on a Personal Developer Instance (PDI).

Every record was configured from scratch — frameworks loaded citation by citation, policies mapped to real control objectives, risks scored using a quantitative model, and a live executive dashboard assembled across all layers.

---

## What Was Built

| Layer | Detail | Count |
|---|---|---|
| Regulatory Frameworks | Authority Documents loaded as the citation backbone | 7 |
| Framework Citations | Controls, subdomains, and domains mapped per framework | 579 |
| Policies | Organisational policies linked to frameworks | 7 |
| Control Objectives | Operational commitments bridging policy to framework | 21 |
| Controls | Assessed controls linked to control objectives | 23 |
| Risk Framework | Saudi Regulatory Risk Framework | 1 |
| Risk Statements | Risk definitions scoped to the Saudi regulatory context | 7 |
| Risk Records | Risks scored against a business entity using SLE × ARO = ALE | 7 |
| Reports | List and chart reports built against live GRC tables | 4 |
| Dashboard | Executive GRC dashboard aggregating all views | 1 |

---

## Phase 1 — Regulatory Frameworks

Seven authority documents loaded into ServiceNow GRC as the foundation for all policies, control objectives, and controls.

**Saudi National Frameworks**

| Framework | Record | Citations | Method |
|---|---|---|---|
| NCA ECC-2:2024 — Essential Cybersecurity Controls | AD0020001 | Manual build | Domain → Subdomain → Control |
| NCA CCC-2:2024 — Cloud Cybersecurity Controls | AD0020002 | Manual build | Domain → Subdomain → Control |
| NCNICC-1:2025 — Critical Infrastructure Cybersecurity Controls | AD0020003 | 61 | CSV import |
| SAMA CSF — Cyber Security Framework | AD0020004 | 89 | CSV import |
| PDPL — Personal Data Protection Law | AD0020007 | 84 | CSV import |

**International Frameworks**

| Framework | Record | Citations | Method |
|---|---|---|---|
| ISO/IEC 27001:2022 — Information Security Management | AD0020008 | 198 | CSV import |
| ISO/IEC 42001:2023 — AI Management Systems | AD0020009 | 48 | CSV import |

**Total: 579 citations across 7 frameworks**

NCA ECC and NCA CCC were built manually — every domain, subdomain, and control entered directly into ServiceNow — to demonstrate full platform depth beyond import. The remaining five frameworks were loaded via CSV import with a staging table and transform map, which is the standard production approach for large frameworks.

---

## Phase 2 — Policies and Control Objectives

Seven organisational policies built, each mapped to its primary regulatory framework. Each policy carries three Control Objectives — the operational layer between a framework requirement and a control assessment.

| Policy | Framework | Control Objectives |
|---|---|---|
| Information Security Policy | ISO 27001 | Access Control · IS Leadership and Direction · Risk Assessment and Treatment |
| Cybersecurity Policy | NCA ECC | ECC-D1 Governance · ECC-D2 Defense · ECC-D3 Resilience |
| Cloud Security Policy | NCA CCC | CCC-D1 Governance · CCC-D2 Controls · CCC-D3 Resilience |
| Critical Infrastructure Protection Policy | NCNICC | NCNICC-D1 Governance · NCNICC-D2 Controls · NCNICC-D3 Resilience |
| AI Governance Policy | ISO 42001 | 42001-D1 Governance · 42001-D2 Risk · 42001-D3 Controls |
| Data Privacy Policy | PDPL | PDPL-D1 Governance · PDPL-D2 Rights · PDPL-D3 Processing |
| Third Party and Vendor Risk Policy | SAMA CSF | SAMA-D1 Governance · SAMA-D2 Requirements · SAMA-D3 Monitoring |

All 7 policies active. All 21 control objectives active and linked.

---

## Phase 3 — Risk Register

**Risk Framework:** Saudi Regulatory Risk Framework (RFR0001001)  
**Entity Assessed:** Information Security and Cybersecurity Division (Business Unit)

Seven risk statements defined and loaded, covering the primary threat categories for a Saudi-regulated organisation.

| Risk Statement | Category |
|---|---|
| Unauthorized Access to Critical Systems | IT |
| Cloud Misconfiguration and Data Exposure | IT |
| Personal Data Breach | Privacy |
| Third Party and Vendor Failure | Operational |
| Critical Infrastructure Disruption | Operational |
| AI System Bias or Failure | IT |
| Information Security Incident | IT |

---

## Phase 4 — Risk Scoring

Each risk scored using the quantitative SLE × ARO = ALE model. ServiceNow maps the resulting ALE to qualitative risk bands automatically.

```
SLE  ×  ARO  =  ALE
Single Loss Expectancy × Annualised Rate of Occurrence = Annualised Loss Expectancy
```

Every risk record carries both an **Inherent score** (pre-control) and a **Residual score** (post-control), showing the impact of controls on risk reduction.

| Risk | Inherent SLE | Inherent ARO | Residual SLE | Residual ARO |
|---|---|---|---|---|
| Unauthorized Access to Critical Systems | 500,000 | 3 | 150,000 | 1 |
| Cloud Misconfiguration and Data Exposure | 400,000 | 4 | 100,000 | 2 |
| Personal Data Breach | 600,000 | 2 | 200,000 | 1 |
| Third Party and Vendor Failure | 300,000 | 3 | 100,000 | 1 |
| Critical Infrastructure Disruption | 1,000,000 | 2 | 300,000 | 1 |
| AI System Bias or Failure | 250,000 | 3 | 75,000 | 1 |
| Information Security Incident | 450,000 | 4 | 150,000 | 2 |

---

## Phase 5 — Control Assessment

23 controls assessed across all 7 frameworks — 21 created via background script (GlideRecord), 2 manually. Each control is linked to a Control Objective and assessed against its framework citations.

| Record | Control | Framework |
|---|---|---|
| CTRL0020001 | Access Control | ISO 27001 |
| CTRL0020042 | Cybersecurity Governance and Risk Management | NCA ECC |
| CTRL0020043 | Third Party Risk Governance and Oversight | SAMA CSF |

> **Note on Compliance Scores:** All controls are set to Monitor state with Compliant status to demonstrate the scoring mechanism end-to-end. In a production environment, scores would reflect actual attestation cycles and typically land in the 65–80% range. This is a demo PDI — the implementation shows the platform configuration and workflow, not a live compliance posture.

---

## Phase 6 — Reports and Dashboard

**4 reports built against live ServiceNow tables:**

| Report | Type | Table |
|---|---|---|
| Risk Register — Saudi Regulatory Stack | List | sn_risk_risk |
| Risk by Category — Saudi Regulatory Stack | Bar chart | sn_risk_risk |
| Policy Compliance — Saudi Regulatory Stack | List | sn_compliance_policy |
| Control Assessment — Saudi Regulatory Stack | List | sn_compliance_control |

**Saudi GRC Dashboard — 4 widgets:**

The dashboard aggregates all four reports into a single executive-facing view — risk distribution by category, policy compliance status, full risk register with inherent and residual scores, and control assessment scoped to the Information Security and Cybersecurity Division.

![Saudi GRC Dashboard](screenshots/dashboard/saudi-grc-dashboard.png)

---

## Screenshots

### PDI Instance

- [00-pdi-instance-activated](screenshots/00-pdi-instance-activated.png)

---

### Frameworks

**NCA ECC-2:2024**
- [01-nca-ecc-authority-document](screenshots/frameworks/nca-ecc/01-nca-ecc-authority-document.png)
- [02-ecc-5-domains-added](screenshots/frameworks/nca-ecc/02-ecc-5-domains-added.png)
- [03-ecc1-subdomains-complete](screenshots/frameworks/nca-ecc/03-ecc1-subdomains-complete.png)
- [04-ecc1-1-controls-complete](screenshots/frameworks/nca-ecc/04-ecc1-1-controls-complete.png)
- [05-ecc2-subdomains-complete](screenshots/frameworks/nca-ecc/05-ecc2-subdomains-complete.png)
- [06-ecc2-1-controls-complete](screenshots/frameworks/nca-ecc/06-ecc2-1-controls-complete.png)
- [07-ecc3-subdomains-complete](screenshots/frameworks/nca-ecc/07-ecc3-subdomains-complete.png)
- [08-ecc3-1-controls-complete](screenshots/frameworks/nca-ecc/08-ecc3-1-controls-complete.png)
- [09-ecc4-subdomains-complete](screenshots/frameworks/nca-ecc/09-ecc4-subdomains-complete.png)
- [10-ecc4-1-controls-complete](screenshots/frameworks/nca-ecc/10-ecc4-1-controls-complete.png)
- [11-ecc5-subdomains-complete](screenshots/frameworks/nca-ecc/11-ecc5-subdomains-complete.png)
- [12-ecc5-1-controls-complete](screenshots/frameworks/nca-ecc/12-ecc5-1-controls-complete.png)
- [13-ecc-authority-document-complete](screenshots/frameworks/nca-ecc/13-ecc-authority-document-complete.png)

**NCA CCC-2:2024**
- [01-nca-ccc-authority-document](screenshots/frameworks/nca-ccc/01-nca-ccc-authority-document.png)
- [02-ccc-8-domains-added](screenshots/frameworks/nca-ccc/02-ccc-8-domains-added.png)
- [03-ccc1-subdomains-complete](screenshots/frameworks/nca-ccc/03-ccc1-subdomains-complete.png)
- [04-ccc2-subdomains-complete](screenshots/frameworks/nca-ccc/04-ccc2-subdomains-complete.png)
- [05-ccc3-subdomains-complete](screenshots/frameworks/nca-ccc/05-ccc3-subdomains-complete.png)
- [06-ccc4-subdomains-complete](screenshots/frameworks/nca-ccc/06-ccc4-subdomains-complete.png)
- [07-ccc5-subdomains-complete](screenshots/frameworks/nca-ccc/07-ccc5-subdomains-complete.png)
- [08-ccc6-subdomains-complete](screenshots/frameworks/nca-ccc/08-ccc6-subdomains-complete.png)
- [09-ccc7-subdomains-complete](screenshots/frameworks/nca-ccc/09-ccc7-subdomains-complete.png)
- [10-ccc8-subdomains-complete](screenshots/frameworks/nca-ccc/10-ccc8-subdomains-complete.png)
- [11-ccc1-1-controls-complete](screenshots/frameworks/nca-ccc/11-ccc1-1-controls-complete.png)
- [12-ccc2-1-controls-complete](screenshots/frameworks/nca-ccc/12-ccc2-1-controls-complete.png)
- [13-ccc3-1-controls-complete](screenshots/frameworks/nca-ccc/13-ccc3-1-controls-complete.png)
- [14-ccc4-1-controls-complete](screenshots/frameworks/nca-ccc/14-ccc4-1-controls-complete.png)
- [15-ccc5-1-controls-complete](screenshots/frameworks/nca-ccc/15-ccc5-1-controls-complete.png)
- [16-ccc6-1-controls-complete](screenshots/frameworks/nca-ccc/16-ccc6-1-controls-complete.png)
- [17-ccc7-1-controls-complete](screenshots/frameworks/nca-ccc/17-ccc7-1-controls-complete.png)
- [18-ccc8-1-controls-complete](screenshots/frameworks/nca-ccc/18-ccc8-1-controls-complete.png)
- [19-nca-ccc-authority-document-complete](screenshots/frameworks/nca-ccc/19-nca-ccc-authority-document-complete.png)

**NCNICC-1:2025**
- [01-ncnicc-authority-document](screenshots/frameworks/ncnicc/01-ncnicc-authority-document.png)
- [02-ncnicc-csv-loaded](screenshots/frameworks/ncnicc/02-ncnicc-csv-loaded.png)
- [03-ncnicc-transform-map-complete](screenshots/frameworks/ncnicc/03-ncnicc-transform-map-complete.png)
- [04-ncnicc-transform-complete](screenshots/frameworks/ncnicc/04-ncnicc-transform-complete.png)
- [05-ncnicc-citations-verified](screenshots/frameworks/ncnicc/05-ncnicc-citations-verified.png)
- [06-ncnicc-authority-document-complete](screenshots/frameworks/ncnicc/06-ncnicc-authority-document-complete.png)

**SAMA CSF**
- [01-sama-csf-authority-document](screenshots/frameworks/sama-csf/01-sama-csf-authority-document.png)
- [02-sama-csf-csv-loaded](screenshots/frameworks/sama-csf/02-sama-csf-csv-loaded.png)
- [03-sama-csf-transform-map-complete](screenshots/frameworks/sama-csf/03-sama-csf-transform-map-complete.png)
- [04-sama-csf-transform-complete](screenshots/frameworks/sama-csf/04-sama-csf-transform-complete.png)
- [05-sama-csf-authority-document-complete](screenshots/frameworks/sama-csf/05-sama-csf-authority-document-complete.png.png)

**PDPL**
- [01-pdpl-authority-document](screenshots/frameworks/pdpl/01-pdpl-authority-document.png)
- [02-pdpl-csv-loaded](screenshots/frameworks/pdpl/02-pdpl-csv-loaded.png)
- [03-pdpl-transform-map](screenshots/frameworks/pdpl/03-pdpl-transform-map.png)
- [04-pdpl-field-maps-complete](screenshots/frameworks/pdpl/04-pdpl-field-maps-complete.png)
- [05-pdpl-transform-complete](screenshots/frameworks/pdpl/05-pdpl-transform-complete.png)
- [06-pdpl-authority-document-complete](screenshots/frameworks/pdpl/06-pdpl-authority-document-complete.png)

**ISO 27001**
- [01-iso27001-authority-document](screenshots/frameworks/iso-27001/01-iso27001-authority-document.png)
- [02-iso27001-csv-loaded](screenshots/frameworks/iso-27001/02-iso27001-csv-loaded.png)
- [03-iso27001-transform-map-complete](screenshots/frameworks/iso-27001/03-iso27001-transform-map-complete.png)
- [04-iso27001-transform-complete](screenshots/frameworks/iso-27001/04-iso27001-transform-complete.png)
- [05-iso27001-citations-loaded](screenshots/frameworks/iso-27001/05-iso27001-citations-loaded.png)

**ISO 42001**
- [01-iso42001-authority-document](screenshots/frameworks/iso-42001/01-iso42001-authority-document.png)
- [02-iso42001-csv-loaded](screenshots/frameworks/iso-42001/02-iso42001-csv-loaded.png)
- [03-iso42001-transform-map-complete](screenshots/frameworks/iso-42001/03-iso42001-transform-map-complete.png)
- [04-iso42001-citations-loaded](screenshots/frameworks/iso-42001/04-iso42001-citations-loaded.png)

---

### Policies

- [01-information-security-policy-3-cos](screenshots/policies/01-information-security-policy-3-cos.png)
- [02-cybersecurity-policy-3-cos](screenshots/policies/02-cybersecurity-policy-3-cos.png)
- [03-cloud-security-policy-3-cos](screenshots/policies/03-cloud-security-policy-3-cos.png)
- [04-critical-infrastructure-policy-3-cos](screenshots/policies/04-critical-infrastructure-policy-3-cos.png)
- [05-ai-governance-policy-3-cos](screenshots/policies/05-ai-governance-policy-3-cos.png)
- [06-data-privacy-policy-3-cos](screenshots/policies/06-data-privacy-policy-3-cos.png)
- [07-third-party-vendor-risk-policy-3-cos](screenshots/policies/07-third-party-vendor-risk-policy-3-cos.png)

---

### Risk Register

- [01-risk-framework-created](screenshots/risk-register/01-risk-framework-created.png)
- [02-risk-statements-all-7](screenshots/risk-register/02-risk-statements-all-7.png)
- [03-risks-register-all-07-risks](screenshots/risk-register/03-risks-register-all-07-risks.png)
- [04-risk-scoring-example](screenshots/risk-register/04-risk-scoring-example.png)

---

### Controls

- [01-policies-list-all-100](screenshots/controls/01-policies-list-all-100.png)
- [02-information-security-policy-cos](screenshots/controls/02-information-security-policy-cos.png)
- [03-cybersecurity-policy-cos](screenshots/controls/03-cybersecurity-policy-cos.png)
- [04-cloud-security-policy-cos](screenshots/controls/04-cloud-security-policy-cos.png)
- [05-critical-infrastructure-policy-cos](screenshots/controls/05-critical-infrastructure-policy-cos.png)
- [06-ai-governance-policy-cos](screenshots/controls/06-ai-governance-policy-cos.png)
- [07-data-privacy-policy-cos](screenshots/controls/07-data-privacy-policy-cos.png)
- [08-third-party-risk-policy-cos](screenshots/controls/08-third-party-risk-policy-cos.png)
- [09-control-record-compliant](screenshots/controls/09-control-record-compliant.png)

---

### Reports

- [01-risk-register-report](screenshots/reports/01-risk-register-report.png)
- [02-risk-by-category-report](screenshots/reports/02-risk-by-category-report.png)
- [03-policy-compliance-report](screenshots/reports/03-policy-compliance-report.png)

---

### Dashboard

- [saudi-grc-dashboard](screenshots/dashboard/saudi-grc-dashboard.png)

---

## Why This Matters for Saudi GRC

Saudi Arabia operates one of the most layered regulatory environments in the region. Organisations must simultaneously satisfy NCA ECC (mandatory cybersecurity baseline), NCA CCC (cloud controls), NCNICC (critical infrastructure), SAMA CSF (financial sector), PDPL (data protection), ISO 27001 (international baseline), and ISO 42001 (AI governance).

This implementation demonstrates the ability to load and manage all seven frameworks inside a single GRC platform, maintain full policy-to-citation traceability, score risks quantitatively, run compliance assessments, and deliver executive-level reporting — the core skill set for a ServiceNow IRM implementation engagement in the Saudi market.

---

## Platform

| | |
|---|---|
| Platform | ServiceNow IRM (Integrated Risk Management) |
| Instance | Personal Developer Instance — Australia release (latest) |
| Instance URL | dev383370.service-now.com |
| Modules | Policy and Compliance Management · Risk Management · Authority Document Management · Reporting · Dashboards |

---

## Author

**Kay Shahbaaz**  
Cybersecurity GRC Analyst & Auditor and AI Governance Researcher with hands-on experience across NCA ECC, NCNICC, SAMA CSF, PDPL, ISO 27001, and ISO 42001.

[GitHub](https://github.com/kayShahbaaz)