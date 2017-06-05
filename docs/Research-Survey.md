## CS50 ##
CS50 is the introductory computer science course at Harvard University taught by Prof David J Malan. The instruction team historically evolved the instruction platform from a classic UNIX server cluster in University (2009). Over the next two years (2009-2011), the instruction team migrated to Amazon EC2 cluster which helped host the course for 700 students at a cost of $4665 per semester in 2011. In 2012, the instruction team released a virtual machine based on Fedora distribution. The installation scripts and `yum` packages were created for installing the needed course software. The virtual appliance gives complete administrative privileges to the students. Students can use the same VM for other CS courses and customize the VM as per their wishes.

Right now, the architecture of CS50 course software is best illustrated using the following diagram.

[[images/cs50-architecture.png]]

On the server side, the crucial components are *CS50 Sandbox* which also contains *CS50 Check* component. Both *CS50 Sandbox* and *CS50 Check* provide REST API for interaction. CS50 Sandbox is responsible for executing user code in a temporary sandbox. User code is sent to the sandbox via a JSON HTTP request and a request for evaluation is submitted. The Sandbox setups temporary root permissions, sets limits on resource usage with the help of security enhanced Linux module (see strace, seunshare, pam_limits Linux commands). CS50 check runs a series of tests on the sandboxed code. The tests themselves are specified in json file as a set of chained tests with strict ordering. If test1 precedes test2 in order, then test1 must pass before test2 can be applied. This chaining has been implemented using javascript call backs.

In the sandbox, the following Linux commands are used.

* *strace* - to detect unnecessary calls to stdin, stdout and stderr
* *seunshare* - to restrict user (process) privileges using SELinux policies
* *pam_limits* - SELinux policy limits on CPU cycles, disk space, file descriptors, RAM on per-user basis

A summary of CS50 components are as follows.

* *CS50 Sandbox* - node.js server with HTTP REST API service. Takes files from user and sets up the evaluation sandbox.
* *CS50Run* - a web-based IDE code editor which calls CS50 sandbox API. This software is ACE C9 code editor.
* *CS50Check* - a sub-module of the sandbox. This module provides automation for running chained/dependent tests
* *VM* - a downloadable Ubuntu virtual appliance of 2GB in size. This appliance has all the required software pre-installed.
  
Interesting questions to ask:

1. Since the tests are written in Javascript, how modular are the tests. Is our way significantly better?
1. The *CS50Run* is a very good idea to integrate into the client-side submission script/application. This application can also reside in the secure VM appliance and provide local development environment for the user inside the VM appliance.
1. The packaging system of this project is amazing and is worth emulating.
1. Our GitLab integration solves a lot of software requirements used in CS50 like rsnapshots, dropbox.
1. The idea of serving the front-end files from a static server is worth emulating. Since the front-end node.js server is also offering REST API, the static files can be pulled from ngnix / apache.

Relevant literature is:

1. Malan, David J. "Moving CS50 into the cloud." Journal of Computing Sciences in Colleges 25.6 (2010): 111-120.
1. Malan, David J. "Cs50 sandbox: secure execution of untrusted code." Proceeding of the 44th ACM technical symposium on Computer science education. ACM, 2013.
1. Malan, David J. "From cluster to cloud to appliance." Proceedings of the 18th ACM conference on Innovation and technology in computer science education. ACM, 2013.

#### CS50 References ####

| | | | | |
|-----------------------------------------| ---------------------------------| ---------------------------------| ---------------------------------| ---------------------------------|
| [CS50 Sandbox code](http://cs.harvard.edu/malan/projects/) | [CS50 Appliance Download](http://mirror.cs50.net/appliance50/) | [CS50 Appliance Manual](https://manual.cs50.net/) | [Debian binaries](http://mirror.cs50.net/ide50/2015/dists/trusty/main/binary-amd64/) | [CS50 course](https://cs50.net/) |    
| [CS50 Sandbox readme](http://cs.harvard.edu/malan/sandbox50/readme.html) | [CS50 GitHub](https://github.com/cs50) | [with c9 webIDE](https://run.cs50.net/) |

    

