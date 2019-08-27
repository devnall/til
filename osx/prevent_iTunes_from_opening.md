# Prevent iTunes from Opening

iTunes has a bad habit of opening when you don't want it to. For example, when
you hit the Play/Pause button.

Prior to Mojave (or maybe High Sierra?) you could just `sudo chmod -x /Applications/iTunes` but that no longer works.
You could reboot into recovery mode and disable csrutil, chmod -x iTunes, re-enable csrutil, and reboot but it's a PITA.
Luckily, Apple announced in June 2019 that they're finally killing iTunes so hopefully it won't be a problem too much longer.
In the interim, the easiest solution is to run the free Overkill menubar app and let it automatically kill iTunes any time it opens.

`brew cask install overkill`

More info:
https://github.com/KrauseFx/overkill-for-mac
https://superuser.com/questions/1383264/prevent-itunes-opening-on-play-button-in-macos-mojave-stop-play-pause-button
