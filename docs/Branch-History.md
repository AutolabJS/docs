
#### Master ####
Contains the latest stable code. All the installations should either be from releases or from master branch. All the code commits onto this branch shall be via a branch merge from dev branch. No direct code commits here.

#### Dev ####
The bleeding edge of development. Contains merged code from development efforts of all the contributors. Once the desired stability is reached for a version of code, it is committed to master and released as a new version.

#### Dev-linted ####
Contains the code snapshot of development work done by Tejas Sangol, Gaurav Narula, Utkarsh Maheswari, and Rajat Agarwal. All the code from previous development has been retained for historic reference. The main_server.js, load_balancer.js and execution_node.js has been linted to remove simple errors. The linting work was done by Yash Singh (main_server.js), Ankshit Jain (load_balancer.js) and Kashyap Gajera (execution_node.js).


#### Dev-linted-update ####
Dev branch updated with only three files (main_server.js, load_balancer.js and execute_node.js) from **dev-linted** branch. This branch tries to check the compatibility of the linted code in **dev-linted** branch with the latest code base in the **dev** branch.


#### Dev-tests ####
The personal working branch of Prasad Talasila. All the work in progress of Prasad Talasila is pushed to this branch. Once the work is deemed complete, it is merged into Dev branch. No forks or merge requests to this branch.

#### Ansible-variables ####
This is the last work-in-progress of Gaurav Narula. Contains a way of separating ansible variables from inventory file. The work is for reference purposes only. The completeness of the work is unknown and should be deemed to be in non-working condition.
