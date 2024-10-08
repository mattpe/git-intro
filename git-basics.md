# Introduction to Version control & Git

## Contents

- Why version control?
- Basic principles of Version Control Systems
- Git
  - Basic concepts
  - Usage & workflows
- Remote repositories and hosting services
- Links to Learning materials
- [Exercises](exercises.md)

---

## Why to use VCS _(Version Control System, a.k.a. revision control)_

- Compulsory tool for professional software development
- Complete history of changes -> Track and trace code changes
- What is changed since last version and before that?
  - Why?
  - When did that happen?
  - Who did that?
- Parallel development of different features
- Compare different versions
- Share project code (and development history) —> Collaboration
- Backup for project?
- Example: [check revisions][wiki1] of an [Wikipedia article][wiki2]

[wiki1]: https://en.wikipedia.org/w/index.php?title=Git_(software)&action=history
[wiki2]: https://en.wikipedia.org/wiki/Git_(software)

Read: [What is version control?](https://www.atlassian.com/git/tutorials/what-is-version-control)

>VCS is a fundamental tool for software development, and it's used not only by individual developers but also by teams and organizations of all sizes to manage and collaborate on software projects efficiently. It plays a crucial role in ensuring code quality, collaboration, and project management in the software development process.

---

## Basic concepts

- **Repository** (or **Repo**): storage for all files, metadata and their revision data for a project
- **Commit**: revision of code (a snapshot of the repository at a specific point in time)
- **Branch**: parallel separate line of development within a repository
- **Tag**: special label for a revision (e.g. Release v. 1.1)
- **Clone**: taking a full copy of an existing repository
- **Checkout**: choosing specified version of code or development branch to work with
- **Merge**: combining changes of different branches together
- **Conflict**: occurs when there is different modifications in the same file while trying to merge branches

---

## Git

- "The Stupid Content Tracker"
- One of the most popular version control systems currently available
- Development started By Linus Torvalds 2005
- Created initially for Linux kernel development
- Distributed Version Control System (DVCS): instead of a central repository of all the version history, each user has a full-fledged repository with complete history and full version-tracking capabilities, independent of network access or a central server
- Content agnostic: can be used for anykind of files
  - with some restrictions
  - full functionality for plain text files
- Is used locally (remote server not mandatory)

![arch image](images/git-arch.png)

---

## Git installation

- Command line user interface running in operating system's terminal is the original/default tool
  - Windows: [Git for windows](https://gitforwindows.org/) provides command line tools (git bash) and Graphic UI tools/integration to Windows explorer
  - MacOS: [Several options](https://git-scm.com/download/mac)
  - Linux/Unix: via package manager, e.g. `apt install git` or `yum install git`
- Multiple [graphical UIs](https://git-scm.com/downloads/guis) are available too  
- Integrated Git support or a plugin is provided for most/all popular IDEs

---

## Git basic usage & commands

### Local Git workflow

- `git init`: create a new git repository
- `git status`: check current status of the repo, **TIP:** Use this all the time to double-check what you are doing with your repo
- `git add [filenames]`: choose files for the next commit (add to staging area)
- `git commit`: save a version of chosen files (needs a message too, e.g. `-m "added new file"`)
- `git log`: show revision history
- `git branch <newBranchName>`: create a new branch based on the current branch
- `git tag`: create a reference to a specific commit in the repository's history
- `git checkout <branchName>`: choose a branch or a revision to work with
- `git diff`: shows the differences in files between working copy and the last commit
- `git merge`: combine changes from one branch into another
- `git rebase`: modify the commit history of a branch
- `git reset`: manipulate the state of the current branch by moving the branch pointer to a different commit (used e.g. to undo changes, unstage files, etc.)
- `git stash`: temporarily save changes that you've made in your working directory but do not want to commit at the moment
- `git reflog`: "reference log", maintains a log of all reference updates in a Git repository including branch creations, checkouts, commits, merges, rebases, etc.
- `gitk`: graphical user interface (GUI) tool that comes bundled with Git

![Workflow graph](images/git-workflow.png)

[Source](http://git-scm.com/book/en/v2/Getting-Started-Git-Basics)

### Synchronising with remotes

- `git clone <URI>`: clone an existing repository (create a new local copy of the repo)
- `git remote`: manage linking with remote repositories
- `git push`: upload the changes in local repo (new commits) to chosen remote repository
- `git pull`: download the changes in remote repo ( get new changes and commits) from remote repo
- `git fetch`: retrieves changes from a remote repository, but it does not automatically merge those changes into your local working branch

---

### Getting started and creating revisions

- Git stores snapshots of all edited files in commits

![Revisions illustration](images/git-revisions.png)

[Source](http://git-scm.com/book/en/v2/Getting-Started-Git-Basics)

1. Open terminal/Git bash in your local project folder
1. Make sure you have set username and email for Git (these are saved within commit data)

    ```sh
    git config --global user.name "My Name"
    git config --global user.email my.email@example.com
    ```

1. Initialize git repo: `git init`
    - When creating a new project, the first step is to initialize a new git repository. This is done by running the `git init` command in the directory of the project. This will create a new `.git` directory in the root of the project, which will contain all the necessary files for the repository. The init command is only be run once, when the project is first created.
1. Choose files/changes you want to include in the next commit with `git add <list-of-files>`. `git add` is used to add file contents to the index. This is the first step in the basic git workflow. When changes are made to the codebase, they need to be added to the index before they can be committed.
    - `git add .` - Add all changes to the index. The `.` is a wildcard that matches all files and directories in the current directory.
    - `git add -A` - Add all changes to the index. This is equivalent to running `git add .`.
    - `git add directory-name/` - Add all changes in the specified directory to the index.
    - `git add file-name` - Add the specified file to the index. This will stage the file for the next commit.
1. Commit chosen files with `git commit -m "my commit message"`
   - use describing commit messages, check tips below
   - previous commit can be replaced with: `git commit --amend -m "my commit message"`, Note that this modifies commit history and should not be used in published branches
   - _before commits make sure that you are in the correct branch and have chosen correct files!_ (`git status`)

#### Tips

A good convention would be to include files and folders relevant to each other to a single commit, instead of adding all changes. This will make it easier to understand the changes made in the commit.

For example if you have changes in files called `login-form.js`, `login-form.css`, `image-carousel.js`, and `image-carousel.css`, it would be a good idea to add the changes in logical groups, such as:

```sh
git add login-form.js login-form.css
git commit -m "Add new feature to login form"

git add image-carousel.js image-carousel.css
git commit -m "Add new feature to image carousel"
```

**Note:** Git commands are executed in terminal, in the folder where the `.git` directory is located. This is usually the root directory of the project. For example, if your project is located in absolute path of `/usr/home/username/projects/my-project`, you should navigate to that directory before running any git commands. Running any git commands outside of the root directory of the project will result in an error, or other unexpected behavior.

##### Commit Messages

`git commit -m "Example of commit message"` - Commit changes to the codebase with a descriptive message. The `-m` flag is used to specify the commit message. The message itself is enclosed in quotes. The message for this commit is "Example of commit message".

When making changes to the codebase, it is important to write clear and descriptive commit messages. This will make it easier to understand the changes that were made, and why they were made.

A good commit message should be concise, and should explain the reasoning behind the changes. It should also be written in the present tense, and should be no longer than 50 characters.

For example:

```txt
Add new feature
```

or

```txt
Fix bug in login form
```

From these two examples, it is not that clear what has been done. Instead, a more descriptive commit message might look like this:

```txt
Add new feature to allow users to reset their password
```

or

```txt
Fix bug in login form that was preventing users from logging in
```

Make sure that the commit message does not use past tense, such as `added`, `fixed`, `removed`, etc. Instead, use present tense, such as `add`, `fix`, `remove`, etc.

Examples of bad commit messages:

```txt
Added new feature
Fixed bug
Removed unused code
```

Instead, use descriptive commit messages with present tense:

```txt
Add new feature to allow users to reset their password
Fix bug in login form that was preventing users from logging in
Remove unused code from the login component
```

Make sure that the commit messages start with a capital letter, and do not end with a period.

One good rule of thumb is to imagine that the commit message completes the sentence `If applied, this commit will...`. This will help to write more descriptive commit messages.

```txt
If applied, this commit will Add new feature to allow users to reset their password
If applied, this commit will Fix bug in login form that was preventing users from logging in
If applied, this commit will Remove unused code from the login component
```

If past tense is used in the commit message, then the sentence will not make sense:

```txt
If applied, this commit will Added new feature
If applied, this commit will Fixed bug
If applied, this commit will Removed unused code
```

Note that many conventions exists and might differ from one project to another. These conventions mentioned in this document will suffice for most projects and be more than enough for studies. Git commit messages are indication of good code quality and good practices. When reading bad git commit messages, it is often an indication of bad code quality and bad practices.

For more information on writing good commit messages, see the following articles:

- [How to Write a Git Commit Message](https://cbea.ms/git-commit/) - make sure to read this article
- [How to Write Better Git Commit Messages – A Step-By-Step Guide](https://www.freecodecamp.org/news/how-to-write-better-git-commit-messages/)

---

### Branching

- a branch is a separate line of development within a Git repository
- allows multiple developers to work on different features or fixes simultaneously without interfering with each other
- basically branches are just pointers to commits
- different [branching strategies](#git-workflows-branching-strategies) can be adapted to project

Some examples of working with branches:

```sh
git branch   # List local branches in repo
git branch --all   # List all branches
git branch new-feature  # Create a new branch named 'new-feature'
git checkout new-feature  # Switch to the 'new-feature' branch
git checkout -b bug-fix  # Create and switch to a new branch named 'bug-fix'
git branch -d bug-fix  # Delete the 'bug-fix' branch (if it's fully merged)
git branch -D bug-fix  # Force delete the 'bug-fix' branch (if not fully merged)
git branch -m new-name  # Rename the current branch to 'new-name'
git log new-feature  # Show commit history for the 'new-feature' branch
git diff new-feature main  # Compare changes between 'new-feature' and 'main' branches
```

---

### Tagging

Tags are used to mark important points in the history of a project, such as software releases or significant milestones. Unlike branches, which can move as new commits are added, tags are static and provide a way to uniquely identify and reference specific commits.

Creating a tag:

```sh
git tag <tagname>  # Tag the current commit
git tag -a <tagname> -m "Tag message"   # Create an annotated tag with a message
git tag <tagname> <commit>   # Tag a specific commit
```

Listing & viewing tags:

```sh
git tag  # list all the tags in your repository
git show <tagname>  # view details about a specifig tag
```

---

### Merging changes

Merging is the process of combining changes from one branch into another. This is typically done when a feature or bug fix is complete and needs to be incorporated into another development branch or into the `main` branch.

1. Merge changes in another branch into the current branch: `git merge <OTHER-BRANCH>`.
2. If the branch you're merging into has not diverged from the source branch, Git performs a fast-forward merge. In this case, no actual merge commit is created; the branch pointer simply moves forward to the latest commit on the source branch. (No need to create commit manually.)
3. If there are changes in both the source and target branches that cannot be resolved automatically (i.e., there are conflicting changes to the same lines of code), Git performs a three-way merge. It creates a merge commit that represents the combination of the changes from both branches. You may need to [resolve any conflicts](#resolving-conflicts) manually before finalizing the merge.
4. If you encounter issues during a merge and want to abort the merge process, you can use: `git merge --abort`
5. Finally, after resolving conflicts and completing the merge, you need to commit the merge changes to finalize the process: `git commit -m "Merge branch 'source-branch' into 'target-branch'"`

#### Using `git rebase` to integrate changes (optional)

git rebase is a Git command used for modifying the commit history of a branch. Unlike git merge, which integrates changes from one branch into another with a new merge commit, git rebase rewrites the commit history by moving or combining commits from one branch onto another. This can result in a linear, more streamlined commit history.

Note that rebasing rewrites commit history, which can make it a powerful tool for maintaining a clean and linear history. However, it should be used with caution, especially in shared branches, because it can cause confusion and conflicts for other team members if they are also working on the same branch.

Read: [Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing) (by Atlassian)

---

### Resolving conflicts

1. **Identify Conflicts**:
   When you attempt to merge or rebase a branch with conflicting changes, Git will notify you of the conflict in the terminal.
2. **Open the Conflicted File**:
   - Open the conflicted file in a code editor.
   - Git will mark the conflicting sections like this:

     ```plaintext
     <<<<<<< HEAD
     // Your changes
     =======
     // Their changes
     >>>>>>> branch-name
     ```

   - The `<<<<<<< HEAD` marker indicates the start of your changes.
   - The `=======` marker separates your changes from the changes in the other branch.
   - The `>>>>>>> branch-name` marker indicates the end of their changes.
   - Many editors and IDEs provide tools for doing this more easily
3. **Manually Resolve the Conflict**:
   - Edit the file to choose which changes to keep and how to combine them.
   - Remove conflict markers and any extra spacing or lines used for markers.
4. **Save the File**:
   - Save the file with your changes.
5. **Repeat as Needed**:
   - If there are conflicts in multiple files, repeat the conflict resolution process for each file.
6. **Add and Commit**:
   - After resolving all conflicts, add the files to the staging area using `git add <list of files or .>`.
   - Commit the changes using `git commit -m "commit message"`. Git will create a new merge commit.
7. **Test Your Changes**:
   - After resolving conflicts, it's important to test your code to ensure that the changes are correct and functional.

Remember that conflicts are a natural part of collaborative development. Good communication with your team is essential to coordinate changes and minimize conflicts. Additionally, using version control best practices, such as keeping branches up to date and using feature branches, can help reduce the frequency of conflicts.

---

## `.git/`

- Contains everything else than the working copy of files
- "physical location" of the local git repo on the file system
- removing the folder deletes the repository completely, only files in current branch are saved

The `.git` folder is a hidden folder and we do not need to interact with it directly. It contains all the necessary files for the repository, such as the configuration, the index, the object database, and the logs. If some catastrophy happens, it is possible to delete the folder, but this should be left as the last resort. Instead, google the error message, ask around. Most likely the issue is not unique.

---

## Git ignore

Which files and changes should be tracked with version control?

For example in following Eclipse Java project

![gitignore](images/gitignore.png)

only `src/` folder contains code files created by developers and everything else is generated automatically by Eclipse IDE (Integrated Development Environment) **->** `.gitignore` file for the project should be something like:

```txt
bin/
.settings/
.project
.classpath
```

`.git/` folder (contains the revision history etc.) and `.gitignore` file itself should be included in version control.

### Stuff to include

- all source code
- `README.md` and other documentation
- license
- `package.json` and other settings files
- `.gitignore` file: list of local files not to be included in the version control ->

### Stuff to exclude

- build targets and other automatically generated files
- packages managed e.g. by _npm_ (= _node_modules_ folder)
- any temp & OS specific files, like Apple's `.DS_Store`
- IDE/editor specific project files & folders

### Examples

A collection of useful _.gitignore_ templates for different kind projects [in GitHub](https://github.com/github/gitignore).

---

## Git workflows (branching strategies)

### Feature based branching

In feature branching strategy, each new feature or task gets its own branch. Developers work on these branches, and when the feature is complete, it's merged back into the main development branch.

- Advantages: Isolates new features, makes it easy to track progress on individual features, and allows for concurrent development of multiple features.
- Disadvantages: Can lead to a large number of branches, and merging can become complex if there are many long-lived feature branches.

```mermaid
%%{init: {'theme': 'default'}}%%
gitGraph
    commit id:"A" tag:"Main Start"
    branch feature
    checkout feature
    commit id:"B" tag:"Feature1 Start"
    commit id:"C" tag:"Feature1 Progress"
    checkout main
    branch feature2
    checkout feature2
    commit id:"G" tag:"Feature2 Start"
    commit id:"H" tag:"Feature2 Progress"
    checkout main
    commit id:"D" tag:"Main Progress"
    checkout feature
    commit id:"E" tag:"Feature1 Complete"
    checkout main
    merge feature
    commit id:"F" tag:"After Feature1 Merge"
    checkout feature2
    commit id:"I" tag:"Feature2 Complete"
    checkout main
    merge feature2
    commit id:"J" tag:"After Feature2 Merge"
```

- **GitHub Flow:**  GitHub Flow is a simplified workflow often used in open-source and web development. It involves a "main" branch for production-ready code and feature branches for development. Changes are continuously integrated into the main branch through pull requests.
  - Advantages Simple and effective for continuous deployment and collaboration. Suitable for fast-paced, web-centric projects.
  - Disadvantages: May not be suitable for projects with longer release cycles or complex version management.

  ```mermaid
  gitGraph
      commit id:"A" tag:"Main Start"
      branch feature
      checkout feature
      commit id:"B" tag:"Feature Start"
      commit id:"C" tag:"Feature Progress"
      checkout main
      commit id:"D" tag:"Main Progress"
      checkout feature
      commit id:"E" tag:"Feature Complete"
      checkout main
      merge feature
      commit id:"F" tag:"After Feature Merge"
  ```

- **GitLab Flow:** Similar to GitHub Flow, GitLab Flow focuses on a simple workflow using merge requests. It includes feature branches for development and long-lived "production" and "staging" branches for different stages of the development process.
  - Advantages Well-suited for teams using GitLab's built-in features. Provides clear separation of different development stages.
  - Disadvantages: May require some adaptation if not using GitLab's specific tools and features.

### Gitflow

Gitflow Workflow is a branching model that defines specific branch naming and usage conventions. It typically includes a "develop" branch for ongoing development, "feature" branches for new features, "release" branches for preparing releases, and a "main" branch for stable releases.

- Advantages: Provides a structured and organized workflow, making it easier to manage releases and hotfixes.
- Disadvantages: Can be seen as overcomplicated for smaller projects and may introduce unnecessary overhead.

```mermaid
gitGraph
    commit id:"A" tag:"Main Start"
    branch develop
    checkout develop
    commit id:"B" tag:"Develop Progress"
    branch feature
    checkout feature
    commit id:"C" tag:"Feature Start"
    commit id:"D" tag:"Feature Progress"
    checkout develop
    commit id:"E" tag:"Develop Progress"
    checkout feature
    commit id:"F" tag:"Feature Complete"
    checkout develop
    merge feature
    commit id:"G" tag:"After Feature Merge"
    branch release
    checkout release
    commit id:"H" tag:"Release Start"
    commit id:"I" tag:"Release Progress"
    checkout main
    merge release
    commit id:"J" tag:"After Release Merge"
```

### Centralized (aka Trunk-Based) Development

In this strategy, there's only one long-lived branch (typically "main" or legacy "master"). All development work, including new features, bug fixes, and experiments, is done on this branch. Continuous integration practices ensure that the code on the main branch is always in a deployable state.

- Advantages Simplicity, encourages small and frequent commits, and ensures a very stable "trunk" at all times.
- Disadvantages: Can be challenging for larger teams or complex projects, as it requires strict discipline and automation.

```mermaid
gitGraph
    commit id:"A" tag:"Main Start"
    commit id:"B" tag:"Main Progress"
    commit id:"C" tag:"Main Progress"
    commit id:"D" tag:"Main Progress"
    commit id:"E" tag:"Main Progress"
    commit id:"F" tag:"Main Progress"
```

### Release Branching

In this strategy, there's a "develop" branch for ongoing work, and when it's time for a release, a "release" branch is created. Bug fixes for the release are made on the release branch, and once it's stable, it's merged into "main."

- Advantages Provides a way to stabilize the code for releases while still allowing ongoing development.
- Disadvantages: Can introduce complexity in managing multiple branches, and merging can be challenging.

```mermaid
gitGraph
    commit id:"A" tag:"Main Start"
    branch develop
    checkout develop
    commit id:"B" tag:"Develop Progress"
    branch release
    checkout release
    commit id:"C" tag:"Release Start"
    commit id:"D" tag:"Release Progress"
    checkout main
    merge release
    commit id:"E" tag:"After Release Merge"
```

### Reading

- [Comparing Git Workflows: What You Should Know](https://www.atlassian.com/git/tutorials/comparing-workflows) (Atlassian)
- [The best Git branching strategies](https://blog.mergify.com/the-best-git-branching-strategies/) (by Hugo Escafit)

---

## [GitHub](https://github.com)

- **GitHub != Git**: Git is the application, GitHub is a company and a web service utilizing Git and providing a lot more than just version tracking.
- Commercial service providing a remote git repository server, project management tools, wiki, issue tracker, webpage hosting, etc.
- Wide user community
- **Fork**: Create a new Github project, clone the git repository of an existing project and add the cloned repo to the new project
- Almost _de facto_ hosting service for Open Source projects at the moment
- Repositories (projects) are public by default, private repos are accessible only for invited collaborators
  - Note: collaborators have always the write access to the repository
- **Pull request**: A request to merge changes from one project branch into another

## Other remote repository service providers

- [Bitbucket](https://bitbucket.org) is another popular git repo hosting service providing free private repos for small teams
- [GitLab](https://about.gitlab.com/install/) provides a commercial service or free open source community edition to installed on one's own server

## Working with remote repositories

`git pull`, `git push`, and `git fetch` are essential Git commands for interacting with remote repositories. They allow you to synchronize your local repository with a remote repository, exchange changes with collaborators, and keep your codebase up to date.

Before testing these commands you need to create an empty project for example in Github and follow the instructions to set the remote in your local repo. Additionally, you need to [setup authentication with Github](https://docs.github.com/en/get-started/getting-started-with-git/caching-your-github-credentials-in-git).

### Git pull

The `git pull` command is used to fetch changes from a remote repository and merge them into your current branch. It's a combination of `git fetch` and `git merge`.

```bash
# <remote> is the name of the remote repository (e.g., origin is the default remote name).
# <branch> is the branch from the remote repository that you want to pull and merge into your current branch.
git pull <remote> <branch>

# Example
git pull origin main
```

### Git push

The `git push` command is used to send your local commits to a remote repository. It updates the remote repository with your changes.

```bash
# <remote> is the name of the remote repository.
# <branch> is the branch you want to push.
git push <remote> <branch>

# Example
git push origin feature-branch
```

If there is changes in the remote branch, you need to pull the changes and resolve possible conflicts before pushing your local branch.

### Git fetch

The `git fetch` command retrieves changes from a remote repository and stores them locally. Unlike git pull, it doesn't automatically merge the changes into your current branch. It's useful for inspecting changes before merging.

```sh
git fetch <remote>

# Examples
git fetch origin  # fetches the latest changes from the origin remote repository but doesn't merge them into your current branch
git fetch --all  # fetches all branches from all remotes
```

### Example workflow

```mermaid
sequenceDiagram
    participant R as Remote Repo
    participant D1 as Developer 1
    participant D2 as Developer 2

    Note over D1: Developer 1 creates a project and a repo
    D1->>D1: initial commit

    Note over D1,R: Developer 1 shares the repository
    D1->>R: push

    Note over D2,R: Developer 2 clones the repository
    R->>D2: clone

    Note over D1: Developer 1 makes changes
    D1->>D1: commit changes

    Note over D1,R: Developer 1 pushes changes
    D1->>R: push changes

    Note over D2: Developer 2 makes changes
    D2->>D2: commit changes

    Note over D2,R: Developer 2 tries to push
    D2-xR: push fails

    Note over D2,R: Developer 2 pulls changes
    R->>D2: pull changes

    Note over D2: Developer 2 resolves conflicts
    D2->>D2: merge changes

    Note over D2,R: Developer 2 pushes successfully
    D2->>R: push changes
```

1. Both Developer 1 and Developer 2 are working with same project (remote repository) on their local machines.
1. Developer 1 makes some changes locally, commits them, and then pushes these changes back to the remote repository.
1. Meanwhile, Developer 2 also makes changes. However, when Developer 2 attempts to push these changes, the operation fails because the remote repository has updates that Developer 2 doesn't have.
1. Developer 2 then pulls the latest changes from the remote repository. This step might involve merging changes and resolving conflicts.
1. After successfully integrating the new changes, Developer 2 pushes their changes to the remote repository.

This sequence represents a common collaborative workflow in Git, demonstrating how developers coordinate by pulling changes from and pushing changes to a shared remote repository.

---

## Command-line `git` vs. GUIs

- command-line version is the original with complete functionality
- most IDEs have built-in or plugin based integrations for common operations
- OS specific & cross-platform Git clients/apps
  - QGit
  - Gitg
  - Git Force
  - Sourcetree
  - GitHub Desktop
  - TortoiseGit
  - GitUp
  - Fork
  - GitFinder
  - GitKraken
  - SmartGit
  - Git Cola
  - GitFiend
  - Gittyup

_If you master the command-line it's easy to understand how git works and use diffenrent GUIs too._ Additionally, all new features are implemented first in original cli application.

## More learning materials

- Free book: [Pro Git](http://git-scm.com/book/en/v2)
- [GitHub Guides](https://guides.github.com/)
- [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials/)

---

[Exercises](./exercises.md)
