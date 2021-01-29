# HOWTO Install a Specific Version of a Homebrew Formula

Homebrew got rid of their `version` subcommand and have made it much harder to
install an arbitrary, older version of a package. Their stance is that
homebrew should only ever install the newest version. Personally, I think
that's naive but whatever.

The homebrew maintainers did offer a means for installing older versions, it's
just not very intuitive or user-friendly. Alternately, you can do it manually
(which, honestly, isn't that much harder or more manual than doing it the
"official" way).

## The Official Way -- `brew extract`

1. First, you'll need a GitHub repo to act as your custom tap. It makes things
   easier if the tap name begins with `homebrew-`. I created a new repo named
   [github.com/devnall/homebrew-custom](https://www.github.com/devnall/homebrew-custom) 
   More info on creating a tap can be [found
   here](https://docs.brew.sh/How-to-Create-and-Maintain-a-Tap).
1. If another version of the formula is currently installed, unlink and/or
   uninstall it. `brew unlink terraform` and/or `brew remove terraform`
1. Use the `brew extract` command to search for a specific version of a
   formula and add it to your tap. E.G. for terraform 0.12.18 `brew extract
   --version=0.12.18 terraform devnall/homebrew-custom`
1. Install the version from your tap: `brew install terraform@0.12.18`
1. If you do a `brew leaves` or `brew info devnall/custom/terraform@0.12.18` you should see your
   version, from your tap.

## The "Unofficial" Way -- Install from and Pin to a Specific Commit Hash
1. If another version of the formula is currently installed, unlink and/or
   uninstall it. `brew unlink terraform` and/or `brew remove terraform`
1. Find the forumula/library that you're looking for at 
   https://github.com/Homebrew/homebrew-core/tree/master/Formula Note that
   GitHub webUI truncates the list so figure out the forumla name via `brew
   search` or clone the repo and look for the formula name locally.
1. Using the formula name, go to the master blob for that formula, e.g.
   https://github.com/Homebrew/homebrew-core/blob/master/Formula/terraform.rb
1. Click the `History` button to view old commits. If GitHub can't generate
   the history, clone the homebrew-core repo locally so you can search history
   that way.
1. Search for a commit that is updating the formula to the version you want to
   install. In the web browser, CTRL+F for the version number to find the
   commit hash. If you cloned locally, `git log master -- Formula/terraform.rb
   | grep -C 5 0.12.8`
1. Find the "raw" link for the commit. If in the browser, click the commit,
   then click "Raw". If you found the hash in the CLI, use it to find the
   commit in the browser to get to the raw link. The URL format is something
   like:
   https://raw.githubusercontent.com/Homebrew/homebrew-core/a1a1a1a1a1a1a1a1a1a1a1/Formula/terraform.rb
1. Brew install the raw URL: `brew install
   https://raw.githubusercontent.com/Homebrew/homebrew-core/a1a1a1a1a1a1a1a1a1a1a1/Formula/terraform.rb`
1. Pin the installed version so that it doesn't get upgraded accidently: `brew
   pin terraform`

## A Third Option

Someone made a tool to make it easier to search for a specific version, but it
hasn't been updated in a while so it's not actually useful. May be worth
forking if dealing with lots of older versions.
https://github.com/bagonyi/brewed

## Notes and References
* https://stackoverflow.com/questions/3987683/homebrew-install-specific-version-of-formula/
* https://stackoverflow.com/a/7787703/2729500
* https://docs.brew.sh/How-to-Create-and-Maintain-a-Tap
* https://docs.brew.sh/Manpage#extract-options-formula-tap
* https://github.com/Homebrew/brew/pull/4563
