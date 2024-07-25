---
published: true

layout: post

title: Does the 'Best Evidence' rule apply in Australia?

image: /images/conny-schneider-3hkKv6WzjcE-unsplash.jpg

categories: [DFIR, Cybersecurity, Certification, Legal]

---

_Discussion of the relevance of the best evidence rule in the Australian legal context for digital evidence._

![digital gavel]({{ site.baseurl }}/images/conny-schneider-3hkKv6WzjcE-unsplash.jpg "Cyberwarfare and Cyberterrorism") 
_Photo by [Conny Schneider](https://unsplash.com/@choys_)_   

#### Introduction

Digital forensics is the science of collecting, preserving, analysing, and presenting digital evidence in a court of law. Many cybersecurity certifications (CISSP, CISM, CCE, GCFE) cover the importance of the “best evidence rule” in the collection of digital evidence. This blog post provides some perspective for Australian practitioners and insights into how the rules of evidence differ compared to the United States, and why if evidence has not been collected in the "best" of circumstances it may still be admissible in an Australian courtroom. 

#### The Best Evidence Rule

The best evidence rule is a common law principle that dates back to 18th Century England in a case called [Omychund v Barker (1745) 26 ER 15](https://vlex.co.uk/vid/omychund-v-barker-804436045). Lord Harwicke stated that no evidence was admissible unless it was the _"best nature will allow"_. Later cases use this [obiter](https://en.wikipedia.org/wiki/Obiter_dictum) to mean that only originals were admissible as evidence. This rule applied to documents, which, back then, were copied by hand, a process with a significant chance of introducing error or fraud.

#### The United States: The Common Law Approach

In the United States, many jurisdictions still adhere to the 18th Century common law best evidence rule, which mandates that only originals are admissible as evidence. This rule applies to both paper and digital documents, although there are some exceptions and variations depending on the state and the type of evidence.

For instance, some states permit copies of digital evidence to be admitted only if the original is lost, destroyed, or inaccessible. Copies may also be admissible if they are authenticated by an expert witness or through other means. Additionally, certain types of digital evidence, such as emails, text messages, or social media posts, are subject to specific rules in some states.

Digital forensics experts in the United States face the challenge of proving that the digital evidence they present is an accurate and faithful representation of the original data. This involves adhering to strict procedures and standards for collecting, preserving, analysing, and presenting digital evidence. In practical terms, this means that the party adducing the evidence in court has the burden of proof in showing that it is a true copy of the original. The digital forensics industry is built around tools to ensure that any digital evidence acquired can be proven to be “best evidence”, which is why write-blocking devices and cryptographically verifiable checksums of images are crucial.

#### Australia: The Statutory Approach

In contrast, Australia has largely abolished the best evidence rule through legislation. Most Australian jurisdictions have introduced [uniform evidence legislation](https://austlii.edu.au/cgi-bin/viewdb/au/legis/cth/consol_act/ea199580/), which harmonises and codifies the evidence laws across federal and state jurisdictions. [Section 147](https://austlii.edu.au/cgi-bin/viewdoc/au/legis/cth/consol_act/ea199580/s147.html) of the Evidence Act 1995 _(Cth)_ exemplifies this. It specifies that a document, which includes digital evidence, produced by a machine e.g., a photocopier is presumed to be the same as the original unless there is _"evidence sufficient to raise doubt about the presumption."_ This essentially reverses the burden of proof found in the common law, placing the burden on the party challenging the evidence to prove that it has been altered.

#### Implications for Digital Forensics in Australia

In Australia, while the abolition of the best evidence rule simplifies the admissibility of digital evidence, forensic experts still need to ensure that their evidence handling and presentation meet the standards of relevance and reliability. The reverse burden of proof under section 147 of the Evidence Act 1995 _(Cth)_ means that the defence must provide credible evidence to challenge the presumption of the accuracy of digital copies.  
In my opinion, this doesn't mean you can stop paying for EnCase and use [Robocopy](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/robocopy) instead; rather, it means if there are situations where evidence was copied in less than ideal circumtances, do not lose hope, it may still be valid in an Australian courtroom.

