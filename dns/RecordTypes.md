### **Common DNS Record Types**

| Type              | Name                                | Purpose                                   |
| ----------------- | ----------------------------------- | ----------------------------------------- |
| **SOA**           | Start of Authority                  | Zone info: primary NS, admin, serial      |
| **A**             | Address                             | Maps hostname → IPv4 address              |
| **AAAA**          | IPv6 Address                        | Maps hostname → IPv6 address              |
| **CNAME**         | Canonical Name                      | Alias → another hostname                  |
| **MX**            | Mail Exchanger                      | Mail delivery server                      |
| **NS**            | Name Server                         | Delegates to authoritative DNS servers    |
| **TXT**           | Text                                | Metadata (SPF, verification, etc.)        |
| **DNSSEC RRSIG**  | RRSIG                               | DNSSEC signature                          |
| **DNSSEC DNSKEY** | DNSKEY                              | DNSSEC public keys                        |
| **DNSSEC DS**     | Delegation Signer                   | Delegation chain security                 |
