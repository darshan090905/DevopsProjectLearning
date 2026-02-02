# Git Branching and Stash Task Documentation

## Task Description

The objective of this task is to demonstrate practical knowledge of Git branching and stash by performing the following steps.

### Task Performed

1. Created a Git working directory with `feature1.txt` and `feature2.txt` in the master branch  
2. Created three branches: `develop`, `feature1`, and `feature2`  
3. In the develop branch, created `develop.txt` without staging or committing it  
4. Stashed the `develop.txt` file and switched to the `feature1` branch  
5. Created `new.txt` in the feature1 branch, staged and committed it  
6. Switched back to the develop branch, unstashed `develop.txt`, and committed it  

This task was performed using Git command-line operations.

## Commands Used to Perform the Task

First, a project directory was created and Git was initialized.

```bash
mkdir git-task
cd git-task
git init

In the master branch, two files were created and committed.

touch feature1.txt feature2.txt
git add .
git commit -m "Added feature1 and feature2 files"

Three branches were created for development and features
git branch develop
git branch feature1
git branch feature2

The develop branch was checked out and a file was created without committing
git checkout develop
touch develop.txt

The uncommitted file was stashed to save unfinished work.
git stash

The feature1 branch was checked out and a new file was created, staged, and committed.
git checkout feature1
touch new.txt
git add new.txt
git commit -m "Added new file in feature1 branch"

The develop branch was checked out again, the stashed file was restored, and committed.
git checkout develop
git stash pop
git add develop.txt
git commit -m "Added develop file"

Final Result

The master branch contains feature1.txt and feature2.txt

The develop branch contains develop.txt committed successfully

The feature1 branch contains new.txt committed successfully

The feature2 branch was created for future development

Git stash was used correctly to handle unfinished work

Conclusion

This task demonstrates the use of Git branches and stash to manage multiple features and safely handle unfinished changes without losing work.
