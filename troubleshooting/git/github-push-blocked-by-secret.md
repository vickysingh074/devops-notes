🚨 GitHub Push Blocked Due to Secret (Push Protection)

Tags: #git #github #security #secrets #troubleshooting

❗ Problem

While pushing commits to GitHub, push gets blocked with error like:

GH013: Repository rule violations found
Push cannot contain secrets
GitHub Personal Access Token detected


GitHub Push Protection prevents pushing commits that contain:

Personal Access Tokens (PAT)

API keys

Passwords

Private keys

Even if secret is later removed in another commit, GitHub still blocks because secret exists in history.

🔍 Root Cause

A sensitive value (like PAT) was:

Written in a markdown/doc file for example

Committed to Git history

Even though later commits removed it, the earlier commit still contains the secret

GitHub scans entire push history, not just latest commit.

✅ Solution (Clean the Git History)

We must remove the bad commit from history using interactive rebase.

✅ Step 1: Start Interactive Rebase

Go back enough commits to include the bad one:

git rebase -i HEAD~10

✅ Step 2: Drop the Commit Containing Secret

In editor, change:

pick ad4e3a3 commit message


to:

drop ad4e3a3 commit message


Or delete that line.

Save and exit:

Esc → :wq → Enter

⚠ If Git Stops With Conflict

Because multiple commits may touch same file, Git may stop with:

CONFLICT in file.md
could not apply <commit>


Then simply skip that commit:

git rebase --skip


Repeat git rebase --skip until you see:

Successfully rebased and updated refs/heads/main

✅ Step 3: Push Clean History

Because history changed:

git push --force

🔐 Mandatory Security Step

If a token was committed (even locally):

👉 Go to GitHub → Settings → Developer Settings → Personal Access Tokens
👉 Revoke the exposed token immediately
👉 Generate a new one if required

Never reuse leaked tokens.

✅ Prevention (Best Practice)

In documentation and examples, always use placeholders:

YOUR_TOKEN
<PAT>
xxxx


Never real secrets in:

Markdown files

Config files

Scripts

Screenshots