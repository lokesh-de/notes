# My Shell Scripting Learning Notes – Session 1

## Script I Wrote

```bash
#!/bin/bash

# Creating Folder
mkdir shell-scripting-demo

# Creating File
cd shell-scripting-demo
touch demo1.sh

# Adding content to the file
echo "Shell Scripting Demo Session1" > demo1.sh
```

## What I Learned

### 1. Shebang Line

```bash
#!/bin/bash
```

- Tells the system to execute the script using Bash shell
- Must always be the first line in the script

### 2. Comments in Shell Script

```bash
# This is a comment
```

- Used to explain the script
- Not executed by the shell
- Helps in readability

### 3. Creating a Folder

```bash
mkdir shell-scripting-demo
```

- `mkdir` → Creates a directory
- Created a folder named shell-scripting-demo
- Better practice:

```bash
mkdir -p shell-scripting-demo
```

- `-p` prevents error if folder already exists

### 4. Changing Directory

```bash
cd shell-scripting-demo
```

- `cd` → Change directory
- Moves inside the created folder

### 5. Creating a File

```bash
touch demo1.sh
```

- `touch` → Creates an empty file
- Created file demo1.sh

### 6. Adding Content to File

```bash
echo "Shell Scripting Demo Session1" > demo1.sh
```

- `echo` → Prints text
- `>` → Redirects output to a file
- Overwrites existing content

To append instead:

```bash
echo "New Line" >> demo1.sh
```

- `>>` → Appends content without deleting old content

## How to Run My Script

1. Save file as: `myscript.sh`
2. Give execute permission: `chmod +x myscript.sh`
3. Run the script: `./myscript.sh`

## Concepts I Practiced

- Writing a shell script
- Using Shebang
- Writing comments
- Creating directory
- Creating file
- Writing content into file
- File redirection (> and >>)
- Giving execute permissions
- Running a script

## Summary of My Understanding

This script:
- Creates a folder
- Moves inside the folder
- Creates a file
- Adds content to the file

This was my first basic automation using shell scripting.