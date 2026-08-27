---
title: Setup
---

## Pre-Workshop Preparation

This workshop teaches you how to classify research data and implement appropriate security measures on the Sagehen HPC cluster. Before attending, please complete the following preparation steps to get the most out of the session.

## Required Reading (30 minutes)

Before the workshop, please read Pomona College's Data Classification and Handling Policy. This short guide establishes the framework we'll use throughout the workshop.

**Download:** Pomona College Data Classification Policy
- Location: This should be provided by your HPC team or accessible via the college intranet
- **Key sections to review:**
  - Three-tier classification system (Public, Proprietary, Restricted)
  - Your role and responsibility in protecting data
  - Consequences of data breaches
  - When and how to escalate security concerns

Note: The current system uses three tiers. If you see references to "Internal" or a four-tier system, these have been consolidated into the three-tier system where Internal shared data is now classified as PUBLIC.

If you haven't received the policy document, contact its-hpc@pomona.edu before the workshop.

## Reflect on Your Own Data (15 minutes)

Think about the data in your current research and answer these questions (write them down; don't worry about accuracy):

1. **What types of data do you work with?**
   - Examples: code, raw measurements, student information, survey responses, health records, proprietary algorithms, published data

2. **Is any of your data sensitive?** Why?
   - Does it contain personal information (names, IDs, emails)?
   - Could it harm someone if leaked?
   - Is it confidential (proprietary, pre-publication)?
   - Does it require regulatory protection (FERPA, HIPAA, etc.)?

3. **How is your data currently stored?**
   - Location: laptop, external drive, lab server, cloud service, Sagehen?
   - Who has access?
   - Is it encrypted?

4. **Have you ever misclassified or mishandled data?** (honestly!)
   - Sent confidential files via unencrypted email?
   - Shared lab data with collaborators without permission?
   - Stored sensitive data on insecure systems?

You'll share some reflections during the workshop (no need to share the sensitive details!). This helps us understand your starting point.

## Review Example Datasets (20 minutes)

Your instructor will provide 3-4 example datasets before the workshop. For each dataset, try to classify it:

**Dataset Example 1: CSV file with student survey responses**
- Contains: Column headers (name, email, age, department, response to Q1, response to Q2, etc.)
- Ask yourself: Should this be Public? Proprietary? Restricted?
- Why?

**Dataset Example 2: Published research code on GitHub**
- Contains: Source code for a published paper, with inline comments, no secrets
- Ask yourself: What tier?
- Why?

**Dataset Example 3: Raw experimental data**
- Contains: Measurements from a lab instrument, timestamps, no identifiers, proprietary method
- Ask yourself: What tier?
- Why?

**Dataset Example 4: Genetic sequence data from human subjects**
- Contains: Participant IDs, DNA sequences, phenotype data, recruited via a study
- Ask yourself: What tier?
- Why?

You don't need to get these right; the goal is to start thinking about classification. We'll discuss answers during the workshop.

## Familiarize Yourself with gocryptfs (Optional but Recommended)

If you have Linux or macOS, try installing and testing gocryptfs, a tool for encrypting files. This is optional but recommended so you're not learning encryption for the first time in the workshop.

### Install gocryptfs

**macOS (via Homebrew):**
```bash
brew install gocryptfs
```

**Linux (Debian/Ubuntu):**
```bash
sudo apt-get install gocryptfs
```

**Windows:**
- Not natively supported, but you can use Windows Subsystem for Linux (WSL)
- Or use VeraCrypt for encryption instead

### Test gocryptfs (Quick Tutorial)

```bash
# Create an encrypted folder
mkdir ~/encrypted_vault_storage ~/encrypted_vault_mount

# Initialize gocryptfs
gocryptfs -init ~/encrypted_vault_storage

# You'll be asked for a password; remember it!

# Mount the encrypted folder
gocryptfs ~/encrypted_vault_storage ~/encrypted_vault_mount

# Create a test file
echo "Secret data" > ~/encrypted_vault_mount/secret.txt

# Verify it's encrypted (look at storage folder):
ls ~/encrypted_vault_storage/
# You'll see cryptic filenames, not "secret.txt"

# Unmount when done
fusermount -u ~/encrypted_vault_mount
# Or on macOS: umount ~/encrypted_vault_mount
```

This gives you hands-on experience with encryption before the workshop.

## Access to Sagehen (Verify)

Confirm that you have access to Sagehen and the necessary directories:

1. **SSH into Sagehen:**
   ```bash
   ssh your.<myusername>@sagehen.hpc.pomona.edu
   ```

2. **Check your home directory:**
   ```bash
   pwd
   ls -la /rhome/<myusername>/
   ```

3. **Verify you can access `/bigdata/` (lab storage):**
   ```bash
   ls -la /bigdata/
   ls -la /bigdata/lab/<labname>/
   ```

4. **Check OnDemand access:**
   - Navigate to https://ondemand.hpc.pomona.edu/
   - Log in with your Pomona AD credentials
   - Explore the "Files" section to browse your home and lab directories

If you encounter any access issues, contact its-hpc@pomona.edu at least 3 days before the workshop.

## Gather Example Datasets (Optional)

If you have real data from your research that you're comfortable discussing, consider bringing a few examples to the workshop. You can use them in case studies and discussions.

**What to bring:**
- A description of the dataset (type, size, source)
- Key metadata (does it contain PII, proprietary info, etc.?)
- Current storage location and access controls

**For privacy:** You don't need to share the actual data, just describe it. If your data is highly sensitive, we can discuss it privately with the instructor after the workshop.

## Understand Your Role

Before the workshop, clarify your role in data management:

- **Researcher/Faculty:** You're responsible for classifying your data and directing team members on proper handling
- **Graduate Student/Postdoc:** You handle data day-to-day; you need to know classification requirements and how to implement them
- **Undergraduate/Lab Assistant:** You work with data under supervision; you need to know your PI's data policy and follow it
- **Lab Manager/Administrator:** You manage lab data systems and policies; you're responsible for compliance and training
- **IT Professional:** You implement technical controls and support users; you need deep understanding of encryption and access control

During the workshop, the instructor will tailor examples to your role.

## System Requirements

To participate fully in hands-on activities, have:

- Computer with Windows, macOS, or Linux
- Stable internet connection
- SSH client (PuTTY, Terminal, or Git Bash; see Workshop 12 setup if needed)
- ~1 GB of free disk space
- Optional: gocryptfs or similar encryption tool installed

## Helpful Resources

- **Pomona College Data Classification Policy:** (provided by HPC team)
- **Sagehen HPC Documentation:** https://sagehen.hpc.pomona.edu/docs/
- **gocryptfs Documentation:** https://nuetzlich.net/gocryptfs/
- **NIST Cybersecurity Framework:** https://www.nist.gov/cyberframework (for technical details)
- **HPC Support:** its-hpc@pomona.edu
- **OnDemand Portal:** https://ondemand.hpc.pomona.edu/

## Troubleshooting Pre-Workshop Issues

**Can't access Sagehen?**
- Verify you're on Pomona network or VPN
- Check credentials with its-hpc@pomona.edu

**Can't install gocryptfs?**
- Installation is optional; we'll demo it in the workshop
- No need to troubleshoot before the workshop

**Didn't receive example datasets?**
- Email its-hpc@pomona.edu to request them
- Or ask your supervisor to share examples from your lab's work

**Questions about the policy?**
- These will be addressed in Episode 1 of the workshop
- Feel free to ask during the workshop Q&A

---

## What to Expect

This workshop covers:

1. **Why data classification matters** (business, legal, ethical drivers)
2. **The three-tier system** (Public, Proprietary, Restricted)
3. **Classifying your own data** (hands-on practice)
4. **Handling requirements per tier** (technical and procedural)
5. **Encryption with gocryptfs** (practical demo)
6. **Sharing and collaboration** (safely)

You'll leave with:
- Clear understanding of where your data fits
- Practical tools and techniques to protect it
- Knowledge of when to ask for help
- Confidence in Sagehen HPC's security measures

**No prior security expertise is required.** Come with curiosity and a willingness to think carefully about data protection.

<!-- highlight <labname>/<myusername> placeholders in code blocks; remove if the varnish theme handles this natively -->
<script>(function(){var CSS='.sh-placeholder{color:#c2410c;font-weight:700}[data-bs-theme="dark"] .sh-placeholder,html.dark .sh-placeholder{color:#fdba74}@media (prefers-color-scheme: dark){[data-bs-theme="auto"] .sh-placeholder{color:#fdba74}}';var RX=/<labname>|<myusername>/g;function firstMatch(el){var w=document.createTreeWalker(el,NodeFilter.SHOW_TEXT,null),nodes=[],full='';while(w.nextNode()){nodes.push({n:w.currentNode,s:full.length});full+=w.currentNode.nodeValue;}RX.lastIndex=0;var m;while((m=RX.exec(full))){var s=m.index,e=s+m[0].length,inSpan=false,parts=[];for(var j=0;j<nodes.length;j++){var ns=nodes[j].s,ne=ns+nodes[j].n.nodeValue.length;if(ne<=s||ns>=e)continue;parts.push({node:nodes[j].n,a:Math.max(s-ns,0),b:Math.min(e-ns,nodes[j].n.nodeValue.length)});var p=nodes[j].n.parentNode;while(p&&p!==el){if(p.classList&&p.classList.contains('sh-placeholder')){inSpan=true;break;}p=p.parentNode;}}if(!inSpan&&parts.length)return parts;}return null;}function wrapParts(parts){for(var i=parts.length-1;i>=0;i--){var t=parts[i].node,txt=t.nodeValue,a=parts[i].a,b=parts[i].b;var span=document.createElement('span');span.className='sh-placeholder';span.textContent=txt.slice(a,b);var f=document.createDocumentFragment();if(a>0)f.appendChild(document.createTextNode(txt.slice(0,a)));f.appendChild(span);if(b<txt.length)f.appendChild(document.createTextNode(txt.slice(b)));t.parentNode.replaceChild(f,t);}}function run(){var st=document.createElement('style');st.textContent=CSS;document.head.appendChild(st);document.querySelectorAll('pre,code').forEach(function(el){var guard=0,parts;while((parts=firstMatch(el))&&guard++<500){wrapParts(parts);}});}if(document.readyState==='loading'){document.addEventListener('DOMContentLoaded',run);}else{run();}})();</script>
