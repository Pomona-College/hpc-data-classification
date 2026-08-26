---
title: Learner Profiles
---

## Learner Profiles for Workshop 14

These profiles represent the diverse audience for this workshop. Understanding these learners helps instructors tailor examples and pacing.

---

## Profile 1: Graduate Student (First Semester)

**Name:** Maria Garcia
**Department:** Biology
**Role:** PhD student, first semester
**Experience:** Basic Linux from undergrad; new to research computing

### Current Situation
- Just started in Dr. Smith's lab
- Working with genomics data from an ongoing study involving human participants
- Accessing Sagehen HPC for the first time
- Unsure of what data handling expectations are

### What Maria Brings
- Curiosity about how to do things right
- Willingness to learn institutional policies
- May not yet understand full research project scope

### What Maria Struggles With
- Technical concepts (encryption, file permissions)
- Regulatory landscape (FERPA, export control)
- Imposter syndrome: "I should already know this"

### Maria's Goal
- Understand what data is sensitive before touching it
- Learn how to set up encryption if needed
- Know who to ask when unsure

### How to Teach Maria
- Use concrete examples (student data, published papers)
- Walk through encryption setup slowly
- Reassure that "not knowing" is expected
- Provide checklists for common tasks
- Give her list of contacts for follow-up questions

---

## Profile 2: Senior Faculty (Well-Established Lab)

**Name:** Prof. James Chen
**Department:** Chemistry
**Role:** Principal Investigator (PI), 20+ years
**Experience:** Expert researcher; limited HPC exposure

### Current Situation
- Lab is transitioning research to Sagehen HPC cluster
- Lab traditionally used local workstations; now scaling up
- Responsible for ensuring lab compliance with institutional policy
- Has mixed team: postdocs, grad students, undergraduates

### What James Brings
- Authority and decision-making power
- Deep understanding of research content
- Experience managing lab operations
- May have some legacy data to classify retroactively

### What James Struggles With
- Technical details of encryption and file permissions
- Regulatory compliance requirements
- Balancing security with research productivity

### James's Goal
- Understand classification system so he can make decisions for his lab
- Delegate implementation tasks with confidence
- Ensure lab complies without creating unnecessary friction
- Establish sustainable data handling practices

### How to Teach James
- Emphasize responsibility and liability (PI accountability)
- Provide templates and workflows his team can use
- Focus on decision-making; let tech staff handle implementation
- Offer to review lab's data classification plan after workshop
- Provide written summary he can reference

---

## Profile 3: Postdoctoral Researcher (International)

**Name:** Dr. Kenji Tanaka
**Department:** Physics
**Role:** Postdoc, 2 years after PhD
**Experience:** Extensive research computing; English speaker, not native

### Current Situation
- Working on computational materials science project (potentially export-controlled)
- Visiting from Japan on approved visa
- May eventually return to Japan; considering publishing results
- Shares lab space and resources with others

### What Kenji Brings
- Technical sophistication with HPC tools
- Clear understanding of research project and data flows
- International perspective on compliance complexity
- Responsibility for own work and data stewardship

### What Kenji Struggles With
- US export control regulations (unfamiliar)
- FERPA/HIPAA (not relevant in most countries)
- Potential visa/residency implications of export-controlled work
- Language: May miss nuance of legal/policy language

### Kenji's Goal
- Understand export control implications of his research
- Know when to consult ORSP before sharing
- Ensure his future publication plans won't be blocked
- Classify and protect his data appropriately

### How to Teach Kenji
- Explain export control (EAR/ITAR) in non-legal language
- Discuss implications for international collaboration and publication
- Provide explicit flowchart for "Am I export-controlled?"
- Offer to facilitate ORSP consultation
- Be clear about who can access what (especially for non-US persons)
- Normalize: "Ask ORSP; this is their job"

---

## Profile 4: Undergraduate Summer Researcher

**Name:** Aisha Williams
**Department:** Computer Science (incoming senior)
**Role:** Summer research intern
**Experience:** Limited HPC; good programming skills; new to research

