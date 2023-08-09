<img src="./images/logo.png" width=100px alt="GitHub Desktop Logo"/>

# GitHub Desktop

[Home](../../Readme.md) / [Dev Tools](../dev-tools.md) / [GitHub Desktop](tool.md)

GitHub Desktop is a GUI desktop interface for utilizing Git. It is not required if you know or like to use the command line instead. This is mainly for those new at using Git; the commands can be hard to remember initally.

## Installation

Select one of the install buttons to install the application:

[![Windows install](./images/windows-install.png)](https://central.github.com/deployments/desktop/desktop/latest/win32)
[![Mac install](./images/mac-intel-install.png)](https://central.github.com/deployments/desktop/desktop/latest/darwin)

You will likely have to sign into your GitHub account. If you don't have one you can follow the steps [here](../github/tool.md#github-account-creation).

## How to use

### Cloning a repo

Cloning a repository is a necessary first step to work on any repository. It is the act of creating a local copy of the repository on your personal device, which mirrors the repository on GitHub. You can do this in a few ways. One way is utilizing the [terminal/shell](../github/tool.md#cloning-a-repo).

1. From the home page select the `Change Repository` tab.

<img src="./images/home.png" alt="home" width=600px/>

2. From there select the `Add` button.

<img src="./images/repo tab.png" alt="change repo" width=600px/>

3. Then select `Clone repository...`.

<img src="./images/repo add.png" alt="add repo" width=600px/>

4. From there it is recommended that you Filter with `Creative` and select the repository. You may also need to adjust your local path if you haven't done so. Then select `Clone`.

<img src="./images/filter repo add.png" alt="filter repos" width=600px/>

If you could not find anything by searching you will need to complete a few more steps. 

1. Go to the repository from our [organization page](https://github.com/CreativeSolutionsGroup).
2. Click on the `Code` button as seen below.

<img src="./images/desktop clone page.png" width=600px alt="Github clone example"/>

3. Select the `Open with GitHub Desktop` button. You may need to allow the website to open the application.
4. It will open a clone window for you. Make sure the local path leads to where you want and click `Clone`.

### [Working on a repo](../github/tool.md#working-on-a-repo)

#### [Selecting a task](../github/tool.md#selecting-a-task)

#### Getting all changes from GitHub

<img src="./images/home.png" alt="home" width=600px/>

To get the new changes, press the button along the top that says `Pull origin`. If it is not present, there should be a different button in its place: `Fetch origin`. Clicking that button should first get all the changes and then allow you to pull properly.

#### Creating a branch

You should have created a branch when you [selected a task](../github/tool.md#selecting-a-task), however, if you need to create a new one after, follow these steps.

1. Check that you are on the `main` branch before continuing. If you are not, you will end up creating a branch off of an offshoot that may be behind. You can switch branches by following the [instructions found here](#switching-branches).
2. Make sure your local branch is up to date. You can find those [instructions here](#getting-all-changes-from-github).
3. Select the `current branch` button from the top middle.

<img src="./images/home.png" alt="home" width=600px/>

4. Select the `New branch` button.

<img src="./images/branches.png" alt="branches" width=600px/>

5. Make sure once again that you are on the `main` branch. From there enter a name following the scheme [found here](../github/tool.md#selecting-a-task).

<img src="./images/name branch.png" alt="name branches" width=600px/>

6. Click `Create branch`.

#### Switching branches

1. Make sure you have no current changed files. If you have any you need to first commit or remove the files by following the steps [here](#committing-changes).
2. Select the `Current branch` button located at the top.

<img src="./images/home.png" alt="home" width=600px/>

3. Select the target branch from the list.

<img src="./images/branches.png" alt="branches" width=600px/>

4. This should complete the process, but if you can't find the branch follow the steps [here](#getting-all-changes-from-github) to get all changes from GitHub.

#### Committing changes

When you need to save your changes to GitHub you can follow the first set of steps. If you need to remove your changes follow the second set of steps below.

1. Make sure all the changes you made appear as either added, changed, or removed files. Clicking any of the file names will show the changes on the right.

<img src="./images/home with changes.png" alt="home" width=600px/>

2. As long as everything appears as you expect, type a message in the summary box as a small explanation for all the changes.
3. Click the `Commit to <BRANCH NAME>` button. Keep in mind that you should **NEVER** commit to `main`. It is purely used as an example here.

Now for removing:

- If you are removing all changes, then `right click` the bar that numbers the changes. Then click the `Discard all changes...` button. Keep in mind that this will not be deleting the files, just removing the local changes you made to them.

<img src="./images/remove all changes.png" alt="remove all change" width=600px/>

- If you need to remove a singular file change `right click` on that file and select `Discard changes...`.

<img src="./images/remove a change.png" alt="remove a change" width=600px/>

## FAQ

*Can't find the repo?*
><img src="./images/cant find repo.png" alt="can't find repo" width=600px/>
>
>When you encounter this problem it is likely because you moved the repository to another location. Just select the `Locate...` button and find the repository again. Once found, select the `Select Folder` button. All fixed!
