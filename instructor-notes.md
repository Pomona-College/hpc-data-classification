---
title: 'Instructor Notes'
---

## Workshop Overview

**Title:** Data Classification and Handling on Sagehen HPC
**Duration:** 3.5-4 hours (including breaks and discussion)
**Target Audience:** Faculty, researchers, graduate students, and lab managers
**Learning Outcomes:** Learners can classify research data according to Pomona's framework and implement appropriate security controls.

## Pre-Workshop Checklist

- [ ] Verify access to gocryptfs demo account and test encryption demo
- [ ] Prepare 3-4 real example datasets for case study analysis
- [ ] Have policy document accessible (hard copy and digital)
- [ ] Test OnDemand access and gocryptfs on Sagehen
- [ ] Review your institution's FERPA, HIPAA, and CUI policies
- [ ] Prepare data breach scenario case study
- [ ] Have a second monitor to display terminal and policy doc simultaneously
- [ ] Contact your IRB and research compliance office in case questions arise
- [ ] Collect real (anonymized) examples of classification mistakes if possible
- [ ] Prepare backup demo (video or slides) in case live tech fails

## Instructor Prerequisites

You should be familiar with:

- Pomona College's data classification policy
- Unix file permissions (`chmod`, `chgrp`, ACLs)
- gocryptfs (test it yourself first!)
- FERPA, HIPAA, and CUI basics
- Common data protection failures and their consequences
- Your institution's data governance structure and contacts

## Episode-by-Episode Teaching Guide

---

### Episode 1: Why Classify Data? (45 min teaching + 15 min discussion)

**Key Concepts:**
- Business, legal, and ethical consequences of data breaches
- Regulatory framework (FERPA, HIPAA, CUI, IRB)
- Cost of poor data handling
- Individual and institutional responsibility

**Teaching Approach:**

1. **Open with impact** (~10 min):
   Present a real or realistic data breach scenario:

   > "A biology lab at a research institution discovers that genetic data from a study (linked to participant names and phenotypes) was stored in an unencrypted folder with world-readable permissions. A visiting researcher found it and downloaded it. The institution was notified by a journalist calling to confirm details.
   >
   > What happens next? Notification to 200+ participants. FERPA/IRB investigation. Lawsuits. Reputational damage. $2+ million in response costs. The lab shuts down. The professor loses tenure prospects."

   Ask: "Has anything like this happened to you or someone you know?"

2. **Connect to learner's world** (~10 min):
   - Ask learners to share (anonymously) what data they work with
   - Write key types on board: genetic data, student records, health info, proprietary code, etc.
   - For each, ask: "What could go wrong if this was breached?"
   - This personalizes the stakes

3. **Explain the regulatory landscape** (~15 min):
   - FERPA: Student educational records (grades, transcripts, research participation)
   - HIPAA: Health information (medical records, genetic data linked to individuals)
   - CUI: Government research funding restrictions
   - IRB: Human subjects research protocols and data retention
   - Use a table or visual: "Who owns your data? What rules apply?"

4. **Discuss costs of failure** (~10 min):
   Show the numbers (2019 data breach study mentioned in episode):
   - Average cost per institution: $2+ million
   - Legal liability: Lawsuits from affected individuals
   - Remediation: Notifications, credit monitoring, incident response
   - Compliance: Ongoing audits, corrective action plans
   - Reputational: Loss of participant trust, trouble recruiting for future studies
   - Career: PIs may lose funding or positions

5. **Transition to solution** (~5 min):
   > "This is why we have a classification system. Simple, clear rules for different types of data. If you follow them, you protect:
   > - Individuals in your research
   > - Your lab and institution
   > - Your career
   > - Your collaborators' data
   >
   > Three tiers. Clear handling rules. That's what we're going to learn."

**Discussion Prompts:**

- "Why do you think data breaches are so expensive?"
- "Who is responsible if data is breached? The person who stored it? The PI? The institution?"
- "What's the difference between losing data (corruption) and having it stolen (breach)?"
- "Has FERPA or HIPAA affected your research?"

**Common Issues & Solutions:**

| Issue | Solution |
|-------|----------|
| Learners think "this won't happen to me" | Ask directly: "Are you sure?" Point to peer institutions' breaches |
| Confusion about who's responsible | Clarify: Everyone shares responsibility; PI is ultimately accountable |
| Defensive reactions ("I'm already careful") | Validate: "Great! This just formalizes best practices." |
| Overwhelming complexity | Reassure: "The three tiers make this simple. You'll see." |

**Timing Tips:**
- Don't rush this episode; emotional buy-in is critical
- If time is short, focus on "why it matters" over regulatory details
- Learners new to the topic may need extra context on FERPA/HIPAA

---

### Episode 2: The Three-Tier Classification System (40 min teaching + 15 min exercises)

