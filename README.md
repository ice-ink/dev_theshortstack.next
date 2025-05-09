# dev_theshortstack.next

fancy next based template packed for butt stuff!

## pre-dev

## todo

- [] revert dev branch to next init with ts/tw
- [] add shadcn?
- [] research database support?
- [] research feed framework or implementation

## deepseek

*output 01*

```
To rewind a Git branch to an earlier commit and start fresh from that point, you have a few options depending on whether you want to keep or discard the changes made after the target commit. Here’s how to do it:
Option 1: Discard All Changes After the Target Commit (Hard Reset)

This permanently deletes all commits and changes after the target commit.
Use case: You want to completely restart the branch from an earlier state.

    Check the commit history to find the target commit hash (git log --oneline).

    Reset the branch to the target commit (replace <commit-hash>):
    bash

git reset --hard <commit-hash>

Example:
bash

git reset --hard abc1234

Force push (if the branch was already pushed remotely):
bash

    git push --force-with-lease

⚠️ Warning: This erases all changes after the target commit. Use only if you’re sure you don’t need them.
Option 2: Keep Changes as Uncommitted (Soft/Mixed Reset)

This rewinds the branch but keeps changes in your working directory (unstaged or staged).
Use case: You want to redo commits from the target point but reuse the changes.

    Soft reset (keeps changes staged):
    bash

git reset --soft <commit-hash>

    Changes will appear as staged (git status shows them ready to commit).

Mixed reset (keeps changes unstaged):
bash

git reset --mixed <commit-hash>  # Default behavior (same as `git reset`)

    Changes will appear as modified but not staged.

Commit the changes anew:
bash

    git commit -m "Restart from <commit-hash>"

Option 3: Create a New Branch from the Target Commit

Use case: You want to preserve the original branch but start fresh from an earlier point.
bash

git checkout <commit-hash>      # Detach HEAD to the target commit
git checkout -b new-branch-name # Create a new branch from there

Option 4: Revert Commits (Safe for Shared Branches)

Use case: You want to undo changes without rewriting history (e.g., for public branches).
This creates new commits that reverse the unwanted ones:
bash

git revert <commit-hash>..HEAD  # Revert all commits from `<commit-hash>` to HEAD

Key Notes

    Uncommitted changes: Stash (git stash) or commit them before resetting.

    Recovering lost commits: Use git reflog to find and restore deleted commits.

    Force-pushing: Only use --force or --force-with-lease on branches not shared with others.

Example Workflow (Hard Reset)

    Find the target commit:
    bash

git log --oneline
# Output: abc1234 (HEAD -> main) Fix login bug
#          def5678 Add feature X
#          9d28a2b Initial commit

Rewind to 9d28a2b (discarding later changes):
bash

git reset --hard 9d28a2b

Force push (if needed):
bash

    git push --force-with-lease origin main

Which Option to Choose?
Scenario	Best Option
Discard all changes permanently	git reset --hard
Reuse changes for new commits	git reset --soft/mixed
Preserve original branch	Create a new branch
Undo changes on shared branches	git revert
```