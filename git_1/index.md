# git_1 git log, git status, git clean


git log, git status, git clean
<!--more-->

## [git log](https://git-scm.com/docs/git-log)

### git log overview
This terminal command shows the commit log

### git log with other handy options
- ```git log --graph``` This command generates the git log with graph user interface
- ```git log grep="more"``` This command will show the commit whose commit information contains the word "more"



## git status

### git status overview
<p>
The git status command displays the state of the working directory and the staging area. It lets you see which changes have been staged, which haven’t, and which files aren’t being tracked by Git. Status output does not show you any information regarding the committed project history. For this, you need to use git log.
</p>

(credit to [gitbucket](https://www.atlassian.com/git/tutorials/inspecting-a-repository))

Often times, once programmer looks at the state of the working directory, one may would like to revert back to certain commit; here, ```git clean``` is a handy git command to use.

## [git clean](https://git-scm.com/docs/git-clean)

### git clean overview

<p>
Cleans the working tree by recursively removing files that are not under version control, starting from the current directory.
</p>

(credit to [git clean](https://git-scm.com/docs/git-clean))

### git clean with other handy options

- ```git clean -n``` This command will tell you what files to be removed, but will not removed them. You can regard these as a rehearse.
- ```git clean -f``` This command will clean the untracked files.
    - ```git clean -fd``` This command will clean the untracked files and directories.
    - ```git clean -xf``` This command will clean the untracked files, regardless of .gitignore
    - ```git clean -f <path>``` This command will clean the untracked files under <path>
- ```git reset --hard && git clean -f`` This is usually used to help your directory back to certain commit
