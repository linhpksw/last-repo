# Introduction

-   What is GitHub and why we use it.
-   Key terms: Repository, clone, commit, branch, merge, pull request, conflict, etc.

# Setup Github with VS Code

-   Download GIT for Windows: https://git-scm.com/downloads
-   Download Node JS for running test file: https://nodejs.org/en

# Hands-on: Creating a Repository

1. **GUI (10 minutes)**

-   How to create a new repository using VS Code's GUI.
-   Adding a README file and initial commit.
-   Pushing to GitHub.
    git config --global user.name "John Doe"

git config --global user.email "johndoe@email.com"

2. Github Web

3. \*\*Command Line (10 minutes)

-   \*\*Commands: `git init`, `git add`, `git commit`, `git remote add`, `git push`.

```bash
mkdir your_project_name
cd your_project_name

git init                                    // initialize a new Git repository
echo "# My New Project" > README.md

git add .                                   // Add your files to the staging area

git commit -m "Initial commit"

// Before you can push your repository to GitHub, we need to create in Github

git remote add origin YOUR_GITHUB_REPOSITORY_URL

git push -u origin main       // Push your commits to the online GitHub repo
```

# Hands-on: Basic Git Operations

1. **GUI (20 minutes)**

-   Making changes and committing them.
-   Syncing with the online repository (pulling and pushing).
-   Introduction to branching and merging using VS Code's GUI.

2. **Command Line (20 minutes)**

-   Commands: `git status`, `git add .`, `git commit -m`, `git pull`, `git push`, `git branch`, `git checkout`, `git merge`.

---

# Collaborative Exercise: Simulating Collaboration

-   Divide participants into pairs. One will be the 'main' developer and the other will be a 'collaborator'.

-   Each pair will have two tasks:

    1. 'Main' developer makes a change and the collaborator pulls it.
    2. Both make changes to the same file to simulate a conflict.

-   **Resolving Conflicts (20 minutes)**
    -   Walk through the process of resolving conflicts using VS Code.
    -   Emphasize the importance of communication between team members.

---

# Origin in Git

-   **Definition**: In Git, `origin` is the default name given to the remote repository where you cloned from. When you run a command like `git clone https://github.com/user/repo.git`, Git automatically names this remote repository `origin`.
-   **Remote Repositories**: In Git, a remote is a common repository that all team members use to exchange their updates. Locally, it's a reference to another copy of the repository that resides on a different location, either on the internet, on a network, or even on the same machine.
-   **Using `origin`**: The term `origin` is used in various Git commands to refer to the remote repository. For example:
    -   `git fetch origin`: Fetches changes from the remote repository but doesn't merge them.
    -   `git push origin master`: Pushes your local `master` branch to the `origin` remote.
    -   `git pull origin master`: Fetches changes from the remote `master` branch in `origin` and merges them into your current branch.
-   **Managing Remotes**: You can have multiple remotes (other than `origin`). For instance, when collaborating on a project, you might add other developer's repositories as remotes to review or merge their changes.
    -   Add a remote: `git remote add remote_name remote_url`
    -   View remotes: `git remote -v`
    -   Remove a remote: `git remote remove remote_name`

# HEAD in GIT

Of course! Let's dive into the concept of `HEAD` in Git.

### **What is `HEAD` in Git?**

In Git, `HEAD` is a special pointer or reference that points to the latest commit in the branch that is currently checked out. Essentially, it represents the "current snapshot" of your project.

### **Characteristics of `HEAD`**

1. **Dynamic Pointer**: Unlike other references (like branches or tags), `HEAD` moves automatically when you create a new commit.

2. **Normally Points to a Branch**: Under typical circumstances, `HEAD` points to the branch reference, which then points to a commit. For instance, if you're on the `master` branch and the latest commit hash is `abcd123`, `HEAD` points to `master`, and `master` points to `abcd123`.

3. **Detached `HEAD` State**: If you checkout a specific commit and not a branch (e.g., `git checkout abcd123`), `HEAD` will point directly to that commit, not through a branch reference. This is called a "detached `HEAD`" state. In this state, you're no longer on a specific branch; you're just at a particular commit.

