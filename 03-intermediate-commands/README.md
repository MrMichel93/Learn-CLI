# Intermediate CLI Commands and Concepts

Building on the basics, this section introduces more powerful commands and concepts.

## Text Processing and Searching

### `grep` - Search Text Patterns
Search for patterns in files or output.
```bash
$ grep "search_term" file.txt                # Search in file
$ grep -r "pattern" directory/               # Recursive search
$ grep -i "pattern" file.txt                 # Case-insensitive
$ grep -n "pattern" file.txt                 # Show line numbers
$ grep -v "pattern" file.txt                 # Invert match (show non-matching lines)
$ grep -E "pattern1|pattern2" file.txt       # Multiple patterns (regex)
```

### `find` - Search for Files and Directories
Locate files based on various criteria.
```bash
$ find . -name "*.txt"                       # Find .txt files in current dir
$ find /home -type f -name "*.log"           # Find log files
$ find . -type d -name "temp"                # Find directories named temp
$ find . -size +10M                          # Files larger than 10MB
$ find . -mtime -7                           # Modified in last 7 days
$ find . -name "*.tmp" -delete               # Find and delete
```

### `sed` - Stream Editor
Edit text in files or streams.
```bash
$ sed 's/old/new/' file.txt                  # Replace first occurrence per line
$ sed 's/old/new/g' file.txt                 # Replace all occurrences
$ sed -i 's/old/new/g' file.txt              # Edit file in-place
$ sed -n '10,20p' file.txt                   # Print lines 10-20
$ sed '/pattern/d' file.txt                  # Delete lines matching pattern
```

### `awk` - Pattern Scanning and Processing
Process and analyze text data.
```bash
$ awk '{print $1}' file.txt                  # Print first column
$ awk -F':' '{print $1}' /etc/passwd         # Use : as delimiter
$ awk '$3 > 100' file.txt                    # Print rows where column 3 > 100
$ awk '{sum+=$1} END {print sum}' file.txt   # Sum values in first column
```

### `sort` - Sort Lines
Sort text file contents.
```bash
$ sort file.txt                              # Alphabetical sort
$ sort -n file.txt                           # Numerical sort
$ sort -r file.txt                           # Reverse sort
$ sort -u file.txt                           # Sort and remove duplicates
```

### `uniq` - Report or Filter Duplicate Lines
Remove or count duplicate adjacent lines.
```bash
$ uniq file.txt                              # Remove duplicates
$ uniq -c file.txt                           # Count occurrences
$ uniq -d file.txt                           # Show only duplicates
```

### `wc` - Word Count
Count lines, words, and characters.
```bash
$ wc file.txt                                # Lines, words, characters
$ wc -l file.txt                             # Count lines only
$ wc -w file.txt                             # Count words only
$ wc -c file.txt                             # Count bytes
```

## File Permissions and Ownership

### Understanding Permissions
Every file has permissions for three categories:
- **Owner (u)** - the user who owns the file
- **Group (g)** - users in the file's group
- **Others (o)** - everyone else

Three permission types:
- **Read (r)** - view file contents or list directory
- **Write (w)** - modify file or add/remove files in directory
- **Execute (x)** - run file as program or access directory

```bash
$ ls -l file.txt
-rw-r--r-- 1 user group 1234 Dec 16 10:00 file.txt
```
This shows: `-rw-r--r--`
- `-` = regular file (d = directory, l = link)
- `rw-` = owner can read and write
- `r--` = group can read
- `r--` = others can read

### `chmod` - Change File Permissions
Modify file access permissions.
```bash
$ chmod u+x script.sh                        # Add execute for owner
$ chmod g-w file.txt                         # Remove write for group
$ chmod o+r file.txt                         # Add read for others
$ chmod 755 script.sh                        # Numeric: rwxr-xr-x
$ chmod 644 file.txt                         # Numeric: rw-r--r--
$ chmod -R 755 directory/                    # Recursive
```

Numeric permissions:
- 4 = read (r)
- 2 = write (w)
- 1 = execute (x)
- Sum them: 7=rwx, 6=rw-, 5=r-x, 4=r--, etc.

### `chown` - Change File Ownership
Change the owner and/or group of files.
```bash
$ sudo chown user file.txt                   # Change owner
$ sudo chown user:group file.txt             # Change owner and group
$ sudo chown -R user:group directory/        # Recursive
```