**Key Concepts:**
- Three tiers: PUBLIC, PROPRIETARY, RESTRICTED
- PUBLIC includes both fully public and data shared within groups
- Key differentiators: encryption needs, access control, sharing permissions
- How to map real data to tiers
- Boundary cases and decision-making

**Teaching Approach:**

1. **Introduce the framework** (~5 min):
   Present a visual of the three tiers (use a table, pyramid, or flowchart):
   ```
   PUBLIC (unrestricted/group access) → PROPRIETARY (restricted access) → RESTRICTED (encrypted, legal controls)
   ```

   Explain: Each tier adds more protection and more restrictions. PUBLIC covers both fully public and data shared within groups.

2. **Deep dive into each tier** (~25 min):

   **PUBLIC (8-10 min)**
   - Definition: Either fully published/public OR freely shared within Pomona/lab groups
   - Examples: Published papers, open-source code, course materials, draft manuscripts shared with lab, lab meeting notes, internal protocols
   - Storage: Anywhere (laptop, GitHub, cloud) if fully public; Sagehen HPC for shared group data
   - Encryption: Not required
   - Access: Unrestricted (fully public) or group-level access (750) if shared within group
   - Sharing: Freely for fully public; with group members if internal to group
   - Live demo: Show a published paper vs. a lab folder with `chmod 750` group access
   - Ask: "Is draft data shared with your lab members public or proprietary?" → Answer: PUBLIC (shared within group)
   - Distinguish: "Does everyone in the world need access (public), or just your team (shared within group)?" → Both are PUBLIC

   **PROPRIETARY (8-10 min)**
   - Definition: Trade secrets, pre-publication research, confidential business data needing restricted access
   - Examples: Grant proposals (pre-award), unpublished novel findings, algorithms before publication, personnel data
   - Storage: Sagehen only
   - Encryption: Recommended (gocryptfs)
   - Access: Specific authorized individuals only (not all lab members)
   - Sharing: Only with legal agreement (NDA, collaboration agreement)
   - Live demo: Show encrypted folder with `chmod 700` or `chmod 750` for restricted group; explain password protection on top
   - Scenario: "Your lab is about to publish a novel algorithm, but it's not public yet. Need PROPRIETARY protection." → Show how
   - Ask: "Why NDA before sharing proprietary research?" → Answer: Legally protects IP

   **RESTRICTED (6-8 min)**
   - Definition: Legally protected personal or sensitive information requiring encryption and audit
   - Examples: Student grades (FERPA), health records (HIPAA), genetic data linked to individuals, export-controlled research
   - Storage: Sagehen only, encrypted (REQUIRED)
   - Encryption: MANDATORY (gocryptfs with AES-256-GCM)
   - Access: Only named researchers with authorization; audit logging required
   - Sharing: Only with legal data use agreement; follow regulations
   - Live demo: Show encrypted container mounted/unmounted; explain legal framework
   - Scenario: "Your study has IRB approval and informed consent. Data is RESTRICTED." → Show encryption setup
   - Ask: "What happens if you share RESTRICTED data without authorization?" → Answer: FERPA/HIPAA violation, federal liability

3. **Boundary cases and decision-making** (~5 min):
   Work through tricky examples:
   - "I have code with proprietary algorithm but no personal data. PUBLIC or PROPRIETARY?" → PROPRIETARY (trade secret, restricted access)
   - "Lab data shared with all 5 team members. PUBLIC or PROPRIETARY?" → PUBLIC (freely shared within group with 750 permissions)
   - "Anonymized genetic data (IDs removed). PUBLIC or RESTRICTED?" → Likely RESTRICTED (re-identification risk)
   - "My PI said everyone in the lab can access this data. PUBLIC or PROPRIETARY?" → PUBLIC (group decision to share; use 750)

4. **Exercises** (~15 min):
   Provide 4-5 datasets and have learners classify them. Discuss:
   - "What clues told you it was PUBLIC/PROPRIETARY/RESTRICTED?"
   - "What would change your classification?"

**Common Issues & Solutions:**

| Issue | Solution |
|-------|----------|
| "I'm not sure what 'proprietary' means" | Example: "Your algorithm is novel and gives competitive advantage. That's proprietary." |
| Learners want to classify too conservatively | Validate caution, but explain: Over-classifying slows collaboration |
| "What if I'm not sure?" | Answer: "Ask your PI or contact its-hpc@pomona.edu. Better safe than sorry." |
| Confusion between PROPRIETARY and RESTRICTED | Simple rule: PROPRIETARY = confidential business/research; RESTRICTED = legal protection required |

**Timing Tips:**
- Make this engaging with lots of examples and scenarios
- Learners should be able to classify simple datasets by the end
- Don't get bogged down in edge cases; note them for follow-up

---

