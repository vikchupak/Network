# Mac Sequoia

```bash
sudo dscacheutil -flushcache; sudo killall -HUP mDNSResponder
```

# Chrome

- chrome://net-internals/#dns
  - Clear host cache
- chrome://net-internals/#sockets
  - Flush socket pools
