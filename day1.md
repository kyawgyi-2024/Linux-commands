# Linux Day-1 – Custom Apache User Setup

We create a custom Apache user to isolate web processes and improve server security.

ssh steve@stapp02                     # Login to server as user 'steve'
sudo -i                               # Switch to root (full admin shell)

useradd -u 1176 -m -d /var/www/koko koko
# Create a new user named 'koko'
# -u 1176        → Assign custom UID (user ID)
# -m             → Create home directory automatically
# -d /var/www/koko → Set custom home directory (useful for Apache web user)
# koko           → Username

grep koko /etc/passwd
# Verify user creation
# Shows user details stored in /etc/passwd

# Expected Output of /etc/passwd
koko:x:1176:1176::/var/www/koko:/bin/bash

# Meaning of Each Field
koko        → Username
x           → Password stored in /etc/shadow
1176        → UID (User ID)
1176        → GID (Group ID)
(empty)     → Comment / GECOS
/var/www/koko → Home directory
/bin/bash   → Default login shell

=================================================================================================================
# Why This Is Used in DevOps / Apache Setup

Runs Apache or web apps with a dedicated user

Improves security isolation

Common in production servers

Avoids using root for web services
================================================================================================================

# Apache Run-As User & Group (How Apache Runs)

Apache does NOT run as root permanently.

🔹 How it works

Apache starts as root (to bind ports like 80/443)

Then it drops privileges and runs workers as a normal user

# Apache config (CentOS / RHEL)
cat /etc/httpd/conf/httpd.conf | grep -E "User|Group"
User apache
Group apache
(This means Apache worker processes run as apache:apache)

# Change Apache to use custom user (koko)
sudo vi /etc/httpd/conf/httpd.conf

change:
User apache
Group apache

To:
User koko
Group koko

sudo systemctl restart httpd

# Verify running user
ps -ef | grep httpd
koko   1234  ... httpd
koko   1235  ... httpd
(Apache now runs as koko)

# Apache Directory Permissions (VERY IMPORTANT)
📁 Web root;
/var/www/koko

Correct ownership;
sudo chown -R koko:koko /var/www/koko

Correct permission;
sudo chmod -R 755 /var/www/koko

Meaning of 755;
Owner (koko)  → read, write, execute
Group         → read, execute
Others        → read, execute
============================================================================
