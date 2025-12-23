# Linux Day-7: Secure Root SSH Access

🔹 Task Goal
Disable direct root login over SSH for enhanced security on application servers (stapp01, stapp02, stapp03) and verify the SSH service status.

🔹 Login to Application Server
ssh tony@stapp01                  # Login to server as regular user 'tony'

🔹 Switch to Root User
sudo -i                           # Become root to modify SSH configuration

🔹 Edit SSH Configuration File
vi /etc/ssh/sshd_config           # Open SSH daemon configuration
Steps inside vi:
1. Press i → Enter insert mode
2. Find the line: /PermitRootLogin yes
3. Change it to: PermitRootLogin no
    no → disables direct root login via SSH
4. Press Esc → exit insert mode
5. Type :wq → save changes and quit vi

🔹 Restart SSH Service to Apply Changes
systemctl restart sshd            # Restart SSH daemon

🔹 Verify SSH Service Status
systemctl status sshd             # Check SSH daemon status
# Active (running) indicates SSH service is functioning properly

🔹 Repeat on Other Servers
Perform the same steps on:
# stapp02
# stapp03
Ensures consistent security policy across all application servers.

# 📝 Summary
Logged in as a non-root user tony
Switched to root using sudo -i
Edited /etc/ssh/sshd_config to disable root login
Restarted SSH service to apply changes
Verified SSH service is running

Applied same configuration on all app servers (stapp01, stapp02, stapp03)

# 🎯 Interview Tips
PermitRootLogin no → critical for securing SSH access
Always verify service status after configuration changes
Use sudo to safely modify system files
Remember to repeat changes on all servers for uniform security