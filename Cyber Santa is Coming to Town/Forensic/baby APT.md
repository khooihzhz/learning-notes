# Baby APT 
- Forensics (Wireshark) PCAP file
- Points : 300 Pts

### Filtering with http

![[Pasted image 20211202213301.png]]

At first, filter out the http packets as the TCP packets does not show anything useful.

![[Pasted image 20211202213356.png]]

Keep checking each packet content, and we find an interesting string that looks like base64 encoded

### Decoding Base64

>SFRCezBrX24wd18zdjNyeTBuM19oNHNfdDBfZHIwcF8wZmZfdGgzaXJfbDN0dDNyc180dF90aDNfcDBzdF8wZmYxYzNfNGc0MW59

Decoding it using [cyberchef](https://gchq.github.io/CyberChef/#recipe=From_Base64('A-Za-z0-9%2B/%3D',true)&input=U0ZSQ2V6QnJYMjR3ZDE4emRqTnllVEJ1TTE5b05ITmZkREJmWkhJd2NGOHdabVpmZEdnemFYSmZiRE4wZEROeWMxODBkRjkwYUROZmNEQnpkRjh3Wm1ZeFl6TmZOR2MwTVc1OQ)

Flag : HTB{0k_n0w_\*\*\*\*_4g41n}