# Malware Traffic Analysis Report

## Lab Overview
- **Source:** malware-traffic-analysis.net
- **PCAP Name:** 2026-01-31-traffic-analysis-exercise.pcap
- **Date Analyzed:** 2/5/26
- **Analyst:** Connor Beard
- **Tools Used:** Wireshark

## Objective
Answer:
1. What is the IP address of the infected Windows client?
2. What is the MAC address of the infected Windows client?
3. What is the host name of the infected Windows client?
4. What is the user account name from the infected Windows client?
5. What is the full name of the user from the user account?
6. What is the domain from 153.92.1[.]49 that triggered the alert for Lumma Stealer?

---
## Background
-- An analyst at a SOC finds a signature hit for "ET MALWARE Lumma Stealer Victim Fingerprinting Activity" that triggered on traffic from 153.92.1[.]49 over TCP port 80. 




## Environment
- Host OS: Windows 11 Home
- Wireshark Version:
- Analysis Type: Passive PCAP Analysis

---

## Initial Observations
- Capture duration: 10 minutes, 23 seconds
- Total packets: 51181
- Notable protocols observed: TCP,HTTP, and TLS. THe host 10.1.21.58 has multiple TCP connections to 153.92.1.49, indicating possible malware infection.
- Immediate red flags: There is only 1 IP that the triggered IP communicated with. 

---

## Traffic Analysis
1. What is the IP address of the infected Windows client?

For this question, my first thought was to filter by the given IP and see what IP addresses made connections to it. 
![Screenshot 1](<screenshots/Screenshot 2026-02-05 222224.png>)
From the screenshot, you can see that the only IP address contacting the given IP is 10.1.21.58

Answer: 10.1.21.58

2. What is the MAC address of the infected Windows client?

For this question, my first thought is just inspecting one of the packets shown and looking at the Ethernet details to find the MAC address.
![Screenshot 2](<screenshots/image.png>)
From here, you can see that the source MAC address is 00:21:5d:c8:0e:f2

Answer: 00:21:5d:c8:0e:f2

3. What is the host name of the infected Windows client?

To be honest, I was pretty stuck on this question. When looking through the traffic for the infected IP address, I just could not find the hostname, so I decided to research what protocol I could filter by to find the hostname. After some searching, I decided to try filtering by DHCP (Dyanamic Host Configuration Protocol) which essentially assigns devices an IP address.

![Screenshot 3](<screenshots/image-1.png>)

As you can see, there are only 4 packets here. After looking through just the 1st packet, I finally found the host name.

![Screenshot 4](<screenshots/image-2.png>)

The host name is highlighted DESKTOP-ES9F3ML, and we can confirm that by looking at the client MAC address listed as the correct MAC address.

Answer: DESKTOP-ES9F3ML

4. What is the user account name from the infected Windows client?

For this one I was stumped. I was going through filter after filter trying to find the user account name. Unfortunately, I again had to do some research and a quick google search told me when trying to identify Windows user accounts, Kerberos is a good protocol to start with. After filtering for Kerberos, I was left with 64 packets. The first 2 packets are LDAP packets, so I ignored those and went to the 3rd packet which was the 1st Kerberos packet. A quick look into the cname tab and I had found my username.
![Screenshot 5](<screenshots/image-3.png>)

Answer: gwyatt

5. What is the full name of the user from the user account?

For this question, since we already had the username as "gwyatt", I decided to use the find feature to look for the full name. I filtered the find to (Packet details, string, "Wyatt", case sensitive) to look through all the packets and to find one that had "Wyatt" to see if I could get the full name. Lo and behold, I found my name in packet 39556.
![Screenshot 6](<screenshots/image-3.png>)

Answer: Gabriel Wyatt

6. What is the domain from 153.92.1[.]49 that triggered the alert for Lumma Stealer?

For this step, I was thinking about how I would go about this for a long time. Eventually, I just decided to filter by the source IP and for either http requests, TLS client hello, and DNS. There was 352 packets displayed, with majority of them being DNS packets. I quickly had to go into a DNS packet and add the name of the host as a column so it would be very easy to go through all of these domain names. The first one that caught my eye was "whitepepper.su". 
![Screenshot 7](<screenshots/image-5.png>)
As you can see in this screenshot, the first "whitepepper.su" query comes at 23:05:36.218945. To further confirm if this is the correct domain, I filtered by the IP of the attacker to see if the first connection comes right after the query to "whitepepper.su".
![Screenshot 8](<screenshots/image-4.png>)
As you can see, the first connection to the attackers IP comes right after the query to the whitepepper domain, which solidifies my suspicions.

Answer: whitepepper.su



## Conclusion

Thank you for reading my traffic analysis of this lab, this is my first one and my further labs will only be more detailed and thorough. 

-Connor Beard

---

