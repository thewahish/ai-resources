# 📁 How to Organize Your /Volumes/Ai Folders

**Goal:** Move all project folders to `/Volumes/Ai/Projects/` for better organization

---

## 🚀 Quick Start (Recommended)

### Step 1: Test First (Dry Run)

**Always test first to see what will happen:**

```bash
/Volumes/Ai/.Master/scripts/organize-projects.sh --dry-run
```

**This will:**
- ✅ Show you exactly what will be moved
- ✅ Check for any issues
- ✅ NOT make any actual changes

### Step 2: Run for Real

**Once you're happy with the dry run:**

```bash
/Volumes/Ai/.Master/scripts/organize-projects.sh
```

**This will:**
1. Ask you to confirm
2. Ask about optional folders (Events, job-applications, resumes)
3. Move project folders to `/Volumes/Ai/Projects/`
4. Create symlinks at old locations (backwards compatibility)
5. Verify git repositories still work
6. Offer to create Documents/ and Media/ folders
7. Log everything

---

## 📋 What Gets Moved

### ✅ Will Move (8 projects)

```
arabian-sweets-empire/  → Projects/arabian-sweets-empire/
Entertainment-Hub/      → Projects/Entertainment-Hub/
Karazah/                → Projects/Karazah/
p-o-h/                  → Projects/p-o-h/
syrian-memory-game/     → Projects/syrian-memory-game/
Tarboush/               → Projects/Tarboush/
website/                → Projects/website/
website2.0/             → Projects/website2.0/
```

### 🔒 Will NOT Move (Protected)

```
.Master/                (critical - contains Claude system)
Desktop/                (your active workspace)
.claude/                (system folder)
[All .dot system folders]
```

### ? Will Ask You

```
Events/                 (project or keep at root?)
job-applications/       (move to Documents or Projects?)
resumes/                (move to Documents or Projects?)
```

---

## 🎯 Final Structure

After running the script:

```
/Volumes/Ai/
├── .Master/                  ← Stayed (critical)
├── Desktop/                  ← Stayed (workspace)
├── .claude/                  ← Stayed (system)
│
├── Projects/                 ← All projects here!
│   ├── ai-courses/
│   ├── arabian-sweets-empire/
│   ├── Entertainment-Hub/
│   ├── Karazah/
│   ├── p-o-h/
│   ├── syrian-memory-game/
│   ├── Tarboush/
│   ├── website/
│   └── website2.0/
│
├── Documents/                ← Optional (script will ask)
│   ├── job-applications/
│   └── resumes/
│
├── Media/                    ← Optional (script will ask)
│   └── من جيل .mov
│
└── [system folders]          ← Stayed (macOS)
```

---

## 🛡️ Safety Features

The script includes:

✅ **Dry-run mode** - Test before making changes
✅ **Safety checks** - Disk space, permissions, open files
✅ **Symlinks** - Old paths still work (backwards compatibility)
✅ **Git verification** - Ensures repositories still work
✅ **Complete logging** - Every action recorded
✅ **User confirmation** - You approve each step
✅ **Protected folders** - .Master/ cannot be moved

---

## 📖 Step-by-Step Example

```bash
# 1. Test first (no changes)
/Volumes/Ai/.Master/scripts/organize-projects.sh --dry-run

# Output shows:
# ✓ Will move: arabian-sweets-empire (125MB)
# ✓ Will move: Entertainment-Hub (45MB)
# ... etc
# 🔒 Protected: .Master (will NOT move)

# 2. Looks good? Run for real
/Volumes/Ai/.Master/scripts/organize-projects.sh

# 3. Script asks:
#    "Proceed with moving folders? (y/N):" → Type 'y'

# 4. Script asks about optional folders:
#    "Move Events to Projects/? (y/N):" → Choose as needed

# 5. Script moves everything and shows:
#    [1/8] → arabian-sweets-empire ✓
#    [2/8] → Entertainment-Hub ✓
#    ... etc

# 6. Script verifies Git repos:
#    Checking ai-courses... ✓
#    Checking website... ✓

# 7. Script asks:
#    "Create /Volumes/Ai/Documents/? (Y/n):" → Type 'y' if you want it

# 8. Done! Summary shows what happened.
```

---

## 🧹 After Moving - Cleanup (Optional)

Once you've verified everything works:

### Remove Symlinks

```bash
# Find all symlinks in /Volumes/Ai root
find /Volumes/Ai -maxdepth 1 -type l

# If they look correct, remove them:
find /Volumes/Ai -maxdepth 1 -type l -delete
```

### Clean .DS_Store Files

```bash
find /Volumes/Ai -name ".DS_Store" -delete
```

---

## 🆘 Troubleshooting

### "Permission denied"

```bash
# Fix permissions
sudo chmod +x /Volumes/Ai/.Master/scripts/organize-projects.sh

# Run with your user
/Volumes/Ai/.Master/scripts/organize-projects.sh
```

### "Some files are open"

- Close all apps (VS Code, browsers, etc.)
- Run the script again
- Or choose "Continue anyway" (less safe)

### "Folder already exists at destination"

- The folder was already moved
- Or there's a conflict
- Check: `ls -la /Volumes/Ai/Projects/`
- Manually resolve if needed

### "Git repository broken"

- Rare, but if it happens:
- The symlink should still work
- Or manually fix git remote:

```bash
cd /Volumes/Ai/Projects/your-project
git remote set-url origin <correct-url>
```

---

## 🔄 Want to Undo?

If you need to move folders back:

```bash
# Move a folder back
mv /Volumes/Ai/Projects/project-name /Volumes/Ai/

# Remove the symlink
rm /Volumes/Ai/project-name
```

---

## 📝 Log Files

Every run creates a detailed log:

```bash
# Location
/Volumes/Ai/.Master/logs/organize-projects-YYYYMMDD-HHMMSS.log

# View latest log
ls -lt /Volumes/Ai/.Master/logs/ | head -5

# Read log
cat /Volumes/Ai/.Master/logs/organize-projects-*.log
```

---

## ✅ Checklist

Before running:

```
□ Close all apps that might have files open
□ Run dry-run mode first
□ Review what will be moved
□ Have backups of important data (just in case)
□ Ensure you have time (5-10 minutes)
```

After running:

```
□ Verify projects open correctly
□ Check git repositories work
□ Test a few files to ensure they're accessible
□ Review log file for any errors
□ Remove symlinks once confirmed (optional)
```

---

## 🚀 Ready?

**Run the dry run first:**

```bash
/Volumes/Ai/.Master/scripts/organize-projects.sh --dry-run
```

**Then run for real:**

```bash
/Volumes/Ai/.Master/scripts/organize-projects.sh
```

**Questions?** Check the log file or open:

```bash
open /Volumes/Ai/FOLDER_ORGANIZATION_PLAN.md
```

---

**Good luck organizing! 🎉**
