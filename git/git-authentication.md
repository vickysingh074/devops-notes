# Git Authentication on Office Laptop

**Tags:** #git #authentication #windows #corporate #security

## Problem
Unable to push to personal GitHub repo from office laptop.
Error:
Permission denied to vranjan-capacity (403)

## Root Cause
- Office laptop had cached GitHub credentials.
- Git automatically used corporate account.
- Personal repo denied permission.

## Solution
Use Personal Access Token and override remote URL locally.

### Commands
git remote -v

git remote set-url origin https://<USERNAME>:<TOKEN>@github.com/<USERNAME>/<REPO>.git

git push


## Why This Works
- Token forces Git to authenticate as personal account.
- Change applies only to this repository.
- Does not affect system or office Git settings.

## Security Notes
- Token should be kept private.
- Can regenerate token anytime.

## Learning
Corporate environments require safe authentication isolation.
