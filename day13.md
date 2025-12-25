# 🐧 Linux Day-13: Restrict Cron Access

🔹 Task Goal
Configure crontab access control on App Server 1 so that:
✅ User kirsty is allowed to use crontab
❌ User garrett is denied access to crontab
Server:stapp01

🔹 Login to Application Server
ssh tony@stapp01                    # Login to App Server 1 as user 'tony'

🔹 Switch to Root User
sudo -i                             # Become root (required to manage cron access files)

🔹 Check Cron Service Status
systemctl status crond              # Verify cron daemon is running
# systemctl → service management tool
# status → shows current state of the service
# crond → cron daemon service

🔹 Allow Crontab Access for User kirsty
vi /etc/cron.allow                  # Open cron allow list
# /etc/cron.allow → users listed here CAN use crontab
# If this file exists, ONLY listed users are allowed
Inside the file:
kirsty
i        # Enter insert mode
kirsty   # Add allowed user
ESC      # Exit insert mode
:wq      # Save and quit

🔹 Deny Crontab Access for User garrett
vi /etc/cron.deny                   # Open cron deny list
# /etc/cron.deny → users listed here CANNOT use crontab
Inside the file:
garrett
i         # Insert mode
garrett   # Add denied user
ESC       # Exit insert mode
:wq       # Save and quit

🔹 Restart Cron Service (Optional but Safe)
systemctl restart crond             # Restart cron to apply changes
# Not always required, but ensures rules are reloaded

🔹 Verify Cron Service Status
systemctl status crond              # Confirm cron service is running normally

# 📝 Summary
Logged into stapp01 as tony
Switched to root user
Verified cron daemon status
Allowed crontab access for user kirsty
Denied crontab access for user garrett
Restarted cron service
Confirmed cron service is active

# 🎯 Interview Tips
/etc/cron.allow
If exists → ONLY listed users can use crontab
/etc/cron.deny
Users listed here are blocked from crontab
If cron.allow exists, cron.deny is ignored
Root user always has cron access
Common task in Linux Admin & DevOps roles