---
title: "De-identification and Best Practices"
teaching: 25
exercises: 15
---

::::::::::::::::::::::::::::::::::::: objectives
- De-identify and prepare data for external transfer or publication
- Apply de-identification techniques (removal, aggregation, generalization, perturbation)
- Publish data in repositories while protecting sensitive information
- Recognize course-wide best practices for data classification and handling
::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: questions
- What does "de-identification" mean, and when is it required?
- What techniques can I use to de-identify data?
- How do I publish my data while protecting privacy?
- What are the key best practices from this workshop?
::::::::::::::::::::::::::::::::::::::::::::::::

## What Is De-identification?

De-identification removes (or obscures) information that could identify individuals, while preserving the research value.

### Identifying Information

Identifiers that must be removed or obscured:

| Category | Examples |
|----------|----------|
| **Direct identifiers** | Names, SSN, email, phone, address |
| **Quasi-identifiers** | Birth date, gender, ZIP code (in combination can re-identify) |
| **Linkable identifiers** | Medical record numbers, student ID numbers |
| **Biometric data** | Fingerprints, photographs, voice, DNA sequence |
| **Sensitive attributes** | Diagnosis, salary, grades (in combination can re-identify) |

## De-identification Techniques

### 1. Removal (Safest for Publication)

```bash
# Before (identifiable student data):
name,student_id,major,gpa
Alice Johnson,S12345678,Biology,3.85
Bob Smith,S87654321,Chemistry,3.72

# After (de-identified):
student_id,major,gpa
1,Biology,3.85
2,Chemistry,3.72
```

### 2. Aggregation (Reduces Detail)

```bash
# Before (identifiable):
student,exam_score
Alice,92
Bob,87
Carol,95

# After (aggregated):
major,mean_score,std_dev,n
Biology,89.3,3.5,15
Chemistry,87.1,2.8,18
```

### 3. Generalization (Reduces Precision)

```bash
# Before (specific, re-identifiable):
birth_date,diagnosis
1989-03-15,Type 2 Diabetes

# After (generalized):
birth_year,diagnosis
1989,Type 2 Diabetes
```

### 4. Perturbation (Adds Noise)

```bash
# Before:
name,height_cm,weight_kg
Alice,165,58

# After (add random noise):
height_cm,weight_kg
166±2,59±3
```

## De-identification Workflow

```
START: Identifiable research data (e.g., student survey)
   ↓
1. Identify what's identifiable
   (Names? IDs? Dates? Locations?)
   ↓
2. Choose de-identification method
   (Remove, aggregate, generalize, perturb?)
   ↓
3. Apply de-identification
   (Create new dataset from original)
   ↓
4. Verify no re-identification is possible
   (Could someone piece it back together?)
   ↓
5. Keep original (encrypted) separate from de-identified
   ↓
6. Share de-identified version
```

## Publication Workflow

To publish data based on Restricted sources: (1) de-identify using the techniques above, (2) clean data and add documentation (README, metadata, codebook, license), (3) choose a repository (Zenodo, OSF, NCBI, etc.), (4) upload and receive a DOI, (5) cite the DOI in your paper. Always keep the original identifiable data encrypted and separate from the de-identified version. Store any mapping files (original ID to anonymous ID) in your gocryptfs encrypted container.

## Course Summary

You've completed Workshop 14: Data Classification and Handling. You can now:

- Classify research data using Pomona's three-tier system (PUBLIC/PROPRIETARY/RESTRICTED)
- Implement security controls appropriate to each tier
- Store and encrypt Restricted data using gocryptfs (AES-256-GCM)
- Share data with collaborators while maintaining compliance
- De-identify sensitive data for publication
- Recognize and report data security incidents

**Next Steps:**

1. **Inventory and classify your lab's data**: Use the classification worksheets
2. **Set up encryption**: Create gocryptfs containers for Restricted data
3. **Document access controls**: Create access authorization lists
4. **Plan retention and deletion**: Know when data can be discarded

**For questions:**
- **Data classification / Encryption / Storage:** its-hpc@pomona.edu
- **Export control:** orsp@pomona.edu
- **IRB/FERPA questions:** orsp@pomona.edu

## Additional Resources

**Pomona Documents:**
- [Pomona Information Security Policy](https://www.pomona.edu/its/)
- [HPC Usage Policy](https://pomona-college.github.io/usage-policy)
- [Sagehen HPC User Guide](https://pomona-college.github.io/sagehen)
- [Data Classification Guide](https://www.pomona.edu/its/)

**External Standards:**
- [NIST SP 800-171](https://csrc.nist.gov/publications/detail/sp/800-171/rev-2) . Safeguarding CUI
- [FERPA Overview](https://www2.ed.gov/policy/gen/guid/fpco/ferpa/) . Student Privacy Law
- [EAR](https://www.bis.doc.gov/index.php/regulations/export-administration-regulations-ear) . Export Controls
- [HIPAA](https://www.hhs.gov/hipaa/) . Health Information Privacy

**Tools:**
- [gocryptfs Documentation](https://nuetzlich.net/gocryptfs/)
- [rclone](https://rclone.org/) . Cloud storage tool

::::::::::::::::::::::::::::::::::::: challenge
### Challenge 12.1: De-identification Assessment

You have health survey data (not HIPAA-covered, but sensitive):

```csv
name,email,phone,birth_date,zip_code,medical_condition,medication
Jane Smith,j.smith@email.com,555-0123,1985-04-15,91010,Type 2 Diabetes,Metformin
John Doe,j.doe@email.com,555-0124,1990-07-22,91010,Hypertension,Lisinopril
Jane Loo,j.loo@email.com,555-0125,1988-11-30,91010,Type 2 Diabetes,Metformin
```

Tasks:
1. Identify all re-identification risks (direct, quasi, sensitive)
2. Propose de-identification strategy
3. Create de-identified version
4. Assess residual re-identification risk

::::::::::::::::::::::::::::::::::::: solution

## Solution

**Risks:** Names (direct), emails (direct), phone (direct), birth_date (quasi), zip_code (quasi, only 3 records for 91010), medical_condition (sensitive), medication (sensitive)

**De-identification:**
- Remove: names, emails, phones, exact birth dates
- Generalize: birth_date → year only; zip_code → state
- Aggregate: medical_condition + medication together

**Result:**
```csv
birth_year,state,condition_medication
1985,CA,Diabetes/Metformin
1990,CA,Hypertension/Lisinopril
1988,CA,Diabetes/Metformin
```

**Residual risk:** Low (no direct identifiers, quasi-identifiers generalized, aggregated condition/med)

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints
- De-identification removes identifiers while preserving research value
- Four techniques: removal, aggregation, generalization, perturbation
- Keep mapping files encrypted and separate from de-identified data
- Publish data with DOI for reproducibility and impact
- Data use agreements formalize access and protection obligations
- Proper data classification protects your research, your community, and Pomona College
::::::::::::::::::::::::::::::::::::::::::::::::
