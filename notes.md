Creating a **complete Linux guide for a DevOps Engineer** (from beginner to pro) in a single PDF is a massive task, but I’ll provide you with a **structured roadmap**, **key topics**, **commands with examples**, and **resources** to help you master Linux for DevOps.

Since I can't directly generate a PDF here, I’ll give you a **detailed breakdown** of all the topics you need to cover, along with **commands, examples, and explanations**. You can copy this into a **Google Doc/Word** and export it as a PDF.

---

# **📌 Complete Linux Guide for DevOps Engineers (Beginner to Pro)**
*(From Non-IT to DevOps Expert)*

---

## **📌 Table of Contents**
1. **Introduction to Linux & DevOps**
2. **Linux Basics (For Absolute Beginners)**
3. **Linux File System & Directory Structure**
4. **Basic Linux Commands (With Examples)**
5. **File Permissions & Ownership (chmod, chown, umask)**
6. **User & Group Management (useradd, usermod, passwd, groupadd)**
7. **Package Management (APT, YUM, DNF, Snap, Flatpak)**
8. **Process Management (ps, top, htop, kill, systemctl)**
9. **Networking in Linux (ifconfig, ip, netstat, ss, ping, curl, wget, nmap)**
10. **Shell Scripting (Bash Scripting for Automation)**
11. **Text Processing (grep, awk, sed, cut, sort, uniq, tr)**
12. **Log Management (journalctl, tail, cat, less, more, logrotate)**
13. **Storage & Disk Management (df, du, fdisk, lsblk, mount, lvm)**
14. **SSH & Remote Access (ssh, scp, rsync, ssh-keygen)**
15. **Cron Jobs & Task Scheduling (crontab, at, systemd timers)**
16. **Security & Firewall (ufw, iptables, firewalld, SELinux, AppArmor)**
17. **Containerization Basics (Docker, Podman, LXC)**
18. **Linux for DevOps Tools (Git, Jenkins, Ansible, Kubernetes, Terraform)**
19. **Troubleshooting & Debugging (strace, lsof, dmesg, sar, vmstat)**
20. **Advanced Linux Concepts (Namespaces, cgroups, System Calls, Kernel Tuning)**
21. **Cloud & Linux (AWS, Azure, GCP CLI Tools)**
22. **Final Project: Automating a DevOps Workflow with Linux**

---

# **📌 1. Introduction to Linux & DevOps**
### **Why Linux for DevOps?**
- **Open-source & Free** (No licensing costs)
- **Stable & Secure** (Used in 90% of cloud servers)
- **Supports Automation** (Bash, Python, Ansible, etc.)
- **Works with DevOps Tools** (Docker, Kubernetes, Jenkins, Terraform)

### **Linux Distributions for DevOps**
| Distro | Best For | Package Manager |
|--------|---------|----------------|
| **Ubuntu/Debian** | Beginners, Cloud | `apt` |
| **CentOS/RHEL** | Enterprise, Servers | `yum`/`dnf` |
| **Fedora** | Latest Features | `dnf` |
| **Arch Linux** | Advanced Users | `pacman` |
| **Alpine Linux** | Containers (Lightweight) | `apk` |

### **DevOps Workflow with Linux**
1. **Code** (Git, GitHub, GitLab)
2. **Build** (Maven, Gradle, Docker)
3. **Test** (JUnit, Selenium, Postman)
4. **Deploy** (Ansible, Kubernetes, Terraform)
5. **Monitor** (Prometheus, Grafana, ELK Stack)

---

# **📌 2. Linux Basics (For Absolute Beginners)**
### **What is a Terminal?**
- **Command-line interface (CLI)** to interact with Linux.
- **Shortcuts:**
  - `Ctrl + C` → Stop current command
  - `Ctrl + D` → Exit terminal (or `exit`)
  - `Ctrl + Z` → Suspend process
  - `Tab` → Auto-complete
  - `↑↓` → Navigate command history

