# Prevent iTunes from Opening

iTunes has a bad habit of opening when you don't want it to. For example, when
you hit the Play/Pause button.

If you never want to use iTunes for anything, the quickest way to prevent it
from opening is to just remove the execute permission:

`sudo chmod -x /Applications/iTunes`

This works as of Sierra (without having to disable SIP) but knowing Apple,
that could change (or it could restore its original permissions without
asking).
