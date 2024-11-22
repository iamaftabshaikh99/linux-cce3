### **Q1. Explain the concept of file permissions in Linux.**
**Introduction**:  
File permissions in Linux are an integral part of its security model. They determine the type of access (read, write, execute) a user has to files and directories, ensuring that only authorized users can interact with critical system resources.

**Answer**:
- **File Permissions**:
  - Define what actions a user can perform on a file or directory.
  - Permissions ensure security and prevent unauthorized access in multi-user systems.
- **Types**:
  - **Read (r)**: View file contents or list directory files.
  - **Write (w)**: Modify file contents or manage directory structure.
  - **Execute (x)**: Execute a file (if it’s a program/script) or traverse a directory.
- **User Categories**:
  1. **Owner (u)**: The file creator, typically with full control.
  2. **Group (g)**: Users within the same group, sharing specified permissions.
  3. **Others (o)**: All other system users.
- **Structure**:
  - Represented as `rwx` (read, write, execute) for each category.  
    Example: `-rw-r--r--` means:
    - Owner: Read and write (`rw-`).
    - Group: Read-only (`r--`).
    - Others: Read-only (`r--`).
  - Numeric representation: `chmod 755 file` gives:
    - Owner: `7 (rwx)`
    - Group: `5 (r-x)`
    - Others: `5 (r-x)`

### **Q2. Difference Between `sudo` and `root` in Linux**
**Introduction**:  
Linux is a multi-user operating system where certain administrative tasks require elevated privileges. These privileges can be accessed using `root`, the superuser account, or via the `sudo` command, which allows temporary privilege escalation. Understanding the difference between these two is essential for managing system security and efficiency.

**Answer**:
- **`sudo` (Substitute User Do)**:
  - Allows a regular user to execute commands as another user, typically `root`.
  - Requires the user to be part of the `sudoers` file, which is a configuration file that specifies which users can use `sudo`.
  - Promotes security by logging all actions performed with `sudo`, making it traceable.
  - Example:
    - `sudo apt update`: Temporarily elevates privileges to update the system.
    - After the command runs, the user reverts back to their regular permissions.
  - Provides granular control by allowing administrators to specify which commands a user can execute with `sudo`.

- **`root`**:
  - The superuser account with full and unrestricted access to the entire system.
  - Directly logging in as `root` grants access to all files, configurations, and commands, without any restrictions.
  - Common uses include:
    - Modifying critical system files.
    - Installing or removing software.
    - Managing user accounts and groups.
  - Risks:
    - Mistakes made as `root` can have catastrophic consequences, such as deleting important system files.
    - No logging of actions when directly logged in as `root`, making it harder to trace issues.

- **Key Differences**:
  1. **Access**:
     - `sudo` provides temporary elevated access for specific commands.
     - `root` has permanent access to all system functionalities.
  2. **Security**:
     - `sudo` is safer as it logs activities and restricts commands to authorized users.
     - Direct `root` login bypasses logging and can lead to accidental damage.
  3. **Usability**:
     - `sudo` is more user-friendly and doesn’t require switching accounts.
     - `root` requires the user to switch to the superuser account (e.g., `su` command).

- **Best Practices**:
  - Use `sudo` for administrative tasks instead of logging in as `root` to reduce risks.
  - Configure `sudoers` to grant necessary privileges without overexposing the system.

---

### **Q3. Explain the process of user management in Linux.**
**Introduction**:  
User management in Linux is essential for controlling system access and maintaining a secure environment in a multi-user system. Administrators can create, modify, and delete user accounts while defining their permissions and roles. The `/etc/passwd` file serves as the primary database for storing user account details.

**Answer**:
- **Adding a User**:
  - Command: `sudo adduser username`
    - This command creates a new user along with their home directory.
    - Default configuration files (e.g., `.bashrc`, `.profile`) are copied to the new user’s home directory.
  - Example:
    - `sudo adduser john`
      - Creates a user named `john` with `/home/john` as the home directory.

- **Modifying User Details**:
  - Command: `sudo usermod [options] username`
    - Used to update user details such as group membership, shell, or home directory.
  - Example:
    - `sudo usermod -aG sudo john`: Adds the user `john` to the `sudo` group, granting administrative privileges.

- **Deleting a User**:
  - Command: `sudo deluser username`
    - Removes the user account but leaves their home directory intact unless specified.
  - Command to delete the user and their home directory:
    - `sudo deluser --remove-home username`

