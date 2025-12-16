# Learn-CLI
Learn about and how to use the CLI to take full advantage of your computer.

## Table of Contents
1. [Introduction to the CLI](#1-introduction-to-the-cli)
2. [Basic CLI Commands and Concepts](#2-basic-cli-commands-and-concepts)
3. [Intermediate CLI Commands and Concepts](#3-intermediate-cli-commands-and-concepts)
4. [Advanced CLI Commands and Concepts](#4-advanced-cli-commands-and-concepts)

---

## 1. Introduction to the CLI

### What is the CLI?

The **CLI (Command-Line Interface)** is a text-based interface for interacting with your computer's operating system. Unlike graphical user interfaces (GUIs) that rely on windows, buttons, and menus, the CLI allows you to execute commands by typing text instructions directly into a terminal or console.

Common CLI environments include:
- **Bash** (Bourne Again Shell) - default on most Linux systems and macOS
- **Zsh** (Z Shell) - default on newer macOS versions
- **PowerShell** - Windows command-line interface
- **Command Prompt (cmd)** - traditional Windows CLI

### Why Learn to Use the CLI?

Learning the command line provides numerous advantages for both beginners and experienced users:

#### 1. **Efficiency and Speed**
- Execute complex tasks with a single command
- Automate repetitive operations with scripts
- Navigate and manipulate files faster than with GUI applications

#### 2. **Power and Flexibility**
- Access advanced system features not available in GUI tools
- Combine commands to create powerful workflows
- Fine-tune operations with precise parameters

#### 3. **Remote System Management**
- Manage servers and cloud systems (which often lack GUIs)
- Work efficiently over slow network connections
- Essential skill for DevOps, system administration, and cloud computing

#### 4. **Automation and Scripting**
- Create scripts to automate workflows
- Schedule tasks to run automatically
- Process large amounts of data efficiently

#### 5. **Universal Skill**
- CLI concepts are consistent across different operating systems
- Many professional tools are CLI-based or CLI-first
- Required for software development, data science, and many tech careers

#### 6. **Better Understanding of Your System**
- Learn how your computer actually works under the hood
- Troubleshoot problems more effectively
- Gain deeper control over system configurations

---

## 2. Basic CLI Commands and Concepts

This section covers fundamental commands you'll use daily when working in the terminal.

### Understanding the Command Prompt

When you open a terminal, you'll see a **prompt** that looks something like this:
```
user@hostname:~/directory$
```

- `user` - your username
- `hostname` - your computer's name
- `~/directory` - your current location (~ represents your home directory)
- `$` - indicates a regular user (# indicates root/admin)

### Basic Navigation Commands

#### `pwd` - Print Working Directory
Shows your current location in the filesystem.
```bash
$ pwd
/home/user/documents
```

#### `ls` - List Directory Contents
Displays files and directories in the current location.
```bash
$ ls                    # Basic listing
$ ls -l                 # Long format with details
$ ls -la                # Include hidden files (starting with .)
$ ls -lh                # Human-readable file sizes
```

#### `cd` - Change Directory
Navigate between directories.
```bash
$ cd /home/user/documents    # Absolute path
$ cd documents               # Relative path
$ cd ..                      # Move up one directory
$ cd ~                       # Go to home directory
$ cd -                       # Return to previous directory
```

### File and Directory Operations

#### `mkdir` - Make Directory
Create new directories.
```bash
$ mkdir my_folder
$ mkdir -p parent/child/grandchild    # Create nested directories
```

#### `touch` - Create Empty File
Create a new empty file or update timestamp of existing file.
```bash
$ touch newfile.txt
$ touch file1.txt file2.txt file3.txt    # Create multiple files
```

#### `cp` - Copy Files and Directories
Copy files or directories to a new location.
```bash
$ cp source.txt destination.txt          # Copy file
$ cp file.txt /path/to/directory/        # Copy to directory
$ cp -r folder1 folder2                  # Copy directory recursively
```

#### `mv` - Move or Rename Files
Move files to a new location or rename them.
```bash
$ mv oldname.txt newname.txt             # Rename file
$ mv file.txt /path/to/directory/        # Move file
$ mv *.txt documents/                    # Move all .txt files
```

#### `rm` - Remove Files and Directories
Delete files or directories (use with caution!).
```bash
$ rm file.txt                            # Remove file
$ rm -r directory/                       # Remove directory recursively
$ rm -i file.txt                         # Interactive (ask before delete)
$ rm -f file.txt                         # Force delete (no confirmation)
```

### Viewing File Contents

#### `cat` - Concatenate and Display Files
Display the entire contents of a file.
```bash
$ cat file.txt
$ cat file1.txt file2.txt    # Display multiple files
```

#### `less` - View File Page by Page
View large files with scrolling capability.
```bash
$ less largefile.txt
# Use arrow keys or Page Up/Down to navigate
# Press 'q' to quit
```

#### `head` - Display Beginning of File
Show the first lines of a file.
```bash
$ head file.txt              # First 10 lines (default)
$ head -n 20 file.txt        # First 20 lines
```

#### `tail` - Display End of File
Show the last lines of a file.
```bash
$ tail file.txt              # Last 10 lines (default)
$ tail -n 20 file.txt        # Last 20 lines
$ tail -f logfile.txt        # Follow file (useful for logs)
```

### Getting Help

#### `man` - Manual Pages
Access the manual/documentation for commands.
```bash
$ man ls                     # View manual for ls command
$ man man                    # Learn about the man command itself
```

#### `--help` Flag
Quick help for most commands.
```bash
$ ls --help
$ grep --help
```

### Wildcards and Pattern Matching

- `*` - Matches any characters
- `?` - Matches any single character
- `[]` - Matches any character in brackets

```bash
$ ls *.txt                   # All files ending in .txt
$ ls file?.txt               # file1.txt, file2.txt, etc.
$ ls [abc]*.txt              # Files starting with a, b, or c
```

### Practice Exercises

1. Create a directory structure: `projects/web/html` and `projects/web/css`
2. Create three empty files in the html directory: `index.html`, `about.html`, `contact.html`
3. List all files in long format with human-readable sizes
4. Copy `index.html` to the css directory and rename it to `styles.css`
5. View the contents of your `.bashrc` or `.bash_profile` file

---

## 3. Intermediate CLI Commands and Concepts

Building on the basics, this section introduces more powerful commands and concepts.

### Text Processing and Searching

#### `grep` - Search Text Patterns
Search for patterns in files or output.
```bash
$ grep "search_term" file.txt                # Search in file
$ grep -r "pattern" directory/               # Recursive search
$ grep -i "pattern" file.txt                 # Case-insensitive
$ grep -n "pattern" file.txt                 # Show line numbers
$ grep -v "pattern" file.txt                 # Invert match (show non-matching lines)
$ grep -E "pattern1|pattern2" file.txt       # Multiple patterns (regex)
```

#### `find` - Search for Files and Directories
Locate files based on various criteria.
```bash
$ find . -name "*.txt"                       # Find .txt files in current dir
$ find /home -type f -name "*.log"           # Find log files
$ find . -type d -name "temp"                # Find directories named temp
$ find . -size +10M                          # Files larger than 10MB
$ find . -mtime -7                           # Modified in last 7 days
$ find . -name "*.tmp" -delete               # Find and delete
```

#### `sed` - Stream Editor
Edit text in files or streams.
```bash
$ sed 's/old/new/' file.txt                  # Replace first occurrence per line
$ sed 's/old/new/g' file.txt                 # Replace all occurrences
$ sed -i 's/old/new/g' file.txt              # Edit file in-place
$ sed -n '10,20p' file.txt                   # Print lines 10-20
$ sed '/pattern/d' file.txt                  # Delete lines matching pattern
```

#### `awk` - Pattern Scanning and Processing
Process and analyze text data.
```bash
$ awk '{print $1}' file.txt                  # Print first column
$ awk -F':' '{print $1}' /etc/passwd         # Use : as delimiter
$ awk '$3 > 100' file.txt                    # Print rows where column 3 > 100
$ awk '{sum+=$1} END {print sum}' file.txt   # Sum values in first column
```

#### `sort` - Sort Lines
Sort text file contents.
```bash
$ sort file.txt                              # Alphabetical sort
$ sort -n file.txt                           # Numerical sort
$ sort -r file.txt                           # Reverse sort
$ sort -u file.txt                           # Sort and remove duplicates
```

#### `uniq` - Report or Filter Duplicate Lines
Remove or count duplicate adjacent lines.
```bash
$ uniq file.txt                              # Remove duplicates
$ uniq -c file.txt                           # Count occurrences
$ uniq -d file.txt                           # Show only duplicates
```

#### `wc` - Word Count
Count lines, words, and characters.
```bash
$ wc file.txt                                # Lines, words, characters
$ wc -l file.txt                             # Count lines only
$ wc -w file.txt                             # Count words only
$ wc -c file.txt                             # Count bytes
```

### File Permissions and Ownership

#### Understanding Permissions
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

#### `chmod` - Change File Permissions
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

#### `chown` - Change File Ownership
Change the owner and/or group of files.
```bash
$ sudo chown user file.txt                   # Change owner
$ sudo chown user:group file.txt             # Change owner and group
$ sudo chown -R user:group directory/        # Recursive
```

### Process Management

#### `ps` - Process Status
Display currently running processes.
```bash
$ ps                                         # Your processes
$ ps aux                                     # All processes with details
$ ps aux | grep process_name                 # Find specific process
```

#### `top` / `htop` - Interactive Process Viewer
Monitor system processes in real-time.
```bash
$ top                                        # Dynamic process viewer
$ htop                                       # Enhanced version (if installed)
```

#### `kill` - Terminate Processes
Send signals to processes.
```bash
$ kill PID                                   # Gracefully terminate (SIGTERM)
$ kill -9 PID                                # Force kill (SIGKILL)
$ killall process_name                       # Kill by name
```

#### Background and Foreground Jobs
```bash
$ command &                                  # Run in background
$ jobs                                       # List background jobs
$ fg %1                                      # Bring job 1 to foreground
$ bg %1                                      # Resume job 1 in background
$ Ctrl+Z                                     # Suspend current process
```

### Redirection and Pipes

#### Output Redirection
```bash
$ command > file.txt                         # Redirect stdout (overwrite)
$ command >> file.txt                        # Redirect stdout (append)
$ command 2> error.txt                       # Redirect stderr
$ command &> all.txt                         # Redirect both stdout and stderr
$ command > output.txt 2>&1                  # Alternative for both
```

#### Input Redirection
```bash
$ command < input.txt                        # Read from file
$ command << EOF                             # Here document
```

#### Pipes (|)
Send output of one command as input to another.
```bash
$ ls -l | grep ".txt"                        # List only .txt files
$ cat file.txt | sort | uniq                 # Sort and remove duplicates
$ ps aux | grep python | wc -l              # Count Python processes
$ history | tail -n 20                       # Last 20 commands
```

### Archiving and Compression

#### `tar` - Archive Files
Create and extract tar archives.
```bash
$ tar -cvf archive.tar directory/            # Create archive
$ tar -xvf archive.tar                       # Extract archive
$ tar -czvf archive.tar.gz directory/        # Create compressed (gzip)
$ tar -xzvf archive.tar.gz                   # Extract compressed
$ tar -cjvf archive.tar.bz2 directory/       # Create compressed (bzip2)
$ tar -tvf archive.tar                       # List contents
```

#### `gzip` / `gunzip` - Compress Files
```bash
$ gzip file.txt                              # Compress (creates file.txt.gz)
$ gunzip file.txt.gz                         # Decompress
$ gzip -k file.txt                           # Keep original file
```

#### `zip` / `unzip` - Zip Compression
```bash
$ zip archive.zip file1.txt file2.txt        # Create zip
$ zip -r archive.zip directory/              # Zip directory
$ unzip archive.zip                          # Extract zip
$ unzip -l archive.zip                       # List contents
```

### Network Commands

#### `ping` - Test Network Connectivity
```bash
$ ping google.com                            # Test connection
$ ping -c 4 google.com                       # Send 4 packets only
```

#### `curl` - Transfer Data from URLs
```bash
$ curl https://example.com                   # Download webpage
$ curl -O https://example.com/file.zip       # Download file
$ curl -I https://example.com                # Fetch headers only
```

#### `wget` - Download Files
```bash
$ wget https://example.com/file.zip          # Download file
$ wget -r https://example.com                # Recursive download
```

#### `ssh` - Secure Shell
Connect to remote systems.
```bash
$ ssh user@hostname                          # Connect to remote system
$ ssh user@hostname command                  # Run command remotely
$ ssh -p 2222 user@hostname                  # Use specific port
```

#### `scp` - Secure Copy
Copy files between systems.
```bash
$ scp file.txt user@remote:/path/            # Copy to remote
$ scp user@remote:/path/file.txt .           # Copy from remote
$ scp -r directory/ user@remote:/path/       # Copy directory
```

### Practice Exercises

1. Find all `.log` files in `/var/log` modified in the last 24 hours
2. Count how many lines contain the word "error" in a log file
3. Create a tar.gz archive of your home directory's documents folder
4. Change permissions on a script to make it executable for everyone
5. Use pipes to find the 10 largest files in a directory
6. Monitor running processes and identify the most CPU-intensive one

---

## 4. Advanced CLI Commands and Concepts

This section covers sophisticated techniques for power users.

### Shell Scripting Basics

Shell scripts automate sequences of commands and can include logic, loops, and functions.

#### Creating a Simple Script
```bash
#!/bin/bash
# My first script

echo "Hello, World!"
echo "Current directory: $(pwd)"
echo "Current user: $USER"
```

Save as `script.sh`, make executable with `chmod +x script.sh`, then run with `./script.sh`

#### Variables
```bash
#!/bin/bash

NAME="John"
AGE=25
echo "Name: $NAME, Age: $AGE"

# Command substitution
FILES=$(ls | wc -l)
echo "Number of files: $FILES"

# Reading user input
read -p "Enter your name: " USERNAME
echo "Hello, $USERNAME"
```

#### Conditionals
```bash
#!/bin/bash

if [ -f "file.txt" ]; then
    echo "File exists"
else
    echo "File does not exist"
fi

# Numeric comparison
if [ $AGE -gt 18 ]; then
    echo "Adult"
else
    echo "Minor"
fi

# String comparison
if [ "$NAME" = "John" ]; then
    echo "Hello John"
fi
```

#### Loops
```bash
#!/bin/bash

# For loop
for i in 1 2 3 4 5; do
    echo "Number: $i"
done

# For loop with range
for i in {1..10}; do
    echo "Count: $i"
done

# For loop through files
for file in *.txt; do
    echo "Processing $file"
done

# While loop
counter=1
while [ $counter -le 5 ]; do
    echo "Counter: $counter"
    ((counter++))
done

# Reading file line by line
while IFS= read -r line; do
    echo "Line: $line"
done < file.txt
```

#### Functions
```bash
#!/bin/bash

# Define function
greet() {
    echo "Hello, $1!"
}

# Call function
greet "Alice"
greet "Bob"

# Function with return value
add_numbers() {
    local sum=$(($1 + $2))
    echo $sum
}

result=$(add_numbers 5 3)
echo "Sum: $result"
```

#### Command-Line Arguments
```bash
#!/bin/bash

echo "Script name: $0"
echo "First argument: $1"
echo "Second argument: $2"
echo "All arguments: $@"
echo "Number of arguments: $#"

# Check if argument provided
if [ $# -eq 0 ]; then
    echo "No arguments provided"
    exit 1
fi
```

### Advanced Text Processing

#### Regular Expressions with grep
```bash
$ grep -E '^[A-Z]' file.txt                  # Lines starting with capital letter
$ grep -E '[0-9]{3}-[0-9]{4}' file.txt       # Phone number pattern
$ grep -E '(error|warning|critical)' log.txt # Multiple patterns
$ grep -P '\d+\.\d+\.\d+\.\d+' file.txt     # IP addresses (Perl regex)
```

#### Advanced sed Techniques
```bash
# Multiple substitutions
$ sed -e 's/old/new/g' -e 's/foo/bar/g' file.txt

# Conditional substitution
$ sed '/pattern/s/old/new/g' file.txt

# Delete blank lines
$ sed '/^$/d' file.txt

# Insert text before/after pattern
$ sed '/pattern/i\New line before' file.txt
$ sed '/pattern/a\New line after' file.txt

# Extract lines between patterns
$ sed -n '/START/,/END/p' file.txt
```

#### Advanced awk Programming
```bash
# Begin and end blocks
$ awk 'BEGIN {print "Start"} {print $0} END {print "End"}' file.txt

# Conditional processing
$ awk '{if ($3 > 100) print $1, $3}' file.txt

# Using variables
$ awk '{sum += $1; count++} END {print sum/count}' file.txt

# Multiple field separators
$ awk -F'[,:]' '{print $1, $3}' file.txt

# Formatted output
$ awk '{printf "%-10s %5d\n", $1, $2}' file.txt
```

### Process and System Management

#### `systemctl` - System Control (systemd)
Manage system services.
```bash
$ sudo systemctl start service_name          # Start service
$ sudo systemctl stop service_name           # Stop service
$ sudo systemctl restart service_name        # Restart service
$ sudo systemctl status service_name         # Check status
$ sudo systemctl enable service_name         # Enable at boot
$ sudo systemctl disable service_name        # Disable at boot
```

#### `df` - Disk Space Usage
```bash
$ df -h                                      # Human-readable disk usage
$ df -h /home                                # Specific filesystem
$ df -i                                      # Inode usage
```

#### `du` - Directory Disk Usage
```bash
$ du -h directory/                           # Directory size
$ du -sh directory/                          # Summary only
$ du -h --max-depth=1                        # One level deep
$ du -sh * | sort -h                         # Sorted by size
```

#### `free` - Memory Usage
```bash
$ free -h                                    # Human-readable memory usage
$ free -h -s 5                               # Update every 5 seconds
```

#### `lsof` - List Open Files
```bash
$ lsof                                       # All open files
$ lsof -u username                           # Files opened by user
$ lsof -i :80                                # What's using port 80
$ lsof -c process_name                       # Files opened by process
```

#### `netstat` / `ss` - Network Statistics
```bash
$ netstat -tuln                              # Listening ports
$ netstat -an                                # All connections
$ ss -tuln                                   # Modern alternative
$ ss -s                                      # Summary statistics
```

### Advanced File Operations

#### `rsync` - Efficient File Synchronization
```bash
$ rsync -av source/ destination/             # Archive mode, verbose
$ rsync -avz source/ user@remote:/path/      # With compression
$ rsync -av --delete source/ destination/    # Delete extra files
$ rsync -av --progress source/ destination/  # Show progress
$ rsync -av --exclude='*.tmp' src/ dest/     # Exclude patterns
```

#### `ln` - Create Links
```bash
$ ln -s /path/to/file link_name              # Symbolic (soft) link
$ ln /path/to/file link_name                 # Hard link
```

#### `diff` - Compare Files
```bash
$ diff file1.txt file2.txt                   # Show differences
$ diff -u file1.txt file2.txt                # Unified format
$ diff -r dir1/ dir2/                        # Recursive directory diff
```

### Command-Line Productivity

#### `alias` - Create Command Shortcuts
```bash
$ alias ll='ls -la'                          # Create alias
$ alias gs='git status'
$ alias ..='cd ..'
$ unalias ll                                 # Remove alias

# Add to ~/.bashrc or ~/.zshrc to make permanent
```

#### `history` - Command History
```bash
$ history                                    # Show command history
$ history | grep command                     # Search history
$ !123                                       # Run command number 123
$ !!                                         # Run last command
$ !$                                         # Last argument of last command
$ Ctrl+R                                     # Reverse search history
```

#### Command Substitution
```bash
$ echo "Today is $(date)"
$ files=$(find . -name "*.txt")
$ echo "Found $(ls | wc -l) files"
```

#### Brace Expansion
```bash
$ echo {1..10}                               # 1 2 3 4 5 6 7 8 9 10
$ echo {a..z}                                # a b c ... z
$ mkdir -p project/{src,bin,docs,tests}      # Create multiple directories
$ cp file.txt{,.backup}                      # cp file.txt file.txt.backup
$ mv file.{txt,md}                           # mv file.txt file.md
```

#### `xargs` - Build and Execute Commands
```bash
$ find . -name "*.tmp" | xargs rm            # Delete all .tmp files
$ echo "file1 file2 file3" | xargs -n 1 cat # Process one at a time
$ cat urls.txt | xargs -I {} curl {}         # Replace {} with input
$ find . -type f | xargs -P 4 grep "pattern" # Parallel execution
```

### Advanced Shell Features

#### Job Control
```bash
$ command &                                  # Run in background
$ nohup command &                            # Run immune to hangups
$ disown %1                                  # Detach job from shell
$ screen                                     # Terminal multiplexer
$ tmux                                       # Modern alternative to screen
```

#### Here Documents and Here Strings
```bash
# Here document
$ cat << EOF > file.txt
Line 1
Line 2
Line 3
EOF

# Here string
$ grep "pattern" <<< "string to search"
```

#### Command Grouping
```bash
$ (cd /tmp && ls)                            # Run in subshell
$ { cd /tmp; ls; }                           # Run in current shell
```

#### `tee` - Read from stdin and Write to stdout and Files
```bash
$ command | tee output.txt                   # Display and save
$ command | tee -a output.txt                # Display and append
$ command | tee file1.txt file2.txt         # Write to multiple files
```

### Text Editors in Terminal

#### `vim` / `vi` - Powerful Text Editor
```bash
$ vim file.txt
# Basic commands:
# i - insert mode
# Esc - normal mode
# :w - save
# :q - quit
# :wq - save and quit
# :q! - quit without saving
# dd - delete line
# yy - copy line
# p - paste
# /pattern - search
```

#### `nano` - Simple Text Editor
```bash
$ nano file.txt
# Ctrl+O - save
# Ctrl+X - exit
# Ctrl+K - cut line
# Ctrl+U - paste
# Ctrl+W - search
```

### Environment Variables

#### Working with Environment Variables
```bash
$ echo $PATH                                 # Display PATH
$ echo $HOME                                 # Home directory
$ echo $USER                                 # Current user
$ export VAR="value"                         # Set environment variable
$ env                                        # List all environment variables
$ export PATH=$PATH:/new/path                # Add to PATH

# Permanent variables: add to ~/.bashrc or ~/.bash_profile
echo 'export VAR="value"' >> ~/.bashrc
```

### Advanced Debugging and Troubleshooting

#### `strace` - Trace System Calls
```bash
$ strace command                             # Trace system calls
$ strace -c command                          # Summary of calls
$ strace -p PID                              # Trace running process
```

#### `ltrace` - Trace Library Calls
```bash
$ ltrace command                             # Trace library calls
```

#### Bash Debugging
```bash
$ bash -x script.sh                          # Debug mode
$ set -x                                     # Enable debugging
$ set +x                                     # Disable debugging
$ set -e                                     # Exit on error
$ set -u                                     # Exit on undefined variable
```

### Performance and Monitoring

#### `time` - Measure Command Execution Time
```bash
$ time command                               # Show real, user, sys time
$ /usr/bin/time -v command                   # Detailed statistics
```

#### `watch` - Execute Command Periodically
```bash
$ watch ls -l                                # Run every 2 seconds
$ watch -n 5 df -h                           # Run every 5 seconds
$ watch -d command                           # Highlight differences
```

#### `iostat` - I/O Statistics
```bash
$ iostat                                     # CPU and I/O stats
$ iostat -x 5                                # Extended stats every 5 seconds
```

### Package Management (Linux)

#### Debian/Ubuntu (apt)
```bash
$ sudo apt update                            # Update package lists
$ sudo apt upgrade                           # Upgrade packages
$ sudo apt install package_name              # Install package
$ sudo apt remove package_name               # Remove package
$ apt search package_name                    # Search packages
$ apt show package_name                      # Show package info
```

#### Red Hat/CentOS (yum/dnf)
```bash
$ sudo yum update                            # Update packages
$ sudo yum install package_name              # Install package
$ sudo yum remove package_name               # Remove package
$ yum search package_name                    # Search packages
```

#### macOS (Homebrew)
```bash
$ brew update                                # Update Homebrew
$ brew install package_name                  # Install package
$ brew uninstall package_name                # Uninstall package
$ brew search package_name                   # Search packages
$ brew list                                  # List installed packages
```

### Advanced Practice Exercises

1. Write a script that backs up a directory, compresses it, and names it with the current date
2. Create a log monitoring script that alerts when specific error patterns appear
3. Write a script that finds and removes duplicate files based on content (using checksums)
4. Set up a cron job to run a maintenance script daily at midnight
5. Create a function to parse and format JSON data from a REST API using `curl` and `jq`
6. Write a script that monitors system resources and sends an alert when usage exceeds thresholds
7. Build a deployment script that syncs files to remote servers with error handling

---

## Additional Resources

### Online Learning Platforms
- [Linux Journey](https://linuxjourney.com/) - Interactive Linux tutorials
- [Command Line Challenge](https://cmdchallenge.com/) - Practice CLI skills
- [OverTheWire](https://overthewire.org/wargames/) - Security-focused CLI challenges
- [Bash Academy](https://www.bash.academy/) - Comprehensive Bash guide

### Books
- "The Linux Command Line" by William Shotts
- "Learning the bash Shell" by Cameron Newham
- "Unix Power Tools" by Shelley Powers, et al.

### Cheat Sheets
- [Devhints](https://devhints.io/bash) - Bash cheat sheet
- [TLDR Pages](https://tldr.sh/) - Simplified man pages
- [Explain Shell](https://explainshell.com/) - Break down command syntax

### Tips for Continued Learning

1. **Practice Daily** - Use the CLI for everyday tasks instead of GUI tools
2. **Read Man Pages** - Explore command documentation with `man command`
3. **Experiment Safely** - Use virtual machines or containers for testing
4. **Learn from Errors** - Error messages are learning opportunities
5. **Automate Repetitive Tasks** - Write scripts to save time
6. **Join Communities** - Participate in forums like Stack Overflow, Reddit's r/commandline
7. **Explore Others' Scripts** - Study shell scripts on GitHub
8. **Build Projects** - Create useful tools and utilities

---

## Conclusion

Mastering the command line is a journey that takes practice and patience. Start with the basics, gradually incorporate intermediate techniques into your workflow, and challenge yourself with advanced concepts. The CLI is an incredibly powerful tool that will make you more efficient, give you deeper control over your systems, and open doors to advanced computing careers.

Remember: every expert was once a beginner. Don't be afraid to make mistakes—they're part of the learning process. Keep practicing, stay curious, and enjoy your command-line journey!

**Happy Learning! 🚀**
