# Find Recently Modified/Created Files in ZSH

ZSH expansion and substition can do some crazy stuff.

To see a long listing of all files in the current directory and its 
subdirectories with an mtime within the last 2 days:
`ls -ltd **/*(m-2)`

1. `ls -ltd` - pretty straightforward; l for long listing, d to show
   directories like they're files, and t to sort by last modified time
2. `**/` - zsh expands this to "the current directory and all of its
   subdirectories"
3. `*(m-2)` - all files (`*`) that were modified (`m`) in the last two (`-2`)
   days.

Days are the default time value but you could also do months (M), weeks (w),
hours (h), minutes (m), or seconds (s). E.G. `*(mh-5)` would be files modified
in the last five hours ago. You could also do `*(mh+5)` for files that were
last touched at least 5 hours ago (i.e. have NOT been modified in last 5
hours).

In addition to `m` for modified, you can do `a` for files accessed n days ago
or `c` for the inode change time.

There's a lot of other options, look at the "Glob Qualifiers" section of the
zshexpn for more info.

## Links
[zshexpn manpage](https://linux.die.net/man/1/zshexpn)
[ZSH Lovers](http://grml.org/zsh/zsh-lovers.html)
