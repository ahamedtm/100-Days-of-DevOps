# 100-Days-of-DevOps
Master the Most In-Demand DevOps Tools, the Hands-On Way from kodekloud

# **Project Nautilus**

## **Overview**

**Project Nautilus** is the Naval subdivision of **xFusionCorp Industries**. The Nautilus application assists Naval forces in making smart procurement decisions for both manned and unmanned maritime systems while ensuring operational requirements are met. It aims to provide best-in-class operational support, improve safety, extend the life of existing machines, and reduce the overall cost of ownership.

---

## **Current Repertoire**

- **Sonar Technology and Systems**  
- **LUSV - Large Unmanned Surface Vehicles**  
- **Autonomous Unmanned Undersea Pods**  
- **Nuclear Submarines**  
- **vLaser Guidance Systems**  
- **Application Architecture**




---

## **Deployment Architecture**

The Nautilus application follows a **three-tier architecture** and is deployed in the **Stratos Datacenter**, located in the **North America Region**.

> [Nautilus project deployment architecture can be viewed here](https://lucid.app/lucidchart/58e22de2-c446-4b49-ae0f-db79a3318e97/edit?shared=true&page=0_0#)
> 
### **1. Data Tier**

- Stores data and manages retrieval and execution operations.
- Uses **MariaDB**, a popular open-source relational database.

### **2. Application Tier**

- Based on the **LAMP** stack:
  - **Linux** operating system
  - **Apache** HTTP Server
  - **MariaDB** (as a MySQL-compatible DBMS)
  - **PHP** for server-side scripting

### **3. Client Tier**

- The web browser acts as the client application.
- Processes and displays HTML resources.
- Issues HTTP requests and handles HTTP responses.

### **Load Balancer**

- **Nginx** is used for HTTP load balancing to distribute requests across multiple application servers.

---

## **Shared Services**

- **Storage Filer:** NAS (Network Attached Storage) is used for reliable and stable external storage for application tier servers.  
- **SFTP Server:** SSH File Transfer Protocol is used for secure file transfers between remote systems.  
- **Backup Server:** Staging backup system for short-term archival.  
- **Jump Server:** An intermediary SSH gateway to securely access the remote network hosting the Nautilus application.

---

## **Infrastructure Details**

- **Storage Filer:** NAS (Network Attached Storage) is used for reliable and stable external storage for application tier servers.  
- **SFTP Server:** SSH File Transfer Protocol is used for secure file transfers between remote systems.  
- **Backup Server:** Staging backup system for short-term archival.  
- **Jump Server:** An intermediary SSH gateway to securely access the remote network hosting the Nautilus application.

# Nautilus Server Information

| Server Name   | IP            | Hostname                          | User    | Password   | Purpose                        |
|:--------------|:--------------|:----------------------------------|:--------|:-----------|:-------------------------------|
| stapp01       | 172.16.238.10 | stapp01.stratos.xfusioncorp.com   | tony    | Ir0nM@n    | Nautilus App 1                 |
| stapp02       | 172.16.238.11 | stapp02.stratos.xfusioncorp.com   | steve   | Am3ric@    | Nautilus App 2                 |
| stapp03       | 172.16.238.12 | stapp03.stratos.xfusioncorp.com   | banner  | BigGr33n   | Nautilus App 3                 |
| stlb01        | 172.16.238.14 | stlb01.stratos.xfusioncorp.com    | loki    | Mischi3f   | Nautilus HTTP LBR              |
| stdb01        | 172.16.239.10 | stdb01.stratos.xfusioncorp.com    | peter   | Sp!dy      | Nautilus DB Server             |
| ststor01      | 172.16.238.15 | ststor01.stratos.xfusioncorp.com  | natasha | Bl@kW      | Nautilus Storage Server        |
| stbkp01       | 172.16.238.16 | stbkp01.stratos.xfusioncorp.com   | clint   | H@wk3y3    | Nautilus Backup Server         |
| stmail01      | 172.16.238.17 | stmail01.stratos.xfusioncorp.com  | groot   | Gr00T123   | Nautilus Mail Server           |
| jump_host     | Dynamic       | jump_host.stratos.xfusioncorp.com | thor    | mjolnir123 | Jump Server to Access Stork DC |
| jenkins       | 172.16.238.19 | jenkins.stratos.xfusioncorp.com   | jenkins | j@rv!s     | Jenkins Server for CI/CD       |

