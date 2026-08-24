---
title: "Why Data Classification Matters"
teaching: 20
exercises: 10
---

::::::::::::::::::::::::::::::::::::: objectives
- Understand why data classification is essential for research institutions
- Recognize the business, legal, and ethical stakes of data security failures
- Identify your role and responsibility in protecting research data
::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: questions
- Why should we classify data instead of treating everything the same?
- What happens if classified data is breached?
- Who is responsible for data classification?
::::::::::::::::::::::::::::::::::::::::::::::::

## The Cost of a Data Breach

Imagine this scenario: A biology lab at a mid-size research institution discovers that student genetic data from a research project (including names, phenotypes, and DNA markers) has been exposed on an unsecured server. The data wasn't encrypted. File permissions were misconfigured. Nobody noticed until a journalist investigating data privacy called the institution with questions.

::::::::::::::::::::::::::::::::::::: callout

## The Domino Effect of a Data Breach

What follows is:
- **Notification requirement:** Alerting 200+ students of the breach
- **Regulatory investigation:** FERPA violation inquiry from the U.S. Department of Education
- **Reputational damage:** Loss of trust from students, families, and collaborators
- **Legal liability:** Lawsuits from affected students
- **Operational costs:** Incident response, forensics, notifications, credit monitoring
- **Compliance consequences:** Corrective action plan, ongoing audits

::::::::::::::::::::::::::::::::::::::::::::::::

This isn't hypothetical. In 2019, over 500 million research records were breached across higher education institutions. The average cost per institution exceeded $2 million.

At Pomona College, we take a different approach: **classify data before it becomes a problem.**

## The Three-Tier System

Pomona College uses a simple but powerful framework: three tiers, each with specific handling requirements.

```
┌─────────────────────────────────────────────┐
│ PUBLIC                                      │
│ Encryption: NOT required                    │
│ Access: Unrestricted or shared with group   │
│ Example: Published papers, course materials,│
│          draft research shared with lab     │
└─────────────────────────────────────────────┘
         ↓
┌─────────────────────────────────────────────┐
│ PROPRIETARY                                 │
│ Encryption: RECOMMENDED                     │
│ Access: Restricted to authorized users      │
│ Example: Grant proposals, personnel data    │
└─────────────────────────────────────────────┘
         ↓
┌─────────────────────────────────────────────┐
│ RESTRICTED                                  │
│ Encryption: REQUIRED (AES-256-GCM)          │
│ Access: Strict controls + audit logging     │
│ Example: Student grades, CUI, export-ctrl  │
└─────────────────────────────────────────────┘
```

## Why Classification Matters at Pomona

### Business Impact

Beyond compliance:

- **Research integrity:** Unauthorized access can compromise your research validity
- **Competitive advantage:** Unpublished research or grant proposals are competitive assets
- **Institutional reputation:** Pomona's reputation for protecting data affects funding and partnerships
- **Insurance coverage:** Some data breaches aren't covered if proper controls weren't in place

## Real-World Scenarios

### Scenario 1: The Published Paper Nobody Meant to Share

Dr. Sarah's lab publishes a genomics study and deposits the processed dataset in a public repository (appropriately). But on Sagehen, the raw sequencing files (which can re-identify study participants) were stored in a standard `/bigdata` directory with permissive file permissions. A summer intern accidentally shared access to the entire directory with a collaborator. The raw data is now partially exposed.

**Problem:** Raw data should have been classified as Restricted and encrypted.

**Consequence:** FERPA violation, breach notification, loss of future research funding.

**Prevention:** Classify data, implement proper access controls, encrypt Restricted data.

---

### Scenario 2: The Intercepted Grant Proposal

A graduate student transfers a draft grant proposal (marked "Proprietary") from Sagehen to her laptop via SCP over an unencrypted connection, intending to work on it at home. The data is intercepted by someone on the same coffee shop WiFi. The competitor institution with whom you're competing for the same grant now knows your approach.

**Problem:** Proprietary data wasn't encrypted in transit.

**Consequence:** Lost funding opportunity, distrust from faculty advisor.

**Prevention:** Encrypt Proprietary data at rest and in transit; use secure channels like OneDrive+rclone.

---

### Scenario 3: The Oversharing AI Researcher

Dr. James uploads a dataset containing student survey responses to an AI model training service (in the cloud) to improve his analysis. The service's terms indicate data can be used for model improvement and shared with other customers. He didn't realize the data is Restricted (contains PII).

**Problem:** Restricted data left Pomona infrastructure without encryption and safeguards.

**Consequence:** Student privacy violation, compliance violation, potential legal action.

**Prevention:** Classify before transferring, de-identify Proprietary/Restricted data, get approval from ORSP/IRB.

---

### Scenario 4: The Helpful Graduate Student

A graduate student, tasked with managing her lab's data, sets up a shared folder on her personal Dropbox account to make it easier for the team to access files from home. The folder contains draft papers, preliminary data, and some student contact information.

**Problem:** Confidential institutional data on an unmanaged personal cloud account.

**Consequence:** Data loss if account is compromised, potential compliance violation, loss of control.

**Prevention:** Use Pomona-managed Box or OneDrive with encryption; classify all data first.

## Your Role and Responsibility

### Who Classifies Data?

The **Principal Investigator (PI)** is responsible for classifying research data before it goes on Sagehen. However:

- **You** must understand the classification system to implement it correctly
- **Your PI** sets policy for the lab's data
- **ITS Research Computing** reviews classification for DOD-funded projects and CUI

### What Happens If You Don't Classify?

1. **Default assumption:** All unclassified data is treated as **Restricted** for compliance purposes
2. **Access restriction:** Overly conservative access controls may impede collaboration
3. **Audit risk:** Unclassified data triggers security reviews
4. **Compliance violation:** Failure to classify is itself a policy violation

**Bottom line:** Classify proactively or face more restrictive (and inconvenient) handling.

### Incident Reporting

::::::::::::::::::::::::::::::::::::: callout

## Report Security Incidents Immediately

If you suspect a data breach or security incident:
1. **Stop working** with the affected data immediately
2. **Email its-hpc@pomona.edu** with:
   - What you observed
   - When you discovered it
   - What data may be affected
   - Any access logs or evidence
3. **Don't investigate further**; let ITS handle forensics

Reporting is not a punishment; it's how we prevent bigger problems.

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: challenge
### Challenge 1.1: Cost Estimation

Research the cost of a data breach at a higher education institution. Consider:
- Notification and credit monitoring
- Legal fees and settlements
- Lost funding due to compliance violations
- Reputational damage

What's the average cost to your institution per record breached?

::::::::::::::::::::::::::::::::::::: solution

## Solution

Typical answer: **$200–$500 per record**. For 1,000 records, that's $200,000–$500,000 minimum — not including reputational damage, lost research funding, or regulatory sanctions.

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints
- Data classification is mandatory at Pomona College
- Pomona uses three tiers: Public, Proprietary, Restricted
- Restricted data requires encryption (AES-256-GCM) using gocryptfs
- Data breaches have significant business, legal, and reputational costs
- PIs are responsible for classification; you implement it correctly
- Incident reporting is your responsibility; contact its-hpc@pomona.edu immediately if compromised
::::::::::::::::::::::::::::::::::::::::::::::::
