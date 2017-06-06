## Execution Nodes ##
### Secure Execution in Containers ###
We must strive to undertake secure execution of user code with bare minimal privileges. We initially thought of containers as a cost effective way of achieving the effect. The idea is to create a container in advance, keep the container running in anticipation of user request. Once an evaluation request comes, the user files are copied into the container via mapped volumes, evaluated inside the container, and the results are left in the mapped volume itself. At the end of the evaluation work, the container is stopped and deleted. Done this way, one users code evaluation has no way of influencing subsequent code evaluations. We can take advantage of Docker API and wrapper clients to perform the fast life cycle management of containers.

The overall code isolation should be better than achieved by SELinux-based user jail method used by CS50 check component. The backend library component of [INGInious](http://inginious.org/) has a controller component that does dynamic spawing of containers that are customized to each course / assignment. We can reuse this library. For further details, see the architecture section of the [INGInious paper](https://github.com/UCL-INGI/INGInious-papers-slides/raw/master/EMOOCs%202015/Automatic%20grading%20of%20programming%20exercises%20in%20a%20MOOC%20using%20the%20INGInious%20platform.pdf).    

See also the [Docker remote API](https://docs.docker.com/engine/reference/api/docker_remote_api/) for automating container lifecycle management.    


Misfit of P2P model
-------------------

For a long time, we were thinking about leveraging P2P model to outsource the deployment of execution nodes. There are two primary concerns with this model.

1. Security requirements are much more complex.
2. Cognitively, this deployment model is equivalent to a teacher asking the students to self-evaluate. It may be difficult for teacher / evaluator to accept such a model.

Instead, if we put emphasis on making the execution node infrastructure auto-scalable in a trusted environment, we get more tangible benefits.


Security Model
--------------
Each component of project currently uses asymmetric PKI using SSL certificates. This setup only provides secrecy, but not the authentication. We need to use symmetric key setup from NaCl (sodium) security library to provide symmetric security.





### Secure Evaluation in Untrustworthy Environments using Exam Protocols ###

1. Remark!: A Secure Protocol for Remote Exams, Rosario Giustolisi
1. Design and Analysis of Secure Exam Protocols, [Rosario GIUSTOLISI](https://sites.google.com/site/sarogiustolisi/) at University of Luxembourg [thesis](https://arxiv.org/pdf/1512.04751.pdf)
1. Trustworthy Exams Without Trusted Parties, Giampaolo Bella et al., Elsevier Computers & Security [paper](https://sites.google.com/site/sarogiustolisi/jw5_round2.pdf?attredirects=0&d=1), [another version](https://sites.google.com/site/sarogiustolisi/paper_189.pdf?attredirects=0)
1. A Secure Exam Protocol Without Trusted Parties, Giampaolo Bella et al., 2016 [paper](https://pdfs.semanticscholar.org/4b7a/8be7598c7ffcef7eb6573ad41f5cd0f47d67.pdf) [c,ode](http://apsia.uni.lu/stast/codes/exams/pv_isec15.tar.gz)
1. A SECURE ELECTRONIC EXAM SYSTEM, ANDREA HUSZTI, ATTILA PETHO [paper](http://www.agr.unideb.hu/if2008/kiadvany/papers/E21.pdf)
1. Formal Correctness of Security Protocols, [Bella, Giampaolo](http://www.dmi.unict.it/~giamp/) 
1. Papers of [Rosario Giustolisi](https://scholar.google.co.in/citations?user=oU-zeikAAAAJ&hl=en)

### Resource Usage Statistics ###
In order to be truly useful to algorithms courses, the execution node must collect the resource usage statistics of the user code after completion of evaluation.


## Load Balancer ##

### Refactor Load Balancer ###
The load balancer can be broken down into 2 conponents(LB1 and LB2) . One would handle communications with the main server, mysql and execution nodes.
The second would schedule the process and dynamically change the number of execution nodes.

Assumptions when devising a mechanism for addition/removal of nodes -   

1. The amount of time taken for execution of one submission is 5 seconds.
2. Out of all the pending jobs, each node gets a maximum of 5 submissions to execute.
3. Hence the maximum waiting time for each submission is 25 seconds.

The second component of the load balancer will have an array of unused ports from 8081 to 8181 from which the new nodes will be attached, one node_queue, array with all the available nodes and job_queue, array with all the pending jobs.

1. When LB1 recieves from the main server, forwards the request to LB2 as per the following algorithm:-    
`    if node is available : `    
     &nbsp;&nbsp;&nbsp;&nbsp;   `send the job with the scheduled node to LB1`    
    `else if number_of_jobs >= number_of_nodes*5 :`    
     &nbsp;&nbsp;&nbsp;&nbsp;   `create a new node, send the job with the new node to LB1`    
    `else : `    
     &nbsp;&nbsp;&nbsp;&nbsp;   `wait for a node to complete execution.`    

2. When LB1 receives a submission from one of the nodes, it forwards the score to the main server, and appends the database. The node details are sent to LB2 -    
`    if number_of_nodes*5 >= number_of_jobs :`    
     &nbsp;&nbsp;&nbsp;&nbsp;   `remove node`    
    `else :`    
     &nbsp;&nbsp;&nbsp;&nbsp;   `if job is pending :`    
           &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `send the job with the node_details to LB1 for execution`    
        &nbsp;&nbsp;&nbsp;&nbsp; `else :`    
             &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `add node to queue`    


