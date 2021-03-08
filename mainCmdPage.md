<center>

<h1>Git Bash Documentation</h1>

</center>

<a name="clone" href="#"></a>
## Cloning Azure DevOps Remote Repo
```BASH
# Clone Repo w/ the following command
git clone [url]
```

## Checkout Branches
```BASH
# Checking out a different branch after all commits/changes
# have been pushed to the remote repo already or have been
# stashed.
git checkout [Branch Name to Checkout]
```

```BASH
# Checking out a different branch, and not caring if the
# changes are discarded.
git checkout -f [Branch Name to Checkout]
```

## Merging Branches
### Merge Prep Steps
```BASH
# The set of steps within this code block 
# ensures that you do not loseall of your 
# changes in case something goes extremely wrong when
# merging another branches code into yours.

# First do a git pull command to ensure you have all of
# the updated remote repo changes.
git pull

# Then check the status to make sure all applicable changes
# are staged. Ignore any .gz, .dll, .pbz(?), .cache, and 
# .json files you or another developer did not add/change.
git status

# If there are untracked changes you want to keep in case
# the merge goes wrong, do the following:

# Tracks all of the changes made to the branch.
git add . 

# Commits the changes to the local branch to be pushed
# to the branch in the remote repo.
git commit -m "Meaningful message about your changes"

# Check the status again; should state that there are
# no changes and you are ready to push to the remote repo.
git status

# Pushes your commit to your branch in the remote repo.
git push

# Ensure the branch you want to merge code from is
# tracked by checking it out.
git checkout [Branch Name Merging Code From]

# NOTE: If the branch seems as if it checked out, but is
# stated that it is headless in the result message and/or
# it displays a hash number instead of the branch name;
# it wasn't successful. Do the following:
git checkout -f [Some Branch Name You Know Is Tracked; i.e. master or Testing]
git pull
git checkout -f [Branch Name Your Merging Code From]

# Once the steps above are complete; you can be sure that
# the branch you are merging from is tracked, has the
# most up-to-date code that has been pushed to the
# remote repo, and everything is ready to begin the merge
# process.

# Checkout the branch you want to merge the code into.
git checkout [Branch Name Merging Code INTO] 
```
### Merge Process Steps
```BASH
# These are the actual steps for merging another branches
# code into your branch.

# NOTE: You MUST be in the branch you want to merge code
# INTO; NOT the branch you're merging code FROM.

# If there are no changes or after you've pushed changes
# to the remote repo, start your merge as follows:
git merge [Branch Name Merging Code From]

# If you get an error that asks if you meant origin/[Branch Name]. If that happens do the following:
git merge origin/[Branch Name Merging Code From]

# If there are merge conflicts they can be resolved in two
# ways; either using the Visual Studio GUI or the git
# mergetool if you have set it up. To use the git mergetool
# enter the following command:
git mergetool

# NOTE: If all of the merge conflicts come from the type
# of files mentioned in the prep steps above you can
# enter the commands below to have git resolve these
# automatically.
git merge --abort
git merge -X theirs [Branch Name Merging Code From]

# Once all of the merge conflicts are resolved, if you didn't
# finish the merge process in Visual Studio, finish the
# process by entering the command below.
git merge --continue
```

## Create Remote Branch
```BASH
# Create a local branch first
git checkout -b [New Branch Name]

# Push local branch to create the branch in the remote repo
git push -u origin [New Branch Name]
```

## Delete Remote Branch (If You have permissions)
```BASH
# You CANNOT be on the branch you want to delete. If you currently
# are in that branch, checkout any other tracked branch.
git checkout -f [Branch Name of Any Other Branch]

# Preferred Way
git push origin --delete [Branch Name You Want to Delete]

# Delete using the branch tool
git branch -d [Branch Name You Want to Delete]

# Delete using the branch tool if -d fails
# The -D is a shortcut for --delete --force
git branch -D [Branch Name You Want to Delete]

# Delete using the branch tool if -d fails
# and you don't want to use the -D shortcut switch.
git branch --delete --force [Branch name You Want to Delete]

# Finally, update the repo by doing a pull
git pull
```

## Get Branch Commit History
```BASH
git log
```

## Move Back in the History
```BASH
git checkout <first 7 chars of the commit, or full sha number>
```
