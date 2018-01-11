# Safer bash Scripts with `set -euxo pipefail`

The `set` builtin to bash provides some nice options to make your scripts perform more dependably or with some safeguards.

## Summary

For most scripts, use:
`set -eou pipefail`

For debugging scripts, use:
`set -eoux pipefail`

For scripts where you're using ERR traps, use:
`set -Eeou pipefail`

## `set -e`

Causes a script to exit immediately if a command within the script fails (that is, exits with a non-zero return code).
It's smart enough to not react to a fail within a conditional.
In the event you don't want a specific command within a script to cause it exit, you can append `|| true` to the command.

## `set -o pipefail`

Normally, bash only looks at the exit code of the last command of a pipeline. This isn't ideal, as it means the `set -e` option can only act on the last command in a pipeline.
The `set -o pipefail` option sets the exit code of a pipeline to the rightmost command that exits with a non-zero status. If all commands in the pipeline exit zero, it sets exit code of the pipeline to zero.
This goes with `set -e` like peanut butter and jelly.

## `set -u`

This option causes the shell to treat unset variables as an error and exit immediately.
Unset variables are a common cause of bugs in shell scripts, so treating then as an error is usually desirable.
This option is smart enough to handle `${a:-b}` variable assignments, to assign a default value `b` to an unset `$a` variable.
If you do want an unset variable (say, in a conditional where you're checking to see if the variable is set), you can use the above construct without setting a default value, e.g. `${a:-}`

## `set -x`

It cause bash to print each command before executing it. This one is mostly useful for debugging. 
Arguments get expanded before the command is printed, which causes logs to contain the actual, potentially sensitive, contents of the variable.

## `set -E`

If you use traps, specificlly the ERR trap, the `set -e` option will fail to fire the trap in some circumstances. If you're using traps that look like the following example and you're using the `set -e` option, you should also use the `set -E` option.
```
#!/bin/bash

trap "echo ERR trap fired!" ERR
```

### Source
https://vaneyckt.io/posts/safer_bash_scripts_with_set_euxo_pipefail/