### **First Commands to Learn**
| Command | Description | Example |
|---------|------------|---------|
| `whoami` | Show current user | `whoami` → `ubuntu` |
| `hostname` | Show system hostname | `hostname` → `devops-server` |
| `uname -a` | Show kernel version | `uname -a` |
| `date` | Show current date/time | `date` |
| `cal` | Show calendar | `cal 2024` |
| `clear` | Clear terminal | `clear` |
| `man <command>` | Manual page | `man ls` |
| `--help` | Help for a command | `ls --help` |

---

# **📌 3. Linux File System & Directory Structure**
### **Linux Directory Hierarchy (FHS - Filesystem Hierarchy Standard)**
| Directory | Purpose |
|-----------|---------|
| `/` | Root directory |
| `/bin` | Essential binary (executable) files |
| `/sbin` | System binary files (admin commands) |
| `/etc` | Configuration files |
| `/home` | User home directories |
| `/var` | Variable data (logs, databases) |
| `/tmp` | Temporary files |
| `/usr` | User programs & libraries |
| `/opt` | Optional/third-party software |
| `/dev` | Device files (hardware) |
| `/proc` | Kernel & process info (virtual FS) |
| `/boot` | Boot loader files |

### **Absolute vs. Relative Paths**
- **Absolute Path:** `/home/user/file.txt` (Full path from root)
- **Relative Path:** `../documents/file.txt` (Relative to current dir)

### **Commands for Navigation**
| Command | Description | Example |
|---------|------------|---------|
| `pwd` | Print working directory | `pwd` → `/home/user` |
| `ls` | List files/directories | `ls -l` (detailed view) |
| `cd` | Change directory | `cd /var/log` |
| `mkdir` | Make directory | `mkdir my_folder` |
| `rmdir` | Remove empty directory | `rmdir my_folder` |
| `touch` | Create empty file | `touch file.txt` |
| `cp` | Copy file/directory | `cp file.txt /backup/` |
| `mv` | Move/rename file | `mv old.txt new.txt` |
| `rm` | Remove file | `rm file.txt` |
| `rm -r` | Remove directory recursively | `rm -r my_folder` |

---

# **📌 4. Basic Linux Commands (With Examples)**
### **File Operations**
| Command | Description | Example |
|---------|------------|---------|
| `cat` | Display file content | `cat file.txt` |
| `less` | View file page by page | `less /var/log/syslog` |
| `head` | Show first 10 lines | `head -n 5 file.txt` |
| `tail` | Show last 10 lines | `tail -f /var/log/syslog` (live log) |
| `grep` | Search text in file | `grep "error" log.txt` |
| `find` | Find files/directories | `find /home -name "*.txt"` |
| `locate` | Fast file search (requires `updatedb`) | `locate file.txt` |
| `wc` | Word/line count | `wc -l file.txt` (line count) |

### **File Permissions (chmod, chown, umask)**
| Command | Description | Example |
|---------|------------|---------|
| `chmod` | Change file permissions | `chmod 755 script.sh` |
| `chown` | Change owner | `chown user:group file.txt` |
| `umask` | Default permissions | `umask 022` |

**Permission Numbers:**
- `4` → Read (r)
- `2` → Write (w)
- `1` → Execute (x)

| Permission | Owner | Group | Others |
|------------|-------|-------|--------|
| `755` | `rwx` | `r-x` | `r-x` |
| `644` | `rw-` | `r--` | `r--` |

**Example:**
```bash
chmod 755 script.sh  # Owner: rwx, Group: r-x, Others: r-x
chown root:root file.txt  # Change owner to root
```

---

