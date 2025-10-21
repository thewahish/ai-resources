# 🤖 Master Prompt for Claude GUI (Copy This to claude.ai on Your Phone)

**Copy everything below the line and paste it into Claude's web interface on your phone:**

---

I need your help setting up my complete AI development environment on my Google Pixel phone using Termux. I have already pushed all my code to GitHub from my Mac, and now I need to clone everything to my phone and set up Claude Code.

## My Setup Details:

**GitHub Username:** thewahish

**Repositories to Clone (13 total):**

1. **Master AI System:**
   - Repo: `master-ai-system`
   - Clone to: `~/Ai/.Master`
   - Contains: 11-agent AI prompt system, scripts, templates

2. **Projects (12 total):**
   - `ai-courses`
   - `arabian-sweets-empire`
   - `Entertainment-Hub`
   - `job-applications`
   - `Karazah`
   - `MSU-Oct2025`
   - `p-o-h`
   - `resumes`
   - `syrian-memory-game`
   - `Tarboush`
   - `website`
   - `website2.0`
   - All clone to: `~/Ai/Projects/[project-name]`

**Final Directory Structure I Need:**
```
~/Ai/
├── .Master/              ← Master AI prompt system
└── Projects/             ← All 12 projects
    ├── ai-courses/
    ├── arabian-sweets-empire/
    ├── Entertainment-Hub/
    ├── job-applications/
    ├── Karazah/
    ├── MSU-Oct2025/
    ├── p-o-h/
    ├── resumes/
    ├── syrian-memory-game/
    ├── Tarboush/
    ├── website/
    └── website2.0/
```

## What I Need You To Do:

**Guide me step-by-step through:**

1. **Installing Termux** (if not installed)
   - From F-Droid: https://f-droid.org/

2. **Installing required packages:**
   - git
   - nodejs
   - python
   - Claude Code CLI (`@anthropic-ai/claude-code`)

3. **Configuring Git**
   - Set up my name and email
   - Help me create a GitHub Personal Access Token for authentication

4. **Creating the directory structure**
   - `~/Ai/Projects/`

5. **Cloning all repositories**
   - Clone `.Master` from `https://github.com/thewahish/master-ai-system.git` to `~/Ai/.Master`
   - Clone all 12 projects from GitHub to `~/Ai/Projects/`

6. **Verifying everything works**
   - Check all folders exist
   - Test git status
   - Test Claude Code CLI

## Important Notes:

- I'm on a **Google Pixel phone** using **Termux**
- I'm using a **touchscreen** keyboard, so make commands easy to copy-paste
- Give me **one command at a time** and wait for me to confirm before moving to the next step
- If something fails, help me troubleshoot immediately
- All my repos are **public** on GitHub under username `thewahish`
- I may need to create a **GitHub Personal Access Token** at: https://github.com/settings/tokens

## Your Approach:

1. **Check what I already have** - Ask me to run commands to see what's already installed
2. **Install missing components** - Give me the exact commands to run
3. **Guide me step by step** - One command at a time, verify each works before continuing
4. **Handle errors gracefully** - If something fails, help me fix it
5. **Verify at the end** - Make sure everything is working correctly

## Commands You'll Likely Give Me:

**Package installation:**
```bash
pkg update && pkg upgrade -y
pkg install git nodejs python -y
npm install -g @anthropic-ai/claude-code
```

**Git configuration:**
```bash
git config --global user.name "Obai Sukar"
git config --global user.email "obai@example.com"
```

**Directory creation:**
```bash
mkdir -p ~/Ai/Projects
```

**Clone .Master:**
```bash
cd ~/Ai
git clone https://github.com/thewahish/master-ai-system.git .Master
```

**Clone projects:**
```bash
cd ~/Ai/Projects
git clone https://github.com/thewahish/ai-courses.git
git clone https://github.com/thewahish/arabian-sweets-empire.git
git clone https://github.com/thewahish/Entertainment-Hub.git
git clone https://github.com/thewahish/job-applications.git
git clone https://github.com/thewahish/Karazah.git
git clone https://github.com/thewahish/MSU-Oct2025.git
git clone https://github.com/thewahish/p-o-h.git
git clone https://github.com/thewahish/resumes.git
git clone https://github.com/thewahish/syrian-memory-game.git
git clone https://github.com/thewahish/Tarboush.git
git clone https://github.com/thewahish/website.git
git clone https://github.com/thewahish/website2.0.git
```

**Verification:**
```bash
ls -la ~/Ai/
ls -la ~/Ai/Projects/
cd ~/Ai/Projects/ai-courses && git status
claude --version
```

## Start Here:

Begin by asking me:
1. "Do you have Termux installed and open?"
2. "What does this command show: `which git`"
3. "What does this command show: `which node`"

Then guide me through the setup process step by step, making sure each step completes successfully before moving to the next one.

Be patient, friendly, and thorough. I'm setting this up so I can use Claude Code CLI on my phone to work on my projects anywhere!

Let's get started! 🚀
