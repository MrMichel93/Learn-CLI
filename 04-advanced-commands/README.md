# Advanced CLI Commands and Concepts

This section covers sophisticated techniques for power users.

## Shell Scripting Basics

Shell scripts automate sequences of commands and can include logic, loops, and functions.

### Creating a Simple Script
```bash
#!/bin/bash
# My first script

echo "Hello, World!"
echo "Current directory: $(pwd)"
echo "Current user: $USER"
```

Save as `script.sh`, make executable with `chmod +x script.sh`, then run with `./script.sh`

### Variables
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

### Conditionals
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

### Loops
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

### Functions
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

### Command-Line Arguments
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

## Advanced Text Processing

### Regular Expressions with grep
```bash
$ grep -E '^[A-Z]' file.txt                  # Lines starting with capital letter
$ grep -E '[0-9]{3}-[0-9]{4}' file.txt       # Phone number pattern
$ grep -E '(error|warning|critical)' log.txt # Multiple patterns
$ grep -P '\d+\.\d+\.\d+\.\d+' file.txt     # IP addresses (Perl regex)
```

### Advanced sed Techniques
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

### Advanced awk Programming
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

## Process and System Management

### `systemctl` - System Control (systemd)
Manage system services.
```bash
$ sudo systemctl start service_name          # Start service
$ sudo systemctl stop service_name           # Stop service
$ sudo systemctl restart service_name        # Restart service
$ sudo systemctl status service_name         # Check status
$ sudo systemctl enable service_name         # Enable at boot
$ sudo systemctl disable service_name        # Disable at boot
```

### `df` - Disk Space Usage
```bash
$ df -h                                      # Human-readable disk usage
$ df -h /home                                # Specific filesystem
$ df -i                                      # Inode usage
```

### `du` - Directory Disk Usage
```bash
$ du -h directory/                           # Directory size
$ du -sh directory/                          # Summary only
$ du -h --max-depth=1                        # One level deep
$ du -sh * | sort -h                         # Sorted by size
```

### `free` - Memory Usage
```bash
$ free -h                                    # Human-readable memory usage
$ free -h -s 5                               # Update every 5 seconds
```

### `lsof` - List Open Files
```bash
$ lsof                                       # All open files
$ lsof -u username                           # Files opened by user
$ lsof -i :80                                # What's using port 80
$ lsof -c process_name                       # Files opened by process
```

### `netstat` / `ss` - Network Statistics
```bash
$ netstat -tuln                              # Listening ports
$ netstat -an                                # All connections
$ ss -tuln                                   # Modern alternative
$ ss -s                                      # Summary statistics
```

## Advanced File Operations

### `rsync` - Efficient File Synchronization
```bash
$ rsync -av source/ destination/             # Archive mode, verbose
$ rsync -avz source/ user@remote:/path/      # With compression
$ rsync -av --delete source/ destination/    # Delete extra files
$ rsync -av --progress source/ destination/  # Show progress
$ rsync -av --exclude='*.tmp' src/ dest/     # Exclude patterns
```

### `ln` - Create Links
```bash
$ ln -s /path/to/file link_name              # Symbolic (soft) link
$ ln /path/to/file link_name                 # Hard link
```

### `diff` - Compare Files
```bash
$ diff file1.txt file2.txt                   # Show differences
$ diff -u file1.txt file2.txt                # Unified format
$ diff -r dir1/ dir2/                        # Recursive directory diff
```

## Command-Line Productivity

### `alias` - Create Command Shortcuts
```bash
$ alias ll='ls -la'                          # Create alias
$ alias gs='git status'
$ alias ..='cd ..'
$ unalias ll                                 # Remove alias

# Add to ~/.bashrc or ~/.zshrc to make permanent
```

### `history` - Command History
```bash
$ history                                    # Show command history
$ history | grep command                     # Search history
$ !123                                       # Run command number 123
$ !!                                         # Run last command
$ !$                                         # Last argument of last command
$ Ctrl+R                                     # Reverse search history
```

### Command Substitution
```bash
$ echo "Today is $(date)"
$ files=$(find . -name "*.txt")
$ echo "Found $(ls | wc -l) files"
```

