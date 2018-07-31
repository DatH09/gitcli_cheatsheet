# gitcli_cheatsheet

```
git pull origin master = git fetch + git merge
	origin: remote repository
	master: branch of remote repository
	check remote repo: git remote -v
	check branch in remote repo: git branch -a
```

## A. Git configuration
- Open Git Bash/Git CMD

- Check git version
`$ git --version`

- Set your name, email in Git
```
$ git config --global user.name <Your Name>
$ git config --global user.mail <Your Mail>
```

- Set line-ending behavior for OS:
`$ git config --global core.autocrlf true`

- Show current config:
`$ git config --list`

## B. Git Operation
### 1.Create the Remote Repository on GitHub

- Login acc in github.com, In the upper right corner, next to your avatar or identicon, click + and then select "**New repository**"
	- Set a GitHub Pages Theme
		1.	In your newly created repository, click the Settings tab
		2.	Scroll down to the GitHub Pages section.
		3.	Click Choose a theme.
		4.	Decide which theme you would like to use, and click Select theme

- Clone the Remote Repository to local:
	`$ git clone <URL>`

- Check status of repository and files: 
```
git status allows us to see the status of the files on our branch at any given time
	$ git status
```
- Summary:
```
1. In GitHub page Navigate to your repository’s Code tab.
2. Click "Clone or download" to view URL:
Use Git or checkout with SVN using the web URL: https://github.com/DatH09/hello-world.git

3. Open Git Bash, cd to desired directory:
	$ cd /where/to/store/git
	$ git clone <URL>
	GitHub Login page account login
	when clone done, cd /<Repository-Name>
	$ git status
```

### 2. Create Local Branches With Git and switch branch

- Create Local branch:
	`$ git branch <Branch-Name>`

- Check status:
	`$ git status`

- Check out to switch new branch:
	`$ git checkout <Branch-Name>`

- Check all branch of repository:
	`$ git branch -a`

### 3. Make Local Changes With Git

- **Make change in your local repository**

### 4. Add Local Commits With Git

```
File's status: 
No new File ---New file---> Untracked ---add to stage--> Unmodified/Staged ---Edit--> Modified -*-> Discard changes
		^													|	  ^					    |				 ^
		|													|	  |					    |				 |
		|												    \/	   --add to stage------- 				 |
		 -----------add to stage-------------------------Deleted ----------* :"checkout -- <file>"------->
```

