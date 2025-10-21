# 📱 Complete Google Pixel Setup Instructions

**Step-by-step guide to set up your entire AI development environment on your phone**

---

## 🎯 What You'll Have When Done

```
~/Ai/
├── .Master/              ← Master AI prompt system (11 agents)
└── Projects/             ← All 12 projects
    ├── ai-courses
    ├── arabian-sweets-empire
    ├── Entertainment-Hub
    ├── job-applications
    ├── Karazah
    ├── MSU-Oct2025
    ├── p-o-h
    ├── resumes
    ├── syrian-memory-game
    ├── Tarboush
    ├── website
    └── website2.0
```

---

## 📲 STEP 1: Install Termux

1. **Open your phone's browser**

2. **Go to:** https://f-droid.org/

3. **Download F-Droid app** (app store for open source apps)

4. **Install F-Droid** (you may need to allow installing from unknown sources)

5. **Open F-Droid**

6. **Search for "Termux"**

7. **Install Termux** (the terminal emulator app)

8. **Open Termux** - you should see a black terminal screen with `$` prompt

---

## ⚙️ STEP 2: Update Termux & Install Essential Tools

**Copy and paste these commands one by one into Termux:**

### Update Package Manager
```bash
pkg update && pkg upgrade -y
```
*(Press `y` if asked to confirm)*

### Install Git
```bash
pkg install git -y
```

### Install Node.js (for Claude Code)
```bash
pkg install nodejs -y
```

### Install Python (useful for projects)
```bash
pkg install python -y
```

### Verify Installations
```bash
git --version
node --version
npm --version
python --version
```

You should see version numbers for each.

---

## 🤖 STEP 3: Install Claude Code

```bash
npm install -g @anthropic-ai/claude-code
```

**Verify installation:**
```bash
claude --version
```

---

## 🔧 STEP 4: Configure Git

**Replace with YOUR name and email:**

```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```

**Example:**
```bash
git config --global user.name "Obai Sukar"
git config --global user.email "obai@example.com"
```

---

## 📂 STEP 5: Create Ai Folder Structure

**Create the main Ai directory and subfolders:**

```bash
mkdir -p ~/Ai/Projects
```

**Verify it was created:**
```bash
ls -la ~/
```

You should see `Ai` in the list.

---

## 🔑 STEP 6: Setup GitHub Authentication

You'll need to authenticate with GitHub to clone your repos.

### Option A: Personal Access Token (Recommended)

1. **On your phone's browser, go to:** https://github.com/settings/tokens

2. **Click** "Generate new token" → "Generate new token (classic)"

3. **Fill in:**
   - Note: `Termux Access`
   - Expiration: `No expiration` (or your preference)
   - Select scopes: Check `repo` (full control of private repositories)

4. **Click** "Generate token"

5. **Copy the token** (it looks like `ghp_xxxxxxxxxxxx`)

6. **IMPORTANT:** Save this token somewhere safe - you'll use it as your password when cloning

### Option B: SSH Key (Advanced)

```bash
ssh-keygen -t ed25519 -C "your-email@example.com"
```
Press Enter 3 times (default location, no passphrase)

```bash
cat ~/.ssh/id_ed25519.pub
```
Copy the output and add it to GitHub: https://github.com/settings/keys

---

## 📥 STEP 7: Clone .Master System

**Navigate to Ai folder:**
```bash
cd ~/Ai
```

**Clone the Master AI system:**
```bash
git clone https://github.com/thewahish/master-ai-system.git .Master
```

**Enter your GitHub credentials when prompted:**
- Username: `thewahish`
- Password: `[Your Personal Access Token from Step 6]`

**Verify it worked:**
```bash
ls -la ~/Ai/
```

You should see `.Master/` folder.

---

## 📦 STEP 8: Clone All 12 Projects

**Navigate to Projects folder:**
```bash
cd ~/Ai/Projects
```

**Clone each project (paste these commands one by one):**

```bash
git clone https://github.com/thewahish/ai-courses.git
```

```bash
git clone https://github.com/thewahish/arabian-sweets-empire.git
```

```bash
git clone https://github.com/thewahish/Entertainment-Hub.git
```

```bash
git clone https://github.com/thewahish/job-applications.git
```

```bash
git clone https://github.com/thewahish/Karazah.git
```

```bash
git clone https://github.com/thewahish/MSU-Oct2025.git
```

```bash
git clone https://github.com/thewahish/p-o-h.git
```

```bash
git clone https://github.com/thewahish/resumes.git
```

```bash
git clone https://github.com/thewahish/syrian-memory-game.git
```

```bash
git clone https://github.com/thewahish/Tarboush.git
```

