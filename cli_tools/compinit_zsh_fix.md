# Fixing compinit Errors in ZSH

I've had an ongoing issue with compinit errors due to some combination of zsh,
zsh-autocomplete, and homebrew.

It's a permissions issue, completion files need to either be owned by root or
the current user. Also, they need to be in a directory that is not world- or
group-writable OR is owned by either root or the current user.

The `compaudit` command will output a list of files/directories that do not
conform to the above. 

Quick fix:
`compaudit | xargs chmod g-w`
and/or
`compaudit | chown -R "$(whoami)"`

Source:
https://stackoverflow.com/questions/13762280/zsh-compinit-insecure-directories