### Current Situation
- Funded 10-week REU internship in Dr. Lopez's lab
- Working on machine learning project with user data
- First time on HPC cluster
- May eventually lead to senior thesis or publication

### What Aisha Brings
- Energy and enthusiasm
- Strong technical skills (Python, Linux)
- Responsibility to PI and institution
- Fresh perspective (might catch issues)

### What Aisha Struggles With
- Research ethics (hasn't taken research methods course)
- Data sensitivity (doesn't know what's sensitive)
- Career implications (worried about "getting it wrong")
- May not realize PII can identify people in practice

### Aisha's Goal
- Do her 10-week project successfully
- Learn how "real" research works
- Not accidentally cause a data breach
- Understand whether her project involves sensitive data

### How to Teach Aisha
- Demystify the process: "Classification isn't hard, just systematic"
- Use her project as example throughout workshop
- Walk through specific scenarios (if you have their approval)
- Reassure: Most issues are caught and corrected
- Provide clear "do" and "don't" lists
- Make her comfortable asking questions
- Give her supervisor's contact info for escalation

---

## Profile 5: Research Manager/Administrator

**Name:** Robert Santos
**Department:** Biology (administrative role)
**Role:** Lab Manager / Research Administrator
**Experience:** Data management experience; some policy background

### Current Situation
- Manages data infrastructure for 8-person lab
- Responsible for shared storage, backups, and access control
- Works closely with PI on compliance
- May manage data for multiple projects

### What Robert Brings
- Systems thinking about data flows
- Practical concern for operational burden
- Likely already manages some access controls
- Invested in both security and usability

### What Robert Struggles With
- Regulatory nuance (FERPA vs. HIPAA vs. export control)
- When to escalate to PI vs. handle independently
- Balancing security with researcher convenience
- Documenting decisions for audit trails

### Robert's Goal
- Implement sustainable data classification system for the lab
- Create processes lab members can follow
- Know when policies apply and when to ask for help
- Maintain documentation for compliance

### How to Teach Robert
- Provide templates and checklists he can customize
- Focus on implementation workflows (not just theory)
- Discuss how to train lab members after workshop
- Offer to review his lab's classification and storage plan
- Connect him with ITS for operational support
- Emphasize documentation as audit trail

---

## Profile 6: Tech-Savvy Researcher (Sensitive Data)

**Name:** Dr. Lisa Zhang
**Department:** Medical Research / Epidemiology
**Role:** Faculty (tenure-track)
**Experience:** Highly technical; works with sensitive health data

### Current Situation
- Running clinical study with patient data and biosamples
- Data includes names, medical conditions, genetic information
- IRB approval for study but new to HPC encryption
- Wants to ensure compliance and protect participants

### What Lisa Brings
- Sophisticated understanding of data sensitivity
- Clear grasp of ethical implications
- Regulatory fluency (works with IRB, medical privacy)
- Motivation to get security right

### What Lisa Struggles With
- Technical encryption implementation
- Understanding how HPC encryption integrates with her current workflows
- How to share data with collaborators while maintaining protection
- Whether her existing protocols are sufficient

### Lisa's Goal
- Ensure her sensitive health data meets AES-256-GCM encryption requirement
- Understand how to maintain participant confidentiality
- Plan data sharing and publishing strategy
- Ensure team members use proper protocols

### How to Teach Lisa
- Deep dive on encryption and audit logging
- Show how gocryptfs integrates with her current workflow
- Discuss de-identification strategies for publication
- Address international collaborator sharing complexity
- Validate that her ethical concerns are appropriate
- Offer technical consultation on her specific data types

---

## Profile 7: Collaborator / Visiting Researcher

**Name:** Dr. Sofia Rodriguez
**Department:** External Institution
**Role:** Collaborating researcher from another university
**Experience:** Experienced researcher; unfamiliar with Pomona systems

### Current Situation
- Visiting Pomona for 3-month collaboration
- Will access shared lab data on Sagehen
- Has her own project data to manage on Pomona systems
- Returns to home institution with processed data

### What Sofia Brings
- Research expertise in area
- Different institutional perspectives on compliance
- Collaborative energy
- May catch process improvements

### What Sofia Struggles With
- Pomona's classification system (different from her institution)
- File permission concepts (if not familiar)
- Export control implications (depends on her citizenship)
- What she can/cannot take back to home institution

### Sofia's Goal
- Understand Pomona's data classification to collaborate effectively
- Know what she can access and what's restricted
- Plan how to share collaborative results
- Ensure she doesn't violate Pomona policy or export control

### How to Teach Sofia
- Explain Pomona system clearly; acknowledge it may differ from her institution
- Clarify what "restricted" means for her specifically (citizenship-dependent)
- Walk through export control implications
- Provide written summary she can refer to
- Clarify data sharing/IP arrangements with her PI
- Connect her with ORSP if export control questions arise

---

## Workshop Accommodations for Diverse Learners

### For Non-Native English Speakers
- Speak clearly; avoid idioms and jargon
- Define regulatory terms (FERPA, EAR/ITAR) early and often
- Provide written handouts with definitions
- Check for understanding (ask "Does this make sense?")
- Allow extra time for questions

### For Non-Technical Researchers
- Explain command-line concepts before demos
- Show live examples, don't just talk through
- Provide copy-paste commands for hands-on work
- Focus on "why" not "how" for technical details
- Offer extended office hours for technical help

### For Experienced Researchers
- Avoid patronizing tone; acknowledge expertise
- Focus on Pomona-specific requirements (not basic security)
- Offer advanced topics or research directions
- Use them as peer mentors during challenges
- Provide resources for independent deep-dive

### For Time-Constrained Participants
- Provide optional follow-up sessions
- Recorded lectures for asynchronous viewing
- Written guides for self-paced learning
- One-on-one consultation by appointment

### For Anxious or Regulatory-Sensitive Researchers
- Normalize asking for help
- Provide clear escalation paths
- Reassure that uncertainty is expected
- Show resources available after workshop
- Make clear that policies help them, not punish them

---

## Common Concerns by Role

### Students (Grad and Undergrad)
- "Will I get in trouble if I didn't do this right before?"
  → Reassure: Retroactive classification is normal
- "What if my project involves data I didn't know was sensitive?"
  → Reassure: Ask PI; reclassify; proceed with corrected approach

### Faculty/PIs
- "How much compliance burden will this add?"
  → Answer: Initial setup is ~1 hour; ongoing is minimal
- "Who is legally liable for compliance?"
  → Answer: PI is responsible; ITS provides tools/guidance
- "Can I trust my team to implement this?"
  → Answer: Yes, with clear documentation and training

### Postdocs/Researchers
- "Will this affect my visa status if I handle restricted data?"
  → Answer: Depends on export control status; consult ORSP
- "Can I share data with my home institution?"
  → Answer: Depends on classification and regulations; need approval

### Lab Managers
- "How do I enforce compliance without being the 'data police'?"
  → Answer: Position as helping team succeed; make it easy
- "What if someone doesn't follow the policy?"
  → Answer: Escalate to PI; offer re-training

---

## Pacing for Different Groups

**If teaching only experienced researchers:**
- Trim Episode 1 (less need for compliance basics)
- Expand Episode 5 (encryption details)
- Focus on export control and international collaboration

**If teaching mostly students:**
- Emphasize Episode 1 (why it matters)
- Slow down Episode 5 (technical setup)
- Use more examples from different domains

**If teaching mixed group:**
- Use advanced participants as peer tutors
- Offer optional "deep dive" sessions for technical topics
- Provide written follow-up for asynchronous learning
- Create single-point escalation path (one contact person)

---

## You Are Teaching for Success

Remember: Your learners want to do research right. They're not trying to cut corners or violate regulations. Your job is to:

1. Make compliance achievable
2. Normalize asking for help
3. Provide clear processes and templates
4. Connect to resources and contacts
5. Celebrate when people get it right

Thank you for empowering Pomona researchers!
