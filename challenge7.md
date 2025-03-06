**Challenge: Bastion**
A Bastion Host is a hardened server designed to regulate access to a private network. However, if misconfigured, it can serve as an entry point for attackers to infiltrate internal systems. This exercise involves identifying vulnerabilities such as misconfigurations, weak authentication, and exposed services that could lead to unauthorized access.

**Steps to Identify and Secure a Bastion Host**
1. Locate the Bastion Host
• Identify public IP addresses within the network.
• Conduct a full port scan to discover open services:
  nmap -sV -p-
• Pay close attention to critical services such as:
  - SSH (Port 22)
  - RDP (Port 3389)
2. Assess SSH Access
• If SSH is open, check for weak or default credentials:
  hydra -L users.txt -P passwords.txt ssh://<target>
• Review .ssh/authorized_keys for improperly configured access permissions.
3. Evaluate Privilege Escalation Risks
• Identify commands that can be executed with administrative privileges:
  sudo -l
• Look for stored private keys in directories such as:
  /home
  /etc/ssh/
• Search configuration files for hardcoded credentials.
4. Explore Internal Network Access
• If the bastion host has network access to internal systems, identify available connections:
  ip a
  netstat -rn
• Utilize SSH proxying to pivot into internal resources:
  ssh -D 1080 user@target

**Conclusion**
A poorly secured bastion host can be exploited as an entry point into a private network. Enforcing strict security controls and continuous monitoring is essential to prevent unauthorized access and maintain network integrity.
