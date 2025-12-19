# Linux Day-3: User Setup and Non-Interactive Shell

ssh steve@stpp01                    # Login to the server as user 'steve' using SSH

sudo -i                             # Switch to root user (required for user management)

useradd -s /sbin/nologin koko
# Create a new user named 'koko'
# -s /sbin/nologin   → Assign a non-interactive shell
#                      This prevents the user from logging in via SSH or terminal
#                      Commonly used for service, system, or application users

getent passwd | grep koko
# Verify user 'koko' exists using the system user database
# getent passwd     → Fetch user information from NSS (local + LDAP if configured)
# grep koko         → Filter output for user 'koko'

===============================================================================================

🔎 Why use /sbin/nologin?

Prevents direct SSH or shell access

Improves system security

Common for:

Web service users

Database users

Application/system accounts

=================================================================================================
Summary

useradd -s /sbin/nologin creates a non-login user

getent passwd is safer than cat /etc/passwd in enterprise systems

Ideal for service and application users

===============================================================================================
# nologin vs /bin/false

1. /sbin/nologin

useradd -s /sbin/nologin koko

What it does:

Prevents interactive login (SSH, console)

Displays a message like:

This account is currently not available.

When to use:

Service accounts (Apache, Nginx, DB users)

Application users that should never log in

Best practice for security

Behavior:

❌ No shell access

❌ No SSH login

✔ Allows running services as that user
=================================================================================================

2. /bin/false

useradd -s /bin/false koko

What it does:

Immediately terminates the session

No message shown to the user

When to use:

Older systems

Very strict lock-down scenarios

Minimal environments

Behavior:

❌ No shell access

❌ No SSH login

❌ Exits instantly
==============================================================================================

| Feature             | `/sbin/nologin` | `/bin/false` |
| ------------------- | --------------- | ------------ |
| Shows login message | ✅ Yes           | ❌ No         |
| User-friendly       | ✅ Yes           | ❌ No         |
| Recommended today   | ✅ Yes           | ❌ No         |
| Service accounts    | ✅ Best choice   | ⚠️ Rare      |

Recommended: /sbin/nologin
================================================================================================

# Locking and Unlocking Users

🔐 Lock a user account

usermod -L koko
# Lock user 'koko'
# Prevents password-based login

passwd -l koko
# Lock the user's password

🔓 Unlock a user account

usermod -U koko
# Unlock user 'koko'

passwd -u koko
# Unlock the user's password

🔍 Check user lock status

passwd -S koko
# Shows account status (L = locked, P = active)
==============================================================================================
Important Admin Tip (Interview Favorite)

🔸 nologin controls shell access
🔸 Locking controls password authentication

👉 You can have:

A nologin user that is unlocked

A login shell user that is locked
=============================================================================================
