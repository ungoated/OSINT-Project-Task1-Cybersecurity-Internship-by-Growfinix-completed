# Command Reference

> Use these commands only against domains you own or are explicitly authorised to assess. This project used them for a passive, academic review of public records.

## Public registration and DNS

| Command | Purpose | Notes |
| --- | --- | --- |
| `whois tesla.com` | Reviews public domain registration, registrar, and name-server metadata. | Results are registry/registrar data and may be redacted or stale. |
| `nslookup tesla.com` | Resolves publicly available IPv4 and IPv6 addresses. | Address resolution does not identify an origin system or prove a service is active. |
| `dig tesla.com A` | Retrieves public IPv4 address records. | Captured in the local DNS output. |
| `dig tesla.com MX` | Retrieves public mail-exchange records. | Used to observe publicly advertised mail routing. |
| `dig tesla.com TXT` | Retrieves TXT records, including SPF policy and domain-verification entries. | TXT records should be interpreted in context; they are not vulnerabilities by default. |
| `dig tesla.com ANY` | Requests an ANY response. | Modern authoritative DNS services often minimise ANY answers; this collection returned SOA information. |

## Passive OSINT sources

| Command | Passive source | Purpose |
| --- | --- | --- |
| `theHarvester -d tesla.com -b crtsh -l 50` | CRT.sh | Queries public certificate-transparency data. |
| `theHarvester -d tesla.com -b certspotter -l 50` | CertSpotter | Queries a public certificate-transparency source. |
| `theHarvester -d tesla.com -b rapiddns -l 50` | RapidDNS | Queries a public passive-DNS index. |

## theHarvester options

| Option | Meaning |
| --- | --- |
| `-d` | Target domain. |
| `-b` | Public data source to query. |
| `-l 50` | Limits returned results to 50 where the source supports the limit. |

## Interpretation guardrails

- A hostname returned by a passive source is not proof that it is current, reachable, owned by the target, or authorised for testing.
- Certificate and DNS data are snapshots and can differ across sources and collection times.
- Do not extend these commands into port scanning, endpoint enumeration, login attempts, or vulnerability testing without written authorisation.
