# Task Report: OSINT and Surface Reconnaissance

**Student:** Mohit Kumar  
**Internship:** Growfinix Cybersecurity Internship  
**Task:** Task 1 - Open Source Intelligence (OSINT) and Surface Reconnaissance

## Objective

To understand how publicly available Internet records can be collected and interpreted during the reconnaissance phase of a cybersecurity assessment.

## Tools used

| Tool | Purpose |
| --- | --- |
| WHOIS | Review public registration and name-server metadata |
| nslookup | Resolve publicly available DNS addresses |
| dig | Review DNS MX, TXT, and SOA records |
| theHarvester | Aggregate passive results from public certificate and DNS-indexing sources |

## Methodology

1. Reviewed public WHOIS information.
2. Collected DNS address-resolution, MX, TXT, and SOA information.
3. Used passive certificate and DNS-indexing sources in theHarvester.
4. Preserved screenshots and local raw output as evidence.
5. Interpreted findings without active validation.

## Findings

- DNS resolution showed distributed network infrastructure.
- MX records indicated Microsoft 365 mail-routing infrastructure.
- TXT records included SPF and third-party domain-verification entries.
- CRT.sh returned no hosts during this collection.
- CertSpotter returned one wildcard certificate entry.
- RapidDNS returned 89 publicly indexed hostname/alias records.
- No email addresses or people were returned in theHarvester result summaries for the selected sources.

## Analysis

Public DNS records, wildcard certificates, and third-party domain-verification records are normal elements of an organisation's Internet-facing presence. They are not vulnerabilities on their own and do not prove that a related service is active, owned, misconfigured, or exploitable.

## Recommendations

1. Maintain an approved inventory of public subdomains and DNS records.
2. Remove stale DNS entries and unused third-party service integrations.
3. Review certificate-transparency records periodically.
4. Keep development and test environments separated from production exposure.
5. Continue enforcing MFA and strong email-security controls.

## Conclusion

This task demonstrated a responsible passive OSINT workflow. Routine DNS hygiene and external asset inventory help organisations understand their public exposure without requiring intrusive testing.
