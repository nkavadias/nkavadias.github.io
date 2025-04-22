---
published: false
layout: post
title: "Living off the Land (LOTL): It’s Not Just for Subsistence Farmers Anymore!"
image: /images/james-baltz-zuhouVw4ZkQ-unsplash.jpg
---

_xxxxxx, _

![living off the land techniques IRL]({{ site.baseurl }}/images/james-baltz-zuhouVw4ZkQ-unsplash.jpg "LOTL in cybersecurity")  
_Photo by [James Baltz](https://unsplash.com/@jimbob63) on Unsplash_

---

## 1. Why another LOTL post?

Mention “living off the land” in a SOC and you’ll hear at least five different definitions.  
*Is it fileless malware? A list of sneaky Windows binaries? Anything signed by Microsoft?*  
Spoiler: the industry can’t agree.  

This article untangles the naming mess. We’ll start with the OG Windows and Linux lists, then look at newer spin‑offs for macOS, kernel drivers and cloud control planes — and finish with why those neat lists crumble in real incidents.

---

## 2. LOTL: Where the term came from  

*Living off the land* jumped from bushcraft to cybersecurity at **DerbyCon 2013**.  
The idea: if the malicious payload is the operating system itself, signature‑based AV has nothing to scan.  

Soon after, the community launched **LOLBAS** — *Living‑off‑the‑Land Binaries And Scripts* — with three inclusion rules:

1. Must be **Microsoft‑signed**.  
2. Must have **unexpected or dual‑use functionality**.  
3. Must map to a MITRE ATT&CK tactic.

---

## 3. Windows vs Linux: LOLBAS & GTFOBins

A Linux‑flavoured twin, **GTFOBins** (Get‑The‑F\*\*‑Out Binaries), appeared in 2018. It keeps the spirit but drops the signing and “unexpected” requirements: if the binary comes with the OS and can help attackers, in it goes.

| Feature               | **LOLBAS (Windows)** | **GTFOBins (Unix/Linux)** |
|-----------------------|-----------------------|---------------------------|
| Signature?            | Microsoft‑signed only | None required |
| Focus                 | **Hidden** tricks     | **Any** useful trick |
| Inclusion criteria    | Strict, maps to ATT&CK| Broad, post‑exploitation |
| Example binaries      | `rundll32.exe`, `regsvr32.exe` | `bash`, `scp`, `find` |
| URL                   | lolbas‑project.github.io | gtfobins.github.io |

---

## 4. Beyond Windows & Linux: The newer lists

| Nickname | Scope | One‑liner | Project link |
|----------|-------|-----------|--------------|
| **LOOBins** | macOS | Apple‑signed binaries with attacker value | loobins.io :contentReference[oaicite:0]{index=0} |
| **LOLDrivers** | Windows **kernel drivers** | Vulnerable or malicious drivers (BYOVD heaven) | loldrivers.io :contentReference[oaicite:1]{index=1} |
| **LOLCloud** | AWS / Azure / GCP | Native cloud CLI & control‑plane calls for recon, persistence, escalation | beercow.github.io/LOLCloud‑Project :contentReference[oaicite:2]{index=2} |

Even government guidance now lumps these resources together when advising defenders on LOTL tradecraft :contentReference[oaicite:3]{index=3}.

---

## 5. LOTL: Blurred lines in practice  

The lists are handy cheat‑sheets, but everyday DFIR is messier:

* **`vssadmin.exe`** — legit backup‑management tool, ransomware delete‑all‑shadows favourite.  
* **`wmic.exe` / `netsh.exe`** — totally expected on admins’ boxes, Volt Typhoon lives inside them.  
* **Cloud IAM CLI** — nothing exotic, but one scripted loop can spray new keys across an AWS org.

Analysts therefore stretch the label based on **intent & context**, not rule‑book purity.

---

## 6. Recap & take‑aways

* *LOTL* now covers at least **five** curated projects: LOLBAS, GTFOBins, LOOBins, LOLDrivers, LOLCloud.  
* Only LOLBAS insists on “unexpected” tricks; the rest care mainly that the tool is **native & trusted**.  
* Real incidents don’t check criteria; defenders must watch for *when* and *how* a tool fires, not just *what* it is.

If the payload comes pre‑installed, trust is already broken.  
Know the lists — but monitor the behaviour.

---

*Based on insights from my recent LOTL survey and continuing research into attacker use of native tooling.* 
