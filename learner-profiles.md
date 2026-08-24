---
title: Learner Profiles
---

## Overview

The following learner profiles represent typical backgrounds, data contexts, and motivations for the Data Classification and Handling workshop. Use these to tailor examples, scenarios, and the pace of discussion during the workshop.

---

## Profile 1: Researcher with Human Subjects Data

**Name:** Dr. Lisa Huang
**Background:** Developmental psychologist running longitudinal study with child participants
**Technical Level:** Low-Medium (basic computer skills, no encryption experience)
**Motivation for Workshop:** Her study involves interviews and developmental assessments with 150 children. She recently heard about FERPA and is worried about compliance.

### Current Challenges

- Doesn't understand FERPA requirements for student/child data
- Currently stores data in Excel file on shared lab computer (unencrypted, accessible to all staff)
- Had a hard drive fail last year; lost some data and hasn't set up backups
- Collaborating with researchers at another institution but no formal data sharing agreement
- Recently had a student intern who left with access to participant records (forgot to disable account)
- Worried about "what if data is breached?"

### Specific Needs from Workshop

- Clear understanding of FERPA requirements for her data
- How to organize participant data safely on Sagehen
- Whether encryption is necessary for her study
- How to share data with collaborators safely
- What to do about that departed intern's access
- Backup and recovery strategies
- How to set up access controls so only authorized team members see data

### Expected Outcomes

- Understands FERPA applies to her child participant data (RESTRICTED tier)
- Can classify her data correctly (RESTRICTED → encrypted on Sagehen)
- Has a documented data security plan for her lab
- Can explain to her team members why data must be encrypted
- Knows how to revoke access and set up new access controls
- Has a collaboration agreement template for future sharing
- Feels confident that her participants' privacy is protected

### Teaching Adjustments

- Use child development research as running example
- Emphasize FERPA regulations specifically (not just general security)
- Show step-by-step: Create encrypted folder on Sagehen, organize participant data inside
- Discuss IRB responsibility: IRB approved the study; data security is part of the approval
- Include scenario: "A grad student asks to take participant data home on laptop. How do you respond?"
- Provide FERPA checklist and DUA template for future collaborations
- Discuss access control: How to give new team members access, remove departing ones

---

## Profile 2: Computer Science Student with Public Code

**Name:** Marcus Kim
**Background:** Senior CS student, working on AI/ML capstone project
**Technical Level:** High (comfortable with Linux, coding, version control)
**Motivation for Workshop:** His project uses a novel machine learning algorithm. He wants to understand if it's okay to publish on GitHub and when he needs to protect it.

### Current Challenges

- Unsure whether his code is "proprietary" or can be freely shared
- Wants to publish on GitHub but worried about losing credit
- Doesn't understand intellectual property and patents
- All code currently on his laptop; no backup if it crashes
- Collaborating with another student on code; unclear who owns what
- Wants to transition code to Pomona's Sagehen cluster for larger experiments

### Specific Needs from Workshop

- How to classify code and research outputs (PUBLIC vs. PROPRIETARY)
- When to publish vs. when to keep confidential
- How to document ownership and collaborations
- How to set up version control and backups on Sagehen
- Whether to use public GitHub or private repository
- Explanation of licensing (MIT, GPL, proprietary, etc.)

### Expected Outcomes

- Can classify their own code correctly (likely PUBLIC if for capstone)
- Understands IP considerations before publishing
- Has code backed up on Sagehen with version control
- Knows how to collaborate on code with clear ownership
- Understands licensing implications
- Feels confident about sharing code on GitHub (if appropriate)

### Teaching Adjustments

