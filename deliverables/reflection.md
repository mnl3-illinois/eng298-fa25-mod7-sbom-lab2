# Reflection – Module 7: Maintaining Secure Systems with SBOMs & Patching

### Baseline Findings
After generating the SBOM using Syft, I found that the system included a large number of Ubuntu-managed packages that make up the full Codespaces environment. The Grype scan identified vulnerabilities across multiple severities, including several High and Medium issues.

I selected one CVE from the report: CVE-2023-44487. According to the NVD, this vulnerability is caused by a weakness in the HTTP/2 protocol called “Rapid Reset,” where an attacker repeatedly opens and cancels streams to overwhelm a server. This matters because it can lead to massive denial-of-service attacks that take systems offline by exhausting their resources.

---

### Packages with Available Updates
When I ran `sudo apt list --upgradable`, the system returned “Listing... Done,” which means there were no packages with updates available. The Codespace environment was already fully up-to-date, so no upgrades were required.


---

### How does maintaining updated packages illustrate complete mediation?
Keeping packages updated ensures that every component of the system is continuously checked and verified before it runs. Complete mediation requires reevaluating trust constantly, and patching enforces this by removing outdated or vulnerable software.

---

### Why is generating a new SBOM after patching essential to assurance?
A new SBOM proves that patches were actually applied. It gives visibility into the new system state and confirms that vulnerable versions were replaced, providing the transparency needed for system assurance.

---

### What risks persist when organizations delay system updates?
Delaying updates leaves known vulnerabilities exposed and increases the risk of exploitation. Attackers routinely scan for unpatched systems, so even short delays can create a dangerous exposure window.

---

### How does this exercise embody the secure design lifecycle principle?
This exercise demonstrates how visibility (SBOM), verification (vulnerability scanning), and action (patching) work together in a continuous loop. Instead of one-time security efforts, it reinforces ongoing maintenance and assurance in the secure design lifecycle.
