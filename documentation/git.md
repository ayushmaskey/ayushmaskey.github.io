# git

## configure
```git
git config --global user.name "amaskey"
git config --global user.email "maskey.maskey@gmail.com"
## password cache for 15 min
git config --global credential.helper cache
```

## intialize git repostory
```git
git init
```

## add
```git
git add octocat.txt
git add '*.txt
git add .
git add FILE/FOLDERNAME

# add to remote repo with name origin
git remote add origin https://github.com/ayushmaskey/test
```

## commit file in staging area
```git
git commit -m "message"
```

## check status
```git
git status
git log
git show
```

## push
```git
# push from master (default name of local) to origin (remote) -u rememebers this setting
git push -u origin master
git push
````

## pull from origin to master (if others have push to origin)
```git
git pull origin master
git pull
git pull https://github.com/ayushmaskey/ayushmaskey.github.io.git
```

## branch
```git
#create branch/copy of the repo to work on
git branch branchName

#shows all branches and highlights active branch
git branch

#delete branch of done with it
git branch -d branchName

#without merging
git branch -D branchName

#remove all txt files from this branch
git rm '*.txt'
```

## checkout to different branch
```git
#put back things like they were
git checkout -- fileName.txt

#move to different branch
git checkout branchName
```

## all changes in branch clean_up into current branch
```git
git merge clean_up
```

## diff
```git
#difference from our last commit to one we pulled today
git diff HEAD

#changes that are staged
git diff --staged
```

## reset
```git
#unstage file from staging area
git reset octofamily/octodog.txt	

#reset to last commit
git reset --hard HEAD
```

## remove from index
```git
git rm --cached FILENAME
git rm --cached FOLDERNAME -r
```



