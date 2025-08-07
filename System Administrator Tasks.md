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