![File Status](https://raw.githubusercontent.com/DatH09/gitcli_cheatsheet/master/Git_FileStatus.png)

File Status | Explaination
------------| ------------
**Untracked files** | New file create
**Unmodified/Staged** | after add new file to staging area
**Modified** | modify the new file already added to stage area
**deleted** | delete the file in status Unmodified/Staged

- Add your file to the staging area/ index (intermediate area)
	`$ git add <File Name>`

- To unstage a file:
	`$ git reset HEAD <file>`

- Discard change when modify or delete the staged file:
	`$ git checkout -- <file>`

- Commit to local repository:
	`$ git commit -m "Your Message"`

- Show git log of commit:
	`$ git log`

### 5.Open a Pull-Request on GitHub
#### Overview

**- Yêu cầu được ghép code vào nhánh chính: yêu cầu này chính là pull request.**

**- Pull request là một yêu cầu gửi tới quản trị viên kho chứa từ xa gộp commit mới được tạo ra từ nhanh my_feature về nhánh master để các lập trình viên khác có thể pull về được.**

- After local commits, it is time to:
	- send your changes to the remote copy of your repository on GitHub.com
	- create a Pull Request

================================================

- Push your commits to the remote, and set a tracking branch
```
 $ git push -u origin <BRANCH-NAME>
  ** -u or --set-upstream: For every branch that is up to date or successfully pushed, add upstream (tracking)reference**
 ```
CMD Component | Explaination
------------- | ------------
origin | remote repository
master | branch of remote repository

> check remote repo: **git remote -v**

> check branch in remote repo: **git branch -a** 

- Create a Pull-Request in **github.com**
 	Click the  "**Pull Request**" tab, then from the Pull Request page, click the green "**New pull request**" button
 	In the "**Comparisons**" box, select the branch you made to compare with base: master (the original).
 	click the big green "**Create Pull Request**" button.

#### Remote repository
- Configure a Remote for the Fork
	- **Remote repositories make it possible for you to collaborate with others on a Git project**
- Check remote server have configured:
```
	$ git remote -v
```
> Output\
	origin  https://github.com/your-username/forked-repository.git (fetch)\
	origin  https://github.com/your-username/forked-repository.git (push)

- Specify a new remote upstream repository for us to sync with the fork
```
   $ git remote add upstream https://github.com/original-owner-username/original-repository.git
   $ git remote -v
```
> Output\
		origin  https://github.com/your-username/forked-repository.git (fetch)\
		origin  https://github.com/your-username/forked-repository.git (push)\
		upstream    https://github.com/original-owner-username/original-repository.git (fetch)\
		upstream    https://github.com/original-owner-username/original-repository.git (push)


### 6. Merge Your Pull-Request on GitHub///----

- Merge branch to master
```
	$ git merge <Branch Name>
```
- Deal with merge conflict
```
PC@DatHoang MINGW64 /C/Users/PC/Desktop/git_practice/hello-world (master)
	$ git merge conflict_test
	Auto-merging README.md
	CONFLICT (content): Merge conflict in README.md
	Automatic merge failed; fix conflicts and then commit the result.
```

- After the conflict noti, check the conflict file then fix
```
	$ cat README.md
	# hello-world
	test hello-world
	
	This is definitely a test
	<<<<<<< HEAD
	line 2 in master branch, this will lead to conflict issue
	=======
	On branch conflict_test
	nothing to commit, working tree clean
	>>>>>>> conflict_test
```

- After fix, **_git add, git commit, git push_** as normal

### 7.Revert to commit code in local repository
- Switched to branch want to revert commit
```
	$ git checkout <BranchName>
```

- Show git log to check the HEAD number: HEAD~0: newest commit
```
	$ git log
```
> Output\
	commit aba133d882499e6700acaa95cb85a4ecfd8f019b (HEAD -> conflict_test2)\
	Author: Mr.D <dath@castis.com>\
	Date:   Tue Jun 26 14:11:00 2018 +0700\
    Add line 1 master branch\
    <br>
	commit 20372a962f94b7b711f6f17e8d15909bb82ecb0b (origin/conflict_test2)\
	Author: Mr.D <dath@castis.com>\
	Date:   Tue Jun 26 13:43:30 2018 +0700\
	<br>\
    This is conflict_branch test 2\
    <br>\
	commit e78d0a35133e0fdded5f816d8ac6bdd3303059b9 (origin/master, origin/HEAD, master)\
	Author: Mr.D <dath@castis.com>\
	Date:   Tue Jun 26 13:36:18 2018 +0700\
	<br>\
    make conflict in master branch\
    <br>

- Revert to desired commit:
```
	$ git reset --hard HEAD~1
```
> Output\
	 &nbsp;&nbsp;HEAD is now at 20372a9 This is conflict_branch test 2



### 8.Git Stash
#### Scenarios

**You want to switch branches for a bit to work on something else. The problem is, you don’t want to do a commit of half-done work just so you can get back to this point later. The answer to this issue is the git stashcommand.**
------

- Add stash your undone working:
```
	$ git stash push –m <message>
```
- Show list of stash:
```	$ git stash list
```
> Output\
	stash@{0}: On conflict_test2: modify: test message\
	stash@{1}: WIP on conflict_test2: 71006e6 Add line 2 conflict branch

- ReApply the stash:
```	$ git stash apply stash@{0}```
