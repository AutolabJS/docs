# Microservices architecture

Microservices is a software based system architecture which supports the construction of complex applications out of smaller independent processes that exist as standalone mini-applications in their own right.Each component has its own allocated storage, memory or CPU resources.

Microservices are usually used with containers.Containers isolate microservice processes and applications into smaller instances that utilize only the virtualized operating system rather than the full virtual machine and the entire complement of abstracted hardware that VM includes.

One of the major driving forces behind any kind of architectural solution is scalability.So, instead of deploying the entire application only once everyone is done, developers can deploy their respective services independently without waiting for the others to finish their modules. This not only improves developer time management, but also offers them much more flexibility to change and redeploy their modules without needing to worry about the rest of the application’s components

The advantages of microservices compared to monolithic design are as follws:-
Improves fault isolation: larger applications can remain largely unaffected by the failure of a single module.
Eliminates long-term commitment to a single technology stack: If you want to try out a new technology stack on an individual service, go right ahead. Dependency concerns will be far lighter than with monolithic designs, and rolling back changes much easier. The less code in play, the more flexible you remain.
Makes it easier for a new developer to understand the functionality of a service.

The application has 5 microservices:-
1) GitLab Server
2) MySQL Server
3) Web Server(main server)
4) Load Balancer
5) Execution Node

# Socket.io protocol operations and sample usage

The socket.io protocol can be delivered over a variety of transports. Socket.io-client is the implementation of the protocol for the browser and Node.JS over engine.io-client.
Socket.io is the server implementation of the protocol over engine.io.

The state of the Socket.IO socket can be disconnected, disconnecting,
connected and connecting.The transport connection can be closed, closing, open, and opening.A simple HTTP handshake takes place at the beginning of a Socket.IO connection.
The handshake, if successful, results in the client receiving:

* A session id that will be given for the transport to open connections.

* A number of seconds within which a heartbeat is expected (heartbeat
timeout).

* A number of seconds after the transport connection is closed when the socket
is considered disconnected if the transport connection is not reopened (close
timeout).

At this point the socket is considered connected, and the transport is signaled
to open the connection.If the transport connection is closed, both ends are to buffer messages and
then frame them appropriately for them to be sent as a batch when the
connection resumes.If the connection is not resumed within the negotiated timeout the socket is
considered disconnected. At this point the client might decide to reconnect the
socket, which implies a new handshake.

Following events are already provided by socket-io:

Client-side events for socket.io object:
* connect
* disconnect
* reconnect
* reconnect_error
* reconnect_failed

Client-side events for socket object:
* connect
* error
* disconnect
* reconnect

Server-side events:
* connection / connect

## Server-side
    var http = require('http');
    var app = http.createServer(function(req, res){
            console.log('createServer');
    });
    app.listen(3000);
    var io = require('socket.io').listen(app);
    io.on('connection', function(socket) {
        io.emit('Server to Client Message', 'Welcome!' );
        socket.on('Client to Server Message', function(message){
            console.log(message);
            io.emit('Server to Client Message');       
        });
    });

## Client-side
    var socket = io.connect(':3000');
    socket.on ('Server to Client Message',
    function(messageFromServer){
    console.log ('server said: ' + messageFromServer);
    });


# Docker containers

Containers are an abstraction at the app layer that packages code and dependencies together. Multiple containers can run on the same machine and share the OS kernel with other containers, each running as isolated processes in user space. Containers take up less space than VMs (container images are typically tens of MBs in size), and start almost instantly.

The three major advantages of docker containers are as follows:

## Lightweight
Docker containers running on a single machine share that machine's operating system kernel; they start instantly and use less compute and RAM. Images are constructed from filesystem layers and share common files. This minimizes disk usage and image downloads are much faster.

## Standard
Docker containers are based on open standards and run on all major Linux distributions, Microsoft Windows, and on any infrastructure including VMs, bare-metal and in the cloud.

## Secure
Docker containers isolate applications from one another and from the underlying infrastructure. Docker provides the strongest default isolation to limit app issues to a single container instead of the entire machine.

All the microservices run inside of containers in our project.

Some of the basic commands to use while handling containers are as follows:
* docker build   -  Build an image from a Dockerfile
* docker cp   -  Copy files/folders between a container and the local filesystem
* docker exec  -   Run a command in a running container
* docker ps  -   List containers
* docker start  -   Start one or more stopped containers
* docker stop  -   Stop one or more running containers


