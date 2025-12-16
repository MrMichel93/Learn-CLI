# Basic CLI Commands and Concepts

This section covers fundamental commands you'll use daily when working in the terminal.

## Basic Navigation Commands

### `pwd` - Print Working Directory
Shows your current location in the filesystem.
```bash
$ pwd
/home/user/documents
```

### `ls` - List Directory Contents
Displays files and directories in the current location.
```bash
$ ls                    # Basic listing
$ ls -l                 # Long format with details
$ ls -la                # Include hidden files (starting with .)
$ ls -lh                # Human-readable file sizes
```

### `cd` - Change Directory
Navigate between directories.
```bash
$ cd /home/user/documents    # Absolute path
$ cd documents               # Relative path
$ cd ..                      # Move up one directory
$ cd ~                       # Go to home directory
$ cd -                       # Return to previous directory
```

## File and Directory Operations

### `mkdir` - Make Directory
Create new directories.
```bash
$ mkdir my_folder
$ mkdir -p parent/child/grandchild    # Create nested directories
```

### `touch` - Create Empty File
Create a new empty file or update timestamp of existing file.
```bash
$ touch newfile.txt
$ touch file1.txt file2.txt file3.txt    # Create multiple files
```

### `cp` - Copy Files and Directories
Copy files or directories to a new location.
```bash
$ cp source.txt destination.txt          # Copy file
$ cp file.txt /path/to/directory/        # Copy to directory
$ cp -r folder1 folder2                  # Copy directory recursively
```

### `mv` - Move or Rename Files
Move files to a new location or rename them.
```bash
$ mv oldname.txt newname.txt             # Rename file
$ mv file.txt /path/to/directory/        # Move file
$ mv *.txt documents/                    # Move all .txt files
```

### `rm` - Remove Files and Directories
Delete files or directories (use with caution!).
```bash
$ rm file.txt                            # Remove file
$ rm -r directory/                       # Remove directory recursively
$ rm -i file.txt                         # Interactive (ask before delete)
$ rm -f file.txt                         # Force delete (no confirmation)
```

## Viewing File Contents

### `cat` - Concatenate and Display Files
Display the entire contents of a file.
```bash
$ cat file.txt
$ cat file1.txt file2.txt    # Display multiple files
```

### `less` - View File Page by Page
View large files with scrolling capability.
```bash
$ less largefile.txt
# Use arrow keys or Page Up/Down to navigate
# Press 'q' to quit
```

### `head` - Display Beginning of File
Show the first lines of a file.
```bash
$ head file.txt              # First 10 lines (default)
$ head -n 20 file.txt        # First 20 lines
```

### `tail` - Display End of File
Show the last lines of a file.
```bash
$ tail file.txt              # Last 10 lines (default)
$ tail -n 20 file.txt        # Last 20 lines
$ tail -f logfile.txt        # Follow file (useful for logs)
```

## Getting Help

### `man` - Manual Pages
Access the manual/documentation for commands.
```bash
$ man ls                     # View manual for ls command
$ man man                    # Learn about the man command itself
```

### `--help` Flag
Quick help for most commands.
```bash
$ ls --help
$ grep --help
```

## Wildcards and Pattern Matching

- `*` - Matches any characters
- `?` - Matches any single character
- `[]` - Matches any character in brackets

```bash
$ ls *.txt                   # All files ending in .txt
$ ls file?.txt               # file1.txt, file2.txt, etc.
$ ls [abc]*.txt              # Files starting with a, b, or c
```

---

## Mini Challenge: File System Navigation and Management

**Objective:** Practice basic file and directory operations to build muscle memory.

### Setup Tasks:
Create the following directory structure and files to practice with:

1. **Create a project structure:**
   ```bash
   mkdir -p my_project/src my_project/docs my_project/tests
   ```

2. **Navigate into the project:**
   ```bash
   cd my_project
   ```

3. **Create some files:**
   ```bash
   touch src/main.py src/utils.py
   touch docs/README.md docs/guide.md
   touch tests/test_main.py
   ```

### Challenge Tasks:

1. **Navigation Challenge:**
   - Use `pwd` to verify you're in the `my_project` directory
   - Use `ls -la` to see all directories and files
   - Navigate to the `src` directory, then back to `my_project` using `cd ..`
   - Use `cd -` to toggle between your last two directories

2. **File Operations Challenge:**
   - Copy `main.py` to `main_backup.py` in the same directory
   - Move `guide.md` from `docs` to the root `my_project` directory
   - Create a new directory called `backup` and copy all `.py` files to it
   - Rename `main_backup.py` to `main.py.bak`

3. **Viewing Content Challenge:**
   - Use `cat` to create a simple file: `cat > src/hello.txt` (type some text, then press Ctrl+D)
   - Use `head` to view the first few lines (if your file has multiple lines)
   - Use `tail` to view the last few lines
   - Use `less` to view the file (practice scrolling and quitting with 'q')

4. **Pattern Matching Challenge:**
   - List all `.py` files using `ls *.py` from the project root
   - Use `ls -R` to see all files recursively
   - Find all markdown files: `ls **/*.md` (may need to enable globstar in bash)

5. **Cleanup Challenge:**
   - Remove the `backup` directory and all its contents
   - Remove all `.bak` files
   - Verify your cleanup with `ls -R`

### Bonus Tasks:
- Create a script that automates creating this structure
- Use `man` to learn about at least 2 new flags for commands you used
- Create files with wildcards: `touch file{1..5}.txt`

### Success Criteria:
- ✅ You can navigate directories without getting lost
- ✅ You can create, copy, move, and delete files confidently
- ✅ You understand the difference between relative and absolute paths
- ✅ You can use wildcards to match multiple files
- ✅ You know how to get help when you need it

**Well done!** You now have a solid foundation in basic CLI operations. You're ready to explore intermediate concepts!

---

[← Previous: Introduction](../01-introduction/README.md) | [Back to Main](../README.md) | [Next: Intermediate Commands →](../03-intermediate-commands/README.md)
