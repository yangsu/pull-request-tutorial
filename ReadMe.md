# Pull Request Tutorial

## What is a Pull Request?
From Github's [Using Pull Requests Page](https://help.github.com/articles/using-pull-requests)
> Pull requests let you tell others about changes you've pushed to a GitHub repository. Once a pull request is sent, interested parties can review the set of changes, discuss potential modifications, and even push follow-up commits if necessary.

Pull Requests are commonly used by teams and organizations collaborating using the [Shared Repository Model](https://help.github.com/articles/using-pull-requests#article-platform-nav), where everyone shares a single repository and topic branches are used to develop features and isolate changes. Many open source projects on Github use pull requests to manage changes from contributors as they are useful in providing a way to notify project maintainers about changes one has made and in initiating code review and general discussion about a set of changes before being merged into the main branch.

Here's [an example pull request](https://github.com/jquery/jquery/pull/1051) from jQuery's github repo.

## Creating a Pull Request

There are 2 main work flows when dealing with pull requests:

1. Pull Request from a [forked repository](https://help.github.com/articles/fork-a-repo)
2. Pull Request from a branch within a repository

Here we are going to focus on 2.

### Creating a Topical Branch

First, we will need to create a branch from the latest commit on master. Make sure your repository is up to date first using

```bash
git pull origin master
```

*Note:* `git pull` does a `git fetch` followed by a `git merge` to update the local repo with the remote repo. For a more detailed explanation, see [this stackoverflow post](http://stackoverflow.com/questions/292357/whats-the-difference-between-git-pull-and-git-fetch).

To create a branch, use `git checkout -b <new-branch-name> [<base-branch-name>]`, where `base-branch-name` is optional and defaults to `master`. I'm going to create a new branch called `pull-request-demo` from the `master` branch and push it to github.

```bash
git checkout -b pull-request-demo
git push origin pull-request-demo
```

### Creating a Pull Request

To create a pull request, you must have changes committed to your new branch.

Go to the repository page on github. And click on "Pull Request" button in the repo header.

![Pull Request Button](https://f.cloud.github.com/assets/676185/316845/2ea7d418-9848-11e2-90af-5b8f31497a51.png)

Pick the branch you wish to have merged using the "Head branch" dropdown. You should leave the rest of the fields as is, unless you are working from a remote branch. In that case, just make sure that the base repo and base branch are set correctly.

![Head Branch Dropdown](https://f.cloud.github.com/assets/676185/316857/0d51b008-9849-11e2-909a-36e6f12436b4.png)

Enter a **title** and **description** for your pull request. Remember you can use [Github Flavored Markdown](https://help.github.com/articles/github-flavored-markdown) in the description and comments

![Title and Description](https://f.cloud.github.com/assets/676185/316873/0c0e4cc8-984a-11e2-89f5-703c31217e17.png)

Finally, click on the green "Send pull request" button to finish creating the pull request.

![Send Pull Request](https://f.cloud.github.com/assets/676185/316876/30d6d0ca-984a-11e2-9c5e-420223c35ed9.png)

You should now see an open pull request.

![Open Pull Request](https://f.cloud.github.com/assets/676185/316899/6a62a7c8-984b-11e2-92ee-182ef257b574.png)

### Using a Pull Request

You can write comments related to a pull request,

![Writing a comment](https://f.cloud.github.com/assets/676185/316903/d9729df8-984b-11e2-9bf6-8fe064957723.png)

view all the commits by all contained by a pull request under the commits tab,

![Commits tab](https://f.cloud.github.com/assets/676185/316908/563073ba-984c-11e2-8bd6-450939fbd7b3.png)

or see all the file changes from the pull request across all the commits under the "Files Changed" tab.

![Files Changed](https://f.cloud.github.com/assets/676185/316911/9e4cbe42-984c-11e2-9636-dd50cb98db44.png)

You can even leave a comment on particular lines in the code changed, simply by hovering to the left of a line and clicking on the blue note icon.

![Comment in line](https://f.cloud.github.com/assets/676185/316916/015be558-984d-11e2-9c4c-2ddc793fac3c.png)

### Merging a Pull Request

Once you and your collaborators are happy with the changes, you start to merge the changes back to master. There are a few ways to do this.

First, you can use github's "Merge pull request" button at the bottom of your pull request to merge your changes. This is only available when github can detect that there will be no merge conflicts with the base branch. If all goes well, you just have to add a commit message and click on "Confirm Merge" to merge the changes.

![Merge pull request button](https://f.cloud.github.com/assets/676185/316946/e8c42c4c-984e-11e2-8a09-5a977652028a.png)
![Confirm Merge](https://f.cloud.github.com/assets/676185/316947/ea15ebee-984e-11e2-8c08-e76a54c89755.png)

#### Merging Locally

If the pull request cannot be merged online due to merge conflicts, or you wish to test things locally before sending the merge to the repo on Github, you can perform the merge locally instead.

You can find the instruction to do so by clicking the `(i)` icon on the merge bar.

![Merging Instructions](https://f.cloud.github.com/assets/676185/316954/b34855f6-984f-11e2-9713-6c8288617a78.png)

However, there's an alternative that may be better for long standing branches.

#### Squash, Rebase, and Cherry Pick

In long standing branches, merging can often cause lots problems when updating if changes in a given branch conflict with changes recently merged into the master branch. If there are many commits to the same file, `git merge` may force you to fix the same merge conflicts over and over again, causing a real headache. While there are many ways to mitigate this issue, such as enabling [`git rerere`](https://www.kernel.org/pub/software/scm/git/docs/git-rerere.html) to reuse recorded resolution of conflict merges, squashing a series of related changes into 1 commit and cherry-picking it into the master is a great solution, especially for topic branches and isolated features.

There are several advantages of performing merges this way. First, you only have to deal with merge conflicts once, since all commits are compressed into 1. Second, each commit represents an entire set of changes required for a feature or task, which makes it easy to pin point bugs and other problems when they arise and to remove a change set when it's no longer necessary.

There are also disadvantages of squashing commits. First, you will lose the details and information for each change, as all changes squashed are compressed together. So the net effect is the same. Second, it can be dangerous and problematic if used incorrectly, such as squashing commits that have been pushed to the remote server **and** others depend on for their work. Because squashing is changing the git history, you can cause many conflicts that way. However, if you are using this locally or you are the only person working on your branch and you know exactly what you are doing.

To perform this, use the following command

```bash
git rebase -i HEAD~10
```

`-i` stands for [interactive mode](http://git-scm.com/book/en/Git-Tools-Rewriting-History#Changing-Multiple-Commit-Messages) and `HEAD~10` means to examine the 10 latest commits.

If you see an `fatal: Needed a single revision` error, this usually means that there are not that many commits left. Try a lower number.

This will open up an editor with git commit messages that looks something like this:

![Git Rebase](https://f.cloud.github.com/assets/676185/317107/cdcd54d6-9858-11e2-9e78-7642fa363f10.png)

There are many options available at this stage. These are detailed in [this github help page](https://help.github.com/articles/interactive-rebase). Here, I'm going to simply squash all changes in this pull request into one. Save and close the editor.

![Squashing commits](https://f.cloud.github.com/assets/676185/317112/21e1a702-9859-11e2-8c03-7f344002768e.png)

The next screen will pop up asking you to edit your commit messages. You can choose to edit them or simply continue. Save and close the editor.

![Squash Result](https://f.cloud.github.com/assets/676185/317086/cb3933f8-9857-11e2-9909-44cdd256bc11.png)

Once your squash completes, you can push it to the remote repo. In this case, these squashed commits have been pushed to the server. However, I'm the only user of this branch and can safely force push the commit to update the git repo.

```bash
git push origin pull-request-demo -f
```

To merge the commit, we will use [`git cherry-pick`](https://www.kernel.org/pub/software/scm/git/docs/git-cherry-pick.html).

![Cherry Picking](https://f.cloud.github.com/assets/676185/319726/fdc11cfa-98d9-11e2-8891-248d9ed09c05.png)

You are done! Github should detect the changes and update the pull request. You can then marked the pull request as merged and optionally delete the branch.

### Closing a Pull Request

You can simply click on the "Close" button on the pull request to close it. Optionally, you can delete the branch directly using the "Delete this branch" button.

![Closing a Pull Request](https://f.cloud.github.com/assets/676185/317150/3f849c86-985b-11e2-9de9-9c555fc81515.png)