### Episode 3: Classifying Your Own Data (30 min teaching + 30 min hands-on)

**Key Concepts:**
- Applying classification framework to real research data
- Identifying sensitive elements (PII, proprietary methods, etc.)
- Decision-making with uncertainty
- Creating a lab classification policy

**Teaching Approach:**

1. **Guided practice with examples** (~10 min):
   Use pre-provided example datasets (ideally real, anonymized examples from your institution):

   **Example 1: Biology lab survey response**
   ```
   student_id,age,gender,major,survey_q1,survey_q2
   A001,19,F,Biology,4,3
   A002,20,M,Chemistry,5,4
   ```
   Ask: "Is this PUBLIC, PUBLIC (internal to group), PROPRIETARY, or RESTRICTED?"
   - Contains student IDs → Traceable to individuals → FERPA concern
   - Likely RESTRICTED (if linked to names/ID system) or PUBLIC (internal to group) (if anonymized)
   - Discussion: Does the institution own this? Are students aware? Is there consent?

   **Example 2: Computational code**
   ```python
   # Novel clustering algorithm developed in house
   def proprietary_cluster(data, k):
       # Implementation details ...
   ```
   Ask: "Classification?"
   - Novel method, not yet published → PROPRIETARY (trade secret)
   - After publication: PUBLIC
   - If algorithm is standard/known: PUBLIC (internal to group)

   **Example 3: Published dataset**
   ```
   dataset_name: "Results from XYZ study"
   source: "Published in Nature 2023"
   url: "https://doi.org/10.1038/xyz"
   ```
   Ask: "Classification?"
   - Already published → PUBLIC
   - Can be freely shared and reused

   **Example 4: Health data from study**
   ```
   participant_id,age,blood_pressure,medication
   P001,45,120/80,Lisinopril
   ```
   Ask: "Classification?"
   - Health information → HIPAA concern → RESTRICTED
   - Must be encrypted even with anonymized IDs (re-identification risk)

2. **Interactive classification exercise** (~10 min):
   Divide learners into small groups (3-4 people). Assign each group a dataset from your institution (examples from research you know):
   - Group A: Raw sequencing data from genomics study
   - Group B: Draft grant proposal
   - Group C: Lab protocols and procedures
   - Group D: Student course evaluation data

   Have groups discuss and classify, then present (1 min each). Instructor provides feedback:
   - Correct classifications: Explain why
   - Borderline cases: Discuss tradeoffs
   - Incorrect classifications: Guide to correct tier

3. **Creating a lab policy** (~10 min):
   Ask: "If you were a lab manager, how would you tell your team to classify data?"
   - Work through a decision tree as a group
   - Agree on lab's default classifications
   - Note: "Default can be conservative; adjust for specific projects"

4. **Hands-on: Classify and organize your own data** (~30 min):
   Have learners reflect on their own research:

   **Part 1: Inventory (10 min)**
   Have them list datasets they work with:
   - Raw data source
   - Processing/analysis results
   - Final figures/manuscripts
   - Anything shared with collaborators

   **Part 2: Classify (15 min)**
   For each dataset, determine:
   - Current tier (PUBLIC, PUBLIC (internal to group), PROPRIETARY, RESTRICTED)
   - Where it's currently stored
   - Who has access
   - Is it properly secured?

   **Part 3: Plan improvements (5 min)**
   For any PROPRIETARY or RESTRICTED data:
   - Where should it be stored? (Answer: Sagehen)
   - How should it be encrypted? (Answer: gocryptfs for PROPRIETARY/RESTRICTED)
   - Who should have access?

   Pair learners and have them discuss findings.

**Common Issues & Solutions:**

| Issue | Solution |
|-------|----------|
| "I don't know if it's PROPRIETARY or RESTRICTED" | Walk through: Is it personal/health data? → RESTRICTED. Trade secret? → PROPRIETARY. |
| Learners underestimate sensitivity | Remind: "If breach would hurt someone or institution, it's at least PROPRIETARY" |
| "My PI stores everything on personal laptop" | Acknowledge common, then explain risks; emphasize: "We're fixing that with this workshop" |
| Data scattered across systems | Normalize: Common problem. This workshop helps organize. |

**Timing Tips:**
- Hands-on work should feel exploratory, not stressful
- Have them discuss with a neighbor, not announce to whole group
- Provide reassurance: "No judgment; we're learning together"
- If time is short, focus on Part 1 & 2; Part 3 can be homework

---

### Episode 4: Handling Requirements and Controls (40 min teaching + 15 min exercises)

**Key Concepts:**
- Storage location requirements per tier
- Unix file permissions and access control
- Encryption with gocryptfs
- Practical implementation on Sagehen
- Compliance and audit

**Teaching Approach:**

