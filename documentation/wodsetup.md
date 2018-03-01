#Intellij
CODE STYLE
1. coding style - ics-se-code-style
2. inspection - all unchecked except eslint
3. language ECMAScript6
4. Enable ESLint:
	nodejs path - /usr/bin/nodejs
	eslint path - /usr/local/lib/node_modules/eslint
	eslint option --quiet
5. sample.eslintrc as .eslintrc

/usr/local/lib/node_modules/eslint

git config --global credential.helper cache			#password caching

git config --global credential.helper "cache --timeout=18000"			#password caching

echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p


# deploy to galaxy
DEPLOY_HOSTNAME=galaxy.meteor.com meteor deploy islandwanderer.meteorapp.com --owner ics314f17 --settings ../config/settings.development.json


#create meteor
cd ~/meteor/
cp -a ~/UHDrive/2017Fall_ICS314_SoftwareEngineering/InjelliJ/sample ./test 
cd test
rm index.html
rm style.css
git init
git remote add origin https://github.com/ayushmaskey/test
git pull origin master

idea ../test

meteor create test
mv test/ app
cd app
meteor npm install && meteor run
5wV@PB1lF7!ZwCr$S1kJ



git add .
git commit -m "meteor and idea stuff"
git push -u origin master
git status


ctrl + c		#stop meteor

#create repository on github

cd ~/UHDrive/2017Fall_ICS314_SoftwareEngineering/InjelliJ/
cp -a ./sample ./test 
cd test
git init
git remote add origin https://github.com/ayushmaskey/test
git pull origin master

touch test.js

idea ../test
git add .
git commit -m "initial commit with idea stuff"
git push -u origin master
git status

git add .
git commit -m "second commit"
git push



#create new branch and go to the new branch
git branch branchName
git checkout branchName

#merge to master
git checkout master
git merge branchName

git branch		#show all branches
git add --all		#all branches

simonEngler
keokilee
philipmjohnson
Wv^L!InzIYOp76ZeuwF9S

DEPLOY_HOSTNAME=galaxy.meteor.com meteor deploy testdeployam.meteorapp.com --owner ics314f17 --settings ../config/settings.production.json





