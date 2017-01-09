# Pretty Colors

Print a bunch of pretty colors to terminal with a snippet of bash:

`yes "$(seq 16 231)" | while read i; do printf "\x1b[48;5;${i}m%${COLUMNS}s\n" " "; sleep .02; done"]"`
