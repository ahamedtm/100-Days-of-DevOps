## **System Administrator Task List**

### **Day 01 - Create a Linux User with Non-Interactive Shell**

The System Admin team of xFusionCorp Industries has installed a backup agent tool on all app servers. As per the tool's requirements, they need to create a user with a non-interactive shell.

**Task:**  
Create a user named `javed` with a non-interactive shell on the `stapp02` server.

**Example Workflow:**

```bash
thor@jumphost ~$ ssh tony@stapp01
tony@stapp01's password:
[tony@stapp01 ~]$
[tony@stapp01 ~]$ sudo useradd --shell /bin/false javed
[sudo] password for tony:
[tony@stapp01 ~]$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
...
javed:x:1002:1002::/home/javed:/bin/false
[tony@stapp01 ~]$
```

> Replace `javed` with `username` and ensure the task is done on `givenapp` server.

## Task 02 - Create Temporary User with Expiry Date

As part of the temporary assignment to the Nautilus project, a developer named **ravi** requires access for a limited duration. To ensure smooth access management, a temporary user account with an expiry date is needed.

**Requirement:**
- Create a user named `ravi` on **App Server 2** in **Stratos Datacenter**.
- Set the expiry date to **2024-03-28**.
- Ensure the username is lowercase as per standard protocol.

**Steps:**
```bash
thor@jumphost ~$ ssh steve@stapp02
steve@stapp02's password: 

[steve@stapp02 ~]$ sudo useradd -e 2024-03-28 ravi
[sudo] password for steve: 

[steve@stapp02 ~]$ sudo chage -l ravi
Last password change                                    : Aug 11, 2025
Password expires                                        : never
Password inactive                                       : never
Account expires                                         : Mar 28, 2024
Minimum number of days between password change          : 0
Maximum number of days between password change          : 99999
Number of days of warning before password expires       : 7
```

---

## Task 03 - Disable Direct Root SSH Login

Following security audits, the **xFusionCorp Industries** security team has rolled out new protocols, including the restriction of direct root SSH login.

**Requirement:**
- Disable direct root SSH login on **all app servers** in the Stratos Datacenter.

**Steps:**

**App Server 1**
```bash
thor@jumphost ~$ ssh tony@stapp01
tony@stapp01's password: 

[tony@stapp01 ~]$ sudo vi /etc/ssh/sshd_config
[sudo] password for tony: 

[tony@stapp01 ~]$ sudo service sshd restart
Redirecting to /bin/systemctl restart sshd.service

[tony@stapp01 ~]$ sudo grep -i permitrootlogin /etc/ssh/sshd_config
PermitRootLogin no
# the setting of "PermitRootLogin without-password".
logout
Connection to stapp01 closed.
```

**App Server 2**
```bash
thor@jumphost ~$ ssh steve@stapp02
steve@stapp02's password: 

[steve@stapp02 ~]$ sudo vi /etc/ssh/sshd_config
[sudo] password for steve: 

[steve@stapp02 ~]$ sudo service sshd restart
Redirecting to /bin/systemctl restart sshd.service

[steve@stapp02 ~]$ sudo grep -i permitrootlogin /etc/ssh/sshd_config
PermitRootLogin no
# the setting of "PermitRootLogin without-password".
```

**App Server 3**
```bash
[steve@stapp02 ~]$ ssh banner@stapp03
banner@stapp03's password: 

[banner@stapp03 ~]$ sudo vi /etc/ssh/sshd_config
[sudo] password for banner: 

[banner@stapp03 ~]$ sudo service sshd restart
Redirecting to /bin/systemctl restart sshd.service

[banner@stapp03 ~]$ sudo grep -i permitrootlogin /etc/ssh/sshd_config
PermitRootLogin no
# the setting of "PermitRootLogin without-password".
```

# Task 04 - Grant Executable Permissions

In a bid to automate backup processes, the xFusionCorp Industries sysadmin team has developed a new bash script named `xfusioncorp.sh`. While the script has been distributed to all necessary servers, it lacks executable permissions on **App Server 2** within the **Stratos Datacenter**.

**Objective:**  
Grant executable permissions to `/tmp/xfusioncorp.sh` on App Server 2, ensuring all users can execute it.

### Steps:

```bash
thor@jumphost ~$ ssh steve@stapp02
steve@stapp02's password:
[steve@stapp02 ~]$ sudo chmod 755 /tmp/xfusioncorp.sh
[sudo] password for steve:
[steve@stapp02 ~]$ ls -l /tmp/xfusioncorp.sh
-rwxr-xr-x 1 root root 40 Aug 11 05:19 /tmp/xfusioncorp.sh
[steve@stapp02 ~]$

```

# Task 05 - SELinux Installation & Configuration

Following a security audit, the xFusionCorp Industries security team has decided to enhance application and server security with SELinux. For App Server 3 in the Stratos Datacenter, the following requirements were set:

**Objective:**  
- Install the required SELinux packages.

- Permanently disable SELinux (for now; it will be re-enabled after configuration changes).

- No reboot required immediately (a scheduled maintenance reboot will happen tonight).

- The SELinux status after the reboot should be disabled.

### Steps:

```bash
thor@jumphost ~$ ssh banner@stapp03
banner@stapp03's password:
[banner@stapp03 ~]$ sudo yum install -y selinux-policy-targeted policycoreutils
[sudo] password for banner:
# [Installation output ]
[banner@stapp03 ~]$ sudo vi /etc/selinux/config
# Change the line to:
SELINUX=disabled
[banner@stapp03 ~]$ grep ^SELINUX= /etc/selinux/config
SELINUX=disabled

```
## Task 06 - Testing Cron Job Deployment on All App Servers

The Nautilus system admins team has prepared scripts to automate several day-to-day tasks.  
They want them to be deployed on all app servers in Stratos DC on a set schedule.  
Before that, they need to test similar functionality with a sample cron job.  

### Requirements
1. **Install `cronie` package** on all Nautilus app servers and start the `crond` service.
2. **Add a cron job** for the `root` user to run every 5 minutes:


---

### Implementation Steps

```bash
thor@jumphost ~$ ssh tony@stapp01
tony@stapp01's password: 
[tony@stapp01 ~]$ sudo yum install -y cronie
[sudo] password for tony: 
[tony@stapp01 ~]$ sudo systemctl start crond
[tony@stapp01 ~]$ sudo systemctl enable crond
[tony@stapp01 ~]$ sudo crontab -e
# (added the cron job)
[tony@stapp01 ~]$ sudo crontab -l
*/5 * * * * echo hello > /tmp/cron_text
logout

thor@jumphost ~$ ssh steve@stapp02
steve@stapp02's password: 
[steve@stapp02 ~]$ sudo yum install -y cronie
[sudo] password for steve: 
[steve@stapp02 ~]$ sudo systemctl start crond
[steve@stapp02 ~]$ sudo systemctl enable crond
[steve@stapp02 ~]$ sudo crontab -e
# (added the cron job)
[steve@stapp02 ~]$ sudo crontab -l
*/5 * * * * echo hello > /tmp/cron_text
logout

thor@jumphost ~$ ssh banner@stapp03
banner@stapp03's password: 
[banner@stapp03 ~]$ sudo yum install -y cronie
[sudo] password for banner: 
[banner@stapp03 ~]$ sudo systemctl start crond
[banner@stapp03 ~]$ sudo systemctl enable crond
[banner@stapp03 ~]$ sudo crontab -e
# (added the cron job)
[banner@stapp03 ~]$ sudo crontab -l
*/5 * * * * echo hello > /tmp/cron_text

