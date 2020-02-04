# Makefile `help` Boilerplate

This snippet adds a new `help` target to Make and sets it as the default
target (when there are no other arguments given).

```
.DEFAULT_GOAL:=help

# COLORS
GREEN  := $(shell tput -Txterm setaf 2)
YELLOW := $(shell tput -Txterm setaf 3)
WHITE  := $(shell tput -Txterm setaf 7)
RESET  := $(shell tput -Txterm sgr0)

TARGET_MAX_CHAR_NUM=20

.PHONY: help
## Show this help text
help:
    @echo ''
    @echo 'Usage:'
    @echo '  ${YELLOW}make${RESET} ${GREEN}<target>${RESET}'
    @echo ''
    @echo 'Targets:'
    @awk '/^[a-zA-Z\-\_0-9]+:/ { \
        helpMessage = match(lastLine, /^## (.*)/); \
        if (helpMessage) { \
            helpCommand = substr($$1, 0, index($$1, ":")-1); \
            helpMessage = substr(lastLine, RSTART + 3, RLENGTH); \
            printf "  ${YELLOW}%-$(TARGET_MAX_CHAR_NUM)s${RESET} ${GREEN}%s${RESET}\n", helpCommand, helpMessage; \
        } \
    } \
    { lastLine = $$0 }' $(MAKEFILE_LIST)
```

Use it by putting the help text on one line that begins with `##`, right above
the target:

```
.PHONY thing1
## Does a thing
thing1:
  exit 0

.PHONY thing2
## Does another thing
thing2:
  exit 0
```

It will output something like this (but colorized!):

```
Usage:
  make <target>

Targets:
  help                 Show this help dialogue
  thing1               Does a thing
  thing2               Does another thing
```
