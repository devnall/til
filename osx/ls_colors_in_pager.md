# Getting `ls` colors working on OSX when piping to a pager

## Setting colorflag

OS X doesn't use gnu ls, so the color flag for ls is weird in OSX.

For portable rc files, it means you have to set the flag based upon the OS
by doing something like this:

```
if ls --color > /dev/null 2>&1; then # GNU ls
  colorflag="--color"
else #OSX ls
  colorflag="-G"
fi
```

then declare your ls aliases using something like:

```
alias l='ls -lAhF ${colorflag}'
alias ll='ls -lhF ${colorflag}'
etc.
```

## Sending to a pager

That still doesn't work on OSX when you pipe the output to a pager like less,
the pager won't display color.

OSX needs `CLICOLOR_FORCE=1` before the `ls` command.

Also, the pager needs to display raw control characters (in this case, the color
escape sequences).

For `less`, this means the `-R` argument.

```
alias lsal='CLICOLOR_FORCE=1 ls -lahF ${colorflag} | less -R'
```

h/t http://mockingeye.com/piping-ls-through-less-with-colors-on-mac-os/
