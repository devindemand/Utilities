# Utilities
This Utility project addresses common requirements and day to day programming needs

Git commands for daily use:

1) go to GitHub.com and fork
2) git clone url -- this is to clone the url
3)cd <directory>
4) git remote add upstream  <upstream url>
     git remote rm upstream -- use this any time if u want to remove an upstream
5) git fetch upstream  -- get latest changes from master / main repo or try git pull upstream master
6) git merge -- this is to merge changes from master to my local


1) run git fetch upstream and git merge before pushing changes
2) git add
3) git commit -m "1) Added regular_2day_S2H_only2day in items_production.json 2) Added test case : Add a S2H Only  item, verify POS [C787067]"
4) git push origin master   -- this pushes to my GitHub account
5) go to github and create a pr

http://10.116.136.77:8080/

Important concepts with GitHub:

Origin -- is my GitHub
Upstream -- is the main repo branch

So we first push to origin using git push origin master

What is GIT cherry-pick? man page
Git cherry-pick allows you to merge a single commit from one branch into another.  To use the cherry-pick command follow these steps:

Check out the branch into which you want to merge the commit. (E.g.: git checkout master)
Identify the commit hash through your favorite method. You can use git log, a GUI tool such as sourcetree or tower, or if you use GitHub or BitBucket you can use their interface. In SWS we use GitHub, so I tend to use that method often. With GitHub you can find the commit hash on the commit list page or on the individual commit page itself.  See the screenshots below. the has is from your git account

Pick'em! eg: git cherry-pick 9638d99c89a92350ad2f205f47af24b81ac39a64
If there is a merge conflict you will have to resolve that with your favorite merge tool, but otherwise you have now successfully pulled in the work from the other branch.







git branch -avv  -- to see all the branches

  git reset --hard upstream/master   -- to force reset your local with changes from master
and then do a git push so all the changes from master will override your changes on fork


git branch --unset-upstream  --> when working on a branch and when our upstream points to master , we don't want to push the changes we made on master to the branch

so we unset upstream

and then we try git push --set-upstream origin release-18-8-4 , so this creates the release-18-8-4 branch on my fork and all local changes get pushed to



   other git -- nice to know

   to clone a branch -- $> git clone -b <branch> <remote_repo>


   git pull upstream homeservice-18-05-31

   git stash -- this will not delete your files , just stash

   to get back stashed files do a git stash pop


   selective stashing ?? stash only one file out of many and then pop that file only ?? how to do it ?


   When we do git remote -v we would know if we have setup an upstream
   m-c02w211rhtdg:checkout-service-commons vn0aifb$ git remote -v
   origin	https://gecgithub01.walmart.com/vn0aifb/checkout-service-commons.git (fetch)
   origin	https://gecgithub01.walmart.com/vn0aifb/checkout-service-commons.git (push)
   upstream	https://gecgithub01.walmart.com/services/checkout-service-commons (fetch)
   upstream	https://gecgithub01.walmart.com/services/checkout-service-commons (push)

   to add an upstream --> git remote add upstream "url of the main repo in quotes"


   git branch -a  --> to list all branches
   git fetch --all -- > to fetch all branches from upstream


   Steps to switch to a branch
     1) git fetch --all
     2) git branch -r. //shows all the branches
     3) git checkout -b release-18-9-1  upstream/release-18-9-1
     4) git branch


     git branch -vv

     to find difference in a file between two branches
     git diff  release-19-2-13 master -- com.walmart.services.checkout.adapter.promise/PromiseServiceRequestResponseUtils.java

     or To get to the compare view on GitHub, append /compare to your repository's path example: https://gecgithub01.walmart.com/services/checkout-service-usgm/compare

     Some nice to know points on Git commands:
     1) never do a git revert if you are not happy with last commit instead use git reset
     git revert creates a new commit in the commit history with new changes , where as git reset simply takes the pointer back

     there are two options with git reset:
     1)git reset --soft,
     2) git reset --hard

     Git reset hard would provide the same workspace and index behavior you would see when you git revert last commit , without all of the associated complications
     git reset soft , the head will move back to a point at a prior commit but none of the files in the working directory will change


     git branch -d release-19-3-6 -- command to delete a branch


     ========================
     Commands to create a release branch

     mvn versions:set -DnewVersion=19.3.6.0-SNAPSHOT versions:commit
     git add . -u
     git commit -m "Cut release-19-3-6.0 branch and update version"
     git push --set-upstream origin release-19-3-6
     git push upstream (instead of this step you can all create a pull request and ask someone to merge)


     ==========================================================


     --- command to remove upstream
     git remote rm upstream



==============

commands to rename a branch

1. Rename your local branch.
If you are on the branch you want to rename:


git branch -m new-name
If you are on a different branch:


git branch -m old-name new-name
2. Delete the old-name remote branch and push the new-name local branch.


git push origin :old-name new-name
3. Reset the upstream branch for the new-name local branch.
Switch to the branch and then:


git push origin -u new-name

=========================
When you think your git is messed up, you can use this command to do everything up-to-date.

git rm -r --cached .
git add .
git commit -am 'git cache cleared'
git push

Also to revert back last commit use this :

git reset HEAD^ --hard
==========================================

> git checkout master
> git pull --rebase upstream master
> git checkout -b release-xxx
> mvn versions:set -DnewVersion=1.0.1.279-AP-SNAPSHOT
> git add . / git commit
> git push origin
> git push --set-upstream origin auto_pilot
> git push upstream auto_pilot
