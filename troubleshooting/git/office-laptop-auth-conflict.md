# ❗ Git 403 Error on Office Laptop (Authentication Conflict)

## Environment

- Office-managed Windows laptop
- Corporate GitHub account configured
- Personal GitHub repo being used

---

## Error

```text
Permission denied to vranjan-capacity (403)
Cause
Windows credential manager had cached corporate GitHub credentials.
Git automatically reused those credentials when pushing to personal repo.

Fix Applied
Overrode remote URL to force Personal Access Token authentication.

bash
Copy code
git remote -v

git remote set-url origin https://USERNAME:TOKEN@github.com/USERNAME/REPO.git

git push
Verification
Push succeeded

Repo now authenticates using personal account only

Prevention
Avoid mixing corporate and personal GitHub accounts

Prefer SSH keys per account if allowed

