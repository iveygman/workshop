# Let's Git Together - A Tale of Commitment

## ABOUT US - Underlying Concepts

### Git
- A version control tool
- Alternatives include SVN and CVS

### GitHub
- A company that acts a host in the cloud
- Alternatives include Bitbucket (Stash) and GitLab

### Commits
- Git is all about commit hashes
- Branch names are just pointers/references to commit hashes
- One commit hash could have multiple branch alias, but every commit must have a unique hash

## TERMS & CONDITIONS - Terminology

- Local: your local drive (computer)
- Remote: on the server, aka GitHub
- Branch: an alias which points to series of commits in one line of development
- Upstream: the remote counterpart of your local branch
- Top of tree: the most recent commit of your master
- Tracked file: a file that Git versions
- .gitignore: a list of files/folders/patterns that should never be tracked, such as tokens, auth keys, binaries (images, executables, etc.)
- HEAD - the commit/position on which you are locally
- HEAD^ or HEAD~1 - one commit before, aka the parent of, your current position
- HEAD^^ or HEAD~2 - two commits before, aka the grandparent of, your current position*
- Detached HEAD - your current position that is not the most recent commit

\* HEAD^^ and HEAD~2 might not always point to the same commit. If you need to refer to a commit more than 2 generations before, it’s better to look up the unique commit hash.

## SIGNING UP - Getting Started

### Forking and Cloning
- Log into your Github account.
- Go to `https://github.com/antoniawang/workshop` and click the `Fork` button in the upper right. Follow the directions to Fork the workshop to you repo.
- Migrate to the folder where you want to house this workshop’s repo files (this folder will be the parent directory). Follow the instuctions to clone: `git clone <YOUR-GITHUB-REPOS-URL>`.
- `cd` into `git_workshop`.
- Do a `git status` to make sure everything is where you want it.
- If you messed up, you can do `rm -rf .git` to “un-git”

### Starting from Scratch (unlikely)
- If you wanted, you can also start by creating some files in a local folder: `git init`


## THE DATING GAME - Adding and Committing
### Basics
- Create a file called `helloWorld.txt` and open it in your preferred text editor. Hint: useful commands are `touch` and `open`.
- Write the line “Hello World!” and save the file.
- Do `git status` and you should see a message about `helloWorld.txt` being an untracked file.
- Let's track it: `git add helloWorld.txt`. Do another `git status` and you should see `helloWorld.txt` is staged for commit.
- Now commit your changes and use the `-m` option to add a message: `git commit -m “created helloWorld”`

**********************************************************




## MULTIPLE PERSONAS - Branching
- Show all you branches: git branch 
- Create a new branch: git branch <new_branch_name>
- Switch to a branch: git checkout <branch_name>
- Creates new branch and switch to that branch: 
- git checkout -b <new_branch_name> 
- List all the remote branches: git branch -r 
- Delete the local copy of your branch: 
- git branch -D <name_of_branch>



## PLAYING THE FIELD - Stashing
You want to mess around without any commitments? Stash it!
1. Make a change
2. Test it out
3. It sucks, but I want keep it on the side? git stash
Each of your stashed changes gets added to a stack
- To retrieve your most recent stashed change: git stash pop (repeat until your stack is empty)
- To see what is at the top of your stack: git stash show

## GETTING SERIOUS AND SETTLING DOWN - Making It Permenant

### Sending Your Branch to the Remote
- Push your branch to the remote: git push -u origin <new_remote_name> 
- This creates remote upstream of your local branch
- Usually, your new remote name should be the same as your local branch name

### Merging
1. Always test changes before you merge - a Continuous Integration (CI) system
2. Go back to your master branch: git checkout master
3. Update your local master to the remote Top of the Tree:git pull origin master 
4. Has master changed? - if yes, you’ll need to rebase
5. Otherwise, merge and see on which commit the merge occurred: git merge --no-ff <new_branch_name>
6. Complete merge by following instructions on the screen

## COUNSELING AND CONFLICTS - Fixing the Kinks

### Rebasing

#### Before you rebase:
- Good practice: always rebase your branch on master before merge
- Go to your local branch: git checkout <new_branch_name>
- Download and update your new remote references (commits): git remote update --prune

#### So what does rebase do? 
- It picks a new starting point for your branch, e.g. master (or any commit), then replays/applies all your branch’s commits, in commit order (oldest first), on that new starting point
- Rebasing my local branch on the remote master: git rebase origin/master
- That line is the equivalent of executing these 4 lines:
1. git checkout master
2. git pull origin master
3. git checkout new_branch_name
4. git rebase master
-Ideally, you’ll see a bunch of “applying” messages and all ends well.

### Still having conflicts?

#### Oops! You still conflicts
- Use the git mergetool to help resolve changes
#### What if you need changes from someone/where else?
- On your current branch: git cherry-pick <some_commit_hash>
- Be careful as cherry-picking could may create conflicts

### The Blame Game

#### Finding a scapegoat
- To get the logs from the HEAD to the branch point off of master and down to beginning of history chronologically: git log 
- To see the logs in an text format showing relations of branches, commits and merge points: git log --graph
- Show the history for a particular file: git log <some_file>
- To show who made the last commit for each line of code: git blame <some_file>

## BREAKING UP IS (NOT) HARD TO DO

### It’s not you. It’s me.

#### Undoing you local changes
- Un-”add” files staged for commit: git reset 
- Blow away local changes on your local current branch to a commit hash: git reset --hard <commit_hash> 
-- Be careful using this, but can be applicable to CKVM
-- Examples: 
--- git reset --hard HEAD~2
--- git reset --hard origin/master

#### Let’s just undo one little thing
- To undo one particular commit: git revert <commit_hash>
- This command creates another commit which is the inverse of (cancels out) that particular commit hash 
- The older the commit you revert, the more dangerous it is
- This command won't work on a commit that is a merge commit (e.g. generated by git merge --no-ff). 

### No, I lied. It's actually you.

#### Erasing your online profile completely
- WARNING: VERY DANGEROUS
- Be wary if someone tells you to do this
- Blow away your remote reference and sets them to your new local: git push -f origin <new_branch_name>
