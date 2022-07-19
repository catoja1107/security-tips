# AD Security Tips
## 1. Basics
### 1(a). General Analysis Approach:
<p align="center"><img src="https://preview.redd.it/xegh56kbrk751.png?width=679&format=png&auto=webp&s=178918de96031d24292c15c8cc34f2163b70f84b" alt="CIA Triad"></p>

>Security is a careful balance of Confidentiality, Accessibility, and Integrity. Data needs to be properly secured and authenticated with the ability of users to read and write to it in mind. 
- <a href="https://nvlpubs.nist.gov/nistpubs/CSWP/NIST.CSWP.04162018.pdf">NIST Cybersecurity Framework v1.1</a>
  - Risk-based analysis of current, and desired cyber readiness
- <a href="https://www.lockheedmartin.com/content/dam/lockheed-martin/rms/documents/cyber/Gaining_the_Advantage_Cyber_Kill_Chain.pdf">Lockheed Martin Cyber Kill Chain</a>
  - Prevent and Identify cyber threats

### 1(b). Securing from the start!
- Design with security in mind
  - Only enable the services REQUIRED for function and efficiency.
    - Disable outdated SMB versions such as 1.0/2.0
    - Please for the love of God, use an openssh server instead of telnet. (and autoupdate to stable!)
  - Super-segment the network!
    - Create specific, yet roomy subnets and vlans for host categorization.
  - Follow the principles of least-privilege!
    - Don't give users, groups, or hosts more privileges than needed.
  - When services are enabled, ensure necessary management and mitigation
    - Whitelist IP adresses or MAC adapter IDs!
      - A jumpbox would work well for centralized access.
    - Change the default TCP/UDP port to perhaps an ephemeral port, preferably higher range.
  - Patch, patch, patch!
    - Centrally manage Windows updates, properly configure WSUS, or choose a provider such as ManageEngine.

- Monitoring in the middle!
  - Monitor core gateway
    - When the location goes live, begin IDS/IPS learning mode for usual traffic.
    - Tune log alerts, point them to a syslog-ng server or centralized SIEM server for best practice.
  - Monitor subnets/vlans
    - Add a tap and enable port mirroring
      - Steer clear of tagging the mirror port as trunk, add taps per vlan tag
  - Monitor hosts
    - Configure EventViewer to capture desired event codes
      - Good practice would be audit failures, as well as enabled services such as SSH/FTP/etc
    - Go a step further with sysmon
      - Monitor suspicious apps/actions based on strings, hash, or other attributes as preference dictates.
  - Monitor assets
    - Configure an ITAM, such as LanSweeper

- Training tackles threats!
  - Testing and Training users
    - Phish test to prepare users for potential threats
      - Create HTML5 emails, make users want to click that link!
    - Train using open-source or paid resources
      - The basics of "check the link, check the sender"
    - A step further... (with approval)
      - Scatter rubberducky USB flashdrives around the workplace
        - Train users not to plug in unapproved hardware!
      - Perform spearphishing 
      - Perform pentesting

## 2. Advanced
### <a href="https://docs.microsoft.com/en-us/sysinternals/">2(a). Sysinternals</a>
- Use it? <a href="https://web.archive.org/web/20220719184857/https://www.reddit.com/r/sysadmin/comments/vbczi9/how_to_prevent_abuse_of_psexec_on_your_network/">Secure it!</a>

>PSEXEC is a curse and a blessing. It makes management of assets much easier, however it is a cult classic for delivering payloads such as reverse shells, as well as for executing malicious commands. Ensure it is secured, as well as any admin$ SMB shares. Log executions and consolidate to a centralized log server. The syntax is provided below for reference.
```
psexec [\\computer[,computer2[,...] | @file]][-u user [-p psswd][-n s][-r servicename][-h][-l][-s|-e][-x][-i [session]][-c executable [-f|-v]][-w directory][-d][-<priority>][-a n,n,...] cmd [arguments]
```
## TBC!