1. **Storage requirements summary** (~5 min):
   Create a clear table:

   | Tier | Must Store On | Encryption | Backup | Access |
   |------|---------------|-----------|--------|--------|
   | PUBLIC | Anywhere | Not required | Standard | Unrestricted |
   | PUBLIC (internal to group) | Sagehen (`/rhome/`, `/bigdata/`) | Not required | Standard | Group (chmod 750) |
   | PROPRIETARY | Sagehen `/bigdata/` | Recommended | Standard | Individual (chmod 700, gocryptfs) |
   | RESTRICTED | Sagehen `/bigdata/` | **Required** | Secure | Individual (chmod 700, gocryptfs) |

   Key point: "PUBLIC/PUBLIC (internal to group) can go on laptop. PROPRIETARY/RESTRICTED must stay on Sagehen and locked up."

2. **Unix permissions hands-on** (~15 min):

   Live demo on Sagehen:

   ```bash
   # Create folders for each tier
   mkdir /bigdata/lab/demo_lab/public
   mkdir /bigdata/lab/demo_lab/internal
   mkdir /bigdata/lab/demo_lab/proprietary
   mkdir /bigdata/lab/demo_lab/restricted

   # Set permissions
   chmod 755 /bigdata/lab/demo_lab/public         # Everyone can read
   chmod 750 /bigdata/lab/demo_lab/internal       # Group can read; others cannot
   chmod 700 /bigdata/lab/demo_lab/proprietary    # Only owner can access
   chmod 700 /bigdata/lab/demo_lab/restricted     # Only owner can access

   # Check permissions
   ls -la /bigdata/lab/demo_lab/

   # Create test files
   echo "public data" > /bigdata/lab/demo_lab/public/data.txt
   echo "internal data" > /bigdata/lab/demo_lab/internal/data.txt
   echo "proprietary data" > /bigdata/lab/demo_lab/proprietary/data.txt
   echo "restricted data" > /bigdata/lab/demo_lab/restricted/data.txt

   # Show what others can see
   # (login as different user or check with getfacl)
   ```

   Walk through permissions:
   - `rwx------` (700) = only owner
   - `rwxr-x---` (750) = owner + group
   - `rwxr-xr-x` (755) = everyone
   - Ask: "Why do we restrict PROPRIETARY and RESTRICTED?" → Answer: Only authorized people need access

3. **Encryption with gocryptfs** (~20 min):

   **Part A: Motivation** (~5 min)
   Show the threat:
   > "Imagine a storage admin, a system maintainer, or someone with physical access to the server. They could read unencrypted files if they wanted. Encryption ensures only the password holder can read the data."

   **Part B: Live demo** (~15 min)
   On Sagehen demo account, show step-by-step:

   ```bash
   # Initialize encrypted folder
   mkdir /bigdata/lab/demo_lab/restricted/.encrypted
   gocryptfs -init /bigdata/lab/demo_lab/restricted/.encrypted

   # (Enter password when prompted)

   # Mount the folder
   mkdir /tmp/restricted_mount
   gocryptfs /bigdata/lab/demo_lab/restricted/.encrypted /tmp/restricted_mount

   # (Enter password)

   # Create test data
   echo "sensitive: health records" > /tmp/restricted_mount/study_data.csv

   # Show that data is in mounted folder
   ls /tmp/restricted_mount/
   cat /tmp/restricted_mount/study_data.csv

   # Show that encrypted folder has gibberish
   ls /bigdata/lab/demo_lab/restricted/.encrypted/
   cat /bigdata/lab/demo_lab/restricted/.encrypted/somefile
   # (Show unintelligible output)

   # Unmount
   fusermount -u /tmp/restricted_mount

   # Show that mounted folder is now empty
   ls /tmp/restricted_mount/
   # (Empty!)

   # Verify: Can you still read the encrypted folder without password?
   cat /bigdata/lab/demo_lab/restricted/.encrypted/somefile
   # (Still gibberish!)

   # To access again, re-mount with password
   gocryptfs /bigdata/lab/demo_lab/restricted/.encrypted /tmp/restricted_mount
   cat /tmp/restricted_mount/study_data.csv  # Works again!
   ```

   Pause after each step to let learners ask questions.

4. **Practical implementation guide** (~5 min):
   Provide a clear checklist:

   ```
   For PROPRIETARY data:
   ☐ Store on /bigdata/lab/<labname>/
   ☐ Set permissions: chmod 700
   ☐ Consider encrypting with gocryptfs if very sensitive
   ☐ Document who has access

   For RESTRICTED data:
   ☐ Store on /bigdata/lab/<labname>/
   ☐ Encrypt with gocryptfs (REQUIRED)
   ☐ Set permissions: chmod 700
   ☐ Store password in password manager
   ☐ Unmount after use
   ☐ Test recovery: Verify you can decrypt if needed
   ☐ Document access list and legal agreements
   ```

