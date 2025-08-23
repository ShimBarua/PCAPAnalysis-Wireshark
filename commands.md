# Commands run on the Analyst VM (Kali). Start Wireshark capture first and let it run for a couple minutes.  
Replace 192.168.235.129 (Target IP) and 192.168.235.128 (Analyst IP) with relevant IPs.  
129 is target IP and 128 is Analyst IP for easy readability.  

# — ARP and ICMP —
Flush ARP cache to force an ARP request, then ping once (generates ARP and ICMP)  
sudo ip neigh flush all  
ping -c 1 192.168.235.129  

## A couple more pings for ICMP examples  
ping -c 2 192.168.235.129  

# — HTTP (plaintext) —
curl -v http://192.168.235.129/  

# — FTP (plaintext credentials) —
If ftp client is missing: sudo apt update && sudo apt install -y inetutils-ftp  
ftp 192.168.235.129  
When prompted:  
Name (username): msfadmin  
Password: msfadmin  
Then at the ftp> prompt:  
ls  
quit  

# — Telnet (plaintext session) —
If telnet is missing: sudo apt install -y telnet  
telnet 192.168.235.129  
When prompted:  
login: msfadmin  
Password: msfadmin  
Then run commands:  
whoami  
uname -a  
exit  

# — SMB (list shares) —
If smbclient is missing: sudo apt install -y smbclient  
smbclient -L //192.168.235.129/ -N  

# — TCP 3‑way handshake example —
Any new TCP connection will have a 3 way handshake.  
curl -v http://192.168.235.129/  

# Stop the Wireshark capture and save as a .pcapng
