---
title: Instructor Notes
---

## Instructor Guide for Workshop 14: Data Classification and Handling

This document provides guidance for instructors delivering this workshop to Pomona College researchers.

### Workshop Overview

- **Target Audience:** All Sagehen HPC users (mandatory)
- **Duration:** 6 hours (typically 2 × 3-hour sessions)
- **Delivery Format:** Carpentries Workbench with hands-on exercises
- **Learning Style:** Mix of lecture (regulatory context), worked examples (decision trees), and hands-on exercises (setting permissions, creating encrypted containers)

### Instructor Preparation

**Before teaching:**

1. Familiarize yourself with:
   - FERPA, HIPAA, EAR/ITAR, NIST 800-171 basics
   - Pomona's Information Security Policy
   - gocryptfs setup and usage
   - Current Sagehen storage and encryption capabilities

2. Test the technical components:
   - gocryptfs initialization, mounting, unmounting
   - File permission changes (chmod, chown)
   - Storage quotas on /rhome and /bigdata
   - Backup procedures

3. Gather institutional context:
   - Contact ORSP for export control guidelines
   - Verify current Pomona Box/OneDrive policies
   - Understand IRB approval requirements
   - Know relevant compliance deadlines

4. Prepare anecdotes:
   - Case studies from Pomona research (with permission)
   - Real data breach scenarios (anonymized)
   - Success stories of proper classification

**Equipment needed:**

- Laptop/desktop with SSH access to Sagehen
- Projector for demonstration
- Whiteboard or digital canvas for drawing decision trees
- Access to live Sagehen systems (not just slides)

### Episode-by-Episode Guidance

#### Episode 1: Why Classify Data? (45 min teaching + 15 min exercises)

**Key Points to Emphasize:**

1. **Business impact, not just compliance:**
   - Cost of breach (data + reputation + legal)
   - Competitive advantage of protecting IP
   - Funding agency requirements

2. **Real-world scenarios:**
   - Engage with stories your audience recognizes
   - Reference actual breaches at research institutions
   - Discuss what happened to other colleges' programs

3. **Regulatory landscape:**
   - Don't be overly legalistic (they're researchers, not lawyers)
   - But be clear: violations have real consequences
   - Make compliance feel achievable, not burdensome

**Common Misconceptions:**

- "My data is not sensitive; nobody would want to steal it"
  → Counter: Breach can happen due to misconfiguration, not targeted attack

- "Classification is just extra bureaucracy"
  → Counter: Classification prevents bigger bureaucracy (incident response, investigations)

- "The university will handle security; I don't need to worry"
  → Counter: PIs are responsible; ITS enables, but PI owns decisions

**Exercises:**

- Challenge 1.1: Have participants identify regulations for realistic scenarios
  - Get them comfortable mapping data → regulation
  - Normalize looking things up (ORSP) rather than guessing

- Challenge 1.2: Cost estimation exercise
  - Makes compliance feel concrete ($, not abstract)
  - Often surprises participants how expensive breaches are

**Time Allocation:**
- Breach scenario: 10 min (story)
- Classification tiers visual: 15 min (explain each tier)
- Real-world scenarios: 15 min (3 scenarios, 5 min each)
- Regulatory frameworks: 5 min (overview)
- Challenges: 15 min (exercises)

#### Episode 2: Three Tiers (60 min teaching + 30 min exercises)

**NOTE:** This episode covers the three-tier system. References to four-tier system, Internal tier, or INTERNAL classification should be removed or updated to map INTERNAL data to PUBLIC tier (for shared group data) or PROPRIETARY tier (if sensitive).

**Key Points to Emphasize:**

1. **Tier stacking:**
   - Each tier inherits requirements from tier below
   - Restricted = strictest (encryption, audit, access controls)
   - Public = most permissive (anyone, anything)

2. **Classification depends on content, not format:**
   - .csv file can be any tier (depends on data)
   - Don't judge by extension; judge by sensitivity

3. **Proprietary vs. Restricted is the trickiest distinction:**
   - Proprietary = competitive harm (business loss)
   - Restricted = legal/privacy harm (compliance violation)
   - Example: Patent disclosure (Proprietary) vs. Student grades (Restricted)

**Common Misconceptions:**

- "All sensitive data is Restricted"
  → Counter: Proprietary can be sensitive; distinction is about regulation/law

