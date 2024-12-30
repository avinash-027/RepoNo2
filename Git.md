    dir /a 
    Get-ChildItem -Force 

Global Configuration

      git config --global --list
      git config --global user.namge
      git config --global user.email

when you initialize a new Git repository using git init in a new folder, it will still use the existing global configuration unless you explicitly override it in the local repository.

If you want to change the name/email for just this repository:

    git config --local user.name "Your Local Name"
      git config --local user.email "yourlocal@email.com"

This will override the global configuration only for this repository, but the global configuration will remain unchanged for others.
it means that the local configuration (specific to the repository) will override the global configuration only for that particular repository/folder.

To change an existing global Git configuration, you simply use the same git config command with the --global flag, but provide the new values you want.  

      git config --global user.name "New Name"
      git config --global user.email "new.email@example.com"
    
      git config --global core.editor "nano"
      git config --global merge.tool vimdiff
      git config --global color.ui auto
      git config --global --list

No, Git doesn't allow you to have multiple global configurations for the same setting (e.g., multiple user.name or user.email). The global configuration is intended to apply to all repositories unless overridden by a local configuration.

However, you can have different configurations for different repositories using local configurations, even if you have a global one set.

So, if you want different configurations for different repositories, you can:
  1. Set your global configuration for general use.
  2. Set specific configurations locally within each repository (which override the global configuration for that repository).

using `git clone <repository-url>`

  - If you don't specify a folder: Git will create a new folder based on the repository name.
  - If the folder is empty: Git will clone into it successfully.
  - If the folder is non-empty: Git will not clone into the existing folder unless it’s empty, and you will either need to create a new folder or clear the existing one.


### CLONING

Cloning is for getting a copy of an existing remote repository to your local machine.
   
    git config --global user.name "Your Name"
    git config --global user.email "you@example.com"
    git config --global core.editor "code --wait"
    git config --global core.autocrlf true   # On Windows

      git clone https://github.com/user/repository.git  # Now clone the repo
      cd repository                                    # Enter the cloned repo folder

    git config user.name "Your Local Name"
    git config user.email "your_local_email@example.com"
    git config core.editor "nano"
    git config core.autocrlf false
    git config --list --local

      # Make changes to files, then stage and commit
      git add .                                        # Add all changes
      git commit -m "Updated README file"              # Commit changes
      git push origin main                             # Push to remote


### ADDING REMOTE URL

Adding a Remote Origin is for linking your local repository to a new or existing remote repository to push and pull changes.

    git config --global user.name "Your Name"
    git config --global user.email "you@example.com"
    git config --global core.editor "code --wait"
    git config --global core.autocrlf true   # On Windows

      git init                                       # Initialize the local repo
      echo "Hello" >> README.md                     # Create a README file
      git add README.md                              # Stage the file
      git commit -m "Initial commit"                 # Commit the file
      git remote add origin https://github.com/user/repository.git  # Link to GitHub repository
      git push -u origin main                        # Push the local commit to GitHub

**Git Commit Identity:**

  When you commit changes in Git, your email address is included in the commit history as part of the commit metadata. This is used to identify the author of each commit.
  
  The user.email value can be any valid email address—it doesn't necessarily need to be your personal or original email, but it's typically your real email because it links your commits to you as the author.

**GitHub and Other Platforms:**

If you're using GitHub or another Git hosting service, the email you configure in Git should usually match the email you use for the GitHub account. This ensures that the commits are associated with your GitHub profile.

If you want to keep your email private when pushing commits to a platform like GitHub, you can use the GitHub-provided "noreply" email. For example, GitHub provides a noreply email like this: yourusername@users.noreply.github.com.

      git config --global user.email "yourusername@users.noreply.github.com"
      git config --global user.email "ken027@users.noreply.github.com"

**How to Find Your GitHub Noreply Email:**

  - If you're unsure of the exact noreply address GitHub is using for you, you can find it by following these steps:
  - Go to GitHub's Email Settings Page.    
  - Under "Primary email address", you should see a section for "GitHub-provided noreply email address". 
