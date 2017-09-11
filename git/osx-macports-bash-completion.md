# Using git bash completion on osx with macports

It appears that the git version installed by [macports](https://www.macports.org/) contains the bash completion script.
Simply add to your .bash_profile:

```bash
[ -e "/opt/local/share/git/contrib/completion/git-completion.bash" ] && . /opt/local/share/git/contrib/completion/git-completion.bash
```

Obviously you need macports and git installed from [macports](https://www.macports.org/):

```bash
sudo port install git
```