### **Examples of `HEAD` Usage in Git**

1. **Viewing the Commit `HEAD` Points to**:

```bash
git log -n 1 HEAD
```

This command shows the latest commit of the current branch.

2. **Move Back to a Previous Commit**:

If you want to go back to the commit before the latest one, you can use:

```bash
git checkout HEAD~1
```

This puts you in a detached `HEAD` state, at one commit before where `HEAD` previously pointed. The `~1` means "one commit before".

3. **Reverting Changes**:
   If you want to undo the changes made in the last commit, but keep a record of it (i.e., create a new commit that undoes the changes), you can use:

```bash
git revert HEAD
```

This will create a new commit that undoes the changes of the commit that `HEAD` was pointing to.

4. **Resetting Changes**:

If you want to discard the last commit:

```bash
git reset --hard HEAD~1
```

This command moves `HEAD` back by one commit, effectively discarding the latest commit. Be cautious with this command as it discards the commit without any trace.

Remember, while `HEAD` gives you a powerful way to navigate and manipulate the commit history, some of the operations (like `reset`) can be destructive. It's essential to have a clear understanding and be sure of what you're doing when manipulating `HEAD` directly.

# Reverting to a Previous Commit

#### **1. Check Commit History**

First, identify the commit hash of the commit you want to revert back to:

```bash
git log
```

#### **2. Resetting the Repository to the Desired Commit**

To remove commits from the local repository and retain the changes in your working directory:

```bash
git reset --soft SHA_HASH_OF_COMMIT
```

To remove commits from the local repository and discard changes:

```bash
git reset --hard SHA_HASH_OF_COMMIT
```

**IMPORTANT**: Force pushing changes to a repository can disrupt the work of others. Only do this if you are sure that no one has based work off the commits you're removing, or if everyone is aware of and has agreed to this action.

```bash
git push origin branch_name --force
```

### **Warning and Recommendations**

-   **Backup Before Reset**: Before performing a reset, consider creating a backup branch so that you can always return to the current state if needed:

```bash
git branch backup_branch_name
```

-   **Alternative - Revert Command**: If you just want to reverse the changes introduced by certain commits without altering the commit history, you can use the `git revert` command. This will create new commits that reverse the changes introduced by the specified commits:

```bash
git revert OLDEST_COMMIT_SHA^..NEWEST_COMMIT_SHA
```

# Git Branch

### **Common Branching Commands:**

1. **Create a New Branch**: This will create a new branch and keep you on your current branch.

```bash
git branch branch_name
```

2. **Switch to a Branch**: This switches your working directory to the specified branch.

```bash
git checkout branch_name
```

3. **Create and Switch**: This command will create a new branch and switch to it in a single step.

```bash
git checkout -b branch_name
```

4. **List Branches**: This will list all the branches in your repository. The branch you're currently on will be indicated.

```bash
git branch
```

5. **Delete a Branch**: This will delete the specified branch.

```bash
git branch -d branch_name
```

6. **Rename a Branch**: To rename the current branch:

```bash
git branch -m new_name
```

### **Merging Branches:**

When you've finished the changes on your branch, you might want to merge those changes back into the `main` or `master` branch (or another target branch).

```bash
git checkout master       # Switch to the branch you want to merge changes into git merge branch_name     # Merge the specified branch into your current branch
```

### **Dealing with Merge Conflicts:**

If Git can't automatically merge changes, you'll encounter a merge conflict. You'd need to manually resolve these conflicts. Git marks the problematic areas in the file. After fixing, you'd add the resolved file to the staging area and then complete the merge.

# Additional Features and Best Practices

-   Using `.gitignore` to exclude files.
-   The importance of meaningful commit messages.
-   The idea of "committing often and pushing regularly."
-   Discussion on GitHub's additional features like Issues, Discussions, and Actions (just a brief intro if further sessions are planned).

---

# Q&A and Feedback

-   Open the floor for questions.
-   Address any common issues or misconceptions.
-   Gather feedback for improving future sessions.

---

# Conclusion

-   Highlight the importance of practice.
-   Encourage team members to collaborate on a small project or task using GitHub to solidify their understanding.
-   Share additional resources for learning.

---
