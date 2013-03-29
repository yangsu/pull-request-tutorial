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

To create a pull request, you must have changes committed to the your new branch.

Go to the repository page on github. And click on "Pull Request" button in the repo header.

![Pull Request Button](https://f.cloud.github.com/assets/676185/316845/2ea7d418-9848-11e2-90af-5b8f31497a51.png)

Pick the branch you wish to have merged using the "Head branch" dropdown. You should leave the rest of the fields as is, unless you are working from a remote branch. In that case, please refer to the [remote branch pull request guide]().

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

You can event leave a comment on particular lines in the code change simply by hovering to the left of a line and clicking on the blue note icon.

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
