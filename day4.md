# Linux Day-4: Service User Creation (Without Home Directory)

ssh banner@stapp03                  # Login to the server as user 'banner' using SSH
sudo -i                             # Switch to root user (required for user management)

useradd -M koko
# Create a service user named 'koko'
# -M               → Do NOT create a home directory
#                    Useful for service or application users
#                    Reduces unnecessary files and improves security

getent passwd | grep koko
# Verify that user 'koko' exists in the system
# getent passwd     → Retrieves user info from system databases (local/LDAP)
# grep koko         → Filters output to show only user 'koko'

🔎 Why create a user without a home directory?

Service users do not need interactive login

Saves disk space and keeps system clean

Common for:

Application services

Daemons

Background processes

✅ Summary

useradd -M creates a user without a home directory

getent passwd is preferred over cat /etc/passwd

Best practice for service and system users

===============================================================================================
# 👤 Normal Users vs ⚙️ System Users (Linux)

1️⃣ Normal Users
🔹 What are they?

Normal users are human users who log in and use the system interactively.

🔹 Characteristics

Usually have UID ≥ 1000 (may vary by distro)

Have a home directory (e.g. /home/username)

Have a login shell (e.g. /bin/bash)

Can log in via SSH / terminal

🔹 Example
useradd -m -s /bin/bash john
john:x:1001:1001::/home/john:/bin/bash

🔹 Use cases
Developers
System administrators
End users
=============================================================================================
2️⃣ System Users
🔹 What are they?

System users are non-human accounts used to run services and applications.

🔹 Characteristics

Usually have UID < 1000

Often no home directory

Often use /sbin/nologin or /bin/false

Cannot log in interactively

Created for security isolation

🔹 Example
useradd -r -M -s /sbin/nologin nginx
nginx:x:995:995::/usr/share/nginx:/sbin/nologin

🔹 Use cases

Web servers (nginx, apache)
Databases (mysql, postgres)
Application services
===============================================================================================

| Feature        | Normal User | System User     |
| -------------- | ----------- | --------------- |
| Purpose        | Human login | Run services    |
| UID range      | ≥ 1000      | < 1000          |
| Home directory | Yes         | Usually no      |
| Login shell    | `/bin/bash` | `/sbin/nologin` |
| SSH login      | Allowed     | Not allowed     |
| Security risk  | Higher      | Lower           |

==================================================================================================
🔐 Why System Users Improve Security

Limits damage if a service is compromised

Prevents SSH access

Applies principle of least privilege

Each service runs as its own user

🧠 Admin Best Practice (Very Important)

❌ Never run services as root
✅ Always use a dedicated system user

📌 Common Commands
# Create a system user
useradd -r -M -s /sbin/nologin appuser

# Create a normal user
useradd -m -s /bin/bash devuser

🎯 Exam / Interview One-Line Answer
Normal users are for human login and interaction,
System users are non-login accounts used to run services securely.
=================================================================================================
