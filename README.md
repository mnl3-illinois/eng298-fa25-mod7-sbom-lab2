# Module 7: Assignment: Maintaining Secure Systems with SBOMs and Patching

### **Exercise Overview**
In Module 7, you explored how assurance, verification, and transparency strengthen system design and maintenance. This lab assignment extends those concepts into the realm of secure maintenance, demonstrating how visibility through SBOMs enables continuous verification of the operating environment itself.

Rather than scanning application code, you will analyze the Ubuntu Linux system that powers your GitHub Codespace - enumerating installed packages, identifying vulnerabilities, applying patches, and verifying improvement through renewed SBOM analysis. 

In their Security Engineering principles, <b><a href="https://doi.org/10.1109/PROC.1975.9939" target="_blank">(Saltzer & Schroeder, 1975)</a></b>) emphasized that every access — and by extension, every component — must be continuously verified to maintain trust. By applying this principle to your Codespaces environment, the lab illustrates how assurance extends beyond applications to the underlying platform itself.
Through system-level SBOM generation, vulnerability assessment, and patch verification, you will connect visibility (SBOM) with action (patching) — transforming transparency into sustained assurance for secure operations.

### **Learning Objectives**
After completing this lab, you will be able to:

1. Generate an SBOM of the system packages installed in your Codespace.  
2. Identify vulnerabilities affecting the base Ubuntu environment.  
3. Apply and verify system updates using `apt`.  
4. Explain how patching operational environments supports *complete mediation* and *assurance* in the secure design lifecycle.

### **Environment Setup**
1. All commands can be executed directly inside your GitHub Codespace using this repo.  

2. Confirm you’re running Ubuntu:

```bash
lsb_release -a
```
Typical output:  
`Description: Ubuntu 22.04 LTS (Jammy Jellyfish)`

### **Tasks**

#### **Part 1 – Generate a Baseline System SBOM**
1. Use **Syft** to inventory all APT-managed packages on your system:
    
   ```bash
   syft packages:apt -o spdx-json > system_sbom_before.json
   ```
   
3. Review the file `system_sbom_before.json`.  
   - How many packages are listed?  
   - Note examples of key utilities (e.g., bash, curl, python3).

4. Generate an initial vulnerability report with **Grype**:
   
   ```bash
   grype sbom:system_sbom_before.json -o table > system_vulns_before.txt
   ```
   
6. Record:  
   - Total vulnerabilities found  
   - Counts by severity (Critical, High, Medium, Low)

#### **Part 2 – Identify Outdated Packages**
1.Take a snapshot of the packages currebntly installed on this Ubuntu VM as follows:


2. Update your package database:
   
   ```bash
   sudo apt update
   ```
   
3. View packages with available upgrades:
   
   ```bash
   sudo apt list --upgradable
   ```
   
4. Choose at least **three (3)** upgradable packages to patch.
   Record their current and target versions.

#### **Part 3 – Apply System Updates**
1. Apply upgrades:
   
   ```bash
   sudo apt upgrade -y
   ```
   
3. Verify that updates were applied successfully:
   
   ```bash
   apt list --upgradable
   ```
   
   (Ideally, no packages should remain upgradable.)

#### **Part 4 – Re-Scan After Updates**
1. Regenerate the SBOM:
   
   ```bash
   syft packages:apt -o spdx-json > system_sbom_after.json
   ```
   
3. Re-run the vulnerability scan:
   
   ```bash
   grype sbom:system_sbom_after.json -o table > system_vulns_after.txt
   ```
   
5. Compare your “before” and “after” results.  
   - Did the number or severity of vulnerabilities change?  
   - What patterns do you notice?  
   - How does patching contribute to system assurance?

#### **Part 5 – Reflection**
Answer the following in 2–3 sentences each:

1. How does maintaining updated packages illustrate *complete mediation*?  
2. Why is generating a new SBOM after patching essential to assurance?  
3. What risks persist when organizations delay system updates?  
4. How does this exercise embody the *secure design lifecycle* principle?

### **Deliverables**
**GitHub Submission**:

Upload a .PDF containing:

1. `system_sbom_before.json` and `system_sbom_after.json`  
2. `system_vulns_before.txt` and `system_vulns_after.txt`  
3. A one-page reflection answering Part 5 questions and summarizing changes observed.

...to `/deliverables/` and push to GitHub.

**Canvas Submission**:

1. Copy your forked repository URL: Go to your forked repo on GitHub (it should look something like:
   
     `https://github.com/<your-username>/eng298-fa25-mod7-sbom-lab2`
   
   - Copy the URL from your browser’s address bar.

3. Submit the URL in Canvas: Module 7: Assignment: Maintaining Secure Systems with SBOMs and Patching

### **Grading (20 Points Total)**

| **Category** | **Description** | **Points** |
|---------------|-----------------|------------|
| **Baseline Scan** | Complete system SBOM and vulnerability report generated before patching | 5 |
| **Update Process** | Correct use of `apt update` / `apt upgrade` with verification | 5 |
| **Post-Update Scan** | Clear comparison demonstrating effect of updates on vulnerabilities | 5 |
| **Reflection & Clarity** | Insightful explanation connecting patching to security-engineering principles | 5 |