- Fast-track through basic data security (Marcus doesn't need encryption basics)
- Focus on code classification and intellectual property
- Discuss version control (Git) as good data management practice
- Use "algorithm novel enough to patent?" as decision point for PROPRIETARY
- Show how to set up private vs. public GitHub repos for different tiers
- Include licensing discussion (brief overview)
- Pair with more experienced learner for discussion of IP/patents

---

## Profile 3: Faculty with Sensitive Grant Data

**Name:** Dr. Robert Patel
**Background:** Chemistry professor, industry collaborations, pending patents
**Technical Level:** Medium (uses computers, some terminal experience)
**Motivation for Workshop:** Recent grant involves proprietary information from a pharmaceutical company. He needs to know how to manage it securely.

### Current Challenges

- Grant includes data that the company considers trade secrets
- No clear policy for his group on how to organize grant data
- Company wants to see security measures before releasing full dataset
- Team is growing; new postdocs and students need access but must sign NDAs first
- Doesn't understand difference between NDA and data use agreement
- Worried about publication timeline: when can they publish research?

### Specific Needs from Workshop

- How to classify proprietary grant data (PROPRIETARY tier)
- Setting up secure storage with access controls
- When encryption is recommended vs. required
- How to manage access as team grows
- Understanding legal agreements (NDA vs. DUA)
- How to handle publication questions (what's allowed, what's restricted)
- Documentation of data security for grant reports

### Expected Outcomes

- Can classify grant data as PROPRIETARY and set up appropriate security
- Has a documented data security plan to share with the company
- Understands role of NDA (confidentiality) vs. restrictions on use
- Can explain to team members why data security is critical
- Can set up access controls: give access to authorized team members, revoke for departing staff
- Has template for collaboration agreements with industry partners
- Feels confident meeting grant compliance requirements

### Teaching Adjustments

- Use "industry collaboration" as running example
- Emphasize legal/business aspects alongside technical security
- Show practical: Create PROPRIETARY folder, set permissions, document who has access
- Discuss publication restrictions: "Can you present this at conference? In journal?"
- Include scenario: "Postdoc wants to take proprietary data to new job. How do you handle?"
- Provide NDA template and guidance on working with legal department
- Connect to grant compliance: "Funder expects you to protect this data"

---

## Profile 4: Lab Manager Responsible for Data Administration

**Name:** Tom Rodriguez
**Background:** Lab manager for neuroscience research group (8 faculty, 25 grad students, 10 undergrads)
**Technical Level:** High (comfortable with Linux, administration, some scripting)
**Motivation for Workshop:** Lab collects electrophysiology and imaging data with human subjects. Tom is responsible for data organization and ensuring compliance.

### Current Challenges

- Lab has no documented data classification policy
- Data is scattered: some on personal computers, some on lab server, some on external drives
- No consistent backup strategy
- No audit trail of who accessed sensitive participant data
- Lab is collaborating with institutions internationally but no formal agreements
- New students don't understand data security requirements
- Recently had near-miss: grad student almost emailed raw participant data to collaborator

### Specific Needs from Workshop

- How to design a lab-wide data organization system
- Creating and documenting data classification policy
- Setting up encrypted storage for sensitive data
- Managing access and permissions at scale
- Backup and disaster recovery planning
- Creating collaboration agreements
- Compliance documentation (what to keep for audit)
- Training materials for new lab members

### Expected Outcomes

- Has designed and documented a lab data policy
- Can classify common data types (imaging, electrophysiology, behavioral, participant-linked)
- Has set up organized folder structure with appropriate encryption and permissions
- Can manage access: grant access to new members, revoke for departing ones
- Understands backup requirements and has implemented recovery testing
- Can work with legal on data sharing agreements
- Can train new lab members on data security
- Has checklist for what to do when someone joins or leaves lab

### Teaching Adjustments

- Fast-track through basic concepts; focus on large-scale administration
- Use "lab with sensitive neuroscience data" as running example
- Provide template for lab data policy and ask him to adapt
- Discuss access control at scale: ACLs, shared group accounts, audit logging
- Show how to create documentation and audit trails
- Discuss compliance: what records to keep for institutional review
- Include scenario: "Collaborating institution asks for data. What steps do you take?"
- Provide resources: policy template, folder structure example, onboarding checklist
- Suggest follow-up: hands-on help setting up encryption and access controls

---

## Profile 5: Visiting Researcher from Abroad

**Name:** Dr. Elena Moretti
**Background:** Postdoc from Italy; visiting for 1-year collaboration; brings genetic data
**Technical Level:** Medium (familiar with Linux, little US regulatory knowledge)
**Motivation for Workshop:** Her data includes genetic information from European study participants. She needs to understand US requirements (HIPAA, IRB) and how to transfer data across countries.

### Current Challenges

- Genetic data is from EU study under GDPR (different rules than HIPAA)
- Needs to transfer data from Europe to Sagehen; worried about legal issues
- Doesn't understand FERPA/HIPAA/IRB (US-specific systems)
- Data is currently encrypted on her home institution's server; needs similar setup here
- Concerned about data leaving EU (GDPR restrictions)
- Will be leaving Pomona in 1 year; needs plan for data at end of visit
- Collaborating with US lab; unclear who owns the data

### Specific Needs from Workshop

- How GDPR differences affect her data handling in the US
- Understanding HIPAA requirements for her genetic data
- IRB approval requirements for human subjects research in US
- Legal transfer of data from EU to US
- Maintaining encryption across institutions
- Data ownership and publication rights
- Archiving and return of data when visit ends

### Expected Outcomes

- Understands how HIPAA and IRB apply to her research (may be RESTRICTED or PROPRIETARY)
- Has engaged with Pomona's IRB to ensure compliance
- Can transfer data securely (encrypted) following legal requirements
- Has set up encrypted storage on Sagehen matching her home institution's level
- Understands data ownership and publication restrictions in collaboration
- Has plan for transferring data back to Europe or archiving at Pomona when visit ends
- Can navigate US data protection requirements

### Teaching Adjustments

- Acknowledge GDPR/EU experience; explain how US system is different
- Clarify: HIPAA applies to health information (genetic data may fall here)
- Emphasize: IRB is similar to European ethics committees but different details
- Discuss data transfer: encryption in transit, legal agreements for cross-border transfer
- Show: Same encryption tools work; gocryptfs is international
- Include scenario: "Collaborator wants to take your genetic data to analyze. What's the process?"
- Provide contacts: IRB, Research & Sponsored Programs, legal for international questions
- Discuss end-of-visit: "Can you take data home? Do you archive it? How long?"

---

## Profile 6: Undergraduate Lab Assistant New to Research Ethics

**Name:** Priya Patel
**Background:** Junior biology student, first research experience, working in cell biology lab
**Technical Level:** Low (knows computers, new to research and data security)
**Motivation for Workshop:** Her lab is setting up a new study. She's been asked to help organize data and was told to attend this workshop.

### Current Challenges

- Doesn't know what "data classification" even means
- Her PI mentioned data security but she's not sure what she should do
- Worried she'll accidentally mishandle sensitive data
- Doesn't understand difference between public and private data
- Has only basic computer skills (some coding, no Linux)
- Worried about asking "dumb questions" about data security

### Specific Needs from Workshop

- Very basic introduction to data classification (what/why)
- Understanding her role and responsibility as a lab assistant
- How to recognize sensitive data
- Practical: "What do I do with data files?"
- Clear rules for her lab (from PI)
- Understanding encryption without technical jargon
- Knowing when to ask for help

### Expected Outcomes

- Understands the three tiers in simple terms
- Knows what types of data her lab works with and their classification
- Can follow her lab's data handling procedures
- Knows what she should NOT do with sensitive data (email, personal laptop, etc.)
- Can recognize when something seems wrong and ask for help
- Feels confident in her role without feeling overwhelmed

### Teaching Adjustments

- Start very basic: Use analogies ("Data tiers like locks on doors")
- Avoid technical jargon; use plain language
- Pair with more experienced lab member for context
- Use cell biology as example (reagent data is PUBLIC, patient/participant data would be RESTRICTED)
- Provide very simple checklist: "Where does your lab's data go? Who can see it? When do you ask PI?"
- Emphasize: "It's okay to ask questions. Better to ask than guess."
- Share simple, visual decision tree for common situations
- Make it clear: "Your PI is responsible for overall compliance. You're learning."

---

## Profile 7: Computer Science Faculty Teaching Data Ethics

**Name:** Dr. James Wong
**Background:** CS professor, teaches data science and ethics; serving on IRB
**Technical Level:** High (very comfortable with technology and data)
**Motivation for Workshop:** Wants to understand Pomona's specific classification system and encryption tools so he can teach students responsibly and model good practices in his own research.

### Current Challenges

- Teaches classes with big datasets; wants to ensure students handle ethically
- Some of his research involves human subjects data (from IRB studies)
- Wants to understand Pomona's specific tools (gocryptfs on Sagehen)
- Needs to know local contacts and escalation procedures to teach students
- Wants to incorporate data ethics and security into his curriculum
- Recent incident: student accidentally left human subjects data on public GitHub

### Specific Needs from Workshop

- Deep understanding of the three tiers and decision-making
- Technical expertise with gocryptfs and Sagehen setup
- Knowledge of Pomona's IRB process and compliance
- Contacts and escalation procedures
- Teaching materials and frameworks to share with students
- How to catch and prevent data security violations

### Expected Outcomes

- Can classify datasets and explain to students (using three-tier system)
- Can set up encrypted storage on Sagehen as example
- Can teach students to recognize sensitive data
- Can incorporate data classification into curriculum
- Can guide students' research projects toward compliance
- Has contacts for escalating IRB/ethics questions
- Can model good data security practices
- Can create teaching materials for data security

### Teaching Adjustments

- Fast-track through basics; focus on nuances and edge cases
- Provide depth on IRB process and compliance
- Show advanced topics: audit logging, access control at scale
- Discuss pedagogy: "How do you teach students about data ethics?"
- Provide teaching materials: slides, exercises, case studies
- Discuss recent student incident; what would you have done?
- Connect to ethics literature (optional): brief references on responsible data science
- Provide researcher/instructor contacts for ongoing collaboration
- Use three-tier system (PUBLIC, PROPRIETARY, RESTRICTED) throughout

---

## Using These Profiles

### During Workshop Planning

- Anticipate which profiles will attend (ask when registering: "What's your role? What data do you work with?")
- Prepare examples matching the group's interests (FERPA for educators, industry data for chemistry, etc.)
- Plan breakout discussions for different contexts (human subjects research, industry collaboration, teaching)

### During Teaching

- Reference profiles: "If you're like Lisa managing participant data, here's what you do..."
- Adjust pace: Speed up for Tom, slow down for Priya
- Use relevant examples: Genetic data for Elena, code for Marcus, grant data for Robert
- Create peer learning: Pair Priya with Marcus; they support each other

### For Differentiated Exercises

- **Beginner (Priya, Marcus):** Identify which tier, simple classification exercises
- **Intermediate (Lisa, Robert, Elena):** Classify their own data, plan encryption setup, draft sharing agreement
- **Advanced (Tom, James):** Design lab policy, plan access control system, create audit procedures

---

## Demographic Mix and Pacing

If your workshop has a mix of these profiles:

- **Mostly faculty/senior researchers (Robert, Dr. Wong, Lisa):** Spend 20% on basics, 40% on compliance, 40% on implementation
- **Mostly students/postdocs (Marcus, Priya, Elena):** Spend 40% on concepts, 40% on hands-on setup, 20% on advanced topics
- **Mixed group:** Use breakout exercises by experience level; pair experienced with novices
- **Large group with Toms (managers):** Offer optional "advanced" session on lab-scale administration

### When Discussing Data Tiers

Use the three-tier framework (PUBLIC, PROPRIETARY, RESTRICTED) consistently. If learners mention "four tiers," clarify that the current system has been simplified to three tiers, with internally-shared data (formerly "INTERNAL") now classified as PUBLIC when freely shared within groups.

---

## Note on Three-Tier System

These learner profiles were developed with the three-tier classification system (PUBLIC, PROPRIETARY, RESTRICTED) in mind. References to "four tiers" or "Internal" data should be interpreted according to the three-tier mapping:
- **Internal lab data** → **PUBLIC** (data shared openly within lab groups)
- **Internal protocol** → **PUBLIC** (if shared with team)
- **Internal operational data** → **PUBLIC** (if shared with team)
- **Sensitive internal data** → **PROPRIETARY** (if restricted to specific people)

---

## Accommodations & Support Needed

- **For Priya (novice):** Provide very simple, visual decision trees. Pair with experienced learner. Reassure that questions are welcome.
- **For Elena (international perspective):** Acknowledge different regulations (GDPR vs. HIPAA). Provide contacts for legal/IRB questions specific to international data transfer.
- **For Marcus (high technical skills):** Don't belabor basics; offer advanced topics like licensing, IP, version control integration.
- **For Tom (administrator):** Provide templates, checklists, and contact info he can use for lab-wide implementation.
- **For James (instructor):** Provide teaching materials, case studies, and opportunities to discuss pedagogy.

---

## Follow-Up and Support by Profile

### Lisa (Human Subjects Researcher)

- Provide: FERPA checklist, DUA template, access control guide, IRB contact
- Follow-up: "Help me set up encrypted folder for my participant data"
- Suggest: Regular access audits, annual data security review

### Marcus (CS Student with Public Code)

- Provide: Licensing guide, GitHub privacy settings, version control integration
- Follow-up: "Help me publish my code appropriately"
- Suggest: Explore open-source licensing, data ownership documentation

### Robert (Industry Collaboration)

- Provide: NDA template, DUA template, publication timeline worksheet
- Follow-up: "Help me set up access control for my grant team"
- Suggest: Quarterly access reviews, compliance documentation checklist

### Tom (Lab Manager)

- Provide: Lab policy template, folder structure example, onboarding/offboarding checklist
- Follow-up: "Hands-on help implementing lab data policy and encryption"
- Suggest: Monthly lab meetings on data security, regular audit of access

### Elena (International Visitor)

- Provide: GDPR vs. HIPAA comparison, international data transfer guide, legal contacts
- Follow-up: "Help me ensure my data transfer complies with both EU and US rules"
- Suggest: Regular check-ins with IRB, plan for end-of-visit data handling

### Priya (Undergrad Assistant)

- Provide: Simple checklist ("What to do with data"), lab-specific rules from PI, when to ask for help
- Follow-up: One-on-one guidance as she takes on more responsibility
- Suggest: Attend future workshops as she progresses

### James (Faculty Educator)

- Provide: Teaching materials, case studies, advanced topics, ongoing collaboration
- Follow-up: "Co-teach data security in your courses"
- Suggest: Join HPC/data governance committees, mentorship of other faculty

---

## Building Community & Continuity

After the workshop:

- Create **online community** (Slack, discussion forum) for ongoing questions
- Offer **monthly office hours** for hands-on help with encryption, classification, etc.
- Share **case study library** of real (anonymized) data security scenarios
- Create **role-specific resources** (one for faculty, one for students, one for administrators)
- Host **quarterly refresher workshops** for institutions in the region
- Build **referral network**: Tom (lab manager) → Lisa (researcher) so they support each other
