---
title: "Handling PROPRIETARY Data"
teaching: 20
exercises: 15
---

::::::::::::::::::::::::::::::::::::: objectives
- Understand the specific handling requirements for PROPRIETARY data
- Implement access controls for Proprietary data on Sagehen HPC
- Manage external sharing of Proprietary data securely
::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: questions
- Who can access Proprietary data, and how do I enforce access?
- What's the difference in handling between Proprietary and Restricted?
- How do I share Proprietary data with external collaborators?
::::::::::::::::::::::::::::::::::::::::::::::::

## PROPRIETARY Data Handling Requirements

### Access Control

**Access:** Specific authorized individuals or designated group members (not all lab members)
**Default file permissions:** owner only (600) or group-restricted (750)

```bash
# Proprietary lab data (grant proposals, unpublished research, restricted datasets)
/bigdata/lab/<labname>/proprietary/
  ├── grant_proposal_2025/
  │   ├── proposal_draft.pdf
  │   └── budget_narrative.doc
  └── unpublished_findings_2024/
      ├── data_analysis.xlsx
      └── manuscript_draft.docx

# Example 1: Permissions for PI-only access
ls -l /bigdata/lab/<labname>/proprietary/
drwx------ 5 pi_user pi_user   500K grant_proposal_2025/
-rw------- 1 pi_user pi_user   500K proposal_draft.pdf

# Example 2: Permissions for restricted group access (e.g., senior lab members only)
drwxr-x--- 5 pi_user senior_group   400K unpublished_findings_2024/
-rw-r----- 1 researcher senior_group  200M data_analysis.xlsx
```

### Setting Up Proprietary Access

**Step 1: Identify authorized users**

Work with your PI to list who needs access:
- PI
- Postdocs directly involved
- Specific grad students (not entire group)
- External collaborators (rare; requires explicit approval)

**Step 2: Set permissions**

```bash
# For PI-owned files (PI is owner)
chmod 600 /bigdata/lab/<labname>/proprietary/grant_proposal_2025/*
ls -l /bigdata/lab/<labname>/proprietary/grant_proposal_2025/
-rw------- 1 pi_user pi_user ...

# For co-owned files (PI and one other person)
# Option A: PI grants explicit access via shared directory
mkdir /bigdata/lab/<labname>/proprietary/grant_proposal_2025/shared_draft/
chmod 700 /bigdata/lab/<labname>/proprietary/grant_proposal_2025/shared_draft/

# Option B: Use encryption (recommended; see Episode 10)
```

### Storage Options

**Option A: Unencrypted + restrictive permissions (for less sensitive proprietary data)**

```
Location: /bigdata with 600 permissions
Encryption: Not required
Advantages: Fast, easy
Disadvantages: Vulnerable to local privilege escalation
```

**Option B: Encrypted (recommended for sensitive proprietary data)**

```
Location: /rhome or /bigdata with gocryptfs
Encryption: AES-256-GCM
Advantages: Resistant to breach even if permission misconfiguration occurs
Disadvantages: Slight performance overhead (see Episode 10)
```

### Audit Logging

**Optional but recommended** for sensitive proprietary data:
- Track who accessed which files
- Useful if breach is suspected
- Can detect unauthorized access attempts

### Handling External Sharing

If you need to share Proprietary data with external collaborators:

1. **Collaboration agreement**: Ensure written agreement exists
2. **Encryption in transit**: Use SSH/SFTP, never plain FTP
3. **Controlled access**: Time-limit access; revoke when done
4. **Audit trail**: Log who accessed what

Example:
```bash
# Create temporary access for collaborator (valid 30 days)
mkdir /bigdata/lab/<labname>/shared_with_external/collaborator_name/
# Add access controls...
# Set calendar reminder to revoke access in 30 days
```

### Retention

Determined by use case:
- Grant proposals: Until award decision + 1 year
- Unpublished research: Until publication (then reclassify to Public)
- Patent disclosures: Until patent filed or decision made not to file
- Personnel records: Per HR policy (typically 5-7 years)

