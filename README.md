# README #

This README is a note that I wrote when I learned about Git. I just recorded the necessary knowledge for me.

# What is this repository for? #

* Quick summary about GIT
* Learn at: https://www.lynda.com/Git-tutorials/Git-Essential-Training/100222-2.html

# 1. What is GIT? #
- Keeps track of the change, especially text changes
- VCS (Version control system)
- Source code management

## History of GIT
- Source Code Contronl system (SCCS)
- Revision Control System (RCS)
- Concurrent Version System (CVS)
- Apache Subversion (SVN)
- BitKeeper SCM : proprietary
- Git is born (2005)
## Distributed version Control
## Git Bash
- Bash is an enviroment in UNIX
- ls -la: list files
- git --version:
# 2. Installing Git
## Configuring Git
- 3 places GIT are stores: System, User, Project
- git config --list : list all config currently visible (in the current directory)
- cat .gitconfig: work in your home directory, show content of the file .gitconfig
- git config --global core.editor "notepad.exe" : set editor default
- git config --global color.ui true
# 3. Getting started
## Commit messages
- 2 parts:
   + single-line sumary (<=50 chars), title : what it does, Ex: This fixes a bug
   + complete description(<=72 chars)
- Present tense
- Can use bullet points ( * and - )
## Viewing commit log:
- git log -n : show n commit logs  in the past
--util=yyyy-mm-dd
--author=""
--grep="abc" : find messages that includes "abc"
# 4. GIT concepts and Architecture
3 trees: repository, staging index, working directory
## GIT workflow
## Using hash value (SHA-1)
- Git generates a checksum for each change set
	+ checksum convert data into simple number
	+ same data -> same checksum
- data integrity is fundamental
	+ data changes -> checksum changes
- Git uses SHA-1 to checksum
 	+ 40 chars hexa
- parent commit : before commit
## HEAD pointer
- point to the last commit
- when create a new branch, HEAD point to new branch
- when check out another branch, HEAD point to the last commit of that branch
- HEAD is pointing where : cat HEAD
# 5. Making changes to files
## Adding files
- When add new file, that file is untracked. So I will "git add <name file>" to add file to staging index.
- git reset HEAD <file> to unstage: untracked file
## Editing files
- git diff: difference between old file and new file, between working tree and staging index
- git diff --staged: difference between staging index and repository
- git rm <file name>: delete file from staging
## Renaming and moving files:
- when I rename a file in working tree, I use command: git add <new-file>, git rm <old-file> to rename file in staging index
- I can use command: git mv <old-file> <new-file> to rename
## git commit -am "" : git add . + git commit -m
- Don't show specific each file.
# 7. Undoing Changes
## Undoing working directory changes
- git checkout <file_name> : when I modified a file, haven't added into staging index (git add *), I can undo this file.
- git checkout <branch_name> : switch to branch name
## Undoing Staging:
- git reset HEAD <file_name> : just undo staging, if you want to undo working, you can do git checkout <file_name> command
## Amending commits:
- When I commited to local rep, I want to modify on this commit:
git commit --amend -m <new commit message>
## Reverting commits:
- git revert <a part of SHA commit> :  undo commit has SHA, just revert on local rep.
## Using reset to undo many commits:
- git reset
	+ soft: just move HEAD pointer, don't change staging index and working directory
	  git reset --soft <SHA commit>
	+ mixed (Default) : move HEAD pointer, change staging index match to rep, don't change working
	+ hard: move HEAD pointer, change both staging index and working.
## Git clean:
- Remove untracked files from working tree.
- git clean [-d] [-f] [-i] [-n] [-q] [-e <pattern>] [-x | -X] [--] <path>…​
 + d : remove untracked directories
 + f (--force) :
 + i (--interactive) :
 + n : show files/dirs woule be removed
 + q (--quiet) : just show error clean, not clean successlly.
 + e
 + x : remove untracked files
 + X : remove ignored files
# 8. Ignore files
## Ignoring files:
- Use project/.gitignore
- Basic regular expression
- Negate expression with !
Ex: !index.php : do not ignore file index.php
*.php : ignore all files that has extension is .php
- Ignore all file in the dir with trailing slash
- Comment line start with #, blank lines are skipped
Step by step
- Create file .gitignore in root dir my PRoject
	+ in Window: echo "" > .gitignore
	+ In LINUX : nano .gitignore
