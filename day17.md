# 🐧 Linux Day-17: Linux Performance Fix
(Setting Process Limits Using limits.conf)

🔹 Task Goal
Fix performance degradation on the Storage Server caused by the user nfsuser holding too many processes.

✅ Solution: Enforce process limits for nfsuser:
Soft limit: 1026
Hard limit: 2026
---
Server:ststor01

🔹 Login to Storage Server
ssh natasha@ststor01                # Login to storage server as user 'natasha'

🔹 Switch to Root User
sudo -i                             # Become root (required to modify limits.conf)

🔹 Edit Process Limits Configuration
vi /etc/security/limits.conf        # Open limits configuration file
# limits.conf → controls user-level resource limits
# Changes here affect login sessions
🔹 Add Process Limits for nfsuser
Move to the end of the file and add:
---
nfsuser  soft  nproc  1026
nfsuser  hard  nproc  2026
---
vi editor steps : 
Shift+G   → Go to end of file
o         → Insert a new line below
Paste / type the entries
ESC       → Exit insert mode
:wq       → Save and quit
---

🔹 Explanation of Entries
---
# nfsuser  soft  nproc  1026
nfsuser → Target user
soft → Warning limit (user can reach this limit)
nproc → Maximum number of processes
1026 → Soft process limit
---
# nfsuser  hard  nproc  2026
hard → Absolute maximum limit
(Cannot be exceeded by the user)

🔹 Apply the Changes
⚠ nfsuser must logout and login back 
(Process limits apply only to new sessions)

(Optional verification after relogin):
ulimit -u                           # Shows max number of user processes

# 📝 Summary
Logged into ststor01 as natasha
Switched to root user
Edited /etc/security/limits.conf
Set soft nproc limit to 1026 for nfsuser
Set hard nproc limit to 2026 for nfsuser
Saved configuration
User must relogin for changes to take effect

# 🎯 Interview Tips
limits.conf controls resource limits per user
nproc → limits number of processes
Soft limit → can be increased up to hard limit
Hard limit → enforced maximum
Changes apply after logout/login
Helps prevent resource exhaustion attacks

✔ Very common KodeKloud & Linux Admin interview topic