### Brace Expansion
```bash
$ echo {1..10}                               # 1 2 3 4 5 6 7 8 9 10
$ echo {a..z}                                # a b c ... z
$ mkdir -p project/{src,bin,docs,tests}      # Create multiple directories
$ cp file.txt{,.backup}                      # cp file.txt file.txt.backup
$ mv file.{txt,md}                           # mv file.txt file.md
```

### `xargs` - Build and Execute Commands
```bash
$ find . -name "*.tmp" | xargs rm            # Delete all .tmp files
$ echo "file1 file2 file3" | xargs -n 1 cat # Process one at a time
$ cat urls.txt | xargs -I {} curl {}         # Replace {} with input
$ find . -type f | xargs -P 4 grep "pattern" # Parallel execution
```

## Advanced Shell Features

### Job Control
```bash
$ command &                                  # Run in background
$ nohup command &                            # Run immune to hangups
$ disown %1                                  # Detach job from shell
$ screen                                     # Terminal multiplexer
$ tmux                                       # Modern alternative to screen
```

### Here Documents and Here Strings
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

### Command Grouping
```bash
$ (cd /tmp && ls)                            # Run in subshell
$ { cd /tmp; ls; }                           # Run in current shell
```

### `tee` - Read from stdin and Write to stdout and Files
```bash
$ command | tee output.txt                   # Display and save
$ command | tee -a output.txt                # Display and append
$ command | tee file1.txt file2.txt         # Write to multiple files
```

## Text Editors in Terminal

### `vim` / `vi` - Powerful Text Editor
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

### `nano` - Simple Text Editor
```bash
$ nano file.txt
# Ctrl+O - save
# Ctrl+X - exit
# Ctrl+K - cut line
# Ctrl+U - paste
# Ctrl+W - search
```

## Environment Variables

### Working with Environment Variables
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

## Advanced Debugging and Troubleshooting

### `strace` - Trace System Calls
```bash
$ strace command                             # Trace system calls
$ strace -c command                          # Summary of calls
$ strace -p PID                              # Trace running process
```

### `ltrace` - Trace Library Calls
```bash
$ ltrace command                             # Trace library calls
```

### Bash Debugging
```bash
$ bash -x script.sh                          # Debug mode (show each command)
$ set -x                                     # Enable debugging in script
$ set +x                                     # Disable debugging in script
$ set -e                                     # Exit immediately on error (fail fast)
$ set -u                                     # Exit on undefined variable usage
$ set -o pipefail                            # Return error if any pipeline command fails
```

Common debugging practice:
```bash
#!/bin/bash
set -euo pipefail  # Strict mode: exit on error, undefined vars, pipe failures

# Your script here
```

## Performance and Monitoring

### `time` - Measure Command Execution Time
```bash
$ time command                               # Show real, user, sys time
$ /usr/bin/time -v command                   # Detailed statistics
```

### `watch` - Execute Command Periodically
```bash
$ watch ls -l                                # Run every 2 seconds
$ watch -n 5 df -h                           # Run every 5 seconds
$ watch -d command                           # Highlight differences
```

### `iostat` - I/O Statistics
```bash
$ iostat                                     # CPU and I/O stats
$ iostat -x 5                                # Extended stats every 5 seconds
```

## Package Management (Linux)

### Debian/Ubuntu (apt)
```bash
$ sudo apt update                            # Update package lists
$ sudo apt upgrade                           # Upgrade packages
$ sudo apt install package_name              # Install package
$ sudo apt remove package_name               # Remove package
$ apt search package_name                    # Search packages
$ apt show package_name                      # Show package info
```

### Red Hat/CentOS (yum/dnf)
```bash
$ sudo yum update                            # Update packages
$ sudo yum install package_name              # Install package
$ sudo yum remove package_name               # Remove package
$ yum search package_name                    # Search packages
```

### macOS (Homebrew)
```bash
$ brew update                                # Update Homebrew
$ brew install package_name                  # Install package
$ brew uninstall package_name                # Uninstall package
$ brew search package_name                   # Search packages
$ brew list                                  # List installed packages
```

## Scheduling Tasks with Cron

Cron allows you to schedule commands to run automatically at specified times.

```bash
$ crontab -e                                 # Edit cron jobs
$ crontab -l                                 # List cron jobs
$ crontab -r                                 # Remove all cron jobs
```

