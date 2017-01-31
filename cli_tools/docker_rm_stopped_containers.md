# Remove all exited Docker containers

`docker rm -v $(docker ps -qa -f status=exited)`
