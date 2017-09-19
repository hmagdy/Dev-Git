Git Cheat Sheet
===


## Overview

This doc is mainly for listing all git commands needed on development cycle, So feel free to contribute. 

## VIP git commands
	
	$ git config core.fileMode false
	$ git branch
	$ git branch -a
	$ git branch -r
	
***

- Delete Local Branch

To delete the local branch use:

	$ git branch -d branch_name
or use:

	$ git branch -D branch_name
	
>Note: The -d option is an alias for --delete, which only deletes the branch if it has already been fully merged in its upstream branch. You could also use -D, which is an alias for --delete --force, which deletes the branch "irrespective of its merged status.

***

- Delete Remote Branch

    	$ git push origin --delete <branch_name>

        $ git fetch origin --prune


## New Task on JIRA "UT-X"

You should have only updated 2 braches

     $ git branch 
     * Dev
     * master
     $ git checkout Dev
     $ git pull origin Dev
     $ git branch UT-X
     $ git checkout UT-X
     
Now can start work on that branch ;) ... once Done

     $ git add .
     $ git commit -a -m "UT-26 | HMagdy Git Cheat Sheet"
     $ git push origin UT-X --force


and open MR into Dev.


## Remotes list, add and no push
     $ git remote -v
      origin	git@github.com:hmagdy/Git-Cheat-Sheet.git (fetch)
      origin	git@github.com:hmagdy/Git-Cheat-Sheet.git (push)
      $ git remote add upstream git@github.com:hmagdy/Dev-Bashrc.git
      $ git remote set-url --push upstream no_push



## If you have many commits on your branch
Your branch should contains only one commit with one message that's identical of your JIRA task Id and Title, So if you have many commits you can squash all of them to one as below:


#### List your commits
Always keep up your branch is clear as 
     
#### 1. If you have clear branch

     $ git checkout Dev
     $ git log -3
	┌─ commit 3927ca7f59eac5179188e46be1a31cf5fd4919cf
	│
	│ Author: HMagdy Saad (HMagdy) <hasan.magdy@gmail.com>
	│ Date:   Tue Jul 18 17:07:28 2017 +0200
	│ 
	│     Merge UT-11 into Dev
	└──
	
	┌─ commit 0e6e047e8653decf6054b4032fc9e0800c20b5f1
	│
	│ Author: sabry <eng.ahmed.s.ahmed@gmail.com>
	│ Date:   Tue Jul 18 14:11:47 2017 +0200
	│ 
	│   UT-11/Admins Full CRUD by Easy Admin Bundle
	└──
	
	┌─ commit a5ca4642a039516a7fd62c827dc5a5453ea99c75
	│ 
	│ Author: sabry <eng.ahmed.s.ahmed@gmail.com>
	│ Date:   Tue Jul 18 14:11:47 2017 +0200
	│ 
	│  Clean and merge conflicts
	└──
       $ git checkout UT-26
       $ git status
        On branch UT-26
        nothing to commit, working directory clean
       $ git log -3

	┌─ commit 5a05f4de3a12ae83e75ea8593226877591838bd3
	│
	│ Author: HMagdy Saad (HMagdy) <hasan.magdy@gmail.com>
	│ Date:   Wed Jul 19 17:06:07 2017 +0200
	│ 
	│     UT-26 | XDG Git Cheat Sheet
	└──

	┌─ commit 3927ca7f59eac5179188e46be1a31cf5fd4919cf
	│
	│ Author: HMagdy Saad (HMagdy) <hasan.magdy@gmail.com>
	│ Date:   Tue Jul 18 17:07:28 2017 +0200
	│ 
	│     Merge UT-11 into Dev
	└──
	
	┌─ commit 0e6e047e8653decf6054b4032fc9e0800c20b5f1
	│
	│ Author: sabry <eng.ahmed.s.ahmed@gmail.com>
	│ Date:   Tue Jul 18 14:11:47 2017 +0200
	│ 
	│   UT-11/Admins Full CRUD by Easy Admin Bundle
	└──

now you can push without ay issue
     
       $ git push origin UT-26 --force
       Counting objects: 3, done.
	Delta compression using up to 8 threads.
	Compressing objects: 100% (3/3), done.
	Writing objects: 100% (3/3), 2.07 KiB | 0 bytes/s, done.
	Total 3 (delta 1), reused 0 (delta 0)
	To git@github.com:hmagdy/Git-Cheat-Sheet.git
	 * [new branch]      UT-26 -> UT-26


     
#### 2. If you have dirty branch .. you have to squash


       $ git commit -a -m "ALL"
       $ git log -4

	┌─ commit new id
	│
	│ Author: HMagdy Saad (HMagdy) <hasan.magdy@gmail.com>
	│ Date:   Wed Jul 19 17:06:07 2017 +0200
	│ 
	│     ALL
	└──

	┌─ commit 5a05f4de3a12ae83e75ea8593226877591838bd3
	│
	│ Author: HMagdy Saad (HMagdy) <hasan.magdy@gmail.com>
	│ Date:   Wed Jul 19 17:06:07 2017 +0200
	│ 
	│     UT-26 | XDG Git Cheat Sheet
	└──

	┌─ commit 3927ca7f59eac5179188e46be1a31cf5fd4919cf
	│
	│ Author: HMagdy Saad (HMagdy) <hasan.magdy@gmail.com>
	│ Date:   Tue Jul 18 17:07:28 2017 +0200
	│ 
	│     Merge UT-11 into Dev
	└──
	
	┌─ commit 0e6e047e8653decf6054b4032fc9e0800c20b5f1
	│
	│ Author: sabry <eng.ahmed.s.ahmed@gmail.com>
	│ Date:   Tue Jul 18 14:11:47 2017 +0200
	│ 
	│   UT-11/Admins Full CRUD by Easy Admin Bundle
	└──

       $ git rebase -i HEAD~2
       pick 5a05f4d UT-26 | XDG Git Cheat Sheet
       s 382979b ALL
       
save that file .. then you can set same clear message

       $ git status
       $ git push origin UT-26 --force


Enjoy ;)
