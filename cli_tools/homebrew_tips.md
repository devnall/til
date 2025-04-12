# Homebrew Tips and Tricks

- If you have a package that was installed as a dependency of another package, and want to identify the parent:
	- `brew uses --installed <child_package>` - list all installed packages that depend on the specified package
	- `brew deps --tree --installed` - detailed dep tree for all installed formula

