# Repository Security & Permissions

**Date:** 2025-10-20  
**Version:** v1.3.1  
**Purpose:** Clarify repository access rights and contribution workflow

---

## ⚠️ IMPORTANT: Who Can Push to This Repository?

### ✅ Authorized to Push Directly to `main` Branch:

**Only Repository Owners/Maintainers:**
1. **Carmen Wrede** (Owner)
2. **Lino Casu** (Owner)

**That's it. Nobody else.**

---

## 🔒 Repository Access Levels

### GitHub Repository Settings

**Repository:** `error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results`

**Access Levels:**

| Role | Who | Can Push? | Can Merge PRs? | Can Delete? |
|------|-----|-----------|----------------|-------------|
| **Owner** | Carmen Wrede, Lino Casu | ✅ YES | ✅ YES | ✅ YES* |
| **Collaborator** | None currently | ❌ NO | ❌ NO | ❌ NO |
| **Public** | Anyone | ❌ NO | ❌ NO | ❌ NO |

*Even owners rarely delete - destructive operations avoided

**Branch Protection (main branch):**
- ✅ Protected against deletion
- ✅ Protected against force push
- ✅ Requires pull request reviews
- ✅ Requires status checks to pass
- ✅ Direct push: Only owners
- ✅ Delete protection: Enabled
- ✅ History protected: No rewriting
- ✅ Administrators NOT exempt (protection applies to everyone)

---

## 👥 How External Contributors Work

### For Everyone Else (Not Owners):

**You CANNOT push directly to this repository.**

**Correct Workflow:**

1. **Fork the Repository**
   ```bash
   # On GitHub: Click "Fork" button
   # This creates YOUR copy: your-username/Segmented-Spacetime-Mass-Projection-Unified-Results
   ```

2. **Clone YOUR Fork**
   ```bash
   git clone https://github.com/YOUR-USERNAME/Segmented-Spacetime-Mass-Projection-Unified-Results
   cd Segmented-Spacetime-Mass-Projection-Unified-Results
   ```

3. **Make Changes in Your Fork**
   ```bash
   git checkout -b feature/your-feature-name
   # Make your changes
   git add .
   git commit -m "Your changes"
   git push origin feature/your-feature-name  # This pushes to YOUR fork only!
   ```

4. **Create Pull Request**
   - Go to GitHub
   - Navigate to your fork
   - Click "Pull Request"
   - Request merge into `error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results:main`
   - Wait for owner review

5. **Owners Review & Merge**
   - Carmen/Lino review your PR
   - If approved: They merge into main
   - If changes needed: You update your fork
   - **You never push to main directly**

---

## 📚 Documentation Commands Explained

### Why Git Push Commands Are in Documentation

**You may see commands like:**
```bash
git push origin main
```

**These are for:**
- ✅ Repository owners (Carmen, Lino)
- ✅ Documentation of maintainer workflow
- ✅ CI/CD pipeline reference

**These are NOT for:**
- ❌ External contributors
- ❌ General public
- ❌ Anyone without explicit permission

**If you try to push without permission:**
```
remote: Permission to error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results.git denied.
fatal: unable to access 'https://github.com/error-wtf/...': The requested URL returned error: 403
```

**You will get HTTP 403 Forbidden error.**

---

## 🔐 Security Measures

### Repository Security

1. **Branch Protection (main) - MAXIMUM SECURITY**
   - ✅ Enabled and enforced
   - ✅ **Delete protection: ENABLED** (cannot delete main branch)
   - ✅ **Force push: BLOCKED** (cannot rewrite history)
   - ✅ Requires pull request reviews before merge
   - ✅ Requires status checks to pass (CI/CD)
   - ✅ Requires linear history (no merge commits without review)
   - ✅ Requires signed commits (optional but recommended)
   - ✅ Restrictions apply to administrators (even owners protected)
   - ✅ Cannot delete branches without explicit permission
   - ✅ Cannot bypass via any method (web UI, CLI, API)

2. **Deletion Protection - CRITICAL**
   - ✅ Main branch: **CANNOT be deleted** (protected)
   - ✅ Tags: Protected from deletion
   - ✅ Releases: Permanent once published
   - ✅ Commits: Cannot be removed (history immutable)
   - ✅ Files: Deletion requires commit + review (traceable)
   - ⚠️ **Any deletion attempt will fail with 403 error**

3. **Write Access - RESTRICTED**
   - ✅ Restricted to 2 owners only (Carmen, Lino)
   - ✅ No public write access
   - ✅ No collaborators with write access
   - ✅ Fork-based contribution model (external)
   - ✅ All changes via Pull Request (reviewed)

4. **Credentials & Secrets**
   - ✅ No credentials in repository
   - ✅ API keys in .env (not tracked, .gitignore)
   - ✅ Secrets in GitHub Secrets (for Actions)
   - ✅ Environment variables encrypted
   - ✅ No hardcoded passwords or tokens

