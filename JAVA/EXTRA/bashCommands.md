## Global Git Configuration (applies to all repositories)
```bash
git config --global user.name "Your Name"            # Set your global Git username           
git config --global user.email "youremail@example.com" # Set your global Git email
git config --global init.defaultBranch main          # Set 'main' as the default branch for new repos
git config --global --list                           # Show current global configuration
```


## Local Configuration (applies only to the current repository)
```bash
git config user.name "Local Name"
git config user.email "localemail@example.com"
git config --list                                    # Show all configuration (includes global + local)
```

## Basic Git Commands
```bash
git init                                             # Initialize a new Git repository in the current directory
git clone REPO_URL                                   # Clone a remote repository to your machine
git status                                           # Show the status of the working directory
git add filename                                     # Stage a specific file
git add .                                            # Stage all modified files
git add folder1/ folder2/                            # Stage specific folders

git commit -m "Descriptive commit message"           # Create a commit with staged files
git push origin main                                 # Push commits to the remote repository on the main branch
git pull origin main                                 # Pull the latest changes from the remote main branch
```

## Branch Management
```bash
git branch                                           # List all branches
git branch -r        
git checkout -b branch_name                          # Create and switch to a new branch
git checkout branch_name                             # Switch to an existing branch
git merge branch_name                                # Merge the specified branch into the current branch
git push --set-upstream origin branch_name           # Push and link the new branch to the remote
```

## Stop tracking files or folders without deleting them locally
```bash
git rm --cached file.txt                             # Stop tracking a file without deleting it locally
git rm -r --cached folder/                           # Stop tracking a folder without deleting it locally
```

## Create a new local repo and push to GitHub (with custom remote)
```bash
git init -b main                                     # Initialize a repo with main as the default branch
git add .                                            # Stage all files
git commit -m "Initial commit"                       # Make the initial commit

git remote add github https://github.com/YourUser/YourRepo.git  # Add remote with name 'github'
git push -u github main                              # Push and link the main branch to the remote
```

## Undo last commit (keep changes staged)
```bash
git reset --soft HEAD~1                              # Removes the last commit
                                                    # Keeps the changes in staging (as if you did 'git add .')
                                                    # You can run 'git commit' again to fix the commit message or content
```                                        