- "FERPA only applies to Pomona students"
  → Counter: If your study involves ANY student, FERPA principles apply (even if study is external)

- "Export control is only for big research projects"
  → Counter: Novel cryptography (even if just for a class project) can be controlled

**Walkthrough Examples:**

Use the published detailed examples in the episode:
- **FERPA scenarios:** Walk through each variant (names, aggregation, etc.)
- **Export control:** Discuss the chemistry/CS labs cases
- **PII:** Show names + data that seems innocuous (age + gender + diagnosis)

**Exercises:**

- Challenge 2.1: Classification practice (4 datasets)
  - Check answers; discuss reasoning if they differ
  - Normalize uncertainty; some cases are genuinely ambiguous

- Challenge 2.2: Real-world scenario (medical imaging)
  - Multifaceted; touches HIPAA, publication, cloud storage
  - Great for discussing complexity of real research

**Time Allocation:**
- Tier 1 (Public): 10 min
- Tier 2 (Proprietary): 12 min (most common confusion)
- Tier 3 (Restricted): 15 min (most important; requires encryption)
- Decision tree: 8 min (walk through step-by-step)
- Challenges: 30 min

**Red Flags to Watch For:**

- Participant saying "I'll just make everything Restricted to be safe"
  → Advise against (burden); use decision tree to refine classification

- Participant unsure about export control
  → Normalize: "Contact ORSP; this is their job. You can proceed with classification, mark as Uncertain"

#### Episode 3: Classifying Your Data (50 min teaching + 40 min exercises)

**Key Points to Emphasize:**

1. **Classification is ongoing:**
   - Not a one-time event
   - Changes as research evolves (draft → published)
   - Review annually

2. **Documentation is key:**
   - Form completes the classification process
   - Future you (or successor) needs to know why
   - Audit trail protects the PI

3. **When in doubt, escalate:**
   - Better to ask PI/ORSP than misclassify
   - Default assumption: Restricted (safer)

**Worksheet Guidance:**

Walk through the classification decision form:
- Explain each field
- Show real examples (fictional from your lab)
- Emphasize it's a thinking tool, not bureaucracy

**Exercises:**

- Challenge 3.1: Classify participant's own data
  - This is the crux of the workshop
  - Best if they bring real datasets
  - Provide time to work; circulate and help
  - Discuss edge cases as a group

- Challenge 3.2: Reclassification scenario
  - Shows data lifecycle
  - Useful for publication planning
  - Helps participants plan future transitions

**Time Allocation:**
- Inventory workflow: 10 min
- Understanding content: 10 min
- Applying rules systematically: 10 min
- Documentation: 10 min
- Scenarios (3 detailed examples): 15 min
- Challenges: 40 min (important; let participants work)

**Facilitation Tips:**

- Encourage peer discussion ("What would you classify this as?")
- No judgment on "wrong" answers; use them as teaching moments
- Celebrate ambiguous cases ("Good catch! This is why we consult ORSP")

#### Episode 4: Handling Requirements (45 min teaching + 35 min exercises)

**Key Points to Emphasize:**

1. **Classification without implementation is useless:**
   - A dataset is only Restricted if you actually encrypt it
   - Access control is only secure if permissions match policy

2. **Practical constraints:**
   - /rhome quota limits where Restricted data can go
   - /bigdata backups affect encryption strategy
   - Group management adds coordination overhead

3. **Audit logging is required for compliance:**
   - Not just "nice to have"
   - Demonstrates due diligence if breach occurs
   - Can detect unauthorized access early

**File Permissions Walkthrough:**

Use live terminal to show:
```bash
# Create example directories
mkdir -p /tmp/demo/{public,internal,proprietary,restricted}

# Set permissions for each tier
chmod 644 /tmp/demo/public/sample.txt    # world-readable
chmod 640 /tmp/demo/internal/sample.txt  # group-readable
chmod 600 /tmp/demo/proprietary/sample.txt  # owner-only

# Show the results
ls -la /tmp/demo/*/
```

**Access Control Matrix:**

Create a visual showing who can access what:

