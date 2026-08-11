# LabEx - Keeper of the Keys

**Course:** Junior System Administrator  
**Lab:** 5 - Keeper of the Keys from LabEx 


## Objective

The goal of this lab was to practice Linux user and group management while applying appropriate access controls and password administration.

## Tasks Performed

### 1. Create a User

Created a new user account for the senior developer:

```bash
sudo useradd b.smith
```

Verified the account using:

```bash
grep "b.smith" /etc/passwd
id b.smith
```

### 2. Create a Home Directory

Created the user's home directory:

```bash
sudo useradd -m b.smith
```

Checked the `/home` directory:

```bash
ls -la /home/
```

Attempting to inspect the user's home directory without sufficient privileges resulted in:

```text
Permission denied
```

This demonstrated that Linux permissions restrict access to protected user directories.

Used `sudo` to inspect the directory:

```bash
sudo ls -la /home/b.smith/
```

### 3. Set a Password

Set a password for the user:

```bash
sudo passwd b.smith
```

Verified password-related information using:

```bash
sudo grep "b.smith" /etc/shadow
```

The `/etc/shadow` file contains protected password and account-aging information and normally requires elevated privileges to access.

### 4. Manage Group Membership

Added the user to the `developers` group:

```bash
sudo usermod -aG developers b.smith
```

Verified the group membership:

```bash
groups b.smith
```

Also verified the user's group information:

```bash
id b.smith
```

### 5. Work with Group Information

Checked the `developers` group in `/etc/group`:

```bash
grep "developers" /etc/group
```

### 6. Password Expiry Management

Worked with password expiry information using:

```bash
sudo passwd -l j.doe
```

and checked the resulting account information:

```bash
sudo grep "j.doe:" /etc/shadow
```

## Key Concepts Learned

- Linux user accounts can be created and managed using `useradd`.
- The `-m` option creates a home directory for a new user.
- `/etc/passwd` stores basic information about local user accounts.
- `/etc/shadow` stores protected password hashes and account-aging information.
- The `id` command displays a user's UID, GID, and group memberships.
- `groups` can be used to check a user's group membership.
- `usermod -aG` can add a user to a supplementary group.
- Linux file and directory permissions control who can access user data.
- Administrative tasks involving protected system files often require `sudo`.
- Password and account-management commands are important for maintaining secure Linux systems.

## Security Takeaways

This lab showed how user management is directly connected to system security.

Properly configuring users, groups, passwords, home directories, and access permissions helps enforce **least privilege** and prevents unauthorized access to sensitive resources.

