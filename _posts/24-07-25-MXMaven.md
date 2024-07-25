---
published: false

layout: post

title: MXMaven: A tool to identify poorly configured DNS records for mail servers

image: /images/conny-schneider-3hkKv6WzjcE-unsplash.jpg

categories: [Phishing, Cybersecurity, Code, ]

---

_A python tool I wrote for scanning DNS records for mail servers that helps organisations prevent domain impersonation attacks in phishing._

![digital gavel]({{ site.baseurl }}/images/conny-schneider-3hkKv6WzjcE-unsplash.jpg "Cyberwarfare and Cyberterrorism") 
_Photo by [Conny Schneider](https://unsplash.com/@choys_)_   



#  MXMaven: A tool to identify poorly configured DNS records for mail servers and help prevent domain impersonation attacks
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

## Tool Capabilities

MX Maven can check a single domain using the -s parameter.  Although, it has a more power option of accepting a text file with a domain on each line with the -m parameter.  All DNS record lookups are stored in a relation database, this defaults to SQLite3, but can be easily reconfigured to use MySQL, PosgresSQL and CockroachDB, as it uses the Peewee Python ORM library.


MXMaven has three options to run the tool. The first option is `-s` or `--single`, which checks a single domain. The second option is `-m` or `--multidomain`, which accepts a text file with a domain on each line. The third option is `-a` or `--showall`, which prints a report of all stored records. The tool stores all DNS record lookups in a relation database, which defaults to SQLite3. However, it can be easily reconfigured to use MySQL, PosgresSQL, and CockroachDB, as it uses the Peewee Python ORM library.

Here are the details of the options:

| **Option** | **Description**                                                                  |
|------------|-----------------                                                                 |
| `-h`, `--help` | Shows the help message and exits.                                            |
| `-s DOMAIN_NAME`, `--single DOMAIN_NAME` | Runs the tool in single domain mode.                |
| `-m DOMAIN_NAME_LIST.TXT`, `--multidomain DOMAIN_NAME_LIST.TXT` | Runs the tool in multiple domain mode. Accepts a text file with a domain on each line. |
| `-a`, `--showall` | Prints a report of all stored records. |
| `-v`, `--verbose` | Increases output verbosity. |
| `-d SQLITE3_DB_FILE.DB`, `--sqlitedb SQLITE3_DB_FILE.DB` | Uses an alternative Sqlitedb. The default is mxmaven.db. |


## Project TODOs
- implement multiprocessing or multithreading for DNS lookups.
- Do additional checks to identify dangling MX records such records which point to domains no longer registered or parked, or public cloud hostnames which are not responding (may be possible for takeover?)
- inspect authorized hosts in SPF which are too broad and could allow any sending from a third party to impersonate domain (e.g. generic SendGrid hosts, or large IP ranges).
- additional tool parameter to allow easy export to csv, JSON of table records from SQLite.
- record and save TLS certificates for mail servers that support secure transport.

[1]:[Reed, J.A. and Reed, J.C., 2020. Potential Email Compromise via Dangling DNS MX.](https://www.dnsinstitute.com/research/dangling-mx/dangling-mx-202007.pdf)