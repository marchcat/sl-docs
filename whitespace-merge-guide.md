# 2024 Consistent Whitespace

## Purpose

The goal of making whitespace consistent across all files is to reduce merge conflicts when pulling changes from LL's canonical upstream into forks. It also makes developers' lives easier as they do not have to deal with files with mixed whitespace. By doing a small amount of work now, future merges will be made simpler. It will also result in a codebase that is less embarrassing and adheres to the [Second Life Coding Standards](https://wiki.secondlife.com/wiki/Coding_standard). Specifically, section 1.1 states that "All text files must use unix (linefeed only) line endings when submitted" and section 2.4.7 requires that "Indentation must use spaces unless the file format requires tabs (Such as in Makefiles), with a default width of 4." Making these changes across the entire codebase will bring it into compliance with these standards.


## Integration

Merging the whitespace changes into your branch is a straightforward process that takes advantage of git's built-in merge strategies. By following the instructions below, you can integrate these changes with minimal or no merge conflicts, making the process smooth and hassle-free.


### Prerequisites

In order to seamlessly merge the whitespace changes into your branch, it should already be up to date with LL's 2024/04/24 [fc71a9c1](https://github.com/secondlife/viewer/commit/fc71a9c1ed96cb1cb97124e3cceabdfa11e1cc75).
Current whitespace changes are located in the [marchcat/w-whitespace](https://github.com/secondlife/viewer/tree/marchcat/w-whitespace) branch, so it should be used until released. If you do this merge after Maint X release, the same should be done with the `main` branch. 


### Instructions

Set up your repository

```bash
# Add the LL upstream remote
git remote add upstream https://bitbucket.org/lindenlab/viewer.git

# Fetch the upstream refs
git fetch upstream

# Verify that you have all changes. This merge command should respond: "Already up to date."
git merge fc71a9c1
```

Now, merge the changes

```bash
# (OPTIONAL) Create a new branch for merge based on master
git checkout master
git pull origin master
git checkout -b spaces-merge

# Merge whitespace changes from whitespace branch
git merge --no-commit --no-ff -Xignore-all-space -Xignore-space-at-eol upstream/marchcat/w-whitespace spaces-merge

# At this point, your merge may have conflicts depending on your viewer. Let's check them
git diff --name-only --diff-filter=U

# If your viewer deleted files which are still present in upstream,
# resolve modify/delete conflicts by removing them. The following is an
# example from Firestorm's delta. Your codebase's changes may vary.
git rm indra/newview/llimpanel.h
git rm indra/newview/llcallbacklist.cpp
git rm indra/newview/llappviewerlinux_api_dbus.cpp
git rm indra/newview/llappviewerlinux_api.h 
git rm indra/linux_crash_logger/llcrashloggerlinux.cpp

# The following script fixes the rest of the files that are not in upstream. 
# Default filter is for the source files only (c, cpp, h, hpp, inl, py, glsl, cmake)
python scripts/code_tools/fix_whitespace.py -d indra

# When ready, add and commit merge
git add .
git commit
```

Congratulations! You have just merged the whitespace changes that follow LL's coding standard, and it was probably easier than expected.

The key to avoiding merge conflicts is the use of the `-Xignore-all-space` and `-Xignore-space-at-eol` merge strategies, so the whitespace changes are ignored while merging. The script also removes trailing spaces, which makes the code a little cleaner.

### Fixing additional branches
You can now use your merged branch to update other branches. This should mean any modify/delete conflicts resolved in the first pass will not need to be addressed again.

```bash
git checkout my-feature-branch
git merge --no-commit --no-ff -Xignore-all-space -Xignore-space-at-eol spaces-merge
python scripts/code_tools/fix_whitespace.py -d indra
git add .
git commit
```


## Notes
This merge also uses an updated [pre-commit hook](https://github.com/secondlife/viewer/commit/a6c89d9185d61027dd761af0c05fdbb05e3692fe) to ensure that no tabs are committed anymore.

Older version of this doc: [2023 Consistent Whitespace](https://wiki.secondlife.com/wiki/2023_Consistent_Whitespace).
