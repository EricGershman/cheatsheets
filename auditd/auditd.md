#General Auditd
Auditd is the Userspace component of the Linux Auditing System.

#Auditd Cheat Sheet 
##Commands
###auditd
Run in the foreground:```auditd -f```


"A boot param of audit=1 should be added to ensure that all processes that run before the audit daemon starts is marked as auditable by the kernel. "
- [Auditd Man Page] [auditd_man]

###auditctl
"auditctl program is used to control the behavior, get status, and add or delete rules into the 2.6 kernel’s audit system."
- [Auditctl Man Page] [auditctl_man]

###aureport 
##Setup 

##Rules
“audit rules come in 3 varieties: control, file, and syscall”
  * Control - “configuring the audit system”
  * File - “audit access to particular files or directories”
  * Syscall - “loaded into a matching engine that intercepts each syscall”
```
-a action list: always log on syscall exit
-F field 
-S syscall: execve
-k Logging Key: programs
```
```bash
-a always,exit -F arch=b32 -F uid=33 -S execve -k programs -k www
-a always,exit -F arch=b64 -F uid=33 -S execve -k programs -k www
-a exit,always -S unlink -S rmdir
-a exit,always -S stime.*
-a exit,always -S setrlimit.*
-w /var/www -p wa
-w /etc/group -p wa
-w /etc/passwd -p wa
-w /etc/shadow -p wa
-w /etc/sudoers -p wa
```
- [audit.rules Man Page] [audit.rules_man]

##OSSEC
https://github.com/ossec/ossec-hids/blob/6eb2d4dce24688c675de3202f21a925b0b7501f9/etc/decoder.xml#L2414

#Links
[auditd_man]: http://linux.die.net/man/8/auditd  "Auditd Man Page"
[auditctl_man]: http://linux.die.net/man/8/auditctl  "Auditctl Man Page"
[audit.rules_man]: http://linux.die.net/man/7/audit.rules  "audit.rules man page"
