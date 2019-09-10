# Allow Running Unsigned Apps From "Unknown" Developers

When running an unsigned app from an "unknown" developer, MacOS throws an error:
"$app is damaged and can't be opened. You should move it to the Trash."

In 10.7 Lion and previous versions, you could go to System Preferences -> Security & Privacy -> General and set "Allow apps downloaded from:" to "Anywhere" but that option was removed in Sierra.
Now it's necessary to use the `spctl` CLI tool to disable Gatekeeper.
`sudo spctl --master-disable`

To re-enable Gatekeeper:
`sudo spctl --master-enable`

## References
https://en.wikipedia.org/wiki/Gatekeeper_(macOS)
https://macreports.com/app-is-damaged-and-cant-be-opened-you-should-move-it-to-the-trash-fix/

