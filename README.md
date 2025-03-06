I started my project by analyzing the target system using Nmap to scan for open ports. The scan revealed two active services: SSH on port 22 and HTTP on port 80.

Next, I explored the web server, examining its structure and content. Using ffuf, I performed a directory brute-force scan and discovered several interesting files and folders, including /static/00, where I found developer notes.

The notes mentioned a hidden path: /dev1243224123123, which led me to a login page. While analyzing the page source code, I found a dev.js file containing login credentials. Using these credentials, I gained access to the internal system, where I discovered references to an FTP server. After rescanning all ports, I identified an FTP service running on a non-standard port: 37370.

Connecting to the FTP server, I downloaded several PCAP files, which I analyzed using Wireshark. In one of the files, I found login credentials for the user valleyDev, which allowed me to access the system via SSH.

During the privilege escalation phase, I examined the file system and discovered an executable called valleyAuthenticator. By analyzing it with strings, I extracted password hashes, which I successfully cracked to gain access to the valley account.

To escalate privileges further, I modified the base64.py standard library by injecting code to create a reverse shell. This allowed me to gain root access, successfully completing the project and achieving all objectives.
