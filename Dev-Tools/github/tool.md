<img src="./images/logo.png" width=100px alt="GitHub Logo"/>

# GitHub

[Home](../../Readme.md) / [Dev Tools](../dev-tools.md) / [GitHub](tool.md)

This is our version control system at CSG. We have many repos (repositories) that are publically accessible and therefore must be protected and well maintained. This is used to save all our work in a manner visible to our entire team. This is also a great way to show future employers the work you have done. One thing to always remember while using git is, do *not* work off of `main`.

## Installation

As GitHub uses Git you will need to install that first. Go to the [git downloads page](https://git-scm.com/downloads) and download and install the version that best suits your needs. Nothing else from here will need to be installed. You may use the mobile device to keep track of the repositories, but you will not be able to work on them from there.

### GitHub account creation

**NOTE**: You will want to use a personal email and **NOT** your Cedarville email. This account is to be yours and therefore should be able to persist after graduation. It acts as a portfolio for your work. It is recommended that if you don't have a professional personal email, make one.

1. Head to the [GitHub registration page](https://github.com/signup).
2. Follow the steps there.
3. You can access our organization from [here](https://github.com/CreativeSolutionsGroup).
4. You will need to be added to the organization to make changes.
5. It is not required but recommended that you set up 2FA on your GitHub. To do so, start by going to your profile [security page](https://github.com/settings/security). There are many options at the bottom of this page. Choose one or many.

### Name and email setup

Go into a terminal/shell and enter the following:

```ps
git config --global user.name "Your name here"
git config --global user.email "your_email@example.com"
```

As long as you replace what is in quotations, you will have "logged in" to git.
Keep in mind that your email should be the one used to create your GitHub account.

### SSH setup (optional)

SSH offers better protection and authentication when working on repositories. It is not required for CSG, but is highly recommended.

1. Open a terminal/shell and enter `cd .\.ssh\`
2. Enter `ls` and look for two different files: `id_rsa` and `id_rsa.pub`.
3. If you have both skip to step 5, else continue to step 4.
4. Create public/private keys by entering this command: `ssh-keygen -t rsa -C "your_email@example.com"`. Make sure to use the same email from the setup above.
5. Copy the contents of the `id_rsa.pub` file. With PowerShell use `cat ~\.ssh\id_rsa.pub | clip` or on Mac `pbcopy < ~/.ssh/id_rsa.pub`.
6. You will now navigate to the [GitHub profile settings](https://github.com/settings/profile).
7. Click on `SSH and GPG keys` on the left side.
8. Select `New SSH key`.
9. Give the key a name linking you back to the device you are on, and then paste the contents into the `Key` box.
10. After saving, go back into the terminal and enter `ssh -T git@github.com` to test that it worked.
11. You will likely get something along the lines of...

```ps
The authenticity of host 'github.com (140.82.112.3)' can't be established.
ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

12. Enter `yes`.
13. If you get something like `Hi username! You've successfully authenticated, but GitHub does not provide shell access.` the setup was successful.

### Default Tracking (optional)

Default tracking enables your local installation of git to always point new branches to the origin. It removes the need to explicitly tell the branch.

1. Open a terminal
2. Check your git version with `git --version`. You need to have version 2.37+
   1. If you are not updated make sure to [update git](#updating-git) before continuing and refresh your terminal
3. Run `git config --global --add --bool push.autoSetupRemote true`

### Powershell Extensions (optional for Windows)

There are two different extensions that are recommended for installation for anyone using powershell to access git. These help speed up your own work and provide a bit of visual feedback to what is happening on the current branch.

#### Tab completion

1. Open powershell and run ``Add-Content $PROFILE.CurrentUserAllHosts "`nSet-PSReadlineKeyHandler -Chord Tab -Function MenuComplete"``
2. Reset powershell; type `cd` and press tab. If you get a few options under the current typed line then the setup was successful.

#### Git status

Follow the [posh-git instructions](https://github.com/dahlbyk/posh-git#installation). They have great documentation. If you can navigate to a git repo and see something resembling the following picture, then you were successful in setup. Don't worry about the green and red numbers right now, those are staged/upstaged changes. The current goal is just to see the branch name.

![posh-git example](https://github.com/dahlbyk/posh-git/wiki/images/PromptDefaultLong.png)

## How to use

You will be able to access all of the repos by going to our [organization page](https://github.com/CreativeSolutionsGroup). Once inside a repository, there are a few things you will need to know how to do.

### Cloning a repo

Cloning a repository is a necessary first step to work on any repository. It creates a local copy of the repository on your personal device which mirrors the repository found on GitHub. You can do this in a few ways: utilizing the [desktop app](../github-desktop/tool.md#cloning-a-repo) (the instructions can be found on the linked page), or utilizing a terminal/shell. The steps for the latter are as follows:

1. Open a terminal/shell and navigate to the folder you would like to contain the repo.
2. Click on the `Code` button as seen below.

<img src="./images/desktop clone page.png" width=600px alt="Github clone example"/>

3. You will be able to choose from three options. We will look at `HTTPS` and `SSH` here.
4. If you set up `SSH` in the installation phase then navigate there and copy the link. If not, copy the `HTTPS` link.
5. Go back into your terminal and enter `git clone` and paste your copied link at the end. If you would like the repository folder to be named something other than what the actual repository is called then add it to the end. Here is an example using `HTTPS` of our wiki repo, renamed to knowledge. `git clone https://github.com/CreativeSolutionsGroup/wiki.git knowledge`
6. You should now have a clone of the repository on your system.

### Working on a repo

Here is a compliation of all the commands used within a repository. They are in order, with the assumption you have not yet created a `feature/`, `fix/` or `update/` branch.

#### Selecting a task

1. Navigate to our [project Kanban board](https://github.com/orgs/CreativeSolutionsGroup/projects/9).
2. From here select one of the items in the `Todo` section that you (or no one) have been assigned to.
3. Move the task into the `In Progress` column.
4. From here you can click `Open in new tab` on the right side.
5. Now you want to create a new branch associated with your work by clicking on the link under `Development` labeled `Create a branch`.
6. You will want to change the branch name.
    - We use a few different prefaces for different reasons.
        - `feature` is our main preface that denotes the changes as mostly new items that add to the application.
        - `fix` is for when you are working purely on fixing bugs.
        - `update` is uncommon, but for when you are just updating dependencies.
    - After the preface add a `/`.
    - Then describe what the task is in as few characters as possible.
    - For example, I would consider the branch that I am working on creating this GitHub page, `feature/github-page`.
7. You can then select `checkout locally` or `open branch with GitHub desktop`, and click `Create branch`.
8. You are now good to [switch branches](#switching-branches).

#### Getting all changes from GitHub

1. Get back to the main branch by running `git checkout main`.
2. Run `git pull`. This will get all of the changes from the remote `main` on GitHub, updating your local `main`. Every time an update is pushed to the repository's `main` you will need to run `git pull` to see the updated status for any of your already-created branches. New branches will automatically pull the latest updates from `main` when created.

#### Creating a branch

If you did not create the branch in the previous section then you can do so in a few different ways. It is recommended that you still link the branch to whatever branch you are working on, however. First, you will want to [update your local repo](#getting-all-changes-from-github).

- `git checkout -b <BRANCH NAME>` will create a new local branch and move you to it.
- `git switch -c <BRANCH NAME>` will also create a new local branch and move you to it. However, this command will also move any uncommitted changes as well.

Now that you have a new local branch and are moved to it, you will need to push the branch to the repo. `git push --set-upstream origin <BRANCH NAME>` will do this for you. You may also shorten it to `git push -u origin <BRANCH NAME>`

#### Switching branches

1. Make sure there are no active changes on the branch you are currently on. This can be done by either removing, committing, or stashing the changes.
    - *Removing*: To remove you have to do one of two commands: 
        - To reset the branch to the previous commit use `git reset --hard`. Keep in mind that this will remove **ALL** of the changes. It is recommended that you first use `git status` to make sure that you desire **none** of the changes to be committed.
        - To remove specific files use `git restore <FILE>`. This will restore any changes to the previous commit. Keep in mind that if there are any leftover changes you will still have to either commit or stash them.
    - *Committing*: You can find the steps for committing your changes further down the page or by clicking [here](#committing-changes).
    - *Stashing*: By stashing you are saving all active changes but storing them for use later. You can stash by using `git stash` and "unstash" by using `git stash pop`. You can pop the stash on any branch in the repo. Keep in mind that a faster way to move your changes to another branch is by using the `switch` command found in step 2b.
2. You can now change the branch you are on. There are two ways to do that:
    - `Checkout`: This is an older way of changing branches. Using `git checkout <BRANCH NAME>` you will switch to an already existing branch as long as there are no uncommitted changes.
    - `Switch`: This way is newer and works a bit faster. It includes a few perks, like moving any uncommitted changes without having to stash them. Using `git switch <BRANCH NAME>` you will switch to an existing branch carrying over any uncommitted changes. This avoids the need to stash, change branches, and then pop the stash.

#### Committing changes

When you have reached a milestone on the task or have finished up your work it is recommended you save all your changes to the repository. That is where committing comes into play.

1. First, run `git status` to make sure that all of the changed files show up.
2. Run `git add .` which will stage all of the changes to be committed.
3. Run `git commit -m "<COMMIT MESSAGE>"` to commit your changes. The commit message should explain the changes you made in an easy-to-understand manner. It will allow for easy backtracking later, if necessary.
4. Run `git push` to push all commits to GitHub. If you get a warning that says that you do not have all remote changes run `git pull` and then `git push`.

At this point you are free to keep working, however, if this is the end of your task you have a few more steps to complete.

1. Go back to our [project board](https://github.com/orgs/CreativeSolutionsGroup/projects/9).
2. Move the task you were working on from `In Progress` to `Ready for Review`.
3. Open the task in a new tab.
4. Select the `Pull Requests` tab at the top.
5. There should be a green bar that shows the branch you were on and an offer to make a pull request for it. Click that button and go to step 8. If there is not, then you will need to click the `New pull request` button.
6. Make sure the `base` branch is `main`, and then change the `compare` branch to the branch you were working on.
7. Select `View pull request`.
8. Go under the `reviewers` section and add your direct executive to review.
9. In the comments field add `Closes #<Task Number>.`. The task number can be found on your task in the Kanban board. After that, add a description of the changes made on the branch. If testing requires extra steps, make sure to add those in the description also.
10. Submit the pull request. It is good practice to let your reviewer know the pull request is ready. You can do this by copying the link in your search bar and sending it to your reviewer through Microsoft Teams.

#### Reviewing Changes

1. Ensure all checks and tests were successful. If there were any failures, figure out why and leave a comment about it.
2. Check files for quality. Your job is not to rewrite the code, but to make sure that what is there keeps with the Cedarville quality of code.
3. If you see anything wrong select those lines and leave a comment specifying the problem.
4. Once all issues are addressed, click the `Review Changes` button at the top and leave an overall comment. Select `Request Changes` and then `Submit Review`.
5. If there were no issues, click the `Review Changes` button at the top and leave an overall comment. Commonly we will say `LGTM` meaning `looks good to me`. Select `Approve` and then `Submit Review`.
6. If approved, head back to the conversation tab and select `Merge pull request`.

#### Updating Git

##### Windows

Version 2.16.1(2)+: `git update-git-for-windows`
Version 2.14.2 to 2.16.1: `git update`

##### Mac

*With Homebrew installed:*

Run `brew upgrade git`

If you haven't installed with Homebrew, but don't have git installed that way, just run `brew install git`. This will override the previous install and automatically update for you.

*Without Homebrew installed:*

Either go through the process of installing the new version from the [git website](https://git-scm.com/download/mac), or install Homebrew with the following steps.

1. `/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`
2. `brew update`
3. `brew install git`

##### Linux

1. Update system packages with `sudo apt-get update`
2. Update git with `sudo apt-get install git`

## FAQ