# **📌 5. User & Group Management**
### **User Commands**
| Command | Description | Example |
|---------|------------|---------|
| `useradd` | Add a new user | `useradd -m devops` |
| `usermod` | Modify user | `usermod -aG sudo devops` (add to sudo) |
| `passwd` | Set password | `passwd devops` |
| `userdel` | Delete user | `userdel -r devops` (remove home dir) |
| `id` | Show user info | `id devops` |
| `who` | Show logged-in users | `who` |
| `last` | Show login history | `last` |

### **Group Commands**
| Command | Description | Example |
|---------|------------|---------|
| `groupadd` | Create group | `groupadd developers` |
| `groupdel` | Delete group | `groupdel developers` |
| `usermod -aG` | Add user to group | `usermod -aG developers devops` |
| `groups` | Show user groups | `groups devops` |

---

# **📌 6. Package Management (APT, YUM, DNF, Snap, Flatpak)**
### **Debian/Ubuntu (APT)**
| Command | Description | Example |
|---------|------------|---------|
| `sudo apt update` | Update package list | `sudo apt update` |
| `sudo apt upgrade` | Upgrade installed packages | `sudo apt upgrade -y` |
| `sudo apt install` | Install a package | `sudo apt install nginx` |
| `sudo apt remove` | Remove a package | `sudo apt remove nginx` |
| `sudo apt autoremove` | Remove unused packages | `sudo apt autoremove` |
| `apt search` | Search for a package | `apt search docker` |

### **RHEL/CentOS (YUM/DNF)**
| Command | Description | Example |
|---------|------------|---------|
| `sudo yum update` | Update all packages | `sudo yum update -y` |
| `sudo yum install` | Install a package | `sudo yum install httpd` |
| `sudo yum remove` | Remove a package | `sudo yum remove httpd` |
| `yum search` | Search for a package | `yum search nginx` |

### **Snap & Flatpak (Universal Packages)**
| Command | Description | Example |
|---------|------------|---------|
| `sudo snap install` | Install a snap package | `sudo snap install docker` |
| `flatpak install` | Install a flatpak | `flatpak install flathub com.spotify.Client` |

---

# **📌 7. Process Management (ps, top, htop, kill, systemctl)**
### **Viewing Processes**
| Command | Description | Example |
|---------|------------|---------|
| `ps` | List processes | `ps aux` (all users) |
| `top` | Interactive process viewer | `top` |
| `htop` | Better `top` alternative | `htop` |
| `pgrep` | Find process by name | `pgrep nginx` |
| `pkill` | Kill process by name | `pkill firefox` |

### **Killing Processes**
| Command | Description | Example |
|---------|------------|---------|
| `kill` | Terminate process by PID | `kill 1234` |
| `kill -9` | Force kill | `kill -9 1234` |
| `pkill` | Kill by name | `pkill -9 firefox` |

### **Systemd (Service Management)**
| Command | Description | Example |
|---------|------------|---------|
| `systemctl start` | Start a service | `sudo systemctl start nginx` |
| `systemctl stop` | Stop a service | `sudo systemctl stop nginx` |
| `systemctl restart` | Restart a service | `sudo systemctl restart nginx` |
| `systemctl enable` | Enable at boot | `sudo systemctl enable nginx` |
| `systemctl status` | Check service status | `sudo systemctl status nginx` |
| `journalctl` | View logs | `journalctl -u nginx` |

---

# **📌 8. Networking in Linux**
### **Basic Networking Commands**
| Command | Description | Example |
|---------|------------|---------|
| `ifconfig` | Show network interfaces | `ifconfig` |
| `ip a` | Modern alternative to `ifconfig` | `ip a` |
| `ping` | Test connectivity | `ping google.com` |
| `netstat` | Network statistics | `netstat -tuln` |
| `ss` | Modern alternative to `netstat` | `ss -tuln` |
| `curl` | Transfer data (APIs, downloads) | `curl https://api.github.com` |
| `wget` | Download files | `wget https://example.com/file.zip` |
| `nmap` | Network scanning | `nmap -sP 192.168.1.0/24` |

