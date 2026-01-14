# 🛠️ Runbook: Fix Linux Permission Issues

## 🎯 Purpose

Diagnose and fix file/folder permission problems when applications or users
cannot read or write files.

---

## ✅ Step 1 — Check Ownership

```bash
ls -l /path/to/file-or-folder
Example output:

text
Copy code
drwxr-xr-x  2 root root 4096 Jan 14 data
Means:

Owner: root

Group: root

✅ Step 2 — Change Owner
Give ownership to correct user:

bash
Copy code
sudo chown vivek:vivek /path/to/file
For folders:

bash
Copy code
sudo chown -R vivek:vivek /path/to/folder
✅ Step 3 — Check Permissions
bash
Copy code
ls -ld /path/to/folder
Example:

text
Copy code
drwxr-x--- 2 vivek dev 4096 Jan 14 appdata
Meaning:

Owner: full access

Group: read + execute

Others: no access

✅ Step 4 — Fix Permissions
Give owner full access:

bash
Copy code
chmod 700 /path/to/folder
Owner + group:

bash
Copy code
chmod 770 /path/to/folder
Temporary open (not for production):

bash
Copy code
chmod 777 /path/to/folder
✅ Step 5 — Fix Group Access
Add user to group:

bash
Copy code
sudo usermod -aG dev vivek
Apply group ownership:

bash
Copy code
sudo chown -R :dev /path/to/folder
❌ If App Still Fails
Check which user app runs as:

bash
Copy code
ps aux | grep appname
Then fix ownership for that user.

✅ Success Criteria
Application can read/write files

No permission denied errors in logs

yaml
Copy code

---

# ✅ After That — Commit

```bat
git add runbooks\linux\fix-permission-issues.md
git commit -m "Add runbook for fixing Linux permission issues"
git push
