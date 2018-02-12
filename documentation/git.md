git config --global credential.helper cache		#password cache for 15 min

https://try.github.io/levels/1/challenges/1
git init				# intialize git repostory
git status				# currennt status of project
git add octocat.txt			# add the txt file to staging area
git commit -m "message"			# commit file(s) in staging area
git add '*.txt				# add all txt files to staging area
git log					# history of all commit

git remote add origin https://github.com/ayushmaskey/test	# add to remote repo with name origin

git push -u origin master		#push from master (default name of local) to origin (remote) -u rememebers this setting

git pull origin master			#pull from origin to master (if others have push to origin)
.

git diff HEAD				#difference from our last commit to one we pulled today
git add octofamily/octodog.txt		#add file to staging
git diff --staged			#changes that are staged
git reset octofamily/octodog.txt	#unstage file from staging area
git checkout -- octocat.txt		#put back things like they were
git branch clean_up			#create branch/copy of the repo to work on
git branch				#shows all branches and highlights active branch
git checkout clean_up			#move to different branch
git rm '*.txt'				#remove all txt files from this branch
git merge clean_up			#all changes in branch clean_up into current branch
git branch -d clean_up			#delete branch of done with it
git branch -D clean_up			#without merging

git push				#send all changes to remote repository. -u origin master remembered earlier changes
.


git reset --hard HEAD			#reset to last commit

**********************************************************************
https://www.howtoforge.com/tutorial/install-git-and-github-on-ubuntu-14.04/ 
http://datastructur.es/sp16/materials/lab/lab1/lab1.html

download and install git:
sudo apt-get install git

Configure:
git config --global user.name "amaskey"
git config --global user.email "maskey.maskey@gmail.com"


local repository
git init FoldeName
git init withoutFolderName


add to index
git add FILE/FOLDERNAME
git add '*.txt'


remove from index
git rm --cached FILENAME
git rm --cached FOLDERNAME -r

check status
git status
git log
git show

git reset HEAD --hard

commit
git commit -m "message"

send to github
git remote add origin https://github.com/amaskey/JavaFXProject.git
git remote add origin https://github.com/try-git/try_git.git
git push -u origin master

.



