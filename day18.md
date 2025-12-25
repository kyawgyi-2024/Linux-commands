# 🐧 Linux Day-18: SELinux Configuration (Temporary Disable)

🔹 Task Goal
Prepare the system for upcoming configuration changes by:
1. Installing required SELinux packages
2. Permanently disabling SELinux (effective after reboot)
3. No reboot now (scheduled maintenance reboot later)
4. Ignore current SELinux runtime status — final state after reboot must be disabled
Server:stapp02

🔹 Login to Application Server
ssh steve@stapp02                   # Login to App Server as user 'steve'

🔹 Switch to Root User
sudo -i                             # Become root (required for SELinux configuration)

🔹 Update Package Repository
yum update -y                       # Update package metadata and system packages
# Ensures latest SELinux packages are available

🔹 Install Required SELinux Packages
yum install -y selinux-policy selinux-policy-targeted policycoreutils
# selinux-policy → Core SELinux policies
# selinux-policy-targeted → Targeted SELinux policy (default on CentOS)
# policycoreutils → SELinux management tools (getenforce, sestatus, etc.)

🔹 Verify SELinux Packages Installation
rpm -qa | grep selinux              # Confirm SELinux-related packages are installed
# rpm -qa → list all installed packages
# grep selinux → filter SELinux packages

🔹 Verify SELinux Configuration Directory
ls /etc/selinux                    # Check SELinux configuration files directory
# config file should exist here

🔹 Permanently Disable SELinux
vi /etc/selinux/config             # Open SELinux main configuration file
# This file controls SELinux state AFTER reboot
Inside the file:
SELINUX=enforcing
Change to:
SELINUX=disabled

vi editor steps
---
/SELINUX=          # Search for SELINUX line
i                  # Enter insert mode
Change enforcing → disabled
ESC                # Exit insert mode
:wq                # Save and quit
---

🔹 Verify SELinux Is Set to Disabled
cat /etc/selinux/config | grep SELINUX=disabled
# Confirms SELinux will be disabled after reboot

# 📝 Important Notes
No reboot is required right now
SELinux may still show as enforcing or permissive
Final SELinux status will be DISABLED after scheduled reboot

# 📝 Summary
Logged into stapp02 as steve
Switched to root user
Updated system packages
Installed required SELinux packages
Verified SELinux package installation
Edited /etc/selinux/config
Set SELINUX=disabled permanently
Confirmed configuration change

# 🎯 Interview Tips
getenforce → shows current runtime SELinux mode
/etc/selinux/config → controls SELinux mode after reboot

SELinux modes:
enforcing → active & blocking
permissive → logging only
disabled → completely off
Permanent changes always require reboot
Common practice: disable temporarily, configure properly, re-enable later

✔ Very common Linux Admin & KodeKloud challenge
