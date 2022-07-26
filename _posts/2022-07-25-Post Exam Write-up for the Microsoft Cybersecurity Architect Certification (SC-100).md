---
published: true

layout: post

title: Post Exam Write-up for the Microsoft Cybersecurity Architect Certification (SC-100)

image: /images/ms-cyber-security-architect-expert-sc-100.png

categories: [Certification, Cybersecurity, Azure]
--- 

_This post describes my experience preparing for and passing the Microsoft Cybersecurity Architect certification exam (SC-100). I’ll describe some background about the exam and the resources I used, I'll also provide my notes._

![Microsoft Certification badge Microsoft Cybersecurity Architect Certification]({{ site.baseurl }}/images/ms-cyber-security-architect-expert-sc-100.png "Microsoft Cybersecurity Architect Certification") 
![Microsoft Certification badge for SC-100 exam]({{ site.baseurl }}/images/ms-sc-100-exam.png "Microsoft Certification badge for SC-100 exam") 


# Exam Background
The Microsoft Cybersecurity Architect certification is the latest addition to Microsoft's role-based certifications for Azure. It's an architect exam, meaning it covers a lot of products and features but without a lot of depth. To gain the certification, you must have completed one of the following four cloud certifications that cover security aspects of Azure or Microsoft 365.  They are: [SC-200](https://docs.microsoft.com/en-us/certifications/exams/sc-200){:target="_blank"} , [SC-300](https://docs.microsoft.com/en-us/certifications/exams/sc-300){:target="_blank"}, [MS-500](){:target="_blank"} or [AZ-500](){:target="_blank"}.

The SC-100 exam recently (July 2022) came out of beta. What this means is that if you are lucky enough to work for an organization that has access to the [Microsoft Enterprise Skills Initiative](https://esi.microsoft.com/){:target="_blank"} program, you can sit the exam for free. 

# My Thoughts and Experience

If you've previously passed the Azure Security Technologies exam (AZ-500), or are an Azure  Solutions Architect Expert (AZ-305), then SC-100 should be easy for you. It would also encourage you to have at least a high-level understanding of products and features such as:
* Microsoft Purview
* Defender for Cloud Apps
* Azure Blueprint
* Azure Policy

It's also important to know about:
* Tools in Azure DevOps and Github Enterprise that can be used to scan source code for credentials and secret keys automatically. 
* Know the difference between Microsoft managed keys and customer managed keys, and what the default encryption and rotation period is for Microsoft managed keys.
* The difference between Azure SQL Database features of Data Masking and SQL Always Encrypted and the key options for SQL Azure TDE (Transparent Data Encryption)
* The typical use cases for using an Application Gateway WAF (Web Application Firewall) and an Azure Front Door WAF.
* Use cases for Azure Container Registry (ACR) and tools you would use to automate container builds in Azure.
* What the use cases are for Private Endpoints.
* Know about the Microsoft Threat Modeling Tool.

## Resources 
The only resource I used for this exam was [John Savill's SC-100 cram video](https://www.youtube.com/watch?v=2Qu5gQjNQh4){:target="_blank"}.  This is all I needed.  It's a 1h 40 min video cram session, but if you are a native English speaker, then you can comfortably bump the playback speed up to x1.5. 

John's opinion of the exam is that it's quite basic. The exam length is 120 minutes. John speedran the exam and said it took him 30 minutes to complete it.  I took a similar approach and finished it in 40 minutes, scoring  748/1000 (see my exam report below). Even for the case study questions, you can take an educated guess of what the answer is, without reading the case study.  

![Microsoft Certification exam report]({{ site.baseurl }}/images/sc-100-score-report-1.png "SC-100 exam report") 
_My exam report result_   


[I've provided a copy of my notes here](/assets/html/sc-100-notes.html){:target="_blank"}.

Goodluck!!
