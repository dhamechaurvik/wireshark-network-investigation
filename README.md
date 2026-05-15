## 🔍 Wireshark Display Filters Used

| File | Filter | Purpose |
|------|--------|---------|
| 01_dns.txt | `dns` | Capture all DNS queries and responses |
| 02_http.txt | `http` | Capture unencrypted HTTP traffic |
| 03_icmp.txt | `icmp` | Capture ping requests and replies |
| 04_tcp_syn.txt | `tcp.flags.syn == 1` | Detect new connection attempts |
| 05_tcp_reset.txt | `tcp.flags.reset == 1` | Detect rejected connections |

## 📊 Findings Summary

### DNS Traffic
- Captured domain resolution requests to google.com, github.com, youtube.com
- DNS queries sent to local resolver then forwarded to upstream DNS server
- All queries used UDP port 53

### HTTP Traffic
- Captured unencrypted GET requests to example.com and neverssl.com
- Plaintext data visible in packet payload
- Demonstrates risk of using HTTP over HTTPS

### ICMP Traffic
- Captured ping requests and replies to 8.8.8.8 (Google DNS)
- Round trip time visible in each packet
- Used to confirm network connectivity

### TCP SYN
- Captured TCP three-way handshake initiation
- SYN packets show new connection attempts to web servers
- Useful for detecting port scanning behavior

### TCP Reset
- Captured RST packets showing rejected connections
- High volume of RST packets can indicate port scanning or firewall activity

## 🚨 Suspicious Activity Detection

| Indicator | What to Look For | Risk Level |
|-----------|-----------------|------------|
| Excessive DNS queries | Same IP querying many domains | Medium |
| HTTP credentials | Plaintext username/password in HTTP | High |
| TCP RST flood | Many rejected connections from one IP | High |
| Unknown DNS servers | DNS queries to non-standard IPs | Medium |

## 🛡️ Mitigation Recommendations
- Always use HTTPS instead of HTTP
- Use encrypted DNS (DNS over HTTPS)
- Monitor for excessive TCP RST packets
- Block ICMP on public-facing interfaces

## 📸 Screenshots
See screenshots/ folder for all Wireshark filter results.

## ⚠️ Disclaimer
This project is for educational purposes only.
All traffic captured is from my own machine on my own network.