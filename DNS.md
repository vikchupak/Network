- Authoritative Name Servers (NS) - servers that host Zone Files
- Zone Files - text files with DNS records
- A DNS Zone is served by a set of one or more Authoritative Name Servers (NS)

- Registrar - A company accredited by ICANN (or a local authority) to sell and manage domain names to the public (the consumer). **Domain seller**. Manages the domain on your behalf.
- Registrant - is the individual or organization that holds the rights to use the domain name - cutomer. **Domain buyer/owner**.
- Registry - The organization that operates the database for all domain names under a specific Top-Level Domain (TLD), such as .com, .org, or .net.

---

### Hostname Subdomain vs Delegated Subdomain

- `hr.example.com.` - hr - Delegated Subdomain
- `blog.example.com.` - blog - Hostname Subdomain

## The DNS Zone Hierarchy

- Top Level Domain (TLD)
- Secondary Level Domain (SLD)

| Zone Level | Example | Administrator | Key Role in DNS |
| :--- | :--- | :--- | :--- |
| **1. Root Zone** | **`.`** (the dot) | ICANN/IANA | The top-most zone; contains the authoritative NS records for all TLDs. |
| **2. TLD Zone** | **`.com`** | Registry (e.g., Verisign) | Contains the authoritative NS records for all Second-Level Domains (SLDs) within that TLD. |
| **3. SLD Zone** | **`example.com`** | The Domain Owner (Registrant) | The primary administrative zone; contains the **Host Records** (A, CNAME) and potentially **NS records** for any delegations. |
| **4. Delegated Sub-Zone** | **`hr.example.com`** | A Separate Administrator/Team | An entirely **independent zone** created when the SLD owner places NS records into the SLD zone, transferring administrative control of that part of the namespace. |
