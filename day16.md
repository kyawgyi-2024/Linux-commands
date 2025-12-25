# 🐧 Linux Day-16: Firewall Configuration Challenge (Open Port 8088/TCP Permanently)

🔹 Task Goal
Configure the firewall on the server to:
Allow all incoming TCP connections on port 8088
Ensure the firewall zone is public
Make the rule permanent (persists after reboot)
Server:stbkp01
Application Port:8088/tcp

🔹 Login to Backup Server
ssh clint@stbkp01                   # Login to backup server as user 'clint'

🔹 Switch to Root User
sudo -i                             # Become root (required to manage firewall rules)

🔹 Check Default Firewall Zone
firewall-cmd --get-default-zone    # Display the default active firewall zone
# firewall-cmd → firewalld management tool
# --get-default-zone → shows which zone is in use
# Expected output: public

🔹 Open Port 8088/TCP Permanently
firewall-cmd --permanent --add-port=8088/tcp
# --permanent → make rule persistent across reboots
# --add-port=8088/tcp → allow TCP traffic on port 8088
# Success output confirms rule is added

🔹 Reload Firewall Rules
firewall-cmd --reload              # Apply permanent firewall rules
# Reloads firewalld configuration without restarting the service
# Success output confirms changes are active

🔹 (Optional) Verify Open Port
firewall-cmd --list-ports          # List all open ports in the active zone
# Should display: 8088/tcp

# 📝 Summary
Logged into stbkp01 as clint
Switched to root user
Verified default firewall zone is public
Opened TCP port 8088 permanently
Reloaded firewall to apply changes
Confirmed firewall rule is active

# 🎯 Interview Tips
firewall-cmd is used with firewalld
--permanent rules require --reload to take effect
public zone is the most commonly used default zone
--add-port opens a port regardless of service name
Always verify with --list-ports

✔ Common Linux Admin & DevOps firewall task