- Add rule into .gitignore file => save
## Ignoring files global
- Ignore file in all repositories
## Git ignore empty directories
# 9. Navigating the commit tree
## Referencing commits
 - moveTree-ish: part of the tree, full or short SHA-1 hash (at least 4 characters)
 - List a tree: git ls-tree HEAD/master
 - List a tree-ish: git ls-tree HEAD/master <tree-ish>
   Ex: git ls-tree HEAD images/
 - blob: file
 - tree: directory
 - Parent commit: HEAD^, master^, 3q66yg6e^, HEAD~, HEAD~1
 - Grandparent commit: HEAD^^, master^^, 3q66yg6e^^, HEAD~2
 - Great-grandparent commit: HEAD^^^, master^^^, 3q66yg6e^^^, HEAD~3
## Getting more from the commit log:
 - git log --oneline -n
  n: number of just commits
  oneline: show one commit in one line
 - git log SHA-1..SHA-1
 - git log -p : show detail the changes.
 - git log --graph --decorate --all
##Viewing Commits:
 - git show <SHA-1 hash of commit> : show detail commit
## Comparing commits:
 - git diff <SHA commit 1>..<SHA commit 2> <file_name> : difference between commit1 and commit 2 in file_name
 - git diff <SHA commit> : difference between this commit and your current rep
 - git diff --stat --summary
# 10. Branching
## Branching overview
 - Try new idea with new branch
 - Isolate features or sections of work
 - Many branches but just one working directory.
 - When I switch to new branch, change files or directories and commit to this branch, but master branch no change
 - I can switch back and forth between master and new branch
 - When I switch to new branch, HEAD point to lasted commit, same as master branch. When I have a new commit on new branch, HEAD point to new commit.
## Viewing and creating branch:
 - git branch: view all branches in my local repository.
 - git branch <name_branch> : create new branch
 - git checkout <name_branch> : switch to another branch
## Switching branches: git checkout <name_branch>
## Creating and switching new branches: git checkout -b <new_name_branch>
## Switching branches with uncommited changes:
 - Need to commit or stash changes before switch branch, because the changes will lose if I switch branch with uncommited changes.
## Comparing branches:
  - git diff <name_branch_1>..<name_branch_2> : difference between 2 lasted commit
  - git diff --color -word <name_branch_1>..<name_branch_2>
## Renaming branches:
  - git branch -m/--move <old_name_branch>..<new_name_branch>
## Deleting branches:
  - git branch -d/--delete <name_branch>
  - Can't delete branch that I am currently on.
  - If you want to delete the branch is not fully merge, use git branch -D <name_branch>
## Configuring the command prompt:
# 11. Merging branches:
## Merging code:
 when I want to merge branch A into branch B,
   - Firstly: git checkout B
   - Secondly: git merge A
## git branch --merge:
- Only list branches whose tips are reachable from the specified commit (HEAD if not specified).
- Only list branches that merged into that branch.  
## Fast-forward merges with real merges:
- fast-forward: don't make new commit to merge those two together.
- git merge --no-ff <name_branch> : forces Git to create commit merge anyway.
- git merge --ff-only <name_branch> : just do fast-forward merge
## Merge conflicts:
- Conflicts occurs when there are 2 change to the same line or set of lines in 2 different commits.
## Resolving merge conflicts
 - abort merge: git merge --abort
 - resolve the conflicts manually
 - use merge tools : git mergetool --tool=<name_tool>
## Strategies to reduce merge conflicts
 - keep lines short
 - keep commits small and focused
 - beware stray edits to whitespace
 - merge often
 - track changes to master
