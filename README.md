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

---

### **Q2. Difference Between `sudo` and `root` in Linux**
**Introduction**:  
In Linux, administrative tasks require elevated privileges. Both `sudo` and `root` allow such privileges, but they serve distinct purposes in terms of access and security.

**Answer**:
- **`sudo` (Substitute User Do)**:
  - Temporary access to execute commands as another user, typically `root`.
  - Requires user authentication and is logged for auditing.
  - Example: `sudo apt update` updates the system with admin rights.
- **`root`**:
  - The default superuser account with unrestricted system access.
  - Direct login is discouraged due to potential system risks.
  - Used for tasks like adding users, modifying system files, or installing software.
- **Key Differences**:
  - **Access**: `sudo` grants temporary access; `root` has permanent privileges.
  - **Safety**: `sudo` is safer as it restricts usage and keeps a log of activities.

---

### **Q3. Explain the process of user management in Linux.**
**Introduction**:  
User management in Linux involves creating, modifying, and deleting user accounts to maintain system security and organization. The `/etc/passwd` file plays a central role in storing user information.

**Answer**:
- **Adding a User**: `sudo adduser username`
  - Creates a new user with default configurations and a home directory.
- **Deleting a User**: `sudo deluser username`
  - Removes the user account but retains files unless specified.
- **Changing Password**: `sudo passwd username`
  - Updates the password for a specific user.
- **/etc/passwd File**:
  - **Purpose**: Stores essential user account information.
  - **Structure**:
    - Each line contains user details separated by `:`.
    - Example: `john:x:1001:1001:John Doe:/home/john:/bin/bash`
    - **Fields**:
      1. Username (`john`).
      2. Encrypted password placeholder (`x`).
      3. User ID (UID): `1001`.
      4. Group ID (GID): `1001`.
      5. User description: `John Doe`.
      6. Home directory: `/home/john`.
      7. Default shell: `/bin/bash`.

---

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
