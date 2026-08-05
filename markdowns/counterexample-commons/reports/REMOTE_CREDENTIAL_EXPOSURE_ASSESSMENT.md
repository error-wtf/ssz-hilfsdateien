# Remote Credential Exposure Assessment

**Date:** 2026-05-25
**Written by:** Cascade (LOCAL ONLY — NO COMMIT, NO PUSH)

---

## 1. Finding

A credential-bearing remote URL was detected during this session in a terminal output
showing `git remote -v`. The URL followed the pattern:

```
https://<ghp_TOKEN>@github.com/error-wtf/counterexample-commons.git
```

This token was not displayed or reproduced further after detection.

---

## 2. Scope of Exposure

| Location | Token Present |
|----------|---------------|
| Local `.git/config` remote.origin.url | YES |
| Tracked repository files | NO |
| Untracked local files (reports, notebooks, etc.) | NO |
| Any committed content (all commits scanned) | NO |
| `.venv` or build artefacts | NOT SCANNED (excluded as irrelevant) |

The token exists **only** in the local `.git/config`. It was not committed to any branch,
does not appear in any file inside the working tree, and is not present in any commit blob
reachable from the repository history.

---

## 3. How the Token Appeared in Terminal Output

The `git remote -v` command, run with `SafeToAutoRun: true` during the repository workspace
identification step, printed the full remote URL including the embedded token to the terminal.
This output was visible in this chat session.

Terminal/chat output is not a committed artefact and is not pushed to GitHub. However, it
constitutes an exposure in the sense that the token appeared in a conversation log.

---

## 4. Risk Assessment

| Risk | Level | Notes |
|------|-------|-------|
| Token in public GitHub repository content | NONE | Confirmed not present |
| Token in local working tree files | NONE | Confirmed not present |
| Token in terminal/chat output | PRESENT | Appeared once in `git remote -v` output |
| Token in local `.git/config` | PRESENT | Standard location for credential-bearing remotes |

Credential-bearing remote URLs in `.git/config` are a common pattern when Git credentials
are stored via HTTPS with token authentication. They are local only and not pushed.

---

## 5. Recommendations

1. **Rotate or revoke the token at GitHub** — go to:
   `https://github.com/settings/tokens`
   Revoke the affected `ghp_*` token and generate a new one if needed.

2. **Replace the remote URL with a token-free form** after rotation:
   ```
   git remote set-url origin https://github.com/error-wtf/counterexample-commons.git
   ```
   Then use Git credential manager or SSH for authentication going forward.

3. **No sanitisation of repository content is required** — the token did not enter
   any tracked file, commit, or pushed artefact.

4. **No further push is authorised** until the token is rotated and the remote URL
   is cleaned.

---

## 6. What Must Not Happen

- Do NOT run `git remote -v` again until the URL is sanitised.
- Do NOT display the `.git/config` contents in any output.
- Do NOT commit or push this report.

---

**NO COMMIT. NO PUSH. Local report only.**