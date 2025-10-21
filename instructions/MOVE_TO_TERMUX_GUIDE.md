# 📱 Moving Everything to Termux (Google Pixel)

**Goal:** Transfer all projects from Mac to Termux and run Claude Code on Android

---

## 🎯 Overview

You'll be moving:
- `/Volumes/Ai/.Master/` - Your master prompt system
- `/Volumes/Ai/Projects/` - All 9 projects
- Everything else you need

**New location on Termux:** `/data/data/com.termux/files/home/Ai/`

---

## 📋 Step-by-Step Guide

### Part 1: Setup Termux on Google Pixel (15 minutes)

### Part 2: Transfer Files from Mac to Pixel (30-60 minutes)

### Part 3: Install Claude Code on Termux (10 minutes)

### Part 4: Adapt Scripts for Termux (5 minutes)

---

## 🚀 PART 1: Setup Termux on Google Pixel

### Step 1: Install Termux

**Option A: F-Droid (Recommended)**
```
1. Install F-Droid app from: https://f-droid.org/
2. Open F-Droid
3. Search "Termux"
4. Install "Termux" (NOT from Google Play - outdated!)
```

**Option B: GitHub (Direct APK)**
```
1. Go to: https://github.com/termux/termux-app/releases
2. Download latest APK
3. Install it
```

### Step 2: Initial Termux Setup

Open Termux and run these commands:

```bash
# Update package lists
pkg update && pkg upgrade -y

# Install essential packages
pkg install -y git curl wget openssh nodejs python rsync

# Install Claude Code
npm install -g @anthropic-ai/claude-code

# Verify installations
node --version
git --version
claude --version

# Create directory structure
mkdir -p ~/Ai/.Master
mkdir -p ~/Ai/Projects
mkdir -p ~/Ai/Desktop
mkdir -p ~/Ai/Documents
```

### Step 3: Setup SSH Server (for file transfer)

```bash
# Install SSH server
pkg install openssh -y

# Set password for SSH access
passwd
# (Enter a password when prompted)

# Start SSH server
sshd

# Find your Pixel's IP address
ifconfig
# Look for "inet" address (e.g., 192.168.1.100)
# Or use: ip addr show wlan0 | grep inet
```

**Important:** Note your IP address and port (default: 8022)

---

## 📂 PART 2: Transfer Files from Mac to Pixel

### Method 1: Using rsync over SSH (Recommended - Fastest)

**On your Mac, run these commands:**

```bash
# Replace YOUR_PIXEL_IP with your Pixel's IP address
PIXEL_IP="192.168.1.XXX"  # Change this!

# Test connection first
ssh -p 8022 u0_a123@$PIXEL_IP
# (Use your Termux username - shown when you type 'whoami' in Termux)
# Enter the password you set earlier

# Exit and start transfer
exit

# Transfer .Master folder (critical!)
rsync -avz -e "ssh -p 8022" \
  /Volumes/Ai/.Master/ \
  u0_a123@$PIXEL_IP:/data/data/com.termux/files/home/Ai/.Master/

# Transfer Projects folder
rsync -avz -e "ssh -p 8022" \
  /Volumes/Ai/Projects/ \
  u0_a123@$PIXEL_IP:/data/data/com.termux/files/home/Ai/Projects/

# Transfer other folders you want
rsync -avz -e "ssh -p 8022" \
  /Volumes/Ai/Desktop/ \
  u0_a123@$PIXEL_IP:/data/data/com.termux/files/home/Ai/Desktop/

# Check progress
rsync -avz --progress -e "ssh -p 8022" \
  /Volumes/Ai/Projects/ \
  u0_a123@$PIXEL_IP:/data/data/com.termux/files/home/Ai/Projects/
```

**Transfer time estimate:**
- .Master: ~1 minute
- Projects (~141 MB): ~5-10 minutes (on same WiFi)
- Desktop: depends on size

### Method 2: Using USB Cable + adb (Alternative)

**Setup:**