# 12. Stashing changes
## Saving changes in the stash:
- Stash: place store changes temporarily without having commit them to the repository. Stash isn't part of the rep, the staging index, working directory. It's a special fourh area in Git, seperate from the others.
- git stash save "message"
## Viewing stashed changes: git stash List
- stash@{<number>} : On branch name : message
- git stash show <name_stash>: view detail of stash
- git stash show -p <name_stash>: view detail of stash, patch: code changes
- Ex: git stash show -p
## Retrieving stashed changes:
- git stash pop <name_stash>:
- git stash apply:
- both them will put stash out, put it in working directory. pop: removes the difference from the stash. apply: stash leave a copy there
## Deleting stashed changes
- Delete one stash: git stash drop <name_stash>
- Delete all stash: git stash clear
# 13. Remotes:
## Using local and remote repositories:
- local rep: not share anyone
- Remote repositories: take change and put them on remote server, so other people can see them. They can download the changes, make changes, upload back to the remote server, and we can pull back down into our repository to get their changes.
- When I make changes in local rep, I push my changes up the remote server. The remote create the same branch with the same commits, at that point my collaborators can see my commits. At the same time, Git makes another branch on our local computer that is typically called "origin slash".
- origin/master is a branch on our local machine that references the remote server branch, and it always tries to stay and sync with that.
- We make some more commits on our master branch => push (push code up to the remote server) => git makes note of the change in our origin/master branch.
- Other people make changes to the remote => we need to "pull" those changes down, we do that with "fetch". We fetch the change => they come into our origin master branch => we do a merge.
## Setting up a GitHub account:
## Adding a remote repository:
- git remote: list all remote
- git remote add <alias> <url>: create a new remote that points to that remote server at that URL.
- 1 project can have many remote
- git remote -v : show little more information.
- git remote rm <name_remote> : remove remote
## Create a remote branch:
- Push code up remote:
	git push -u <alias> <name_branch>:
	Ex: git push -u origin master
## Cloning a remote repository:
- git clone <URL_Https>
- If repo are exists, git clone <URL> <new_repo>
## Tracking remote branches:
- Checking out a local branch from a remote branch automatically creates what is called a "tracking branch" (or upstream branch). Tracking branches are local branches that have a relationship to a remote branch.
- If you on a tracking branch and type "git push" or "git pull", Git automatically knows which server to push and server to fetch and branch to merge into.
- git checkout -b [branch] [remotename]/[branch]
	shorthand: git checkout --track [remotename]/[branch]
## Pushing changes to a remote repository:
- git push origin master
## Fetching changes from a remote repository:
- git fetch: when remote has changes, I have t fetch to origin/master sync with remote.
- Should:  
	+ Fetch before work
	+ Fetch before push
	+ Fetch often
## Merging in fetched changes:
- git merge origin/master: merge origin/master branch into master branch in working directory.
- Fetch => merge
- git pull = git fetch + git merge
## Checking out remote branches:
- git branch -r
## Pushing to an updated remote branch:
- fetch => merge => push
## Deleting a remote branch:
- git push origin --delete [branch_name]
## Enabling collaboration:
- Issues: the problem or the feature and maybe has even started a discussion about it.
## Collaboration workflow:
- My work
+ git checkout master
+ git fetch
+ git merge origin/master
+ git checkout -b <new_branch>
+ git commit -am "new commit"
+ git fetch
+ git push -u orign <new_branch>
- My collaboration's work:
+ git checkout master
+ git fetch
+ git merge origin/master
+ git checkout -b <new_branch> origin/<new_branch>: create and switch to new_branch from origin/<new_branch>
+ git log
+ git show <new_commit>
+ git commit -am "modified..."
+ git fetch
+ git push
# 14. Tools and Next Steps
## Setting up aliases for commom commands
+ git config --global alias.<alias> "command"
	Ex: git config --global alias.st "status"
## Using SSH keys for remotes login:
- Checking exists SSH key: ls -al ~/.ssh
- Generating a new SSH key:
	+ Open Git Bash
	ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
	+ Enter a file in which to save the key (/c/Users/you/.ssh/id_rsa):[Press enter]
	+ Enter passphrase (empty for no passphrase): [Type a passphrase]
	+ Enter same passphrase again: [Type passphrase again]
- Adding your SSH key to the ssh-agent:
	+ Ensure the ssh-agent is running: eval $(ssh-agent -s)
	+ ssh-add ~/.ssh/id_rsa
- Adding a new SSH key to your GitHub account:
	+ Copy the SSH key to your clipboard: clip < ~/.ssh/id_rsa.pub
	+ Settings=> SSH and CPG keys => New SSH key or Add SSH key => fill Title and paste key => Add SSH key
## Exploring integrated development enviroments
+ TextMate
+ Vim
## Exploring graphical user interfaces
+ GitWeb:
+ GitHub
+ SmartGit
## Understanding Git hosting
+ GitHub
+ Bitbucket
+ Gitorious
Git Self-Hosting: Gitosis, Gitolite

------- Thank for reading! -------
------------- The end ------------
rebase:
submodule
cherrypick