### **Firewall (UFW, iptables, firewalld)**
#### **UFW (Uncomplicated Firewall - Ubuntu)**
```bash
sudo ufw enable          # Enable firewall
sudo ufw allow 22        # Allow SSH
sudo ufw allow 80/tcp    # Allow HTTP
sudo ufw status          # Check rules
```

#### **Firewalld (RHEL/CentOS)**
```bash
sudo systemctl start firewalld
sudo firewall-cmd --add-port=80/tcp --permanent
sudo firewall-cmd --reload
sudo firewall-cmd --list-all
```

---

# **📌 9. Shell Scripting (Bash Automation)**
### **Basic Bash Script**
```bash
#!/bin/bash
# My first script

echo "Hello, $USER!"
echo "Today is $(date)"
```

**Save as `script.sh` and run:**
```bash
chmod +x script.sh
./script.sh
```

### **Variables & User Input**
```bash
#!/bin/bash

NAME="DevOps"
echo "Hello, $NAME!"

read -p "Enter your name: " USER_NAME
echo "Welcome, $USER_NAME!"
```

### **Conditionals (if-else)**
```bash
#!/bin/bash

read -p "Enter a number: " NUM

if [ $NUM -gt 10 ]; then
    echo "Number is greater than 10"
elif [ $NUM -eq 10 ]; then
    echo "Number is 10"
else
    echo "Number is less than 10"
fi
```

### **Loops (for, while)**
```bash
#!/bin/bash

# For loop
for i in {1..5}; do
    echo "Number: $i"
done

# While loop
COUNT=0
while [ $COUNT -lt 5 ]; do
    echo "Count: $COUNT"
    COUNT=$((COUNT + 1))
done
```

### **Functions**
```bash
#!/bin/bash

greet() {
    echo "Hello, $1!"
}

greet "DevOps Engineer"
```

---

# **📌 10. Text Processing (grep, awk, sed, cut, sort, uniq, tr)**
### **grep (Search Text)**
| Command | Description | Example |
|---------|------------|---------|
| `grep "text"` | Search in file | `grep "error" log.txt` |
| `grep -i` | Case-insensitive | `grep -i "warning" log.txt` |
| `grep -v` | Invert match | `grep -v "success" log.txt` |
| `grep -r` | Recursive search | `grep -r "function" /home/` |

### **awk (Text Processing)**
| Command | Description | Example |
|---------|------------|---------|
| `awk '{print $1}'` | Print first column | `awk '{print $1}' data.txt` |
| `awk -F','` | Set delimiter | `awk -F',' '{print $2}' data.csv` |
| `awk 'NR==1'` | Print first line | `awk 'NR==1' file.txt` |

### **sed (Stream Editor)**
| Command | Description | Example |
|---------|------------|---------|
| `sed 's/old/new/'` | Replace text | `sed 's/error/warning/' file.txt` |
| `sed -i` | Edit file in-place | `sed -i 's/old/new/' file.txt` |
| `sed '3d'` | Delete 3rd line | `sed '3d' file.txt` |

### **cut (Extract Columns)**
| Command | Description | Example |
|---------|------------|---------|
| `cut -d',' -f1` | Extract 1st column (CSV) | `cut -d',' -f1 data.csv` |

### **sort & uniq (Sort & Remove Duplicates)**
| Command | Description | Example |
|---------|------------|---------|
| `sort file.txt` | Sort lines | `sort names.txt` |
| `uniq` | Remove duplicates | `sort file.txt | uniq` |
| `uniq -c` | Count duplicates | `sort file.txt | uniq -c` |

---

# **📌 11. Log Management (journalctl, tail, cat, less, logrotate)**
### **Viewing Logs**
| Command | Description | Example |
|---------|------------|---------|
| `tail -f /var/log/syslog` | Follow log in real-time | `tail -f /var/log/nginx/error.log` |
| `journalctl -u nginx` | View service logs | `journalctl -u docker --since "1 hour ago"` |
| `cat /var/log/auth.log` | View auth logs | `cat /var/log/auth.log | grep "failed"` |