5. **Exercises** (~15 min):
   Have learners practice:
   - Create a restricted folder on Sagehen
   - Set permissions to 700
   - Initialize gocryptfs encryption
   - Create a test file, unmount, re-mount to verify
   - (Optional: Try gocryptfs on their local machine if they want)

**Common Issues & Solutions:**

| Issue | Solution |
|-------|----------|
| "I don't understand Unix permissions" | Show visual: `rwx` = read, write, execute; first three are owner, next three are group, last three are others |
| gocryptfs installation fails | Troubleshoot: check OS, try package manager, offer alternative (VeraCrypt) |
| Learner forgets password | Emphasize: "This is why you write it down in a password manager, not on a sticky note" |
| "This is too complicated" | Reassure: "You only do this once. Then it's just mount/unmount" |
| Questions about compliance audit | Answer: "Sagehen admins can verify permissions; encryption means they can't read data without password" |

**Timing Tips:**
- gocryptfs demo is important; take time to do it right
- Have a pre-created encrypted folder as backup if live demo fails
- Learners might skip hands-on if nervous; pair them up or demo and let them try later

---

### Episode 5: Storage and Encryption (40 min teaching + 15 min exercises)

**Key Concepts:**
- Where to store data on Sagehen
- Backup and retention policies
- Disaster recovery considerations
- Encryption's role in access control vs. backup protection

**Teaching Approach:**

1. **Sagehen storage options** (~10 min):
   Review storage tiers (from Workshop 12):
   - `/rhome/<myusername>` (100 GB, persistent, weekly snapshots)
   - `/bigdata/lab/<labname>` (1 TB, persistent, weekly snapshots)
   - `/scratch/$SLURM_JOB_ID` (temporary, SSD-backed)
   - `/tmpfs/$SLURM_JOB_ID` (temporary, RAM-backed)

   Key point: "For classified data (PROPRIETARY/RESTRICTED), you must use persistent storage (`/rhome/` or `/bigdata/`), and you must encrypt it."

2. **Backup and recovery** (~10 min):
   Explain Sagehen's backup policy:
   - Weekly snapshots of `/rhome/` and `/bigdata/`
   - Snapshots accessible via `.snapshot/` hidden directory
   - Not a substitute for offsite backups
   - Unencrypted snapshots are backup of unencrypted data

   Discuss implications:
   - If you have encrypted data, snapshots protect the encrypted files (not readable without password)
   - If you have unencrypted data, snapshots could expose it if breached
   - For RESTRICTED data, encryption protects even if backup is compromised

   Live demo on Sagehen:
   ```bash
   ls -la /rhome/<myusername>/.snapshot/
   # Shows recent snapshots
   ls -la /rhome/<myusername>/.snapshot/daily.0/
   # Shows your files from X days ago
   ```

3. **Disaster recovery for encrypted data** (~10 min):
   Address learner concern: "What if my encryption password is lost?"

   Scenario: "You encrypted your RESTRICTED data with gocryptfs. Two years later, you need the data but forgot the password."

   Solutions:
   - **Before encryption:** Write down password in secure password manager (Dashlane, 1Password, etc.)
   - **Backup encryption key:** gocryptfs stores key in .encrypted folder; back this up securely
   - **Recovery service:** Contact HPC support (its-hpc@pomona.edu) if you lose access
     - Explain: Admin can verify identity but cannot decrypt without password
     - Data is not recoverable without password (this is good security!)

4. **Retention and deletion** (~5 min):
   Discuss legal/ethical requirements:
   - FERPA: Student data retention (typically 1 year after graduation)
   - HIPAA: Health data retention (varies by legal hold, 6+ years)
   - IRB: Research data retention (per protocol, often 3-7 years)
   - Grants: Funder requirements (often 3-7 years)

   Practical guidance:
   - Keep research data per IRB protocol
   - Archive (compressed, encrypted) when no longer actively used
   - Securely delete when retention period ends
   - Document deletion for audit trail

   Demo:
   ```bash
   # Archive old project
   tar -czf old_project_archive_2021.tar.gz /bigdata/lab/<labname>/old_project/

   # Encrypt archive (if RESTRICTED)
   # [gocryptfs steps]

   # Delete original
   rm -rf /bigdata/lab/<labname>/old_project/

   # Keep archive for retention period, then securely delete
   ```

5. **Exercises** (~15 min):
   Have learners:
   - Check their current storage usage: `quota -s`, `du -sh /rhome/`, `du -sh /bigdata/`
   - Identify old projects they could archive
   - Plan a retention schedule for their data
   - Review backup snapshots: `ls -la .snapshot/`

**Common Issues & Solutions:**

