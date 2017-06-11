The desirable features for the AutoLabJS software are listed below in the descending order of priority.    

1. After every evaluation in an execution node, the *results/* directory need to be committed back to the student repository.
1. Replicate and solve the serialization problem raised in [this issue](https://github.com/prasadtalasila/JavaAutolab/issues/19).
1. Containers have problems with files containing non-ascii characters. The reasons need to be known.
1. Correctly display _time of submission_ column on the scoreboard. See [issue #107](https://github.com/AutolabJS/AutolabJS/issues/107).      
1. Provide log display settings for each lab. See the related [notes](https://github.com/AutolabJS/AutolabJS/wiki/FR-Logs-to-User) and [issue](https://github.com/AutolabJS/AutolabJS/issues/164).     
1. Show server time in the top-menu with a clock ticking. Use moment.js on the client side to fulfill this requirement.
1. Make the repository structure semantically close with language names from drop-down menu of submit page. We can provide folder name in the brackets language name in the drop down menu.    
1. Provision for explicit specification of author solutions repository. See [issue #46](https://github.com/AutolabJS/AutolabJS/issues/46).
1. Give helpful debug log messages for two frequent mistakes -- missing file, missing directory.    
1. Preserve the last entered form settings on the submit form page. This would reduce the submission work for the student. Use cookies for this feature. See libraries - [cookies.js](https://developer.mozilla.org/en-US/docs/Web/API/Document/cookie/Simple_document.cookie_framework), [scott hamper](https://www.npmjs.com/package/cookies-js)    
1. Revaluation button in admin section. Once a revaluation is requested, take the list of students from DB table, revaluate for all the commits of specified lab and add an extra column in the existing lab scores table. Once the instructor approves the suggested changes, update the lab scores column from revaluation column. See [FR notes on this feature](https://github.com/AutolabJS/AutolabJS/wiki/FR-Processing-of-Evaluation-Requests)    
1. Script to initialize course, instructor, students and projects for a course. The script can use GitLab API to complete this step.    
1. Single commandline interface for AutolabJS administration. See [autolabctl](https://github.com/AutolabJS/AutolabJS/wiki/FR-autolabctl) feature request.       
1. Addition of socket.io event on client and main server to fetch the score of a user.
1. A script to check for installation problems. This verification script would be run immediately after installation, addition of new execution nodes or with reconfiguration of any of the AutolabJS components. This would ideally be an [electron](https://electron.atom.io/)-based package.    
1. Add gitlab live check to status page. Gitlab has health check token and status check URLs for all the components available on https://<base-url>/admin/health_check    
1. Use ORM module in load balancer to interact with DB. A good use of ORM module would also protect the software against SQL injection attacks. See [Sequelize.js](http://docs.sequelizejs.com/en/v3/). Also migrate from MySQL to PostgreSQL. PostgreSQL supports JSON data type.
1. Log support with various log-levels using [winston library](https://github.com/winstonjs/winston).
1. Provision for environment variables where ever needed. No hard coding of filenames. Even magic constants, if any, will become environment variables.
1. Automated update script. Again, this would ideally be an Ansible package.
1. _commit hash_ and _programming language_ columns in scoreboard. The scoreboard would also have title showing the lab name.
1. Simplify the directory structure for basic labs like "C Programming" and "Data Structures and Algorithms". If there is a lab composer for instructor, that would be useful.
1. Document source code using [jsdoc](http://usejsdoc.org/).
1. Give warning message to user when a browser's back button is pressed.  Inform the user of a way to go to home page. If the user still wishes to go back to a previously visited website, let the user exercise that option.
1. Refactor the execution.sh script into template approach. Provide a webpage to administrator for composing changing parts of the execution.sh. The newly created execution.sh gets committed to the lab_author/lab# repository. By default, support unit testing strategy. We may also think about migration scripts in execution nodes to a javascript/python environment.
1. Refactor load balancer into two sub-components. One is responsible for communication with other components. Another one is responsible for scheduling and dynamic provisioning of execution nodes. [See issue #35](https://github.com/AutolabJS/AutolabJS/issues/35).
1. Change the encryption library to libsodium (NaCl). All communication between web application / load balancer / execution nodes must be using symmetric session key.
1. Add valid SSL certificates from [letsencrypt](https://letsencrypt.org/).    
1. Subnet access control restriction for each lab. Access logs at one place for both web application / client front end and gitlab. Have a separate module to detect and mitigate DoS attacks. This module acts as a application firewall for the AutoLabJS web application. Any DoS protection module must review the best practices of application firewalls. One of the requirements here would be to translate high-level administrator directives to low-level packet-level firewall filter rules. This is possible using API gateway module such as Kong. Before using Kong API gatway, contemplate its advantages over NGINX use case.        
1. Subject submission to plagiarism check using [jplag](https://github.com/jplag/jplag). JPlag works for C, C++, C#, Java and Scheme languages.    
1. Node.js CLI application to bootstrap a course. Similar applications are: gitlab-cli [1](https://github.com/der-On/gitlab-cli), [2](https://github.com/drewblessing/gitlab-cli), [3](https://github.com/narkoz/gitlab). Check github for similar projects before developing this on your own.
1. Security audit of the application.
1. Provide support for different testing strategies using testing libraries like JUnit, Mockito and Cucumber.    
1. Right now, each test requires separate compilation and run. If all tests belong to JUnit, we can use/refactor [JUnit](https://github.com/junit-team/junit) and [JUnitParams](https://github.com/Pragmatists/JUnitParams) to complete testing much more quickly. See JUnit runners, theories and results classes/packages. They are enormously helpful in cutting down the Java testing time by at least 80%.
1. Refactor the code base to be microservices architecture compliant. Before refactoring the architecture, select appropriate ER model for the database and move to a lighter, scalable database than MySQL. PostgreSQL may be an appropriate DB for persistence with redis being the cache. While doing this, we need to keep in mind the need to distribute the execution node to the student. We also need to think about the possibility of refactoring load balancer into two sub-components: one is load balancer which can be taken care of by HAProxy and other is the controller which is application specific.
1. Private scoreboard - give instructor an option to hide the scoreboard. In case of hidden scoreboard, summary statistical view can be provided for students.
1. Provide evaluation logs containing details like <submissionID, studentID, lab, commit hash, language, time, testcase status array, testcase marks array> for each lab to the instructor. We can have a submissionID generated in mainserver and stored as primary key for the evaluation log table. Log this information in a DB table and provide an export option. Also provide simple statistics for each lab.
1. Make the C driver (Driver.c) use exception handling using _setjmp()_ and _longjmp()_ functions. For concrete implementation ideas, see Chapter 13: Exceptions, [Object Oriented Programming with ANSI-C](https://www.cs.rit.edu/~ats/books/ooc.pdf), Prof. Axel Tobias Schreiner.

1. A different, rich view of scoreboard for instructor. The instructor's scoreboard must contain links to code directory of student, commit hash, programming language used, time of submission.
1. An *orchestrator/agent* component in a computer that runs execution nodes. The orchestrator can create / start / stop / destroy the execution nodes on demand from load balancer.
1. A portable *orchestrator/agent* component put on a live Linux distribution with a ready to run status. The security requirements must still be satisfied.    



# Date -- 10 August 2016     
## High priority bug fixes and enchancements-      
1. Prevent concurrent submissions of the same code (Issue #19).       

## Low priority bug fixes and enhancements-    
1. NodeJS wrapper to complete the initial configuration at install time. Moodle installation setup is a good example to emulate here.           
1. On-commit evaluations from command-line using one-step submission script.      
1. After revaluation, storing the revaluation scores in the database and displaying the same on the scoreboard.    
1. Prevent repeated submissions of the same code.      
1. Keep track of AutolabJS services using [ELK Stack](http://logz.io/learn/complete-guide-elk-stack/).
1. Package the application with a Vagrant box.  I think we can complement either of the approaches with a Vagrant template. The idea would be to give a Vagrant template similar to [Didit](https://github.com/maxg/didit) project, and let Ansible/Python packaging installer run inside the Vagrant VM. All the containers we are spawning can run in the Vagrant box. Since, we preallocate the memory to a vagrant virtualbox, all the containers get dedicated memory as well.    
1. Refactor load balancer as suggested in [this](https://github.com/AutolabJS/AutolabJS/issues/35) issue.    
1. Refactor view part of web application using react and redux libraries.    
1. Integrate [GitHub classroom](https://classroom.github.com/) into the web application part of AutolabJS.    

# Date -- 1 September 2016     
Following are a few articles discussing the pros and cons of AJAX and Nodejs Socket.io .      
1. https://dzone.com/articles/nodejs-speed-dilemma-ajax-or     
2. https://www.quora.com/Is-Socket-IO-more-scalable-than-AJAX      
3. http://stackoverflow.com/questions/7193033/nodejs-ajax-vs-socket-io-pros-and-cons       
