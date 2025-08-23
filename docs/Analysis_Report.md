# Lab — Network Traffic Analysis on Wireshark

Short summary: Captured ARP, ICMP, HTTP, FTP, Telnet, SMB, and a TCP 3‑way handshake between an Analyst VM and a vulnerable VM. Documented evidence (screenshots), key fields, and quick takeaways.

## Lab Info
- Date: 08-23-2025
- Analyst IP: 192.168.235.128
- Target IP: 192.168.235.129
- Network: Host only
- Capture file: msf2_Lab.pcapng
- Tooling: Wireshark Version 4.4.7

## How to Reproduce 
1) Start Wireshark on the host‑only interface and begin capture.
2) Run the commands in commands.txt (same order).
3) Use filters to isolate each protocol.
4) Save capture

---

## Findings by Protocol

### ARP
- Display filter: arp
- Evidence:
- Notes:
  - Request: “Who has 192.168.235.129? Tell 192.168.235.128”
  - Shows MACs for analyst and target.

### ICMP (Ping)
- Command: ping -c 2 <Target_VM_IP>
- Display filter: icmp
- Evidence:
- Notes:
  - Real Time Text from the Echo reply field.
  - Echo request ID/seq numbers match reply.

### HTTP (plaintext)
- Command: curl -v http://192.168.235.129/
- Display filter: http or http.request
- Evidence: 
- Notes:
  - Server header: <e.g., Apache>
  - Any Set-Cookie or interesting paths.

### FTP (plaintext credentials)
- Command sequence: ftp 192.168.235.129 → USER msfadmin → PASS msfadmin
- Display filter: ftp
- Evidence: 
- Notes:
  - Credentials visible in plaintext.

### Telnet (plaintext session)
- Command: telnet 192.168.235.129 → login: msfadmin/msfadmin → whoami; uname -a; exit
- Display filter: telnet or tcp.port == 23
- Evidence:
- Notes:
  - Keystrokes and prompts readable (unencrypted).

### SMB
- Command: smbclient -L //192.168.235.129/ -N
- Display filter: smb || smb2 || nbss
- Evidence: 
- Notes:


### TCP 3‑Way Handshake
- Example connection: HTTP to 192.168.235.129:80
- Evidence:
- Notes:
  - SYN starts, SYN/ACK responds, ACK completes.

---

## Statistics
- Protocol Hierarchy (Wireshark: Statistics → Protocol Hierarchy): 
- Conversations → TCP tab: 

## Key Takeaways
- Plaintext protocols (FTP/Telnet) expose credentials and shows the importance of encryption
- Wireshark filters and conversation views make it easy to isolate packets and understand what is happening.
- SMB negotiation reveals protocol version and auth context.

## Appendix
- Display filters used: see filters/display_filters.txt
- Commands run: see commands.txt
- Capture metadata: see docs/pcap_metadata.txt
