---
published: true

layout: post

title: Introducing MXMaven, A tool for identifying poorly configured mail server DNS records

image: /images/jeremy-cai-unsplash.jpg

categories: [Phishing, Cybersecurity, Code, ]

---

_I wrote a small tool in python for scanning DNS mail records that can help organisations prevent domain impersonation attacks commonly used in phishing attacks._

![koi fish]({{ site.baseurl }}/images/jeremy-cai-unsplash.jpg "help organisations protect their mail servers from impersonation attacks used in phishing") 
_Photo by [Jeremy Cai](https://unsplash.com/@j)_   



# Introducing MXMaven: A Cybersecurity Tool to Secure Your Email Domains

### Why MXMaven?

Large organisations often manage hundreds of domains. A single misconfiguration in one of these domains can be a goldmine for threat actors. They can exploit these vulnerabilities to impersonate your domain, sending phishing emails that appear to come from your organisation. That's where MXMaven comes in. 

MXMaven quickly identifies poorly or misconfigured MX, SPF, and DMARC records in DNS, which can leave a domain susceptible to domain impersonation attacks. It also detects MX records that do not resolve, potentially causing mail delivery issues or even leaving dangling DNS records vulnerable to take-over[^1]. Furthermore, MXMaven checks SPF and DMARC records for compliance with RFC standards, ensuring they do not exceed the 255-character limit for TXT records, which can cause mail services to ignore them.

MXMaven provides a terminal report highlighting poorly configured domains. By storing all the DNS results in a datastore it also means more sophisticated reports can be created, as well as tracking of historical DNS changes. 

### How to Get Started

For details on installation and usage, visit the [MXMaven GitHub repo](https://github.com/nkavadias/mxmaven).

## Understanding SPF Records

SPF (Sender Policy Framework) records prevent spammers and phishers from sending emails with forged “From” addresses using your domain. An SPF record is a [DNS TXT record](https://www.cloudflare.com/learning/dns/dns-records/dns-txt-record/) that specifies which IP addresses or hostnames are authorised to send emails on behalf of your domain. 

When an email reaches the receiving server, it looks up the SPF record to check if the email comes from an authorised source. Based on the SPF policy, the server decides how to handle emails from unauthorised sources:

- **Hard Fail (-all)**: Strictly rejects emails from unauthorised sources. Recommended for business domains.
- **Soft Fail (~all)**: Marks emails from unauthorised sources as spam.
- **Neutral (?all)**: Ignores the SPF check. Not recommended for business domains.
- **Pass (+all)**: Accepts emails from any source. This weak setting is not recommended.

If the SPF record is not set, the server defaults to a neutral setting.

MXMaven reports domains with no SPF policy, a neutral policy (warning), or a pass policy (bad) and stores the entire SPF record in the SPFRecord table.

## Understanding DMARC Records

DMARC (Domain-based Message Authentication, Reporting, and Conformance) adds another layer of email authentication. A DMARC policy instructs the receiving server on handling emails that fail SPF and DKIM checks. DKIM (DomainKeys Identified Mail) uses cryptographic keys to verify email sources, but MXMaven does not check DKIM records as it requires sending an email from the domain.

A DMARC record, a DNS TXT record, defines the following policies:

- **NONE**: Takes no action on emails failing SPF and DKIM checks.
- **REJECT**: Rejects emails failing SPF and DKIM checks. Recommended for high-security domains.
- **QUARANTINE**: Marks emails failing checks as suspicious, placing them in quarantine or spam.

DMARC also supports reporting back to the domain owner about authentication results. MXMaven stores this part of the record in the DMARCRecord table.

## 255-Character Limit on DNS TXT Strings

According to [RFC 1035 section 2.3.4](https://datatracker.ietf.org/doc/html/rfc1035#section-2.3.4), a single DNS TXT record string cannot exceed 255 bytes. Longer records must be divided into multiple strings, each within the 255-byte limit. While some providers like Google and Microsoft may accept longer records, exceeding this limit can cause authentication failures and email delivery issues.

MXMaven checks if TXT records comply with this limit and stores the results in the SPFRecord and DMARCRecord tables.

[^1]: [Reed, J.A. and Reed, J.C., 2020. Potential Email Compromise via Dangling DNS MX.](https://www.dnsinstitute.com/research/dangling-mx/dangling-mx-202007.pdf)
