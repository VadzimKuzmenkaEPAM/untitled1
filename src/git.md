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
        cd .. (do urovnya papki Vadzim_Kuzmenka)
        cp -r git_test newrepo_folder

## 18. folder2: git_1: Change two lines in firstFile.txt. commit + push
        cd newrepo_folder/
        git checkout git_1
        vi firstFile.txt
        git add firstFile.txt
        git commit -m "step 18: folder2 git_1: Change 2 lines in firstFile"
        git push

## 19. folder1: git_1: Change another two lines in firstFile.txt.
        cd ..
        cd git_test
        git checkout git_1
        vi firstFile.txt

## 20. folder1: git_1:
## Change another line in firstFile.txt (not the same as in 18, 19).
## merge changes from Step 18 (pull) without committing changes from Step 19 and any additional commits.
## push without commit changes.
## Return to local state of Step 19. (stash)
        
        vi firstFile.txt
        git remote add newrepo_folder ../newrepo_folder
        git remote update
        git stash save "Changes from step 19"
        git stash list

        git merge --allow-unrelated-histories newrepo_folder/git_1
        git push
        git stash pop stash@{0} 

## Part 2


## 1. Create git_3 branch from git_task. Checkout to git_3.
        git branch git_3
        git checkout git_3

## 2. Add new empty file doubtingFile.txt and commit it.
        echo "" >> doubtingFile.txt
        git add doubtingFile.txt
        git commit -m "step 2: Add new empty file doubtingFile.txt"

## 3. Add a line to a file and commit changes. Do it 5 times. 
##    You should end up with 5 lines in a file and 6 commits: 
##        1 for creating an empty file and 5 for adding a line.
vi doubtingFile.txt
git add doubtingFile.txt
git commit -m "step 3: Added 1 line in file doubtingFile.txt"
vi doubtingFile.txt
git add doubtingFile.txt
git commit -m "step 3: Added 2 line in file doubtingFile.txt"
vi doubtingFile.txt
git add doubtingFile.txt
git commit -m "step 3: Added 3 line in file doubtingFile.txt"
vi doubtingFile.txt
git add doubtingFile.txt
git commit -m "step 3: Added 4 line in file doubtingFile.txt"
vi doubtingFile.txt
git add doubtingFile.txt
git commit -m "step 3: Added 5 line in file doubtingFile.txt"

## 4. Check you log and copy it somewhere
$ git log -10

commit 3890e3236a7563dbbfddd3bcce7521c5c3b23731 (HEAD -> git_3)
Author: Vadzim Kuzmenka <Vadzim_Kuzmenka@epam.com>
Date:   Wed Jul 6 00:01:36 2022 +0400

    step 3: Added 5 line in file doubtingFile.txt

commit fa5fd34033e62a8b849513d356f77ac9e08dc2c6
Author: Vadzim Kuzmenka <Vadzim_Kuzmenka@epam.com>
Date:   Wed Jul 6 00:00:59 2022 +0400

    step 3: Added 4 line in file doubtingFile.txt

commit a11815bfc62c367f7cf88651a3337eef797f0432
Author: Vadzim Kuzmenka <Vadzim_Kuzmenka@epam.com>
Date:   Wed Jul 6 00:00:32 2022 +0400

    step 3: Added 3 line in file doubtingFile.txt

commit 531abfe79bf6ce81e34a441393fde78289bcd27d
Author: Vadzim Kuzmenka <Vadzim_Kuzmenka@epam.com>
Date:   Tue Jul 5 23:59:53 2022 +0400

    step 3: Added 2 line in file doubtingFile.txt

commit 05d6a7f08152e973227d7dac3503c2038030bf62
Author: Vadzim Kuzmenka <Vadzim_Kuzmenka@epam.com>
Date:   Tue Jul 5 23:59:11 2022 +0400

    step 3: Added 1 line in file doubtingFile.txt

commit c858dc2c13d23e15c19f6a6109715d7f68b6aaf4
Author: Vadzim Kuzmenka <Vadzim_Kuzmenka@epam.com>


Launch interactive rebase for 5 last commits
    git rebase -i HEAD~5    