```bash
git clone https://github.com/thewahish/website.git
```

```bash
git clone https://github.com/thewahish/website2.0.git
```

**Note:** You may need to enter your GitHub credentials for each one, OR they may remember it after the first time.

---

## ✅ STEP 9: Verify Everything

**Check Projects folder:**
```bash
cd ~/Ai/Projects
ls -la
```

You should see all 12 project folders:
- ai-courses
- arabian-sweets-empire
- Entertainment-Hub
- job-applications
- Karazah
- MSU-Oct2025
- p-o-h
- resumes
- syrian-memory-game
- Tarboush
- website
- website2.0

**Check .Master folder:**
```bash
cd ~/Ai/.Master
ls -la
```

You should see:
- CLAUDE_INSTRUCTIONS.md
- scripts/
- templates/
- README.md
- etc.

**Test Git in a project:**
```bash
cd ~/Ai/Projects/ai-courses
git status
```

Should show "On branch main" and "up to date"

---

## 🚀 STEP 10: Test Claude Code

**Navigate to a project:**
```bash
cd ~/Ai/Projects/ai-courses
```

**Start Claude:**
```bash
claude
```

**You should see Claude's welcome screen!**

**Test it by typing:**
```
List all files in this project
```

Claude should show you the project files.

**Exit Claude:**
Type `exit` or press `Ctrl+D`

---

## 🎉 STEP 11: You're Done!

Your phone now has:
- ✅ Termux terminal
- ✅ Git version control
- ✅ Node.js & npm
- ✅ Claude Code AI assistant
- ✅ Master AI prompt system (.Master)
- ✅ All 12 projects
- ✅ Full sync with GitHub

---

## 🔄 Daily Usage

### To work on a project:

```bash
cd ~/Ai/Projects/website
claude
```

Then ask Claude to help you code!

### To sync changes FROM your Mac:

```bash
cd ~/Ai/Projects/website
git pull
```

This pulls the latest changes from GitHub.

### To push changes TO GitHub (from phone):

After making changes with Claude:

```bash
git add .
git commit -m "Description of changes"
git push
```

Or ask Claude to do it:
```
Commit my changes and push to GitHub
```

### To sync changes TO your Mac:

On your Mac:
```bash
cd /Volumes/Ai/Projects/website
git pull
```

---

## 🆘 Troubleshooting

### Can't see .Master folder?
```bash
ls -la ~/Ai/
```
Hidden folders start with `.` and need `-a` flag to show.

### Clone failed - "Repository not found"?
- Check your GitHub username is correct: `thewahish`
- Make sure you created the repository on GitHub
- Check your internet connection

### Authentication failed?
- Use your Personal Access Token, not your GitHub password
- Token should start with `ghp_`
- Generate new token: https://github.com/settings/tokens

### Permission denied?
Make scripts executable:
```bash
chmod +x ~/Ai/.Master/scripts/*.sh
```

### Claude command not found?
Reinstall:
```bash
npm install -g @anthropic-ai/claude-code
```

### Out of storage?
Check space:
```bash
df -h ~
```

---

## 📝 Pro Tips

### Save your GitHub token
Create a file to store it:
```bash
echo "GitHub Token: ghp_your_token_here" > ~/github-token.txt
```

### Create shortcuts
Add to `~/.bashrc`:
```bash
echo "alias ai='cd ~/Ai/Projects'" >> ~/.bashrc
source ~/.bashrc
```

Now you can just type `ai` to go to Projects folder!

### Multiple projects at once
Open multiple Termux sessions:
- Swipe from left edge → "New session"
- Switch between them with swipe

---

## 📱 Phone-Specific Tips

### Keyboard shortcuts in Termux:
- **Volume Down + C** = Ctrl+C (cancel)
- **Volume Down + D** = Ctrl+D (exit)
- **Volume Down + L** = Clear screen
- **Swipe from left** = Show extra keys

### Install Termux:API (optional):
Gives access to phone features (camera, GPS, etc.)
```bash
pkg install termux-api
```

### Keep Termux running:
Enable "Acquire wakelock" in Termux notification

---

## 🎯 Next Steps

1. **Try editing a project** - Use Claude to make changes
2. **Test the sync** - Make changes on phone, push, pull on Mac
3. **Explore .Master** - Check out the 11-agent system
4. **Build something** - Start coding on your phone!

---

**You now have a full development environment in your pocket! 🚀**

Your Mac and phone are fully synced via GitHub. Work on either device, and keep them in sync with `git pull` and `git push`.

---

*Last Updated: October 20, 2025*
*GitHub User: thewahish*
*All 13 repos synced (.Master + 12 projects) ✅*