- **Changing Password**:
  - Command: `sudo passwd username`
    - Allows updating the password for a specific user.
  - Example:
    - `sudo passwd john`: Updates the password for user `john`.

- **Viewing All Users**:
  - Command: `cat /etc/passwd`
    - Lists all user accounts on the system.

- **/etc/passwd File**:
  - Purpose: Stores user account information in a colon-separated format.
  - Each line represents a single user account with multiple fields.
  - **Structure**:
    - Example Line: `john:x:1001:1001:John Doe:/home/john:/bin/bash`
    - **Fields**:
      1. **Username**: `john` (the account name).
      2. **Encrypted password placeholder**: `x` (passwords are stored securely in `/etc/shadow`).
      3. **User ID (UID)**: `1001` (identifies the user).
      4. **Group ID (GID)**: `1001` (primary group associated with the user).
      5. **User Info**: `John Doe` (optional description or real name).
      6. **Home Directory**: `/home/john` (the default location for user files).
      7. **Shell**: `/bin/bash` (default shell assigned to the user).

- **Groups and Permissions**:
  - Groups are used to manage permissions for multiple users collectively.
  - Command to view groups: `groups username`.
  - Command to add a user to a group: `sudo usermod -aG groupname username`.

- **Best Practices**:
  1. Always use `sudo` for user management tasks to avoid accidental changes.
  2. Regularly audit `/etc/passwd` and `/etc/shadow` to ensure no unauthorized accounts exist.
  3. Enforce strong password policies by configuring `passwd` options (e.g., minimum length, expiration).


### **Q4. Explain the purpose of `uniq` and `sort` commands.**
**Introduction**:  
In Linux, `uniq` and `sort` are text processing commands used to manipulate data files. They help organize and filter data for better readability and analysis.

**Answer**:
- **`sort` Command**:
  - Purpose: Sorts data in ascending or descending order.
  - Syntax: `sort [options] file`
    - Options:  
      - `-n`: Sort numerically.  
      - `-r`: Reverse order.  
      - `-k`: Sort based on a specific field.
  - Example:
    - Input:
      ```
      apple:red:120
      orange:orange:80
      banana:yellow:50
      ```
    - Command: `sort file.txt`
    - Output:
      ```
      apple:red:120
      banana:yellow:50
      orange:orange:80
      ```
- **`uniq` Command**:
  - Purpose: Filters out duplicate lines from a file (requires sorted input).
  - Syntax: `uniq [options] file`
    - Options:  
      - `-c`: Counts occurrences of duplicate lines.  
      - `-u`: Displays only unique lines.
  - Example:
    - Input:
      ```
      apple:red:120
      apple:red:120
      banana:yellow:50
      ```
    - Command: `sort file.txt | uniq`
    - Output:
      ```
      apple:red:120
      banana:yellow:50
      ```

---

### **Q5. Explain the usage of the following commands.**
**Introduction**:  
Linux provides various commands to monitor and manage system resources, including disk usage, memory, and file properties. Below is a brief explanation of `du`, `df`, `free`, `touch`, and `stat`.

**Answer**:
1. **`du` (Disk Usage)**:
   - Displays the size of files and directories.
   - Syntax: `du [options] [directory]`
     - `-h`: Human-readable format.
     - `-s`: Summarizes the total size.
   - Example: `du -sh /home`
     - Output: `1.2G /home`

2. **`df` (Disk Free)**:
   - Shows disk space usage of mounted file systems.
   - Syntax: `df [options]`
     - `-h`: Human-readable format.
   - Example: `df -h`
     - Output:
       ```
       Filesystem      Size  Used Avail Use% Mounted on
       /dev/sda1        20G   15G  5G   75% /
       ```

3. **`free`**:
   - Displays system memory usage (RAM).
   - Syntax: `free [options]`
     - `-h`: Human-readable format.
   - Example: `free -h`
     - Output:
       ```
       total        used        free      shared  buff/cache   available
       16G          8G          4G        2G      4G           6G
       ```

4. **`touch`**:
   - Creates an empty file or updates the modification timestamp of an existing file.
   - Syntax: `touch filename`
   - Example: `touch newfile.txt`
     - Creates an empty file `newfile.txt` if it doesn’t exist.

5. **`stat`**:
   - Provides detailed information about a file or directory.
   - Syntax: `stat filename`
   - Example:
     - Command: `stat file.txt`
     - Output:
       ```
       File: file.txt
       Size: 1024       Blocks: 8          IO Block: 4096  regular file
       ```
