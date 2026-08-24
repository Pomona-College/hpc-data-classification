---
title: "Identifying Data Types"
teaching: 25
exercises: 15
---

::::::::::::::::::::::::::::::::::::: objectives
- Understand the Proprietary and Restricted tiers in detail
- Identify which tier applies to specific research data
- Recognize examples of Proprietary and Restricted data across disciplines
::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: questions
- How do I know if my data is Proprietary or Restricted?
- What makes data Restricted versus Proprietary?
- What are common examples of each tier?
::::::::::::::::::::::::::::::::::::::::::::::::

## Tier 2: PROPRIETARY

**Definition:** Data that provides competitive or institutional advantage and would cause harm if disclosed to unauthorized parties. Access is restricted to specific authorized individuals. Examples include unpublished research, grant proposals, sensitive personnel data, and data needing group-level access control beyond simple sharing.

### Characteristics

- **Availability:** Restricted to specific authorized individuals (may be broader than one person, but not unrestricted)
- **Sensitivity:** Loss or disclosure would cause business/institutional/competitive harm; or contains sensitive information requiring controlled access
- **Examples:** Grant proposals, unpublished research findings, patent disclosures, business plans, salary information, data requiring departmental/group-level access controls
- **Regulatory concern:** Varies; may involve intellectual property or institutional policy

### Key Features

| Aspect | Details |
|--------|---------|
| **Encryption** | Recommended, especially for sensitive proprietary data |
| **Access controls** | User-level or group-level restrictions (specific individuals or authorized group members) |
| **Storage** | `/rhome` or `/bigdata` with 750 permissions (canonical PROPRIETARY) |
| **Sharing** | Restricted; requires explicit authorization |
| **Retention** | Until publication or as specified by PI |
| **Audit logging** | Recommended for highly sensitive data |
| **Transfers** | Use secure channels; encryption recommended |
| **File permissions** | 750 (canonical PROPRIETARY). A 600 (user-only) variant is acceptable for sub-team-only files but is a *variant* of PROPRIETARY handling, not a separate tier. |

### Examples from Pomona Research

- **Grant proposal (pre-award)**: NSF CAREER proposal being prepared; not yet submitted
  - Why Proprietary? Competitive; other labs might be pursuing similar ideas
  - Classification changes: Becomes Public after award announcement

- **Patent disclosure**: Novel data suggesting patentable methodology
  - Why Proprietary? Patent novelty requires non-disclosure until filing
  - Classification changes: Becomes restricted once patent filed (legal privilege)

- **Unpublished novel findings**: Preliminary data showing unexpected biological phenomenon
  - Why Proprietary? Competitive advantage if first to publish
  - Classification changes: Becomes Public once published

- **Industry collaboration data**: Preliminary results from partnership with a biotech firm
  - Why Proprietary? Contractual confidentiality clause
  - Classification changes: Determined by collaboration agreement

- **Personnel data**: Staff salaries, performance reviews, contact information
  - Why Proprietary? Privacy and institutional policy
  - Classification changes: Remains Proprietary indefinitely (or moves to Restricted if PII)

::::::::::::::::::::::::::::::::::::: callout

### Encryption Recommendation for Proprietary Data

While not required, encryption is **strongly recommended** for Proprietary data because:
- Grant proposals are highly valuable
- Unencrypted data on shared clusters can be breached (misconfigured permissions)
- Intellectual property loss has lasting consequences
- Encryption requires minimal effort with modern tools
::::::::::::::::::::::::::::::::::::::::::::::::

## Tier 3: RESTRICTED

**Definition:** Data that is strictly confidential and requires the highest level of protection. Unauthorized access could result in legal liability, regulatory violation, privacy harm, or security risk. Encryption is mandatory.

### Characteristics

- **Availability:** Strictly limited to authorized individuals; audit trails required
- **Sensitivity:** Disclosure would violate law, regulation, or privacy rights
- **Examples:** Student education records (FERPA), export-controlled research (EAR/ITAR), personally identifiable information (PII), health information (HIPAA), Controlled Unclassified Information (CUI)
- **Regulatory concern:** High; violations can result in federal penalties

### Key Features

| Aspect | Details |
|--------|---------|
| **Encryption** | **REQUIRED** (AES-256-GCM via gocryptfs) |
| **Access controls** | Strict user-level controls; specific authorization required |
| **Storage** | `/rhome` or `/bigdata` in encrypted container |
| **Sharing** | Extremely restricted; institutional/legal approval required |
| **Retention** | Governed by regulation or legal requirement |
| **Audit logging** | **REQUIRED**; all access must be logged |
| **Transfers** | Prohibited without encryption in transit; approved channels only |
| **Destruction** | Secure deletion required at end of retention period |
| **File permissions** | 700+gocryptfs (encrypted container with strict access) |

### Examples from Pomona Research

**FERPA-Protected Data (Student Education Records)**
- Student grades from a research study
- Student names linked to academic performance data
- Email addresses combined with performance metrics
- Encryption: **REQUIRED**
- Access: Only researchers and authorized staff

**Export-Controlled Research (EAR/ITAR)**
- Advanced materials research potentially useful for military applications
- Cryptographic algorithms and implementations
- Semiconductor design specifications
- Biotech dual-use research of concern (DURC)
- Encryption: **REQUIRED**
- Access: Only authorized personnel (typically U.S. citizens on approved projects)

**Personally Identifiable Information (PII)**
- Names + social security numbers
- Names + financial information (bank accounts, credit cards)
- Genetic data linked to identifiable information
- Medical records
- Encryption: **REQUIRED**
- Access: Only individuals with explicit need-to-know

**Controlled Unclassified Information (CUI)**
- Research data funded by Department of Defense
- Cybersecurity/critical infrastructure research
- Biological agents research data
- Encryption: **REQUIRED**
- Audit logging: **REQUIRED**

::::::::::::::::::::::::::::::::::::: challenge
### Challenge 4.1: Classify Pomona Research Datasets (Part 2)

For each dataset, identify the appropriate classification and explain your reasoning:
1. **Neuroscience Lab Dataset:**
   - fMRI brain scans from participants (no names, coded with ID numbers)
   - Demographic data: age, gender (de-identified, statistical summary only)
   - Raw brain images linked to participant ID codes
2. **Chemistry Lab Dataset:**
   - Synthesis procedures for novel catalysts (before publication)
   - Final published paper in *Nature Chemistry* with all data

::::::::::::::::::::::::::::::::::::: solution

## Solution

1. fMRI scans without names → **Proprietary** (valuable research asset); demographic summary → **Public** (aggregated, shared within group); raw images linked to IDs → **Restricted** (re-identification risk)
2. Pre-publication procedures → **Proprietary** (competitive); published paper → **Public**

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints
- Proprietary data is restricted to specific authorized individuals; encryption recommended
- Restricted data requires mandatory encryption (AES-256-GCM via gocryptfs) and audit logging
- File permissions: PUBLIC=755, PROPRIETARY=750 (canonical; 600 variant for sub-team-only files), RESTRICTED=700+gocryptfs
- FERPA, EAR/ITAR, CUI, and PII data are automatically Restricted
- When in doubt, classify conservatively and ask your PI
::::::::::::::::::::::::::::::::::::::::::::::::