## Process Management

### `ps` - Process Status
Display currently running processes.
```bash
$ ps                                         # Your processes
$ ps aux                                     # All processes with details
$ ps aux | grep process_name                 # Find specific process
```

### `top` / `htop` - Interactive Process Viewer
Monitor system processes in real-time.
```bash
$ top                                        # Dynamic process viewer
$ htop                                       # Enhanced version (if installed)
```

### `kill` - Terminate Processes
Send signals to processes.
```bash
$ kill PID                                   # Gracefully terminate (SIGTERM)
$ kill -9 PID                                # Force kill (SIGKILL)
$ killall process_name                       # Kill by name
```

### Background and Foreground Jobs
```bash
$ command &                                  # Run in background
$ jobs                                       # List background jobs
$ fg %1                                      # Bring job 1 to foreground
$ bg %1                                      # Resume job 1 in background
$ Ctrl+Z                                     # Suspend current process
```

## Redirection and Pipes

### Output Redirection
```bash
$ command > file.txt                         # Redirect stdout (overwrite)
$ command >> file.txt                        # Redirect stdout (append)
$ command 2> error.txt                       # Redirect stderr
$ command &> all.txt                         # Redirect both stdout and stderr
$ command > output.txt 2>&1                  # Alternative for both
```

### Input Redirection
```bash
$ command < input.txt                        # Read from file
$ command << EOF                             # Here document
```

### Pipes (|)
Send output of one command as input to another.
```bash
$ ls -l | grep ".txt"                        # List only .txt files
$ cat file.txt | sort | uniq                 # Sort and remove duplicates
$ ps aux | grep python | wc -l              # Count Python processes
$ history | tail -n 20                       # Last 20 commands
```

## Archiving and Compression

### `tar` - Archive Files
Create and extract tar archives.
```bash
$ tar -cvf archive.tar directory/            # Create archive
$ tar -xvf archive.tar                       # Extract archive
$ tar -czvf archive.tar.gz directory/        # Create compressed (gzip)
$ tar -xzvf archive.tar.gz                   # Extract compressed
$ tar -cjvf archive.tar.bz2 directory/       # Create compressed (bzip2)
$ tar -tvf archive.tar                       # List contents
```

### `gzip` / `gunzip` - Compress Files
```bash
$ gzip file.txt                              # Compress (creates file.txt.gz)
$ gunzip file.txt.gz                         # Decompress
$ gzip -k file.txt                           # Keep original file
```

### `zip` / `unzip` - Zip Compression
```bash
$ zip archive.zip file1.txt file2.txt        # Create zip
$ zip -r archive.zip directory/              # Zip directory
$ unzip archive.zip                          # Extract zip
$ unzip -l archive.zip                       # List contents
```

## Network Commands

### `ping` - Test Network Connectivity
```bash
$ ping google.com                            # Test connection
$ ping -c 4 google.com                       # Send 4 packets only
```

### `curl` - Transfer Data from URLs
```bash
$ curl https://example.com                   # Download webpage
$ curl -O https://example.com/file.zip       # Download file
$ curl -I https://example.com                # Fetch headers only
```

### `wget` - Download Files
```bash
$ wget https://example.com/file.zip          # Download file
$ wget -r https://example.com                # Recursive download
```

### `ssh` - Secure Shell
Connect to remote systems.
```bash
$ ssh user@hostname                          # Connect to remote system
$ ssh user@hostname command                  # Run command remotely
$ ssh -p 2222 user@hostname                  # Use specific port
```

### `scp` - Secure Copy
Copy files between systems.
```bash
$ scp file.txt user@remote:/path/            # Copy to remote
$ scp user@remote:/path/file.txt .           # Copy from remote
$ scp -r directory/ user@remote:/path/       # Copy directory
```

---

## Mini Challenge: Text Processing and System Management

**Objective:** Apply intermediate commands to real-world scenarios involving text processing, file management, and system monitoring.

### Challenge 1: Log File Analysis

