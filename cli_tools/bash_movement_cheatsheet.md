# Moving around efficiently in bash and zsh

## Useful (IMO)

### Cursor Movement

* `CTRL+a` - jump to the beginning of the line
    * Note: If CTRL+a is screen/tmux leader, use `CTRL+a CTRL+a`
* `CTRL+e` - jump to the end of the line
* `ALT+b` - jump backwards one word
* `ALT+f` - jump forwards one word
* `CTRL+xx` - jump between current cursor position and beginning of line (and back)

### Command Editing
* `CTRL+u` - delete to the beginning of the line
* `CTRL+k` - delete to the end of the line
* `ALT+d` - delete to the end of the word
* `CTRL+w` - delete to the beginning of the word
* `CTRL+y` - paste word or text that was cut using a deletion shortcut
* `ALT+u` - make uppercase from cursor to end of word
* `ALT+l` - make lowercase from cursor to end of word
* `ATL+t` - swap current word with previous word

## Less Useful (IMO)

### Cursor Movement

* `CTRL+f` - move forward one character
* `CTRL+b` - move backward one character
* `CTRL+d` - delete the character under the cursor
* `CTRL+h` - delete the character before the cursor
* `CTRL+t` - swap character under cursor with the previous character

### Command Editing

* `ALT+c` - capitalize to end of word
    * I'm using that keybind for fuzzy directory search, but capitalization's not particularly useful anyway IMO