### **Log Rotation (logrotate)**
**Config File:** `/etc/logrotate.conf`
**Example:**
```bash
/var/log/nginx/*.log {
    daily
    missingok
    rotate 7
    compress
    delaycompress
    notifempty
    create 0640 www-data adm
    sharedscripts
    postrotate
        systemctl reload nginx
    endscript
}
```

---

# **📌 12. Storage & Disk Management (df, du, fdisk, lsblk, mount, LVM)**
### **Disk Usage Commands**
| Command | Description | Example |
|---------|------------|---------|
| `df -h` | Disk free space | `df -h` |
| `du -sh /home` | Directory size | `du -sh /var/log` |
| `lsblk` | List block devices | `lsblk` |
| `fdisk -l` | List partitions | `sudo fdisk -l` |

### **Mounting Drives**
```bash
sudo mkdir /mnt/mydrive
sudo mount /dev/sdb1 /mnt/mydrive
```
**Permanent Mount (edit `/etc/fstab`):**
```bash
/dev/sdb1  /mnt/mydrive  ext4  defaults  0  2
```
Then run:
```bash
sudo mount -a
```

### **LVM (Logical Volume Management)**
| Command | Description | Example |
|---------|------------|---------|
| `pvcreate` | Create physical volume | `sudo pvcreate /dev/sdb1` |
| `vgcreate` | Create volume group | `sudo vgcreate myvg /dev/sdb1` |
| `lvcreate` | Create logical volume | `sudo lvcreate -L 10G -n mylv myvg` |
| `mkfs.ext4` | Format LV | `sudo mkfs.ext4 /dev/myvg/mylv` |
| `mount` | Mount LV | `sudo mount /dev/myvg/mylv /mnt` |

---

# **📌 13. SSH & Remote Access (ssh, scp, rsync, ssh-keygen)**
### **SSH (Secure Shell)**
| Command | Description | Example |
|---------|------------|---------|
| `ssh user@host` | Connect to remote server | `ssh devops@192.168.1.10` |
| `ssh -p 2222` | Custom port | `ssh -p 2222 user@host` |
| `ssh-keygen` | Generate SSH key | `ssh-keygen -t rsa -b 4096` |
| `ssh-copy-id` | Copy key to server | `ssh-copy-id user@host` |

### **SCP (Secure Copy)**
| Command | Description | Example |
|---------|------------|---------|
| `scp file.txt user@host:/path` | Copy file to remote | `scp script.sh devops@192.168.1.10:/home/` |
| `scp -r dir/ user@host:/path` | Copy directory | `scp -r my_folder devops@host:/backup/` |

### **rsync (Fast File Transfer)**
| Command | Description | Example |
|---------|------------|---------|
| `rsync -avz source/ dest/` | Sync directories | `rsync -avz /local/ user@host:/remote/` |
| `rsync --delete` | Delete extra files | `rsync -avz --delete /local/ user@host:/remote/` |

---

# **📌 14. Cron Jobs & Task Scheduling**
### **Crontab (Schedule Tasks)**
| Command | Description | Example |
|---------|------------|---------|
| `crontab -e` | Edit cron jobs | `crontab -e` |
| `crontab -l` | List cron jobs | `crontab -l` |

**Cron Syntax:**
```
* * * * * command
│ │ │ │ │
│ │ │ │ └── Day of the Week (0-6, 0=Sunday)
│ │ │ └──── Month (1-12)
│ │ └────── Day of Month (1-31)
│ └──────── Hour (0-23)
└────────── Minute (0-59)
```

**Examples:**
```bash
# Run every day at 3 AM
0 3 * * * /backup/script.sh

# Run every 5 minutes
*/5 * * * * /home/user/check_status.sh

# Run at reboot
@reboot /home/user/startup_script.sh
```

