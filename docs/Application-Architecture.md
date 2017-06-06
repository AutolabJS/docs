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

# Notes
1. Load balancer pushes the scores in the database instead of the main server. This is because scores reach the main server by a route `/results` and a user can mock that request and update scores in the database. We can solve this problem by using socket-level authentication with config file and SSL certificate pinning for extra measure of caution.