It will look like: yourusername@users.noreply.github.com
This is the email GitHub uses for commits to keep your email address private while still attributing the commits to your account.

###################################################################################################

### Overview of Git and Version Control Systems (VCS)

#### Version Control Systems (VCS)
Version Control Systems are tools that help manage and track changes to source code over time. There are two main types:
1. Centralized Version Control Systems (CVCS): 
   - Example: Subversion (SVN), Team Foundation Server (TFS).
   - Centralized Server: All code and history are stored on a central server.
   - Advantages: Centralized access, simpler for smaller teams.
   - Disadvantages: Single point of failure, performance bottleneck, no offline work.

2. Distributed Version Control Systems (DVCS):
   - Example: Git, Mercurial.
   - Multiple Servers: Each developer has a full copy of the repository, allowing for offline work.
   - Advantages: High speed, scalable, supports branching/merging, can work offline.
   - Disadvantages: Larger initial repository size, complex merges.

---

### What is Git?
Git is a distributed version control system (DVCS) primarily used to track changes in source code during software development. It allows for both local and remote repositories, enabling efficient collaboration and code versioning.

- Features of Git:
  - Free and Open Source.
  - Snapshots: Git stores a snapshot of changes rather than differences between file versions, making it fast and efficient.
  - Branching/Merging: Git supports powerful branching and merging workflows.
  - Local (on the developer's machine) and Remote (on servers like GitHub, GitLab) repositories.

#### Git Terminology
- Repository: A storage location for your project files and their version history.
- Staging Area (Index): The area where changes are placed before committing to the repository.
- Commit: A snapshot of changes, including a message, author information, and timestamp.

---

### Git Configurations

#### 1. Global Configuration
   - These configurations apply to all repositories on the system. 
   - Examples:
     ```bash
     git config --global user.name "Your Name"
     git config --global user.email "you@example.com"
     git config --global core.editor "code --wait" # Sets the default editor to VSCode
     ```
   - Configuration is stored in `~/.gitconfig`.

#### 2. Local Configuration
   - Specific to a repository. Stored in the `.git/config` file inside the repository.
   - Can override global configurations.
   - Example:
     ```bash
     git config user.name "Your Repo-Specific Name"
     ```

#### 3. System Configuration
   - These configurations apply to all users on the system.
   - Can be modified by system administrators.

#### Line Endings Configuration:
- Git handles different line endings across platforms (Windows vs Linux).
  - Windows: Line endings are `\r\n`.
  - Linux: Line endings are `\n`.
- Configuration for handling line endings:
  ```bash
  git config --global core.autocrlf true   # On Windows
  git config --global core.autocrlf input  # On Linux
  ```

---

### Basic Git Workflow
1. Working Directory: Where your files live and are being modified.
2. Staging Area (Index): A place to prepare changes before committing.
3. Repository: A storage of committed files and their version history.

#### Commands for Managing Git Workflow

- Initialize a Repository:
  ```bash
  git init  # Creates a new Git repository
  git clone <repository-url>  # Clone an existing repository
  ```

- Check the Status:
  ```bash
  git status   # Shows modified, staged, and untracked files
  git status -s  # Shows short status output
  ```

- Track Files (Add to Staging Area):
  ```bash
  git add <file-name>   # Add specific files
  git add .             # Add all modified files
  ```

- Commit Changes:
  ```bash
  git commit -m "Your commit message"  # Commit changes with a message
  git commit -am "Your commit message"  # Add and commit changes in one step (skip staging)
  ```

- View Commit History:
  ```bash
  git log              # Full commit history
  git log --oneline    # Shortened commit history
  git log --oneline --reverse  # View commits in reverse order
  ```

- Change/Checkout Branch:
  ```bash
  git checkout <branch-name>     # Switch to an existing branch
  git checkout -b <branch-name>  # Create and switch to a new branch
  ```

- Merge Branches:
  ```bash
  git merge <branch-name>  # Merge another branch into the current branch
  ```

- Delete a Branch:
  ```bash
  git branch -d <branch-name>   # Delete branch after merging
  git branch -D <branch-name>   # Force delete a branch
  ```

---

### Special Git Commands

- Amend Last Commit:
  ```bash
  git commit --amend  # Modify the last commit (can change message, add files, etc.)
  ```

- Force Push (Overwriting Remote):
  ```bash
  git push --force  # Forcefully push changes to the remote repository
  ```

- Revert a Commit (Undo):
  ```bash
  git revert <commit-hash>  # Reverts a commit by creating a new commit
  ```

- Stash Changes:
  ```bash
  git stash     # Temporarily save changes
  git stash pop # Apply the most recent stash
  ```

- Reset Changes:
  ```bash
  git reset --hard  # Reset the working directory and staging area to the last commit
  git reset HEAD~1  # Undo the last commit, keep changes in working directory
  ```

- Show Changes:
  ```bash
  git diff       # See unstaged changes
  git diff --staged  # See staged changes
  ```

- Git Clean (Remove Untracked Files):
  ```bash
  git clean -fd  # Remove untracked files and directories
  ```
---

### Remote Repositories
Remote repositories, like GitHub, allow you to store your code in the cloud and collaborate with others.

- Add a Remote Repository:
  ```bash
  git remote add origin <repository-url>  # Add a remote repository (e.g., GitHub)
  ```

- Push to Remote:
  ```bash
  git push -u origin main  # Push changes to the main branch on remote repository
  ```

- Fetch from Remote:
  ```bash
  git fetch origin  # Get changes from the remote repository
  ```

- Pull Changes:
  ```bash
  git pull origin main  # Pull the latest changes from the main branch
  ```

- View Remote URLs:
  ```bash
  git remote -v  # View remote repositories associated with the local repo
  ```

- Rename Remote:
  ```bash
  git remote rename origin old-origin  # Rename a remote repository
  ```

---

### GitHub Specific Commands
GitHub is a hosting service for Git repositories, enabling collaboration and sharing.

1. Initialize a GitHub Repository:
   ```bash
    echo "Hello" >> README.md           # Create the README.md file with "Hello"
    git init                            # Initialize a new Git repository
    git add README.md                   # Stage the README.md file
    git commit -m "Initial commit"       # Commit the changes
    git branch -M main                  # Rename the current branch to 'main'
    git remote add origin https://github.com/user/repo.git  # Add remote URL
    git push -u origin main             # Push the changes to GitHub
   ```

If the GitHub repository doesn't exist yet, you can create it directly from GitHub. After creating the repository, GitHub will provide you with the repository URL (e.g., https://github.com/user/repo.git).

If you already have an existing GitHub repository and want to push an existing local repository to it, the above steps are valid. Just make sure that the repository URL (https://github.com/user/repo.git) matches the GitHub repository you want to push to.

2. Forking and Pull Requests (PR):
   - Fork: Create your own copy of a repository.
   - Clone: Download the repository to your local machine.
   - Commit Changes: Make changes to the code.
   - Push Changes: Push the changes back to your fork.
   - Pull Request: Request the original repository owner to merge your changes.

3. Collaborating on GitHub:
   - Review and comment on pull requests.
   - Resolve merge conflicts and review code before merging.
   
---
### Example Workflow After Cloning a Repository
After cloning a repository, you can start working on it. Here's an example workflow: 

  git clone https://github.com/username/repository-name.git
  cd repository-name
  git add file1.txt
  git add folder1/
  git status
  git commit -m "Update files or add new files"
  git push origin main



### Useful Git Aliases
You can create Git aliases to shorten frequently used commands:

```bash
git config --global alias.co "checkout"
git config --global alias.br "branch"
git config --global alias.ci "commit"
git config --global alias.st "status"
```

---

### Git GUI Tools
While the command-line interface (CLI) is powerful, there are several Git GUI tools that provide a more user-friendly interface:

- GitKraken
- Sourcetree
- GitHub Desktop
- Git GUI

These tools allow you to perform Git operations through graphical interfaces, making them useful for beginners or those who prefer visual tools.

---

### Notes
Git is a powerful tool for managing code versions and collaborating with others. Its flexibility, speed, and branching features make it essential for software development. Understanding its key commands and workflows will help you effectively manage your codebase and collaborate with other developers.