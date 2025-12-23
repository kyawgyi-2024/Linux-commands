# Linux Day-5: Temporary User Setup with Expiry

🔹 Task Goal
Create a temporary Linux user account that automatically expires on a specific date and verify the expiry details.

🔹 Login to Application Server
ssh tony@stapp01                     # Login to application server

🔹 Switch to Root User
sudo -i                              # Become root for user management

🔹 Create Temporary User with Expiry Date
useradd -e 2026-01-30 koko
# useradd → create new user
# -e 2026-01-30 → account expiry date (YYYY-MM-DD)
# koko → username
📌 After 30 Jan 2026, user koko will not be able to log in.

🔹 Verify User Account Expiry Details
chage -l koko
# chage → manage password aging
# -l → list user account details
# koko → username

🔹 Sample Output Explanation
Last password change                    : Aug 20, 2025
Password expires                        : never
Password inactive                       : never
Account expires                         : Jan 30, 2026
Minimum number of days between changes  : 0
Maximum number of days between changes  : 99999
Number of days of warning before expire : 7

| Field                | Description                      |
| -------------------- | -------------------------------- |
| Last password change | Last password update             |
| Password expires     | Password expiry date             |
| Password inactive    | Lock delay after password expiry |
| Account expires      | **User login expiry date**       |
| Minimum days         | Min days before password change  |
| Maximum days         | Password validity period         |
| Warning days         | Days before expiry warning       |

🔹 Modify Account Expiry (Optional)
chage -E 2026-03-01 koko
# -E → set new account expiry date

# 📝 Summary
Created temporary user koko
Set account expiry to 2026-01-30
Verified expiry using chage -l
Account automatically disables after expiry date

# 🎯 Interview Tips
useradd -e → sets account expiry
chage -l → displays expiry and password aging info
chage -E → modify existing expiry date
Commonly used for interns, contractors, temporary access

✔ Standard Linux user management task in DevOps environments

========================================================================================================

🔹 All Commands (In Order)
ssh tony@stapp01              # Login to server
sudo -i                       # Switch to root
useradd -e 2026-01-30 koko    # Create user with expiry date
chage -l koko                 # Verify account expiry details

🔹 Optional (Modify Expiry Date)
chage -E 2026-03-01 koko      # Change account expiry date

🔹 Key Command Meanings
useradd -e DATE USER          # Create user with account expiry
chage -l USER                 # List expiry & password aging info
chage -E DATE USER            # Update account expiry date

useradd -e → set expiry
chage -l → check expiry