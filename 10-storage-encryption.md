---
title: "Storage and Encryption"
teaching: 30
exercises: 20
---

::::::::::::::::::::::::::::::::::::: objectives
- Understand Sagehen HPC storage options (`/rhome` vs. `/bigdata`)
- Learn when and how to use gocryptfs for encrypting Restricted data
- Implement encrypted containers for sensitive research data
- Manage encrypted volumes: mounting, unmounting, backup
::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: questions
- Where should each classification tier be stored on Sagehen?
- What is gocryptfs and why do we use it?
- How do I create and mount an encrypted container?
- How do I ensure encrypted data is backed up securely?
::::::::::::::::::::::::::::::::::::::::::::::::

## Sagehen HPC Storage Architecture

### Storage Options

Sagehen provides two main storage spaces for research data:

```
Sagehen HPC Cluster Storage
================================

/rhome                              /bigdata
├─ Home directories                ├─ Shared project storage
├─ ~100 GB per user                ├─ ~1 TB per lab
├─ Fast SSD                        ├─ Large capacity (BeeGFS)
├─ Backed up (6-month retention)   ├─ Not backed up
├─ Per-user quotas                 └─ Shared across group
└─ Good for: Small files, code
   Encrypted containers,           Good for: Raw data, analysis,
   active work                      large files, archives
```

Note: `/rhome` and `/bigdata` share a 1 TB quota on BeeGFS.

### Choosing Storage Location

| Data Tier | /rhome | /bigdata | Decision |
|-----------|--------|----------|----------|
| **Public** | OK (if <100GB) | Preferred | Use `/bigdata` for large datasets |
| **Proprietary** | Preferred (PI-only) | OK with restricted access | Use `/rhome` for sensitive PI data |
| **Restricted** | Preferred (encrypted) | OK (encrypted) | Encrypt in either location |

## Encryption with gocryptfs

Pomona requires **AES-256-GCM** encryption for Restricted data. gocryptfs creates encrypted directories on the filesystem -- like a virtual encrypted hard drive inside your normal file system. It is ideal because it requires no root access, uses per-directory encryption, and performs well for HPC workflows.

### Step 1: Create an Encrypted Container

```bash
cd /rhome/<myusername>/

# Create directory structure
mkdir -p encrypted_base    # Encrypted files (unreadable without passphrase)
mkdir -p restricted        # Mount point (where files appear decrypted)

# Initialize encrypted container
gocryptfs -init encrypted_base/

# When prompted, choose:
# 1: AES-256-GCM (Recommended)
```

When prompted for password:

```
DO:
✓ Use strong password (14+ characters per NIST SP 800-63B)
✓ Store password securely (password manager, not file)
✓ Make it unique (not your Pomona password)

DON'T:
✗ Use weak password (password, 123456, etc.)
✗ Store password in a file
✗ Share password with anyone
```

### Step 3: Mount the Encrypted Container

```bash
gocryptfs /rhome/<myusername>/encrypted_base /rhome/<myusername>/restricted
# Enter your passphrase when prompted

# Work with files as usual
cd /rhome/<myusername>/restricted/
ls -l
cp ~/analysis.csv ./results/
```

### Step 4: Unmount When Done

```bash
fusermount -u /rhome/<myusername>/restricted/

# Verify unmount
ls /rhome/<myusername>/restricted/
# (Directory is empty; files are inaccessible without passphrase)
```

## Backup and Password Management

**Never backup the unencrypted contents!** Always unmount first, then back up the encrypted container:

```bash
fusermount -u /rhome/<myusername>/restricted/
tar czf /bigdata/lab/<labname>/backups/restricted_backup_2025_03.tar.gz \
    /rhome/<myusername>/encrypted_base/
```

**Password storage** (ranked by security): (1) Password manager (Bitwarden, 1Password, KeePass); (2) GPG-encrypted file; (3) Never use plain text files, email, or cloud storage.

**Troubleshooting:** If "password wrong," check for typos and verify the correct container directory. If "already mounted," run `fusermount -u /path/`. If quota is exhausted, move the encrypted container to `/bigdata`.

::::::::::::::::::::::::::::::::::::: challenge
### Challenge 10.1: Set Up Encrypted Container

1. Create an encrypted container for Restricted data
2. Generate test data (create sample restricted files)
3. Unmount and verify files are inaccessible
4. Remount and verify files are recovered
5. Test backup: tar the encrypted_base directory

Document your process and any issues encountered.

:::::::::::::::::::::::::::::::::: solution

## Solution

**Step 1 -- Create directories:**
```bash
$ mkdir -p /rhome/$(whoami)/encrypted_base
$ mkdir -p /rhome/$(whoami)/restricted
```