```bash
# On Mac, install adb
brew install android-platform-tools

# On Pixel, enable Developer Options:
# Settings → About Phone → Tap "Build Number" 7 times
# Settings → Developer Options → Enable "USB Debugging"

# Connect Pixel to Mac via USB

# On Mac, verify connection
adb devices
# Should show your device

# Push files to Pixel
adb push /Volumes/Ai/.Master /sdcard/Download/
adb push /Volumes/Ai/Projects /sdcard/Download/

# Then in Termux on Pixel
cd ~/Ai
mv /sdcard/Download/.Master ./
mv /sdcard/Download/Projects ./
```

### Method 3: Cloud Storage (Slowest but Easiest)

**Using Google Drive / Dropbox:**

```bash
# On Mac
# 1. Upload /Volumes/Ai to Google Drive
# 2. Share the folder

# On Termux (Pixel)
pkg install rclone

# Configure rclone for Google Drive
rclone config
# Follow prompts to add Google Drive

# Download files
rclone copy gdrive:Ai ~/Ai --progress
```

---

## 🔧 PART 3: Adapt Scripts for Termux

Some paths need to change for Termux:

### Update Master Scripts

**On Termux, run:**

```bash
cd ~/Ai/.Master/scripts

# Update init-project.sh
sed -i 's|/Volumes/Ai|/data/data/com.termux/files/home/Ai|g' init-project.sh

# Update setup-existing.sh
sed -i 's|/Volumes/Ai|/data/data/com.termux/files/home/Ai|g' setup-existing.sh

# Update organize-projects.sh
sed -i 's|/Volumes/Ai|/data/data/com.termux/files/home/Ai|g' organize-projects.sh

# Update verify-setup.sh
sed -i 's|/Volumes/Ai|/data/data/com.termux/files/home/Ai|g' verify-setup.sh

# Or use the simpler home path
sed -i 's|/Volumes/Ai|~/Ai|g' *.sh
```

### Create Termux-Specific Aliases

```bash
# Add to ~/.bashrc or ~/.zshrc
cat >> ~/.bashrc << 'EOF'

# Claude Code aliases for Termux
export AI_ROOT="$HOME/Ai"
export PROJECTS_DIR="$AI_ROOT/Projects"
export MASTER_DIR="$AI_ROOT/.Master"

alias cdai="cd $AI_ROOT"
alias cdprojects="cd $PROJECTS_DIR"
alias cdmaster="cd $MASTER_DIR"

# Quick project access
alias ai-courses="cd $PROJECTS_DIR/ai-courses"
alias website="cd $PROJECTS_DIR/website"
alias website2="cd $PROJECTS_DIR/website2.0"

EOF

# Apply changes
source ~/.bashrc
```

---

## 🤖 PART 4: Running Claude Code on Termux

### Install Claude Code (if not done already)

```bash
# Install Node.js (if not installed)
pkg install nodejs -y

# Install Claude Code globally
npm install -g @anthropic-ai/claude-code

# Verify installation
claude --version
```

### Setup Claude Code

```bash
# Initialize Claude Code
claude init

# Login (if required)
claude login

# Or set API key
export ANTHROPIC_API_KEY="your-api-key-here"

# Add to ~/.bashrc for persistence
echo 'export ANTHROPIC_API_KEY="your-api-key-here"' >> ~/.bashrc
```

### Test Claude Code

```bash
# Navigate to a project
cd ~/Ai/Projects/ai-courses

# Start Claude Code
claude

# Or run with specific model
claude --model claude-sonnet-4
```

---

## 📝 Complete Command Reference for Termux

### Quick Setup (Copy-Paste)

**On your Google Pixel in Termux:**

