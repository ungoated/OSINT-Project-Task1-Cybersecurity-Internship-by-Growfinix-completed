# Commands Used

> These commands were used only for passive, publicly available OSINT collection.

| Command | Description |
| --- | --- |
| `whois tesla.com` | Displays public domain registration, registrar, and name-server information. |
| `nslookup tesla.com` | Resolves the domain to publicly available IPv4 and IPv6 addresses. |
| `dig tesla.com MX` | Retrieves mail-exchange records to identify public email-routing information. |
| `dig tesla.com TXT` | Retrieves TXT records, including SPF policy and domain-verification entries. |
| `dig tesla.com ANY` | Requested an ANY response; this DNS server returned SOA information only, which is common on modern DNS services. |
| `theHarvester -d tesla.com -b crtsh -l 50` | Queries the CRT.sh passive certificate source. |
| `theHarvester -d tesla.com -b certspotter -l 50` | Queries the CertSpotter passive certificate source. |
| `theHarvester -d tesla.com -b rapiddns -l 50` | Queries the RapidDNS passive DNS index. |

## theHarvester options

- `-d` specifies the target domain.
- `-b` specifies the public data source.
- `-l 50` limits returned results to 50 where applicable.
