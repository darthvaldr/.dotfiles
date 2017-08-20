# .dotfiles

## setup your $HOME

run this in your terminal to setup a repo to push your dotfiles to. it uses a 'config' alias to keep things nice & tidy.

* inits a git repo
* setups 'config' alias for a git-dir out of the way (.cfg)
* enable setting that hides untracked files
* echos our 'config' alias setup to ~/.bashrc for persistence

```bash
git init --bare $HOME/.cfg
alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'
config config --local status.showUntrackedFiles no
echo "alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'" >> $HOME/.bashrc
```

## add some files to your dot
you know the drill, just remember you want 'config <add|commit|push|pull>' cos alias.

```bash
# add files
config add .bashrc

# add folders
config add .i3/*

# commit like usual (i know '-m' is bad practice, forgive me)
config commit -m "Add some files"
```

## setup your GIT

* create your github/bitbucket repo

example, my .dotfiles.git repo (remember 'config' is a bash alias setup in first step)

```bash
config remote add origin git@github.com:darthvaldr/.dotfiles.git
config push --set-upstream origin master
```

you will get an error for your troubles, because your github repo has files your local repo doesn't:

```bash
To git@github.com:darthvaldr/dotfiles.git
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'git@github.com:darthvaldr/dotfiles.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

rectify this with a pull:

```bash
config pull origin master

From github.com:darthvaldr/.dotfiles
 * branch            master     -> FETCH_HEAD
Merge made by the 'recursive' strategy.
 README.md | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
```

then you should be good to 'config push' from here:

```bash
darthvaldr@localhost:~ $ config push --set-upstream origin master
Counting objects: 20, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (16/16), done.
Writing objects: 100% (20/20), 9.02 KiB | 0 bytes/s, done.
Total 20 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), done.
To git@github.com:darthvaldr/.dotfiles.git
   bced3f7..0e18231  master -> master
Branch master set up to track remote branch master from origin.
```

## References

### credits
[Nicola Paoluci](https://developer.atlassian.com/blog/2016/02/best-way-to-store-dotfiles-git-bare-repo/)
[StreakyCobra/HackerNews](https://news.ycombinator.com/item?id=11071754)
