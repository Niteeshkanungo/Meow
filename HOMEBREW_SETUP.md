# Homebrew Setup Guide

## Quick Setup (Personal Tap - Recommended)

### Step 1: Create Homebrew Tap Repository
1. Go to https://github.com/new
2. Repository name: `homebrew-tap` (must be exactly this name)
3. Make it **public**
4. Don't initialize with README, .gitignore, or license
5. Click "Create repository"

### Step 2: Add Formula to Tap
1. Clone your new tap repository:
   ```bash
   git clone https://github.com/Niteeshkanungo/homebrew-tap.git
   cd homebrew-tap
   ```

2. Create Formula directory:
   ```bash
   mkdir -p Formula
   ```

3. Copy the formula from this project:
   ```bash
   cp /path/to/Meow/Formula/meow.rb Formula/meow.rb
   ```

4. Update the version and SHA256 in the formula:
   ```bash
   # Get the SHA256 of your release tarball
   curl -sL https://github.com/Niteeshkanungo/Meow/archive/refs/tags/V1.22.1.tar.gz | shasum -a 256
   ```

5. Commit and push:
   ```bash
   git add Formula/meow.rb
   git commit -m "Add meow formula"
   git push origin main
   ```

### Step 3: Set Up GitHub Secrets
1. Go to your Meow repository: https://github.com/Niteeshkanungo/Meow/settings/secrets/actions
2. Create a Personal Access Token (PAT):
   - Go to https://github.com/settings/tokens
   - Generate new token (classic)
   - Give it `repo` scope
   - Copy the token
3. Add secret to Meow repository:
   - Name: `PAT_TOKEN`
   - Value: (paste your token)

### Step 4: Create a Release
```bash
cd /path/to/Meow
git tag V1.22.1
git push origin V1.22.1
```

This will trigger the GitHub Actions workflow to automatically update the formula!

### Step 5: Users Install
```bash
brew tap Niteeshkanungo/homebrew-tap
brew install meow
```

## Alternative: Submit to Homebrew Core

If you want to be in the official Homebrew repository:

1. Fork https://github.com/Homebrew/homebrew-core
2. Create a formula file
3. Submit a pull request
4. Wait for maintainer review and approval

The GitHub Actions workflow will automatically create PRs to homebrew-core when you tag releases.

## Testing the Formula Locally

```bash
# Test the formula
brew install --build-from-source Formula/meow.rb

# Or test from your tap
brew tap Niteeshkanungo/homebrew-tap
brew install --build-from-source meow
```
