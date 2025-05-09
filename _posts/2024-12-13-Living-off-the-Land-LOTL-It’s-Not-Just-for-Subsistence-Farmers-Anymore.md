---
published: true

layout: post

title: "Living off the Land (LOTL): It’s Not Just for Subsistence Farmers Anymore!"

image: /images/james-baltz-zuhouVw4ZkQ-unsplash.jpg
---

_xxxxxx, _

![living off the land techniques IRL]({{ site.baseurl }}/images/james-baltz-zuhouVw4ZkQ-unsplash.jpg "LOTL in cybersecurity") 
_Photo by [James Baltz](https://unsplash.com/@jimbob63) on [Unsplash](https://unsplash.com/s/photos/cyber-warfare-terrorism)_  

      

Picture this: You’re reviewing a device timeline in the [Microsoft 365 Defender portal](https://security.microsoft.com) after a suspected breach. All the suspicious entries you see involve native Windows 11 binaries: `powershell.exe`, `cmd.exe`, `rundll32.exe`. There’s no obvious giveaway: no Mimikatz dumping credentials, no telltale ransomware payload pulled down by a browser. You know something isn’t right, Defender hasn’t raised any alerts. It’s as if you’re chasing ghosts. This is the new reality for security teams. 

Living Off the Land (LOTL) threats are the new normal. From low-rent ransomware operators to state-sponsored APTs, adversaries now weaponise legitimate system tools rather than deploy malicious executables. In this post, I’ll give you survery of the various definitions of "LOTL"  and take a look at community projects that try and document LOTL tactics, threats and procedures (TPPs) and explain the variance in definitions. because spolier alert: LOTL doesn't mean the same thing to everyone. 

## When is malware not malware?
In CrowdStrike's 2025 Global Threat Report, it was found that 79% of detections were malware-free. Table 1 below highlights the increasing trend of malware-free detections (often involving Living-off-the-Land techniques) as reported in CrowdStrike's Global Threat Reports over the last six years.

#### Figure 1: Rise of Malware-Free attacks in CrowdStrike's Annual Threat Reports
![CrowdStrike Global Threat Report 2025 malware free attacks detected](/images/crowdstrike-global-threat-report-2025.png "Malware free attacks")

*Source: [CrowdStrike Global Threat Reports](https://www.crowdstrike.com/resources/reports/)*
## LOTL: An Origin Story

Traditionally, the phrase _“living off the land”_ describes the practice of subsisting on natural resources through farming and hunting. In cybersecurity, this same concept is applied to threat actors exploiting installed binaries, scripts, and tools on target systems to carry out malicious objectives.

The phrase and the acronym **LOTL** were first popularised at the hacker conference [DerbyCon](https://en.wikipedia.org/wiki/DerbyCon) in 2013, along with related terms like _LOLBins_ and _LOLBAS_ (*Living-off-the-Land Binaries and Scripts*). Shortly after DerbyCon, a collective effort called the [LOLBAS Project](https://github.com/LOLBAS-Project/LOLBAS) launched on GitHub. Its goal was to:

- Document every Windows binary and script with <u>hidden or unexpected features</u> that attackers might exploit; and  
- Map each of these LOLBins to known tactics within the [MITRE ATT&CK framework](https://attack.mitre.org/) so defenders can see which stage of an attack a particular binary might be used in.


The LOLBAS Project defines a very narrow set of rules for what qualifies as a LOLBAS, it must:

1. Be **Microsoft-signed** (i.e., trusted by the operating system);  
2. Possess **unexpected functionality** that threat actors can exploit, and;  
3. Map to a **legitimate tactic or technique** in MITRE ATT&CK.

A few years after LOLBAS took off, a similar project emerged for Unix-like systems: [GTFOBins](https://gtfobins.github.io/) (Get the F** Out Binaries*). It was created in 2018 by security researchers inspired by the idea of cataloguing legitimate binaries that could be abused for privilege escalation, command execution, and data exfiltration on Unix systems.

Unlike the LOLBAS Project, GTFOBins project has a wider definition for what they includ as a LOTL binary. If a binary is typical on Unix machine and can help an attacker perform a task to bypass security restictions or some other abuse by an attacker, no matter how obvious the functionality is, then it’s in scope.

Here's a table explaining the scope differences between the projects:  

### LOLBAS vs GTFOBins: A Quick Comparison

| Feature                     | **LOLBAS (Windows)**                                          | **GTFOBins (Unix/Linux)**                                  |
|----------------------------|---------------------------------------------------------------|-------------------------------------------------------------|
| Platform                   | Windows                                                       | Unix-like (Linux, macOS, etc.)                              |
| Signature requirement      | Must be **Microsoft-signed**                                  | No signing requirement                                      |
| Focus                      | Exploiting **unexpected or non-obvious** functionality        | Exploiting **any useful** functionality                     |
| Inclusion criteria         | Strict (signed, exploitable, maps to MITRE ATT&CK tactic)     | Broad (any native binary that can assist in an attack)      |
| Examples                   | `rundll32.exe`, `mshta.exe`, `regsvr32.exe`                  | `bash`, `awk`, `scp`, `find`, `perl`                         |
| Primary use case           | Defender awareness of obscure abuses in trusted binaries      | Attacker-friendly reference for post-exploitation tactics   |
| Project URL                | [LOLBAS ](https://lolbas-project.github.io/)  | [GTFOBins](https://gtfobins.github.io/)                                     |


## LOTL: Blurred Lines in Practice
While the LOLBAS and GTFOBins projects define clear inclusion criteria, the real-world application of LOTL concepts often blurs these lines. Many tools used by malware are built-in system utilities with expected functionality, but they're still used maliciously.

Take vssadmin.exe, for example — commonly used by ransomware to delete Volume Shadow Copy backups before encrypting files. Although this is expected behaviour for the binary, most analysts still classify this as a LOTL technique.

In other words, the practical definition of LOTL tends to be more inclusive than any formal list — it’s less about surprise functionality and more about intent and context.
