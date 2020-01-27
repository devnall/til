# Using zsh's Directory Stack

zsh supports a pushd/popd-like directory stack with an interactive frontend.

```
$ setopt autopushd pushdminus pushdsilent pushdtohome pushdignoredups
$ DIRSTACKSIZE=8
$ cd dir1
~/dir1 $ cd dir2
~/dir1/dir2 $ cd dir3
~/dir1/dir2/dir3 $ dirs -v
0   ~/dir1/dir2/dir3
1   ~/dir1/dir2
2   ~/dir1
3   ~
~/dir1/dir2/dir3 $ cd -2
```

It also works with tab completion:
```
$ cd -<tab>
1 -- ~/dir1/dir2
2 -- ~/dir1
3 -- ~
```

And is referenceable in commands:
```
$ ls =1/dir4
ls ~/dir1/dir2/dir4
```

The above options do the following:
* autopushd - make `cd` act like `pushd` (while dealing with the edge cases that prevent `alias cd=pushd` from being sufficient)
* pushdminus - swaps the meanings of `cd +1` and `cd -1` to mean the opposite of what they mean in csh, because it makes more sense and is easier to type
* pushdsilent - prevent the shell from printing the directory stack on every `cd`
* pushdtohome - push to $HOME when no argument is given
* pushdignoredups - ignore duplicate entries in directory stack
* DIRSTACKSIZE - maximum number of entries in the directory stack

## Links & References
* http://zsh.sourceforge.net/Intro/intro_6.html
* https://github.com/mattjj/my-oh-my-zsh/blob/master/directory.zsh
