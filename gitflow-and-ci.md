# Intro
This page contains general information about Gitflow and CI processes in our repos.


# Gitflow

* In project repo we have a master (or main) and development branches
* Master contains stable code of latest App version.
* Development contains new code for the next App release.
* Development is a default branch, from which you can create branches for your tasks.


# How CI configured

* All commits from the master branch will produce production build & deployment.
* All commits from development and other branches will produce development build & deployment.
* In CircleCI every new commit will create a new job, that will have "On Hold" status.
* To start the build & deployment process for a specific job you need to "Approve Job" manually.
