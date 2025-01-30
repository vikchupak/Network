- The entire **127.0.0.0/8** range is reserved for loopback addresses.
- That means that any request sent to **127.x.x.x** **never leaves** the local machine — it always refers to itself.

List all loopback addresses
```bash
# IPv4 + IPv6
ip addr show dev lo

# IPv4
ip -4 addr show dev lo

# IPv6
ip -6 addr show dev lo
```

By default, some addresses may not be assigned to your machine. You can manually add them as a loopback alias
```bash
sudo ip addr add 127.0.0.42/32 dev lo
```

If you added more loopback IPs (e.g., 127.0.0.42), they would also appear under `inet` entries. You can list all loopback IPs using
```bash
ip addr show dev lo
```