```
                Public      Internal    Proprietary    Restricted
Yourself        ✓✓✓         ✓✓✓         ✓✓✓            ✓✓✓
Lab members     ✓✓✓         ✓✓✓         ✓              -
External collab ✓✓✓         ✗           ✓(agreement)   -
Anonymous       ✓✓✓         ✗           ✗              ✗

Legend: ✓✓✓ = full access, ✓ = restricted access, ✗ = no access
```

**Audit Logging:**

Show simple manual logging:
```bash
# Create access log
date >> ACCESS_LOG.txt
echo "User: $(whoami), File: data.csv, Action: READ" >> ACCESS_LOG.txt
```

**Exercises:**

- Challenge 4.1: Set up access controls
  - Hands-on in terminal
  - Verify with `ls -la` and `id`
  - Troubleshoot permission issues

- Challenge 4.2: Audit logging scenario
  - One-week exercise (optional, for follow-up)
  - Builds awareness of what to log

**Time Allocation:**
- Public data: 5 min
- Internal data: 10 min (permission setup)
- Proprietary data: 10 min (access control complexity)
- Restricted data: 15 min (encryption critical)
- Summary table: 5 min
- Challenges: 35 min

#### Episode 5: Storage and Encryption (60 min teaching + 40 min exercises)

**Key Points to Emphasize:**

1. **gocryptfs is tool, not magic:**
   - It helps; it doesn't replace access control
   - Passphrase is critical; loss = data loss
   - Mounting/unmounting workflow is essential

2. **Storage strategy matters:**
   - /rhome for Restricted (small, backed up)
   - /bigdata for large data (backed up encrypted containers only)
   - Plan storage before encrypting

3. **Encryption is not just a technical step:**
   - It's a compliance requirement for Restricted data
   - It's a PII protection measure
   - It's also a statement: "This data is sensitive"

**Live Demonstration:**

Do a live gocryptfs setup (15 min):

```bash
# Show step-by-step
mkdir -p demo_encrypted demo_mount

gocryptfs -init demo_encrypted/
# Prompt for password: use "DemoPass123!" (say it out loud to show)

gocryptfs demo_encrypted/ demo_mount/

# Create test files
echo "This is sensitive data" > demo_mount/test.txt

# Show encrypted state
ls demo_encrypted/
# Shows random character filenames

# Unmount
fusermount -u demo_mount/

# Files are inaccessible
ls demo_mount/
# Empty!

# Remount
gocryptfs demo_encrypted/ demo_mount/
cat demo_mount/test.txt
# "This is sensitive data" (recovered!)
```

**Backup Strategy Diagram:**

Show visually:
```
WRONG (backs up unencrypted data):
mount gocryptfs
backup /mount/restricted/
↓ This backs up plaintext!

RIGHT (backs up encrypted data):
unmount gocryptfs
backup /encrypted_base/
↓ This backs up ciphertext (safe!)
```

**Exercises:**

- Challenge 5.1: Create encrypted container
  - Hands-on; slow down to let participants follow
  - Troubleshoot password issues (common)
  - Celebrate successful mount/unmount

- Challenge 5.2: Storage planning
  - Combines classification, encryption, permissions
  - Good capstone for storage section

**Time Allocation:**
- Storage architecture: 8 min
- Encryption concepts: 10 min
- gocryptfs intro: 7 min
- Setup steps: 25 min (detailed walkthrough)
- Backup strategy: 10 min
- Challenges: 40 min

**Troubleshooting Tips:**

- "Wrong password" → Remind: Passphrases are case-sensitive; use password manager for safety
- "Already mounted" → Show `mount | grep gocryptfs` to find existing mounts
- "Quota exceeded" → Explain trade-off: /rhome is faster/backed-up but smaller; /bigdata is larger but not backed-up

#### Episode 6: Sharing and Collaboration (55 min teaching + 35 min exercises)

**Key Points to Emphasize:**

1. **Data sharing is complex:**
   - Not just "click and send"
   - Legal agreements required for proprietary
   - De-identification required for restricted

2. **De-identification is an art and science:**
   - Removing names isn't enough
   - Combinations can re-identify
   - No hard rules; case-by-case judgment

3. **Publication is opportunity, not burden:**
   - Sharing data increases impact
   - Repositories give DOI for citation
   - De-identification enables public sharing of sensitive research

**De-identification Walkthrough:**

Use the student survey example step-by-step:

