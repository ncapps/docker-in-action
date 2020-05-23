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


## Attribution
Docker in Action, Second Edition by Stephen Kuenzli, Jeffrey Nickoloff, Manning Publications, 2019
