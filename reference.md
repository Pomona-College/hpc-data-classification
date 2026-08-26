---
title: Reference
---

## Quick Reference Guide for Data Classification

### Classification Decision Quick Decision Tree

```
1. Student education records? (FERPA)
   YES → RESTRICTED

2. Health information + ID? (HIPAA)
   YES → RESTRICTED

3. Export-controlled research? (EAR/ITAR)
   YES → RESTRICTED

4. DOD-funded CUI data? (NIST 800-171)
   YES → RESTRICTED

5. Any PII (names, SSN, etc.)?
   YES → PROPRIETARY (minimum; may be Restricted)

6. Unpublished novel findings?
   YES → PROPRIETARY

7. Grant proposals, patents, IP?
   YES → PROPRIETARY

8. Default/Published data?
   YES → PUBLIC
```

### Tier Summary Table

| Aspect | Public | Proprietary | Restricted |
|--------|--------|-------------|-----------|
| **Encryption** | No | Recommended | **Required** |
| **Access** | Unrestricted or group | Specific users | Specific users only |
| **Permissions** | 755 or 750 | 600 | 600 in gocryptfs |
| **Audit logging** | No | Optional | **Required** |
| **Storage** | /bigdata or /rhome | /rhome preferred | /rhome encrypted |
| **External share** | Yes (if public) | With agreement | No (de-identify first) |
| **Retention** | Indefinite | Variable | Per regulation |

### Common Data Classification Examples

| Type | Classification | Reason |
|------|---|---|
| Published paper + data | Public | Intentionally released |
| Course materials | Public | Educational, publicly available |
| Student grades (linked to names) | Restricted | FERPA student record |
| Student test scores (aggregated) | Public | No individual IDs, no sensitive info |
| Lab notebook (draft research) | Public | Shared with team during active research |
| Grant proposal (pre-award) | Proprietary | Competitive advantage |
| Published grant summary | Public | Official announcement |
| Unpublished findings | Proprietary | Novel research asset |
| Export-controlled simulation code | Restricted | EAR/ITAR compliance |
| Personnel data (salary) | Proprietary | Sensitive institutional info |
| Lab operational data | Public | Shared with team |

### Regulatory Checklist

**FERPA (Student Education Records)**
- Applies to: Pomona students' grades, assessments, performance data
- Trigger: Data linked to student identity (even by ID number)
- Compliance: Treat as Restricted; de-identify before sharing
- Contact: ORSP (orsp@pomona.edu) for questions

**HIPAA (Health Information Privacy)**
- Applies to: Patient health data (if covered entity)
- Trigger: Names + health information
- Compliance: Treat as Restricted; encryption required
- Contact: ORSP or Compliance Officer

**EAR/ITAR (Export Control)**
- Applies to: Cryptography, advanced materials, semiconductors, biotech
- Trigger: Novel algorithms, designs, implementations
- Compliance: Treat as Restricted; approval required before international sharing
- Contact: ORSP (orsp@pomona.edu) for export control determination

**NIST SP 800-171 (CUI Protection)**
- Applies to: DOD-funded research with Controlled Unclassified Information
- Trigger: Contract specifies CUI data
- Compliance: Treat as Restricted; specific access controls + audit logging required
- Contact: Its-hpc@pomona.edu for compliance questions

**Pomona Information Security Policy**
- Applies to: All Pomona institutional data
- Trigger: Data stored on Pomona systems
- Compliance: Follow classification and handling requirements
- Contact: its-hpc@pomona.edu for policy questions

### File Permission Quick Reference

**Public data (world-readable):**
```bash
chmod 644 public_file.txt      # Files: -rw-r--r--
chmod 755 public_dir/          # Dirs: drwxr-xr-x
```

**Internal data (group-readable):**
```bash
chmod 640 internal_file.txt    # Files: -rw-r-----
chmod 750 internal_dir/        # Dirs: drwxr-x---
```

**Proprietary data (owner-only):**
```bash
chmod 600 proprietary_file.txt # Files: -rw-------
chmod 700 proprietary_dir/     # Dirs: drwx------
```

**Restricted data (in gocryptfs, owner-only):**
```bash
chmod 600 restricted_file.txt  # Files: -rw-------
chmod 700 restricted_dir/      # Dirs: drwx------
```

### gocryptfs Quick Commands

**Initialize encrypted container:**
```bash
gocryptfs -init /path/to/encrypted_base
```