```
BEFORE (identifiable):
name,age,exam_score,absences
Alice,20,92,2
Bob,21,87,1

STEP 1: Remove direct identifiers
age,exam_score,absences
20,92,2
21,87,1
↓ Still identifiable in small cohort

STEP 2: Generalize quasi-identifiers
age_range,exam_score,absences
20-21,92,2
20-21,87,1
↓ Harder to identify but individual scores still visible

STEP 3: Aggregate
age_range,mean_score,std_score
20-21,89.5,3.54
↓ No individual-level data; publication-safe
```

**Collaboration Agreement Checklist:**

Show template; discuss each clause:
- Data description (what exactly?)
- Use restrictions (what are they allowed to do?)
- Duration (how long can they keep it?)
- Security (how must they protect it?)
- IP (who owns results?)

**Export Control Red Flags:**

Ask participants: "Does your research involve...?"
- Novel cryptography → Probably EAR
- Advanced materials → Maybe EAR
- Biological agents → Maybe DURC
- Military applications → Definitely controlled

If "maybe" or "yes" → Consult ORSP

**Exercises:**

- Challenge 6.1: De-identification assessment
  - Identify risks, propose fixes, assess residual risk
  - Great for building judgment
  - Discuss why certain approaches work/don't work

- Challenge 6.2: Sharing decision tree
  - Combines all 6 episodes
  - Tests decision-making ability
  - Good capstone for entire workshop

**Time Allocation:**
- Sharing problem: 5 min
- Public/Internal/Proprietary: 10 min
- Restricted data & de-identification: 20 min
- De-identification techniques: 15 min
- Cloud storage options: 10 min
- Publishing & export control: 10 min
- Challenges: 35 min

---

### Assessment and Certification

**Knowledge Check (Optional Post-Workshop Quiz)**

Sample questions:

1. Student survey data linked to student IDs is what classification?
   A) Internal   B) Proprietary   **C) Restricted**   D) Public

2. What encryption algorithm does gocryptfs use?
   A) DES   **B) AES-256-GCM**   C) MD5   D) SHA-256

3. Which storage location is backed up and has smaller quota?
   **A) /rhome**   B) /bigdata   C) Both equally   D) Neither backed up

4. Can you share Restricted data (student grades) with external collaborators?
   A) Yes, with encryption
   **B) Only if de-identified; encrypted containers don't exempt from de-ID**
   C) Yes, with collaboration agreement
   D) No, never

5. Export control (EAR/ITAR) applies to:
   A) All research
   B) Only military-funded research
   **C) Research with certain technical content (cryptography, materials, biotech)**
   D) Only research shared internationally

**Completion Certificate**

Provide certificate requiring:
- Attendance at all 6 episodes (or watchable recordings)
- Completion of challenges (or equivalent hands-on exercise)
- Passing knowledge assessment (e.g., 80% on quiz)
- Signed acknowledgment of Pomona ISP

---

### Common Facilitation Challenges

**Challenge: Participant's data has export control implications**

Response:
- Don't try to determine export status yourself
- Offer to put them in touch with ORSP
- Continue with workshop; mark as "uncertain" in classification
- Reassure: This is normal; ORSP is used to vague questions

---

**Challenge: Participant overwhelmed by complexity**

Response:
- Normalize it: "Data classification gets easier with practice"
- Offer systematic approach: Use decision tree, consult when uncertain
- Break down into steps: Classify first, implement later
- Provide resources: They don't need to memorize everything

---

**Challenge: Participant wants to store everything as Restricted (over-classifying)**

Response:
- Validate concern (better safe than sorry mentality is reasonable)
- Explain burden: Encryption overhead, storage quota limits, collaboration friction
- Suggest: Use decision tree to be precise; ask PI if still uncertain
- Reassure: Being slightly over-cautious is better than being lax, but being precise is ideal

---

