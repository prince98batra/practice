# SOP: Managing Cron Jobs on Ubuntu

## 👤 **Author Information**
| **Author** | **Created on** | **Version**  | **Comment** | **Reviewer** |
|------------|----------------|--------------|-------------|--------------|
| **Prince Batra**   | **14-04-2025**   | **Version 1.1** | **Internal review** | **Siddharth Pawar** |
| **Prince Batra**   | **14-04-2025**   | **Version 1.1** | **L0 review** | **Shikha** |
---

## 📑 Table of Contents

  - [1. Introduction](#1-introduction)
  - [2. What is cron, crontab and cronjob?](#2-what-is-cron-crontab-and-cronjob)
  - [3. Cron Syntax Format](#3-cron-syntax-format)
  - [4. Prerequisites](#4-prerequisites)
  - [5. Creating, Viewing, Removing and Editing Cron Jobs](#5-creating-viewing-removing-and-editing-cron-jobs)
  - [6. Check System Cron Logs](#6-check-system-cron-logs)
  - [7. System & Directory-Based Cron Jobs](#7-system--directory-based-cron-jobs)
  - [8. Example Cron Jobs for Common Use Cases](#8-example-cron-jobs-for-common-use-cases)
  - [9. References](#9-references)
  - [10. Contact Information](#contact-information)

---

## 1. Introduction
Cron is a time-based job scheduler in Unix-like operating systems. This SOP provides step-by-step instructions for creating, editing, managing, and troubleshooting cron jobs on Ubuntu systems.

---

## 2. What is cron, crontab and cronjob?

**🕒 What is cron?**

**cron** is like a personal assistant on your computer/server that runs tasks **automatically** at scheduled times.

- Think of it like setting an alarm clock: "Do this thing every day at 6am."

**📄 What is crontab?**

**crontab** = **cron table**
- It’s a **file** where you **write down the schedule** for the tasks (aka **cron jobs**) you want to run.
- You use the `crontab` command to **view, edit, or manage** your cron jobs.

**✅ What is a cron job?**

A **cron job** is just the **task** you want to run on a schedule.
- Example: Backing up files every night at 2am.
- In crontab, it looks like this:

```
0 2 * * * /home/user/backup.sh
```

This means:  
🕑 At 2:00 AM, every day, run the `backup.sh` script.

---

**Check cron status**

```
sudo systemctl status cron
```

**Start cron (if inactive)**
If cron is already active, this command will simply ensure it's running without restarting it unnecessarily.

```
sudo systemctl start cron
```

**Enable cron on system boot**

```
sudo systemctl enable cron
```

## 3. Cron Syntax Format

Learn how to write the correct cron job schedule format to run tasks at specific times — like hourly, daily, or on specific weekdays.

```
* * * * * command_to_run
│ │ │ │ │
│ │ │ │ └─ Day of the Week (0 - 7) (Sunday = 0 or 7)
│ │ │ └──── Month (1 - 12)
│ │ └────── Day of Month (1 - 31)
│ └──────── Hour (0 - 23)
└────────── Minute (0 - 59)
```

---

## 4. Prerequisites

- Ubuntu 22.04 or compatible Linux environment  
- User access with `sudo` privileges  
- Basic shell scripting knowledge  

---

## 5. Creating, Viewing, Removing and Editing Cron Jobs

Open the cron table (crontab) of the current user in edit mode, so you can create, modify, or delete scheduled tasks (cron jobs).

```
crontab -e
```

**Example to Create a Cron job**

**Step 1: Create a Script**

```
nano /home/ubuntu/hello.sh
```

Paste this into the file:
```bash
#!/bin/bash
echo "Hello from cron at $(date)" >> /home/ubuntu/hello_log.txt
```
Then make it executable:
```bash
chmod +x /home/ubuntu/hello.sh
```

**Step 2: Schedule It in Cron**
```
crontab -e
```

Add your cron job in the file:
```
0 9 * * * /home/ubuntu/hello.sh
```

This will run the hello.sh script every day at 9:00 AM.

**Step 3: Verify It’s Working**
```
cat /home/ubuntu/hello_log.txt
```

You should see something like:

```
Hello from cron at Wed Apr 14 09:00:01 UTC 2025

```

**Viewing Cron Jobs**

For Current User
List your scheduled jobs:

```
crontab -l
```

For Another User (as root)

```
crontab -u username -l
```

**Removing Cron Jobs**

Remove All Cron Jobs without confirmation

```
crontab -r
```

Remove All Cron Jobs with confirmation:

```
crontab -i -r
```

**To edit your existing cron jobs**

Open the crontab:

```
crontab -e
```

Modify the scheduled jobs (e.g., change the time or script) in the crontab file.  
Save and exit after making the changes.

## 6. Check System Cron Logs

```
grep CRON /var/log/syslog
```

This command will show logs for cron job executions, both user-specific and system-wide jobs.


## 7. System & Directory-Based Cron Jobs

**System-wide Cron File**
**Location:** `/etc/crontab`  

Can Be Used For: Running scripts as any user with specific permissions for system-wide tasks.

**Step 1: Open the system cron file:**

```
sudo nano /etc/crontab
```
**Step 2: Add the following line at the bottom:**
```
0 2 * * * root /home/ubuntu/hello.sh
```
This runs the script daily at 2:00 AM as the root user

---

**Custom Cron Files Directory:**
**Location:** `/etc/cron.d/`  

This allows you to store cron jobs in separate files and specify the user for each job.

Can Be Used For: Storing cron jobs for different users, making management easier without modifying the main cron file.

**Step 1: Create a new file in /etc/cron.d/ for user1.**
Let’s name it user1_hello_cron
```
sudo nano /etc/cron.d/user1_hello_cron
```

**Step 2: Add the following line to run hello.sh:**
```
0 2 * * * user1 /home/ubuntu/hello.sh
```
This runs the script daily at 2:00 AM as the user1

**Step 3: Create a new file in /etc/cron.d/ for user2.** 
Let’s name it user2_hello_cron
```
sudo nano /etc/cron.d/user2_hello_cron
```

**Step 4: Add the following line to run hello.sh:**
```
0 2 * * * user2 /home/ubuntu/hello.sh
```
This runs the script daily at 2:00 AM as the user2

---

**🗓️ Time-Based Cron Directories**

Want your script to run automatically every hour, day, week, or month? Just copy it to the right directory and make it executable:

```bash
# Hourly
sudo cp hello.sh /etc/cron.hourly/
sudo chmod +x /etc/cron.hourly/hello.sh
```

```bash
# Daily
sudo cp hello.sh /etc/cron.daily/
sudo chmod +x /etc/cron.daily/hello.sh
```

```bash
# Weekly
sudo cp hello.sh /etc/cron.weekly/
sudo chmod +x /etc/cron.weekly/hello.sh
```

```bash
# Monthly
sudo cp hello.sh /etc/cron.monthly/
sudo chmod +x /etc/cron.monthly/hello.sh
```

✅ Just change the directory path based on how often you want it to run. The system takes care of the schedule automatically.

## 8. Example Cron Jobs for Common Use Cases

**Running System Updates**
Run system updates every day at 5 AM:

```
0 5 * * * root apt update && apt upgrade -y.
```

**Running System Updates**
Run log rotation every day at midnight:

```
0 0 * * * root /usr/sbin/logrotate /etc/logrotate.conf
```
---

## 9. References

1. [Cron Jobs - Ask Ubuntu](https://askubuntu.com/questions/2368/how-do-i-set-up-a-cron-job)  
   - Official documentation about cron jobs and crontab file format.

2. [Using Cron for Automation](https://www.digitalocean.com/community/tutorials/how-to-use-cron-to-automate-tasks-ubuntu-1804))  
   - A blog post from DigitalOcean explaining cron jobs and how they can be used for automation tasks.

---

## **Contact Information**
| **Name** | **Email Address**        |
|----------|--------------------------|
| **Prince Batra**  | **prince.batra.snaatak@mygurukulam.co**   |

