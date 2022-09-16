---
published: true

layout: post

title: Future Developments and Challenges in Evidence Recovery for Digital Forensics

image: /images/adi-goldstein1.jpg

categories: [DFIR, Cybersecurity]
--- 

_This report discusses future developments and challenges in evidence recovery for digital forensics and new laws, techniques and technology developed to overcome these issues._


![DFIR cybersecurity digital forensics]({{ site.baseurl }}/images/adi-goldstein1.jpg "Future of Evidence Recovery for Digital Forensics") 
_Photo by [Adi Goldstein](https://unsplash.com/@adigold1){:target="_blank"} on [Unsplash](https://unsplash.com/s/photos/hacking){:target="_blank"}_   

# Introduction
This report discusses future developments and challenges in evidence recovery for digital forensics. The exponential growth in volumes of data, the increase in Internet of Things (IoT) devices and the ubiquity of encryption all pose challenges to the digital forensics practitioner. It also discusses new techniques and technology developed to overcome these issues and how the Australian and US governments have responded to these challenges by introducing new laws.

# Growth in data volumes
The increasing data capacities held by suspects are creating problems for forensic investigations. Currently (August 2022), the largest hard drive capacity for a personal computer is 20 terabyte (TB), with [Seagate having plans for a 30 TB HDD in 2023](https://www.extremetech.com/computing/338238-seagate-to-launch-30tb-hard-drives-in-2023){:target="_blank"}. Growth rate predictions for computer hard drives are estimated at 30% per year, meaning consumers will have access to hard drives above 70 TB in the next five years [(Evans, 2019)](https://www.architecting.it/blog/dude-wheres-my-100tb-hard-drive/){:target="_blank"}. Although drive capacities are increasing, disk throughput is not. According to Novak et al. [(2019)](https://www.ojp.gov/pdffiles1/nij/250700.pdf){:target="_blank"}, physical acquisition of a 1TB drive can take 11 hours, creating significant delays for time-critical law enforcement investigations and creating investigation backlogs. Researchers are investigating new techniques for speeding up acquisition and analysis. Sifting collectors and using public cloud compute clusters are two methods of helping solve the data volume growth problem.

## Sifting Collectors
Most law enforcement agencies still perform physical disk acquisition for forensic investigations, which can take days to complete with larger volumes. Although, for most investigations, the files of interest in the investigation are user documents, email, internet history and illicit videos and images. A sifting collect allows an investigator to skip the acquisition of program binaries, operating system files, and blank space and focus on areas of the disk that contain temporary files, history, logs, browser artifacts, and system metadata. In testing, Sifting Collectors have been two to fourteen times faster than traditional acquisition methods whilst still yielding up to 95% of evidence [(Novak et al., 2019)](https://www.ojp.gov/pdffiles1/nij/250700.pdf){:target="_blank"}. 

## Public Cloud Compute Clusters
While sifting collectors focus on improving acquisition speed, tools that utilise public cloud, such as the open source project [Digital Forensics Compute Cluster (DFORC2)](https://github.com/RANDCorporation/DFORC2){:target="_blank"} focus on accelerating digital data analysis of acquired images. DFORC2 takes advantage of the parallel computing power available in public cloud providers, such as Amazon Web Services (AWS). Essentially, the project uses stream processing technology [(Kafka)](https://kafka.apache.org/){:target="_blank"} to process a disk image in multiple [Apache Spark](https://spark.apache.org/){:target="_blank"} nodes and then present the processed data to a cloud-based [Autopsy](https://www.autopsy.com/){:target="_blank"} front-end for an investigator to perform analysis. The solution uses Kubernetes meaning that Spark nodes can be scaled out [(Novak et al., 2019)](https://www.ojp.gov/pdffiles1/nij/250700.pdf){:target="_blank"}.

# Growth of Internet Of Things (IoT)
The growth of the heterogeneous nature of the IoT devices that can hold potential evidence will continue to cause problems for forensic investigators as the number of smart consumer devices grows. Apart from the increased difficulty in the acquisition of embedded devices that may hold local storage evidence, the bigger problem with IoT is that devices send data to the cloud for persistent storage. In many cases, it may not be apparent to investigators where the data is located in the cloud and may create multi-jurisdictional problems in trying to subpoena vendors [(Lillis et al., 2016)](https://arxiv.org/pdf/1604.03850.pdf){:target="_blank"}.   
Whilst not only useful for IoT, but for any data stored in the cloud, US legislators have introduced the [_Clarifying Lawful Overseas Use of Data (CLOUD) Act_](https://en.wikipedia.org/wiki/CLOUD_Act){:target="_blank"} [(Box, 2020)](https://iapp.org/news/a/how-the-cloud-act-will-affect-the-way-cloud-providers-serve-their-customers/){:target="_blank"} as a way for law enforcement to gain certainty over the data stored in foreign jurisdictions. The Act requires that data held by a US company can be subpoenaed by federal law enforcement no matter where the data is stored in the world. Furthermore, Australia recently signed a mutual legal assistance treaty, passing it into local law with the Telecommunications Legislation Amendment (International Production Orders) Bill 2020. This reciprocal arrangement allows Australian law enforcement to compel US companies in a similar way to CLOUD but also allows for US law enforcement to compel Australian businesses for similar data access rights [(Garland, 2021)](https://www.insideprivacy.com/cross-border-transfers/australia-passes-cross-border-data-access-law-creates-a-pathway-for-cloud-act-bilateral-agreement/){:target="_blank"}. 

# Ubiquity of Encryption 
Another problem for future forensic investigations is strong encryption on devices, which can prevent forensic analysis, especially for mobile technology, where both the latest iOS and Android operating systems encrypt filesystems by default [(Nield, 2020)](https://www.wired.com/story/smartphone-encryption-apps/){:target="_blank"}. Although there are ever-increasing sophisticated ways to use unpatched exploits to break into devices using tools created by vendors such as [Cellebrite](https://cellebrite.com){:target="_blank"}, in the future, there may be other ways to break disk encryption on devices by using quantum computing. [Nashilov (2020)]( https://www.kaspersky.com/blog/quantum-computing-vs-data-encryption/36301/){:target="_blank"} speculates that although AES-256 may be quantum-resistant, most symmetric ciphers are not. Although in practical terms, this would remain out of reach for most practitioners and be expensive, it would be reserved for national-security level investigations. It means that in current cases where investigators have been unable to break encryption by existing means, the data will be crackable in future. 

# Conclusion
This report discussed new techniques in physical data acquisition and data analysis in digital forensics. For example, sifting collectors can improve acquisition speed by up to fourteen times while still finding 95% of evidence compared to traditional p techniques. The report also discussed the use of cloud computing to accelerate the speed of analysis using an open-source forensic compute cluster called DFORC2 and how AI techniques for automating parts of the forensic process can also be used to speed up investigations. There was also discussion regarding the challenges of IoT and data stored in cloud servers across the world being inaccessible to law enforcement and how the US government has helped solve the issue by introducing the [CLOUD Act](https://en.wikipedia.org/wiki/CLOUD_Act){:target="_blank"}. This section also discussed the problem of the ubiquity of encryption and how quantum computing may be able to crack symmetric encryption in the future. 


# References

Box, J. (2020, 6 May). _How the CLOUD Act will affect the way cloud providers serve their customers_. International Association of Privacy Professionals. https://iapp.org/news/a/how-the-cloud-act-will-affect-the-way-cloud-providers-serve-their-customers/

Evans, C. (2019, 26 June). _Dude, Where's my 100TB Hard Drive?_ Architecting IT. https://www.architecting.it/blog/dude-wheres-my-100tb-hard-drive/

Garland, J. (2021, 14 July). _Australia Passes Cross-Border Data Access Law, Creates a Pathway for CLOUD Act Bilateral Agreement_. Inside Privacy. https://www.insideprivacy.com/cross-border-transfers/australia-passes-cross-border-data-access-law-creates-a-pathway-for-cloud-act-bilateral-agreement/

Lillis, D., Becker, B. A., O'Sullivan, T., & Scanlon, M. (2016, April). _CURRENT CHALLENGES AND FUTURE RESEARCH AREAS FOR DIGITAL FORENSIC INVESTIGATION_. School of Computer Science, University College Dublin. https://arxiv.org/pdf/1604.03850.pdf

Nashilov, E. (2020, 13 July). _Quantum computers and cryptography for dummies_. Kapersky. https://www.kaspersky.com/blog/quantum-computing-vs-data-encryption/36301/

Nield, D. (2020, 29 January). _How to Get the Most Out of Your Smartphone's Encryption_. Wired. https://www.wired.com/story/smartphone-encryption-apps/

Novak, M., Grier, J., & Gonzales, D. (2019). New Approaches to Digital Evidence Acquisition and Analysis. _National Institute of Justice_, _280_, 1–8. https://www.ojp.gov/pdffiles1/nij/250700.pdf