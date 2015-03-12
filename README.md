DWP
===
Deployment of Web Projects

# Creating Basic Server


## Setting Up Server
Login as root

	ssh root@[ipAddress]

Add user

	adduser [userName]
	adduser [userName] sudo

Logout of root and login with new user

	exit
	ssh [userName]@[ipAddress]

Update and Upgrade Package System

	sudo apt-get update
	sudo apt-get upgrade

Update package system after upgrade

	sudo apt-get update

Install Apache2

	sudo apt-get install apache2

Update package system

	sudo apt-get update

Install Git

	sudo apt-get install git-core

Update package system

	sudo apt-get update

Add git username and email

	git config --global user.name "username"
	git config --global user.email email@email.com

Change permissions to /var/www directory

	sudo chown [userName] /var/www

Create another server for production


## Creating Git Hook
Switch to beginning of file system

	cd /

Create directory for repos

	sudo mkdir /var/repos

Change permissions to /var/repos directory

	sudo chown [userName] /var/repos

Switch to repos directory and make a new directory for the page created

	cd /var/repos
	mkdir [pageName].git

Instantiate git

	git init --bare

Switch to hooks directory; separate working tree and git directory locations

	cd [pageName].git/hooks
	nano post-receive

Write in editor

	#!/bin/sh
	GIT_WORK_TREE=/var/www git checkout -f

Save file

Change permissions to post-receive

	chmod +x post-receive


## Pushing to Server

Go to your local git directory (where all files for page are)

Make sure you are in master branch

	git checkout master

Add Stage Server remote

	git remote add [stageServerName] ssh://[userName]@[ipAddress]/var/repos/[pageName].git

Add Production Server remote

	git remote add [productionServerName] ssh://[userName]@[ipAddress]/var/repos/[pageName].git

Check status of files ready to be committed

	git status

Add all files to be committed later

	git add -A

Commit all files

	git commit -m '[Enter message of changes made]'

Push to stage server

	git push [stageServerName] master

Make sure everything is working fine in stage server, test everything, once everything has been tested push to production server

	git push [productionServerName] master

Push all changes to github

	git push