| Issue | Solution |
|-------|----------|
| "What if Sagehen catches fire?" | Explain: Snapshots are local, not offsite. For critical data, archive to offsite (cloud, tape) |
| "Can admin access my encrypted data?" | Answer: No (without password). Encryption ensures privacy even from admins. |
| "I lost my encryption password" | Sympathize, then: Password manager is essential. For future data, keep backup of encryption key. |
| Confusion about backup vs. encryption | Clarify: Backup protects against data loss (hardware failure). Encryption protects against unauthorized access. |

**Timing Tips:**
- Storage and encryption can be technical; use concrete examples
- Hands-on verification of snapshots and storage usage is helpful
- If running short, focus on key concepts; backup details can be in reference

---

### Episode 6: Sharing and Collaboration (50 min teaching + 15 min exercises)

**Key Concepts:**
- Safe sharing of each tier
- Legal agreements for external sharing
- Collaboration across institutions
- Tracking data access and compliance

**Teaching Approach:**

1. **Sharing matrix by tier** (~15 min):
   Create a clear guide:

   | Tier | Internal Team | External Collab | Public Web | Legal Required |
   |------|---------------|-----------------|-----------|----------------|
   | PUBLIC | Yes | Yes | Yes | No |
   | PUBLIC (internal to group) | Yes (with permission) | Limited | No | No (courtesy) |
   | PROPRIETARY | No | Only w/ NDA | No | Yes (NDA) |
   | RESTRICTED | No | Only w/ DUA | No | Yes (DUA) |

   Explain terms:
   - **NDA** (Non-Disclosure Agreement): "Recipient promises not to disclose or use for own benefit"
   - **DUA** (Data Use Agreement): "More comprehensive; covers confidentiality, use restrictions, IRB compliance, publication rights"
   - Example situations:
     - Sharing PROPRIETARY with competitor → NDA required
     - Sharing RESTRICTED with collaborating institution → DUA required

2. **Sharing methods by tier** (~15 min):

   **PUBLIC:**
   - Share freely: email, GitHub, web, conferences
   - No restrictions
   - Encourage wide dissemination

   **PUBLIC (internal to group):**
   - Share with team members via Sagehen or email
   - Ask permission from team lead before external sharing
   - If sharing externally, remove sensitive context
   - Example: "Okay to share lab SOP with another lab? Ask your PI first"

   **PROPRIETARY:**
   - Don't share electronically; meet in person if possible
   - If must share: Use encrypted email, secure file transfer
   - Require NDA before sharing
   - Example process:
     1. Draft email: "I have a pre-publication manuscript. May I share for feedback?"
     2. Get PI approval
     3. Send NDA to recipient
     4. Once signed, share via encrypted email or secure link

   **RESTRICTED:**
   - Never share by email, cloud, or unsecure methods
   - Only with signed DUA and formal collaboration agreement
   - Maintain audit trail of who accessed what, when
   - Example process:
     1. IRB reviews collaboration and data sharing plan
     2. Formal DUA with legal review
     3. Data transfer only after DUA is signed
     4. Recipient must have IRB approval for the research

   Live demo: Show how to use Sagehen's OnDemand + gocryptfs to share with collaborator:
   ```bash
   # Create shared encrypted folder
   mkdir /bigdata/lab/<labname>/collaborator_project
   gocryptfs -init /bigdata/lab/<labname>/collaborator_project/.encrypted

   # Set permissions (only collaborator can read)
   chmod 700 /bigdata/lab/<labname>/collaborator_project
   # (Or use ACL if system supports; contact HPC)

   # Mount, add files, unmount
   gocryptfs /bigdata/lab/<labname>/collaborator_project/.encrypted /tmp/collab_mount
   # (Copy files, unmount)

   # Share password via separate, secure channel (not email!)
   # Phone call, Signal, Zoom call, etc.
   ```

3. **Avoiding common sharing mistakes** (~10 min):

   Scenario discussion:

   **Mistake 1:** "I emailed a grant proposal (PROPRIETARY) to a collaborator"
   - Problem: Email is unsecured; copy now exists on external server
   - Solution: Use encrypted email service or secure file link + password

   **Mistake 2:** "I uploaded student data (RESTRICTED) to Google Drive"
   - Problem: HIPAA/FERPA violation; Google is not authorized
   - Solution: Never use cloud unless explicit data use agreement; use Sagehen only

   **Mistake 3:** "My collaborator downloaded genetic data (RESTRICTED) and now stores it on her laptop"
   - Problem: Data security failure; risk of loss or breach
   - Solution: Ensure DUA specifies data security (must be encrypted, on secure server)

   **Mistake 4:** "I shared my lab's algorithms with a company, but no NDA"
   - Problem: Trade secret protection lost; company can use freely
   - Solution: Always require NDA before sharing PROPRIETARY data

