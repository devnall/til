# How to change the default screenshot location in MacOS

By default, OSX/MacOS saves screenshots to the Desktop.
I hate saving stuff to or seeing stuff on the Desktop.

1. Create a new directory for screenshots to be saved to:
`mkdir ~/Pictures/Screenshots`
2. Set that dir as the default save location for screenshots:
`defaults write com.apple.screencapture location ~/Pictures/Screenshots`
3. Restart the SystemUIServer:
`killall SystemUIServer`
