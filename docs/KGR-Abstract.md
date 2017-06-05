# Abstract of Kashyap Gajera's report

The work was mainly based on improving the code quality of the project and making future commits testable by adding code climate and travis-ci tests in place. The initial part of the work was to improve the code climate score of the present code.
Travis-ci was used to test the PRs.These tests would run on every PR made to the main repository and would decide whether to merge the PR. Previously due to lack of such a testing framework,It was very difficult to keep track of commits made by everyone and to review the commits.

The tests mostly make sure that the website(front-end) components are working, the execution-node evaluations are giving the correct results with multiple simultaneous requests,the load-balancer updates the database on better scores,the Input-output testing for all the supported languages and exception handling of execution-node. 