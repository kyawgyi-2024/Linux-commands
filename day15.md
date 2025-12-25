# 🐧 Linux Day-15: Timezone Challenge (Datacenter Synchronization)

🔹 Task Goal
Synchronize the timezone settings on all App Servers so they match the local datacenter timezone.
Required timezone:America/Argentina/Jujuy

🔹 Login to Application Server
ssh tony@stapp01                    # Login to App Server as user 'tony'

🔹 Switch to Root User
sudo -i                             # Become root (required to change system timezone)

🔹 Check Current Timezone
timedatectl                        # Display current date, time, and timezone
# timedatectl → systemd time & date control tool
# Shows:
# - Local time
# - Universal time (UTC)
# - Current Timezone

🔹 Find the Required Timezone
timedatectl list-timezones | grep America/Argentina/Jujuy
# list-timezones → shows all available timezones
# grep → filter output to locate the required timezone
# Confirms the timezone exists on the system

🔹 Set Datacenter Timezone
timedatectl set-timezone America/Argentina/Jujuy
# set-timezone → change system timezone
# America/Argentina/Jujuy → datacenter-required timezone

🔹 Recheck Timezone Configuration
timedatectl                        # Verify timezone has been updated
# Expected output:
# Time zone: America/Argentina/Jujuy

🔹 Repeat on All App Servers
Apply the same timezone configuration on every App server
(stapp01, stapp02, stapp03, etc.)

# 📝 Summary
Logged into App server as tony
Switched to root user
Checked existing timezone configuration
Verified availability of required timezone
Updated system timezone to America/Argentina/Jujuy
Confirmed timezone synchronization
Repeated process on all App servers

# 🎯 Interview Tips
timedatectl → view and manage system time settings
Timezone files are stored in /usr/share/zoneinfo/
Correct timezone is critical for:
Log timestamps
Cron jobs
Monitoring & alerting systems
set-timezone does not require a system reboot

✔ Frequently asked in Linux Admin & DevOps interviews