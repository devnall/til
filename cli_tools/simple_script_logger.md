# Simple logging function for bash scripts

Put this somewhere at/near the top:
`SCRIPT_NAME=$(basename "$0")`

Define this function:
```
log_message() {
  LOG_FILE=${LOG_FILE?Must specify log file destination}
  MESSAGE=${1?Must specify message to log}
  NOW=$(date -u +"%Y-%m-%dT%H:%M:%S")
  printf "%s [${SCRIPT_NAME}] %s\n" "${NOW}" "${MESSAGE}" | tee -a "${LOG_FILE}"
}
```

Call it like so:
`log_message "The script is doing a thing!"`

Will also need to either define the LOG_FILE var at runtime, above the function, or change the LOG_FILE
line to something like:
`LOG_FILE=${LOG_FILE:-/var/log/myapp.log}`