1. **Create a sample log file:**
   ```bash
   cat > app.log << 'EOF'
   2024-01-15 10:23:45 INFO Application started
   2024-01-15 10:24:12 ERROR Failed to connect to database
   2024-01-15 10:24:15 WARN Retrying connection
   2024-01-15 10:24:20 INFO Connected to database
   2024-01-15 10:25:30 ERROR Invalid user input
   2024-01-15 10:26:10 INFO Processing request
   2024-01-15 10:27:05 ERROR Network timeout
   2024-01-15 10:27:08 WARN Retry attempt 1
   2024-01-15 10:27:12 ERROR Network timeout
   2024-01-15 10:27:15 WARN Retry attempt 2
   EOF
   ```

2. **Analysis tasks:**
   - Count total lines in the log: `wc -l app.log`
   - Find all ERROR messages: `grep "ERROR" app.log`
   - Count how many errors occurred: `grep -c "ERROR" app.log`
   - Extract only the timestamp and message type: `awk '{print $1, $2, $3}' app.log`
   - Sort log entries by message type: `sort -k3 app.log`
   - Find unique message types: `awk '{print $3}' app.log | sort -u`

### Challenge 2: File Permission Management

1. **Create a test script:**
   ```bash
   echo '#!/bin/bash' > myscript.sh
   echo 'echo "Hello, World!"' >> myscript.sh
   ```

2. **Permission tasks:**
   - Check current permissions: `ls -l myscript.sh`
   - Make it executable: `chmod +x myscript.sh`
   - Run the script: `./myscript.sh`
   - Set specific permissions (rwxr-xr-x): `chmod 755 myscript.sh`
   - Remove execute permission from group and others: `chmod go-x myscript.sh`

### Challenge 3: Process and Pipeline Mastery

1. **Process exploration:**
   - View all running processes: `ps aux`
   - Find processes by name (e.g., "bash"): `ps aux | grep bash`
   - Count running processes: `ps aux | wc -l`
   - Monitor processes in real-time: `top` (press 'q' to quit)

2. **Pipeline challenges:**
   - List files, sort by size: `ls -lh | sort -k5 -h`
   - Find largest files: `du -h * | sort -h | tail -5`
   - Count specific file types: `ls | grep ".txt" | wc -l`
   - Create a sorted list of unique words from a file:
     ```bash
     echo "apple banana apple cherry banana apple" > fruits.txt
     cat fruits.txt | tr ' ' '\n' | sort | uniq -c
     ```

### Challenge 4: Archive and Network Operations

1. **Archiving tasks:**
   - Create a directory with files:
     ```bash
     mkdir backup_test
     touch backup_test/file{1..5}.txt
     ```
   - Create a tar.gz archive: `tar -czvf backup.tar.gz backup_test/`
   - List archive contents: `tar -tvf backup.tar.gz`
   - Extract to a new location:
     ```bash
     mkdir extracted
     tar -xzvf backup.tar.gz -C extracted/
     ```

2. **Network tasks:**
   - Test connectivity: `ping -c 4 google.com`
   - Download a webpage: `curl https://example.com > page.html`
   - Fetch only headers: `curl -I https://github.com`

### Challenge 5: Advanced Pipeline Project

**Build a data processing pipeline:**

1. Create a sample data file:
   ```bash
   cat > sales.csv << 'EOF'
   Product,Price,Quantity
   Apple,1.50,100
   Banana,0.75,150
   Cherry,2.00,80
   Date,3.50,50
   Elderberry,4.00,30
   EOF
   ```

2. Process the data:
   - Extract product names: `tail -n +2 sales.csv | cut -d',' -f1`
   - Calculate total inventory: `tail -n +2 sales.csv | cut -d',' -f3 | awk '{sum+=$1} END {print sum}'`
   - Sort by price: `tail -n +2 sales.csv | sort -t',' -k2 -n`
   - Find most expensive item: `tail -n +2 sales.csv | sort -t',' -k2 -n | tail -1`

### Success Criteria:
- ✅ You can search and filter text effectively with grep, awk, and sed
- ✅ You understand and can modify file permissions
- ✅ You can monitor and manage running processes
- ✅ You can chain commands with pipes to create powerful workflows
- ✅ You can create and extract archives
- ✅ You can use network tools to interact with remote systems

**Excellent work!** You've mastered intermediate CLI concepts. You're ready for advanced techniques!

---

[← Previous: Basic Commands](../02-basic-commands/README.md) | [Back to Main](../README.md) | [Next: Advanced Commands →](../04-advanced-commands/README.md)
