
## Configuration:

- git config --global user.name "Your Name" # Set global user name
- git config --global user.email "your_email" # Set global user email
- git config --global color.ui auto # Enable colored Git output

## Starting a Project:
- git init [project-name] # Create a new local repository
- git clone [repository-url] # Clone a remote repository

## Making and Storing Changes:

- git status # Show modified files, staged files, and untracked files
- git add [file] # Stage a specific file for commit
- git add . # Stage all changes in the current directory
- git rm [file] # Remove a file from working directory and staging area
- git commit -m "Commit message" # Commit staged changes with a message
- git commit --amend # Amend the last commit
- git stash # Temporarily save changes in the working directory
- git stash apply # Restore stashed changes
-git stash drop # Delete a specific stash

## Inspecting History:

- git log # Display commit history
- git log --oneline # Display condensed commit history
- git diff # Show changes between working directory and staging area
- git diff [commit1] [commit2] # Show changes between two commits



