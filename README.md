# pfSense Firewall / Router

## Introduction to pfSense & Squid Proxy

pfSense is a powerful open-source firewall and router based on FreeBSD. It provides advanced network security features, including packet filtering, VPN, NAT, and intrusion prevention. In this lab, pfSense plays the role of our perimeter firewall, giving us visibility into inbound/outbound network traffic and policy enforcement. Alongside pfSense, we are also deploying the Squid Proxy package.

![pfsense1](https://github.com/user-attachments/assets/09971112-5574-4bcd-be11-33c45294ddc9)

### Why We Need pfSense + Squid Proxy

In a SOC environment, visibility is everything. Firewalls and proxies are some of the primary data sources analysts rely on to detect threats. Here’s why they are important for our lab:

- Acts as the first line of defense between the internal lab network and external traffic.
- Provides logs of allowed and denied connections, NAT, and VPN activity.
- Helps detect unauthorized access attempts, port scans, and traffic patterns that could indicate attacks.
- When integrated with Splunk, pfSense firewall logs give us network context to correlate with IDS (Suricata) and NDR (Zeek) data.

### Squid Proxy (Web Proxy & Caching)
- Monitors and logs HTTP/HTTPS requests, showing what users (or attackers) are accessing online.
- Enables content filtering (blocking malicious domains, file types, or categories).
- Provides URL-level visibility, which firewall logs alone cannot give.
- Essential for detecting command-and-control (C2) traffic, data exfiltration attempts, or suspicious web browsing.

### Combined Value

By having both:

***pfSense*** = “Who is connecting where on the network?”

***Squid Proxy*** = “What content is being accessed on the web?”

![squid-proxy](https://github.com/user-attachments/assets/a14941a9-0a17-45a7-b26e-9fc3168cab74)

---

### Setting UP Splunk Universal Forwarder:

Change into the forwarder binary, switch to the splunkforwarder user, start it, and accept the license. I set the username to admin and a secure password. 

![splunkfwd-user](https://github.com/user-attachments/assets/4b38f012-f86a-44ee-9e08-9b12887fe10f)

### Point this UF to the Splunk indexer

![splunkfwd-indexer](https://github.com/user-attachments/assets/804592e5-2180-42b3-8ac5-98672472f0e0)

# Splunk Inputs Configuration

In the directory ```/opt/splunk/etc/system/local/```, the ```inputs.conf``` file will be configured manually, unlike outputs.conf and ```server.conf```, which are usually present. However, we will configure ```inputs.conf``` to specify how our logs will be forwarded to Splunk.

![splunkinputs-conf](https://github.com/user-attachments/assets/92b094af-c845-49b3-9067-bec809a7f06a)

### Pfsense Log Query Overview

![pfsense-splunk](https://github.com/user-attachments/assets/4ff4ac01-cd03-463f-a018-23aa2e37ba0c)









