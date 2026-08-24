---
title: "Handling RESTRICTED Data"
teaching: 25
exercises: 15
---

::::::::::::::::::::::::::::::::::::: objectives
- Understand the specific handling requirements for RESTRICTED data
- Implement mandatory encryption and audit logging
- Manage access authorization lists and secure deletion
::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: questions
- What security controls are mandatory for Restricted data?
- How do I set up audit logging for compliance?
- How long must I retain data, and how do I delete it securely?
::::::::::::::::::::::::::::::::::::::::::::::::

## RESTRICTED Data Handling Requirements

::::::::::::::::::::::::::::::::::::: callout

## RESTRICTED Data: Mandatory Controls

### Access Control

**Access:** Specific authorized individuals (strict)
**Audit logging:** REQUIRED
**Default file permissions:** owner only (700) + encrypted container

```bash
# Restricted data (must be in encrypted container)
/rhome/<myusername>/encrypted_restricted/  # gocryptfs mount point

# Cannot be accessed without:
# 1. Correct passphrase to mount the encrypted container
# 2. User must be specifically authorized
```

::::::::::::::::::::::::::::::::::::::::::::::::

### Storage (Mandatory Encryption)

**Restricted data MUST be stored in an encrypted container.** Standard permissions are not sufficient.

```
All Restricted data lives in a gocryptfs encrypted container
├─ Passphrase protects access (AES-256-GCM)
├─ Mounted at user's request
├─ Unmounted when not in use
└─ Requires authorization to mount
```

### Setting Up Restricted Access

**Step 1: Create encrypted container (see Episode 10 for full details)**

```bash
# Initialize encrypted container
gocryptfs-init /bigdata/lab/<labname>/restricted_encrypted_base

# Creates:
# /bigdata/lab/<labname>/restricted_encrypted_base/ (encrypted files)
# /rhome/<myusername>/.config/gocryptfs/... (passphrase storage)
```

**Step 2: Mount when needed**

```bash
# Mount encrypted container
gocryptfs /bigdata/lab/<labname>/restricted_encrypted_base /rhome/<myusername>/restricted

# Encrypted data is now accessible
cd /rhome/<myusername>/restricted/
ls -l
```

**Step 3: Access control within encrypted container**

Even within encrypted container, use file permissions:

```bash
# Within mounted encrypted container
/rhome/<myusername>/restricted/
  ├── student_data/
  │   └── survey_responses_2024/
  │       ├── approved_researcher_1/ (readable by researcher_1 only)
  │       └── approved_researcher_2/ (readable by researcher_2 only)

# Permissions within encrypted container
-rw------- 1 researcher_1 lab_group
-rw------- 1 researcher_2 lab_group
```

## Audit Logging (REQUIRED)

**Every access to Restricted data must be logged.**

**Option A: Manual access log (simplest)**

```bash
# Before accessing restricted data, log it
date >> /rhome/<myusername>/RESTRICTED_ACCESS_LOG.txt
echo "User: $(whoami), File: survey_data.csv, Action: READ" \
  >> /rhome/<myusername>/RESTRICTED_ACCESS_LOG.txt

# Example entry:
# Thu Mar 06 14:23:45 PDT 2025
# User: jane_postdoc, File: student_grades.csv, Action: READ
```

**Option B: Automated logging (recommended)**

```bash
# Set up automatic audit via auditd (with ITS help)
# Logs all reads/writes to encrypted container
auditctl -w /rhome/<myusername>/restricted/ -p rwa -k restricted_access_log

# View logs:
ausearch -k restricted_access_log
```

**Option C: SFTP access logging (for transfers)**

```bash
# If sharing Restricted data via SFTP, logs are automatic
# Review in /var/log/auth.log or server logs
```

## Who Can Access Restricted Data?

Create an explicit access list documenting: the dataset name and classification, each authorized user (name, role, scope of access, who approved), unauthorized categories (e.g., summer interns not approved by IRB), and revocation triggers (user leaves lab, project ends, annual review expires). Store this alongside your classification decision record.

## Handling Transfers of Restricted Data

**Never transfer Restricted data unencrypted.** Use: (A) copy within the encrypted container, (B) SCP/SFTP over SSH, or (C) Pomona-managed Box/OneDrive with encryption. Never use plain FTP, email attachments, unencrypted USB drives, or personal cloud storage.

## Retention and Secure Deletion

### Retention Requirements

| Type | Retention | Reason |
|------|-----------|--------|
| FERPA student records | 3-7 years (per FERPA) | Education records |
| HIPAA health data | 6 years minimum (per HIPAA) | Health information |
| CUI/DOD data | Per contract (typically 5-7 years) | NIST 800-171 requirement |
| Research data | Per funding agency (typically 3-7 years) | NIH, NSF requirements |
| Export-controlled | Until publication or declassification | EAR/ITAR requirement |

**Document retention requirements in your classification record.**

### Secure Deletion