```bash
# 1. Update and install essentials
pkg update && pkg upgrade -y
pkg install -y git curl wget openssh nodejs python rsync nano

# 2. Install Claude Code
npm install -g @anthropic-ai/claude-code

# 3. Create directory structure
mkdir -p ~/Ai/{.Master,Projects,Desktop,Documents,Media}

# 4. Setup SSH (for file transfer)
pkg install openssh -y
passwd  # Set a password
sshd    # Start SSH server

# 5. Get your IP address
ip addr show wlan0 | grep inet

# (Now transfer files from Mac - see Part 2)

# 6. After files are transferred, update scripts
cd ~/Ai/.Master/scripts
for file in *.sh; do
    sed -i 's|/Volumes/Ai|~/Ai|g' "$file"
done

# 7. Setup aliases
cat >> ~/.bashrc << 'EOF'
export AI_ROOT="$HOME/Ai"
export PROJECTS_DIR="$AI_ROOT/Projects"
alias cdai="cd $AI_ROOT"
alias cdprojects="cd $PROJECTS_DIR"
EOF

source ~/.bashrc

# 8. Verify everything
ls -la ~/Ai/
ls -la ~/Ai/Projects/
claude --version
```

---

## 🔍 Verification Checklist

After setup, verify everything works:

```bash
# Check directory structure
cd ~/Ai
ls -la

# Should see:
# .Master/
# Projects/
# Desktop/
# etc.

# Check .Master folder
ls -la ~/Ai/.Master/
# Should see: scripts/, CLAUDE_INSTRUCTIONS.md, etc.

# Check Projects
ls ~/Ai/Projects/
# Should see all 9 projects

# Check Git repositories
cd ~/Ai/Projects/ai-courses
git status

# Test Claude Code
claude --version

# Test a script
~/Ai/.Master/scripts/verify-setup.sh
```

---

## 🚀 PART 5: Full Transfer Script (Automated)

Save this on your **Mac** to automate the transfer:

**File:** `/Volumes/Ai/transfer-to-termux.sh`

```bash
#!/bin/bash

# Transfer to Termux Script
# Run this on your Mac

echo "🚀 Transfer to Termux - Automated Setup"
echo "========================================"
echo ""

# Configuration
read -p "Enter your Pixel's IP address: " PIXEL_IP
read -p "Enter your Termux username (default: u0_a123): " TERMUX_USER
TERMUX_USER=${TERMUX_USER:-u0_a123}
TERMUX_PORT=8022
TERMUX_HOME="/data/data/com.termux/files/home"

# Test connection
echo ""
echo "Testing connection..."
if ssh -p $TERMUX_PORT $TERMUX_USER@$PIXEL_IP "echo 'Connected!'" 2>/dev/null; then
    echo "✓ Connection successful!"
else
    echo "✗ Connection failed!"
    echo "Make sure:"
    echo "  1. Termux SSH server is running (run 'sshd' in Termux)"
    echo "  2. You've set a password (run 'passwd' in Termux)"
    echo "  3. IP address is correct"
    exit 1
fi

# Create directories on Termux
echo ""
echo "Creating directories on Termux..."
ssh -p $TERMUX_PORT $TERMUX_USER@$PIXEL_IP "mkdir -p ~/Ai/{.Master,Projects,Desktop,Documents}"
echo "✓ Directories created"

# Transfer .Master
echo ""
echo "Transferring .Master folder..."
rsync -avz --progress -e "ssh -p $TERMUX_PORT" \
    /Volumes/Ai/.Master/ \
    $TERMUX_USER@$PIXEL_IP:~/Ai/.Master/
echo "✓ .Master transferred"

# Transfer Projects
echo ""
echo "Transferring Projects folder..."
rsync -avz --progress -e "ssh -p $TERMUX_PORT" \
    /Volumes/Ai/Projects/ \
    $TERMUX_USER@$PIXEL_IP:~/Ai/Projects/
echo "✓ Projects transferred"

# Update scripts for Termux paths
echo ""
echo "Updating scripts for Termux paths..."
ssh -p $TERMUX_PORT $TERMUX_USER@$PIXEL_IP << 'ENDSSH'
cd ~/Ai/.Master/scripts
for file in *.sh; do
    if [ -f "$file" ]; then
        sed -i 's|/Volumes/Ai|~/Ai|g' "$file"
    fi
done
ENDSSH
echo "✓ Scripts updated"

# Setup aliases
echo ""
echo "Setting up aliases..."
ssh -p $TERMUX_PORT $TERMUX_USER@$PIXEL_IP << 'ENDSSH'
cat >> ~/.bashrc << 'EOF'

# Claude Code Setup
export AI_ROOT="$HOME/Ai"
export PROJECTS_DIR="$AI_ROOT/Projects"
alias cdai="cd $AI_ROOT"
alias cdprojects="cd $PROJECTS_DIR"
EOF
ENDSSH
echo "✓ Aliases configured"

# Summary
echo ""
echo "=========================================="
echo "✅ Transfer Complete!"
echo "=========================================="
echo ""
echo "Files transferred:"
echo "  • .Master/ → ~/Ai/.Master/"
echo "  • Projects/ → ~/Ai/Projects/"
echo ""
echo "On your Pixel in Termux, run:"
echo "  source ~/.bashrc"
echo "  cd ~/Ai"
echo "  ls -la"
echo ""
echo "Then install Claude Code:"
echo "  npm install -g @anthropic-ai/claude-code"
echo ""
echo "Enjoy Claude Code on your Pixel! 🎉"
```

