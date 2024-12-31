## Adding a Remote Origin

Adding a Remote Origin is for linking your local repository to a new or existing remote repository to push and pull changes.

### 1. Create a New Repository on the command line

        echo "# RepoNo2" >> README.md
        git init
        git add README.md

        git config --global user.name "Your Name"
        git config --global user.email "you@example.com"
        
        git commit -m "first commit"
        
        git commit -m "first commit" --amend # This command modifies the most recent commit instead of creating a new one. Any changes made will be added to the previous commit.
        git branch -M main
        git remote add origin https://github.com/avinash-027/RepoNo2.git
        git push -u origin main

### 2. Push an Existing Repository from the command line

        git remote add origin https://github.com/avinash-027/RepoNo2.git
        git branch -M main
        git push -u origin main

1. Create a Version
```
git init
git status
git add .
git commit -m “Message”
```
2. To View Previous Versions
```
git log --all --graph
git checkout <commit_hash>
git checkout <branch_name>
```
3. Restore to Previous Version 
```
git checkout <hash|branch> <file|folders>
git commit -m “Message” 
```

### What is a Git Repository?
A Git repository (or repo) is a folder that contains all your project files along with the necessary metadata for tracking changes. This includes the history of all changes made to the files, branches, commits, and more. Git uses this folder to store information about the version control and file states.

- Local Repository: This is the version-controlled directory on your local machine where you run Git commands.
- Remote Repository: This refers to a repository hosted on a platform like GitHub, GitLab, Bitbucket, etc.

Git actually tracks changes, not files.

**Git Workflow: Staging Area vs. Working Area**

- Staging Area (changes here WILL go in the next version)
- Working Area (changes here WILL NOT go in next version)

**Git Basics: HEAD vs. Branches (main/master)**
- HEAD refers to the current commit that you are viewing or working on.
When you switch branches, HEAD moves to the latest commit of the new branch, keeping track of where you are in the project.

- main/master is the name of the branch. 
In Git, a branch name points to a specific commit in the repository. More precisely, a branch name is a reference (or pointer) to the latest commit on that branch. Here's a breakdown of how it works:

---
**1. To View Previous Versions**

* Show Commit History (with a graph):

        git log --all --graph --oneline
* Checkout a Specific Commit:

         git checkout <commit_hash>
This will detached HEAD state, meaning you are no longer on a branch.
* Checkout a Branch:

        git checkout <branch_name>

**2. Restore to Previous Version (without affecting HEAD position)**

* Restore a File or Folder from a Specific Commit: 

        git checkout <commit_hash> -- <file_or_folder> 
<!-- or  -->
                git checkout <commit_hash> <file_or_folder>
* Restore a File or Folder from Another Branch: 

        git checkout <branch_name> -- <file_or_folder>
* Commit
        git commit -m "Restored <file_or_folder> from <commit_hash/branch_name>"

---

        git reset .
This command resets the index (staging area) to match the current working directory.

It will unstage all the changes that have been added with `git add`.

        git reset < filename >
This resets the staging area for a specific file, effectively unstaging changes that have been added.

The file in the working directory is not modified.

        git reset --hard HEAD~1 
This resets the working directory and index to the state of the previous commit (HEAD~1).

        git checkout branch_name
This command checks out an existing branch (i.e., switches to it).

        git checkout -b branch_name 
This creates a new branch and checks it out in a single command.

**commands are used to discard changes in the working directory by reverting files (or all files) to their state at the last commit.**
        git checkout -- .
This reverts all changes in the working directory (i.e., all files) to the state of the last commit.

        git checkout -- < filename>
This reverts the changes in the specified file to the state of the last commit.

* **To view** 
        `git checkout < commit hash >`

This checks out a specific commit by its commit hash, updating the working directory and index to that state.

* **To Restore**
        `git checkout < commit hash >` 

This checks out the contents of a specific commit for the working directory, but keeps the current branch intact.

It updates the working directory for all files.

        git log
        git log --all
        git log --oneline
        git log --all --graph