5. **Automated Security Checks**
   - ✅ GitHub Actions run on all PRs
   - ✅ Tests must pass before merge (71 tests)
   - ✅ Code scanning enabled (vulnerabilities)
   - ✅ Dependency scanning (known CVEs)
   - ✅ Secret scanning (leaked credentials)
   - ✅ No malicious code patterns detected

6. **Audit Trail**
   - ✅ All changes logged in Git history
   - ✅ Commit author tracked
   - ✅ Pull Request reviews recorded
   - ✅ Merge history preserved
   - ✅ **Deletions traceable** (if any occur)

---

## 📖 Correct Documentation Interpretation

### Documents with Push Commands

These documents are **for maintainers only:**

1. **REPO_UPDATE_CHECKLIST.md** - Maintainer release workflow
2. **GIT_SYNC_README.md** - Owner sync procedures
3. **GIT_UPLOAD_STATUS_REPORT.md** - Owner upload documentation
4. **Archive documents** - Historical maintainer notes

### Documents for Contributors

These documents are **for everyone:**

1. **CONTRIBUTING.md** - Public contribution guide
   - ✅ Explains fork workflow
   - ✅ Shows how to create PRs
   - ✅ Does NOT give push access

2. **README.md** - Public documentation
   - ✅ Installation instructions
   - ✅ Usage examples
   - ✅ No push required

3. **COMPREHENSIVE_TESTING_GUIDE.md** - Testing guide
   - ✅ How to test locally
   - ✅ No repository access needed

---

## ✅ What You CAN Do (Public)

**Without Any Permissions:**

1. ✅ **Clone the Repository**
   ```bash
   git clone https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results
   ```

2. ✅ **Read All Documentation**
   - All 312+ documents are public
   - Browse on GitHub
   - Download and read locally

3. ✅ **Run Tests Locally**
   ```bash
   python run_full_suite.py
   ```

4. ✅ **Use the Code**
   - Licensed under ANTI-CAPITALIST SOFTWARE LICENSE v1.4
   - Read LICENSE file for terms
   - Use for non-commercial purposes

5. ✅ **Fork and Modify**
   - Create your own copy
   - Make any changes in your fork
   - Publish your fork (following license)

6. ✅ **Submit Issues**
   - Report bugs on GitHub Issues
   - Suggest features
   - Ask questions

7. ✅ **Create Pull Requests**
   - Fork → Change → PR
   - Owners review and merge if appropriate

---

## ❌ What You CANNOT Do (Without Permission)

**Forbidden Actions:**

1. ❌ **Push Directly to Main Branch**
   - Will fail with 403 error
   - Only owners can push
   - Branch protection blocks unauthorized access

2. ❌ **Delete ANY Branches**
   - ⚠️ **STRICTLY FORBIDDEN** for everyone except owners
   - Main branch: Protected against deletion (even owners blocked)
   - Feature branches: Only creator can delete their own fork branches
   - Attempting to delete: 403 Forbidden error
   - **This is the most critical protection**

3. ❌ **Delete ANY Files or Commits**
   - Cannot delete files from repository
   - Cannot delete commits (history rewriting blocked)
   - Cannot force push to rewrite history
   - All destructive operations blocked

4. ❌ **Merge Pull Requests**
   - Only owners can merge
   - You can only create PRs
   - Cannot approve your own PRs

5. ❌ **Modify Repository Settings**
   - Only owners have access
   - No public admin rights
   - Cannot change branch protection

6. ❌ **Access GitHub Secrets**
   - CI/CD secrets owner-only
   - API keys protected
   - Environment variables hidden

7. ❌ **Force Push**
   - ⚠️ Even owners avoid this (dangerous!)
   - History is protected
   - Branch protection blocks force push

8. ❌ **Rewrite History**
   - Cannot rebase published branches
   - Cannot amend published commits
   - Git history is immutable once published

---

## 🚨 If You See Suspicious Activity

### Report Security Issues

**If you discover:**
- Security vulnerabilities
- Unauthorized access
- Suspicious commits
- Malicious code

**Contact:**
- Email: mail@error.wtf
- GitHub Issues: Tag as "security"
- Do NOT publish exploit details publicly

---

## 📞 Requesting Collaborator Access

### Want to Become a Collaborator?

**Requirements:**
1. Demonstrate expertise in the field
2. Multiple accepted pull requests
3. Active engagement with the project
4. Trust established with owners

**Process:**
1. Contribute via forks and PRs for several months
2. Show consistent high-quality contributions
3. Email request to mail@error.wtf
4. Owners evaluate and decide

**Current Policy:**
- **Very selective**
- **Trust-based**
- **Long-term contributors only**

