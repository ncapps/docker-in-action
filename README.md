# Docker in Action Notes
## Part 1. Process isolation and environment-independent computing
### Chapter 1. Welcome to Docker
- Docker takes a logistical approach to solving common software problems and simplifies your experience installing, running, publishing, and removing software.
- It a command-line program, an engine background process, and a set of remote services
- Container abstraction is at the core of its logistical approach
- Working with containers instead software creates a consistent interface and enables the development of more sophisticated tools
- Containers help keep your computers tidy because software inside containers can't interact with anything outside those containers, and no shared dependencies can be formed
- Docker doesn't provide container technology; it hides the complexity of working directly with the container software and turns best practices into reasonable defaults
- Docker works with the greater container ecosystem; that ecosystem is rich with tooling that solves new and higher-level problems
- `docker help` to get a description of all the docker commands

### Chapter 2. Running software in containers
- Containers can be run with virtual terminals attached to the user's shell or in detached mode
- By default, every Docker container has its own PID namespace, isolating process information for each container
- Docker identifies every container by its generated container id, abbeviated container id, or it's human-friendly name
- All containers are in any one of six distinct states: created, running, restarting, paused, removing, or exited
- The `docker exec` command can be used to run additional processes inside a running container
- A user can pass input or provide additional configuration to a process in a container by specifying environment variables at container-creation time
- Using the `--read-only` flag at container-creation time will mount the container filesystem as read-only and prevent specialization of the container
- A container restart policy, set with the `--restart` flag at container-creation time, will help your systems automatically recover in the event of a failure
- Docker makes cleaning up containers with the `docker rm` command as simple as creating them

## Attribution
Docker in Action, Second Edition by Stephen Kuenzli, Jeffrey Nickoloff, Manning Publications, 2019
