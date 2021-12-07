# pgadmin4-ssh-tunnel-dockerfile

Docker Compose recipe for running pgAdmin 4 as a Docker container with SSH keys shared by the host machine.

Based on [this StackOverflow question](https://stackoverflow.com/q/68438404/764906).

## Use case

As of late 2021 pgAdmin 4 macOS application is not compatible with Mac computers with the Apple M1 chip.
But it is still possible to run pgAdmin 4 in Docker on these machines.

But if you need to connect to remote Postgres servers that use SSH key authentication, the container needs
to hold a valid SSH key. It is quite practical to share the host machine's SSH keys instead of generating
keys for each of the containers and this Docker Compose recipe mounts the host's `~/.ssh` directory
to achieve this.

However, since the oficial Docker image for the ARM architecture uses a non-privileged user, the recipe
elevates the container role to `root` to be able to access the mounted host's SSH keys in pgAdmin
(connection preferences dialog / SSH Tunnel tab).