**Challenge: Participant has no Restricted data (thinks workshop doesn't apply)**

Response:
- Remind: Workshop is mandatory for all users
- Explain: Even labs with only Public/Internal data must understand the system
  - Prevents misclassification later
  - Builds institutional culture of security
  - May help colleagues/students with classified data
- Reassure: Quick to get through; no hands-on needed for unclassified data

---

### Timing and Pacing

**Suggested Two-Session Schedule**

**Session 1 (3 hours): Why and How**
- Episode 1: Why Classify (45 min teaching + 15 min exercises)
- Episode 2: Three Tiers (60 min teaching + 30 min exercises)
- Episode 3: Classifying Your Data (50 min teaching + 25 min exercises)
- **Total:** 3 hours 45 min (trim as needed)

**Session 2 (3 hours): Implementing and Sharing**
- Episode 4: Handling Requirements (45 min teaching + 20 min exercises)
- Episode 5: Storage and Encryption (60 min teaching + 30 min exercises)
- Episode 6: Sharing and Collaboration (55 min teaching + 20 min exercises)
- **Total:** 3 hours 50 min (trim as needed)

**Trimming Tips** (if time is limited):

- Episode 1: Skip detailed breach cost analysis; focus on compliance
- Episode 2: Don't cover every example; focus on FERPA + export control
- Episode 3: Provide pre-made classification worksheets; don't design from scratch
- Episode 4: Skip manual audit logging; mention it as alternative to automated
- Episode 5: Demo gocryptfs live, but don't require all participants to execute
- Episode 6: Focus on de-identification; skip international export control depth

---

### Follow-Up and Support

**After the Workshop**

Send email to participants:

```
Subject: Workshop 14 - Next Steps

Hi [Participants],

Thanks for attending Workshop 14: Data Classification and Handling!
Here's what to do next:

1. CLASSIFY YOUR LAB'S DATA
   Use the worksheet from Episode 3 to classify your datasets.
   Send classification summary to your PI for approval.

2. IF YOU HAVE RESTRICTED DATA
   Follow Episode 5 to set up gocryptfs encryption.
   Test mount/unmount workflow.
   Contact its-hpc@pomona.edu if issues arise.

3. DOCUMENT ACCESS CONTROLS
   Create access authorization list (template in Episode 4).
   Share with your PI.
   Update annually.

4. QUESTIONS?
   📧 its-hpc@pomona.edu (data classification & encryption)
   📧 orsp@pomona.edu (export control, FERPA, IRB questions)
   🔗 https://pomona-college-hpc.github.io/sagehen/ (Sagehen docs)

Your PI may require completion certification before enabling full cluster access.

Best regards,
[Instructor Name]
```

**Common Follow-Up Questions**

**Q:** "I don't have Restricted data yet; can I skip encryption setup?"
A:** You can defer it, but better to test now when stakes are low. Use demo data.

**Q:** "Can I store my encrypted container on /bigdata?"
A:** Yes, if you back up the encrypted_base directory (not the mount point).

**Q:** "What if I forget my gocryptfs passphrase?"
A:** Data is unrecoverable (AES-256 can't be brute-forced). Use password manager.

**Q:** "Do I need to encrypt Proprietary data?"
A:** Not required, but recommended if highly sensitive (e.g., patent disclosures).

**Q:** "Can I share a gocryptfs passphrase with my lab?"
A:** Not recommended. Audit trail can't distinguish who accessed what. Better: Multiple encrypted containers per user or shared group mount.

---

### Resources for Instructors

**Internal (Pomona) Resources**
- ORSP contact: orsp@pomona.edu
- ITS contact: its-hpc@pomona.edu
- Sagehen docs: https://pomona-college-hpc.github.io/sagehen/
- ISP policy: https://www.pomona.edu/its/

**External Resources**
- NIST SP 800-171: https://csrc.nist.gov/publications/detail/sp/800-171/rev-2
- FERPA guide: https://www2.ed.gov/policy/gen/guid/fpco/ferpa/
- EAR/ITAR basics: https://www.bis.doc.gov/index.php/regulations/export-administration-regulations-ear
- gocryptfs docs: https://nuetzlich.net/gocryptfs/

**Training Materials**
- Carpentries Best Practices: https://carpentries.org/
- Creating Effective Handouts: https://carpentries.org/instructor-training/
- Example assessment: https://carpentries.org/assessment/

---

## Conclusion

This workshop fills a critical gap: teaching researchers how to protect their data while maintaining research productivity. Your role as instructor is to:

1. **Make it real:** Use stories, not just policies
2. **Make it practical:** Show hands-on examples, not just concepts
3. **Make it safe:** Normalize asking for help; don't expect them to be experts
4. **Make it sustainable:** Focus on repeatable workflows, not one-time setup

Thank you for protecting Pomona research!
