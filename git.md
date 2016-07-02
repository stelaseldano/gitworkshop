# git


## Part Zero: Intro

### what is a vcs?

* version control system
* software tools that keep track of changes to the source code managed by a single programmer or a team


### git is a vcs

* free and open source, GPL
* created by Linus Torvalds in 2005 for more efficient development of the Linux kernel
* the most widely used vcs today
* tracks changes in files and stores the differences
* changes include file creation and deletion as well


### why is git useful?

* earlier version of the code are accessible
* each developer can make changes to each file without locking
* branching


### branching

* think of them as a way to request a brand new working directory, staging area, and project history
* it possible to work on many unrelated features at the same time
* switching between branches can be done offline



## Part One: The basics

* 	Step 1:
	Installation

	* Windows
	* Linux
	* Mac

*	Step 2:
	Setup

	Do the following:

	$ git config --global user.name "Yout Username Here"
	$ git config --global user.email your_email@email.com
	$ git config --global core.editor preferred_editor



* 	Step 3:
	Create a git-tracked repo

	terminal/cmd

	$ mkdir cats-project
	$ cd cats-project


	**Initialise a repo**
	```
	$ git init
	$ ls .git
	```

	... 
	branches/  config  description  HEAD  hooks/  info/  objects/  refs/
	...

	```
	$ touch README.md
	$ echo "# Cats project" >> README.md
	```

	or

	Open README.md
	On line 1 write "# A project about cats" on line 1.

	**Check what's going on**
	```
	$ git status
	...
	Untracked files:
	README.md
	```


* 	Step 4:
	GitHub

	* go to https://github.com
	* register
	* remember your password, you will need it
	* create a new repository


*	Step 5:
	The connection

	**Tell git to track README.md.**

	```
	$ git add README.md 
	$ git status
	```

	```
	...
	new file: README.md
	...
	```

	**Tell git to take a snapshop of a tracked file**
	```
	$ git commit -m "e.g. First line of code done."
	```

	**Check of everything is Okay**
	`$ git status`

	```
	...
	On branch master
	nothing to commit, working directory clean
	...
	```

	**Connect the repos**
	`$ git remote add origin https://github.com/your_username/cats-project.git`

	**Push to the repo in GitHub**
	`$ git push -u origin master`

	**Go to your GitHub profile and feel content**


* 	Step 6:
	Changes to files

	README.md
	on line 3 add "e.g. This is a project about cartoon cats"

	`$ git status`

	```
	...
	modified:   README.md
	...
	```
	```
	$ git commit -am"e.g. Description added"

	$ git push
	```

	go to GitHub and see the change in the README.md


*	Step 7:
	Adding a new file

	`$ touch GARFIELD.md`

	README.md
	On line 5 add more info e.g. "Cat number 1 is called Garfield"

	GARFIELD.md
	On line 1 add "# Garfield"
	On line 3 add "Description: sleepy and lazy"

	`$ git status`

	```
	...
	modified: README.md

	Untracked files:
	GARFIELD.md
	...
	```

	```
	$ git commit -am "e.g. Garfield"
	$ git push
	$ git status
	```

	```
	...
	Untracked files:
	GARFIELD.md
	...
	```

	`$ git add GARFIELD.md `
	or
	`$ git add --all`
	
	`$ git commit -am "e.g. Garfield file created"`

	Now push the new file to the repo and see the new file in GitHub


*	Step 8:
	Ignoring files

	$ touch NOTES.md
	$ git status

	NOTES.md
	On line 1 write e.g. "Notes about cats others don't need to be bothered with"

	$ touch .gitignore
	
	.gitignore
	On line 1 write NOTES.md

	$ git status
	
	Add the newly created file to the staging area and commit. Don't push yet.

	$ git cherry -v

	Now push


*	Step 9:
	There is always going back

	$ touch SPIKE.md TOM.md

	TOM.md
	Line 1: "I am going to join the cat project"
	
	SPIKE.md
	Line 1: "They will not like my presence in the cat project. Woof"

	$ git add --all
	$ git status
	$ git reset HEAD SPIKE.md

	$ git commit -am"e.g. new cat TOM.md created"

	TOM.md
	Line 3 add "(Cat barking) Woof. Woof"

	$ git checkout TOM.md

	commit, push and see if TOM.md is in the repo

	Short break and then we will talk about working together on a single project.

	Split in groups of two and sit next to each other



## Part Two: Working on a project with git and other human beings.


