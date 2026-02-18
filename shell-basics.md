# Shell Scripting Basics

## What is Shell Scripting?

A shell script is a text file containing a series of Linux/Unix commands executed by a shell. The shell is the user-facing command interpreter for the operating system.

Common shells:

- Bash (`/bin/bash`)
- sh (`/bin/sh`)
- Dash (`/bin/dash`)
- ksh (`/bin/ksh`)

Shell scripts automate tasks you would otherwise type interactively.

## Why Use Shell Scripting

- Automation: run repetitive tasks automatically (backups, user creation, log cleanup, service restarts).
- Save time: write once, run many times.
- Widely used in system administration, DevOps, cloud (AWS), and CI/CD pipelines.

## Creating a Shell Script

Create a file:

```bash
touch script.sh
```

Or edit with `vim`:

```bash
vim script.sh
# in vim: i (insert), write your script, Esc, :wq
```

## Listing Files — `ls`

```bash
ls
ls -l    # long listing
ls -a    # show hidden files
ls -lh   # human readable sizes
```

## Shebang (Interpreter Line)

Start scripts with a shebang to specify the interpreter:

```bash
#!/bin/bash
```

Examples for other shells:

```bash
#!/bin/sh
#!/bin/ksh
```

## Make a Script Executable

```bash
chmod +x script.sh
./script.sh        # run directly
# or
bash script.sh     # run with interpreter
```

## sh vs bash (quick comparison)

| Feature | sh | bash |
|---|---:|---:|
| Full name | Bourne Shell | Bourne Again Shell |
| Arrays | No | Yes |
| Auto-completion | No | Yes |
| History | Limited | Yes |

bash is largely backward compatible with sh; `/bin/sh` may be linked to `dash` on some systems.

## Simple Example

```bash
#!/bin/bash
echo "Hello World"
echo "This is my first shell script"
```

Run:

```bash
chmod +x script.sh
./script.sh
```

Output:

```
Hello World
This is my first shell script
```

## Real-World Example — Backup Script

```bash
#!/bin/bash
tar -czvf backup.tar.gz /home/user
echo "Backup Completed"
```

## Summary

- Shell scripting = automation using command files.
- Create scripts with `touch` or an editor, start with a shebang, make executable with `chmod +x`.
- Use `bash` for richer features; use `sh` for maximum portability.
