# Git Cheatset

## Git areas

![git areas](https://i.stack.imgur.com/Z7o3V.png)

## Git objects

Located in `.git` directory, list them by `ls -a` -

1. Commit
2. tree
3. Blob
4. Tag

Inspect objects by - `git cat-file <hash>`

## Init new repository

1. Create new repo - `git init`
2. Create new bare repo (Like GitHub) - `git init --bare`

## Clone existing repository

1. Clone exsiting repo - `git clone <ssh/url/path> <target_dir>`

## Remotes

1. Add remotew to track - `git remote add <name-[origin by default]> <path/url/ssh>`
2. List remotes - `git remote -v`

## Status - Working tree / Staging / Repo (directory)

1. Status - `git status`

## Log

1. Simple log - `git log`
2. Log bound - `git log -<numbe of commits>`
3. Log one line - `git log --oneline`
4. Log like graph - `git log --graph`
5. Log filters -
    1. dates -

       ```shell
        --since="1 week ago"
        --until="yesterday"
        ```

    2. Author - 

        ```shell
        --author="Rico"
        --committer="Rico"
        ```

    3. Path - `git log <path>`
    4. Commit message grep - `--grep="Merge pull request"`

## Branchs

1. Create new branch - `git checkout -b <feature_name> <base_branch>`
2. Change branch - `git checkout <branch>`
3. List local branchs - `git branch -l`
4. List remote branchs - `git branch -r`
5. List all branchs - `git branch -a`
6. Deleting branch - `git branch -d <branch>`

## Stage changes

1. Move path to staging - `git add <file/regex>`
2. Move all to staging - `git add -A # Stage all changes`
3. Unstage chanes - `git restore --staged <path>`

## Create commit

1. Create new commit - `git commit -m "<messege>"`
2. Add to previous commit - `git commit --amend`
3. Create new commit without hooks - `git commit -m "<messege>" -n`

## Push changes

1. If history not diverged - `git push <remote name> <branch>`
2. If history is diverged - `git push -f <remote name> <branch>`

## Fetch remote

1. Fecth branch from specific remote - `git fetch <remote_name>`
2. Fecth branch from specific remote branch - `git fetch <remote_name> <branch>`

## Reset

move between commits objects
`git reset --<type> <commit>`

### Types

1. `hard` -
    a. `Working directory` to commit.
    b. reset `Staging` to commit.
    c. reset ref `Repo` to commit.

2. `mixed` (default) -
    a. Same `Working directory`.
    b. reset `Staging` to commit, but move changes to `Working directory`.
    c. reset ref `Repo` to commit.

3. `soft` -
    a. Same `Working directory`.
    b. Same `Staging`, but more change happend from moves commit message.
    c. reset ref `Repo` to commit.
