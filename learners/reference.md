---
title: 'Reference'
---

## Pomona College Three-Tier Data Classification System

### Overview Table

| Tier | Encryption | Access Control | Sharing | File Permissions | Examples |
|------|-----------|-----------------|---------|---------|----------|
| **PUBLIC** | Not required | Unrestricted or group-level | Yes, freely (or within group) | 755 or 750 | Published papers, course materials, open-source code, draft research shared with lab |
| **PROPRIETARY** | Recommended | Restricted to authorized | Case-by-case | 750 or 600 | Grant proposals, trade secrets, pre-publication data, personnel records |
| **RESTRICTED** | REQUIRED (AES-256-GCM) | Strict access control + audit logging | Only with legal agreement | 700+gocryptfs | Personal data (FERPA), health data (HIPAA), genetic data, government CUI |

---

## Tier Details and Handling Requirements

### PUBLIC

**Definition:** Data that can be published or shared without restriction.

**Characteristics:**
- Already published or intended for publication
- No personal information
- No proprietary or confidential content
- Benefits from being widely available

**Storage Requirements:**
- Can be stored on any system (Sagehen, cloud, public repositories)
- Encryption: Not required
- Access control: Not required
- Backup: Standard backup policies apply

**Sharing:**
- Can be freely shared with anyone
- Can be posted on public websites, GitHub, etc.
- Can be included in grant proposals as supporting material

**Examples:**
- Published research papers (PDF)
- Supplementary materials (code, data, figures)
- Course lecture slides
- Open-source software
- Publicly available datasets

**Commands & Actions:**
```bash
# Upload to public GitHub
git push origin main

# Share via email attachment (no restrictions)
mail -s "Open data" colleague@institution.edu < dataset.csv

# Upload to open-access repository
# (instructions vary by repository)
```

---

### PROPRIETARY

**Definition:** Data containing trade secrets, intellectual property, or prepublication research requiring restricted access.

**Characteristics:**
- Contains confidential or proprietary information
- Limited distribution even within organization
- Pre-publication research data
- Grant proposals and funding information
- Strategic/business-sensitive content

**Storage Requirements:**
- Store on Sagehen (`/bigdata/`) only, with restricted access
- Encryption: Recommended (use gocryptfs or similar)
- Access control: Restrict to specific authorized individuals
- Backup: Standard backup policies apply
- Deletion policy: Securely delete when no longer needed

**Sharing:**
- Only with explicit permission
- External sharing requires legal agreement (NDA, collaboration agreement)
- Never include in public repositories

**Examples:**
- Grant proposals (pre-submission or pre-award)
- Pre-publication research data
- Proprietary algorithms or methods
- Personnel records (salaries, evaluations)
- Business data or strategic plans
- Trade secrets or competitive information

**Commands & Actions:**
```bash
# Create restricted proprietary folder
mkdir /bigdata/lab/<labname>/proprietary
chmod 700 /bigdata/lab/<labname>/proprietary

# Restrict to specific users (using ACLs if available)
# Contact HPC support for complex permission scenarios

# Encrypt sensitive data with gocryptfs
gocryptfs -init /bigdata/lab/<labname>/proprietary/.encrypted
gocryptfs /bigdata/lab/<labname>/proprietary/.encrypted /tmp/decrypt_proprietary

# Work with decrypted files, unmount when done
fusermount -u /tmp/decrypt_proprietary

# Before sharing, confirm legal agreement is in place
# Contact its-hpc@pomona.edu if uncertain
```

---

### RESTRICTED

**Definition:** Data subject to legal or regulatory protection requiring strict security and access controls.

**Characteristics:**
- Contains personally identifiable information (PII)
- Subject to FERPA (student records), HIPAA (health), CUI (government)
- Genetic or sensitive biometric data
- Financial information (bank accounts, SSN)
- Requires explicit consent for use/sharing
- Can expose individuals to harm if breached

**Storage Requirements:**
- Store on Sagehen (`/bigdata/`) in encrypted form only
- Encryption: REQUIRED (use gocryptfs, VeraCrypt, or approved encryption)
- Access control: Strict; only authorized researchers
- Logging: Consider audit logging for access
- Backup: Use secure backup procedures (encrypted)
- Deletion: Securely delete sensitive PII when no longer needed
- Access review: Periodic audit of who has access

