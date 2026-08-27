---
title: "Handling PUBLIC Data"
teaching: 15
exercises: 10
---

::::::::::::::::::::::::::::::::::::: objectives
- Understand the specific handling requirements for PUBLIC data
- Implement access controls appropriate to Public data
- Set up storage for Public data on Sagehen HPC
::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: questions
- What access controls are needed for Public data?
- Where should Public data be stored on Sagehen?
- What permissions should I set for Public files?
::::::::::::::::::::::::::::::::::::::::::::::::

## PUBLIC Data Handling Requirements

### Access Control

```
Who can access: Anyone (unrestricted) or lab group (shared)
Default file permissions: world-readable (755) or group-readable (750)
```

**No special access control is needed.** Public data is by definition available to the world or freely shared within groups.

### Storage

- **Location:** Anywhere on Sagehen (`/rhome` or `/bigdata`)
- **Encryption:** Not required (not recommended; unnecessary overhead)
- **File system:** Standard Sagehen filesystem

### Example: Published Dataset

```bash
# Published paper's supplementary data
/bigdata/lab/<labname>/published_paper_2025/
  ├── README.md (DOI, citation info)
  ├── data_clean.csv
  ├── analysis.R
  └── figures/

# Permissions (world-readable)
ls -l /bigdata/lab/<labname>/published_paper_2025/
-rw-r--r-- 1 pi_user lab_group  500M data_clean.csv
-rw-r--r-- 1 pi_user lab_group   50K analysis.R
```

### Audit Logging

Not required for Public data.

### Retention

No special requirements. Retain as long as useful for reproducibility (typically as long as the paper is cited, indefinitely for reproducibility).

## Storage Layout for Public Data

### Fully Public Data

```bash
/bigdata/lab/<labname>/public_datasets/
├── published_paper_data/
│   ├── data_clean.csv
│   └── analysis.R
└── course_materials/
    ├── lecture_notes.pdf
    └── sample_data.csv

# Permissions (world-readable)
chmod 644 /bigdata/lab/<labname>/public_datasets/*
```

### Public Data Shared within Group

```bash
/bigdata/lab/<labname>/projects/
├── exp_2025_01/
│   ├── raw_data.h5
│   └── analysis/
└── exp_2025_02/
    ├── images/
    └── processed/

# Permissions (group-readable, 750)
chmod 750 /bigdata/lab/<labname>/projects/
find /bigdata/lab/<labname>/projects/ -type f -exec chmod 640 {} \;
```

## Practical Exercise: Set Up Public Data Access

```bash
# Check your lab group
groups

# Set directory permissions for Public shared data
chmod g+rx /bigdata/lab/<labname>/public/
find /bigdata/lab/<labname>/public/ -type f -exec chmod 640 {} \;
find /bigdata/lab/<labname>/public/ -type d -exec chmod 750 {} \;

# Verify
ls -ld /bigdata/lab/<labname>/public/
ls -l /bigdata/lab/<labname>/public/data.csv
```

::::::::::::::::::::::::::::::::::::: challenge
### Challenge 7.1: Public Data Setup

You have two datasets to store:
1. Published paper data (CSV, 5 GB) -- fully public
2. Lab meeting notes (Markdown, 5 MB) -- shared with lab group

For each:
- Choose the storage location (`/rhome` or `/bigdata`)
- Set the correct permissions
- Explain whether encryption is needed

::::::::::::::::::::::::::::::::::::: solution

## Solution

1. Published data → `/bigdata` (large dataset) → permissions 755 → no encryption needed
2. Lab meeting notes → `/bigdata` (shared with group) → permissions 750 → no encryption needed

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints
- Public data: World-readable (755) or group-readable (750); no encryption needed
- Use `/bigdata` for large public datasets; `/rhome` is acceptable for small files
- No audit logging or special retention required for Public data
- Still verify data was approved for public release before sharing
::::::::::::::::::::::::::::::::::::::::::::::::

<!-- highlight <labname>/<myusername> placeholders in code blocks; remove if the varnish theme handles this natively -->
<script>(function(){var CSS='.sh-placeholder{color:#c2410c;font-weight:700}[data-bs-theme="dark"] .sh-placeholder,html.dark .sh-placeholder{color:#fdba74}@media (prefers-color-scheme: dark){[data-bs-theme="auto"] .sh-placeholder{color:#fdba74}}';var RX=/<labname>|<myusername>/g;function firstMatch(el){var w=document.createTreeWalker(el,NodeFilter.SHOW_TEXT,null),nodes=[],full='';while(w.nextNode()){nodes.push({n:w.currentNode,s:full.length});full+=w.currentNode.nodeValue;}RX.lastIndex=0;var m;while((m=RX.exec(full))){var s=m.index,e=s+m[0].length,inSpan=false,parts=[];for(var j=0;j<nodes.length;j++){var ns=nodes[j].s,ne=ns+nodes[j].n.nodeValue.length;if(ne<=s||ns>=e)continue;parts.push({node:nodes[j].n,a:Math.max(s-ns,0),b:Math.min(e-ns,nodes[j].n.nodeValue.length)});var p=nodes[j].n.parentNode;while(p&&p!==el){if(p.classList&&p.classList.contains('sh-placeholder')){inSpan=true;break;}p=p.parentNode;}}if(!inSpan&&parts.length)return parts;}return null;}function wrapParts(parts){for(var i=parts.length-1;i>=0;i--){var t=parts[i].node,txt=t.nodeValue,a=parts[i].a,b=parts[i].b;var span=document.createElement('span');span.className='sh-placeholder';span.textContent=txt.slice(a,b);var f=document.createDocumentFragment();if(a>0)f.appendChild(document.createTextNode(txt.slice(0,a)));f.appendChild(span);if(b<txt.length)f.appendChild(document.createTextNode(txt.slice(b)));t.parentNode.replaceChild(f,t);}}function run(){var st=document.createElement('style');st.textContent=CSS;document.head.appendChild(st);document.querySelectorAll('pre,code').forEach(function(el){var guard=0,parts;while((parts=firstMatch(el))&&guard++<500){wrapParts(parts);}});}if(document.readyState==='loading'){document.addEventListener('DOMContentLoaded',run);}else{run();}})();</script>
