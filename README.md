# PCAPAnalysis-Wireshark

This Repository documents a hands-on network traffic analysis lab using Wireshark on Kali Linux against a vulnerable VM (e.g., Metasploitable). It captures and explains core protocols such as ARP, ICMP, HTTP, FTP, Telnet, SMB, plus a TCP handshake. You'll find commands, display filters, PCAPS, and screenshots from the lab. The goal is to demonstrate practical packet analysis, highlight the risks of plaintext (FTP/Telnet), and provide a clean, repeatable workflow.

-Role: SOC Analyst  
-Lab hosts: Analyst (Kali) 192.168.235.128 > Target VM 192.168.235.129  
-Deliverables: PCAPS, protocol screenshots, filters, commands, analysis report.  

## Protocols Captured
-ARP, ICMP, HTPP, FTP, Telnet, SMB  
-TCP handshake example  
-Notes include: MAC/IP mappings, HTTP headers, plaintext credentials  

## What I Learned
-How to isolate conversations and interpret protocols  
-Risks of plaintext protocols and the need for encryption  
-Practical Wireshark capture  

## Safety
This lab runs in an isolated environment; DO NOT scan or attack hosts you do not own.
