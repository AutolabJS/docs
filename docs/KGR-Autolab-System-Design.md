# Architecture

The diagram below is a high level representation of how the application works.  
[[images/architecture.png]]

# Components
The application has 5 main components:  
1. GitLab Server to push code.  
2. MySQL server to store scores.   
3. Web Server which acts as UI and controls submission requests alongside lab management.  
4. Execution nodes to evaluate the submission and return the score.  
5. Load Balancer which assigns an execution node to be used for a submission.

# Description
1. The Web Server reads the configuration file which has information regarding the lab like lab name, start time etc. and initializes relevant tables in the database.
2. The student pushes code to the GitLab server. 
3. The student selects the lab in the web server and the enters ID number to  start the evaluation. 
4. The web server forwards the request to the load balancer.
5. The load balancer assigns one of the execution nodes to the submission.
6. Execution node then pulls the test code and the submission from the GitLab server and starts the evaluation procedure.
7. The scores are returned to the load balancer and the node is added back to the queue.
8. The scores are updated in the database.
9. The load balancer pulls the submission from the GitLab server and makes a copy of the final solution with maximum score.
10. The scores are forwarded to the Web Sever to be displayed to the user.
11. The scores are shown on the frontend.


# UML using PlantUML
* Activity diagrams

1) To check the authenticity of submission

[[https://cloud.githubusercontent.com/assets/9445462/25675510/571536d8-305c-11e7-8dee-6529de95e05f.png]]

    @startuml
    start
    partition Initialization {
        :connection;
        :init labs;
    }
    if (legit_submission) then (yes)
      :submit to load_balancer;
    else (no)
      :submission_pending;
    endif

2) To check if new score is greater than the previous one

[[https://cloud.githubusercontent.com/assets/9445462/25675544/7e21a95a-305c-11e7-888c-b883a3dbb53d.png]]

    @startuml
    start
    :get_score from executionnode;
    if (score greater than previous) then (yes)
      :update score and code in mysql;
    else (no)
      :continue;
    endif

* Sequence diagram

1) Status request from user

[[https://cloud.githubusercontent.com/assets/9445462/25675550/829efa78-305c-11e7-9d71-3acfbc033421.png]]

	@startuml
	actor user
	entity mainserver
	entity loadbalancer
	entity executionnode
	user-> mainserver : status
	activate mainserver
	mainserver -> loadbalancer :connectionCheck
	activate loadbalancer
	loadbalancer -> executionnode :connectionCheck
	activate executionnode
	executionnode -> loadbalancer :response
	deactivate executionnode
	loadbalancer -> mainserver :response
	deactivate loadbalancer
	mainserver -> user :response
	deactivate mainserver
	@enduml


2) Lab check from user

[[https://cloud.githubusercontent.com/assets/9445462/25675535/70090142-305c-11e7-9959-7ba6107d1c39.png]]

	@startuml
	actor user
	entity mainserver
	database mysql
	user-> mainserver : /scoreboard/:Lab_no
	activate mainserver
	mainserver -> mysql :query for lab 
	mainserver -> user :response
	deactivate mainserver
	@enduml

3) submission event from user

[[https://cloud.githubusercontent.com/assets/9445462/25697633/5a709e94-30d9-11e7-8dd2-665405c13a5c.png]]

	@startuml
	actor user
	entity mainserver
	database mysql
	entity loadbalancer
	entity executionnode
	entity gitlab
	user -> gitlab :save_code
	user-> mainserver : submission
	activate mainserver
	mainserver -> loadbalancer :submit
	activate loadbalancer
	loadbalancer -> executionnode :requestrun
	activate executionnode
	executionnode ->gitlab :get_code
	activate gitlab
	gitlab -> executionnode :code
	deactivate gitlab
	executionnode -> loadbalancer :sendScores
	loadbalancer -> mysql :save_code
	deactivate executionnode
	loadbalancer -> mainserver :results
	deactivate loadbalancer
	mainserver -> user :scores
	deactivate mainserver
	@enduml