**Mount:**
```bash
gocryptfs /path/to/encrypted_base /path/to/mount_point
```

**Unmount:**
```bash
fusermount -u /path/to/mount_point
```

**List mounts:**
```bash
mount | grep gocryptfs
```

**Force unmount (if stuck):**
```bash
fusermount -uz /path/to/mount_point
```

### Storage Location Recommendations

**Use `/rhome` for:**
- Encrypted containers (Restricted data)
- Small files (<100 GB total)
- Code and active projects
- PI-sensitive data

**Use `/bigdata` for:**
- Large datasets (>10 GB)
- Shared lab projects
- Public/Internal data
- Backups of encrypted containers (encrypted at source)

### Data Transfer Methods (Ranked by Security)

**1. Most Secure**
```bash
# For Restricted data: encrypted container only
gocryptfs /encrypted /mount
scp -r /mount/data user@remote:/secure/
```

**2. Highly Secure**
```bash
# SFTP over SSH (encrypted in transit)
sftp -P 22 user@remote
put file.tar.gz
```

**3. Secure**
```bash
# Pomona Box with password
rclone copy /rhome/data pomona_box:shared/
```

**4. Acceptable (with restrictions)**
```bash
# Pomona OneDrive (internal use only)
rclone copy /rhome/data onedrive:Research/
```

**5. NOT RECOMMENDED**
```bash
# Unencrypted FTP (visible to network traffic)
ftp user@remote
# Email (unencrypted in transit and at rest)
# Google Drive, Dropbox (unencrypted, personal account)
# USB drive (unencrypted, easily lost)
```

### De-identification Checklist

Before sharing research data:

- [ ] Identified all direct identifiers (names, IDs, email, phone, address)
- [ ] Identified all quasi-identifiers (age, gender, ZIP code, etc.)
- [ ] Removed or obscured direct identifiers
- [ ] Generalized quasi-identifiers if necessary
- [ ] Aggregated data where possible
- [ ] Verified no re-identification is possible
- [ ] Created mapping file (if needed) and encrypted it separately
- [ ] Documented de-identification method
- [ ] Obtained necessary approvals (PI, IRB, etc.)

### Incident Reporting

**If you suspect a data breach:**

1. STOP working with the data
2. Email: **its-hpc@pomona.edu**
3. Include:
   - What you observed
   - When discovered
   - What data is affected
   - Any access evidence

**Do NOT:**
- Attempt to investigate yourself
- Delete evidence
- Share information widely
- Modify files

### Contact Information

| Issue | Contact | Email | Phone |
|-------|---------|-------|-------|
| **Sagehen HPC access** | ITS Help Desk | servicedesk@pomona.edu | (909) 621-8061 |
| **Data classification** | ITS Research Computing | its-hpc@pomona.edu | N/A |
| **Encryption/gocryptfs** | ITS Research Computing | its-hpc@pomona.edu | N/A |
| **Storage quota issues** | ITS Research Computing | its-hpc@pomona.edu | N/A |
| **Export control questions** | ORSP | orsp@pomona.edu | N/A |
| **FERPA/IRB questions** | ORSP | orsp@pomona.edu | N/A |
| **Data breach incident** | ITS Research Computing | its-hpc@pomona.edu | **URGENT** |
| **General ITS questions** | ITS Service Desk | servicedesk@pomona.edu | (909) 621-8061 |

### Useful Commands for Data Classification

**Check file permissions:**
```bash
ls -la /path/to/file
ls -ld /path/to/directory
```

**Check group membership:**
```bash
groups
id
```

**Change permissions:**
```bash
chmod 640 /path/to/file
chown owner:group /path/to/file
```

**Check disk usage:**
```bash
du -sh /rhome/*/
du -sh /bigdata/*/
quota -s
```

**Find large files:**
```bash
find /rhome -size +1G -type f
find /bigdata -size +100M -type f
```

**Create encrypted backup:**
```bash
fusermount -u /mnt/restricted  # Unmount first
tar czf backup_encrypted.tar.gz /rhome/<myusername>/encrypted_base/
```

**View audit logs (if available):**
```bash
ausearch -k restricted_access_log
tail -f /var/log/auth.log
```

### Data Retention Default Periods

