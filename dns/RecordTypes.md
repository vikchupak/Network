# Common DNS Record Types

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

# MX RECORDS

An **MX (Mail Exchanger) record** tells the world **which mail servers are responsible for receiving email for a domain**.

If someone sends email to **user@example.com**, the sender looks up the **MX records** of `example.com` to know where to deliver the message.

---

# 🔹 What MX Records Contain

An MX record has **two main parts**:

| Field                     | Meaning                                 |
| ------------------------- | --------------------------------------- |
| **Priority (Preference)** | Numeric value (lower = higher priority) |
| **Mail server hostname**  | Domain name of mail server              |

> MX records **must point to a hostname**, never directly to an IP.

✅ Good

```
example.com.   MX   10   mail1.example.com.
```

❌ Invalid

```
example.com.   MX   10   192.168.1.10
```

Because the server must have A or AAAA record(s) resolving its name to IP.

---

# 🔹 Priority

Lower number = higher priority.
Senders try lowest first. If unreachable → next.

Example:

```
example.com.   MX   10   primary.example.com.
example.com.   MX   20   backup.example.com.
example.com.
```

Meaning:

1. Try `primary`
2. If down, try `backup`

If several MX have equal priority → random selection.

---

# 🔹 Typical Workflow (How email arrives)

1. Mail server looks up MX of `example.com`
2. Pick server with lowest priority number
3. Resolve A / AAAA record of that hostname
4. Connect using SMTP (port 25)
5. Deliver message

# 🔹 Example MX Listing

```
example.com.  MX  1   ASPMX.L.GOOGLE.COM.
example.com.  MX  5   ALT1.ASPMX.L.GOOGLE.COM.
example.com.  MX  5   ALT2.ASPMX.L.GOOGLE.COM.
example.com.  MX 10   ALT3.ASPMX.L.GOOGLE.COM.
```

- Primary → `ASPMX`
- Secondaries → `ALT*`
