---
title: Setup
---

## Requirements for This Workshop

This workshop is designed for researchers and students using Pomona College's Sagehen HPC cluster. To participate, you need:

### Prerequisites

1. **Active Sagehen HPC account**
   - Account setup via IT Services
   - SSH access to login nodes
   - Verified password (not your Pomona password)

2. **Basic Linux knowledge**
   - Comfortable with command line (ls, cd, cat, etc.)
   - Understanding of file permissions (chmod, chown)
   - Can navigate the file system

3. **Familiarity with your research data**
   - Know what data your lab collects
   - Understand data sources and contents
   - Can describe who uses the data

### Pre-Workshop Checklist

Before starting, verify you have:

- [ ] Sagehen SSH access
  ```bash
  ssh <myusername>@sagehen.hpc.pomona.edu
  ```

- [ ] Access to /rhome and /bigdata
  ```bash
  ls /rhome/$(whoami)/
  ls /bigdata/
  ```

- [ ] Basic command-line comfort
  ```bash
  pwd                    # Print working directory
  ls -la                 # List files with permissions
  cat filename.txt       # View file contents
  ```

### Software Requirements

The following software should be available on Sagehen (pre-installed):

- **gocryptfs**: Encryption tool for Restricted data
  ```bash
  which gocryptfs
  gocryptfs --version
  ```

- **Standard Linux utilities**: tar, zip, ssh, scp, rsync
  ```bash
  which tar zip ssh scp rsync
  ```

If any tools are missing, contact ITS at its-hpc@pomona.edu to request installation.

### What You'll Need During This Workshop

#### Episode 1: Why Classify Data?
- No software or setup required
- Have your research projects in mind

#### Episode 2: Three Tiers
- Text editor or notebook (for taking notes)
- Your research data descriptions

#### Episode 3: Classifying Your Data
- Access to your lab's data directories
- List of people who access the data
- Any IRB approvals or collaboration agreements

#### Episode 4: Handling Requirements
- Sagehen SSH access
- Knowledge of your lab group name
  ```bash
  groups
  ```

#### Episode 5: Storage and Encryption
- Sagehen SSH access
- gocryptfs installed on Sagehen
- ~100 MB free space in /rhome for testing

#### Episode 6: Sharing and Collaboration
- Text editor for creating documentation
- Email access (for collaboration agreements)
- Understanding of your PI's publishing preferences

### Getting Help

If you encounter technical issues:

1. **Sagehen access problems**
   - Contact ITS Help Desk: (909) 621-8061 or servicedesk@pomona.edu

2. **HPC or data classification questions**
   - Email: its-hpc@pomona.edu
   - Response time: Usually within 1-2 business days

3. **During workshop sessions**
   - Reach out to instructor (Andrew Wilson)
   - Speak up about unclear concepts

### Optional: Get Your Tools Ready

Before the workshop, it's helpful to have:

1. **A text editor for documentation**
   - On Sagehen: nano, vi, vim
   - On your local machine: VSCode, Sublime, etc.

2. **Password manager (for future use)**
   - To store gocryptfs passphrases
   - Examples: Bitwarden (free), 1Password, KeePass

3. **Collaboration agreement template (optional)**
   - Ask your PI or Pomona legal office
   - Useful for Episode 6

### Workshop Format

This is a Carpentries Workbench workshop. Each episode contains:

- **Teaching Content**: Key concepts and examples
- **Learning Objectives**: What you'll be able to do
- **Challenges**: Hands-on exercises to test understanding
- **Key Points**: Summary of main ideas

**Estimated time per episode:**
- Episodes 1-2: 45-60 minutes each (theory-heavy)
- Episodes 3-6: 50-80 minutes each (hands-on exercises)
- **Total:** 6 hours (typically 2 sessions of 3 hours)

### After the Workshop

To ensure you've completed the workshop successfully:

