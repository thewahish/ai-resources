# 📁 Folder Organization Plan for /Volumes/Ai

**Goal:** Move project folders to /Volumes/Ai/Projects/ for better organization

---

## ⚠️ CRITICAL: DO NOT MOVE

These folders MUST stay at `/Volumes/Ai/`:

### 1. `.Master/` 🔴 CRITICAL
**Path:** `/Volumes/Ai/.Master/`
**Reason:**
- Contains master prompt system for all projects
- ALL scripts reference this exact path: `/Volumes/Ai/.Master/`
- Moving it will break:
  - init-project.sh
  - setup-existing.sh
  - All Claude instructions loading

**Action:** ✅ KEEP AT ROOT

### 2. System Folders (macOS)
**Folders:**
- `.DocumentRevisions-V100/`
- `.fseventsd/`
- `.Spotlight-V100/`
- `.TemporaryItems/`
- `.Trashes/`
- `.claude/`

**Reason:** macOS system folders, moving will cause issues
**Action:** ✅ KEEP AT ROOT

### 3. `Desktop/`
**Path:** `/Volumes/Ai/Desktop/`
**Reason:**
- Likely your main working desktop folder
- Has 461 files - probably active workspace
- Moving could disrupt your workflow

**Action:** ✅ KEEP AT ROOT (unless you want to reorganize)

---

## ✅ SAFE TO MOVE (Projects)

These look like project folders and should be moved to `/Volumes/Ai/Projects/`:

### Active Projects
```
✓ arabian-sweets-empire/    → /Volumes/Ai/Projects/arabian-sweets-empire/
✓ Entertainment-Hub/        → /Volumes/Ai/Projects/Entertainment-Hub/
✓ Karazah/                  → /Volumes/Ai/Projects/Karazah/
✓ p-o-h/                    → /Volumes/Ai/Projects/p-o-h/
✓ syrian-memory-game/       → /Volumes/Ai/Projects/syrian-memory-game/
✓ Tarboush/                 → /Volumes/Ai/Projects/Tarboush/
✓ website/                  → /Volumes/Ai/Projects/website/
✓ website2.0/               → /Volumes/Ai/Projects/website2.0/
```

### Special Folders (Optional Move)
```
? Events/                   → /Volumes/Ai/Projects/Events/ (or keep at root)
? job-applications/         → /Volumes/Ai/Documents/job-applications/ (create Documents folder?)
? resumes/                  → /Volumes/Ai/Documents/resumes/
```

---

## 📄 Files

**File:** `من جيل .mov` (1GB video file)
**Recommendation:**
- Move to `/Volumes/Ai/Media/` (create new folder)
- Or keep at root if frequently accessed
- Or move to specific project folder if it belongs to one

---

## 📊 Recommended Final Structure

```
/Volumes/Ai/
├── .Master/                    ← KEEP (critical system folder)
├── .claude/                    ← KEEP (system)
├── Desktop/                    ← KEEP (active workspace)
│
├── Projects/                   ← All project folders here
│   ├── ai-courses/            (already here)
│   ├── arabian-sweets-empire/
│   ├── Entertainment-Hub/
│   ├── Events/                (optional)
│   ├── Karazah/
│   ├── p-o-h/
│   ├── syrian-memory-game/
│   ├── Tarboush/
│   ├── website/
│   └── website2.0/
│
├── Documents/                  ← NEW: Personal documents
│   ├── job-applications/
│   └── resumes/
│
├── Media/                      ← NEW: Video/audio files
│   └── من جيل .mov
│
└── [System folders]            ← KEEP (macOS managed)
    ├── .DocumentRevisions-V100/
    ├── .fseventsd/
    ├── .Spotlight-V100/
    ├── .TemporaryItems/
    └── .Trashes/
```

---

## 🚀 Automated Move Script

I can create a script to safely move everything. Here's what it will do:

```bash
#!/bin/bash
# Move project folders to /Volumes/Ai/Projects/

# Safety checks
- Verify source folders exist
- Check destination has enough space
- Create backups before moving
- Update git remotes if needed

# Move operations
- Move each project folder
- Preserve permissions and timestamps
- Create symlinks at old locations (optional)
- Log all operations

# Verification
- Verify all files copied
- Check git repositories still work
- Test that nothing broke
```

**Would you like me to:**
1. ✅ **Create the automated move script** (recommended)
2. ✅ **Move folders manually with guidance**
3. ✅ **Just create the new structure and you move yourself**

---

## ⚠️ Before Moving - Checklist

```
□ Close all apps that might have files open in these folders
□ Backup important data (just in case)
□ Check if any projects have absolute paths that need updating
□ Verify you have write permissions to /Volumes/Ai/
□ Ensure enough disk space for operation
```

---

## 🔧 Post-Move Tasks

After moving, you may need to:

```
□ Update git repository paths (if any use absolute paths)
□ Update any scripts that reference old locations
□ Update IDE/editor project paths
□ Clear .DS_Store files: find /Volumes/Ai -name ".DS_Store" -delete
□ Verify all projects still open correctly
```

---

## 📝 Summary

**Safe to move:** 8 project folders
**Must keep at root:** .Master/, Desktop/, system folders
**Optional:** Create Documents/ and Media/ folders
**Risk level:** Low (with proper script)

**Recommended approach:**
1. I create an automated, safe move script
2. Script moves folders and logs everything
3. Creates symlinks at old locations (backwards compatibility)
4. You verify everything works
5. Remove symlinks once confirmed

**Ready to proceed?**