### **Systemd Timers (Alternative to Cron)**
```bash
# Create a service
sudo nano /etc/systemd/system/backup.service
```
```ini
[Unit]
Description=Backup Script

[Service]
ExecStart=/backup/script.sh
```
```bash
# Create a timer
sudo nano /etc/systemd/system/backup.timer
```
```ini
[Unit]
Description=Run backup daily

[Timer]
OnCalendar=daily
Persistent=true

[Install]
WantedBy=timers.target
```
**Enable & Start:**
```bash
sudo systemctl enable backup.timer
sudo systemctl start backup.timer
```

---

# **📌 15. Security & Firewall (SELinux, AppArmor, iptables)**
### **SELinux (Security-Enhanced Linux)**
| Command | Description | Example |
|---------|------------|---------|
| `getenforce` | Check SELinux status | `getenforce` (Enforcing/Permissive/Disabled) |
| `setenforce 0` | Set to Permissive | `sudo setenforce 0` |
| `sestatus` | SELinux status | `sestatus` |
| `chcon` | Change file context | `sudo chcon -t httpd_sys_content_t /var/www/html/` |

### **AppArmor (Alternative to SELinux)**
| Command | Description | Example |
|---------|------------|---------|
| `aa-status` | Check AppArmor status | `sudo aa-status` |
| `aa-enforce` | Enforce a profile | `sudo aa-enforce /etc/apparmor.d/usr.sbin.nginx` |

### **iptables (Advanced Firewall)**
| Command | Description | Example |
|---------|------------|---------|
| `iptables -L` | List rules | `sudo iptables -L` |
| `iptables -A INPUT -p tcp --dport 22 -j ACCEPT` | Allow SSH | `sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT` |
| `iptables -A INPUT -j DROP` | Block all other traffic | `sudo iptables -A INPUT -j DROP` |
| `iptables-save` | Save rules | `sudo iptables-save > /etc/iptables.rules` |

---

# **📌 16. Containerization Basics (Docker, Podman, LXC)**
### **Docker Commands**
| Command | Description | Example |
|---------|------------|---------|
| `docker pull` | Download image | `docker pull nginx` |
| `docker run` | Run a container | `docker run -d -p 80:80 nginx` |
| `docker ps` | List running containers | `docker ps -a` |
| `docker stop` | Stop container | `docker stop container_id` |
| `docker rm` | Remove container | `docker rm container_id` |
| `docker images` | List images | `docker images` |
| `docker rmi` | Remove image | `docker rmi nginx` |
| `docker exec` | Run command in container | `docker exec -it container_id bash` |
| `docker build` | Build from Dockerfile | `docker build -t myapp .` |

### **Dockerfile Example**
```dockerfile
FROM ubuntu:22.04
RUN apt update && apt install -y nginx
COPY index.html /var/www/html/
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

**Build & Run:**
```bash
docker build -t my-nginx .
docker run -d -p 8080:80 my-nginx
```

---

# **📌 17. Linux for DevOps Tools**
### **Git (Version Control)**
| Command | Description | Example |
|---------|------------|---------|
| `git clone` | Clone repo | `git clone https://github.com/user/repo.git` |
| `git add` | Stage changes | `git add .` |
| `git commit` | Commit changes | `git commit -m "Initial commit"` |
| `git push` | Push to remote | `git push origin main` |
| `git pull` | Pull changes | `git pull origin main` |

### **Ansible (Configuration Management)**
**Install Ansible:**
```bash
sudo apt install ansible  # Ubuntu
sudo yum install ansible  # RHEL
```

**Basic Commands:**
| Command | Description | Example |
|---------|------------|---------|
| `ansible --version` | Check version | `ansible --version` |
| `ansible all -m ping` | Test connectivity | `ansible all -m ping` |
| `ansible-playbook` | Run playbook | `ansible-playbook playbook.yml` |

