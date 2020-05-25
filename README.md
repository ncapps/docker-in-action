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

### Chapter 5. Single-host networking
- Create containers with network exposure appropriate for the application you're running
- Use network software in one container from another
- Understand how containers interact with the host and the host's network
- *Networking* is all about communicating between processes that may or may not share the same local resources
- A *protocol* with respect to communication and networking is a sort of language. Two parties that agree on a protocol can understand what the other is communicating.
- A *network interface* has an address and represents a location. A network interface has an *IP address* which is defined by the Internet Protocol.
- IP addresses are unique in their network and contain information about their location on their network
- Computers commonly have an *Ethernet* interface and *loopback* interface
- *Ethernet interface* is used to connect to other interfaces and processes
- *Loopback interface* uses network protocols to communicate with other programs on the same computer
- A *port* is like a recipient or a sender. Several programs might receive messages at a single address.
- Ports are just numbers and defined as part of the Transmission Control Protocol (TCP) or User Datagram Protocol (UDP)
- Ports are written on TCP messages just as names are written on envelopes
- A bridge is an interface that connects multiple networks so that they can function as a single network
- A container attached to a Docker network will get a unique IP address that is routable from other containers attached to the same Docker network
- Docker networks have their own life cycle and are not bound to other objects
- By default, Docker includes three networks: `bridge, host, none`
- The `bridge` network uses the `bridge` driver and provide intercontainer connectivity for all containers running on the same machine
- Containers on the `host` network interace with the host's network stack like uncontained processes
- The `none` network uses the `null` driver and do not have connectivity outside themselves
- The *scope* of a network can take three values: `local, global, swarm`
- Bridge networks use network address translation (NAT) to make all outbound container traffic with destinations outside the bridge network look like it is coming from the host itself
- *Domain Name System (DNS)* is a protocol for mapping hostnames to IP addresses. This mapping enables clients to decouple from a dependency on a specific host IP and instead depend on whatever host is referred to by a known name
- DNS is a tool for changing outbound traffic behavior
- Firewall and network topology are tools for controlling inbound traffic
- Docker networks are first-class entities that can be created, listed, and removed just like containers, volumes, and images
- Bridge networks are special kind of network that allows direct intercontainer network communication with built-in container name resolution
- Docker provides tow other special networks by default: `host` and `none`
- Networks created with the `none` driver will isolate attached containers from the network
- A container on a host network will have full access to the network facilities and interfaces on the host
- Forward network traffic to a host port into a target container and port with *NodePort* publishing
- Docker bridge networks do not provide any network firewall or access-control functionality
- The network-name resolution stack can be customized for each container. Custom DNS servers, search domains, and static hosts can be defined
- Network management can be externalized with third-party tooling and by using the Docker `none` network

### Chapter 6. Limiting risk with resource controls
- A *context switch* is the task of changing from executing one process to executing another. Context switching is expensive and may cause a noticeable impact on performance of the system.
-  The linux user database is stored in a file located at /etc/passwd
- Docker uses `cgroups`, which let a user set memory limits, CPU weight & limits, and core restrictions as well as restrict access to specific devices
- Docker containers each have their own IPC namespace that can be shared with other containers or the host in order to facilitate communcation over shared memory
- Docker supports isolating the USR namespace. By default , user and group IDs inside a container are equivalent to the same IDs on the host machine. When the user namespace is enabled, user and group IDs in the container are remapped to IDs that do not exist on the host.
- You can and should use the `-u` option on `docker container run` and `docker container create` to run containers as nonroot users
- Avoid running containers in privileged mode whenever possible
- Linux capabilities provide operating system feature authorization. Docker drops certain capabilities in order to provide reasonably isolating defaults.
- The capabilities granted to any container can be set with the `--cap-add` and `--cap-drop` flags
- Docker provides tooling for integrating easily with enhanced isolation technologies such as seccomp, SELinux, and AppArmor. These are powerful security tools.

### Chapter 7. Packaging software in images
- `docker container diff` shows you all the filesystem changes that have been made inside a container
- `docker container commit` creates an image from a modified container. `-a` signs the image with an author string. `-m` sets a commit message. This commits a new layer to an image.
- An *entrypoint* is the program that will be executed when the container starts
- Use the `--entrypoint` flag to set the entrypoint
- The root filesystem is provided by the image that the container was started from. That filesystem is implemented with a union filesystem.
- A union filesystem is made up of layers. Each time a change is made to a union filesystem, that change is recorded on a new layer on top of all of the others. The *union* of all those layers, or top-down view, is what the container sees when accessing the filesystem
- Union filesystems **copy-on-change**
- A *repository* is roughly defined as a named bucket of images. More specifically, repositories are location/name pairs that point to a set of specific layer identifiers
- Repository name = REGISTRY_HOST/USER_NAME/SHORT_NAME
- Eaach repository contains at least one tag that points to a specific layer identifier
- If you pull a repository without specifying a tag, Docker will try to pull an image tagged with `latest`.
- You can pull all tagged images in a repository by adding the `--all-tags` option
- Repositories and tags are created with the `docker tag`, `docker commit`, or `docker build` commands
- If you want to copy an image, you need only to create a new tag or repository from the existing one
- Every repository contains a `latest` tag by default. That will be used if the tag is omitted
- `docker image history` examine all the layers in an image
- You can flatten images by saving the image to a TAR file with `docker image save`, and then importing the contents of that filesystem back into Docker with `docker image import`.
    - That's a bad idea because you lose the original image's metadata, it's change history, and any savings customers might get when they download images with the same lower levels
- Create image branches using Dockerfiles to manage image size
- `docker container export` will stream the full contents of the flattened union filesystem to stdout or an output file as a tarball
- `docker import` will stream the content of a tarball into a new image
- Statically linked programs have not external file dependencies at runtime. This means this statically linked version of "Hello, World" can run in a container with no other files.
- The understanding that every repository contains multiple tags and that multiple tags can reference the same image is at the core of a pragmatic tagging scheme
- A repository maintainer should always make sure that its repository's `latest` refers to the latest *stable* build of its software instead of the true latest
- When software dependencies change, or the software needs to be distributed on top of multiple bases, then those dependencies should be included with your tagging scheme
**Summary**
- New images are created when changes to a container are committed using the `docker container commit` command
- When a container is committed, the configuration it was started with will be encoded into the configuration for the resulting image
- An image is a stack of layers that's identified by it's top layer
- An image's size on disk is the sum of the sizes of its component layers
- Images can be exported to and imported from a flat tarball representation by using the `docker container export` and `docker image import` commands
- The `docker image tag` command can be used to assign several tags to a single repository
- Repository maintainers should keep pragmatic tags to ease user adoption and migration control
- Tag your latest *stable* build with the `latest` tag
- Provide fine-grained and overlapping tags so that adopters have control of the scope of their dependency version creep


## Attribution
Docker in Action, Second Edition by Stephen Kuenzli, Jeffrey Nickoloff, Manning Publications, 2019