**Sharing:**
- Only with explicit legal agreement
- Must follow applicable regulations (FERPA, HIPAA, etc.)
- Requires written data use agreement
- Cannot be shared publicly under any circumstance
- Anonymization may be possible but requires careful consideration

**Examples:**
- Student names, IDs, grades, academic records (FERPA)
- Health information, medical records (HIPAA)
- Genetic sequences linked to individuals
- Social security numbers, financial data
- Research data involving human subjects (especially vulnerable populations)
- Government controlled unclassified information (CUI)
- Proprietary third-party data

**Commands & Actions:**
```bash
# Create strongly encrypted restricted folder
mkdir /bigdata/lab/<labname>/restricted_data
gocryptfs -init /bigdata/lab/<labname>/restricted_data/.encrypted

# Set very restrictive permissions on encrypted folder
chmod 700 /bigdata/lab/<labname>/restricted_data
chmod 700 /bigdata/lab/<labname>/restricted_data/.encrypted

# Only you (or specific authorized users) can access
# When you need to work with data:
gocryptfs /bigdata/lab/<labname>/restricted_data/.encrypted /tmp/restricted_access

# Do work, then unmount immediately after
fusermount -u /tmp/restricted_access

# Verify encryption is working
# Encrypted files should be unreadable if mounted folder is unmounted
cat /bigdata/lab/<labname>/restricted_data/.encrypted/somefile
# Should show gibberish, not readable data

# To delete sensitive data securely:
# On most systems, simply deleting encrypted files is sufficient
# Contact HPC support for secure deletion of unencrypted data
```

---

## Encryption Tools: gocryptfs Basics

### When to Use gocryptfs

- Encrypting PROPRIETARY data (recommended)
- Encrypting RESTRICTED data (required)
- Not needed for PUBLIC data

### Installation

**macOS:**
```bash
brew install gocryptfs
```

**Linux (Debian/Ubuntu):**
```bash
sudo apt-get install gocryptfs
```

**Linux (RHEL/CentOS):**
```bash
sudo yum install gocryptfs
```

**Windows:**
- Use WSL (Windows Subsystem for Linux) and follow Linux instructions
- Or use VeraCrypt instead

### Quick Start

**Initialize encryption on a folder:**

```bash
# Create encrypted storage folder
mkdir /bigdata/lab/<labname>/secret_storage/.encrypted

# Initialize gocryptfs
gocryptfs -init /bigdata/lab/<labname>/secret_storage/.encrypted

# You'll be asked to set a password (use a strong one!)
# Stores encryption key in the .encrypted folder
```

**Mount (decrypt) the folder:**

```bash
# Create a mount point (temporary access folder)
mkdir /tmp/my_decrypted_files

# Mount the encrypted folder
gocryptfs /bigdata/lab/<labname>/secret_storage/.encrypted /tmp/my_decrypted_files

# You'll be asked for the password
# Now /tmp/my_decrypted_files contains decrypted files
```

**Work with files:**

```bash
# Copy files to encrypted storage
cp sensitive_data.csv /tmp/my_decrypted_files/

# Edit files
nano /tmp/my_decrypted_files/config.txt

# Create new files
echo "secret info" > /tmp/my_decrypted_files/notes.txt
```

**Unmount (encrypt and lock):**

```bash
# When done, unmount to encrypt everything
fusermount -u /tmp/my_decrypted_files

# On macOS:
# umount /tmp/my_decrypted_files

# Files are now encrypted and inaccessible without the password
```

### Best Practices

1. **Use strong passwords:** at least 14 characters (NIST SP 800-63B; 20+ recommended for long-term keys), mix uppercase, lowercase, numbers, symbols
2. **Don't reuse passwords:** Each encrypted folder can have a different password
3. **Store password securely:** Password manager, not a text file
4. **Unmount when done:** Never leave encrypted folder mounted unattended
5. **Test restore:** Verify you can decrypt files before relying on encryption
6. **Back up encryption key:** gocryptfs stores the key in the encrypted folder; backing this up ensures you won't lose data if filesystem corrupts

