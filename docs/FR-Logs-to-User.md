The display of logs to user after an evaluation. We can make the following choices.

| Instructor Preference | mode for logs |
|-------- |:----------:|
| No logs |  disable |
| Return compilation and run-time errors |  tools |
| Return program output |  output |
| Return stack trace log |  strace |

All the above listed modes except disable mode are disjoint. Thus the modes such as tools / output / strace can be combined to provide more complete logs.    

Typically, we don't return the program output for the fear of exposing the test cases. A student can always just print the input being received. Since inputs are the test case inputs, a student can always look at the test case inputs by just printing them to the terminal which is redirected to output log file. Students lose the facility of debugging using print statements on AutolabJS. Students seem to strongly prefer this facility. Would instructor's be comfortable with it? Should AutolabJS be used as a debug platform or an evaluation platform? More importantly, do we want to artificially separate debugging from evaluation which is against the spirit of TDD?        

Most likely, the choice and comprehensiveness of logs returned is a technical, local decision made by the instructor. Hence, there should be a support for all modes. The logs mode option selected by the instructor during lab setup is respected after the program execution. The main server uses labs.json to pick chosen log settings and insert the same into evaluation request json. The settings are passed on by the load balancer to the execution node. The execution node returns logs as per the setting.