4. **Creating a collaboration agreement** (~5 min):
   Provide template outline:
   ```
   Data Sharing Agreement Template

   Parties: [Institution A] and [Institution B]
   Effective Date: [Date]
   Data Description: [Brief description of data]
   Classification: [PUBLIC/PUBLIC (internal to group)/PROPRIETARY/RESTRICTED]

   1. Purpose: [Use of data]
   2. Confidentiality: [Recipient promises not to disclose]
   3. Security: [How data will be stored and protected]
   4. Access: [Who can access; on need-to-know basis]
   5. Use Restrictions: [What recipient can/cannot do with data]
   6. Publication: [Who decides on publication; review period]
   7. Duration: [How long agreement lasts]
   8. Termination: [When data must be deleted or returned]
   9. Liability: [What happens if breach occurs]

   [Signatures and dates]
   ```

   Note: "For RESTRICTED data, your legal office and IRB should review the DUA."

5. **Exercises** (~15 min):

   **Part A: Scenario analysis** (10 min)
   Discuss scenarios:
   - "Can I share my draft paper with a colleague at another institution?" → PUBLIC (internal to group), need PI permission
   - "Can I post my algorithm on GitHub?" → Depends: is it pre-publication (PROPRIETARY, not yet) or published (PUBLIC, yes)?
   - "A collaborator wants genetic data. What do I need?" → RESTRICTED; need DUA and IRB approval
   - "My grad student is graduating. Can they take lab data with them?" → Depends on classification and who owns it

   **Part B: Plan a collaboration** (5 min)
   Have learners think of a real collaboration they have or want:
   - What data would be shared?
   - Which tier(s)?
   - What's the appropriate sharing method?
   - What agreements are needed?

**Common Issues & Solutions:**

| Issue | Solution |
|-------|----------|
| "Isn't NDA enough for all external sharing?" | Explain: NDA protects confidentiality; for RESTRICTED (especially health/genetic), need DUA with IRB/legal review |
| "Collaborator insists on cloud (Google Drive, Dropbox)" | Answer: Not allowed for PROPRIETARY/RESTRICTED without signed data use agreement with cloud provider. Use Sagehen instead. |
| "Legal review for DUA takes months" | Acknowledge: It does. Plan ahead. Many institutions have templates to speed it up. |
| Learners unsure if collaboration needs DUA | Simple rule: "If data is PROPRIETARY or RESTRICTED and going outside your institution, get legal team involved" |

**Timing Tips:**
- Scenario discussion is engaging; use real examples from your institution if possible
- Learners will have lots of questions about their specific collaborations; encourage email follow-up
- Provide templates and contact info for institutional legal/IRB

---

## Common Learner Mistakes & How to Address Them

| Mistake | Why It's Wrong | How to Prevent |
|---------|----------------|----------------|
| Storing RESTRICTED data unencrypted | Regulatory violation; data breach risk | Always encrypt RESTRICTED; make it non-negotiable |
| Using laptop for sensitive data | Data loss risk; access control risk | Explain: "PROPRIETARY/RESTRICTED stays on Sagehen" |
| Sharing data without permission | Breach of PI's/collaborator's trust | Establish lab rule: "Always ask before sharing" |
| Emailing sensitive data | Email is unsecured; copy on external servers | Demo risks; provide alternatives (encrypted file share) |
| Using public cloud for restricted data | Violates HIPAA/FERPA without DUA | Explain regulations; emphasize Sagehen advantage |
| Forgetting encryption password | Data permanently inaccessible | Emphasize password manager requirement |
| Mixing tiers in one folder | Complex permissions; risk of misclassification | Recommend: Separate folders per tier |
| No audit trail of who accessed data | Can't verify compliance | For RESTRICTED: Document and log access; contact HPC for help |

## Assessment & Feedback

### Informal Checks (During Workshop)

- Ask: "What tier is [dataset]?" (should be able to classify)
- Ask: "How would you share PROPRIETARY data with a collaborator?" (should mention NDA)
- Ask: "Why must RESTRICTED data be encrypted?" (should mention access control/regulatory)
- Have them show you a folder with correct permissions for their tier

### Post-Workshop Feedback

- Provide survey: "Which tier caused most confusion?"
- Offer optional follow-up: "Help me set up encryption for my data"
- Share example data security incident (anonymized) and ask how they'd handle it

## Resource Materials

### For Instructors

- Pomona College Data Classification Policy (your version)
- FERPA Quick Reference: https://www2.ed.gov/policy/gen/guid/fpco/ferpa/
- HIPAA Overview: https://www.hhs.gov/hipaa/
- CUI Information: https://www.archives.gov/cui/
- gocryptfs Docs: https://nuetzlich.net/gocryptfs/
- VeraCrypt (Windows alternative): https://www.veracrypt.fr/

### For Learners (In Reference Guide)

