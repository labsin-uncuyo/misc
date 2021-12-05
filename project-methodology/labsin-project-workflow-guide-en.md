[comment]: <> (Markdown online editor: https://dillinger.io/)

# LABSIN Git Workflow Methodology

At LABSIN we use a workflow methodology that relies heavily on [github](https://github.com) (or eventually [gitlab](https://gitlab.com)). [Git](https://git-scm.com/) is a version control system that allows you to keep track of the changes made in a project in general and in the source code in particular.

Unlike CVS, SVN or TFS (scm from Microsoft), `git` is a distributed version control system: that is, there is a repo called `origin`, which is like the point where eventually the work starts, but then each developer has at least one local repo. That is why the changes are first `committed` (to your local repo), and then a `push` is made to submit those changes.

## Github
Github is a website that relies on git and allows you to keep track of changes made into the code. Its main advantage is that it allows you to work collaboratively. In addition, github relies heavily on a ticket system or *issues*, where some characteristic or feature that must be fulfilled is indicated. These issues are assigned to different participants, and their status change as the resolution progresses. The final status of the issue is flagged as `Closed` when the task has already been concluded. 

Most of these issues will be related to code implementation, ** BUUUUT**, it is not the only use case. We actually use issues for everything. For example, to indicate that some task of reading / writing a paper related to the project is missing or make a presentation, prepare a lecture about the project topics, etc.

## The workflow

The main idea is to follow the [github worflow](https://docs.github.com/en/get-started/quickstart/github-flow).

There is nothing new about our methodology, but since the github doc is large, following it is a summary about it.

1. We work hierarchically with 2 branches simultaneously:

    `main`: Production branch. Nothing is merged to `main` except there is a strong consensus among all the participants working on the repository. Only the `develop` branch can be merged to the `main` branch.

    `develop`: it is the integration branch used by all the branches to merge particular changes.

2. For each new feature we need to create a new topic branch. These branches should always be created from `develop`. The process is the following:

    a. Download the complete repository: `git clone htpp://github.com/<user>/<repository>.git`

    b. Change to branch develop: `git checkout develop`.

    c. Get the last version from origin: `git pull origin develop`.

    d.  Create a new branch from develop and change to that new branch: `git checkout -b <branch-name> develop`. You can change to any branch just doing `git checkout <branch-name>`.

    e. Then you work on the new branch adding a new feature or fixing a bug.

    f. Add the files that have to be commited `git add <file1> <file2> ...`.

    g. Commit changes in your local repo: `git commit -m "<a descriptive comment about the commit...>"`. In the comment you can make a link to the related issue using #<issue-number>, or close an issue directly from the comment. For example, `git commit -m "Minor corrections, closes #9"`. For more information about this topic, check out this [link](https://github.com/gitbucket/gitbucket/wiki/How-to-Close-Reference-issues-and-pull-request) and this  [link](https://stackoverflow.com/questions/60027222/github-how-can-i-close-the-two-issues-with-commit-message).

    h. Submit the branch content to the remote repo `origin`, creating the branch if it doesn't exist or updating it if it already exists: `git push origin <branch-name>`.

    i. Then, you must create a Pull Request (PR) at the github site. Comments from the others developers are expected.

    j. When the PR is approved, the merge between `develop` and `<branch-name>` is made at the github site.

    k. Finally, if all issues were resolved related the branch, the branch may be deleted, `git branch -d <branch>`.

## Downloading other branches

Later, if someone creates a new branch and sets it to `origin`, and you want to download it to your local repo, you first download a snapshot of the entire project doing `git fetch origin`. Then, you can do `git checkout <branch-name>` or alternatively do `git checkout --track origin / <branch-name>`


## About the releases

A release is an official version of the project under development. When you are going to make a release, you typically do a single PR from `develop` to `main`, check and merge in `main`. 

Then, the version history is usually keeped by adding tags in `main` (you can add them in any branch anyway if you need them). The tags are like markers in the history and then if necessary you can create branches off of those tags.

## Useful commands

### Check current branch and commited files
`git status`

### Delete N commits
`git reset --hard HEAD~2` command moves the current branch backward by 2 commits.

### Unstage a file (uncommit)
`git restore --staged <file>...`

 