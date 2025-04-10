# Git Guide

This guide provides an overview of Git workflows and practices for the HeyHomie Next.js application.

## Setting Up Git

1. **Install Git** - Make sure you have Git installed on your machine
2. **Configure Your Identity**

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

3. **Generate and Add SSH Key** (recommended)

```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "your.email@example.com"

# Start the SSH agent
eval "$(ssh-agent -s)"

# Add your SSH key to the agent
ssh-add ~/.ssh/id_ed25519

# Copy your public key and add it to your GitHub/GitLab account
cat ~/.ssh/id_ed25519.pub
```

## Git Workflow

We follow a feature branch workflow:

### Creating a Branch

Always create a new branch for your work:

```bash
# First, update your main branch
git checkout main
git pull origin main

# Create a new branch
git checkout -b feature/descriptive-name
```

Use these branch naming conventions:

- `feature/` - For new features
- `fix/` - For bug fixes
- `refactor/` - For code refactoring
- `docs/` - For documentation changes
- `chore/` - For maintenance tasks

### Making Commits

Write meaningful commit messages using conventional commits format:

```bash
git commit -m "feat: add product search functionality"
git commit -m "fix: resolve order calculation issue"
git commit -m "docs: update API documentation"
git commit -m "refactor: simplify authentication flow"
git commit -m "chore: update dependencies"
```

### Pull Requests

1. **Keep Pull Requests Small and Focused**
   - Each PR should address a single concern
   - Break large features into smaller PRs

2. **Write Descriptive PR Titles and Descriptions**
   - Title should summarize the changes
   - Description should explain the purpose and implementation approach

3. **Request Reviews from Team Members**
   - At least one approval is required before merging

### Code Review

1. **Be Responsive to Review Comments**
   - Address all comments
   - If you disagree with a comment, explain your reasoning

2. **As a Reviewer, Provide Constructive Feedback**
   - Be specific about issues
   - Suggest improvements when possible
   - Approve once all concerns are addressed

### Merging

We use squash merging to keep the main branch history clean:

```bash
# When merging feature branch to main via CLI
git checkout main
git pull origin main
git merge --squash feature/your-feature
git commit -m "feat: comprehensive description of the feature"
git push origin main
```

However, most merges should be done through the GitHub/GitLab interface using the "Squash and merge" option.

## Git Hooks

We use Husky for Git hooks:

- **Pre-commit** - Runs linting and formatting on staged files
- **Pre-push** - Runs type checking and tests

## Handling Merge Conflicts

When encountering merge conflicts:

```bash
# Update your branch with the latest main
git checkout main
git pull origin main
git checkout your-branch
git merge main

# Resolve conflicts in your editor
# After resolving
git add .
git commit -m "Merge main into your-branch and resolve conflicts"
```

## Advanced Git Commands

### Stashing Changes

```bash
# Stash your changes
git stash

# Apply the most recent stash
git stash apply

# List all stashes
git stash list

# Apply a specific stash
git stash apply stash@{n}

# Pop the most recent stash (apply and remove)
git stash pop
```

### Rebasing

```bash
# Rebase your branch on latest main
git checkout main
git pull
git checkout your-branch
git rebase main

# Interactive rebase for cleaning up commits
git rebase -i HEAD~n  # where n is the number of commits to rebase
```

### Amending Commits

```bash
# Amend the last commit
git commit --amend

# Amend without changing the commit message
git commit --amend --no-edit
```

### Cherry-picking

```bash
# Apply a specific commit to your current branch
git cherry-pick <commit-hash>
```

## Troubleshooting

### Undo Last Commit (But Keep Changes)

```bash
git reset --soft HEAD~1
```

### Discard All Local Changes

```bash
git reset --hard HEAD
```

### Find Which Commit Introduced a Bug

```bash
git bisect start
git bisect bad  # Current commit has the bug
git bisect good <known-good-commit>  # Last known good commit
# Git will checkout various commits for you to test
# After testing each commit, mark it as good or bad
git bisect good  # or git bisect bad
# When done
git bisect reset
```

## Best Practices

1. **Commit Early and Often** - Make small, logical commits
2. **Keep Branches Short-Lived** - Merge or delete branches soon after they've served their purpose
3. **Pull Before Push** - Always pull the latest changes before pushing
4. **Write Meaningful Commit Messages** - Use the conventional commits format
5. **Never Force Push to Main** - Only force push to your own feature branches
6. **Avoid Committing Generated Files** - Make sure your .gitignore is properly configured
7. **Regularly Cleanup Old Branches** - Delete merged or stale branches
