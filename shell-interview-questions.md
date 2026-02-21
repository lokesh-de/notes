# Shell Interview Questions

Below are common shell scripting and Linux shell interview questions with concise answers and examples.

## 1. How do you use the shell in day-to-day life?

I use shell commands for file management, system monitoring, and troubleshooting.

Common commands:

- `ls` — list files and directories
- `cp` — copy files
- `mv` — move or rename files
- `mkdir` — create directories
- `touch` — create files
- `vim` — edit files
- `grep` — filter text
- `find` — locate files
- `top` — monitor processes
- `df` — check disk space
- `free` — check memory usage
- `ps` — list running processes

## 2. Print processes (example)

List all processes:

```bash
ps -ef
```

Print only the PID column:

```bash
ps -ef | awk '{print $2}'
```

## 3. Print only errors from a remote log file

Use `curl` to fetch and `grep` to filter:

```bash
curl https://example.com/logs | grep "error"
```

## 4. Print numbers divisible by 3 or 5 but not 15

Example script:

```bash
#!/bin/bash

for i in {1..100}; do
    if (( (i % 3 == 0 || i % 5 == 0) && i % 15 != 0 )); then
        echo "$i"
    fi
done
```

## 5. Count occurrences of `s` in "mississippi"

```bash
x="mississippi"
grep -o "s" <<< "$x" | wc -l
```

## 6. How will you debug a shell script?

Enable debug mode:

```bash
set -x
```

This prints each command as it is executed.

## 7. What is `crontab`? Example usage

`crontab` schedules commands or scripts to run at specified intervals.

Open editor:

```bash
crontab -e
```

Example (run daily at 6:00 AM):

```
0 6 * * * /home/user/node_health.sh
```

## 8. How do you open a read-only file?

Use `vim` read-only mode:

```bash
vim -r test.sh
```

## 9. What is an inode? Soft link vs hard link

An inode stores filesystem metadata (type, size, owner, permissions, timestamps, link count, pointers to data blocks). Filenames map to inode numbers in directories.

- Hard link: another directory entry pointing to the same inode. Survives deletion of the original name; must be on same filesystem. Example: `ln file1.txt file2.txt`.
- Soft (symbolic) link: separate file that points to the original path. Breaks if target is removed; can cross filesystems. Example: `ln -s file1.txt file2.txt`.

Check inode numbers:

```bash
ls -i
```

Quick memory trick: Hard link → same inode; Soft link → shortcut.

## 10. Difference between `break` and `continue`

- `break`: exit the loop immediately.
- `continue`: skip the current iteration and continue with the next.

## 11. Disadvantages of shell scripting

- Slower for large or complex tasks
- Portability differences across systems
- Limited programming features compared to higher-level languages
- Potential security risks if not written carefully

## 12. Is Bash dynamically or statically typed?

Bash is dynamically typed — variables do not require explicit type declarations.

Example:

```bash
x=10
x="hello"
```

## 13. Commands used for network troubleshooting

- `traceroute`
- `tracepath`
- `ping`
- `netstat`
- `ss`
- `nslookup`
- `curl`
- `wget`

## 14. How to sort a list of names in a file

```bash
sort filename.txt
```

## 15. How to manage large log files

Use `logrotate` to rotate, compress, and remove old logs automatically.

```bash
logrotate /etc/logrotate.conf
```
