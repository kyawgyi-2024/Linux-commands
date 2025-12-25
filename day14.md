# 🐧 Linux Day-14: Enable GUI Boot by Default (Runlevel Fix)

🔹 Task Goal
Adjust the default system runlevel (target) on all App Servers so the system boots into GUI mode by default.
👉 One-line fix command: systemctl set-default graphical.target

🔹 Login to Application Server
ssh tony@stapp01                    # Login to App Server as user 'tony'

🔹 Switch to Root User
sudo -i                             # Become root (required to change system targets)

🔹 Check Current Default Target
systemctl get-default               # Display current default boot target
# multi-user.target → CLI mode (no GUI)
# Equivalent to runlevel 3 in older systems

🔹 Set GUI as Default Boot Target
systemctl set-default graphical.target
# set-default → change default boot target
# graphical.target → GUI mode with display manager
# Equivalent to runlevel 5 (GUI)

🔹 Verify New Default Target
systemctl get-default               # Confirm default target is updated
# Expected output: graphical.target

🔹 Exit Root Session
exit                                # Leave root shell

🔹 Repeat on All App Servers
Apply the same steps on every App server
(stapp01, stapp02, stapp03, etc.)

# 📝 Summary
Logged into App server as tony
Switched to root user
Checked current default runlevel (multi-user)
Set graphical.target as default
Verified GUI is now the default boot mode
Repeated process on all App servers

# 🎯 Interview Tips
systemctl get-default → check current runlevel
systemctl set-default graphical.target → enable GUI at boot
multi-user.target → CLI only (no GUI)
graphical.target → GUI + display manager
Modern systems use systemd targets instead of classic runlevels

✔ Common Linux Admin & DevOps interview question