**Example Playbook (`nginx.yml`):**
```yaml
---
- hosts: webservers
  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present
    - name: Start Nginx
      service:
        name: nginx
        state: started
        enabled: yes
```

### **Kubernetes (kubectl Commands)**
| Command | Description | Example |
|---------|------------|---------|
| `kubectl get pods` | List pods | `kubectl get pods -A` |
| `kubectl describe pod` | Pod details | `kubectl describe pod my-pod` |
| `kubectl logs` | Pod logs | `kubectl logs my-pod` |
| `kubectl apply -f` | Apply YAML | `kubectl apply -f deployment.yaml` |
| `kubectl delete` | Delete resource | `kubectl delete pod my-pod` |

---

# **📌 18. Troubleshooting & Debugging**
### **Common Debugging Commands**
| Command | Description | Example |
|---------|------------|---------|
| `dmesg` | Kernel logs | `dmesg | grep error` |
| `lsof` | List open files | `lsof -i :80` (check port 80) |
| `strace` | Trace system calls | `strace ls` |
| `vmstat` | Virtual memory stats | `vmstat 1` |
| `sar` | System activity report | `sar -u 1 5` (CPU usage) |
| `free -h` | Memory usage | `free -h` |
| `top` | Process monitoring | `top` |
| `htop` | Interactive process viewer | `htop` |

### **Network Troubleshooting**
| Command | Description | Example |
|---------|------------|---------|
| `ping` | Test connectivity | `ping google.com` |
| `traceroute` | Trace route | `traceroute google.com` |
| `mtr` | Combines ping & traceroute | `mtr google.com` |
| `nslookup` | DNS lookup | `nslookup google.com` |
| `dig` | DNS query | `dig google.com` |
| `netstat -tuln` | Open ports | `netstat -tuln` |
| `ss -tuln` | Modern alternative | `ss -tuln` |

---

# **📌 19. Advanced Linux Concepts**
### **Namespaces (Isolation)**
- **PID Namespace** → Isolate processes
- **Network Namespace** → Isolate network
- **Mount Namespace** → Isolate filesystem
- **User Namespace** → Isolate users

**Example (Create a new network namespace):**
```bash
sudo ip netns add myns
sudo ip netns exec myns ip a
```

### **cgroups (Resource Limits)**
- **CPU, Memory, Disk I/O limits**
- Used by **Docker & Kubernetes**

**Example (Limit CPU):**
```bash
sudo cgcreate -g cpu:/mygroup
sudo cgset -r cpu.cfs_quota_us=50000 mygroup
sudo cgexec -g cpu:mygroup stress --cpu 1
```

### **System Calls (strace)**
```bash
strace ls  # Trace system calls for 'ls'
strace -c ls  # Summary of calls
```

### **Kernel Tuning (sysctl)**
| Command | Description | Example |
|---------|------------|---------|
| `sysctl -a` | List all kernel params | `sysctl -a` |
| `sysctl net.ipv4.ip_forward=1` | Enable IP forwarding | `sudo sysctl -w net.ipv4.ip_forward=1` |
| `/etc/sysctl.conf` | Permanent changes | `echo "vm.swappiness=10" | sudo tee -a /etc/sysctl.conf` |

---

# **📌 20. Cloud & Linux (AWS, Azure, GCP CLI)**
### **AWS CLI**
| Command | Description | Example |
|---------|------------|---------|
| `aws configure` | Set up AWS CLI | `aws configure` |
| `aws ec2 describe-instances` | List EC2 instances | `aws ec2 describe-instances` |
| `aws s3 ls` | List S3 buckets | `aws s3 ls` |

### **Azure CLI**
| Command | Description | Example |
|---------|------------|---------|
| `az login` | Login to Azure | `az login` |
| `az vm list` | List VMs | `az vm list` |
| `az storage account list` | List storage accounts | `az storage account list` |

