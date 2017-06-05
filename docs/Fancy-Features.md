The following features would be nice to have, but are not a high priority right now.


1. Fast submission procedure:    
People were either slowed down by the two-step submission procedure or because of unavailability of logs. There could be multiple ways to make the submission faster:    
    1. Parallelization:    
    We could pursue the idea of dynamically changing the number of execution nodes. Also, we could look at evaluating the test cases in a submission in parallel (on a single or multiple nodes) and then aggregating the results. Execution of multiple testcases in parallel can be achieved inside one execution node using [docker-pm2](http://pm2.keymetrics.io/docs/usage/docker-pm2-nodejs/).    
    [Node.js cluster](https://nodejs.org/api/cluster.html) helps provide concurrent capabilities for Node processes. We can utilize the idea to improve main server and execution nodes. See [tutorial](http://rowanmanning.com/posts/node-cluster-and-express/)    

    1. Online in-browser IDE    
    This could really useful in solving directory structure based problems and would help people who don't want version control modify and submit code faster. We would need to add support for multiple tabs for multiple files - like in standard text editors. Interestingly, HackerRank also allows in-browser version control. The backend of this submission can be over GitLab.

    1. Auto-commit and evaluate request script on the client side

    1. BlueJ / Eclipse plugin:    
    This would involve some more work but would help in submission without leaving the coding window. I guess this can be an add-on over the evaluate script on the client-side.

    1. Event listener on GitLab:    
    Auto-evaluate on receiving a commit on GitLab. Not in the best spirit of version control though.


1. Submitting in pair-programming:
    Both students should be able to submit together. Although this is possible using Git, making the feature more explicit enhances the user-experience. Gitlab [project members API](https://docs.gitlab.com/ce/api/members.html) allows us to do this seamlessly.

1. Populate student repositories with starting code. This option should be available in /admin section. Make use of GitHub education package for this purpose.

1. Scoreboard and Statistics:
I guess we should add names (a feature request) on the scoreboard and also a feature to turn the scoreboard off if the instructor wants. Another interesting and engaging feature would be to add statistics for a lab and across labs in a course - not only the average marks, but also total across labs, the number of submissions by a user, average completion time and other such things. We have all the data and creating views should be easy enough.  

1. Misc:
    1. In-built plagiarism checker.    
    1. Minor UI fixes - back button takes you out of AutolabJS.    
    1. Accepting submission requests from non-existing usernames - I'm not sure if this bug has been fixed.   

1. Hacker Rank compatibility mode: the instructor only provides input and output files. The instructor does not have to write the language-specific test scripts.    

1. Date picker in /admin section. The graphic date picker would help solve the ease of use problem.

1. Create an execution cluster with one load balancer (NGINX or HAProxy) and N execution nodes. Based on install script, the number of execution nodes in the cluster (N) can change. Treat the execution cluster as one hot plug ready to install and use module. We can use the docker compose to clear the hot plug execution cluster. See the relevant documentation - [1](https://www.keithcirkel.co.uk/load-balancing-node-js/), [2](https://www.nginx.com/blog/5-performance-tips-for-node-js-applications/), [3](https://docs.docker.com/compose/)    
   For this execution cluster, it is safer to make the execution node image configurable. That way, we can continuously update the execution nodes and still have the stable execution cluster code.
   Another potentially useful Docker platform scenarios are [docker swarm](https://docs.docker.com/engine/swarm/) and [docker cloud](https://docs.docker.com/docker-cloud/)    

1. Create the docker-compatible continuous integration server for AutolabJS using Docker cloud.    

1. Time labs: Each student gets a fixed amount of time to solve the problem. After a student starts the assignment in Gitlab by making the first commit, the student will have the a maximum time limit to finish the assignment. After the time limit, the assignment becomes inactive for that specific user.    

1. Replace gitlab component with [gitolite](https://github.com/sitaramc/gitolite). See the gitolite [documentation](http://gitolite.com/gitolite/). Ideally we should be able to choose between gitlab and gitolite.    

1. Make Gitlab use non-standard ports for SSH, HTTP and HTTPS services so that the AutolabJS can be installed on a standard server setup with webserver and SSH running.    

1. Rebuild main server using sails framework with a front-end Kong API gateway. If Kong is not used, at least have NGINX gateway terminating TLS and serving static assets. See reviews [1](https://www.nginx.com/blog/nginx-nodejs-websockets-socketio/), [2](https://www.nginx.com/blog/5-performance-tips-for-node-js-applications/), stackoverflow - [1](http://stackoverflow.com/questions/16770673/using-node-js-only-vs-using-node-js-with-apache-nginx), [2](http://stackoverflow.com/questions/5009324/node-js-nginx-what-now?noredirect=1&lq=1), hardening node.js with nginx - [part-2](http://blog.argteam.com/coding/hardening-node-js-for-production-part-2-using-nginx-to-avoid-node-js-load/), [part-3](http://blog.argteam.com/coding/hardening-node-js-for-production-part-3-zero-downtime-deployments-with-nginx/)    

1. Have Kong gateway or another filter service filter incoming API based on three modes - learning mode, single lab mode, group lab mode, exam mode. Define resource access limits for each mode and enforce them using Kong gateway or service filter.

1. Allow students to specify the files names to be evaluated for IO-tests. This can be done through a config file at top-level of student repository. In reality though, only 5% of the students really need this feature.

1. Pop quiz in a class is an interesting quick assessment method to assess the reception of a concept taught just now. If we can make AutolabJS work for pop quiz for programming courses, that would be amazing. The hard requirements are: quiz setup time: 5 minutes, aggregation of multiple quiz questions into one group for evaluation, question-wise (may be anonymous) statistics to give a feedback to teacher.

1. Convert the submission times to user's local time zone. All the submission times are stored as unix time stamps and they are converted to user's local time using the browser JS code. A good candidate for this is github's [time-elements](https://github.com/github/time-elements). Also check other alternatives before choosing this one.

1. Create an encrypted course bundle. Those who want to distribute the course bundle can do so. Those who purchased / downloaded the encrypted course bundle can place the bundle in the autolab and have the students submit code against the exercises in the bundle. AutolabJS can evaluate and save the scoreboard.    
    A course bundle also helps with the bulk export and import of courses. In any academic setting, courses are repeated with a lot of repeating content. Thus bulk export and import are much needed features.
