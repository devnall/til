# Writing to a Root-Owned File After Forgetting to Open vim With sudo

When you open a root-owned (really, any file on which you don't have write permission) file in vim as a normal user, you'll see an error when you first go into insert mode:
`W10: Warning: chaning a readonly file`

If you miss or ignore that and make edits and try to write your changes, you'll either not be able to save or you'll get some weird behavior (e.g. changing file permissions).

When you're ready to write your changes and start seeing errors, you can run:
`:w !sudo tee %` 
to write to the file as root.

Even better, add the following to your .vimrc and you can just type `:w!!` to accomplish the same thing:
```
" Allow saving of files as sudo when you forgot to start vim w/ sudo
cmap w!! w !sudo tee > /dev/null %
```

## Why this works

In `:w !sudo tee %`...
`%` means "current file" (just as when searching, `:%s /blah...` means "search current file")
`!` means "run the following shell command"
`tee` is basically a pipe that sends output to 1) specified file (%=current file, in this case) and 2) standard out. 
(note, we don't really need to send it to stdout, hence the redirect to /dev/null in the key mapping)

## Reference
https://stackoverflow.com/questions/2600783/how-does-the-vim-write-with-sudo-trick-work
