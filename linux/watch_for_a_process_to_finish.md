If you have, say, a long running process and you want to know
when it completes and what exit code it finishes with:
`(while sudo kill -0 $pid; do sleep 5; done) && echo "Finished $?"`

So, if PID 2498 is the one you care about:
`(while sudo kill -0 2498; do sleep 5; done) && echo "Finished $?"`

Basically, `kill -0` doesn't send a signal to the PID, instead it
checks to see if the current user has access to do anything with
the PID and, if so, watches for it to exit/send an exit code.

Or something like that. Docs are bad about `kill -0`, including
the `kill` manpage. I should read up on it, it seems really
useful.

Reference:
[1](https://stackoverflow.com/questions/11012527/what-does-kill-0-pid-in-a-shell-script-do)
[2](https://unix.stackexchange.com/questions/153544/alert-when-running-process-finishes)