---

## Handling Requirements Summary

### What You Must Do for Each Tier

#### PUBLIC
- [ ] Can be stored anywhere (laptop, GitHub, cloud, etc.)
- [ ] No encryption required
- [ ] No access restrictions
- [ ] Share freely

#### PROPRIETARY
- [ ] Store on Sagehen only
- [ ] Use encryption (gocryptfs) for sensitive parts
- [ ] Restrict access to authorized individuals
- [ ] Never share externally without legal agreement

#### RESTRICTED
- [ ] Store on Sagehen in encrypted folder (gocryptfs)
- [ ] Strictly limit access (individual authorization)
- [ ] Follow applicable regulations (FERPA, HIPAA, CUI, etc.)
- [ ] Only share with legal data use agreement in place
- [ ] Securely delete when no longer needed

---

## Permission Reference

### Unix Permissions

```bash
# Check permissions
ls -la /bigdata/lab/<labname>/

# Set permissions (examples)
chmod 755 public_folder/        # Everyone can read, only owner can write
chmod 750 internal_folder/      # Group can read, only owner can write
chmod 700 proprietary_folder/   # Only owner can access
chmod 600 file.txt              # Only owner can read/write

# Change group ownership (if needed)
chgrp labgroup /bigdata/lab/<labname>/shared_folder
chmod 750 /bigdata/lab/<labname>/shared_folder
```

### Check Your Permissions

```bash
# See who you are
whoami

# See what groups you belong to
groups

# See folder permissions
ls -ld /rhome/<myusername>
ls -ld /bigdata/lab/<labname>
```

---

## Quick Reference: Which Tier?

### Decision Tree

```
Is the data already published or intended for public use?
  → YES: PUBLIC

Does it contain trade secrets, pre-publication research, or proprietary info?
  → YES: PROPRIETARY

Does it contain personal data (names, SSN, health info, genetic data, etc.)?
  OR is it subject to legal protection (FERPA, HIPAA, CUI)?
  → YES: RESTRICTED
```

### Examples

| Data | Tier | Why |
|------|------|-----|
| Published paper PDF | PUBLIC | Already published |
| GitHub code (open source) | PUBLIC | Intended for public use |
| Lab meeting notes (shared with team) | PUBLIC | Shared openly within lab |
| Draft manuscript (shared with team) | PUBLIC | Freely shared among collaborators |
| Grant proposal (pre-submission) | PROPRIETARY | Confidential until award |
| Pre-publication research data | PROPRIETARY | Confidential research |
| Student names and grades | RESTRICTED | FERPA regulated |
| Genetic sequences + participant IDs | RESTRICTED | Human subject data |
| Health records | RESTRICTED | HIPAA regulated |
| Salary information | PROPRIETARY | Personnel confidential |

---

## Contact Information & Escalation

### Questions about Classification

Email: its-hpc@pomona.edu

Provide:
- Description of your data
- Current storage location
- What you plan to do with it

### Data Breach or Security Incident

Email: its-hpc@pomona.edu (immediate)
Phone: (available through IT helpdesk)

Provide:
- What happened (briefly)
- When you discovered it
- What data was affected
- Any immediate concerns

### Confusion about Legal Requirements (FERPA, HIPAA, etc.)

Contact:
- Your IRB (Institutional Review Board) for research involving human subjects
- Research & Sponsored Programs office for grant-related questions
- Pomona College Legal Counsel for data protection questions

### Help with gocryptfs or Encryption

Email: its-hpc@pomona.edu

Provide:
- Operating system and gocryptfs version
- Error message (if applicable)
- What you're trying to accomplish

---

## Common Mistakes (and How to Avoid Them)

| Mistake | Impact | Prevention |
|---------|--------|-----------|
| Storing RESTRICTED data unencrypted | Data breach liability | Always encrypt RESTRICTED data with gocryptfs |
| Sharing PROPRIETARY data via unencrypted email | Confidentiality loss | Use encrypted file share or request legal agreement first |
| Leaving encrypted folder mounted overnight | Unauthorized access | Unmount immediately after use; use aliases to remind yourself |
| Classifying data too high (overcautiousness) | Inefficiency, blocks collaboration | Carefully read the three tiers; ask if unsure |
| Classifying data too low (underestimation) | Security risk, regulatory violations | Err on side of caution; ask HPC support if uncertain |
| Mixing tiers in one folder | Complex access control | Keep RESTRICTED separate; use different mount points for different tiers |
| Forgetting encryption password | Data inaccessible forever | Store password in secure password manager; test restore before relying |

