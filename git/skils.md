# Practice your git skils

## CVCS / DVCS - Version control system

![vcs topologies](https://docs.appfusions.com/download/attachments/20777906/CVSvsDVCSFlowDiag.png?version=1&modificationDate=1429998612977&api=v2)

## Git areas

![git areas](https://i.stack.imgur.com/Z7o3V.png)

## EX1 - Create your own GitHub

1. GitHub remote bare repo creation -

    ```shell
    mkdir -p ~/github/repo
    git init --bare ~/github/repo.git
    ```

2. Developer local repo creation -

    ```shell
    mkdir -p ~/developer/repos/local_repo001
    cd ~/developer/repos/local_repo001
    git init
    git remote add origin ~/github/repo.git
    ```

3. Developer first changes -

    ```shell
    echo first_line001 > file001.txt
    git add file001.txt
    git commit -m "first commit"
    ```

4. Push changes to github

    ```shell
    git push origin master
    ```

## EX2 - Moving between stages

1. Creating new file not tracked:

    ```shell
    echo first_line001 > file002.txt
    git status
    ```

2. Move it to staging/Index area -

    ```shell
    git add file002.txt
    git status
    ```

3. Move it back to not tracked area -

    ```shell
    git restore --staged file002.txt
    git status
    ```

4. Move it to staging/Index area and to Repo (.git) -

    ```shell
    git add file002.txt
    git commit -m "second commit"
    git status
    ```

5. Now the file is part of the working tree (tracked but not staged)-

    ```shell
    echo first_line002 >> file002.txt
    git status
    ```

6. Remove change in file to working tree state -

    ```shell
    git restore file002.txt
    git status
    ```

7. Move it to staging/Index area and to Repo (.git) -

    ```shell
    echo first_line003 >> file002.txt
    git add file002.txt
    git commit --amend
    ```

## EX3 - Handling branch

1. Create new branch based on local branch -

    ```shell
    cd ~/developer/repos/local_repo001
    git checkout -b branch001 master
    ```

2. List local branchs -

   ```shell
   git branch -l
   ```

3. Deleting branch

    ```shell
    git branch -d branch001
    ```

4. Checkout someone else branch
    1. First we will create some one else branch -
        1. Going back to repos area - `cd ~/developer/repos/`
        2. Clone from our local GitHub - `git clone ~/github/repo.git local_repo002`
        3. Create new feature branch - `git checkout -b feature001 master`
        4. Create changes and commit them -

            ```shell
            echo first_line001 > file001.txt
            git add file001.txt
            git commit -m "first commit"
            ```

        5. Push local changes to CVS - `git push origin feature001`

    2. Going back to our repo `cd ~/developer/repos/local_repo001` -
        1. List remote branches (should be empty) - `git branch -r`
        2. Fetch branches from remote  - `git fetch origin`
        3. List remote branches (should be empty) - `git branch -r`
        4. Checkout remote branch - `git checkout -b feature001 origin/feature001`
        5. Check upstream (where to push when using `git push`) - `git branch -vv`

## EX4 - Commits handling

1. Adding to last commit -
    1. Create commit -

        ```shell
        echo first_line002 >> file001.txt
        git add file001.txt
        git commit -m "first commit"
        ```

    2. Add to last commit -

        ```shell
        echo first_line003 >> file001.txt
        git add file001.txt
        git commit --amend
        ```

    3. Add to last commit without change last message -

        ```shell
        echo first_line004 >> file001.txt
        git add file001.txt
        git commit --amend --no-edit
        ```

    4. Inspect commits -
        1. First inspect history with:
            1. simple - `git log`
            2. Bound number of commits - `git log -10`
            3. Cleaner output - `git log --oneline --graph -10`
        2. Afetr finding our requested commit - save its short hash -
            1. Inspect git object - `git show <hash>`
            2. Diff changes between commits - `git diff <hash> <hash>`
            3. Diff changes between current HEAD to commit - `git diff HEAD <hash>`

## EX5 - Git internals

1. Where all stored in:

    ```shell
    cd .git
    ls -F
    ```

    output:

    ```txt
    HEAD - Current inuse reference.
    config* - git config for this repo
    description
    hooks/ - demisto-sdk lint
    info/
    objects/ - blobs/trees/commits (SHA1)
    refs/ - branchs/tags references
    ```

## EX5 - Helpfull tricks

1. Take file from diffrent branch - `git checkout <branch> <path>`
2. Resore file from working tree - `git restore <path>`
3. Move from staging to working tree - `git restore --staged <path>`
4. Remove all from any area to specific commit - `git add -A && git reset --hard <commit>`

## Next - reset, rebase, merge, rebase interacive

Move our HEAD to commit object - Next lesson...
