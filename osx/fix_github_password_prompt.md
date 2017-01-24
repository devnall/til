# Fix Github Password Prompt

If github starts constantly prompting for a password, despite using git/ssh (rather than
HTTPS) and despite already having correct pub key on Github, it may be related to some keychain
helper changes that occured around El Capitan/Sierra.

This seems to have fixed it.

`ssh-add -K ~/.ssh/id_rsa &> /dev/null`
`eval "$(ssh-agent -s)"`
`ssh-add -A`
