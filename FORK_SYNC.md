# Fork Synchronization Guide

This document explains how to sync the `eschatonic-studios/godot-bevy` fork with the upstream `bytemeadow/godot-bevy` repository.

## Repository Structure

- **Fork (Origin)**: `eschatonic-studios/godot-bevy`
- **Upstream**: `bytemeadow/godot-bevy`

## One-Time Setup

If you're working with this fork for the first time, you need to add the upstream remote:

```bash
# Add upstream remote (only needed once)
git remote add upstream https://github.com/bytemeadow/godot-bevy.git

# Verify remotes are configured correctly
git remote -v
# Should show:
# origin    https://github.com/eschatonic-studios/godot-bevy (fetch)
# origin    https://github.com/eschatonic-studios/godot-bevy (push)
# upstream  https://github.com/bytemeadow/godot-bevy.git (fetch)
# upstream  https://github.com/bytemeadow/godot-bevy.git (push)
```

## Sync Process

To sync the fork with upstream changes:

### Step 1: Fetch Latest Changes

```bash
# Fetch all changes from upstream
git fetch upstream

# Optionally, also fetch from origin to get latest fork changes
git fetch origin
```

### Step 2: Update Main Branch

```bash
# Switch to main branch
git checkout main

# Reset main branch to match upstream main exactly
git reset --hard upstream/main

# Alternative approach (creates merge commit if there are differences):
# git merge upstream/main
```

### Step 3: Push to Fork

```bash
# Push the synchronized main branch to your fork
# Note: Use --force only if you're sure about overwriting fork history
git push origin main --force

# Or use --force-with-lease for safer force pushing
git push origin main --force-with-lease
```

## Last Sync Information

- **Last Sync Date**: December 19, 2024
- **Last Sync Commit**: `a5f0f60` (chore: update benchmark baseline from CI [skip ci])
- **Commits Synced**: 2566 objects including multiple new branches and tags

## Verification

To verify the sync was successful:

```bash
# Check that local main matches upstream main
git log main upstream/main --oneline -5

# Both should show the same commits
# Verify main is tracking upstream
git branch -vv
```

## Branch Management

After syncing main:

1. **Update feature branches**: Rebase or merge your feature branches onto the new main
2. **Clean up**: Remove any branches that were merged upstream
3. **Update dependencies**: Check if any Cargo.toml or package files need updates

## Automated Sync (Recommended)

Consider setting up a GitHub Action or script to automatically sync the fork weekly or on new upstream releases.

## Troubleshooting

### Authentication Issues
If you get authentication errors when pushing:
- Ensure you have appropriate permissions for the fork repository
- Use a personal access token instead of password authentication
- Check that your Git remote URLs are correct

### Merge Conflicts
If there are conflicts during merge:
```bash
# Reset to known good state
git reset --hard upstream/main
# Then force push (this will lose fork-specific changes)
git push origin main --force
```

### Divergent Histories
If fork and upstream have completely different histories:
```bash
# Replace fork main with upstream main completely
git checkout -B main upstream/main
git push origin main --force
```

## Contact

For questions about this fork or sync process, check the fork repository issues or contact the fork maintainers.