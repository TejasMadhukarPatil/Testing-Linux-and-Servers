# Testing-Linux-and-Servers
Task 1: System Monitoring Setup    .   Task 2: User Management and Access Control     .   Task 3: Backup Configuration for Web Servers

**1. Install Monitoring Tools**

# Install htop
sudo apt update && sudo apt install htop -y

# OR install nmon (choose one)
sudo apt install nmon -y

**2. Monitor CPU, Memory, and Processes**
- Run htop or nmon to view real-time system metrics.
- Use ps aux --sort=-%mem | head to identify memory-intensive processes.
- Use top or htop to identify CPU-intensive processes.
**3. Disk Usage Monitoring**
# Check disk space
df -h > /var/log/disk_usage.log

# Check directory sizes
du -sh /home/* >> /var/log/disk_usage.log
**4. Logging System Metrics**
Create a cron job to log metrics every hour:
sudo crontab -e
**Task 2: User Management and Access Control **
Create User Accounts
sudo adduser Sarah
sudo adduser Mike
2. Set Secure Passwords
sudo passwd Sarah
sudo passwd Mike


3. Create Isolated Directories
mkdir -p /home/Sarah/workspace
mkdir -p /home/Mike/workspace

# Set ownership
sudo chown Sarah:Sarah /home/Sarah/workspace
sudo chown Mike:Mike /home/Mike/workspace

# Restrict access
sudo chmod 700 /home/Sarah/workspace
sudo chmod 700 /home/Mike/workspace


**4. Enforce Password Policy**
sudo apt install libpam-pwquality -y

**Task 3: Backup Configuration for Web Servers**
sudo nano /home/Sarah/apache_backup.sh
#!/bin/bash
DATE=$(date +%F)
tar -czf /backups/nginx_backup_$DATE.tar.gz /etc/nginx/ /usr/share/nginx/html/
tar -tzf /backups/nginx_backup_$DATE.tar.gz > /backups/nginx_backup_$DATE.log
sudo chmod +x /home/Mike/nginx_backup.sh

3. Schedule Cron Jobs
   sudo crontab -u Sarah -e
0 0 * * 2 /home/Sarah/apache_backup.sh
   sudo crontab -u Mike -e

 **  4. Verify Backup Integrity**
 cat /backups/apache_backup_YYYY-MM-DD.log
cat /backups/nginx_backup_YYYY-MM-DD.log






Task 1: System Monitoring Setup

Objective: Configure a monitoring system to ensure the development environment’s health, performance, and capacity planning.

Scenario:

The development server is reporting intermittent performance issues.

New developers need visibility into system resource usage for their tasks.

System metrics must be consistently tracked for effective capacity planning.

Requirements:

Install and configure monitoring tools (htop or nmon) to monitor CPU, memory, and process usage.

Set up disk usage monitoring to track storage availability using df and du.

Implement process monitoring to identify resource-intensive applications.

Create a basic reporting structure







Task 2: User Management and Access Control

Objective: Set up user accounts and configure secure access controls for the new developers.

Scenario:

Two new developers, Sarah and Mike, require system access.

Each developer needs an isolated working directory to maintain security and confidentiality.

Security policies must ensure proper password management and access restrictions.

Requirements:

Create user accounts for Sarah and Mike with secure passwords.

Set up dedicated directories: 

Sarah: /home/Sarah/workspace

Mike: /home/mike/workspace

Ensure only the respective users can access their directories using appropriate permissions.

Implement a password policy to enforce expiration and complexity









Task 3: Backup Configuration for Web Servers

Objective: Configure automated backups for Sarah’s Apache server and Mike’s Nginx server to ensure data integrity and recovery.

Scenario:

Sarah is responsible for managing an Apache web server.

Mike is responsible for managing a Nginx web server. 

Both servers require regular backups to a secure location for disaster recovery.

Requirements:

Sarah and Mike need to automate backups for their respective web server configurations and document roots: 

Sarah: Backup the Apache configuration (/etc/httpd/) and document root (/var/www/html/).

Mike: Backup the Nginx configuration (/etc/nginx/) and document root (/usr/share/nginx/html/).

Schedule the backups to run every Tuesday at 12:00 AM using cron jobs.

Save the backups as compressed files in /backups/ with filenames including the server name and date (e.g., apache_backup_YYYY-MM-DD.tar.gz).

Verify the backup integrity after each run by listing the contents of the compressed file.



<img width="791" height="82" alt="image" src="https://github.com/user-attachments/assets/69035325-db0c-461f-af8d-ee6f442d6b6c" />
<img width="587" height="187" alt="image" src="https://github.com/user-attachments/assets/aaadcf66-e6de-4f19-b93b-a3670226cf7d" />
<img width="860" height="170" alt="image" src="https://github.com/user-attachments/assets/bb6a5d4c-4941-42df-bce3-68ba0431b0f0" />






**Report Structure**
- **Introduction**
- Objective of the setup
- Roles of Sarah and Mike
- **Task Implementation**
- Step-by-step commands and configurations
- Screenshots or terminal outputs
- **Challenges**
- Any issues faced (e.g., permission errors, cron syntax)
- **Verification**
- Logs from /var/log/system_monitor.log
- Backup verification logs from /backups/
- **Conclusion**
- - Summary of successful setup
- Future recommendations (e.g., centralized logging, monitoring dashboards)


