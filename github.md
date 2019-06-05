

I'll use the Spring Music app for example. Assume sk-life/spring-music is on your internal git server, and sk-life/spring-test on GitHub.com.

First navigate to the respective repo for syncing. If it's not already cloned, clone it to your local environment.
You then can view your current git remote servers configuration of your repository.

```bash
$ git clone https://github.com/sk-life/spring-music
$ cd spring-music
$ git remotes -v
origin	https://github.com/sk-life/spring-music (fetch)
origin	https://github.com/sk-life/spring-music (push)
```

Configure your origin remote (by using the "git remote set-url') to add the second remote repository (sk-life/spring-test)

```bash
$ git remote set-url origin --add  https://github.com/sk-life/spring-test.git
$ git remote -v
origin	https://github.com/sk-life/spring-music (fetch)
origin	https://github.com/sk-life/spring-music (push)
origin	https://github.com/sk-life/spring-test.git (push)
```

Now, once you do a `git push origin`, all your remotes should be synced up!
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
 * [new branch]      master -> master
```

_NOTE: Ensure you have the credentials configured for both repositories, and you have read/write permissions._


If you want to pull from both the 2 different git repositories, then you will have to add the secondary one as another remote and run `git pull --all`.
```bash
$ git add remote origin-github https://github.com/sk-life/spring-test.git
$ git pull --all

```
