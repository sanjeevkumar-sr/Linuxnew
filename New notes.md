# Linux for DevOps Engineers: A Complete Mastery Guide
### From Zero to Professional — Tailored for Mechanical Engineering Backgrounds

---

> **A Note to You, the Mechanical Engineer:**
> You already think in systems — fluid dynamics, thermodynamics, stress analysis. Linux is no different. It is a precision-engineered system where every component has a defined role, every process obeys rules, and every failure leaves a traceable signature. Think of the Linux kernel as your engine block, processes as pistons firing in sequence, and DevOps pipelines as your assembly line. This guide translates Linux concepts into that mental model wherever possible.

---

## Table of Contents

1. [Part 1: Foundations — Setting Up Your Environment](#part-1)
2. [Part 2: The Linux File System](#part-2)
3. [Part 3: Shell Mastery — Your Primary Interface](#part-3)
4. [Part 4: Users, Permissions, and Security](#part-4)
5. [Part 5: Process Management](#part-5)
6. [Part 6: Networking in Linux](#part-6)
7. [Part 7: Package Management and Software](#part-7)
8. [Part 8: Shell Scripting for DevOps Automation](#part-8)
9. [Part 9: Storage, Disks, and File Systems](#part-9)
10. [Part 10: System Monitoring and Performance Tuning](#part-10)
11. [Part 11: Logging and Troubleshooting](#part-11)
12. [Part 12: DevOps Core Tools — Git, Docker, Kubernetes](#part-12)
13. [Part 13: CI/CD Pipelines on Linux](#part-13)
14. [Part 14: Infrastructure as Code (IaC)](#part-14)
15. [Part 15: Security Hardening](#part-15)
16. [Part 16: AI Integration in Modern DevOps](#part-16)
17. [Part 17: Real-World Day-in-the-Life Scenarios](#part-17)
18. [Quick Reference Cheat Sheet](#cheat-sheet)

---

<a name="part-1"></a>
## PART 1: Foundations — Setting Up Your Environment

### 1.1 What Is Linux and Why Does DevOps Run on It?

Linux is an open-source operating system kernel, first written by Linus Torvalds in 1991. It powers approximately 96% of the world's web servers, all major cloud platforms (AWS, GCP, Azure), and nearly every DevOps tool in existence.

**Why Linux dominates DevOps:**
- Free and open-source: No licensing costs on thousands of servers
- Stable: Servers run for years without rebooting
- Scriptable: Every action can be automated from the command line
- Transparent: You can see and control everything the OS does
- Ecosystem: Docker, Kubernetes, Ansible, Terraform — all native to Linux

**The Mechanical Engineering analogy:** If Windows is a sealed gearbox, Linux is an open-architecture drivetrain. You can see every gear, replace individual components, and tune performance to exact specifications.

### 1.2 Choosing a Linux Distribution

A "distribution" (distro) is a packaged version of Linux bundled with a desktop environment, package manager, and default software.

| Distribution | Use Case | Package Manager |
|---|---|---|
| **Ubuntu** (recommended start) | Desktops, servers, cloud VMs | apt |
| **CentOS / Rocky Linux** | Enterprise servers, RHEL-compatible | yum / dnf |
| **Debian** | Stable production servers | apt |
| **Alpine Linux** | Docker containers (tiny footprint) | apk |
| **Amazon Linux 2** | AWS EC2 instances | yum |
| **Arch Linux** | Advanced users, rolling releases | pacman |

**For beginners: Start with Ubuntu 22.04 LTS.** "LTS" means Long Term Support — 5 years of security updates.

### 1.3 Installing Linux

#### Option A: Virtual Machine (Recommended for Beginners)

A Virtual Machine (VM) runs Linux inside your Windows or macOS computer, safely isolated.

**Step-by-step:**
1. Download **VirtualBox** (free): https://www.virtualbox.org
2. Download **Ubuntu 22.04 LTS ISO**: https://ubuntu.com/download/server
3. Open VirtualBox → New → Name: "Ubuntu-DevOps" → Type: Linux → Version: Ubuntu (64-bit)
4. Allocate: 4 GB RAM minimum, 25 GB disk, 2 CPU cores
5. Start the VM, select the ISO, follow the installer
6. Create a username and password — **remember these**

**After installation, install Guest Additions** (improves performance):
```bash
sudo apt update
sudo apt install -y virtualbox-guest-additions-iso
```

#### Option B: Windows Subsystem for Linux (WSL2)

If you're on Windows 10/11, WSL2 lets you run a real Linux environment inside Windows with no VM overhead.

```powershell
# Run in Windows PowerShell as Administrator
wsl --install
# Restart your computer, then Ubuntu will launch automatically
```

#### Option C: Cloud VM (Best for Production Mindset)

Create a free-tier account on AWS or GCP and launch a Linux instance. This mirrors real DevOps work.

```
AWS Free Tier: t2.micro (1 vCPU, 1 GB RAM) — 750 hours/month free
GCP Free Tier: e2-micro — Always free
```

### 1.4 Your First Login

When you open a terminal or SSH into a server, you see:

```
ubuntu@devops-server:~$
```

This is the **shell prompt**. Breaking it down:
- `ubuntu` — your username
- `devops-server` — the machine's hostname
- `~` — your current directory (~ means home directory: /home/ubuntu)
- `$` — you are a regular user (# means root/superuser)

**Your first three commands:**
```bash
whoami          # Prints your current username
pwd             # Print Working Directory — shows where you are
ls              # List files in current directory
```

Expected output:
```
ubuntu
/home/ubuntu
Desktop  Documents  Downloads  Music  Pictures
```

---

<a name="part-2"></a>
## PART 2: The Linux File System

### 2.1 The Filesystem Hierarchy Standard (FHS)

Linux uses a single unified tree structure starting from `/` (root). Everything — drives, network shares, devices — is mounted somewhere in this tree.

**Mechanical analogy:** Think of `/` as the main assembly floor. Every subdirectory is a workstation with a defined function.

```
/
├── bin/        → Essential user binaries (ls, cp, mv)
├── sbin/       → System binaries (only root uses: fdisk, iptables)
├── etc/        → Configuration files (like your engineering specs folder)
├── home/       → User home directories (/home/ubuntu, /home/john)
├── root/       → Root user's home directory
├── var/        → Variable data: logs, databases, mail spools
│   └── log/    → System and application logs
├── tmp/        → Temporary files (cleared on reboot)
├── usr/        → Installed software and libraries
│   ├── bin/    → User programs (python3, git, vim)
│   └── lib/    → Shared libraries
├── opt/        → Optional/third-party software (often enterprise apps)
├── proc/       → Virtual filesystem: live kernel/process data
├── sys/        → Virtual filesystem: hardware/kernel info
├── dev/        → Device files (disks, terminals, serial ports)
├── mnt/        → Temporary mount points
└── boot/       → Bootloader and kernel images
```

**Key DevOps directories to know:**
- `/etc/` — All configuration lives here. Change `/etc/nginx/nginx.conf` to configure Nginx.
- `/var/log/` — All logs live here. This is where you investigate problems.
- `/opt/` — Jenkins, custom tools often install here.
- `/proc/` — Read CPU info: `cat /proc/cpuinfo`; Read memory: `cat /proc/meminfo`

### 2.2 Navigating the File System

```bash
# Print current directory
pwd
# Output: /home/ubuntu

# Change directory
cd /var/log          # Go to /var/log
cd ..                # Go up one level
cd ~                 # Go to your home directory
cd -                 # Go to previous directory (toggle)

# List files
ls                   # Basic list
ls -l                # Long format (permissions, size, date)
ls -la               # Long format including hidden files (starting with .)
ls -lh               # Human-readable file sizes (KB, MB, GB)
ls -lt               # Sort by modification time (newest first)
ls /etc/             # List a specific path

# Example: ls -lh /var/log
total 52M
-rw-r--r-- 1 root   root   4.2M Apr  9 08:22 syslog
-rw-r--r-- 1 root   root    85K Apr  8 23:17 auth.log
drwxr-xr-x 2 root   root   4.0K Apr  1 10:05 apt/
```

**Reading `ls -l` output (left to right):**
```
-rw-r--r-- 1 root root 4.2M Apr 9 08:22 syslog
│└────────┘ │ │    │    │    └──────────┘ └─────┘
│ permissions│ │    │    │     timestamp   filename
│           │ owner group size
│           number of hard links
│
└─ file type: - = file, d = directory, l = symlink
```

### 2.3 File Operations

```bash
# Create files and directories
touch notes.txt              # Create empty file (or update timestamp)
mkdir projects               # Create directory
mkdir -p projects/app/src    # Create nested directories (-p = parents)

# Copy
cp file.txt backup.txt              # Copy file
cp -r /src/dir /dest/dir            # Copy directory recursively
cp -p file.txt backup.txt           # Preserve permissions and timestamps

# Move and Rename
mv old_name.txt new_name.txt        # Rename file
mv file.txt /var/backup/            # Move file to directory
mv -i file.txt /dest/               # -i = interactive, ask before overwrite

# Delete (BE CAREFUL — no recycle bin in Linux)
rm file.txt                         # Delete file
rm -r directory/                    # Delete directory recursively
rm -f file.txt                      # Force delete without asking
rm -rf /path/to/dir/                # ⚠️ Very powerful — deletes everything

# View file contents
cat file.txt                        # Print entire file to terminal
less file.txt                       # Paginated viewer (q to quit, arrows to scroll)
head -n 20 file.txt                 # Show first 20 lines
tail -n 50 /var/log/syslog          # Show last 50 lines of a log file
tail -f /var/log/syslog             # Follow log in real time (Ctrl+C to stop)
```

**DevOps Real-World Use:** `tail -f /var/log/nginx/error.log` — Watch your web server error log live as you deploy an update, catching errors instantly.

### 2.4 Finding Files

```bash
# find command — searches filesystem
find /etc -name "*.conf"            # All .conf files under /etc
find /home -type f -size +10M       # Files larger than 10MB
find /var/log -mtime -1             # Files modified in last 24 hours
find / -user john -type f           # All files owned by user "john"
find . -name "*.log" -exec rm {} \; # Find and delete all .log files

# locate command — uses a pre-built index (fast)
sudo updatedb                       # Update the index first
locate nginx.conf

# which — find where a command is installed
which python3
# Output: /usr/bin/python3

which docker
# Output: /usr/bin/docker
```

### 2.5 Symbolic Links (Symlinks)

A symlink is a pointer to another file — like a Windows shortcut but more powerful. DevOps engineers use them to manage multiple versions of software.

```bash
# Create symlink
ln -s /usr/local/python3.11/bin/python3 /usr/local/bin/python3

# View symlink
ls -la /usr/local/bin/python3
# lrwxrwxrwx 1 root root 32 Apr 9 python3 -> /usr/local/python3.11/bin/python3

# Real-world example: Switch between Node.js versions
ln -sf /opt/node-18/bin/node /usr/local/bin/node
# Later, upgrade:
ln -sf /opt/node-20/bin/node /usr/local/bin/node
```

---

<a name="part-3"></a>
## PART 3: Shell Mastery — Your Primary Interface

### 3.1 Understanding the Shell

The **shell** is a command interpreter — it takes your text commands and passes them to the Linux kernel. The most common shell is **Bash** (Bourne Again Shell).

**Shell variants:**
- `bash` — Default on most systems, used in this guide
- `zsh` — Extended bash with better autocompletion (macOS default)
- `sh` — POSIX-compliant, minimal, used in scripts for portability
- `fish` — User-friendly, interactive

Check your current shell:
```bash
echo $SHELL
# Output: /bin/bash
```

### 3.2 Essential Command Patterns

#### Input/Output Redirection

Every Linux command has three streams:
- **stdin (0):** Input (keyboard by default)
- **stdout (1):** Output (terminal by default)
- **stderr (2):** Error messages (terminal by default)

```bash
# Redirect stdout to file (overwrite)
ls -la > file_list.txt

# Redirect stdout to file (append)
echo "new log entry" >> application.log

# Redirect stderr to file
python3 script.py 2> error.log

# Redirect both stdout and stderr
./deploy.sh > output.log 2>&1

# Discard output entirely (send to /dev/null — the black hole)
./noisy_script.sh > /dev/null 2>&1

# Read from file as stdin
mysql -u root -p database_name < schema.sql
```

#### Pipes — Chaining Commands

The pipe `|` sends the output of one command as input to the next. This is Linux's superpower.

```bash
# Chain: list processes → filter for nginx → count lines
ps aux | grep nginx | wc -l

# Chain: read log → filter errors → show last 20
cat /var/log/syslog | grep "ERROR" | tail -20

# Find largest files in /var
du -sh /var/* | sort -rh | head -10

# Count unique IP addresses hitting your web server
cat /var/log/nginx/access.log | awk '{print $1}' | sort | uniq -c | sort -rn | head -20
```

### 3.3 Text Processing — The DevOps Toolkit

These tools are indispensable for processing logs, configs, and data.

#### grep — Search Text

```bash
# Basic search
grep "error" /var/log/syslog

# Case-insensitive
grep -i "error" /var/log/syslog

# Show line numbers
grep -n "404" /var/log/nginx/access.log

# Invert match (lines NOT containing pattern)
grep -v "DEBUG" application.log

# Recursive search in directory
grep -r "database_host" /etc/myapp/

# Extended regex
grep -E "ERROR|CRITICAL|FATAL" application.log

# Show 3 lines before and after match (context)
grep -B 3 -A 3 "OutOfMemoryError" app.log

# Count matches
grep -c "404" /var/log/nginx/access.log
# Output: 342
```

**Real DevOps use:** After a deployment, run `grep -i "exception\|error\|fatal" /var/log/app/app.log | tail -50` to quickly check if your service is healthy.

#### awk — Pattern Processing and Field Extraction

Think of awk as a row-by-column data processor. It splits each line into fields.

```bash
# Print specific column (space-delimited by default)
# Nginx log format: IP - - [date] "request" status bytes
awk '{print $1}' /var/log/nginx/access.log    # Print IP addresses

# Print lines where HTTP status is 500
awk '$9 == 500 {print $0}' /var/log/nginx/access.log

# Sum a column (total bytes transferred)
awk '{sum += $10} END {print sum " bytes"}' /var/log/nginx/access.log

# Print username and UID from /etc/passwd (colon-delimited)
awk -F: '{print $1, $3}' /etc/passwd

# Print lines between patterns
awk '/START/,/END/' logfile.txt

# Calculate average response time
awk '{sum+=$NF; count++} END {print "Avg:", sum/count, "ms"}' response_times.log
```

#### sed — Stream Editor

sed edits text without opening a file. Ideal for automated find-and-replace in config files.

```bash
# Replace first occurrence per line
sed 's/old_text/new_text/' file.txt

# Replace all occurrences per line (g = global)
sed 's/localhost/prod-db-01.internal/g' config.txt

# Replace in-place (modify the actual file)
sed -i 's/DEBUG/INFO/g' /etc/myapp/config.yaml

# Delete lines matching pattern
sed '/^#/d' config.txt          # Remove comment lines

# Delete blank lines
sed '/^$/d' config.txt

# Print specific line range
sed -n '10,25p' large_file.txt

# Insert line after match
sed '/\[database\]/a host = prod-db-01' config.ini

# Real-world: Update database host in config during deployment
sed -i "s/DB_HOST=.*/DB_HOST=${NEW_DB_HOST}/" /etc/app/.env
```

### 3.4 Shell Variables and Environment

```bash
# Set a variable
SERVER_NAME="web-01"
PORT=8080

# Use a variable ($ prefix)
echo "Deploying to $SERVER_NAME on port $PORT"
# Output: Deploying to web-01 on port 8080

# Environment variables — inherited by child processes
export DB_PASSWORD="secret123"
export ENVIRONMENT="production"

# View all environment variables
env
printenv

# View a specific one
echo $PATH
echo $HOME
echo $USER

# Important built-in variables
echo $?      # Exit code of last command (0 = success, non-zero = error)
echo $$      # PID of current shell
echo $!      # PID of last background command
echo $#      # Number of arguments passed to a script
echo $@      # All arguments passed to a script
```

### 3.5 Shell History and Productivity

```bash
# View command history
history
history | grep docker          # Find docker commands you've used

# Re-run commands
!!                             # Repeat last command
!nginx                         # Repeat last command starting with "nginx"
!512                           # Run command number 512 from history
Ctrl+R                         # Reverse search through history (type to filter)

# Tab completion — press Tab to auto-complete
cd /etc/sys[Tab]               # Completes to /etc/systemd/

# Brace expansion — generate multiple items
mkdir -p /opt/app/{logs,config,data,backup}
# Creates: /opt/app/logs, /opt/app/config, /opt/app/data, /opt/app/backup

touch server_{01..05}.conf
# Creates: server_01.conf through server_05.conf

# Command substitution
current_date=$(date +%Y-%m-%d)
echo "Backup created on $current_date"
# Output: Backup created on 2026-04-09

# Arithmetic
echo $((5 * 8))       # 40
echo $((2 ** 10))     # 1024
```

### 3.6 Aliases and Shell Configuration

Your shell configuration file (`.bashrc` for bash) runs every time you open a terminal.

```bash
# Edit your bashrc
nano ~/.bashrc

# Add useful aliases
alias ll='ls -lah'
alias gs='git status'
alias gp='git pull'
alias dk='docker'
alias kc='kubectl'
alias ..='cd ..'
alias ...='cd ../..'
alias grep='grep --color=auto'
alias alert='notify-send "Command finished"'

# Add a custom function
dklogs() {
    docker logs -f --tail=100 "$1"
}

# Reload bashrc without restarting terminal
source ~/.bashrc
# or
. ~/.bashrc
```

---

<a name="part-4"></a>
## PART 4: Users, Permissions, and Security

### 4.1 User and Group Management

Linux is a multi-user system with strict access controls. Every file, process, and resource belongs to a user and a group.

```bash
# User management
sudo adduser john                    # Create user interactively
sudo useradd -m -s /bin/bash john    # Create user (non-interactive)
sudo passwd john                     # Set password
sudo userdel john                    # Delete user
sudo userdel -r john                 # Delete user AND home directory

# Group management
sudo groupadd devops                 # Create group
sudo usermod -aG devops john         # Add john to devops group (-aG = append to groups)
sudo usermod -aG sudo john           # Give john sudo privileges
groups john                          # Show john's groups
id john                              # Show UID, GID, and all groups

# Switch users
su - john                            # Switch to john (- = full login environment)
sudo -u john command                 # Run a command as john
sudo su -                            # Switch to root

# Who is logged in?
who                                  # Current logged-in users
w                                    # Who + what they're doing
last                                 # Login history
```

### 4.2 File Permissions Deep Dive

Every file has three permission sets: **owner**, **group**, **others**.

```
-rwxr-xr-- 1 ubuntu devops 4096 Apr 9 10:00 deploy.sh
│└──┘└──┘└──┘
│ │    │    └── Others: r-- = read only
│ │    └─────── Group (devops): r-x = read + execute
│ └──────────── Owner (ubuntu): rwx = read + write + execute
└────────────── File type: - = regular file
```

**Permission values:**
| Symbol | Octal | Meaning |
|--------|-------|---------|
| r | 4 | Read |
| w | 2 | Write |
| x | 1 | Execute |
| - | 0 | No permission |

```bash
# Change permissions (chmod)
chmod 755 deploy.sh          # rwxr-xr-x (owner:all, group:r+x, others:r+x)
chmod 644 config.yaml        # rw-r--r-- (owner:rw, group:r, others:r)
chmod 600 ~/.ssh/id_rsa      # rw------- (only owner can read/write — SSH keys MUST be this)
chmod 777 file.sh            # ⚠️ Everyone can do everything — avoid in production!
chmod +x script.sh           # Add execute for all
chmod u+x,g-w script.sh      # Add execute to owner, remove write from group
chmod -R 755 /opt/app/       # Recursive (entire directory tree)

# Change ownership (chown)
sudo chown ubuntu:ubuntu file.txt       # Change owner and group
sudo chown -R www-data:www-data /var/www/html/   # Give nginx ownership
sudo chown john /opt/app/data/          # Change only owner

# Change group (chgrp)
sudo chgrp devops /opt/deployments/
```

### 4.3 sudo — Controlled Superuser Access

`sudo` (Superuser Do) lets authorized users run commands as root without logging in as root. This is the standard in production.

```bash
# Run a command as root
sudo apt update
sudo systemctl restart nginx

# Edit the sudoers file (ALWAYS use visudo, never edit directly)
sudo visudo

# Example sudoers entries:
# Give john full sudo access:
john  ALL=(ALL:ALL) ALL

# Allow john to restart nginx without password:
john  ALL=(ALL) NOPASSWD: /bin/systemctl restart nginx

# Allow devops group to run all commands:
%devops ALL=(ALL:ALL) ALL
```

**Common Error:**
```
john is not in the sudoers file. This incident will be reported.
```
**Fix:** `sudo usermod -aG sudo john` (run as a user who already has sudo)

### 4.4 SSH — Secure Shell

SSH is how you connect to remote Linux servers. Every DevOps engineer uses it daily.

```bash
# Connect to a remote server
ssh user@192.168.1.100
ssh ubuntu@ec2-54-123-45-67.compute-1.amazonaws.com

# Connect with a specific private key
ssh -i ~/.ssh/my-key.pem ubuntu@server-ip

# Connect on a non-standard port
ssh -p 2222 user@server-ip

# Generate an SSH key pair
ssh-keygen -t ed25519 -C "john@company.com"
# Creates: ~/.ssh/id_ed25519 (private) and ~/.ssh/id_ed25519.pub (public)

# Copy your public key to a remote server (enables passwordless login)
ssh-copy-id user@server-ip

# Manual method (if ssh-copy-id is unavailable)
cat ~/.ssh/id_ed25519.pub | ssh user@server "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"

# SSH config file — shortcuts for frequent connections
nano ~/.ssh/config
```

**~/.ssh/config example:**
```
Host prod-web
    HostName 10.0.1.50
    User ubuntu
    IdentityFile ~/.ssh/prod-key.pem
    Port 22

Host bastion
    HostName jump.company.com
    User ec2-user
    IdentityFile ~/.ssh/bastion-key.pem

Host internal-db
    HostName 10.0.2.100
    User ubuntu
    ProxyJump bastion          # Connect via bastion host
```

After this config, just type: `ssh prod-web`

---

<a name="part-5"></a>
## PART 5: Process Management

### 5.1 Understanding Processes

A process is a running program. Every process has a unique PID (Process ID), a parent process, an owner, and resource usage metrics.

**Mechanical analogy:** Processes are like individual machines on a factory floor. The kernel is the floor supervisor — it schedules who runs, allocates resources, and kills runaway machines.

```bash
# View processes
ps aux                    # All processes, detailed
ps aux | grep nginx       # Find nginx processes

# Example ps aux output:
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT  COMMAND
root       842  0.0  0.1 124776  4352 ?        Ss   nginx: master process
www-data   843  0.0  0.0 125232  2048 ?        S    nginx: worker process

# Column meanings:
# PID — Process ID
# %CPU — CPU usage
# %MEM — Memory usage
# VSZ — Virtual memory size
# RSS — Resident Set Size (actual RAM used)
# STAT — S=sleeping, R=running, Z=zombie, D=disk wait

# Interactive process viewer (like Task Manager)
top
htop          # Better version — install with: sudo apt install htop

# top keyboard shortcuts:
# k  — Kill a process (enter PID)
# r  — Renice (change priority)
# q  — Quit
# 1  — Toggle per-CPU view
# M  — Sort by memory
# P  — Sort by CPU
```

### 5.2 Controlling Processes

```bash
# Kill a process
kill PID                  # Send SIGTERM (graceful shutdown request)
kill -9 PID               # Send SIGKILL (force kill — last resort)
killall nginx             # Kill all processes named nginx
pkill -f "python app.py"  # Kill processes matching pattern

# Send signals
kill -1 PID               # SIGHUP — Reload config (nginx, apache respond to this)
kill -15 PID              # SIGTERM — Graceful termination (same as kill PID)
kill -9 PID               # SIGKILL — Cannot be caught or ignored

# Background processes
./long_script.sh &         # Run in background
jobs                       # List background jobs
fg %1                      # Bring job 1 to foreground
bg %1                      # Send job 1 to background
Ctrl+Z                     # Suspend current foreground process
Ctrl+C                     # Terminate current foreground process

# nohup — Run process that survives terminal logout
nohup ./server.sh > server.log 2>&1 &
echo $!                    # Get its PID

# disown — Detach a running background job from terminal
./server.sh &
disown %1
```

### 5.3 systemd — Service Management

`systemd` is the init system in modern Linux. It manages services (daemons) that run in the background. This is a critical DevOps skill.

```bash
# Service control
sudo systemctl start nginx        # Start service
sudo systemctl stop nginx         # Stop service
sudo systemctl restart nginx      # Stop + Start
sudo systemctl reload nginx       # Reload config without stopping
sudo systemctl status nginx       # Show status, recent logs, PID

# Enable/disable on boot
sudo systemctl enable nginx       # Start automatically on boot
sudo systemctl disable nginx      # Do not start on boot
sudo systemctl enable --now nginx # Enable AND start immediately

# Inspect services
systemctl list-units --type=service --state=running   # All running services
systemctl list-units --type=service --state=failed    # Failed services
sudo systemctl daemon-reload      # Reload systemd after editing unit files

# View service logs (journald)
sudo journalctl -u nginx                    # All logs for nginx
sudo journalctl -u nginx -f                 # Follow nginx logs
sudo journalctl -u nginx --since "1 hour ago"
sudo journalctl -u nginx --since "2026-04-09 09:00" --until "2026-04-09 10:00"
sudo journalctl -p err -u nginx             # Only error-level logs
sudo journalctl --disk-usage                # How much disk logs are using
sudo journalctl --vacuum-time=7d            # Delete logs older than 7 days
```

**Creating a Custom systemd Service — Real DevOps Task:**

Say you wrote a Python web app at `/opt/myapp/app.py` and want it to run as a service:

```bash
sudo nano /etc/systemd/system/myapp.service
```

```ini
[Unit]
Description=My Python Web Application
After=network.target postgresql.service
Requires=postgresql.service

[Service]
Type=simple
User=appuser
Group=appgroup
WorkingDirectory=/opt/myapp
EnvironmentFile=/etc/myapp/.env
ExecStart=/usr/bin/python3 /opt/myapp/app.py
Restart=always
RestartSec=5
StandardOutput=append:/var/log/myapp/app.log
StandardError=append:/var/log/myapp/error.log

[Install]
WantedBy=multi-user.target
```

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now myapp
sudo systemctl status myapp
```

---

<a name="part-6"></a>
## PART 6: Networking in Linux

### 6.1 Network Fundamentals for DevOps

```bash
# View network interfaces
ip addr show                  # All interfaces with IP addresses
ip addr show eth0             # Specific interface
ifconfig                      # Older command (still widely used)

# Example output:
# eth0: inet 10.0.1.50/24 brd 10.0.1.255
# lo: inet 127.0.0.1/8

# View routing table
ip route show
route -n

# Test connectivity
ping 8.8.8.8                  # Test internet connectivity (Ctrl+C to stop)
ping -c 4 google.com          # Send exactly 4 packets

# Trace network path
traceroute google.com
mtr google.com                # Real-time traceroute (install: sudo apt install mtr)

# DNS resolution
nslookup google.com
dig google.com                # More detailed DNS query
dig google.com MX             # Query MX records (mail servers)
host google.com               # Simple DNS lookup

# Check what's using a port
sudo ss -tlnp                 # All listening TCP ports with process names
sudo ss -ulnp                 # Listening UDP ports
sudo netstat -tlnp            # Older equivalent
sudo lsof -i :80              # What's using port 80
sudo lsof -i :443             # What's using port 443

# ss output example:
State  Recv-Q Send-Q Local Address:Port  Process
LISTEN 0      128    0.0.0.0:22         sshd
LISTEN 0      128    0.0.0.0:80         nginx
LISTEN 0      128    0.0.0.0:5432       postgres
```

### 6.2 curl and wget — HTTP from Command Line

These are daily tools for testing APIs, downloading files, and debugging web services.

```bash
# curl — transfer data from/to servers
curl https://api.example.com/health

# HTTP methods
curl -X GET https://api.example.com/users
curl -X POST https://api.example.com/users \
     -H "Content-Type: application/json" \
     -d '{"name": "John", "email": "john@example.com"}'
curl -X DELETE https://api.example.com/users/123

# Add headers (Auth token)
curl -H "Authorization: Bearer eyJ..." https://api.example.com/protected

# Follow redirects
curl -L http://example.com      # Follow HTTP 301/302 redirects

# Show response headers
curl -I https://example.com     # HEAD request (headers only)
curl -v https://example.com     # Verbose (shows full request and response)

# Download a file
curl -o nginx.tar.gz https://nginx.org/download/nginx-1.24.0.tar.gz
curl -O https://nginx.org/download/nginx-1.24.0.tar.gz  # Save with original name

# Test with response time
curl -w "\nTime: %{time_total}s\nHTTP: %{http_code}\n" -o /dev/null https://example.com

# wget — robust downloader (resumes interrupted downloads)
wget https://example.com/largefile.tar.gz
wget -c https://example.com/largefile.tar.gz   # Continue interrupted download
wget -r -np https://example.com/docs/          # Recursive download
```

### 6.3 Firewall Management with UFW and iptables

```bash
# UFW — Uncomplicated Firewall (Ubuntu's friendly frontend)
sudo ufw status                   # Check firewall status
sudo ufw enable                   # Enable firewall
sudo ufw disable                  # Disable firewall

sudo ufw allow 22                 # Allow SSH
sudo ufw allow 80                 # Allow HTTP
sudo ufw allow 443                # Allow HTTPS
sudo ufw allow 8080/tcp           # Allow specific TCP port
sudo ufw allow from 10.0.1.0/24   # Allow entire subnet
sudo ufw deny 3306                # Block MySQL from external access
sudo ufw delete allow 8080        # Remove a rule

# Allow SSH before enabling (to avoid locking yourself out!)
sudo ufw allow OpenSSH
sudo ufw enable

# iptables — lower level, more powerful
sudo iptables -L -n -v            # List all rules verbosely
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT    # Allow port 80
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT    # Allow SSH
sudo iptables -A INPUT -j DROP                         # Drop everything else
```

### 6.4 SSH Tunneling — Port Forwarding

SSH tunneling is one of the most powerful networking tricks in DevOps.

```bash
# Local Port Forwarding: Access remote service locally
# Access remote database (port 5432) as if it were local (port 5433)
ssh -L 5433:localhost:5432 ubuntu@prod-server
# Now in another terminal: psql -h localhost -p 5433

# Remote Port Forwarding: Expose local service to remote server
ssh -R 8080:localhost:3000 ubuntu@remote-server
# People on remote-server can now access your local port 3000 via port 8080

# Dynamic forwarding (SOCKS proxy)
ssh -D 1080 ubuntu@jump-server
# Use with proxychains to route traffic through the tunnel

# Persistent tunnel with autossh
sudo apt install autossh
autossh -M 20000 -f -N -L 5433:db-internal:5432 ubuntu@bastion
```

---

<a name="part-7"></a>
## PART 7: Package Management and Software

### 7.1 APT — Ubuntu/Debian Package Management

```bash
# Update package index (always do this before installing)
sudo apt update

# Upgrade installed packages
sudo apt upgrade -y              # Upgrade all packages
sudo apt full-upgrade -y         # Upgrade + remove obsolete packages

# Install/remove packages
sudo apt install -y nginx git curl vim htop jq tree
sudo apt remove nginx            # Remove but keep config
sudo apt purge nginx             # Remove and delete config files
sudo apt autoremove              # Remove unused dependency packages

# Search for packages
apt search nginx
apt show nginx                   # Detailed package info

# List installed packages
apt list --installed
dpkg -l | grep nginx             # Check if nginx is installed

# Fix broken packages
sudo apt install -f              # Fix dependencies
sudo dpkg --configure -a         # Reconfigure pending packages

# Add a third-party repository (PPA)
sudo add-apt-repository ppa:deadsnakes/ppa   # Python versions PPA
sudo apt update
sudo apt install python3.11
```

### 7.2 Installing Common DevOps Tools

```bash
# Git
sudo apt install -y git
git --version

# Docker (official method)
curl -fsSL https://get.docker.com | bash
sudo usermod -aG docker $USER    # Add yourself to docker group
newgrp docker                    # Activate without relogging

# kubectl
curl -LO "https://dl.k8s.io/release/$(curl -sL https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
kubectl version --client

# Terraform
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install terraform

# Ansible
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible

# AWS CLI v2
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
aws --version
```

### 7.3 Managing Software Versions with asdf

`asdf` is a universal version manager — like having multiple gearbox ratios for different projects.

```bash
# Install asdf
git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.14.0
echo '. "$HOME/.asdf/asdf.sh"' >> ~/.bashrc
source ~/.bashrc

# Add plugins and install versions
asdf plugin add nodejs
asdf install nodejs 18.19.0
asdf install nodejs 20.12.0
asdf global nodejs 20.12.0       # Set default
asdf local nodejs 18.19.0        # Set for current project only

asdf plugin add python
asdf install python 3.11.8
asdf global python 3.11.8
```

---

<a name="part-8"></a>
## PART 8: Shell Scripting for DevOps Automation

### 8.1 Script Structure and Best Practices

```bash
#!/bin/bash
# ──────────────────────────────────────────────────────────────
# Script: deploy.sh
# Description: Deploys the application to the target environment
# Author: John Engineer
# Date: 2026-04-09
# Usage: ./deploy.sh [environment] [version]
# Example: ./deploy.sh production v1.2.3
# ──────────────────────────────────────────────────────────────

set -euo pipefail
# set -e  → Exit immediately if any command fails
# set -u  → Treat unset variables as errors
# set -o pipefail → Pipe fails if any command in it fails

# ──── Configuration ────
ENVIRONMENT="${1:-staging}"          # Default to staging if not provided
VERSION="${2:-latest}"
APP_DIR="/opt/myapp"
LOG_FILE="/var/log/deploy/deploy_$(date +%Y%m%d_%H%M%S).log"
SLACK_WEBHOOK="${SLACK_WEBHOOK_URL}"  # From environment variable

# ──── Color output ────
RED='\033[0;31m'
GREEN='\033[0;32m'
YELLOW='\033[1;33m'
NC='\033[0m'    # No Color

# ──── Functions ────
log() {
    echo -e "[$(date '+%Y-%m-%d %H:%M:%S')] $1" | tee -a "$LOG_FILE"
}

log_success() { log "${GREEN}✓ $1${NC}"; }
log_error()   { log "${RED}✗ $1${NC}"; }
log_warn()    { log "${YELLOW}⚠ $1${NC}"; }

notify_slack() {
    curl -s -X POST -H 'Content-type: application/json' \
         --data "{\"text\":\"$1\"}" "$SLACK_WEBHOOK" > /dev/null
}

cleanup() {
    log_warn "Script interrupted. Cleaning up..."
    # Add rollback logic here
    exit 1
}

# ──── Trap signals ────
trap cleanup SIGINT SIGTERM ERR

# ──── Validation ────
validate_environment() {
    local valid_envs=("staging" "production" "development")
    for env in "${valid_envs[@]}"; do
        [[ "$ENVIRONMENT" == "$env" ]] && return 0
    done
    log_error "Invalid environment: $ENVIRONMENT"
    log_error "Valid options: ${valid_envs[*]}"
    exit 1
}

# ──── Main deployment ────
main() {
    log "Starting deployment: version=$VERSION, env=$ENVIRONMENT"
    validate_environment

    # Create log directory
    mkdir -p "$(dirname "$LOG_FILE")"

    # Check dependencies
    for cmd in docker kubectl git curl; do
        if ! command -v "$cmd" &> /dev/null; then
            log_error "Required command not found: $cmd"
            exit 1
        fi
    done
    log_success "All dependencies verified"

    # Pull latest code
    log "Pulling version $VERSION..."
    cd "$APP_DIR"
    git fetch origin
    git checkout "tags/$VERSION" 2>/dev/null || git checkout "$VERSION"
    log_success "Code updated to $VERSION"

    # Run tests
    log "Running tests..."
    if ! ./run_tests.sh; then
        log_error "Tests failed. Aborting deployment."
        notify_slack "🚨 Deployment FAILED: Tests failed for $VERSION on $ENVIRONMENT"
        exit 1
    fi
    log_success "Tests passed"

    # Build and deploy
    log "Building Docker image..."
    docker build -t "myapp:$VERSION" .
    docker push "myapp:$VERSION"

    log "Deploying to $ENVIRONMENT..."
    kubectl set image deployment/myapp myapp="myapp:$VERSION" -n "$ENVIRONMENT"
    kubectl rollout status deployment/myapp -n "$ENVIRONMENT" --timeout=300s

    log_success "Deployment complete: $VERSION → $ENVIRONMENT"
    notify_slack "✅ Deployment SUCCESS: $VERSION deployed to $ENVIRONMENT"
}

main "$@"
```

### 8.2 Control Flow

```bash
# ──── if / elif / else ────
if [[ $ENVIRONMENT == "production" ]]; then
    echo "Deploying to production — double-checking..."
    read -p "Are you sure? (yes/no): " confirm
    [[ "$confirm" != "yes" ]] && { echo "Aborted."; exit 1; }
elif [[ $ENVIRONMENT == "staging" ]]; then
    echo "Deploying to staging"
else
    echo "Unknown environment"
    exit 1
fi

# ──── Test conditions ────
# File tests
[[ -f /etc/nginx/nginx.conf ]]     # True if file exists
[[ -d /var/log/myapp ]]            # True if directory exists
[[ -r /etc/config ]]               # True if readable
[[ -w /var/data ]]                 # True if writable
[[ -x /usr/local/bin/deploy ]]     # True if executable
[[ -s /var/log/app.log ]]          # True if file exists and not empty

# String tests
[[ -z "$VAR" ]]                    # True if string is empty
[[ -n "$VAR" ]]                    # True if string is not empty
[[ "$A" == "$B" ]]                 # String equality
[[ "$A" != "$B" ]]                 # String inequality
[[ "$A" =~ ^[0-9]+$ ]]            # Regex match

# Numeric tests
[[ $A -eq $B ]]    # Equal
[[ $A -ne $B ]]    # Not equal
[[ $A -lt $B ]]    # Less than
[[ $A -gt $B ]]    # Greater than
[[ $A -le $B ]]    # Less than or equal
[[ $A -ge $B ]]    # Greater than or equal

# ──── Loops ────

# For loop over list
for server in web-01 web-02 web-03 db-01; do
    echo "Deploying to $server"
    ssh ubuntu@"$server" "sudo systemctl restart myapp"
done

# For loop over array
servers=("web-01" "web-02" "web-03")
for server in "${servers[@]}"; do
    echo "Checking $server..."
    ssh ubuntu@"$server" "systemctl is-active --quiet myapp && echo OK || echo FAILED"
done

# C-style for loop
for ((i=1; i<=10; i++)); do
    echo "Attempt $i"
    ./check_health.sh && break
    sleep 5
done

# While loop
retry=0
max_retries=5
while [[ $retry -lt $max_retries ]]; do
    curl -sf http://localhost/health && break
    retry=$((retry + 1))
    echo "Health check failed, retry $retry/$max_retries..."
    sleep 10
done
[[ $retry -eq $max_retries ]] && { echo "Service unhealthy after $max_retries attempts"; exit 1; }

# ──── Functions ────
wait_for_service() {
    local service_url="$1"
    local timeout="${2:-60}"    # Default 60 seconds
    local interval=5
    local elapsed=0

    echo "Waiting for $service_url to become healthy..."
    while [[ $elapsed -lt $timeout ]]; do
        if curl -sf "$service_url" > /dev/null 2>&1; then
            echo "Service healthy after ${elapsed}s"
            return 0
        fi
        sleep $interval
        elapsed=$((elapsed + interval))
    done
    echo "Timeout: service not healthy after ${timeout}s"
    return 1
}

# Call the function
wait_for_service "http://localhost:8080/health" 120
```

### 8.3 Error Handling Patterns

```bash
# Pattern 1: Check return code
if ! mkdir -p /opt/app/logs; then
    echo "ERROR: Could not create log directory" >&2
    exit 1
fi

# Pattern 2: OR operator (run right side if left fails)
mkdir -p /opt/app/logs || { echo "Failed to create directory"; exit 1; }

# Pattern 3: Comprehensive error handler
error_exit() {
    echo "ERROR at line $1: $2" >&2
    # Send alert, rollback, cleanup...
    exit 1
}
trap 'error_exit $LINENO "$BASH_COMMAND"' ERR

# Pattern 4: Retry function
retry() {
    local max=$1
    local delay=$2
    shift 2
    local count=0
    until "$@"; do
        count=$((count + 1))
        [[ $count -ge $max ]] && { echo "Failed after $count attempts"; return 1; }
        echo "Attempt $count failed, retrying in ${delay}s..."
        sleep "$delay"
    done
}

# Usage: retry 5 10 curl -sf http://api.example.com/health
```

---

<a name="part-9"></a>
## PART 9: Storage, Disks, and File Systems

### 9.1 Disk and Partition Management

```bash
# View disk layout
lsblk                            # Block devices in tree format
lsblk -f                         # Include filesystem type and UUID
fdisk -l                         # Detailed partition table
sudo parted -l                   # Partition sizes and types

# Example lsblk output:
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda      8:0    0  100G  0 disk
├─sda1   8:1    0    1G  0 part /boot
├─sda2   8:2    0   49G  0 part /
└─sda3   8:3    0   50G  0 part /data
sdb      8:16   0  500G  0 disk           ← unformatted new disk

# View disk usage
df -h                            # Disk usage per mounted filesystem
df -h /                          # Usage for root filesystem
du -sh /var/log/                 # Size of a directory
du -sh /var/log/*                # Size of each subdirectory
du -sh /* 2>/dev/null | sort -rh | head -10  # Largest directories in /

# Format a new disk
sudo fdisk /dev/sdb              # Start partitioning
# Press: n (new), p (primary), Enter×3 (defaults), w (write)
sudo mkfs.ext4 /dev/sdb1        # Format as ext4
sudo mkfs.xfs /dev/sdb1         # Format as XFS (preferred for large files)

# Mount a filesystem
sudo mkdir /data
sudo mount /dev/sdb1 /data
df -h /data                      # Confirm it's mounted

# Persist mount across reboots (add to /etc/fstab)
# Get UUID of partition:
sudo blkid /dev/sdb1
# Output: UUID="a1b2c3d4-..."

sudo nano /etc/fstab
# Add line:
# UUID=a1b2c3d4-... /data ext4 defaults 0 2

sudo mount -a                    # Test fstab without rebooting
```

### 9.2 Logical Volume Management (LVM)

LVM adds an abstraction layer allowing you to resize partitions online — no downtime. This is essential in cloud and production environments.

```bash
# LVM concepts:
# Physical Volume (PV) → your actual disk partitions
# Volume Group (VG) → pool of storage from multiple PVs
# Logical Volume (LV) → virtual partitions you actually use

# Create LVM stack
sudo pvcreate /dev/sdb /dev/sdc               # Initialize disks as PVs
sudo vgcreate data_vg /dev/sdb /dev/sdc       # Create volume group
sudo lvcreate -l 100%FREE -n data_lv data_vg  # Create logical volume
sudo mkfs.ext4 /dev/data_vg/data_lv           # Format it
sudo mount /dev/data_vg/data_lv /data

# View LVM status
sudo pvs                         # Physical volumes
sudo vgs                         # Volume groups
sudo lvs                         # Logical volumes
sudo lvdisplay /dev/data_vg/data_lv

# Extend a logical volume (NO downtime required!)
sudo lvextend -L +50G /dev/data_vg/data_lv    # Add 50GB
sudo resize2fs /dev/data_vg/data_lv            # Resize filesystem (ext4)
# or for XFS:
sudo xfs_growfs /data
df -h /data                      # Confirm new size
```

### 9.3 NFS — Network File System

NFS lets servers share directories over the network — common in DevOps for shared storage.

```bash
# NFS Server setup
sudo apt install nfs-kernel-server
sudo mkdir -p /exports/shared
sudo chown nobody:nogroup /exports/shared

# Edit exports file
sudo nano /etc/exports
# /exports/shared    10.0.1.0/24(rw,sync,no_subtree_check,no_root_squash)

sudo exportfs -ra
sudo systemctl restart nfs-kernel-server

# NFS Client mount
sudo apt install nfs-common
sudo mkdir /mnt/shared
sudo mount -t nfs 10.0.1.100:/exports/shared /mnt/shared
df -h /mnt/shared

# Persist in /etc/fstab:
# 10.0.1.100:/exports/shared /mnt/shared nfs defaults 0 0
```

---

<a name="part-10"></a>
## PART 10: System Monitoring and Performance Tuning

### 10.1 Resource Monitoring Commands

```bash
# CPU information
lscpu                            # CPU architecture details
nproc                            # Number of CPU cores
cat /proc/cpuinfo | grep "model name" | head -1
mpstat 1 5                       # CPU stats per second, 5 samples
top -b -n 1 | head -20           # Non-interactive top snapshot

# Memory
free -h                          # RAM and swap usage
cat /proc/meminfo                # Detailed memory info
vmstat 1 5                       # Virtual memory stats (1 second interval)

# Example free -h output:
#               total    used    free  shared  buff/cache  available
# Mem:           15Gi    3.2Gi   8.1Gi  254Mi    4.1Gi      11Gi
# Swap:         2.0Gi      0B   2.0Gi

# I/O and disk performance
iostat -xz 1 5                   # Disk I/O stats (detailed)
iotop                            # Real-time I/O by process (sudo apt install iotop)
dstat -cdngy 1                   # Combined CPU/disk/net/sys stats

# Network monitoring
iftop                            # Network usage by connection (sudo apt install iftop)
nethogs                          # Network usage by process (sudo apt install nethogs)
nload eth0                       # Network load on interface
ss -s                            # Socket statistics summary
```

### 10.2 System Load and Troubleshooting

```bash
# Load average explained
uptime
# Output: 14:32:01 up 42 days, 3:21,  2 users,  load average: 1.23, 0.98, 0.87
# Load averages = last 1 min, 5 min, 15 min
# On a 4-core system, load of 4.0 = 100% busy (fully loaded)
# Load > number_of_cores = overloaded!

# Find what's consuming resources
# Top CPU consumers
ps aux --sort=-%cpu | head -10

# Top memory consumers
ps aux --sort=-%mem | head -10

# Find processes consuming I/O
sudo iotop -oP

# Check for memory leaks over time
watch -n 5 'ps aux --sort=-%mem | head -15'

# Analyze performance with perf (advanced)
sudo apt install linux-perf
sudo perf top                    # Real-time function-level profiling
sudo perf stat ./myapp           # Count hardware events for a command
```

### 10.3 System Benchmarking

```bash
# CPU benchmark
sysbench cpu run

# Memory bandwidth test
sysbench memory run

# Disk write speed
dd if=/dev/zero of=/tmp/test bs=1G count=1 oflag=dsync
# Output: 1073741824 bytes copied, 2.14 s, 501 MB/s

# Disk read speed
dd if=/tmp/test of=/dev/null bs=1G
rm /tmp/test

# Network bandwidth (between two servers)
# Server 1: sudo iperf3 -s
# Server 2: iperf3 -c server1-ip
sudo apt install iperf3
iperf3 -c 10.0.1.100 -t 30      # 30-second bandwidth test
```

---

<a name="part-11"></a>
## PART 11: Logging and Troubleshooting

### 11.1 Understanding the Linux Logging System

Logs are the single most important diagnostic tool in DevOps. When something fails, logs tell the story.

```bash
# Key log files:
/var/log/syslog          # General system log (Ubuntu)
/var/log/messages        # General system log (CentOS)
/var/log/auth.log        # Authentication: logins, sudo, SSH
/var/log/kern.log        # Kernel messages
/var/log/dmesg           # Hardware and driver messages (boot-time)
/var/log/dpkg.log        # Package installation log
/var/log/apt/history.log # apt command history
/var/log/nginx/          # Nginx web server logs
/var/log/mysql/          # MySQL database logs

# Real-time log watching
tail -f /var/log/syslog
sudo journalctl -f                  # Follow systemd journal (all services)
sudo journalctl -fu nginx           # Follow nginx only
multitail /var/log/nginx/access.log /var/log/nginx/error.log  # Watch multiple

# Log parsing workflows
# ─── Find errors in the last hour ───
sudo journalctl -p err --since "1 hour ago"

# ─── Count HTTP status codes from nginx ───
awk '{print $9}' /var/log/nginx/access.log | sort | uniq -c | sort -rn
# Output:
# 142503 200
#   1832 304
#    423 404
#     87 500
#     12 503

# ─── Find the 10 most-requested URLs ───
awk '{print $7}' /var/log/nginx/access.log | sort | uniq -c | sort -rn | head -10

# ─── Find IPs generating most traffic ───
awk '{print $1}' /var/log/nginx/access.log | sort | uniq -c | sort -rn | head -20
```

### 11.2 The DevOps Troubleshooting Framework

When something breaks, follow this systematic approach:

```
1. DEFINE THE PROBLEM
   → What exactly is broken? (service down, slow, wrong output?)
   → When did it start?
   → What changed recently?

2. CHECK SYMPTOMS
   → Is the service running? (systemctl status)
   → Is the process alive? (ps aux)
   → Is the port listening? (ss -tlnp)
   → Are there error messages? (journalctl, /var/log/)

3. ISOLATE THE CAUSE
   → Is it a resource issue? (top, free, df)
   → Is it a network issue? (ping, curl, ss)
   → Is it a permission issue? (ls -la, id, sudo)
   → Is it a config issue? (test config files)

4. FIX AND VERIFY
   → Apply the fix
   → Verify service is running correctly
   → Watch logs for continued errors

5. DOCUMENT AND PREVENT
   → Document what happened and what fixed it
   → Add monitoring/alerting so you catch it earlier next time
```

### 11.3 Common Problems and Solutions

#### Problem: "Permission Denied"
```bash
# Diagnose
ls -la /path/to/file          # Check permissions
id                            # Check your groups
stat /path/to/file            # Detailed file info

# Fix scenarios:
# 1. You need sudo
sudo cat /etc/shadow

# 2. Wrong ownership
sudo chown ubuntu:ubuntu /opt/app/data

# 3. File not executable
chmod +x /opt/app/start.sh

# 4. SSH key permissions wrong
chmod 600 ~/.ssh/id_rsa
chmod 700 ~/.ssh/
```

#### Problem: "No space left on device"
```bash
# Find what's using space
df -h                                  # Check all filesystems
du -sh /var/log/* | sort -rh           # Check logs
du -sh /home/* | sort -rh             # Check home dirs
find / -type f -size +500M 2>/dev/null # Files larger than 500MB

# Common culprits and fixes:
# 1. Large log files
sudo truncate -s 0 /var/log/syslog     # Truncate (don't delete!)
sudo journalctl --vacuum-size=500M     # Limit journal to 500MB

# 2. Old Docker images/containers
docker system prune -a                 # ⚠️ Removes ALL unused images
docker image prune                     # Remove only dangling images

# 3. Temp files
sudo rm -rf /tmp/*
sudo apt clean                         # Clear APT package cache
```

#### Problem: Service Fails to Start
```bash
# Step 1: Check status
sudo systemctl status nginx
# Look for: "Active: failed" and error message

# Step 2: Check logs
sudo journalctl -u nginx --since "10 minutes ago"
# or
sudo tail -50 /var/log/nginx/error.log

# Step 3: Test configuration
sudo nginx -t
# Output: nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
# or:     nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address in use)

# Step 4: Check if port is in use
sudo ss -tlnp | grep :80
sudo lsof -i :80
# Find and kill the conflicting process, or change nginx's port
```

#### Problem: High CPU / Memory Usage
```bash
# Identify the culprit
top          # Press M to sort by memory, P for CPU
ps aux --sort=-%cpu | head -10

# Check if it's expected (compilation, data processing) or a leak
# For a specific process (PID 12345):
cat /proc/12345/status             # Process details
ls -la /proc/12345/fd/ | wc -l    # File descriptor count (leaks = huge number)
cat /proc/12345/smaps | grep Pss | awk '{sum+=$2} END {print sum/1024 "MB"}'  # Memory

# Quick relief (kill runaway process)
kill -9 12345

# Permanent fix: set resource limits with cgroups or ulimit
ulimit -v $((512*1024))            # Limit virtual memory to 512MB
ulimit -t 3600                     # Limit CPU time to 1 hour
```

---

<a name="part-12"></a>
## PART 12: DevOps Core Tools — Git, Docker, Kubernetes

### 12.1 Git — Version Control

```bash
# Git configuration (first-time setup)
git config --global user.name "John Engineer"
git config --global user.email "john@company.com"
git config --global core.editor vim
git config --global init.defaultBranch main

# Repository operations
git init                             # Initialize a new repo
git clone https://github.com/org/repo.git
git clone --depth 1 https://github.com/org/repo.git  # Shallow clone (faster)

# Daily workflow
git status                           # What's changed?
git diff                             # Show unstaged changes
git diff --staged                    # Show staged changes
git add file.txt                     # Stage a file
git add .                            # Stage all changes
git add -p                           # Interactively stage hunks
git commit -m "feat: add deployment health check"
git push origin main
git pull origin main                 # Fetch + merge
git fetch origin                     # Fetch without merging

# Branching
git branch feature/add-monitoring   # Create branch
git checkout feature/add-monitoring # Switch to branch
git checkout -b feature/add-monitoring  # Create AND switch
git merge feature/add-monitoring    # Merge branch into current
git branch -d feature/add-monitoring  # Delete merged branch

# Stashing (temporarily save uncommitted changes)
git stash                           # Save current changes
git stash pop                       # Restore saved changes
git stash list                      # List stashes

# Viewing history
git log --oneline --graph --all     # Graphical branch history
git log --author="John" --since="2 weeks ago"
git show HEAD                       # Show last commit details
git blame file.txt                  # Who changed each line and when

# Undoing changes
git checkout -- file.txt            # Discard unstaged changes to file
git reset HEAD file.txt             # Unstage a file
git reset --soft HEAD~1             # Undo last commit (keep changes staged)
git reset --hard HEAD~1             # ⚠️ Undo last commit and discard changes
git revert HEAD                     # Create a new commit that undoes last commit
```

### 12.2 Git Workflow for DevOps Teams

```bash
# GitFlow branching model — standard in enterprise DevOps:
# main     → Production code only. Never commit directly.
# develop  → Integration branch. Features merge here.
# feature/ → Feature branches. Branch from develop.
# release/ → Release prep. Branch from develop.
# hotfix/  → Emergency fixes. Branch from main.

# ─── Typical feature development ───
git checkout develop
git pull origin develop
git checkout -b feature/add-ssl-termination

# ... make changes ...

git add .
git commit -m "feat(nginx): add SSL termination with Let's Encrypt"
git push origin feature/add-ssl-termination

# Create Pull Request in GitHub/GitLab
# After code review and CI passes → merge to develop
```

### 12.3 Docker — Containerization

**Mechanical analogy:** Docker containers are like standardized ISO shipping containers. Your app and all its dependencies go inside. The container runs identically on your laptop, the CI server, or a cloud VM.

```bash
# Docker basics
docker version                       # Check installation
docker info                          # System-wide info

# Working with images
docker pull ubuntu:22.04             # Download image
docker images                        # List local images
docker rmi ubuntu:22.04              # Remove image
docker image prune                   # Remove dangling images

# Running containers
docker run hello-world               # Test Docker
docker run -it ubuntu:22.04 bash     # Interactive bash shell
docker run -d -p 8080:80 nginx       # Run nginx in background, map port 8080→80
docker run -d \
    --name myapp \
    -p 8080:8000 \
    -e DATABASE_URL="postgresql://db:5432/mydb" \
    -v /opt/app/data:/data \
    -v /opt/app/config:/app/config:ro \
    --restart unless-stopped \
    myapp:v1.2.3

# Container management
docker ps                            # Running containers
docker ps -a                         # All containers (including stopped)
docker stop myapp                    # Graceful stop (SIGTERM)
docker kill myapp                    # Force stop (SIGKILL)
docker rm myapp                      # Remove container
docker rm $(docker ps -aq)           # Remove all stopped containers

# Container inspection
docker logs myapp                    # View logs
docker logs -f --tail=100 myapp     # Follow logs
docker exec -it myapp bash           # Get shell inside running container
docker exec myapp cat /etc/hosts     # Run command inside container
docker inspect myapp                 # Full container metadata (JSON)
docker stats                         # Real-time resource usage
docker top myapp                     # Processes inside container

# Build an image from Dockerfile
docker build -t myapp:v1.2.3 .
docker build -t myapp:v1.2.3 -f Dockerfile.prod .
docker build --no-cache -t myapp:latest .
docker push registry.company.com/myapp:v1.2.3
```

**Production Dockerfile Example:**

```dockerfile
# Stage 1: Build
FROM python:3.11-slim AS builder
WORKDIR /app

# Install dependencies first (cached layer)
COPY requirements.txt .
RUN pip install --user --no-cache-dir -r requirements.txt

# Copy source code
COPY src/ ./src/

# Stage 2: Runtime (smaller final image)
FROM python:3.11-slim AS runtime
WORKDIR /app

# Security: run as non-root user
RUN groupadd -r appgroup && useradd -r -g appgroup appuser

# Copy only built artifacts from builder
COPY --from=builder /root/.local /home/appuser/.local
COPY --from=builder /app/src ./src

# Set ownership
RUN chown -R appuser:appgroup /app
USER appuser

# Health check
HEALTHCHECK --interval=30s --timeout=5s --retries=3 \
    CMD curl -f http://localhost:8000/health || exit 1

EXPOSE 8000
ENV PATH="/home/appuser/.local/bin:$PATH"
CMD ["python", "-m", "uvicorn", "src.main:app", "--host", "0.0.0.0", "--port", "8000"]
```

**Docker Compose — Multi-container Applications:**

```yaml
# docker-compose.yml
version: '3.9'

services:
  app:
    build: .
    ports:
      - "8000:8000"
    environment:
      - DATABASE_URL=postgresql://appuser:secret@db:5432/mydb
      - REDIS_URL=redis://cache:6379
    depends_on:
      db:
        condition: service_healthy
      cache:
        condition: service_started
    volumes:
      - app_data:/data
    networks:
      - backend
    restart: unless-stopped

  db:
    image: postgres:15-alpine
    environment:
      POSTGRES_DB: mydb
      POSTGRES_USER: appuser
      POSTGRES_PASSWORD: secret
    volumes:
      - postgres_data:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U appuser -d mydb"]
      interval: 10s
      timeout: 5s
      retries: 5
    networks:
      - backend

  cache:
    image: redis:7-alpine
    volumes:
      - redis_data:/data
    networks:
      - backend

  nginx:
    image: nginx:alpine
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf:ro
      - ssl_certs:/etc/ssl:ro
    depends_on:
      - app
    networks:
      - backend

volumes:
  postgres_data:
  redis_data:
  app_data:
  ssl_certs:

networks:
  backend:
    driver: bridge
```

```bash
# Docker Compose commands
docker compose up -d                 # Start all services in background
docker compose down                  # Stop and remove containers
docker compose down -v               # Also remove volumes
docker compose ps                    # Status of all services
docker compose logs -f app           # Follow app logs
docker compose exec app bash         # Shell into app container
docker compose restart app           # Restart specific service
docker compose pull                  # Pull latest images
docker compose build --no-cache      # Rebuild images
```

### 12.4 Kubernetes — Container Orchestration

Kubernetes (K8s) manages containers at scale across clusters of machines.

**Mechanical analogy:** If Docker is one CNC machine, Kubernetes is the entire factory floor management system — deciding which machine runs which job, rerouting when machines fail, and scaling up capacity under load.

```bash
# kubectl basics
kubectl version --client
kubectl cluster-info
kubectl get nodes                    # List cluster nodes
kubectl get nodes -o wide            # With IP and OS info

# Namespaces — logical cluster separation
kubectl get namespaces
kubectl create namespace production
kubectl config set-context --current --namespace=production

# Working with deployments
kubectl get deployments -n production
kubectl get pods -n production
kubectl get pods -n production -o wide  # With IP and node info
kubectl describe pod myapp-pod-xyz -n production  # Detailed pod info

# Apply configurations
kubectl apply -f deployment.yaml
kubectl apply -f ./k8s/               # Apply all files in directory
kubectl delete -f deployment.yaml

# Scaling
kubectl scale deployment myapp --replicas=5 -n production
kubectl autoscale deployment myapp --min=3 --max=10 --cpu-percent=70

# Rolling updates and rollbacks
kubectl set image deployment/myapp myapp=myapp:v1.3.0 -n production
kubectl rollout status deployment/myapp -n production   # Watch rollout
kubectl rollout history deployment/myapp -n production  # See revision history
kubectl rollout undo deployment/myapp -n production     # Rollback!
kubectl rollout undo deployment/myapp --to-revision=3   # Rollback to specific version

# Debugging
kubectl logs myapp-pod-xyz -n production
kubectl logs -f myapp-pod-xyz -n production              # Follow
kubectl logs myapp-pod-xyz -c sidecar -n production      # Specific container
kubectl exec -it myapp-pod-xyz -n production -- bash     # Shell into pod
kubectl port-forward pod/myapp-pod-xyz 8080:8000         # Forward port locally
kubectl get events -n production --sort-by='.lastTimestamp'  # Recent events

# Resource quotas
kubectl top nodes
kubectl top pods -n production
```

**Kubernetes Deployment YAML:**

```yaml
# deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
  namespace: production
  labels:
    app: myapp
    version: v1.3.0
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 0        # Zero-downtime deployments
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp
        image: myapp:v1.3.0
        ports:
        - containerPort: 8000
        env:
        - name: DATABASE_URL
          valueFrom:
            secretKeyRef:
              name: myapp-secrets
              key: database-url
        resources:
          requests:
            memory: "256Mi"
            cpu: "250m"
          limits:
            memory: "512Mi"
            cpu: "500m"
        livenessProbe:
          httpGet:
            path: /health
            port: 8000
          initialDelaySeconds: 30
          periodSeconds: 10
        readinessProbe:
          httpGet:
            path: /ready
            port: 8000
          initialDelaySeconds: 5
          periodSeconds: 5
```

---

<a name="part-13"></a>
## PART 13: CI/CD Pipelines on Linux

### 13.1 What Is CI/CD?

**CI (Continuous Integration):** Every code push automatically runs tests, builds, and checks.  
**CD (Continuous Delivery/Deployment):** Automatically deploys passing builds to environments.

**The pipeline flow:**
```
Developer pushes code
        ↓
  Git webhook fires
        ↓
  CI server picks up
        ↓
  Run unit tests
        ↓
  Build Docker image
        ↓
  Run integration tests
        ↓
  Push image to registry
        ↓
  Deploy to staging
        ↓
  Run smoke tests
        ↓
  (Manual approval gate)
        ↓
  Deploy to production
        ↓
  Monitor & alert
```

### 13.2 GitHub Actions Pipeline

```yaml
# .github/workflows/deploy.yml
name: CI/CD Pipeline

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

env:
  REGISTRY: ghcr.io
  IMAGE_NAME: ${{ github.repository }}

jobs:
  # ──── Job 1: Test ────
  test:
    runs-on: ubuntu-latest
    services:
      postgres:
        image: postgres:15
        env:
          POSTGRES_PASSWORD: testpass
          POSTGRES_DB: testdb
        options: >-
          --health-cmd pg_isready
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5

    steps:
    - uses: actions/checkout@v4

    - name: Set up Python
      uses: actions/setup-python@v5
      with:
        python-version: '3.11'
        cache: 'pip'

    - name: Install dependencies
      run: pip install -r requirements.txt -r requirements-test.txt

    - name: Run tests with coverage
      run: |
        pytest --cov=src --cov-report=xml --cov-fail-under=80
      env:
        DATABASE_URL: postgresql://postgres:testpass@localhost:5432/testdb

    - name: Upload coverage report
      uses: codecov/codecov-action@v4

  # ──── Job 2: Build and Push ────
  build:
    needs: test
    runs-on: ubuntu-latest
    if: github.event_name == 'push'
    outputs:
      image-tag: ${{ steps.meta.outputs.tags }}

    steps:
    - uses: actions/checkout@v4

    - name: Log in to Container Registry
      uses: docker/login-action@v3
      with:
        registry: ${{ env.REGISTRY }}
        username: ${{ github.actor }}
        password: ${{ secrets.GITHUB_TOKEN }}

    - name: Extract metadata
      id: meta
      uses: docker/metadata-action@v5
      with:
        images: ${{ env.REGISTRY }}/${{ env.IMAGE_NAME }}
        tags: |
          type=sha,prefix=sha-
          type=ref,event=branch
          type=semver,pattern={{version}}

    - name: Build and push Docker image
      uses: docker/build-push-action@v5
      with:
        context: .
        push: true
        tags: ${{ steps.meta.outputs.tags }}
        cache-from: type=gha
        cache-to: type=gha,mode=max

  # ──── Job 3: Deploy to Staging ────
  deploy-staging:
    needs: build
    runs-on: ubuntu-latest
    environment: staging

    steps:
    - name: Deploy to staging
      run: |
        echo "${{ secrets.KUBECONFIG }}" | base64 -d > kubeconfig.yaml
        export KUBECONFIG=kubeconfig.yaml
        kubectl set image deployment/myapp \
          myapp="${{ needs.build.outputs.image-tag }}" \
          -n staging
        kubectl rollout status deployment/myapp -n staging --timeout=300s

    - name: Run smoke tests
      run: |
        sleep 30
        curl -f https://staging.myapp.company.com/health || exit 1
```

### 13.3 Jenkins Pipeline on Linux

```bash
# Install Jenkins on Ubuntu
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | \
    sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
    https://pkg.jenkins.io/debian-stable binary/" | \
    sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt update && sudo apt install -y jenkins openjdk-17-jdk
sudo systemctl enable --now jenkins

# Get initial admin password
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

**Jenkinsfile (Declarative Pipeline):**

```groovy
pipeline {
    agent any

    environment {
        APP_NAME = 'myapp'
        DOCKER_REGISTRY = 'registry.company.com'
        IMAGE_TAG = "${BUILD_NUMBER}-${GIT_COMMIT[0..7]}"
    }

    options {
        timeout(time: 30, unit: 'MINUTES')
        buildDiscarder(logRotator(numToKeepStr: '10'))
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Test') {
            steps {
                sh '''
                    python3 -m venv venv
                    source venv/bin/activate
                    pip install -r requirements.txt
                    pytest tests/ --junitxml=test-results.xml
                '''
            }
            post {
                always {
                    junit 'test-results.xml'
                }
            }
        }

        stage('Build') {
            steps {
                sh "docker build -t ${DOCKER_REGISTRY}/${APP_NAME}:${IMAGE_TAG} ."
            }
        }

        stage('Push') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-registry',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                        echo "$DOCKER_PASS" | docker login ${DOCKER_REGISTRY} \
                             -u "$DOCKER_USER" --password-stdin
                        docker push ${DOCKER_REGISTRY}/${APP_NAME}:${IMAGE_TAG}
                    '''
                }
            }
        }

        stage('Deploy to Production') {
            when { branch 'main' }
            input { message "Deploy to production?" }
            steps {
                sh """
                    kubectl set image deployment/${APP_NAME} \
                      ${APP_NAME}=${DOCKER_REGISTRY}/${APP_NAME}:${IMAGE_TAG} \
                      -n production
                    kubectl rollout status deployment/${APP_NAME} -n production
                """
            }
        }
    }

    post {
        success {
            slackSend color: 'good', message: "✅ ${APP_NAME} ${IMAGE_TAG} deployed!"
        }
        failure {
            slackSend color: 'danger', message: "🚨 Pipeline failed: ${APP_NAME} ${BUILD_URL}"
        }
    }
}
```

---

<a name="part-14"></a>
## PART 14: Infrastructure as Code (IaC)

### 14.1 Terraform — Infrastructure Provisioning

Terraform lets you define cloud infrastructure in code, version it in Git, and apply it repeatably.

```hcl
# main.tf — Deploy a web application on AWS

terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
  backend "s3" {
    bucket = "company-terraform-state"
    key    = "prod/web-app/terraform.tfstate"
    region = "us-east-1"
  }
}

provider "aws" {
  region = var.aws_region
}

# ──── Variables ────
variable "aws_region"    { default = "us-east-1" }
variable "instance_type" { default = "t3.medium" }
variable "environment"   { default = "production" }

# ──── Data sources ────
data "aws_ami" "ubuntu" {
  most_recent = true
  owners      = ["099720109477"]  # Canonical (Ubuntu)
  filter {
    name   = "name"
    values = ["ubuntu/images/hvm-ssd/ubuntu-jammy-22.04-amd64-server-*"]
  }
}

# ──── Resources ────
resource "aws_instance" "web" {
  count         = 3
  ami           = data.aws_ami.ubuntu.id
  instance_type = var.instance_type

  vpc_security_group_ids = [aws_security_group.web.id]
  iam_instance_profile   = aws_iam_instance_profile.web.name

  user_data = <<-EOF
    #!/bin/bash
    set -euo pipefail
    apt-get update -q
    apt-get install -y -q nginx
    systemctl enable --now nginx
    echo "Server $(hostname)" > /var/www/html/index.html
  EOF

  tags = {
    Name        = "web-${var.environment}-${count.index + 1}"
    Environment = var.environment
    ManagedBy   = "Terraform"
  }
}

resource "aws_security_group" "web" {
  name_prefix = "web-sg-"
  ingress {
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
  ingress {
    from_port   = 443
    to_port     = 443
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}

# ──── Outputs ────
output "web_public_ips" {
  value = aws_instance.web[*].public_ip
}
```

```bash
# Terraform workflow
terraform init              # Initialize, download providers
terraform fmt               # Format code
terraform validate          # Validate syntax
terraform plan              # Preview changes (ALWAYS do this first)
terraform apply             # Apply changes (asks for confirmation)
terraform apply -auto-approve  # Apply without confirmation (use carefully)
terraform destroy           # Destroy all resources
terraform show              # Show current state
terraform state list        # List all resources in state
terraform output            # Show outputs
```

### 14.2 Ansible — Configuration Management

Ansible automates configuration of servers using SSH — no agents required.

```yaml
# site.yml — Configure web servers
---
- name: Configure web servers
  hosts: webservers
  become: true         # Use sudo
  vars:
    app_port: 8000
    nginx_worker_processes: auto

  tasks:
    - name: Update apt cache
      ansible.builtin.apt:
        update_cache: true
        cache_valid_time: 3600

    - name: Install required packages
      ansible.builtin.apt:
        name:
          - nginx
          - python3
          - python3-pip
          - git
          - curl
          - htop
        state: present

    - name: Create app user
      ansible.builtin.user:
        name: appuser
        shell: /bin/bash
        create_home: true
        groups: www-data

    - name: Deploy application
      ansible.builtin.git:
        repo: https://github.com/company/myapp.git
        dest: /opt/myapp
        version: "{{ app_version | default('main') }}"
        force: true

    - name: Install Python dependencies
      ansible.builtin.pip:
        requirements: /opt/myapp/requirements.txt
        virtualenv: /opt/myapp/venv

    - name: Deploy nginx config
      ansible.builtin.template:
        src: templates/nginx.conf.j2
        dest: /etc/nginx/sites-available/myapp
        owner: root
        group: root
        mode: '0644'
      notify: Restart nginx

    - name: Enable nginx site
      ansible.builtin.file:
        src: /etc/nginx/sites-available/myapp
        dest: /etc/nginx/sites-enabled/myapp
        state: link

    - name: Deploy systemd service
      ansible.builtin.template:
        src: templates/myapp.service.j2
        dest: /etc/systemd/system/myapp.service
      notify:
        - Reload systemd
        - Restart myapp

    - name: Ensure myapp is running
      ansible.builtin.systemd:
        name: myapp
        state: started
        enabled: true

  handlers:
    - name: Restart nginx
      ansible.builtin.systemd:
        name: nginx
        state: restarted

    - name: Reload systemd
      ansible.builtin.systemd:
        daemon_reload: true

    - name: Restart myapp
      ansible.builtin.systemd:
        name: myapp
        state: restarted
```

```bash
# Ansible commands
ansible all -m ping -i inventory.ini          # Test connectivity
ansible webservers -m shell -a "df -h"        # Run command on all web servers
ansible-playbook site.yml -i inventory.ini    # Run playbook
ansible-playbook site.yml --check            # Dry run (no changes made)
ansible-playbook site.yml --diff             # Show config file diffs
ansible-playbook site.yml -l web-01          # Limit to specific host
ansible-playbook site.yml -e "app_version=v1.3.0"  # Pass extra variable
ansible-playbook site.yml -t deploy          # Run only tasks tagged "deploy"
ansible-vault encrypt secrets.yml            # Encrypt sensitive files
ansible-vault view secrets.yml               # View encrypted file
```

---

<a name="part-15"></a>
## PART 15: Security Hardening

### 15.1 Server Hardening Checklist

```bash
# ── 1. Keep system updated ──
sudo apt update && sudo apt upgrade -y
sudo apt install unattended-upgrades
sudo dpkg-reconfigure unattended-upgrades   # Enable automatic security updates

# ── 2. Secure SSH ──
sudo nano /etc/ssh/sshd_config
# Recommended settings:
# PermitRootLogin no              ← Never SSH as root
# PasswordAuthentication no       ← Keys only (disable passwords)
# PubkeyAuthentication yes
# Port 2222                       ← Change default port
# AllowUsers ubuntu john          ← Whitelist specific users
# MaxAuthTries 3
# ClientAliveInterval 300
# ClientAliveCountMax 2

sudo systemctl restart sshd

# ── 3. Fail2Ban — Automatically block brute-force attacks ──
sudo apt install fail2ban
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
sudo nano /etc/fail2ban/jail.local
# [sshd]
# enabled = true
# port = 2222
# maxretry = 3
# bantime = 3600
sudo systemctl enable --now fail2ban
sudo fail2ban-client status               # Status
sudo fail2ban-client status sshd          # SSH-specific status
sudo fail2ban-client set sshd unbanip 1.2.3.4  # Unban an IP

# ── 4. Enable firewall ──
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow 2222/tcp                   # SSH (new port)
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw enable

# ── 5. Disable root login ──
sudo passwd -l root                       # Lock root password
```

### 15.2 Secrets Management

**Never store secrets in code or environment variables in plain text.** Use a secrets manager.

```bash
# HashiCorp Vault — enterprise secrets management
# Store a secret:
vault kv put secret/myapp/db password="super-secret" username="appuser"

# Retrieve in scripts:
DB_PASSWORD=$(vault kv get -field=password secret/myapp/db)

# AWS Secrets Manager:
DB_PASSWORD=$(aws secretsmanager get-secret-value \
    --secret-id prod/myapp/database \
    --query SecretString --output text | jq -r '.password')

# sops — encrypt secrets files for Git storage
sops --encrypt secrets.yaml > secrets.enc.yaml  # Encrypt
sops --decrypt secrets.enc.yaml                  # Decrypt
# Stores in Git encrypted; decryption requires AWS KMS or GPG key
```

### 15.3 Audit and Compliance

```bash
# auditd — Kernel-level audit logging
sudo apt install auditd
sudo systemctl enable --now auditd

# Monitor file access
sudo auditctl -w /etc/passwd -p wa -k passwd_changes
sudo auditctl -w /etc/shadow -p wa -k shadow_changes
sudo auditctl -w /etc/sudoers -p wa -k sudoers_changes

# View audit log
sudo ausearch -k passwd_changes
sudo aureport --summary                   # Summary report
sudo aureport --auth --start today        # Today's auth events

# Lynis — security audit tool
sudo apt install lynis
sudo lynis audit system                   # Full system security scan
# Output: hardening index score and recommendations

# CIS Benchmark compliance check
# Download and run CIS-CAT or use openscap:
sudo apt install openscap-scanner
oscap xccdf eval --profile xccdf_org.ssgproject.content_profile_cis \
    /usr/share/xml/scap/ssg/content/ssg-ubuntu2204-ds.xml
```

---

<a name="part-16"></a>
## PART 16: AI Integration in Modern DevOps

### 16.1 AI in the DevOps Landscape (AIOps)

AI is rapidly being integrated into DevOps workflows. Here's where it's making the biggest impact:

**1. Intelligent Log Analysis**
Instead of manually searching through millions of log lines, AI models detect anomalies, correlate events, and predict failures before they happen.

```bash
# Install and use Grafana Loki with AI-powered querying
# Loki stores logs; AI (like Grafana's ML features) detects anomalies

# Example: Send logs to a local AI summarizer
tail -n 1000 /var/log/nginx/error.log | \
    curl -s -X POST http://localhost:11434/api/generate \
    -H "Content-Type: application/json" \
    -d "{\"model\":\"llama3\",\"prompt\":\"Analyze these logs and identify the top 3 issues:\n$(cat)\",\"stream\":false}" \
    | jq -r '.response'
```

**2. AI-Assisted Incident Response**

Tools like **Opsgenie AI**, **PagerDuty Copilot**, and **Datadog Bits AI** automatically:
- Correlate alerts across systems
- Suggest probable root causes
- Recommend runbook steps

**3. Automated Code Review with AI**

```yaml
# GitHub Actions: AI code review on PRs
- name: AI Code Review
  uses: coderabbitai/ai-pr-reviewer@latest
  with:
    openai_api_key: ${{ secrets.OPENAI_API_KEY }}
    system_message: "Review for security vulnerabilities, performance issues, and DevOps best practices."
```

**4. Predictive Scaling**

```bash
# Kubernetes VPA (Vertical Pod Autoscaler) with ML-based recommendations
kubectl apply -f https://github.com/kubernetes/autoscaler/releases/download/vertical-pod-autoscaler-0.14.0/vpa-v1-crd-gen.yaml

# KEDA — Event-driven autoscaling with custom metrics including AI predictions
kubectl apply -f https://github.com/kedacore/keda/releases/download/v2.13.1/keda-2.13.1.yaml
```

### 16.2 Running Local AI Models for DevOps

**Ollama** lets you run large language models locally — no API costs, data stays on-premise.

```bash
# Install Ollama
curl -fsSL https://ollama.com/install.sh | bash

# Pull and run a model
ollama pull llama3
ollama pull codellama      # Optimized for code
ollama pull mistral

# Run in interactive mode
ollama run llama3

# Use the API in scripts
curl -s http://localhost:11434/api/generate \
    -d '{"model":"codellama","prompt":"Write a bash script to check if all kubernetes pods are running","stream":false}' \
    | jq -r '.response'

# AI-powered shell assistant script
#!/bin/bash
# ai-explain.sh — Explain what a command does
explain_command() {
    local cmd="$*"
    curl -s http://localhost:11434/api/generate \
        -H "Content-Type: application/json" \
        -d "{
          \"model\": \"llama3\",
          \"prompt\": \"Explain this Linux/DevOps command in simple terms. Include what each flag does and when a DevOps engineer would use it:\n\n$cmd\",
          \"stream\": false
        }" | jq -r '.response'
}
explain_command "$@"
```

### 16.3 AI-Powered Monitoring Stack

```yaml
# docker-compose for AI-enhanced monitoring
version: '3.9'
services:

  prometheus:
    image: prom/prometheus:latest
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
    ports: ["9090:9090"]

  grafana:
    image: grafana/grafana:latest
    environment:
      GF_FEATURE_TOGGLES_ENABLE: mlExpressions
    ports: ["3000:3000"]

  # AI anomaly detection with Prophet or Isolation Forest
  anomaly-detector:
    build: ./anomaly-detector
    environment:
      PROMETHEUS_URL: http://prometheus:9090
      MODEL: isolation_forest
      SENSITIVITY: 0.95
    ports: ["8001:8001"]

  # LLM-powered alert enrichment
  alert-enricher:
    image: python:3.11-slim
    command: python enricher.py
    environment:
      OLLAMA_URL: http://ollama:11434
      MODEL: llama3
```

### 16.4 Using AI Tools in Your Daily DevOps Workflow

```bash
# ── GitHub Copilot CLI (AI in your terminal) ──
# Install:
npm install -g @githubnext/github-copilot-cli

# Ask in natural language:
github-copilot-cli what-the-shell "find all docker containers using more than 500MB of memory and show their names"
# Output: docker stats --no-stream --format "{{.Name}} {{.MemUsage}}" | awk '{if($2+0 > 500) print $1}'

# ── Shell-GPT (ChatGPT in terminal) ──
pip install shell-gpt
sgpt "Write a systemd service file for a Python FastAPI app running on port 8000"
sgpt --shell "Find all files modified in the last 24 hours larger than 100MB"

# ── AI-assisted log analysis script ──
#!/bin/bash
# smart-diagnose.sh — AI-powered server diagnosis
analyze_server() {
    local report=""
    report+="=== SYSTEM STATUS $(date) ===\n"
    report+="$(uptime)\n"
    report+="$(free -h)\n"
    report+="$(df -h)\n"
    report+="=== RECENT ERRORS ===\n"
    report+="$(sudo journalctl -p err --since '1 hour ago' --no-pager | tail -50)\n"
    report+="=== TOP PROCESSES ===\n"
    report+="$(ps aux --sort=-%cpu | head -10)\n"

    echo -e "$report" | curl -s -X POST \
        -H "Content-Type: application/json" \
        -H "Authorization: Bearer $OPENAI_API_KEY" \
        https://api.openai.com/v1/chat/completions \
        -d "{
          \"model\": \"gpt-4o\",
          \"messages\": [{
            \"role\": \"user\",
            \"content\": \"You are a Linux DevOps expert. Analyze this server status report and identify any issues, their likely causes, and recommended fixes:\n\n$(echo -e "$report" | head -100)\"
          }]
        }" | jq -r '.choices[0].message.content'
}

analyze_server
```

---

<a name="part-17"></a>
## PART 17: Real-World Day-in-the-Life Scenarios

### Scenario 1: Production Service Is Down — 3AM Incident

```
Alert: PagerDuty fires. "myapp: HTTP 503 — All health checks failing"
```

```bash
# Step 1: Assess (< 2 minutes)
ssh ubuntu@prod-bastion
ssh ubuntu@web-01

systemctl status myapp            # Is the service running?
# Active: failed (Result: exit-code) since 02:47:13

# Step 2: Get recent logs
sudo journalctl -u myapp --since "30 minutes ago" --no-pager | tail -80
# [03:47:10] FATAL: Unable to connect to database: Connection refused
# [03:47:10] FATAL: Retries exhausted. Shutting down.

# Step 3: Check the database
ping -c 2 prod-db-01.internal      # Reachable?
# Request timeout for icmp_seq 0

telnet prod-db-01.internal 5432    # Port open?
# Trying 10.0.2.100... Connection refused

# Step 4: Check the DB server
ssh ubuntu@prod-db-01

systemctl status postgresql
# Active: failed — Out of disk space

df -h
# /dev/sda2  100G  100G  0  100% /

# Step 5: Emergency fix
# Find and remove large files
du -sh /var/lib/postgresql/14/main/pg_wal/*  | sort -rh | head -5
# Large WAL files due to replication lag

# Archive old WAL files
sudo pg_archivecleanup /var/lib/postgresql/14/main/pg_wal/ 000000010000003400000050
# Freed 15GB

df -h       # Confirm space recovered
sudo systemctl start postgresql
sudo systemctl status postgresql  # Confirm running

# Step 6: Restart app
exit                               # Back to web server
sudo systemctl start myapp
sudo systemctl status myapp        # Active: running

curl http://localhost/health       # {"status": "ok"}

# Step 7: Notify and document
# Send Slack message: resolved
# Write incident report
# Add disk monitoring alert (so this never happens silently again)
```

### Scenario 2: Zero-Downtime Deployment

```bash
#!/bin/bash
# blue-green-deploy.sh
set -euo pipefail

NEW_VERSION="$1"
NAMESPACE="production"

echo "Starting blue-green deployment: $NEW_VERSION"

# Identify current active color
CURRENT=$(kubectl get service myapp -n "$NAMESPACE" \
    -o jsonpath='{.spec.selector.color}')
echo "Current active: $CURRENT"

NEW_COLOR=$([ "$CURRENT" = "blue" ] && echo "green" || echo "blue")
echo "Deploying to: $NEW_COLOR"

# Deploy new version to inactive color
kubectl set image "deployment/myapp-$NEW_COLOR" \
    myapp="myapp:$NEW_VERSION" -n "$NAMESPACE"

kubectl rollout status "deployment/myapp-$NEW_COLOR" \
    -n "$NAMESPACE" --timeout=300s

echo "New version deployed to $NEW_COLOR. Running smoke tests..."
NEW_POD=$(kubectl get pod -n "$NAMESPACE" \
    -l "app=myapp,color=$NEW_COLOR" \
    -o jsonpath='{.items[0].metadata.name}')

# Smoke test against new pods directly
kubectl port-forward "$NEW_POD" 18080:8000 -n "$NAMESPACE" &
PF_PID=$!
sleep 5

if curl -sf http://localhost:18080/health; then
    echo "Smoke tests passed!"
    kill $PF_PID
else
    echo "Smoke tests FAILED — aborting, NOT switching traffic"
    kill $PF_PID
    exit 1
fi

# Switch traffic by updating service selector
kubectl patch service myapp -n "$NAMESPACE" \
    -p "{\"spec\":{\"selector\":{\"color\":\"$NEW_COLOR\"}}}"

echo "Traffic switched to $NEW_COLOR ($NEW_VERSION)"
echo "Previous version ($CURRENT) still running as fallback"
echo "To rollback: kubectl patch service myapp -n $NAMESPACE -p '{\"spec\":{\"selector\":{\"color\":\"$CURRENT\"}}}'"
```

### Scenario 3: Performance Degradation Investigation

```
Alert: "API response time p99 > 5000ms (was 200ms)"
```

```bash
# Step 1: Check system resources
ssh ubuntu@api-server

top                                # Quick overview
# Load: 15.23 15.40 14.20 on 8-core machine = 2x overloaded!

# Step 2: What's causing high load?
ps aux --sort=-%cpu | head -10
# PID    USER  %CPU %MEM  COMMAND
# 28741  app   380  2.1   python worker.py --queue celery

# Step 3: What is that worker doing?
strace -p 28741 -e trace=network,file 2>&1 | head -20
# connect(5, {sin_family=AF_INET, sin_addr=10.0.2.50, sin_port=6379...
# read(5, ... blocks for long time
# → Worker is waiting on Redis

# Step 4: Check Redis
redis-cli -h 10.0.2.50 INFO stats
redis-cli -h 10.0.2.50 INFO clients
# connected_clients: 1842  ← WAY too many connections
# blocked_clients: 1839   ← All waiting!

redis-cli -h 10.0.2.50 MONITOR  # Live command stream
# 1000s of requests: LPOP job:queue (empty queue, workers spinning!)

# Root cause: A job publisher crashed but workers kept polling empty queue
# Fix: Restart the publisher service
sudo systemctl restart job-publisher

# Watch Redis connections drop
watch -n 1 'redis-cli -h 10.0.2.50 INFO clients | grep connected'

# Step 5: Verify API response times improving
for i in $(seq 1 10); do
    curl -w "Time: %{time_total}s  HTTP: %{http_code}\n" \
         -o /dev/null -s https://api.example.com/v1/users
    sleep 2
done

# Add this monitoring to prevent recurrence:
# Prometheus alert: redis_connected_clients > 500
```

---

<a name="cheat-sheet"></a>
## QUICK REFERENCE CHEAT SHEET

### Navigation and Files
```bash
pwd; ls -lah; cd -; find / -name "file"; locate file; tree /path
cp -r src dst; mv old new; rm -rf dir; ln -s target link
cat; less; head -20; tail -f; wc -l; diff file1 file2
```

### Permissions
```bash
chmod 755 file; chmod -R 644 dir; chown user:group file
ls -la; stat file; umask 022; getfacl file; setfacl -m u:john:r file
```

### Process Management
```bash
ps aux | grep app; kill -9 PID; pkill app; killall app
nohup cmd &; jobs; fg; bg; Ctrl+Z; Ctrl+C
systemctl status|start|stop|restart|enable|disable service
journalctl -u service -f --since "1h ago"
```

### Networking
```bash
ip addr; ss -tlnp; curl -I url; wget url; ping -c4 host
ssh -i key user@host; scp file user@host:/path; rsync -avz src dst
nmap -p 80,443 host; nc -zv host port; dig domain; nslookup domain
```

### Text Processing
```bash
grep -rni "pattern" /path; grep -E "ERR|WARN" log
awk '{print $1}' file; awk -F: '{print $1}' /etc/passwd
sed 's/old/new/g' file; sed -i 's/old/new/g' file
sort | uniq -c | sort -rn; cut -d: -f1,3; tr 'a-z' 'A-Z'
```

### Disk and Storage
```bash
df -h; du -sh /path/*; lsblk; fdisk -l; mount; umount
dd if=/dev/zero of=test bs=1G count=1; hdparm -t /dev/sda
tar czf archive.tar.gz /path; tar xzf archive.tar.gz
```

### Docker
```bash
docker ps -a; docker logs -f name; docker exec -it name bash
docker build -t name:tag .; docker push registry/name:tag
docker compose up -d; docker compose logs -f; docker system prune -a
```

### Kubernetes
```bash
kubectl get pods -n ns; kubectl describe pod name -n ns
kubectl logs -f pod -n ns; kubectl exec -it pod -n ns -- bash
kubectl apply -f file.yaml; kubectl delete -f file.yaml
kubectl rollout undo deployment/name -n ns; kubectl scale deployment name --replicas=5
```

### Git
```bash
git log --oneline --graph --all; git diff; git stash; git stash pop
git checkout -b feature/name; git rebase main; git cherry-pick SHA
git tag v1.0.0; git push origin --tags; git bisect start/good/bad
```

### Monitoring and Debugging
```bash
top; htop; vmstat 1; iostat -xz 1; iftop; nethogs
strace -p PID; lsof -p PID; /proc/PID/status; /proc/PID/fd/
perf top; perf stat cmd; tcpdump -i eth0 port 80 -w capture.pcap
```

---

## Recommended Learning Path

**Month 1 (Foundation):**
- Parts 1–4: Installation, file system, shell basics, permissions
- Daily: 30 min of command-line practice (try `vimtutor` for vim)
- Project: Set up a personal Ubuntu server on a VM

**Month 2 (Core Skills):**
- Parts 5–8: Process management, networking, packages, scripting
- Daily: Write one shell script that automates something in your workflow
- Project: Write a system health-check script that emails a report

**Month 3 (DevOps Tools):**
- Parts 9–12: Storage, monitoring, Git, Docker
- Project: Dockerize a sample web application and run it locally

**Month 4 (Advanced DevOps):**
- Parts 13–15: CI/CD, IaC with Terraform/Ansible, security
- Project: Build a full CI/CD pipeline using GitHub Actions

**Month 5 (Professional Level):**
- Parts 16–17: AI integration, real-world scenarios
- Project: Deploy a Kubernetes cluster on a cloud provider with monitoring

---

*Guide Version: 2026 Edition | Last Updated: April 2026*
*This guide is designed to evolve with you — revisit advanced sections as your experience grows.*
