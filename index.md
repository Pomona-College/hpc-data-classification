---
title: Data Classification and Handling
---

# Data Classification and Handling

> **MANDATORY WORKSHOP**
>
> This workshop is mandatory for all users storing research data on the Sagehen HPC cluster.
> Completion of this workshop is required before your research computing account can be fully activated.

### Why This Workshop Matters

Research data is one of Pomona College's most valuable and sensitive assets. Every day, researchers on Sagehen store data ranging from public course materials to export-controlled research findings, from published papers to students' confidential grades. The way we handle this data (who can access it, how we store it, how we share it) determines whether we comply with federal regulations, protect research integrity, and safeguard our community.

This workshop teaches you **Pomona's three-tier data classification system** and the specific security controls required for each tier. By the end of this workshop, you'll be able to:

- Classify your research data correctly
- Understand the handling requirements for each classification level
- Store data securely on Sagehen with appropriate encryption and access controls
- Share data with collaborators while maintaining compliance
- Recognize and report data security incidents

:::::::::::::::::::::::::::::::::::::::: prereq

### Prerequisites

This workshop assumes you have:
- Basic knowledge of HPC cluster usage (Workshop 01: HPC Cluster Basics)
- An active Sagehen account and can log in via SSH (Workshop 02: Account Setup and Login)
- Basic familiarity with Linux file permissions and command-line tools

If you're new to Pomona's HPC cluster, please complete Workshops 01 and 02 first.

::::::::::::::::::::::::::::::::::::::::::::::::

### What You'll Learn

| Episode | Focus |
|---------|-------|
| **01 - Why Classify Data?** | The business case, compliance landscape, and real-world consequences of data breaches |
| **02 - Three Tiers** | Detailed classification system: Public, Proprietary, Restricted |
| **03 - Classifying Your Data** | Decision tree and scenarios to classify your own research data |
| **04 - Handling Requirements** | Access controls, audit requirements, and retention policies per tier |
| **05 - Storage and Encryption** | Sagehen storage options, encryption tools (gocryptfs), file permissions |
| **06 - Sharing and Collaboration** | Sharing with collaborators, external transfers, publishing, de-identification |

### Key Facts About Data Classification at Pomona

- **Three tiers** (Public, Proprietary, Restricted) with increasing security requirements
- **Public data** can be fully public or shared freely within lab groups
- **Restricted data requires encryption** using gocryptfs (AES-256-GCM) before storage on Sagehen
- **Your PI is responsible** for classifying data before it goes on the cluster
- **Violations can result in** data loss, incident response, loss of computing privileges, or legal action
- **Incident reporting:** Email its-hpc@pomona.edu if you suspect a data breach

### About This Workshop

- **Duration:** about 7.5 hours (typically delivered in 2 sessions)
- **Prerequisites:** HPC Cluster Basics (Workshop 1), Account Setup and Login (Workshop 2)
- **Format:** Carpentries Workbench with hands-on exercises
- **Instructor:** Andrew Wilson, Director of Research Computing, Pomona College ITS
- **Contact:** its-hpc@pomona.edu

### Compliance Frameworks

This workshop ensures your compliance with:

- **NIST SP 800-171**: Safeguarding controlled unclassified information (CUI)
- **FERPA**: Family Educational Rights and Privacy Act for student records
- **EAR/ITAR**: Export control for research with military/dual-use implications
- **Pomona Information Security Policy**: Institutional data protection standards
- **Pomona HPC Usage Policy**: Cluster-specific security requirements

### How to Use This Workshop

1. **Work through episodes in order**: Each builds on the previous one
2. **Classify your own data**: Use Episode 03's decision tree with your research datasets
3. **Implement controls**: Apply Episode 05's guidance to your current storage
4. **Document your decisions**: Keep records of classification decisions for audit purposes
5. **Ask questions**: Reach out to its-hpc@pomona.edu if anything is unclear

### Storage Quick Reference

| Classification | Location | Encryption | Access | Permissions | Typical Data |
|---|---|---|---|---|---|
| **Public** | `/rhome` or `/bigdata` | Not required | Anyone/group | 755 or 750 | Published papers, course materials, lab notebooks |
| **Proprietary** | `/rhome` or `/bigdata` | Recommended | Restricted | 750 or 600 | Grant proposals, personnel data, unpublished research |
| **Restricted** | `/rhome` or `/bigdata` | **Required** (gocryptfs) | Specific users | 700+gocryptfs | Student records, CUI, PII, EAR/ITAR, health data |

### Important Policies and Documents

Before taking this workshop, familiarize yourself with:

- [Pomona Information Security Policy](https://www.pomona.edu/about/policies)
- [HPC Usage Policy](https://pomona-college.github.io/usage-policy/)
- [Data Classification Guide](https://www.pomona.edu/its/)
- [Sagehen Cluster Documentation](https://pomona-college.github.io/sagehen/)

---

**Ready to get started?** Begin with [Episode 01: Why Classification Matters](episodes/01-why-classification-matters.md)

**Questions?** Contact Andrew Wilson at its-hpc@pomona.edu or visit ITS during office hours.

## Acknowledgments

Developed by **Andrew Wilson**, Director of Research Computing and Digital
Scholarship at Pomona College, with **Andrei Motchenko**, who tested, edited
and produced screenshots for the workshop series.
