### Linux Day-2: User and Group Management

ssh tony@stapp01                     # Login to the server as user 'tony' via SSH
sudo -i                              # Switch to root user (admin privileges required)

cat /etc/passwd | grep koko          # Check whether user 'koko' already exists
cat /etc/group | grep k-group        # Check whether group 'k-group' already exists

groupadd k-group                     # Create a new group named 'k-group'

useradd -G k-group koko              # Create user 'koko' and add to secondary group 'k-group'

cat /etc/passwd | grep koko          # Recheck and confirm user creation
cat /etc/group | grep k-group        # Recheck and confirm group creation

id koko                              # Verify UID, GID, and group membership of user 'koko'
exit                                 # Exit from root shell or SSH session

=====================================================================================================

## Advanced `useradd` Options

useradd -u 1176 -m -d /var/www/koko koko
# Create a new user named 'koko' with advanced options
# -u 1176              → Assign a custom UID (User ID)
# -m                   → Automatically create the home directory
# -d /var/www/koko     → Set a custom home directory (commonly used for web/app users)
# koko                 → Username being created

### Why use advanced options?

* Custom UID helps maintain consistency across multiple servers
* Custom home directory is useful for Apache, Nginx, or application users
* `-m` ensures the directory exists with correct ownership


### Notes

* `/etc/passwd` → Stores user account information
* `/etc/group`  → Stores group information
* `groupadd`    → Used to create new groups
* `useradd`     → Used to create new users
* `id`          → Used to verify user and group details

✔ Suitable for quick revision, lab practice, and interviews

==============================================================================================================