At end of retention period, data must be securely deleted (not just removed):

```bash
# Insecure deletion (Don't do this!)
rm /path/to/restricted/data.csv
# File is removed from directory but recoverable from disk

# Secure deletion (Do this!)
shred -vfz /path/to/restricted/data.csv
# Overwrites file with random data multiple times before deletion
```

::::::::::::::::::::::::::::::::::::: challenge
### Challenge 9.1: Audit Logging Scenario

A researcher is working with FERPA-protected student data. For the next week:
1. Keep a manual access log every time you access the data
2. Record: date, time, user, file name, action (read/write/delete)
3. Review the log at week's end

Example log entry:
```
2025-03-06 14:23:45 jane_postdoc survey_responses.csv READ
2025-03-06 15:10:22 jane_postdoc analysis.R WRITE
2025-03-07 09:15:10 jane_postdoc student_grades.csv READ
```

After one week:
- How many accesses occurred?
- Who accessed what?
- Were there any unusual patterns?

::::::::::::::::::::::::::::::::::::: solution

## Solution

Here is an example completed one-week access log:

```
RESTRICTED DATA ACCESS LOG
===========================
Dataset: student_learning_survey_2025 (FERPA-protected)
Week of: 2025-03-03 to 2025-03-07

DATE                 USER           FILE                          ACTION
2025-03-03 09:12:33  jgarcia        survey_responses.csv          READ
2025-03-03 09:45:10  jgarcia        analysis_cleaning.R           WRITE
2025-03-04 10:05:22  jgarcia        survey_responses_clean.csv    WRITE
2025-03-05 11:30:00  jgarcia        survey_responses_clean.csv    READ
2025-03-06 09:42:33  jgarcia        regression_results.csv        WRITE
2025-03-07 13:15:08  jgarcia        survey_responses.csv          READ
```

**Observations:**
- **Total accesses:** 6 entries across 5 working days
- **Who accessed:** Only `jgarcia` (sole authorized analyst)
- **Pattern:** READ operations at start of day, WRITE operations follow -- normal analytical workflow
- **Recommendation:** For ongoing work, set up automated `auditd` logging

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints
- Restricted data: Owner-only (700) PLUS mandatory encryption (AES-256-GCM via gocryptfs); audit logging required
- Every access to Restricted data must be logged for compliance
- Create explicit access authorization lists; review annually
- Retention and secure deletion are required by regulation; use `shred` not `rm`
- Never transfer Restricted data unencrypted; use SSH/SCP or institutional channels
::::::::::::::::::::::::::::::::::::::::::::::::

<!-- highlight <labname>/<myusername> placeholders in code blocks; remove if the varnish theme handles this natively -->
<script>(function(){var CSS='.sh-placeholder{color:#c2410c;font-weight:700}[data-bs-theme="dark"] .sh-placeholder,html.dark .sh-placeholder{color:#fdba74}@media (prefers-color-scheme: dark){[data-bs-theme="auto"] .sh-placeholder{color:#fdba74}}';var RX=/<labname>|<myusername>/g;function firstMatch(el){var w=document.createTreeWalker(el,NodeFilter.SHOW_TEXT,null),nodes=[],full='';while(w.nextNode()){nodes.push({n:w.currentNode,s:full.length});full+=w.currentNode.nodeValue;}RX.lastIndex=0;var m;while((m=RX.exec(full))){var s=m.index,e=s+m[0].length,inSpan=false,parts=[];for(var j=0;j<nodes.length;j++){var ns=nodes[j].s,ne=ns+nodes[j].n.nodeValue.length;if(ne<=s||ns>=e)continue;parts.push({node:nodes[j].n,a:Math.max(s-ns,0),b:Math.min(e-ns,nodes[j].n.nodeValue.length)});var p=nodes[j].n.parentNode;while(p&&p!==el){if(p.classList&&p.classList.contains('sh-placeholder')){inSpan=true;break;}p=p.parentNode;}}if(!inSpan&&parts.length)return parts;}return null;}function wrapParts(parts){for(var i=parts.length-1;i>=0;i--){var t=parts[i].node,txt=t.nodeValue,a=parts[i].a,b=parts[i].b;var span=document.createElement('span');span.className='sh-placeholder';span.textContent=txt.slice(a,b);var f=document.createDocumentFragment();if(a>0)f.appendChild(document.createTextNode(txt.slice(0,a)));f.appendChild(span);if(b<txt.length)f.appendChild(document.createTextNode(txt.slice(b)));t.parentNode.replaceChild(f,t);}}function run(){var st=document.createElement('style');st.textContent=CSS;document.head.appendChild(st);document.querySelectorAll('pre,code').forEach(function(el){var guard=0,parts;while((parts=firstMatch(el))&&guard++<500){wrapParts(parts);}});}if(document.readyState==='loading'){document.addEventListener('DOMContentLoaded',run);}else{run();}})();</script>
