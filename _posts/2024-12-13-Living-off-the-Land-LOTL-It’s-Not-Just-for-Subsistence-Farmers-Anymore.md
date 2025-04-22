---
published: false

layout: post

title: "Living off the Land (LOTL): It’s Not Just for Subsistence Farmers Anymore!"

image: /images/james-baltz-zuhouVw4ZkQ-unsplash.jpg
---

_xxxxxx, _

![living off the land techniques IRL]({{ site.baseurl }}/images/james-baltz-zuhouVw4ZkQ-unsplash.jpg "LOTL in cybersecurity") 
_Photo by [James Baltz](https://unsplash.com/@jimbob63) on [Unsplash](https://unsplash.com/s/photos/cyber-warfare-terrorism)_  

      

Picture this: You’re reviewing a device timeline in the [Microsoft 365 Defender portal](https://security.microsoft.com) after a suspected breach. All the suspicious entries you see involve native Windows 11 binaries: `powershell.exe`, `cmd.exe`, `rundll32.exe`. There’s no obvious giveaway: no Mimikatz dumping credentials, no telltale ransomware payload pulled down by a browser download. Yet you know something isn’t right, but Defender hasn’t raised any alerts. It’s as if you’re chasing ghosts.

Living Off the Land (LOTL) is the new normal. From low-rent ransomware operators to state-sponsored APTs, adversaries now weaponise legitimate system tools rather than deploy malicious executables. In this post, I’ll give you my insight into the various definitions of "LOTL"  and based on [my research](assets/pdf/lotl_paper_nkavadias.pdf) I'll introduce a tiered framework for understanding the term, because spolier alert: it doesn't mean the same thing to everyone. 

## LOTL: An Origin Story

Traditionally, the phrase _“living off the land”_ describes the practice of subsisting on natural resources through farming and hunting. In cybersecurity, this same concept is applied to threat actors exploiting installed binaries, scripts, and tools on target systems to carry out malicious objectives.

The phrase and the acronym **LOTL** were first popularised at the hacker conference [DerbyCon](https://en.wikipedia.org/wiki/DerbyCon) in 2013, along with related terms like _LOLBins_ and _LOLBAS_ (*Living-off-the-Land Binaries and Scripts*). Shortly after DerbyCon, a collective effort called the [LOLBAS Project](https://github.com/LOLBAS-Project/LOLBAS) launched on GitHub. Its goal was to:

- Document every Windows binary and script with <u>hidden or unexpected features</u> that attackers might exploit; and  
- Map each of these LOLBins to known tactics within the [MITRE ATT&CK framework](https://attack.mitre.org/) so defenders can see which stage of an attack a particular binary might be used in.


The LOLBAS Project defines a very narrow set of rules for what qualifies as a LOLBAS, it must:

1. Be **Microsoft-signed** (i.e., trusted by the operating system);  
2. Possess **unexpected functionality** that threat actors can exploit, and;  
3. Map to a **legitimate tactic or technique** in MITRE ATT&CK.

A few years after LOLBAS took off, a similar project emerged for Unix-like systems: GTFOBins (Get the F** Out Binaries*). It was created in 2018 by security researchers [Andrea Cardaci](https://cardaci.xyz/) and [Emilio Pinna](https://x.com/norbemi), who were inspired by the idea of cataloguing legitimate binaries that could be abused for privilege escalation, command execution, and data exfiltration on Unix systems.

Unlike LOLBAS, GTFOBins has a wider definition for a LOLBin. If a binary is already on a typical Unix machine and can help an attacker perform a task—no matter how obvious the functionality is, then it’s in scope.

Each GTFOBin entry outlines how the tool can be used maliciously and is tagged into categories for abuse, with the entry reading a lot like a [man page](https://en.wikipedia.org/wiki/Man_page) for red teamers. 

Here's a table which explains the differences between the projects:  

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


But here’s where definitions can get muddy. It's common in malware to see the same built-in system tools used maliciously, even if it’s _expected_ behaviour. For example,  deleting [volume shadow copy](https://learn.microsoft.com/en-us/windows-server/storage/file-server/volume-shadow-copy-service) backups via `vssadmin.exe` which almost all cryptolockers do before they start encrypting files. Most security researchers will lump that into being a LOTL, attack whether the functionality is "unexpected" or not, although strictly speaking by the LOLBAS project's definition vssadmin.exe isn't a LOLBin. 