## Practical Exercise: Set Up Proprietary Data Access

```bash
# Create proprietary directory
mkdir -p /bigdata/lab/<labname>/proprietary/grant_proposal_2025

# Set permissions: owner only
chmod 700 /bigdata/lab/<labname>/proprietary/
chmod 600 /bigdata/lab/<labname>/proprietary/grant_proposal_2025/*

# Verify
ls -ld /bigdata/lab/<labname>/proprietary/
ls -l /bigdata/lab/<labname>/proprietary/grant_proposal_2025/
```

::::::::::::::::::::::::::::::::::::: challenge
### Challenge 8.1: Set Up Proprietary Access Controls

**Scenario:** You have a lab with:
- Draft grant proposal (PI-only access)
- Unpublished research findings (PI + 2 grad students)

For each:
1. Identify the appropriate file permissions
2. Describe who can access what
3. Explain how you'd enforce access (what commands)

::::::::::::::::::::::::::::::::::::: solution

## Solution

**Grant proposal (PI-only):**
- Permissions: 600 (owner only)
- Who can access: PI only
- Enforcement: `chmod 600 grant_proposal/*`; only PI owns the files

**Unpublished findings (PI + 2 grad students):**
- Permissions: 750 (group-restricted)
- Who can access: PI + approved grad students via a Unix group
- Enforcement: `chgrp approved_group unpublished_findings/` + `chmod 750`; group retains access control

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints
- Proprietary data: Group-readable (750) or owner-only (600); optional encryption for sensitive assets
- Access control is enforced through file permissions, not trust
- External sharing requires collaboration agreement + secure transfer + time-limited access
- Retention varies by use case; reclassify to Public after publication
::::::::::::::::::::::::::::::::::::::::::::::::

<!-- highlight <labname>/<myusername> placeholders in code blocks; remove if the varnish theme handles this natively -->
<script>(function(){var CSS='.sh-placeholder{color:#c2410c;font-weight:700}[data-bs-theme="dark"] .sh-placeholder,html.dark .sh-placeholder{color:#fdba74}@media (prefers-color-scheme: dark){[data-bs-theme="auto"] .sh-placeholder{color:#fdba74}}';var RX=/<labname>|<myusername>/g;function firstMatch(el){var w=document.createTreeWalker(el,NodeFilter.SHOW_TEXT,null),nodes=[],full='';while(w.nextNode()){nodes.push({n:w.currentNode,s:full.length});full+=w.currentNode.nodeValue;}RX.lastIndex=0;var m;while((m=RX.exec(full))){var s=m.index,e=s+m[0].length,inSpan=false,parts=[];for(var j=0;j<nodes.length;j++){var ns=nodes[j].s,ne=ns+nodes[j].n.nodeValue.length;if(ne<=s||ns>=e)continue;parts.push({node:nodes[j].n,a:Math.max(s-ns,0),b:Math.min(e-ns,nodes[j].n.nodeValue.length)});var p=nodes[j].n.parentNode;while(p&&p!==el){if(p.classList&&p.classList.contains('sh-placeholder')){inSpan=true;break;}p=p.parentNode;}}if(!inSpan&&parts.length)return parts;}return null;}function wrapParts(parts){for(var i=parts.length-1;i>=0;i--){var t=parts[i].node,txt=t.nodeValue,a=parts[i].a,b=parts[i].b;var span=document.createElement('span');span.className='sh-placeholder';span.textContent=txt.slice(a,b);var f=document.createDocumentFragment();if(a>0)f.appendChild(document.createTextNode(txt.slice(0,a)));f.appendChild(span);if(b<txt.length)f.appendChild(document.createTextNode(txt.slice(b)));t.parentNode.replaceChild(f,t);}}function run(){var st=document.createElement('style');st.textContent=CSS;document.head.appendChild(st);document.querySelectorAll('pre,code').forEach(function(el){var guard=0,parts;while((parts=firstMatch(el))&&guard++<500){wrapParts(parts);}});}if(document.readyState==='loading'){document.addEventListener('DOMContentLoaded',run);}else{run();}})();</script>