**Make it executable and run:**

```bash
chmod +x /Volumes/Ai/transfer-to-termux.sh
/Volumes/Ai/transfer-to-termux.sh
```

---

## 🎯 Quick Command Summary

### On Mac (Before Transfer)

```bash
# Create transfer script
nano /Volumes/Ai/transfer-to-termux.sh
# (Paste the script above)

chmod +x /Volumes/Ai/transfer-to-termux.sh
```

### On Pixel (Termux Setup)

```bash
# Initial setup
pkg update && pkg upgrade -y
pkg install -y git curl wget openssh nodejs python rsync
npm install -g @anthropic-ai/claude-code
mkdir -p ~/Ai/{.Master,Projects,Desktop}

# Start SSH server
passwd
sshd

# Get IP
ip addr show wlan0 | grep inet
```

### On Mac (Transfer)

```bash
# Run transfer script
/Volumes/Ai/transfer-to-termux.sh
```

### On Pixel (After Transfer)

```bash
# Verify
source ~/.bashrc
cd ~/Ai
ls -la

# Test Claude Code
claude --version
cd ~/Ai/Projects/ai-courses
claude
```

---

## 🆘 Troubleshooting

### "Connection refused" when SSH

```bash
# On Termux
# Make sure SSH is running
sshd

# Check if running
pgrep sshd

# Restart if needed
pkill sshd
sshd
```

### "Permission denied"

```bash
# On Termux
# Make sure you set a password
passwd

# Check SSH config
cat ~/.ssh/sshd_config
```

### "Command not found: claude"

```bash
# On Termux
# Reinstall
npm install -g @anthropic-ai/claude-code

# Or check PATH
echo $PATH
which claude
```

### Scripts don't work

```bash
# On Termux
# Make scripts executable
chmod +x ~/Ai/.Master/scripts/*.sh

# Update paths
cd ~/Ai/.Master/scripts
sed -i 's|/Volumes/Ai|~/Ai|g' *.sh
```

---

## 📱 Termux Tips

### Storage Access

```bash
# Grant Termux storage access
termux-setup-storage

# Now you can access:
~/storage/shared  # Internal storage
~/storage/dcim    # Camera
~/storage/downloads  # Downloads folder
```

### Keep Termux Running

```bash
# Install Termux:Boot (from F-Droid)
# Enable "Autostart on boot"

# Or use wake lock
termux-wake-lock
```

### Sync with Mac (ongoing)

```bash
# On Mac, create sync script
rsync -avz --delete -e "ssh -p 8022" \
    /Volumes/Ai/Projects/ \
    u0_a123@192.168.1.XXX:~/Ai/Projects/
```

---

## ✅ Final Checklist

After setup, you should have:

```
On Termux:
□ Node.js installed
□ Git installed
□ Claude Code installed
□ ~/Ai/.Master/ folder (with all scripts)
□ ~/Ai/Projects/ folder (with all 9 projects)
□ Scripts updated for Termux paths
□ Aliases configured in ~/.bashrc
□ SSH server running (for future transfers)
□ Claude Code working
```

---

**Ready to run Claude Code on your Google Pixel! 📱🤖**

_Last Updated: January 20, 2025_
