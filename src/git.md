git init
git clone https://github.com/VadzimKuzmenkaEPAM/mjs.git

## First create a new remote repository. Clone it. Create new file named README.md with any text and commit it with "initial commit" message.
    echo "some text" >> README.md
    git add README.md
    git commit -m "initial commit"
## When you have first commit, you're able to create branches. To start this task, you need to create 3 branches:
## 1.	Start from master. From master create branch named git_task and checkout it.
## 2.	From git_task you should create two branches: git_1 and git_2.

    git branch git_task
    git checkout git_task
    git branch git_1
    git branch git_2
    git push --all -u


## 1.	git_1: Add and commit firstFile.txt file with 10 lines.

    git checkout git_1
    echo "" >> firstFile.txt
    vi firstFile.txt
    git add firstFile.txt
    git commit -m "first file"
## 2.	git_1: Add and commit secondFile.txt file with 10 lines.
      echo "" >> secondFile.txt
      vi secondFile.txt (i, esc, Shift+z, shift+z)
      git add secondFile.txt
      git commit -m "second file"

## 3.	merge branch git_1 to git_2
      git checkout git_2
      git merge git_1

## 4.	git_2: Update and commit any two lines in secondFile.txt.
      git checkout git_2
      vi secondFile.txt
      git add secondFile.txt
      git commit -m "two lines added in second file"

## 5.	git_1: Update and commit the same 2 lines with the different info in secondFile.txt

    git checkout git_1
    vi secondFile.txt
    git add secondFile.txt
    git commit -m "two lines updated in second file git_1"

## 6.	merge branch git_2 to git_1, resolve conflict. Left all (4) modified lines. Commit.
      git checkout git_1
      git merge git_2
      vi secondFile.txt
      git add secondFile.txt
      git commit -m "conflict resolved, Left 4 modified lines"

## 7.	git_1: Update and commit firstFile.txt file, modify two lines.

    git checkout git_1
    vi firstFile.txt
    git add firstFile.txt
    git commit -m "step 7: in firstFile.txt modified two lines"

## 8.	git_1: Update and commit firstFile.txt file, modify another two lines.
      git checkout git_1
      vi firstFile.txt
      git add firstFile.txt
      git commit -m "step 8: in firstFile.txt modified another two lines"

///////////////////////git format-patch git_2 -o patches
///////////////////rm -r patches/*

## 9.	Transfer changes of commit from Step 7 only to git_2, using format patch.
      git format-patch -1 23c9b1bbb0513de8c386444472c47510ba474c62 -o patches
      ls patches
      git checkout git_2
      git status
      ls patches
      git am patches/0001-step-7-in-firstFile.txt-modified-two-lines.patch


## 10.	Transfer changes of commit from Step 8 only to git_2, using cherrypick command.
       git checkout git_2
       git cherry-pick fc7b5410a8552fff57d269eac0de317297c8b404

## 11.	git_2: Concatenate the last two commits using reset + commit commands.
       git reset --soft HEAD~2 &&
       git commit
       (‘enter commit message’)
## 12.	git_2: Change date, author and message of the last commit and add non-empty thirdFile.txt file to it.

    git commit --amend --no-edit --date "Mon 04 July 2023 10:00:00 BST"
    git commit --amend --author="John Doe <john@doe.org>"
    (можно поменять сразу автора и сообщение)
    echo "non-empty file" >> thirdFile.txt
    git add thirdFile.txt
    git commit --amend --no-edit
    (The --no-edit flag allows to make an amendment to the commit without changing the commit message.)

## 13.	git_2: Create a new commit that reverts changes of the last one.
       $ git revert HEAD
## 14.	git_2: Create and commit thirdFile.txt file.
       echo "" >> thirdFile.txt.
       git add thirdFile.txt
       git commit -m «commit thirdFile.txt»
## 15.	git_2: Run command that removes all changes of the last two commits

    git reset HEAD~2

## 16.	Synchronize git_1 and git_2 with a remote repository.
       git checkout git_1
       git push -u origin git_1
       git_checkout git_2
       git push -u origin git_2

## 17.	clone your project to another folder.
       create new folder «new_forlder»
       $ cd ~/git_test/new_folder
       $ git clone git@github.com:VadzimKuzmenkaEPAM/mjs_lab.git
       git remote add origin https://github.com/VadzimKuzmenkaEPAM/mjs_lab.git
       git fetch --all