Cron syntax: `minute hour day month weekday command`
```
# Example cron entries:
0 0 * * * /path/to/backup.sh                 # Daily at midnight
30 2 * * 0 /path/to/weekly.sh                # Weekly on Sunday at 2:30 AM
0 */6 * * * /path/to/script.sh               # Every 6 hours
*/15 * * * * /path/to/monitor.sh             # Every 15 minutes
0 9 1 * * /path/to/monthly.sh                # First day of month at 9 AM
```

## Working with JSON Data

### `jq` - JSON Processor
Parse and manipulate JSON data from APIs and files.
```bash
$ curl api.example.com/data | jq '.'         # Pretty-print JSON
$ echo '{"name":"John","age":30}' | jq '.name'  # Extract field
$ jq '.[] | .name' data.json                 # Array processing
$ jq '.users[] | select(.age > 25)' data.json   # Filter data
$ jq -r '.name' data.json                    # Raw output (no quotes)
```

---

## Mini Challenge: Building Real-World Automation

**Objective:** Create practical automation scripts and manage complex system tasks.

### Challenge 1: System Backup Script

Create a comprehensive backup script:

```bash
#!/bin/bash
# backup.sh - Automated backup script

set -euo pipefail

# Configuration
BACKUP_SOURCE="$HOME/documents"
BACKUP_DEST="$HOME/backups"
DATE=$(date +%Y%m%d_%H%M%S)
BACKUP_NAME="backup_${DATE}.tar.gz"

# Create backup directory if it doesn't exist
mkdir -p "$BACKUP_DEST"

# Create backup
echo "Starting backup of $BACKUP_SOURCE..."
tar -czf "$BACKUP_DEST/$BACKUP_NAME" "$BACKUP_SOURCE"

# Verify backup was created
if [ -f "$BACKUP_DEST/$BACKUP_NAME" ]; then
    echo "Backup completed: $BACKUP_NAME"
    ls -lh "$BACKUP_DEST/$BACKUP_NAME"
else
    echo "Backup failed!"
    exit 1
fi

# Optional: Remove backups older than 7 days
find "$BACKUP_DEST" -name "backup_*.tar.gz" -mtime +7 -delete
echo "Old backups cleaned up"
```

**Tasks:**
1. Create and test the backup script
2. Make it executable: `chmod +x backup.sh`
3. Run it: `./backup.sh`
4. Modify it to accept command-line arguments for source and destination
5. Add error handling for missing directories

### Challenge 2: Log Monitor Script

Create a log monitoring script that alerts on errors:

```bash
#!/bin/bash
# monitor.sh - Log monitoring script

LOGFILE="/var/log/syslog"  # Adjust for your system
ALERT_PATTERN="error|fail|critical"

# Check if log file exists
if [ ! -f "$LOGFILE" ]; then
    echo "Log file not found: $LOGFILE"
    exit 1
fi

# Monitor for errors in the last 100 lines
ERRORS=$(tail -n 100 "$LOGFILE" | grep -iE "$ALERT_PATTERN" | wc -l)

echo "Found $ERRORS error(s) in the last 100 lines"

if [ $ERRORS -gt 0 ]; then
    echo "Recent errors:"
    tail -n 100 "$LOGFILE" | grep -iE "$ALERT_PATTERN"
fi
```

**Tasks:**
1. Create a test log file with sample entries
2. Run the monitor script
3. Enhance it to send email notifications (using `mail` or `sendmail`)
4. Schedule it to run every 15 minutes using cron

### Challenge 3: Disk Usage Reporter

Create a script that reports disk usage:

```bash
#!/bin/bash
# disk_report.sh - Disk usage reporter

THRESHOLD=80

echo "Disk Usage Report - $(date)"
echo "================================"

df -h | tail -n +2 | while read line; do
    usage=$(echo $line | awk '{print $5}' | sed 's/%//')
    filesystem=$(echo $line | awk '{print $1}')
    
    if [ "$usage" -ge "$THRESHOLD" ]; then
        echo "⚠️  WARNING: $filesystem is at ${usage}%"
    else
        echo "✓ OK: $filesystem is at ${usage}%"
    fi
done

echo ""
echo "Top 10 Largest Directories:"
du -h ~ --max-depth=1 2>/dev/null | sort -hr | head -10
```

