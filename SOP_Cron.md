# SOP: Managing Cron Jobs on Ubuntu

## 👤 **Author Information**
| **Author** | **Created on** | **Version**  | **Comment** | **Reviewer** |
|------------|----------------|--------------|-------------|--------------|
| **Prince Batra**   | **14-04-2025**   | **Version 1** | **Internal review** | **Siddharth Pawar** |

---

## 🎯 Purpose 

This SOP outlines how to create, edit, and manage cron jobs on Ubuntu systems. It helps in automating tasks like backups, log rotation, and monitoring.

---

## 🛠 Prerequisites

- Ubuntu 22.04 or compatible Linux environment  
- User access with `sudo` privileges  
- Basic shell scripting knowledge  

---

## 1. Introduction
Cron is a time-based job scheduler in Unix-like operating systems. This SOP provides step-by-step instructions for creating, editing, managing, and troubleshooting cron jobs on Ubuntu systems.

## 2. What is cron and crontab?

🎯 Objective / Use Case:  
Cron is a time-based job scheduler in Unix-like operating systems like Ubuntu. It lets users schedule tasks (called cron jobs) to run automatically at specified times or intervals.

📌 Example Use Case:  
Automatically run a backup script every night at midnight to save important files or logs for future use.

Check cron status

```
sudo systemctl status cron
```

Start cron (if inactive)
If cron is already active, this command will simply ensure it's running without restarting it unnecessarily.

```
sudo systemctl start cron
```

Enable cron on system boot 

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

## 4. Creating, Viewing, Removing and Editing Cron Jobs

Open the cron table (crontab) of the current user in edit mode, so you can create, modify, or delete scheduled tasks (cron jobs).

```
crontab -e
```

### 4.1 Example to Create a Cron job

#### Step 1: Create a Script

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

#### Step 2: Schedule It in Cron
```
crontab -e
```

Add your cron job in the file:
```
0 9 * * * /home/ubuntu/hello.sh
```

This will run the hello.sh script every day at 9:00 AM.

#### Step 3: Verify It’s Working
```
cat /home/ubuntu/hello_log.txt
```

You should see something like:

```
Hello from cron at Wed Apr 14 09:00:01 UTC 2025

```

## 4.2. Viewing Cron Jobs

### For Current User
List your scheduled jobs:

```
crontab -l
```

### For Another User (as root)

```
crontab -u username -l
```

## 4.3. Removing Cron Jobs

### Remove All Cron Jobs without confirmation

```
crontab -r
```

### Remove All Cron Jobs with confirmation:

```
crontab -i -r
```

## 4.4. To edit your existing cron jobs

Open the crontab:

```
crontab -e
```

Modify the scheduled jobs (e.g., change the time or script) in the crontab file.  
Save and exit after making the changes.

## 5. Check System Cron Logs

```
grep CRON /var/log/syslog
```

This command will show logs for cron job executions, both user-specific and system-wide jobs.

### System-wide Cron File 
**Location:** `/etc/crontab`  

Can Be Used For: Running scripts as any user with specific permissions for system-wide tasks.

#### Step 1: Open the system cron file:

```
sudo nano /etc/crontab
```
#### Step 2: Add the following line at the bottom:
```
0 2 * * * root /home/ubuntu/hello.sh
```
This runs the script daily at 2:00 AM as the root user

### Custom Cron Files Directory:
**Location:** `/etc/cron.d/`  

This allows you to store cron jobs in separate files and specify the user for each job.

Can Be Used For: Storing cron jobs for different users, making management easier without modifying the main cron file.

#### Step 1: Create a new file in /etc/cron.d/ for user1. 
Let’s name it user1_hello_cron
```
sudo nano /etc/cron.d/user1_hello_cron
```

#### Step 2: Add the following line to run hello.sh:
```
0 2 * * * user1 /home/ubuntu/hello.sh
```
This runs the script daily at 2:00 AM as the user1

#### Step 3: Create a new file in /etc/cron.d/ for user2. 
Let’s name it user2_hello_cron
```
sudo nano /etc/cron.d/user2_hello_cron
```

#### Step 4: Add the following line to run hello.sh:
```
0 2 * * * user2 /home/ubuntu/hello.sh
```
This runs the script daily at 2:00 AM as the user2

### Directory for Hourly Cron Jobs
**Location:** `/etc/cron.hourly/`  

**Use Case:** Running scripts every hour for frequent tasks like monitoring or cleanup.

#### Step 1: Copy your hello.sh script to the /etc/cron.hourly/ directory: 
```
sudo cp /home/ubuntu/hello.sh /etc/cron.hourly/
sudo chmod +x /etc/cron.hourly/hello.sh
```
The script will now run automatically every hour, as /etc/cron.hourly/ is for hourly tasks.

### Directory for Daily Cron Jobs
**Location:** `/etc/cron.daily/`  

**Use Case:** Running scripts once a day for maintenance tasks like backups.

#### Step : Copy your hello.sh script to the /etc/cron.daily/ directory: 

```
sudo cp /home/ubuntu/hello.sh /etc/cron.daily/
sudo chmod +x /etc/cron.daily/hello.sh
```
The script will now run automatically once a day, as /etc/cron.daily/ is for daily tasks.

### Directory for Weekly Cron Jobs
**Location:** `/etc/cron.weekly/`

**Use Case:** Running scripts weekly for tasks like audits or reports.

#### Step : Copy your hello.sh script to the /etc/cron.weekly/ directory:

```
sudo cp /home/ubuntu/hello.sh /etc/cron.weekly/
sudo chmod +x /etc/cron.weekly/hello.sh
```
The script will now run automatically once a week.

### Directory for Monthly Cron Jobs
**Location:** `/etc/cron.monthly/`

Use Case:Running scripts monthly for tasks like archiving or reporting.

#### Step : Copy your hello.sh script to the /etc/cron.monthly/ directory:

```
sudo cp /home/ubuntu/hello.sh /etc/cron.monthly/
sudo chmod +x /etc/cron.monthly/hello.sh
```

The script will now run automatically once a month.

## 6. Example Cron Jobs for Common Use Cases

## 6.1 Running System Updates
Run system updates every day at 5 AM:

```
0 5 * * * root apt update && apt upgrade -y.
```

## 6.2 Running System Updates
Run log rotation every day at midnight:

```
0 0 * * * root /usr/sbin/logrotate /etc/logrotate.conf
```

---

**End of SOP**

## 📬 **Contact Information**
| **Name** | **Email Address**        |
|----------|--------------------------|
| **Prince Batra**  | **prince.batra.snaatak@mygurukulam.co**   |


