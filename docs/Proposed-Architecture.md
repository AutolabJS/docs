**NOTE:** This page is a work in progress.

### Architectural Principles ###
Architectural principles are listed here in the descending order of priority.

1. **Transactions**    
    1. There is a clear treatment of each evaluation request as a transaction. There would be a clear traceability of all transactions.
    1. Two equivalent submissions that are equivalent from tests point of view would receive same evaluation
1. **Security**    
    1. All services communicate securely.
    1. All the evaluation transactions happen securely and are verifiable by examination committee (audit team).
    1. Upon permission from instructor, a student can verify an evaluation transaction.
    1. Protection against cheating or plagiarism.
1. **Liveliness**    
    1. System would not contain any dead components / code / parts. Reducing the lines of code footprint of the system is a priority.
    1. Rarely used parts of the code become optionally installable plug-ins
1. **Interoperability**    
    The core competence of the system is _automatic program evaluation at scale_. This evaluation service is to be available as a service. All other peripheral services such as user-interface are better outsourced to learning management systems such as Moodle.
1. **Collaboration**
    1. Three kinds of collaboration -- Teacher-student, Teacher-Teacher and Student-Student collaborations -- are to be naturally enabled.
    1. Concurrent, recursive workspaces to facilitate three kinds of collaboration.
    1. A yardstick of collaboration is to make the collaboration as easy as group study with  on-demand, real-time result verification from the system.
1. Follow **Microservices Architecture** by adhering to the principles of: 
    1. **Resilience**    
        * Each service would have multiple running instances to provide service in case of failure. Failure of one service does not fail the system. The system fails gracefully.    
        * Under no circumstances, can the user code or plug-ins break the functionality of the system.
    1. **Modularity**    
        * Each service is implemented using a single module / component / object.
        * All communications between objects is via REST messages
    1. **Monitoring**    
    There would be a separate monitoring service to log and monitor the real-time performance of the system
    1. **Distributed system**    
    All the components are going to be distributed on Internet. This is especially true for evaluation nodes.
    1. **Automation**    
    The system should be installable, operable, maintainable, upgradable by a single instructor for up to 10,000 students
    1. **Evolution with Backward Compatibility**    
    Components behave nicely and have backward compatibility with older components. Upgrade of any part of the system would only enhance the functionality of the system. A part upgrade should never degrade or break the system.
1. **Mobility**    
    All the service instances should have the mobility. A running service instance can be shutdown in one computer and respawned in another computer. None of the other dependent service instances would notice the mobility.
    Use **late binding** idea aggressively to support mobility.


### Design Principles ###
Follow object-oriented analysis and design. Make each service instance correspond to one object. Provide a system-wide unique name for each service end point. 

### Physical Architecture ###
Show an architectural diagram with

*. Match the architecture with domain metaphor    
    All components of physical architecture must be understood by a non-CS instructor.
* microservices architecture with service discovery ideas from [seneca.js](http://senecajs.org/)
* identity and distributed discovery using ideas from scaling websites, Internet, MIT Reed's paper
* distributed, trust worthy evaluation on student's computers using exam protocols. 
* extreme automation and small footprint
* multiple front-ends, one load balancer, one time capsule, one gitlab, multiple execution nodes


#### References ####
1. Design Principles behind Smalltalk, Dan Ingalls [paper](http://www.cs.virginia.edu/~evans/cs655/readings/smalltalk.html)
1. [TLS Seminar](https://tlseminar.github.io/) by Prof David Evans
1. Distributed synchronization architecture implemented in [Open Cobalt](http://www.opencobalt.net/about/synchronization-architecture) and [Croquet](https://en.wikipedia.org/wiki/Croquet_Project)
1. Croquet - A collaborative system architecture [paper](http://liacs.leidenuniv.nl/~verbeekfj/courses/hci/Croquet2003-paper.pdf)
1. David Reed's - [atomic actions](https://pdfs.semanticscholar.org/a05c/a97c7128fe9b74b550896291797f1573dcd2.pdf), naming and synchronization in decentralized system.
1. Thought Works [microservices page](https://martinfowler.com/microservices/) [paper](https://martinfowler.com/articles/microservices.html)
1. See the collaborative workspaces as implemented in _Croquet_ and _Open Cobalt_.
1. Remark!: A Secure Protocol for Remote Exams, Rosario Giustolisi
1. See chapter on Coordination by Peter Denning and Thomas Malone which is part of the book "Interactive Computation", Dina Goldin (ed) et al., Springer, 2006.    
    They talk about action loops, CoS
1. [seneca.js](http://senecajs.org/)
1. Service registry and discovery - [SWIM in Seneca](https://github.com/senecajs/seneca-mesh), [Consul](https://www.consul.io/), [etcd](https://coreos.com/etcd), [zoo keeper](http://zookeeper.apache.org/)
1. Scaling web applications - [Brandon Cannaday](https://www.youtube.com/watch?v=TsOySquMh3A), [Chander Dhall](https://www.youtube.com/watch?v=tQ2V9QSv48M), [AWS Way](https://www.youtube.com/watch?v=n28lDDdlnVg)
1. Thoughtworks videos on Microservices Architecture - [Sam Newman](https://www.youtube.com/watch?v=PFQnNFe27kU), [Martin Fowler](https://www.youtube.com/watch?v=wgdBVIX9ifA), [Neal Ford](https://www.youtube.com/watch?v=pjN7CaGPFB4), [James Lewis](https://www.youtube.com/watch?v=ijhoQ0PKJ0A)
1. Microservices at Netflix - [Netflix](https://www.youtube.com/watch?v=57UK46qfBLY), [Netflix evolution](https://www.youtube.com/watch?v=CZ3wIuvmHeM)
1. Node.js with redis - [1](https://www.youtube.com/watch?v=0g9Jag4az0g), [tutorial](https://www.youtube.com/watch?v=9S-mphgE5fA)
1. Service monitoring and visualization - [spigo](https://github.com/adrianco/spigo)
1. [DevOps Bookmarks](http://www.devopsbookmarks.com/) - a list of open source DevOps tools
1. DB comparison - [mysql vs postgres](http://vschart.com/compare/postgresql/vs/mysql), [postgres vs couchDB](http://vschart.com/compare/postgresql/vs/couchdb)