1. **Classify your lab's data**: Use Episode 3's worksheets
2. **Set up encryption** (if you have Restricted data): Follow Episode 5
3. **Document access controls**: Create access authorization lists
4. **Take the final quiz**: Verify your understanding

Your PI or ITS may require completion certification before you can access Restricted data on Sagehen.

---

## Troubleshooting Setup

### Can't SSH to Sagehen

**Error:** "Connection refused" or "No such host"

**Solutions:**
1. Verify you're using correct hostname: `sagehen.hpc.pomona.edu`
2. Verify your username is correct (often your Pomona email prefix)
3. Contact ITS to verify your account is active

---

### Can't Find gocryptfs

**Error:** "command not found: gocryptfs"

**Solution:**
1. Request installation from ITS: its-hpc@pomona.edu
2. Mention: "gocryptfs needed for Workshop 14 (Data Classification)"

---

### Quota Issues

**Error:** "Disk quota exceeded" in /rhome

**Solutions:**
1. Clean up old files: `du -sh ~/*` to find large directories
2. Move large files to /bigdata: `mv ~/large_data /bigdata/lab/<labname>/`
3. Request quota increase from ITS

---

### File Permissions Issues

**Error:** "Permission denied" accessing /bigdata files

**Solutions:**
1. Check file ownership: `ls -l /bigdata/lab/<labname>/`
2. Verify you're in the correct group: `groups`
3. Contact your PI to add you to the group: `usermod -aG group_name username`

---

## Getting Started

Ready to begin? Start with [Episode 01: Why Classify Data?](episodes/01-why-classify-data.md)

If you have setup questions before starting, contact its-hpc@pomona.edu with the subject line: **"Workshop 14 Setup Help"**

<!-- highlight <labname>/<myusername> placeholders in code blocks; remove if the varnish theme handles this natively -->
<script>(function(){var CSS='.sh-placeholder{color:#c2410c;font-weight:700}[data-bs-theme="dark"] .sh-placeholder,html.dark .sh-placeholder{color:#fdba74}@media (prefers-color-scheme: dark){[data-bs-theme="auto"] .sh-placeholder{color:#fdba74}}';var RX=/<labname>|<myusername>/g;function firstMatch(el){var w=document.createTreeWalker(el,NodeFilter.SHOW_TEXT,null),nodes=[],full='';while(w.nextNode()){nodes.push({n:w.currentNode,s:full.length});full+=w.currentNode.nodeValue;}RX.lastIndex=0;var m;while((m=RX.exec(full))){var s=m.index,e=s+m[0].length,inSpan=false,parts=[];for(var j=0;j<nodes.length;j++){var ns=nodes[j].s,ne=ns+nodes[j].n.nodeValue.length;if(ne<=s||ns>=e)continue;parts.push({node:nodes[j].n,a:Math.max(s-ns,0),b:Math.min(e-ns,nodes[j].n.nodeValue.length)});var p=nodes[j].n.parentNode;while(p&&p!==el){if(p.classList&&p.classList.contains('sh-placeholder')){inSpan=true;break;}p=p.parentNode;}}if(!inSpan&&parts.length)return parts;}return null;}function wrapParts(parts){for(var i=parts.length-1;i>=0;i--){var t=parts[i].node,txt=t.nodeValue,a=parts[i].a,b=parts[i].b;var span=document.createElement('span');span.className='sh-placeholder';span.textContent=txt.slice(a,b);var f=document.createDocumentFragment();if(a>0)f.appendChild(document.createTextNode(txt.slice(0,a)));f.appendChild(span);if(b<txt.length)f.appendChild(document.createTextNode(txt.slice(b)));t.parentNode.replaceChild(f,t);}}function run(){var st=document.createElement('style');st.textContent=CSS;document.head.appendChild(st);document.querySelectorAll('pre,code').forEach(function(el){var guard=0,parts;while((parts=firstMatch(el))&&guard++<500){wrapParts(parts);}});}if(document.readyState==='loading'){document.addEventListener('DOMContentLoaded',run);}else{run();}})();</script>