**Tasks:**
1. Run the disk usage reporter
2. Modify the threshold value
3. Add a feature to send alerts when threshold is exceeded
4. Create a version that outputs to a file with timestamp

### Challenge 4: API Data Processing

Work with JSON data from APIs:

```bash
# Create sample JSON data
cat > users.json << 'EOF'
{
  "users": [
    {"id": 1, "name": "Alice", "age": 28, "active": true},
    {"id": 2, "name": "Bob", "age": 34, "active": false},
    {"id": 3, "name": "Charlie", "age": 22, "active": true},
    {"id": 4, "name": "Diana", "age": 29, "active": true}
  ]
}
EOF
```

**Tasks:**
1. Install jq if not available: `sudo apt install jq` (or `brew install jq` on macOS)
2. Extract all user names: `jq '.users[].name' users.json`
3. Filter active users: `jq '.users[] | select(.active == true)' users.json`
4. Calculate average age: `jq '[.users[].age] | add/length' users.json`
5. Create a CSV from JSON:
   ```bash
   echo "ID,Name,Age,Active" > users.csv
   jq -r '.users[] | [.id, .name, .age, .active] | @csv' users.json >> users.csv
   ```

### Challenge 5: Automated Deployment Script

Create a deployment automation script:

```bash
#!/bin/bash
# deploy.sh - Simple deployment script

set -euo pipefail

PROJECT_DIR="/path/to/project"
REMOTE_USER="user"
REMOTE_HOST="example.com"
REMOTE_DIR="/var/www/html"

echo "Starting deployment..."

# Check if project directory exists
if [ ! -d "$PROJECT_DIR" ]; then
    echo "Error: Project directory not found"
    exit 1
fi

# Run tests (example)
cd "$PROJECT_DIR"
echo "Running tests..."
# npm test || exit 1

# Build project (example)
echo "Building project..."
# npm run build || exit 1

# Sync to remote server
echo "Syncing to remote server..."
rsync -avz --delete \
    --exclude 'node_modules' \
    --exclude '.git' \
    "$PROJECT_DIR/" \
    "${REMOTE_USER}@${REMOTE_HOST}:${REMOTE_DIR}/"

echo "Deployment completed successfully!"
```

**Tasks:**
1. Adapt the script for your project structure
2. Add rollback functionality
3. Add pre-deployment and post-deployment hooks
4. Include logging with timestamps

### Challenge 6: System Health Check

Create a comprehensive system health check:

```bash
#!/bin/bash
# health_check.sh - System health monitoring

echo "System Health Check - $(date)"
echo "========================================"

# CPU Load
echo -e "\n📊 CPU Load:"
uptime

# Memory Usage
echo -e "\n💾 Memory Usage:"
free -h

# Disk Usage
echo -e "\n💿 Disk Usage:"
df -h / | tail -1

# Top Processes by CPU
echo -e "\n🔥 Top 5 CPU-consuming processes:"
ps aux --sort=-%cpu | head -6

# Top Processes by Memory
echo -e "\n🧠 Top 5 Memory-consuming processes:"
ps aux --sort=-%mem | head -6

# Network Connectivity
echo -e "\n🌐 Network Status:"
ping -c 1 google.com > /dev/null 2>&1 && echo "✓ Internet: Connected" || echo "✗ Internet: Disconnected"

# Service Status (example - adjust for your services)
echo -e "\n⚙️  Critical Services:"
# systemctl is-active --quiet ssh && echo "✓ SSH: Running" || echo "✗ SSH: Not Running"

echo -e "\n========================================"
echo "Health check completed"
```

**Tasks:**
1. Run the health check script
2. Schedule it to run daily via cron
3. Add email notifications for critical issues
4. Create a log rotation mechanism

### Success Criteria:
- ✅ You can write shell scripts with variables, conditionals, and loops
- ✅ You can use advanced text processing with regex, sed, and awk
- ✅ You can automate system administration tasks
- ✅ You can schedule tasks with cron
- ✅ You can process JSON data from APIs
- ✅ You can create deployment and monitoring scripts
- ✅ You understand job control and background processes

**Congratulations!** You've mastered advanced CLI concepts and are now a command-line power user!

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

[← Previous: Intermediate Commands](../03-intermediate-commands/README.md) | [Back to Main](../README.md)
