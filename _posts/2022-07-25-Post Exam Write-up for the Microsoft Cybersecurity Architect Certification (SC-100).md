---
published: true

layout: post

title: Post Exam Write-up for the Microsoft Cybersecurity Architect Certification (SC-100)

image: /images/ms-cyber-security-architect-expert-sc-100.png

categories: [Certification, Cybersecurity, Azure]
--- 

_This post describes my experience in preparing for and passing the Microsoft Cybersecurity Architect certification exam (SC-100).  I’ll describe some background about the exam, the resources I used and provide a link to my notes._

![Microsoft Certification badge for SC-100]({{ site.baseurl }}/images/ms-cyber-security-architect-expert-sc-100.png "Microsoft Cybersecurity Architect Certification") 
  

# Exam Background
The Microsoft Cybersecurity Architect certification is the latest addition to Microsoft’s role based certifications for Azure.  As an architect exam it means it covers a lot of products and features, but not a lot of depth about how to implement those features. To gain the certification, you need to have completed any one of the other four cloud certifications which cover security aspects of Azure or Microsoft 365. They are: [SC-200](https://docs.microsoft.com/en-us/certifications/exams/sc-200){:target="_blank"} , [SC-300](https://docs.microsoft.com/en-us/certifications/exams/sc-300){:target="_blank"}, [MS-500](){:target="_blank"} or [AZ-500](){:target="_blank"}

The SC-100 exam recently (July 2022) came out of beta. What this means is that if you are lucky enough to work for an organization that has access to the [Microsoft Enterprise Skills Initiative](https://esi.microsoft.com/){:target="_blank"} program, you can sit the exam for free. 

# My Thoughts and Experience

If you've previously passed the AZ-500, the Azure  have had experience in Azure then the SC-100 should be quite easy for you.  You should have a high-level understanding of products such as:
* Microsoft Purview
* Defender for Cloud Apps
* Azure Blueprint
* Azure Policy

It's also important to know about:
* Tools in Azure DevOps and tools in Github Enterprise that can be used to automatically scan source code for credential and key leaks. 
* Know the difference between Microsoft managed keys and customer managed key, and what the default encryption and rotation period is for Microsoft managed keys.
* The difference between Azure SQL Database features of Data Masking and SQL Always Encrypted, and the key options for SQL Azure TDE (Transparent Data Encryption)
* The typical use cases for using an Application Gateway WAF (Web Application Firewall) and an Azure Front Door WAF.
* Use cases for Azure Container Registry (ACR) and tools you would use to automate container builds in Azure.
* What the use cases are for Private Endpoints.
* Know about the Microsoft Threat Modeling Tool.

## Resources 
The only resource I used for this exam was [John Savill's SC-100 cram video](https://www.youtube.com/watch?v=2Qu5gQjNQh4){:target="_blank"}.  This is all I needed.  It's a 1h 40 min video cram session, but if you are a native English speaker, then you can comfortably bump the playback speed up to x1.5. 

John's opinion of the exam is that it's quite basic. The exam length is 120 minutes. John speedran the exam and said it took him 30 minutes to complete it.  I took a similar approach and finished it in 40 minutes, scoring  748/1000 (see my exam report below). Even for the case study questions, you can take an educated guess what the answer is, without reading the case study.  

![Microsoft Certification exam report]({{ site.baseurl }}/images/sc-100-score-report-1.PNG "SC-100 exam report") 
_My exam report result_   


[I've provided a copy of my notes here](/assets/html/sc-100-notes.md){:target="_blank"}.

Goodluck!!