### **GCP CLI (gcloud)**
| Command | Description | Example |
|---------|------------|---------|
| `gcloud init` | Initialize GCP CLI | `gcloud init` |
| `gcloud compute instances list` | List VMs | `gcloud compute instances list` |
| `gcloud storage ls` | List buckets | `gcloud storage ls` |

---

# **📌 21. Final Project: Automating a DevOps Workflow**
### **Project: Deploy a Web App with Nginx, Docker, and CI/CD**
1. **Write a Bash script** to install Docker & Nginx.
2. **Create a Dockerfile** for a simple web app.
3. **Set up a GitHub Actions CI/CD pipeline** to:
   - Build Docker image on push.
   - Deploy to a Linux server.
4. **Use Ansible** to configure the server.
5. **Monitor** with Prometheus & Grafana.

**Example Script (`setup_server.sh`):**
```bash
#!/bin/bash

# Update system
sudo apt update -y
sudo apt upgrade -y

# Install Docker
sudo apt install -y docker.io
sudo systemctl enable docker
sudo systemctl start docker

# Install Nginx
sudo apt install -y nginx
sudo systemctl enable nginx
sudo systemctl start nginx

# Deploy a sample app
sudo docker run -d -p 80:80 nginx
```

**GitHub Actions Workflow (`.github/workflows/deploy.yml`):**
```yaml
name: Deploy to Server

on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Build Docker image
        run: docker build -t myapp .

      - name: Log in to Docker Hub
        run: echo "${{ secrets.DOCKER_PASSWORD }}" | docker login -u "${{ secrets.DOCKER_USERNAME }}" --password-stdin

      - name: Push to Docker Hub
        run: docker push myapp

      - name: SSH and Deploy
        uses: appleboy/ssh-action@master
        with:
          host: ${{ secrets.SERVER_IP }}
          username: ${{ secrets.SERVER_USER }}
          key: ${{ secrets.SSH_KEY }}
          script: |
            docker pull myapp
            docker stop myapp || true
            docker rm myapp || true
            docker run -d -p 80:80 --name myapp myapp
```

---

# **📌 How to Convert This to PDF**
1. **Copy all content** into **Google Docs** or **Microsoft Word**.
2. **Format properly** (headings, code blocks, tables).
3. **Export as PDF**:
   - **Google Docs:** `File → Download → PDF`
   - **Word:** `File → Export → PDF`

---

# **📌 Additional Resources**
### **Books**
- **The Linux Command Line** (William Shotts)
- **Linux Pocket Guide** (Daniel J. Barrett)
- **DevOps Handbook** (Gene Kim)

### **Online Courses**
- [Linux for DevOps (Udemy)](https://www.udemy.com/)
- [Linux Foundation Courses](https://training.linuxfoundation.org/)
- [DevOps Bootcamp (KodeKloud)](https://kodekloud.com/)

### **Practice Labs**
- [OverTheWire (Bandit)](https://overthewire.org/wargames/bandit/)
- [Linux Journey](https://linuxjourney.com/)
- [KodeKloud Engineer](https://kodekloud.com/)

---

# **📌 Final Notes**
- **Practice daily** (Use a VM or [Play with Docker](https://labs.play-with-docker.com/))
- **Automate everything** (Bash, Python, Ansible)
- **Learn troubleshooting** (`dmesg`, `journalctl`, `strace`)
- **Master DevOps tools** (Docker, Kubernetes, Terraform, Jenkins)

---

### **🚀 Next Steps**
1. **Set up a Linux VM** (VirtualBox, AWS EC2, or GCP).
2. **Practice commands** daily.
3. **Automate tasks** with Bash & Ansible.
4. **Learn Docker & Kubernetes**.
5. **Build CI/CD pipelines** (GitHub Actions, Jenkins).

---

**📄 Want a PDF?**
Copy this into **Google Docs** → **Format** → **Export as PDF**.

Would you like me to **focus on any specific section** in more detail? 😊