*	Step 1:
	Initialising and cloning a repo

	Decide who is going to be B1 and who is going to be B2. Peeking at each others' terminals everytime something new happens

	1. B1 goes to https://github.com and creates a new repository called bananas.
	2. B1 makes a new directory (could be called anything, but let's stick to bananas for consistency) and does the following:

		$ git init
		$ touch README.md
		$ echo "# Bananas in Pyjamas" >> README.md
		$ git add --all
		$ git commit -am"e.g. New repo founded"
		$ git remote add origin git@github..
		$ git push -u origin master

	3. B1 invites B2 to the repo (settings - collaborators)
	4. B2 accepts the invitation from GitHub
	5. B2 does the following:

		$ git clone https://github.com...

		'B2 edits the README.md
		On line 3: "Are you thinking what I'm thinking, B1?"

		$ git commit -am "e.g. A questions added"
		$ git push

	6. B1 does:

		$ git pull

*	Step 2:
	

	1. B1 answers

		B1 edits the README.md
		On line 5: "I think, I am, B2"
		
		$ git commit -am "e.g. Question answered"
		$ git push

	2. B2 does:

		$ git pull


*	Step 3:
	Push rejected

	1. Open the README.md in your favourite editor.
	2. B2 adds "B2: " in the beginning of their line and puts the text in quotation marks. (line 3)
	3. B1 adds "B1: " in the beginning of their line and puts the text in quotation marks. (line 5)
	4. both does

		$ git commit -am "e.g. Quotes added"
		
	5. B1 does:

		$ git push

	6. B2 does:

		$ git push
		...
		 ! [rejected]        master -> master (fetch first)
		error: failed to push some refs to 'https://github.com/...git'
		...

	7. B2 does:

		$ git pull
		$ git push

	8. B1 pulls


*	Step 4:
	Merge Conflict

	1. On line 7, both add "It's conflict time!"
	2. B1 adds "B1: " in the beginning of line 7.
	3. B2 adds "B2: " in the beginning of line 7.
	4. Both commit
	5. B2 pushes
	6. B1 pushes
	7. B1 pulls
	...

	...

	'B1 resolves the conflict manually
	7. B1 edits the file by putting his line on line 7 and adding B2's line on line 8 and delete the message
	8. B1 does the following:

		$ git add README.md
		$ git commit
		$ git push

	9. B2 adds "Both: Conflict resolving time!" on line 8
	10. B2 commits
	11. B2 pulls, resloves the conflict, adds the file, commits and pushes
	12. B1 pulls

	There should be no conflict even though you edited the same line. Both should have something like that

	------
	# bananas in pyjamas

	B2: "Are you thinking what I'm thinking, B1?"

	B1: "I think I am, B2."

	B1: "It's merge conflict time!"
	B2: "It's merge conflict time!"
	Both: "Conflict resolving time!"
	------



## Part Three: Branching

### step 1

Branching: Local branches

1. Both do the following:

```
$ git branch lulu
$ git checkout lulu
```

or:

```
$ git checkout -b lulu
```

2. touch LULU.md

```
# Bn meets Lulu

Bn: "Hi, Lulu! How is it going?"
```

```
$ git add LULU.md
$ git commit -am"e.g. met Lulu"
$ git checkout master
```

3. There is no LULU.md on this branch
4. Switch to the lulu branch (git checkout lulu)
5. Add more line to your dialogue with Lulu

e.g.

```
[...]
Lulu: "Hi Bn, very well, where is Bn?"
Bn: "This is my private branch he still doesn't know about."
Lulu: "Ah, I see"
```

6. Do the following:

```
$ git commit -am "e.g. Talked to Lulu"
$ git branch
$ git checkout -b morgan
```

LULU.md:

```
# Morgan meets Lulu

Morgan: "Hi, Lulu! How is it going?"
Lulu: "Hi Morgan, very well, where are the Bananas?"
Morgan: "They are doing branching and merging"
```

8. commit and switch to branch lulu
9. do the following

```
$ git merge morgan
```

Now LULU.md on branch lulu should be the same as LULU.md on branch morgan

```
$ git branch -d morgan
```


### step 2

Branching: Remote branches

Go on branch master

Both:

1. create a branch with your name (e.g. b2)
2. create a .md file and write your message to the other banana
3. add and commit
4. do the following

```
$ git push origin <branch name>
$ git checkout master

$ git branch <new remote>
$ git pull origin <new remote>
```

or

```
$ git checkout master
$ git pull
```



## Part Four: Cheatsheet

initialise a repo

```
$ git init
```

tell your repo which repo to track

```
$ git remote add origin
```

clone a repo

```
$ git clone link_to_repo
```

track a file

```
$ git add <file>
```

track all files in the directory

```
$ git add --all
```

ignore files

* create a .gitignore file
* white the name of the files or directories
* put each name on a new line
* add the .gitignore ($ git add .gitignore) 

take a snapshop of a single file

```
$ git commit -m "Message" path/to/file
```

commit every tracked file

```
$ git commit -am "Message"
```

push them to GitHub fo the first time

```
$ git push -u origin master
```

push them to GitHub

```
$ git push
```

if push is rejected with the message fetch first

```
$ git pull
$ git push
```

get the last version (if sb did a change)

```
$ git pull
```

discard changes to the last commit

```
$ git checkout <filename>
```

move a file back to the unstaged area

```
$ git reset HEAD <filename>
```

resolve a merge conflict

* open the problematic files
* decide what to keep
* make the changes
* delete git's comments

```
$ git add <file>
$ git commit
```

go back to a specific commit

```
git reset --hard <commit_string_name>
NOTE! commits done later than the commit ypu are going back to, will be lost
```

create a branch

```
$ git branch <branchname>
```

move to a specific branch

```
$ git checkout -b <branchname>
```

create a new branch and move to it

```
$ git checkout -b <branchname>
```

check how many branches are there and on which one you are on

```
$ git branch
```

change a local branch's name

```
$ git branch -m <old name> <new name>
```

merge branches

go to the branch the merge is going to be made to

```
$ git merge <branchname>
```

e.g.

```
$ git checkout design
$ git merge new-colour-pallette
```

delete a merged branch

```
$ git branch -d <branchname>
```

delete an unmerged branch

```
$ git branch -D <branchname>
```


check the status

```
$ git status
```

check the last commits 

```
$ git log
```

check the unpushed commits 

```
$ git cherry -v
```

more about git

* https://git-scm.com/doc
* https://www.atlassian.com/git/tutorials/setting-up-a-repository


