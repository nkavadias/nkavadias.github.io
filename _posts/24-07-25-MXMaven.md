---
published: false

layout: post

title: Introducing MXMaven, A tool for identifing poorly configured mail server DNS records

image: /images/jeremy-cai-unsplash.jpg

categories: [Phishing, Cybersecurity, Code, ]

---

_A python tool I wrote for scanning DNS mail records that helps organisations prevent domain impersonation attacks in phishing._

![digital gavel]({{ site.baseurl }}/images/jeremy-cai-unsplash "help organisations protect their mailservers from impersonation attacks used in phishing") 
_Photo by [Conny Schneider](https://unsplash.com/@choys_)_   



#  Why MXMaven?
#### Description:
Large organisations can have hundreds of domains. A threat actor may use a single misconfiguration in one of these domains to their advantage. MXMaven can identify poorly or misconfigured MX, SPF and DMARC records in DNS that may leave a domain susceptible to domain impersonation attacks (i.e. using your domain identity to send phishing emails to victims impersonating your organisation.) MXMaven will also find MX records that do not resolve, which could lead to mail delivery issues or, worse, be a dangling DNS record that could be vulnerable to take-over[^1]. MX Maven can detect SPF and DMARC records that do not comply with RFC standards for strings longer than 255 characters in TXT records. This issue can cause mail services to ignore long SPF and DMARC records. MX Maven will store all DNS lookups for MX, SPF and DMARC in a SQLite database and will provide a report after scanning to highlight poorly configured SPF and DMARC policies or MX resolution issues.

### What is a SPF Record?

SPF (Sender Policy Framework) records prevent spammers and phishers from sending emails with forged “From” addresses using your domain. An SPF record is a [DNS TXT record](https://www.cloudflare.com/learning/dns/dns-records/dns-txt-record/) that specifies a list of IP addresses or hostnames that are authorized to send emails on behalf of your domain. When an email reaches the receiving server, it will look up the DNS SPF record and check to determine if the email comes from an authorized IP address. The server will follow the policy set in the SPF record on how to handle an incoming email from an unauthorized IP.

Four types of SPF policies specify how receiving mail servers should handle emails that fail the SPF check :

- Hard Fail (-all): This is the strictest policy recommended for domains hosting business emails where a threat actor may seek to impersonate people in the organization. Any mail server sending email will be rejected unless it is on the authorized list of servers in the SPF record.

- Soft Fail (~all): If the email is not from an authorized server, the receiving mail server should mark the email as spam.

- Neutral (?all): The receiving mail server should not use the SPF record to verify the email. This policy is not recommended for business domains.

- Pass (+all): The receiving mail server should pass the email even if the email is not from an authorized server. This is the weakest setting and is not recommended.

If the SPF record is not set, the receiving mail server will consider this the neutral setting.

MXMaven will report on domains it finds where the SPF policy is not set, is set to neutral (as a warning, in yellow) and as bad (in red) if the policy is set to pass. MXMaven does not report rules for authorized servers but stores the entire SPF record in the SPFRecord table.

## What is a DMARC Record?
DMARC stands for Domain-based Message Authentication, Reporting, and Conformance. It is an additional method to SPF used for authenticating email messages. A DMARC policy tells a receiving email server what to do after checking a domain’s SPF and DKIM  records. DKIM is Domain Keys Identified Mail. It is an additional verification that relies on cryptographic keys embedded in email messages to verify the source mail server) records. MX Maven does not check DKIM records. To do so would require an email sent from the domain being checked.

A DMARC record is also a DNS TXT record that stores a domain’s DMARC policy. The DMARC policy instructs the receiving mail server on how to treat a message that fails SPF and DKIM verification. The policies are:

- NONE: If the email fails the SPF and DKIM checks, the receiving mail server will not take additional actions.

- REJECT: If the email fails the SPF and DKIM checks, the receiving mail server should reject the email. This is the strictest policy recommended for domains where a threat actor may seek to impersonate people in your organization.

- QUARANTINE: If the email fails the SPF and DKIM checks, the receiving mail server should mark it as suspicious and quarantine the email or mark it as spam.

DMARC also enables reports to be sent back to the domain owner about messages authenticating. MX Maven does not report on this part of the record but stores it in the DMARCRecord table.

## 255 char limit on DNS TXT strings
According to [RFC 1035 section 2.3.4](https://datatracker.ietf.org/doc/html/rfc1035#section-2.3.4). A single string in a DNS TXT record cannot exceed 255 bytes, but a single record is allowed to contain multiple strings. For records longer than 255 bytes the record should be divided into 255 byte Strings with quotation mark (") and separate each Strings by space.

There are reports that Google and Microsoft may obey SPF records that exceed 255 characters. However, it is not recommended and Google's own documentation states that and exceeding this character limit can cause authentication failure and lead to email delivery issues.
The MXMaven report will indicate is TXT_length_OK for each domain SPF/DMARC record and the result check is stored on the SPFRecord and DMARCRecord tables.


[1]:[Reed, J.A. and Reed, J.C., 2020. Potential Email Compromise via Dangling DNS MX.](https://www.dnsinstitute.com/research/dangling-mx/dangling-mx-202007.pdf)