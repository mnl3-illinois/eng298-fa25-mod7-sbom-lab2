# Reflection – Module 7: Maintaining Secure Systems with SBOMs & Patching

### Baseline Findings
When I generated the SBOM with Syft, I realized how many Ubuntu packages are actually running in the background for the Codespace. The Grype scan also showed a bunch of vulnerabilities across different levels, mostly High and Medium.

I focused on CVE-2023-44487. It's an HTTP/2 issue called “Rapid Reset,” where an attacker repeatedly opens and cancels streams to overwhelm a server. This can lead to major denial-of-service attacks because it drains server resources super fast.

---

### Packages with Available Updates
When I ran `sudo apt list --upgradable`, it just said “Listing... Done,” meaning there were zero updates available. So the system was already totally up-to-date and didn’t need any upgrades.

---

### How does maintaining updated packages illustrate complete mediation?
Updating packages makes sure every part of the system keeps getting re-verified before it runs. Complete mediation is about constantly checking access, and patching helps enforce that by removing outdated or vulnerable components.

---

### Why is generating a new SBOM after patching essential to assurance?
A new SBOM basically confirms that the patches actually went through. It gives a clear, updated picture of the system so you can see that the old vulnerable versions were replaced.

---

### What risks persist when organizations delay system updates?
Delaying updates leaves known vulnerabilities exposed and easy for attackers to find. Since attackers actively scan for unpatched systems, even a short delay can create unnecessary security risks.

---

### How does this exercise embody the secure design lifecycle principle?
This whole process shows how security is continuous. You get visibility through the SBOM, verify with vulnerability scans, take action with patching, and then repeat. It fits the secure design lifecycle because it focuses on ongoing assurance instead of one-time fixes.
