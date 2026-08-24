---
title: "Regulations and Compliance"
teaching: 20
exercises: 10
---

::::::::::::::::::::::::::::::::::::: objectives
- Learn about regulatory compliance requirements affecting Pomona College
- Understand FERPA, EAR/ITAR, and NIST SP 800-171 obligations
- Recognize which regulations apply to your research
::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: questions
- Which regulations apply to research at Pomona College?
- What are the consequences of regulatory violations?
- How do I know if my research falls under export control?
::::::::::::::::::::::::::::::::::::::::::::::::

## Legal Compliance

Pomona College is subject to multiple regulations that mandate data protection:

::::::::::::::::::::::::::::::::::::: callout

### FERPA: Family Educational Rights and Privacy Act

- Protects student education records (grades, assessments, personal information)
- Violation risk: Loss of federal funding, lawsuits
- **Your responsibility:** Any research involving Pomona students falls under FERPA

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: callout

### EAR/ITAR: Export Administration Regulations / International Traffic in Arms Regulations

- Controls research with military applications or dual-use potential
- Covers: Cryptography, aerospace, semiconductors, biotech, materials science
- Violation risk: Federal criminal charges, loss of export privileges
- **Your responsibility:** Even basic research can become subject to export control; consult ORSP before publishing

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: callout

### NIST SP 800-171: Safeguarding Controlled Unclassified Information

- Required for any research involving Department of Defense funding
- Mandates specific security controls for CUI data
- **Your responsibility:** DOD-funded projects must meet 800-171 controls or lose funding

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: callout

### Pomona Information Security Policy

- Institutional requirement for all data stored on college systems
- Defines classification tiers and required controls
- Violation risk: Loss of computing privileges, dismissal

::::::::::::::::::::::::::::::::::::::::::::::::

## FERPA Data Classification

Not all student data is Restricted. Here's how FERPA classification works:

| Data | Classification | Reason |
|------|---|---|
| Published study with anonymous aggregated student data | Public | No identification possible; fully public |
| Aggregated class grades (average GPA by major) | Public | No individual identification; shared within institution |
| List of students enrolled in BIOL 101 (with names but no grades) | Proprietary | Directory information, but protected by FERPA |
| Student grades linked to names or identifiers | **Restricted** | "Education record" under FERPA |
| Survey responses with student names or IDs | **Restricted** | Counts as education record if conducted by institution |

## Export Control: When Your Research Becomes Restricted

Some research isn't obviously restricted until analysis shows it might have export-control implications:

**Chemistry Lab:** Developing new catalysts for chemical synthesis
- Pure research → Public/Proprietary (early stage, depending on sharing within group or restricted)
- Novel catalyst with asymmetric properties → Discuss with ORSP
- If applicable to pharmaceutical manufacturing or weapons → **Restricted** (EAR)

**Computer Science Lab:** Cryptography research
- Academic paper on theoretical security proofs → Public (once published)
- Implementation of novel encryption algorithm (before publication) → **Restricted** (EAR Category 5, Part 2)
- Unclassified cryptographic software (even if open-source) → **Restricted** (EAR until published/reviewed)

**Biology Lab:** Genomics research
- Published analysis of human genome variation → Public
- Raw genomic data from participants → Restricted (FERPA + PII)
- Research on pathogenic organisms → Restricted (CUI or potential dual-use concern)

::::::::::::::::::::::::::::::::::::: challenge
### Challenge 2.1: Identify the Regulation

For each scenario, identify which regulation(s) apply:
1. A researcher stores student performance data for an education study
2. A lab works on cryptographic algorithms for secure communication
3. A faculty member manages payroll data for lab staff
4. A researcher analyzes publicly available Census data

::::::::::::::::::::::::::::::::::::: solution

## Solution

- (1) **FERPA**, Pomona ISP — student performance data is an education record
- (2) **EAR/ITAR** (if novel/advanced crypto), **NIST 800-171** (if DOD-funded)
- (3) **Pomona ISP** — personnel data = Proprietary at minimum
- (4) None specific (**Public**); standard Pomona ISP applies

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints
- Multiple regulations (FERPA, EAR/ITAR, NIST 800-171) drive Pomona's data policy
- FERPA protects student education records; violations risk federal funding
- Export controls (EAR/ITAR) apply to cryptography, advanced materials, and dual-use research
- NIST SP 800-171 governs DOD-funded research with CUI
- Pomona's Information Security Policy applies to all data on college systems
- When in doubt about export control, consult ORSP before sharing or publishing
::::::::::::::::::::::::::::::::::::::::::::::::