| Type | Retention | Reason |
|------|-----------|--------|
| **NIH-funded research** | 3 years post-award | Federal requirement |
| **NSF-funded research** | 3 years post-award | Federal requirement |
| **DOD-funded research** | Per contract (typically 5-7 years) | Federal requirement |
| **Student education records** | 3-7 years after graduation | FERPA guideline |
| **HIPAA health records** | 6 years minimum | HIPAA requirement |
| **Proprietary/grant proposals** | Until decision made | Institutional policy |
| **Lab operational data** | 2-5 years | Lab discretion |
| **Published research data** | Indefinitely | Reproducibility |

---

## Appendix: Multi-Tier Classification Form

Print and use this for classifying your data:

```
DATA CLASSIFICATION WORKSHEET
=============================

Project Name: _________________________
Date: _________________________
Classified by: _________________________

DATASET 1: __________________________

Description: ___________________________________________________

Content Analysis:
  - Data types: ________________________________________________
  - Source: _____________________________________________________
  - Size: _______________________________________________________
  - Contains student data? [ ] Yes [ ] No
  - Contains health info? [ ] Yes [ ] No
  - Export-controlled? [ ] Yes [ ] No [ ] Uncertain
  - PII/personal info? [ ] Yes [ ] No
  - Novel unpublished findings? [ ] Yes [ ] No

Classification Decision:
  [ ] PUBLIC
  [ ] PROPRIETARY
  [ ] RESTRICTED

Reasoning: ____________________________________________________

Access authorization:
  - User 1: ______________________ Role: __________
  - User 2: ______________________ Role: __________
  - User 3: ______________________ Role: __________

Questions to ask PI/ORSP: ________________________________________
```

---

## Additional Resources

**Pomona Documents:**
- Information Security Policy: https://www.pomona.edu/its/
- HPC Usage Policy: https://pomona-college.github.io/usage-policy
- Data Classification Guide: https://www.pomona.edu/its/

**Federal Standards:**
- NIST SP 800-171: https://csrc.nist.gov/publications/detail/sp/800-171/rev-2
- FERPA Overview: https://www2.ed.gov/policy/gen/guid/fpco/ferpa/
- EAR/ITAR: https://www.bis.doc.gov/index.php/regulations/export-administration-regulations-ear

**Tools:**
- gocryptfs: https://nuetzlich.net/gocryptfs/
- rclone: https://rclone.org/

<!-- highlight <labname>/<myusername> placeholders in code blocks; remove if the varnish theme handles this natively -->
<script>(function(){var CSS='.sh-placeholder{color:#c2410c;font-weight:700}[data-bs-theme="dark"] .sh-placeholder,html.dark .sh-placeholder{color:#fdba74}@media (prefers-color-scheme: dark){[data-bs-theme="auto"] .sh-placeholder{color:#fdba74}}';var RX=/<labname>|<myusername>/g;function firstMatch(el){var w=document.createTreeWalker(el,NodeFilter.SHOW_TEXT,null),nodes=[],full='';while(w.nextNode()){nodes.push({n:w.currentNode,s:full.length});full+=w.currentNode.nodeValue;}RX.lastIndex=0;var m;while((m=RX.exec(full))){var s=m.index,e=s+m[0].length,inSpan=false,parts=[];for(var j=0;j<nodes.length;j++){var ns=nodes[j].s,ne=ns+nodes[j].n.nodeValue.length;if(ne<=s||ns>=e)continue;parts.push({node:nodes[j].n,a:Math.max(s-ns,0),b:Math.min(e-ns,nodes[j].n.nodeValue.length)});var p=nodes[j].n.parentNode;while(p&&p!==el){if(p.classList&&p.classList.contains('sh-placeholder')){inSpan=true;break;}p=p.parentNode;}}if(!inSpan&&parts.length)return parts;}return null;}function wrapParts(parts){for(var i=parts.length-1;i>=0;i--){var t=parts[i].node,txt=t.nodeValue,a=parts[i].a,b=parts[i].b;var span=document.createElement('span');span.className='sh-placeholder';span.textContent=txt.slice(a,b);var f=document.createDocumentFragment();if(a>0)f.appendChild(document.createTextNode(txt.slice(0,a)));f.appendChild(span);if(b<txt.length)f.appendChild(document.createTextNode(txt.slice(b)));t.parentNode.replaceChild(f,t);}}function run(){var st=document.createElement('style');st.textContent=CSS;document.head.appendChild(st);document.querySelectorAll('pre,code').forEach(function(el){var guard=0,parts;while((parts=firstMatch(el))&&guard++<500){wrapParts(parts);}});}if(document.readyState==='loading'){document.addEventListener('DOMContentLoaded',run);}else{run();}})();</script>