---

## 📜 License & Usage Rights

### ANTI-CAPITALIST SOFTWARE LICENSE v1.4

**You CAN:**
- ✅ Use for personal projects
- ✅ Use for research
- ✅ Use for education
- ✅ Fork and modify (following license)
- ✅ Contribute back via PRs

**You CANNOT:**
- ❌ Use for commercial exploitation
- ❌ Use for military purposes
- ❌ Remove license/attribution
- ❌ Push without permission (technical limitation)

**Read:** LICENSE file for complete terms

---

## 🔄 Contribution Workflow Summary

### Standard Workflow for External Contributors

```
1. YOU: Fork repository (creates YOUR copy)
2. YOU: Clone YOUR fork to local machine
3. YOU: Make changes in YOUR fork
4. YOU: Push to YOUR fork (you own it, allowed)
5. YOU: Create Pull Request to main repository
6. OWNERS: Review your PR
7. OWNERS: Merge if approved (or request changes)
8. YOU: Sync your fork with updated main
```

**At NO point do you push to main repository.**

**You always work in your fork.**

---

## 📊 Access Statistics

**Repository Access (Public):**
- Reads: Unlimited (public repository)
- Clones: Unlimited (anyone can clone)
- Forks: Unlimited (anyone can fork)
- Writes: 2 people only (Carmen, Lino)

**Current Collaborators with Write Access:**
- Total: 2 (owners only)
- External Collaborators: 0
- Public Contributors: Via PRs only

---

## ✅ Summary

**IMPORTANT TO UNDERSTAND:**

1. ✅ This is a **public repository** (anyone can read/clone/fork)
2. ✅ Only **2 people** can push directly (Carmen, Lino)
3. ✅ Everyone else contributes via **Fork + Pull Request**
4. ✅ `git push` commands in docs are **for owners only**
5. ✅ You **will get 403 error** if you try to push without permission
6. ✅ This is **normal and correct** - it's how GitHub security works
7. ✅ Follow **CONTRIBUTING.md** for how to contribute
8. ⚠️ **DELETION IS STRICTLY PROHIBITED** - Main branch protected, history immutable
9. ⚠️ **FORCE PUSH IS BLOCKED** - Cannot rewrite published history
10. ✅ All security enforced by **GitHub, not just documentation**

**Nobody can push "ungefragt" (without permission) - GitHub prevents it automatically.**

**⚠️ CRITICAL: Nobody can delete branches, files, or commits "ungefragt" - Branch protection and GitHub permissions block ALL destructive operations automatically.**

---

## 🛡️ DELETION PROTECTION - MOST IMPORTANT

### Why Deletion is Strictly Forbidden

**The main concern: Preventing unauthorized deletion of code, branches, or history.**

### What is Protected:

1. **Main Branch - CANNOT be deleted**
   - Protected by GitHub branch protection rules
   - Even repository owners cannot delete it accidentally
   - Requires explicit disabling of protection (logged action)
   - Any deletion attempt: 403 Forbidden

2. **All Commits - PERMANENT**
   - Once pushed, commits are immutable
   - Cannot be deleted without force push
   - Force push is BLOCKED on main branch
   - Git history is permanent record

3. **All Files - TRACEABLE**
   - File deletion requires commit
   - Commit must pass review (for main)
   - Deletion is visible in history
   - Can be reverted at any time

4. **Tags & Releases - PROTECTED**
   - Release tags cannot be deleted
   - Published releases permanent
   - Version history preserved

### How Protection Works:

```
User attempts: git push --delete origin main
GitHub responds: ERROR 403 Forbidden

User attempts: git push --force origin main
GitHub responds: ERROR 403 Forbidden (Branch protection)

User attempts: Delete branch via Web UI
GitHub responds: Protected branch cannot be deleted

User attempts: Delete file without commit
GitHub responds: Must commit changes (traceable)
```

### Multiple Layers of Protection:

1. **GitHub Permissions** - Only 2 people have write access
2. **Branch Protection** - Main branch locked against deletion
3. **Force Push Block** - Cannot rewrite history
4. **Audit Trail** - All actions logged
5. **Review Required** - Changes must be reviewed
6. **CI/CD Checks** - Tests must pass

### Summary:

**🔒 DELETION IS IMPOSSIBLE FOR UNAUTHORIZED USERS**
- No write access = No deletion ability
- Branch protection = Main cannot be deleted
- Force push blocked = History cannot be rewritten
- All changes tracked = Deletions are visible

**Even if someone had write access (they don't), they still couldn't delete the main branch due to branch protection.**

**Even owners rarely delete anything - destructive operations are avoided as policy.**

---

**Last Updated:** 2025-10-20  
**Next Review:** Before v1.4.0 release

© 2025 Carmen Wrede, Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