- Three-tier classification table
- Tier decision flowchart
- gocryptfs quick start
- Shared folder permission examples
- Contacts: HPC support, IRB, Research & Sponsored Programs

## Tips for Engagement

1. **Use real scenarios**: "A study you're running is collecting sensitive health data. How do you set it up?"
2. **Discuss ethical stakes**: "Your research participant's genetic data is breached. What are consequences?"
3. **Normalize questions**: "Everyone struggles with classification at first; that's okay"
4. **Celebrate caution**: "If you ever think 'maybe I should encrypt this,' do it. Better safe."
5. **Provide templates**: Share working examples (folder structure, DUA template, gocryptfs init script)
6. **Connect to regulations**: Reference FERPA/HIPAA by name; learners are motivated by legal compliance

## Instructor Logistics

- **Setup time**: 30 min to test gocryptfs, ensure Sagehen access, prepare example datasets
- **Backup plan**: Have pre-recorded gocryptfs demo if live fails
- **Pair programming**: Pair learners unfamiliar with Linux with experienced ones for hands-on
- **Follow-up email**: Share reference guide, templates, and HPC contact within 24 hours
- **Office hours**: Offer optional follow-up session for learners setting up encryption

---

## Questions to Engage Learners

- "What's the most sensitive data you work with?"
- "Has your data ever been lost or breached?"
- "What makes you think a collaborator should have access to your data?"
- "How would you feel if your research data was leaked?"
- "What's the difference between a data breach and data loss?"
- "If you encrypted your data and forgot the password, how bad would that be?"

These personalize the workshop and help you understand learner contexts.

---

## Regulatory Contacts for Your Institution

Document these for quick reference:

- **IRB (Human Subjects Research):** [Contact]
- **Research & Sponsored Programs (Grants):** [Contact]
- **Legal/General Counsel (Data Protection, DUA review):** [Contact]
- **Compliance Office (FERPA, HIPAA, CUI):** [Contact]
- **HPC Support (Technical questions):** its-hpc@pomona.edu

---

## Follow-Up Recommendations

After workshop, encourage learners to:

1. **Classify their current data** (use worksheet from Episode 3)
2. **Set up encryption** for any PROPRIETARY/RESTRICTED data
3. **Document their lab's data policy** (use template from Episode 3)
4. **Schedule a follow-up** if setting up collaboration agreements
5. **Complete the post-workshop survey** for feedback

Offer optional "office hours" sessions in weeks following workshop for hands-on help with encryption or classification questions.

<!-- highlight <labname>/<myusername> placeholders in code blocks; remove if the varnish theme handles this natively -->
<script>(function(){var CSS='.sh-placeholder{color:#c2410c;font-weight:700}[data-bs-theme="dark"] .sh-placeholder,html.dark .sh-placeholder{color:#fdba74}@media (prefers-color-scheme: dark){[data-bs-theme="auto"] .sh-placeholder{color:#fdba74}}';var RX=/<labname>|<myusername>/g;function firstMatch(el){var w=document.createTreeWalker(el,NodeFilter.SHOW_TEXT,null),nodes=[],full='';while(w.nextNode()){nodes.push({n:w.currentNode,s:full.length});full+=w.currentNode.nodeValue;}RX.lastIndex=0;var m;while((m=RX.exec(full))){var s=m.index,e=s+m[0].length,inSpan=false,parts=[];for(var j=0;j<nodes.length;j++){var ns=nodes[j].s,ne=ns+nodes[j].n.nodeValue.length;if(ne<=s||ns>=e)continue;parts.push({node:nodes[j].n,a:Math.max(s-ns,0),b:Math.min(e-ns,nodes[j].n.nodeValue.length)});var p=nodes[j].n.parentNode;while(p&&p!==el){if(p.classList&&p.classList.contains('sh-placeholder')){inSpan=true;break;}p=p.parentNode;}}if(!inSpan&&parts.length)return parts;}return null;}function wrapParts(parts){for(var i=parts.length-1;i>=0;i--){var t=parts[i].node,txt=t.nodeValue,a=parts[i].a,b=parts[i].b;var span=document.createElement('span');span.className='sh-placeholder';span.textContent=txt.slice(a,b);var f=document.createDocumentFragment();if(a>0)f.appendChild(document.createTextNode(txt.slice(0,a)));f.appendChild(span);if(b<txt.length)f.appendChild(document.createTextNode(txt.slice(b)));t.parentNode.replaceChild(f,t);}}function run(){var st=document.createElement('style');st.textContent=CSS;document.head.appendChild(st);document.querySelectorAll('pre,code').forEach(function(el){var guard=0,parts;while((parts=firstMatch(el))&&guard++<500){wrapParts(parts);}});}if(document.readyState==='loading'){document.addEventListener('DOMContentLoaded',run);}else{run();}})();</script>