---

## Regulatory Checklist

### FERPA (Education Records)

- Student names, IDs, grades, transcripts
- **Required handling:** RESTRICTED tier
- **Access:** Only authorized educators and students themselves
- **Sharing:** Only with written consent

### HIPAA (Health Information)

- Patient names, medical records, health data
- **Required handling:** RESTRICTED tier
- **Access:** Only authorized healthcare personnel with need-to-know
- **Sharing:** Only with authorization and business associate agreements

### CUI (Controlled Unclassified Information)

- Government-funded research with restrictions
- **Required handling:** RESTRICTED tier
- **Access:** Only authorized personnel listed in grant
- **Sharing:** Only as specified in grant/contract

### IRB (Human Subjects Research)

- Data from human subjects research
- **Required handling:** Depends on sensitivity (often PROPRIETARY or RESTRICTED)
- **Access:** Only research team listed in IRB approval
- **Retention:** Follow IRB protocol (often 3-7 years)

---

## Additional Resources

- **Pomona College Data Classification Policy:** Available from HPC team
- **FERPA Overview:** https://www2.ed.gov/policy/gen/guid/fpco/ferpa/
- **HIPAA Basics:** https://www.hhs.gov/hipaa/
- **NIST Cybersecurity:** https://www.nist.gov/cyberframework
- **gocryptfs Docs:** https://nuetzlich.net/gocryptfs/
- **HPC Support:** its-hpc@pomona.edu

<!-- highlight <labname>/<myusername> placeholders in code blocks; remove if the varnish theme handles this natively -->
<script>(function(){var CSS='.sh-placeholder{color:#c2410c;font-weight:700}[data-bs-theme="dark"] .sh-placeholder,html.dark .sh-placeholder{color:#fdba74}@media (prefers-color-scheme: dark){[data-bs-theme="auto"] .sh-placeholder{color:#fdba74}}';var RX=/<labname>|<myusername>/g;function firstMatch(el){var w=document.createTreeWalker(el,NodeFilter.SHOW_TEXT,null),nodes=[],full='';while(w.nextNode()){nodes.push({n:w.currentNode,s:full.length});full+=w.currentNode.nodeValue;}RX.lastIndex=0;var m;while((m=RX.exec(full))){var s=m.index,e=s+m[0].length,inSpan=false,parts=[];for(var j=0;j<nodes.length;j++){var ns=nodes[j].s,ne=ns+nodes[j].n.nodeValue.length;if(ne<=s||ns>=e)continue;parts.push({node:nodes[j].n,a:Math.max(s-ns,0),b:Math.min(e-ns,nodes[j].n.nodeValue.length)});var p=nodes[j].n.parentNode;while(p&&p!==el){if(p.classList&&p.classList.contains('sh-placeholder')){inSpan=true;break;}p=p.parentNode;}}if(!inSpan&&parts.length)return parts;}return null;}function wrapParts(parts){for(var i=parts.length-1;i>=0;i--){var t=parts[i].node,txt=t.nodeValue,a=parts[i].a,b=parts[i].b;var span=document.createElement('span');span.className='sh-placeholder';span.textContent=txt.slice(a,b);var f=document.createDocumentFragment();if(a>0)f.appendChild(document.createTextNode(txt.slice(0,a)));f.appendChild(span);if(b<txt.length)f.appendChild(document.createTextNode(txt.slice(b)));t.parentNode.replaceChild(f,t);}}function run(){var st=document.createElement('style');st.textContent=CSS;document.head.appendChild(st);document.querySelectorAll('pre,code').forEach(function(el){var guard=0,parts;while((parts=firstMatch(el))&&guard++<500){wrapParts(parts);}});}if(document.readyState==='loading'){document.addEventListener('DOMContentLoaded',run);}else{run();}})();</script>
