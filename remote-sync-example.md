## Git Remote Sync Example

I'll use the Spring Music app for example. Assume _../sk-life/spring-music_ is on your internal git server, and _../sk-life/spring-test_ on GitHub.com.


### Clone & Check Remote
First navigate to the respective repo for syncing. If it's not already cloned, clone it to your local environment.
You can then view your current `git remote` configuration of your repository.

```bash
$ git clone https://github.com/sk-life/spring-music
$ cd spring-music
$ git remote -v
origin	https://github.com/sk-life/spring-music (fetch)
origin	https://github.com/sk-life/spring-music (push)
```
### Configure origin  
Configure your origin remote (by using the "git remote set-url') to add the second remote repository (sk-life/spring-test)

```bash
$ git remote set-url origin --add  https://github.com/sk-life/spring-test.git
$ git remote -v
origin	https://github.com/sk-life/spring-music (fetch)
origin	https://github.com/sk-life/spring-music (push)
origin	https://github.com/sk-life/spring-test.git (push)
```
### Sync both servers
Now, once you do a `git push`, all your remotes should be synced up!
```bash
$ git push origin master
Username for 'https://github.com': sk-life
Password for 'https://sk-life@github.com':
Everything up-to-date
Counting objects: 1007, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (422/422), done.
Writing objects: 100% (1007/1007), 685.82 KiB | 228.61 MiB/s, done.
Total 1007 (delta 350), reused 1007 (delta 350)
remote: Resolving deltas: 100% (350/350), done.
To https://github.com/sk-life/spring-test.git
 * [new branch]      master -> master #You can see it pushing master branch to remote repo
```

_NOTE: Ensure you have the credentials configured for both repositories, and you have read/write permissions._

----

## Will you be doing active development in both your GitHub and git server repository?

In this case, if you have changes on GitHub, you cannot pull them in to your git server repository since it will only pull from the url annotated with (fetch). So, if the GitHub repository has commits that are not in your git server repo, your next push will get rejected since the commit history will not match.

To fix this, you will need to add the repo as a new remote repository.

### Add new remote
If you want to pull from both the 2 different git repositories, then you will have to add the secondary one as another remote.
```bash
$ git remote add origin-github https://github.com/sk-life/spring-test.git
$ git remote -v
origin	https://github.com/sk-life/spring-music (fetch)
origin	https://github.com/sk-life/spring-music (push)
origin	https://github.com/sk-life/spring-test.git (push)
origin-github	https://github.com/sk-life/spring-test.git (fetch)
origin-github	https://github.com/sk-life/spring-test.git (push)
```

### Pull Changes & Sync
You can then pull from specific branch of the GitHub repo to merge into the your local environment. Once you merge and commits match, you can push to sync all again.
```bash
# Pulling master branch from remote server "origin-github"
$ git pull origin-github master
From https://github.com/sk-life/spring-test
 * branch            master     -> FETCH_HEAD
Updating 71f89c2..f574dc9
Fast-forward
 github.md | 50 ++++++++++++++++++++++++++++++++++++++++++++++++++
 1 file changed, 50 insertions(+)
 create mode 100644 github.md

# checking the status of my local repository
$ git status
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean

# pushing the latest commit to all remotes
$ git push
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 1.01 KiB | 1.01 MiB/s, done.
Total 3 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/sk-life/spring-music
   71f89c2..f574dc9  master -> master
Everything up-to-date
```
