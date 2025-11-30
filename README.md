# 🔐 Linux Authorization Management: File & Directory Permissions

This repository documents my hands-on lab with Linux file permissions and authorization. As a beginner learning system administration and cybersecurity, understanding how to manage file access is crucial for maintaining system security.

## 📖 Project Overview

This lab simulated a real-world scenario where I needed to audit and correct file permissions for a researcher's project directory. The goal was to ensure that only authorized users could access sensitive files and directories.

### **Scenario Context**
- **User:** `researcher2`
- **Group:** `research_team`
- **Directory:** `/home/researcher2/projects`
- **Task:** Review and fix permissions to align with security requirements

### **What I Learned & Practiced**

*   Using `ls -l` to examine file permissions
*   Understanding the Linux permission structure (user/group/other)
*   Using `chmod` to modify file and directory permissions
*   Working with hidden files (files starting with `.`)
*   Managing directory execute permissions for access control

## 🛠️ Lab Tasks & My Solutions

### **Task 1: Audit Current Permissions**

**Goal:** Explore the current permissions of files and directories in the `projects` directory.

**My Solution:**
```bash
# Navigate to the projects directory
cd projects

# List all files with detailed permissions (including hidden files)
ls -la
```

**Findings:**

**Owning Group:** research_team

**Hidden File Found:** .project_x.txt

**Initial Directory Contents:**

```bash
total 20
drwx--x--- 2 researcher2 research_team 4096 Oct 14 18:40 drafts
-rw-rw-rw- 1 researcher2 research_team   46 Oct 14 18:40 project_k.txt
-rw-r----- 1 researcher2 research_team   46 Oct 14 18:40 project_m.txt
-rw-rw-r-- 1 researcher2 research_team   46 Oct 14 18:40 project_r.txt
-rw-rw-r-- 1 researcher2 research_team   46 Oct 14 18:40 project_t.txt
```

### **Task 2: Fix Regular File Permissions**

**Goal part 1:** Identify and fix files that allowed **other users** to write.

**Problem Found:** project_k.txt had permissions rw-rw-rw-, meaning anyone on the system could modify it.

**Solution:**
```bash
chmod o-w project_k.txt
```

**Goal Part 2:** Restrict project_m.txt so only the owner can read/write it.

**Initial State:** The file had rw-r----- permissions, meaning the group could read it.

**Solution:**

```bash
chmod g-r project_m.txt
```
Final permissions: rw------- (only user can read/write)

### **Task 3: Secure Hidden Files**
**Goal:** Fix permissions on the hidden file .project_x.txt

**Problem:** Both the user and group had write permissions on an archived file that should be read-only.

**Solution:**
```bash
chmod u-w,g-w .project_x.txt
```

**Result:** The file became read-only for both user and group while maintaining readability.

### **Task 4: Secure Directory Access**
**Goal:** Restrict access to the drafts directory so only researcher2 can access it.

**Initial State:** The directory had permissions drwx--x---, meaning the group had execute (access) permission.

**Problem Identified:** Yes, the group could access the drafts directory.

**Solution:**
```bash
chmod g-x drafts
```

Final permissions: drw------- (only user can access)

### **🔍 Key Concepts Demonstrated**
## **Linux Permission Structure**
```text-rw-r--r--
│ │  │  │
│ │  │  └─ Other permissions (r--)
│ │  └───── Group permissions (r--)
│ └──────── User permissions (rw-)
└────────── File type (- = regular file)
```

**chmod Syntax**

- u = user (owner)

- g = group

- o = other

- **+** = add permission

- **-** = remove permission

- r = read

- w = write

- x = execute

  ### **✅ Conclusion**
This lab gave me practical experience in:

- Security Auditing: Systematically checking file and directory permissions

- Principle of Least Privilege: Ensuring users only have the access they absolutely need

- Permission Management: Using chmod to precisely control access rights

- Hidden File Management: Understanding that hidden files also need proper security configurations

  These skills are fundamental for anyone pursuing roles in system administration, cybersecurity, or DevOps.
