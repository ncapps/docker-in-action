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

### Chapter 3. Software installation simplified
- Human users of Docker use repository names to communicate which software they would like Docker to install
- Docker Hub is the default Docker registry.
- The `docker` CLI makes it simple to install software that's distributed through alternative registries, TAR archives, or Dockerfiles
- The image repository specification includes a registry host field
- The `docker load` and `docker save` commands can be used to load and save images from TAR archives
- Distributing a Dockerfile with a project simplifies image builds on user machines
- Images are usually related to other images in parent/child relationships. These relationships form layers. When we install an image, we have installed a target image and each image layer in its lineage
- Structuring images with layers enables layer reuse and save bandwidth during distribution and storage space on your computer and image distribution servers

### Chapter 4. Working with storage and volumes
- A *volume"* is a tool for segmenting and sharing data that has a scope or life cycle that's independent of a single container
- Images are used for packaging relatively static files such as programs; volumes hold dynamic data or specializations
- A *polymorphic* tool is one that maintains a consistent interface but might have several implementations that do different things
- Unlinke shares based on bind mounts, named volumes enable containers to share files without any knowledge of the underlying host filesystem
- Volume plugins will help you solve problems associated with writing files on one machine and depending on them from another
- Mount points allow many filesystems from many devices to be attached to single file tree. 
- Every container has its own file tree
- Containers can use **bind mounts** to attach parts of the host filesystem into a container
- In-memory filesystems (tmpfs) can be attached to a container file tree so that sensitive or temporary data is not written to disk
- Docker provides anonymous or named storage references called **volumes**
- Volumes can be created, listed, and deleted using the appropriate `docker volume` subcommand
- Volumes are part of the host filesystem that Docker mounts into containers at specified locations
- Volumes have life cycles that are indepednent from containers and may need to be cleaned up periodically
- Docker can provide volumes backed by network storage or other more sophisticated tools if the appropriate volume plugin is installed

## Attribution
Docker in Action, Second Edition by Stephen Kuenzli, Jeffrey Nickoloff, Manning Publications, 2019
