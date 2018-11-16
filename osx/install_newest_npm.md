# Install Newest NPM

As of this writing, brew installing node installs an old version of NPM. To
install new version, do the following:
1. `ls /usr/local/lib/node_modules` and make a note of any packages to
   reinstall
1. `rm -rf /usr/local/lib/node_modules`
1. `brew uninstall node`
1. `brew install node --without-npm`
1. `echo prefix=~/.npm-packages >> ~/.npmrc`
1. `curl -L https://www.npmjs.com/install.sh | sh`
1. Add .npm-pachages to PATH:
```
export NODE_PATH="$HOME/homebrew/lib/node_modules"
export PATH="$HOME/.npm-packages/bin:$PATH"
```
1. Reinstall any packages deleted in the second step