Note: 
- git log does not **show** [Unnamed Branches](#unnamed-branches)
- Press “q” to close the git log (if needed)

### Git Alias

```
git config --global alias.s "status"
git config --global alias.cm "commit -m"
git config --global alias.co "checkout"
```

### .gitignore

`.gitignore` = Ignores specified files

- The .gitignore file is used to specify which files or directories Git should ignore in a repository.
- The .gitignore file prevents specified files from being added to the repository or tracked by Git.

**KEY Notes:**

- You should add the .gitignore file to your repository after creating it, to ensure that the files listed within it are ignored by Git. This helps keep your repository clean and avoids tracking files that don't need to be versioned, such as build artifacts, temporary files, or sensitive data.

- If you add README.md to .gitignore after it has already been tracked, Git will continue tracking it, and you don't need to worry about .gitignore unless you remove it from tracking.
- If you add README.md to .gitignore before it was ever tracked, then it won't show up in the repository, and you'll need to follow the steps above to track it explicitly.

Conclusion:
- In .gitignore, you can exclude files from being tracked by Git, but you can always explicitly include files with the ! rule. If you want README.md to be tracked even though it's ignored, simply unignore it in the .gitignore file using !README.md, then stage and commit it.

#### If You Add README.md to .gitignore After Tracking It?

1. If README.md Is Already Tracked and Then Added to .gitignore:

   Once a file like README.md has been added to the Git repository and is being tracked (i.e., it has been committed at least once), adding it to .gitignore will not stop it from being tracked. Git will continue to track it as normal.

3. What Happens If You Add README.md to .gitignore After Tracking It?

   If README.md was already tracked, adding it to .gitignore will have no effect on the file—it will continue to be tracked by Git as it was before. However, it will not be staged for future commits unless you explicitly add it again (e.g., with git add).

4. If You Want to Stop Tracking a Previously Tracked File (e.g., README.md):

   If you want Git to stop tracking a file that is already being tracked (like README.md), you'll need to remove it from the index (staging area) while leaving it in the working directory. This can be done with the following command:
```
        git rm --cached README.md
        git commit -m "Stop tracking README.md"
```
- --cached tells Git to stop tracking the file but leave it in your working directory (so it won't be deleted from your local file system).

The .gitignore file only affects files that have not yet been tracked by Git. It prevents Git from starting to track new files or changes to files that haven't been added to the repository yet.

#### Multiple .gitignore Files

**➡ Multiple .gitignore files are fine as long as they’re in different directories.**
```
/my-project
  ├── .gitignore    # Applies to files in the root and all subdirectories
  ├── src/
  │   └── .gitignore # Applies to files in the src/ directory and its subdirectories
  └── build/
```
**Example Scenario:**
```
/my-project
  ├── .gitignore        # Ignores *.log and *.tmp files globally
  ├── src/
  │   └── .gitignore    # Ignores build artifacts like *.o and *.class files
  └── build/
```
**➡ Multiple .gitignore files in the same directory is not recommended and doesn't work as intended.**
```
/my-project
  ├── .gitignore       # First .gitignore
  ├── .gitignore       # Second .gitignore (ignored by Git)
```

### Removing the Git Directory

```
rm -rf .git
```
```
PowerShell              : Remove-Item -Recurse -Force .git
Command Prompt (CMD)    : rmdir /s /q .git
Git Bash/Bash           : rm -rf .git
```
- Removes Version Control: 
  It removes all the version control metadata (commits, branches, history, etc.) in the repository. After doing this, your folder will no longer be a Git repository — it’s just a regular directory with files, no longer tracked by Git.

- Warning:
  This action is permanent (unless you have backups or undo the action via file recovery tools). If you run this command, you lose all your Git history and cannot easily recover it from that directory.

## ISSUES :

### Unnamed Branches:

Unnamed Branches (also referred to as detached HEAD states) don't have a specific name associated with them. However, you can still view them and understand what happens when you're in such a state.

**1. What Happens to Unnamed Branches (Detached HEAD)?**

* Detached HEAD State: When you are in a detached HEAD state, you're not working on any named branch. Instead, the HEAD is pointing directly to a specific commit.
* In this state, Git doesn't associate your changes with any branch, and if you make new commits, they won't belong to any named branch unless you explicitly create a new branch with git checkout -b `<branch-name>`.

**2. Impact of Detached HEAD:**

* You can still commit changes and create new commits, but they are not attached to any branch. If you switch branches without creating a new branch from your current state, the new commits will be lost.
* If you want to keep these commits, you need to create a new branch from this detached state.

**How to View Detached HEAD States or Unnamed Branches:**

        git log --oneline
        git reflog
        git branch -a

If you're in a detached state, you won’t see any branch with HEAD pointing to it. Instead, it will show something like: `* (HEAD detached at <commit-hash>)`

        git checkout -b <new-branch-name> 

This will create a new branch and attach it to your current commit, effectively giving a name to your "unnamed" branch.
 
### Why `git commit --amend` Creates a New Commit

The reason a new commit is being created despite using git commit --amend is that your previous commit (with the message "Initial Commit") **was already pushed to the remote repository** (origin/main). Once you amend a commit that has already been pushed, Git treats the amended commit as a new commit because it changes the commit hash, and your local history diverges from the remote history.

The **key factor** here is that you're amending a commit that has already been pushed to the remote. git commit --amend works by rewriting history, which changes the commit hash. If you amend a commit that's already been pushed to the remote, you'll create a new commit locally with a new hash, but the remote history remains unchanged until you push.

**How to Fix or Avoid It:**

- If you don't need to preserve the remote commit history, you can force-push the amended commit to the remote
- If you want to avoid rewriting history, a better approach would be to simply create a new commit (instead of amending) that addresses any issues in the previous commit.  
