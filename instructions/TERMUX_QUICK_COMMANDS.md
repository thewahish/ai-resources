# 📱 Termux Quick Command Reference

**Essential commands to run on your Google Pixel**

---

## 🚀 STEP 1: Setup Termux (First Time Only)

**On your Google Pixel, open Termux and run:**

```bash
# Update packages
pkg update && pkg upgrade -y

# Install essential tools
pkg install -y git nodejs openssh python rsync nano

# Install Claude Code
npm install -g @anthropic-ai/claude-code

# Set password for SSH
passwd

# Start SSH server
sshd

# Find your IP address
ip addr show wlan0 | grep inet
```

**Copy your IP address** (e.g., 192.168.1.100) - you'll need it for the Mac!

---

## 🖥️ STEP 2: Transfer Files from Mac

**On your Mac, run:**

```bash
/Volumes/Ai/transfer-to-termux.sh
```

Enter your Pixel's IP when prompted. The script will transfer everything automatically.

---

## 📱 STEP 3: After Transfer (On Termux)

**On your Pixel in Termux:**

```bash
# Reload environment
source ~/.bashrc

# Check everything arrived
ls -la ~/Ai/

# Navigate to projects
cdprojects

# List all projects
ls
```

---

## 🤖 STEP 4: Use Claude Code

```bash
# Go to a project
cd ~/Ai/Projects/ai-courses

# Start Claude Code
claude

# Or specify model
claude --model claude-sonnet-4
```

---

## 📋 Useful Aliases (Already Set Up)

```bash
cdai              # Go to ~/Ai/
cdprojects        # Go to ~/Ai/Projects/
cdmaster          # Go to ~/Ai/.Master/

ai-courses        # Go to ai-courses project
website           # Go to website project
website2          # Go to website2.0 project

projects          # List all projects
```

---

## 🔧 If You Need to Restart SSH

```bash
# Kill SSH server
pkill sshd

# Start SSH server again
sshd

# Check if running
pgrep sshd
```

---

## 📂 Access Android Storage

```bash
# Grant storage access (one time)
termux-setup-storage

# Now you can access:
~/storage/shared      # Internal storage
~/storage/downloads   # Downloads folder
~/storage/dcim        # Camera/Photos
```

---

## 🔄 Keep Termux Running in Background

```bash
# Acquire wake lock (prevents Android from killing Termux)
termux-wake-lock

# Release wake lock
termux-wake-unlock
```

---

## 💾 Backup/Restore

**Backup to Android storage:**

```bash
# Backup everything
tar -czf ~/storage/downloads/ai-backup-$(date +%Y%m%d).tar.gz ~/Ai

# List backups
ls -lh ~/storage/downloads/ai-backup*
```

**Restore:**

```bash
cd ~
tar -xzf ~/storage/downloads/ai-backup-20250120.tar.gz
```

---

## 🆘 Troubleshooting

### Claude Code not found

```bash
npm install -g @anthropic-ai/claude-code
which claude
```

### SSH not working

```bash
# Check if running
pgrep sshd

# Restart
pkill sshd
sshd

# Verify password is set
passwd
```

### Scripts don't work

```bash
# Make executable
chmod +x ~/Ai/.Master/scripts/*.sh

# Update paths
cd ~/Ai/.Master/scripts
sed -i 's|/Volumes/Ai|~/Ai|g' *.sh
```

---

## 📱 Essential Termux Commands

```bash
pkg update            # Update package lists
pkg upgrade           # Upgrade installed packages
pkg install <name>    # Install a package
pkg search <name>     # Search for a package
pkg list-installed    # List installed packages

exit                  # Exit Termux
clear                 # Clear screen
```

---

## 🎯 Complete Setup in One Go

**Copy-paste this entire block into Termux:**

```bash
# Initial setup
pkg update && pkg upgrade -y && \
pkg install -y git nodejs openssh python rsync nano && \
npm install -g @anthropic-ai/claude-code && \
mkdir -p ~/Ai/{.Master,Projects,Desktop} && \
passwd && \
sshd && \
echo "" && \
echo "✓ Setup complete!" && \
echo "" && \
echo "Your IP address:" && \
ip addr show wlan0 | grep inet && \
echo "" && \
echo "Run this on your Mac:" && \
echo "/Volumes/Ai/transfer-to-termux.sh"
```

---

## 📊 Check Status

```bash
# Check Node.js
node --version

# Check Git
git --version

# Check Claude Code
claude --version

# Check SSH
pgrep sshd && echo "SSH running" || echo "SSH not running"

# Check projects
ls -la ~/Ai/Projects/

# Check disk space
df -h ~
```

---

**That's it! You're ready to use Claude Code on your Google Pixel! 📱✨**
