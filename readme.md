WonderCMS Vulnerability Exploit Walkthrough
Initial Foothold
Directory Enumeration
Starting from the /themes endpoint, we performed directory enumeration and found an interesting sub-directory: /bike (HTTP 301 Redirect).

bash
Copy code
URL: sea.htb/themes/bike/
Theme Files and CRM Information
In the /bike/ directory, we discovered the following files, which revealed details about the WonderCMS theme and version:

Contents of readme.md
The readme.md file provided information on the CRM software version and theme details:

CRM Version: 3.2.0
Theme Name: WonderCMS bike theme
Author: turboblack
Based on this information, we found an exploit for this version:

Exploit: CVE-2023-41425 - WonderCMS Remote Code Execution (RCE)
By following the exploit steps, we successfully gained a reverse shell with www-data privileges.

Privilege Escalation
Within the /data directory, we found database.js, containing a password hash for a user. The password was stored in bcrypt format, and backslashes had to be removed to use it correctly.

Steps Taken:
Accessed /data/database.js.
Extracted the bcrypt password hash.
Removed backslashes as required to obtain the usable password.
SSH Forwarding
Using the discovered credentials, we performed SSH forwarding to maintain access.

Useful Commands and Evidence
Network Activity: netstat -auntp
SSH Evidence: Screenshots provided below.
Screenshots
Directory Enumeration
CRM Information (readme.md)
SSH Forwarding
Network Activity
Additional Evidence
For full details, including a step-by-step exploitation process, refer to the screenshots in this repository.