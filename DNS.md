- Authoritative Name Servers (NS) - servers that host Zone Files
- Zone Files - text files with DNS records
- A DNS Zone is served by a set of one or more Authoritative Name Servers (NS)

- Registrar - A company accredited by ICANN (or a local authority) to sell and manage domain names to the public (the consumer). **Domain seller**. Manages the domain on your behalf.
- Registrant - is the individual or organization that holds the rights to use the domain name - cutomer. **Domain buyer/owner**.
- Registry - The organization that operates the database for all domain names under a specific Top-Level Domain (TLD), such as .com, .org, or .net.

---

### Hostname Subdomain vs Delegated Subdomain

- `blog.example.com.` - blog - Hostname Subdomain
- `static.example.com.` - static - Hostname Subdomain
- `hr.example.com.` - hr - Delegated Subdomain

## The DNS Zone Hierarchy

- Top Level Domain (TLD)
- Secondary Level Domain (SLD)

| Zone Level | Example | Administrator | Key Role in DNS |
| :--- | :--- | :--- | :--- |
| **1. Root Zone** | **`.`** (the dot) | ICANN/IANA | The top-most zone; contains the authoritative NS records for all TLDs. |
| **2. TLD Zone** | **`.com`** | Registry (e.g., Verisign) | Contains the authoritative NS records for all Second-Level Domains (SLDs) within that TLD. |
| **3. SLD Zone** | **`example.com`** | The Domain Owner (Registrant) | The primary administrative zone; contains the **Host Records** (A, CNAME) and potentially **NS records** for any delegations. |
| **4. Delegated Sub-Zone** | **`hr.example.com`** | A Separate Administrator/Team | An entirely **independent zone** created when the SLD owner places NS records into the SLD zone, transferring administrative control of that part of the namespace. |

- Hostname Subdomain points/resolves to the naked domain (They are in the same SLD Zone).
  - `CNAME www example.com.` > www.example.com and example.com > resolves to the same IP
  - `CNAME blog example.com.` > blog.example.com and example.com > resolves to the same IP
  - `CNAME static other.domain.com.` > static.example.com resoves to another IP, but it is still Hostname subdomain, not delegated.
- Delegated Subdomain points/resolves to other IPs
  - NS hr ns1.hrvendor.com. > points to delegate Authoritative NS that "create" another Zone > resolves to another IP

### The Parent Zone File: `example.com`

| Record Type | Host | Value | Purpose |
| :--- | :--- | :--- | :--- |
| **A** | `www` | `192.0.2.10` | Standard A record for the main website. |
| **NS** | `@` | `ns1.examplehost.com.` | Authoritative servers for the main `example.com` zone. |
| **NS** | `@` | `ns2.examplehost.com.` | |
| **NS** | **`hr`** | **`ns1.hrvendor.com.`** | **DELEGATION:** These NS records delegate the authority for `hr.example.com` to a new server set. |
| **NS** | **`hr`** | **`ns2.hrvendor.com.`** | |

The **`hr` NS records** above tell the world that the `example.com` zone is no longer responsible for answering queries for `hr.example.com`—it has passed that job to the servers at `ns1.hrvendor.com` and `ns2.hrvendor.com`.

### The Delegated Zone File: `hr.example.com`

| Record Type | Host | Value | Purpose |
| :--- | :--- | :--- | :--- |
| **SOA** | `@` | ... | Declares the Start of Authority for the **new `hr.example.com` zone**. |
| **NS** | `@` | `ns1.hrvendor.com.` | The servers that are authoritative for this new HR zone. |
| **NS** | `@` | `ns2.hrvendor.com.` | |
| **A** | **`@`** | `198.51.100.20` | Defines the IP for the main HR homepage (`hr.example.com`). |
| **A** | **`benefits`** | `198.51.100.21` | Defines the IP for a sub-subdomain (`benefits.hr.example.com`). |
