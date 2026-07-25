# OSINT & Surface Reconnaissance Report

| Field | Detail |
| --- | --- |
| Prepared by | Mohit Kumar |
| Programme | Growfinix Cybersecurity Internship |
| Task | Task 1 — OSINT and Surface Reconnaissance |
| Target | `tesla.com` |
| Collection type | Passive public-information review |
| Collection record | 25 July 2026 (see screenshots and local collection outputs) |

## Executive summary

This exercise demonstrates a responsible reconnaissance workflow using only public registration, DNS, certificate-transparency, and passive DNS-indexing sources. The collection observed a distributed delivery footprint, Microsoft 365 MX routing, SPF and third-party verification TXT entries, and public hostname/alias records returned by passive sources.

No intrusive testing was performed. The observations are not vulnerabilities and were not actively validated.

## Objective

To understand how publicly available Internet records can be collected, documented, and interpreted during the reconnaissance phase of a cybersecurity assessment without interacting with target services beyond standard public DNS and data-source queries.

## Scope and safety boundary

**In scope:** public WHOIS, public DNS resolution, DNS records, and results returned by passive third-party indexes.

**Out of scope:** port/vulnerability scanning, endpoint enumeration, authentication attempts, exploitation, brute force, credential collection, social engineering, and verification of individual hosts.

## Tools and sources

| Tool / source | Purpose | Evidence |
| --- | --- | --- |
| WHOIS | Review public registrar and name-server metadata. | `whois.txt` (local raw record) |
| `nslookup` | Resolve public address records. | `nslookup.txt` (local raw record) |
| `dig` | Review A, MX, TXT, and SOA/ANY responses. | `dns.txt`, [Screenshots/](Screenshots/) |
| theHarvester + CRT.sh | Query a passive certificate-transparency source. | `harvester-crtsh.txt` (local raw record) |
| theHarvester + CertSpotter | Query a passive certificate source. | `harvester-certspotter.txt` (local raw record) |
| theHarvester + RapidDNS | Query a passive DNS index. | `harvester-rapiddns.txt` (local raw record) |

> Raw `.txt` output is intentionally excluded from the public repository. It is retained locally as supporting evidence and may contain volatile or sensitive operational detail.

## Methodology

1. Queried public WHOIS data for registration and name-server metadata.
2. Collected DNS address-resolution and MX/TXT/SOA information using standard recursive DNS queries.
3. Queried CRT.sh, CertSpotter, and RapidDNS through theHarvester, limiting results where applicable.
4. Recorded terminal output through screenshots and retained raw outputs locally.
5. Reported results as time-bound observations and avoided active validation of any discovered hostname.

See [COMMANDS.md](COMMANDS.md) for the command reference.

## Results

| Area | Observation | Interpretation |
| --- | --- | --- |
| Registration and delegation | WHOIS output identified MarkMonitor as registrar and listed Akamai/UltraDNS name servers. | Indicates an externally managed domain-registration and authoritative-DNS posture; this does not imply a security issue. |
| Address resolution | A and translated IPv6 responses showed multiple public addresses. | Consistent with a distributed delivery or CDN-backed architecture. No origin inference was attempted. |
| Email routing | MX records indicated Microsoft 365 mail routing. | Mail is routed through a common enterprise email platform; routing information alone is not a weakness. |
| TXT records | SPF and multiple third-party domain-verification entries were present. | These are typical for email-policy enforcement and SaaS ownership verification. They should be maintained as part of normal DNS hygiene. |
| Certificate transparency | CRT.sh returned no hosts in this collection; CertSpotter returned one wildcard entry. | Results vary across data sources and time. A wildcard certificate is not evidence that every matching host exists or is active. |
| Passive DNS | RapidDNS returned 89 publicly indexed hostname/alias records. | Passive-index results should be reconciled against an approved inventory; they do not establish current ownership, availability, or authorisation. |
| Person/email results | theHarvester summaries returned no email addresses or people for the selected sources. | No conclusions about the organisation's personnel or exposure should be drawn from this limited result set. |

## Evidence index

| Evidence | Content |
| --- | --- |
| [command1.png](Screenshots/command1.png) | `dig tesla.com ANY` response, including SOA information. |
| [command2.png](Screenshots/command2.png) | Captured terminal evidence. |
| [command3.png](Screenshots/command3.png) | Captured terminal evidence. |
| [command4.png](Screenshots/command4.png) | Captured terminal evidence. |
| [command5.png](Screenshots/command5.png) | Captured terminal evidence. |
| [Command6.png](Screenshots/Command6.png) | `dig tesla.com TXT` response. |

## Recommendations

1. Maintain an authorised external-asset inventory covering public subdomains, DNS records, certificates, and third-party integrations.
2. Periodically reconcile passive-DNS and certificate-transparency results with that inventory; investigate only within an approved security-testing scope.
3. Remove stale DNS records, unneeded verification strings, and unused third-party integrations through change-controlled processes.
4. Separate development, test, and production assets; ensure non-production systems are not unintentionally exposed through public DNS.
5. Continue enforcing MFA, SPF/DKIM/DMARC, and routine email-security controls.

## Limitations

- Public data is incomplete, source-specific, and changes over time.
- DNS and certificate records do not prove that a service is live, reachable, owned, misconfigured, or exploitable.
- No active validation was performed, so the exercise cannot determine service state or vulnerability.
- This was an educational point-in-time collection, not a penetration test or comprehensive external attack-surface assessment.

## Conclusion

The exercise demonstrates that passive OSINT can provide useful context for asset inventory and DNS hygiene while respecting a strict non-intrusive boundary. The appropriate next step in a real engagement would be to reconcile observations with an approved asset inventory and obtain explicit written authorisation before any validation activity.
