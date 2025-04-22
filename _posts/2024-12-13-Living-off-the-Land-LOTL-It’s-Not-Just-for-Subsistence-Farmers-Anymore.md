---
published: false

layout: post

title: "Living off the Land (LOTL): It’s Not Just for Subsistence Farmers Anymore!"

image: /images/james-baltz-zuhouVw4ZkQ-unsplash.jpg
---

_An essay on the definition of cyberwarfare and cyberterrorism and how Australia's terrorism laws differ from other western democracies._

![living off the land techniques IRL]({{ site.baseurl }}/images/james-baltz-zuhouVw4ZkQ-unsplash.jpg "LOTL in cybersecurity") 
_Photo by [James Baltz](https://unsplash.com/@jimbob63) on [Unsplash](https://unsplash.com/s/photos/cyber-warfare-terrorism)_  

      

Picture this: You’re reviewing a device timeline in the [Microsoft 365 Defender portal](https://security.microsoft.com) after a suspected breach. All the “suspicious” entries you see involve native Windows 11 binaries: `powershell.exe`, `cmd.exe`, `rundll32.exe`. There’s no obvious giveaway: no Mimikatz dumping credentials, no telltale ransomware payload pulled down by a suspicious browser download. Yet you know something isn’t right, but Defender hasn’t flagged anythin. It’s as if you’re chasing ghosts.

Living Off the Land (LOTL) is the new normal. From small-scale ransomware operators to state-sponsored APTs, adversaries now weaponise legitimate system tools rather than deploy malicious executables. In this post, I’ll give you my insight into the various definitions of “LOTL”  based on my research and introduce a simple hierarchical definition in order to help you gain a better understanding of the scope of LOTL

## Ok, who come up with this phrase LOTL?

Traditionally, the phrase _“living off the land”_ describes the practice of subsisting on natural resources through farming and hunting. In cybersecurity, this same concept is applied to threat actors exploiting installed binaries, scripts, and tools on target systems to carry out malicious objectives.

The phrase and the acronym **LOTL** were first popularised at the hacker conference [DerbyCon](https://en.wikipedia.org/wiki/DerbyCon) in 2013, along with related terms like _LOLBins_ and _LOLBAS_ (*Living-off-the-Land Binaries and Scripts*). Shortly after DerbyCon, a collective effort called the [LOLBAS Project](https://github.com/LOLBAS-Project/LOLBAS) launched on GitHub. Its goal was to:

- Document every Windows binary and script with hidden or unexpected features that attackers might exploit; and  
- Map each of these LOLBins to known tactics within the [MITRE ATT&CK framework](https://attack.mitre.org/) so defenders can see which stage of an attack a particular binary might be used in.

A similar project, _GTFOBins_ (*Get the F*** Out Binaries*), catalogues Unix-based equivalents. Both aim to help defenders identify which native binaries are likely to be used by an attacker.

The LOLBAS Project defines a very narrow set of rules for what qualifies as a LOLBAS, it must:

1. Be **Microsoft-signed** (i.e., trusted by the operating system);  
2. Possess **unexpected functionality** that threat actors can exploit, and;  
3. Map to a **legitimate tactic or technique** in MITRE ATT&CK.

But here’s where the industry’s definitions can get muddy. It is common in malware to see the same built-in system tool used maliciously—even if it’s _expected_ behaviour. For example,  deleting [volume shadow copy](https://learn.microsoft.com/en-us/windows-server/storage/file-server/volume-shadow-copy-service) backups via `vssadmin.exe` which almost all cryptolockers do before they start encrypting files. Researchers will lump that as a  LOTL, attack whether the functionality is “unexpected” or not.
