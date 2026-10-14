Topology
- HQ: HQ-core (192.168.10.1) - HQ-Edge (10.0.0.2 / 203.0.113.2)
- BR1: PC4 Network (192.168.30.0/24)
- ISP: 203.0.113.1/30
- Servers: HQ-Server 192.168.10.10 , DNS/HTTP 192.168.10.12

Problem
- PC4 could not ping ISP (203.0.113.1)
- PC4 could not ping DNS/HTTP (192.168.10.12)
- HQ-core interfaces down (Gig0/1, Fa0/8-24)

Solution
1.HQ-Edge
cisco
ip route 0.0.0.0 0.0.0.0 203.0.113.1
ip route 192.168.10.0 255.255.255.0 10.0.0.1
ip route 192.168.30.0 255.255.255.0 10.10.10.2
2.ISP
ip route 192.168.10.0 255.255.255.0 203.0.113.2
ip route 192.168.30.0 255.255.255.0 203.0.113.2
ip route 10.0.0.0 255.255.255.252 203.0.113.2
ip route 10.10.10.0 255.255.255.252 203.0.113.2
3.BR1 & BR2
ip route 0.0.0.0 0.0.0.0 10.10.10.1
ip route 0.0.0.0 0.0.0.0 10.10.10.5
4.HQ-core & Switch1
int range gig0/1-2
 no shutdown
int range fa0/1-24
 no shutdown
Verification
PC4> ping 192.168.10.12 -> 0% loss
PC4> ping 203.0.113.1 -> 0% loss
PC4> ping 203.0.113.2 -> 0% loss
Proof: See screenshots in /screenshots

Author
Your Name - Yohan Kavishka

bash
git init
git add .
git commit -m "Fix: PC4 to ISP and DNS/HTTP connectivity - DONE"
git branch -M main
git remote add origin https://github.com/Yohan Kavishka/ccna-packet-tracer-pc4-isp-dns.git
git push -u origin main
