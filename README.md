# How to Schedule Windows Server Backups to a NAS Device?
This documentation provides a step-by-step guide to implementing reliable backups from Windows Server 2019 to a networked NAS device using built-in tools.

 
 
## Table of Contents

1. [System Overview](#1-system-overview)  
2. [NAS Configuration](#2-nas-configuration)  
3. [Windows Server 2019 Preparation](#3-windows-server-2019-preparation)  
4. [Backup Configuration on Windows Server 2019](#4-backup-configuration-on-windows-server-2019)  
5. [Conclusion](#5-conclusion)

---

## 1. System Overview

| Component               | Details               |
|-------------------------|------------------------|
| **NAS IP Address**      | `192.168.1.100`        |
| **Server IP Address**   | `192.168.1.10`         |
| **User Account**        | `sysadmin`             |
| **Password**            | `Pa@ssW0rd@11`         |

> **Note:** The `sysadmin` user and password are consistent across both the NAS and Windows Server environments.

---

## 2. NAS Configuration

### 2.1 Create User Account

- **Username:** `sysadmin`  
- **Password:** `Pa@ssW0rd@11`

### 2.2 Create Shared Folder

- **Folder Name:** `serverbackupcollection`

### 2.3 Assign Permissions

- Share the folder `serverbackupcollection` with the `sysadmin` user.
- Grant **Read/Write** permissions to allow backup operations.

---

## 3. Windows Server 2019 Preparation

### 3.1 Create Matching User Account

- **Username:** `sysadmin`  
- **Password:** `Pa@ssW0rd@11`

### 3.2 Test Network Connectivity

Open **Command Prompt** and run:

```bash
ping 192.168.1.100
````

Ensure successful replies are received.

### 3.3 Verify NAS Folder Access

1. Open **File Explorer**.
2. In the address bar, enter:

   ```
   \\192.168.1.100\serverbackupcollection
   ```
3. Press **Enter**.
4. Confirm write access by creating a test folder named `192.168.1.10`.

   * If successful, you have appropriate permissions.

---

## 4. Backup Configuration on Windows Server 2019

### 4.1 Launch Windows Server Backup

1. Open the **Start Menu** and search for **Windows Server Backup**.
2. Launch the application.

### 4.2 Start Backup Schedule Wizard

1. In the left pane, select **Local Backup**.
2. In the right pane, click **Backup Schedule**.
3. On the Getting Started screen, click **Next**.

### 4.3 Select Backup Configuration

* Choose **Full Server (recommended)**.
* Click **Next**.

### 4.4 Schedule the Backup

* Select **Once a day**.
* Set the backup time to **9:00 PM**.
* Click **Next**.

### 4.5 Set Backup Destination

* Choose **Back up to a shared network folder**.
* Confirm the warning message by clicking **OK**.

### 4.6 Enter Network Path

* In the path field, input:

  ```
  \\192.168.1.100\serverbackupcollection
  ```
* Click **Next**.

### 4.7 Provide Credentials

* **Username:** `sysadmin`
* **Password:** `Pa@ssW0rd@11`
* Click **OK**.

### 4.8 Finalize Configuration

* Click **Finish** to complete the setup.
* A confirmation message will appear:

  > *Status: You have successfully created the backup schedule.*
* Click **Close**.

---

## 5. Conclusion

The scheduled backup is now configured. **Windows Server 2019** will automatically perform a daily backup to the designated **NAS folder** at **9:00 PM**.

### Best Practices:

* Ensure the NAS is powered on and accessible at all times.
* Regularly monitor backup logs for any errors or failures.
* Verify sufficient storage is available on the NAS.


---

 