**Step 2 -- Initialize gocryptfs:**
```bash
$ gocryptfs -init /rhome/jgarcia/encrypted_base/
# Choose strong passphrase (14+ characters)
# The gocryptfs filesystem has been created successfully.
```

**Step 3 -- Mount and create test file:**
```bash
$ gocryptfs /rhome/jgarcia/encrypted_base /rhome/jgarcia/restricted/
$ echo "This is test restricted data" > /rhome/jgarcia/restricted/test_file.txt
```

**Step 4 -- Verify encryption on disk:**
```bash
$ ls /rhome/jgarcia/encrypted_base/
gocryptfs.conf  gocryptfs.diriv  ZxKr8Q2kNvE3pGtYwM7bLd
```

**Step 5 -- Unmount and verify:**
```bash
$ cd ~
$ fusermount -u /rhome/jgarcia/restricted/
$ ls /rhome/jgarcia/restricted/
# (empty -- data is locked)
```

**Step 6 -- Remount and verify recovery:**
```bash
$ gocryptfs /rhome/jgarcia/encrypted_base /rhome/jgarcia/restricted/
$ cat /rhome/jgarcia/restricted/test_file.txt
This is test restricted data
```

**Step 7 -- Test backup:**
```bash
$ fusermount -u /rhome/jgarcia/restricted/
$ tar czf /rhome/jgarcia/encrypted_backup.tar.gz \
    -C /rhome/jgarcia encrypted_base/
$ tar tzf /rhome/jgarcia/encrypted_backup.tar.gz
encrypted_base/
encrypted_base/gocryptfs.conf
encrypted_base/gocryptfs.diriv
encrypted_base/ZxKr8Q2kNvE3pGtYwM7bLd
```

The backup contains only encrypted files -- safe to store on unencrypted media.

::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints
- Use `/rhome` for encrypted Restricted data (smaller, backed up); `/bigdata` for large encrypted data
- /rhome and /bigdata share 1 TB quota on BeeGFS
- gocryptfs provides AES-256-GCM encryption without root access
- Create encrypted container once, mount/unmount as needed
- Always unmount when not actively using Restricted data
- Back up the encrypted container, not the unencrypted contents
- Passphrase must be 14+ characters (NIST SP 800-63B); store securely, never share
::::::::::::::::::::::::::::::::::::::::::::::::

<!-- highlight <labname>/<myusername> placeholders in code blocks; remove if the varnish theme handles this natively -->
<script>(function(){var CSS='.sh-placeholder{color:#c2410c;font-weight:700}[data-bs-theme="dark"] .sh-placeholder,html.dark .sh-placeholder{color:#fdba74}@media (prefers-color-scheme: dark){[data-bs-theme="auto"] .sh-placeholder{color:#fdba74}}';var RX=/<labname>|<myusername>/g;function firstMatch(el){var w=document.createTreeWalker(el,NodeFilter.SHOW_TEXT,null),nodes=[],full='';while(w.nextNode()){nodes.push({n:w.currentNode,s:full.length});full+=w.currentNode.nodeValue;}RX.lastIndex=0;var m;while((m=RX.exec(full))){var s=m.index,e=s+m[0].length,inSpan=false,parts=[];for(var j=0;j<nodes.length;j++){var ns=nodes[j].s,ne=ns+nodes[j].n.nodeValue.length;if(ne<=s||ns>=e)continue;parts.push({node:nodes[j].n,a:Math.max(s-ns,0),b:Math.min(e-ns,nodes[j].n.nodeValue.length)});var p=nodes[j].n.parentNode;while(p&&p!==el){if(p.classList&&p.classList.contains('sh-placeholder')){inSpan=true;break;}p=p.parentNode;}}if(!inSpan&&parts.length)return parts;}return null;}function wrapParts(parts){for(var i=parts.length-1;i>=0;i--){var t=parts[i].node,txt=t.nodeValue,a=parts[i].a,b=parts[i].b;var span=document.createElement('span');span.className='sh-placeholder';span.textContent=txt.slice(a,b);var f=document.createDocumentFragment();if(a>0)f.appendChild(document.createTextNode(txt.slice(0,a)));f.appendChild(span);if(b<txt.length)f.appendChild(document.createTextNode(txt.slice(b)));t.parentNode.replaceChild(f,t);}}function run(){var st=document.createElement('style');st.textContent=CSS;document.head.appendChild(st);document.querySelectorAll('pre,code').forEach(function(el){var guard=0,parts;while((parts=firstMatch(el))&&guard++<500){wrapParts(parts);}});}if(document.readyState==='loading'){document.addEventListener('DOMContentLoaded',run);}else{run();}})();</script>
