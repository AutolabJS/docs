The execution scripts usually placed in test_cases/ should be modular to minimize repetition. Also the standard parts of these scripts should be taken out of the lab_author's folder and placed permanently in execution_nodes/ code base. Having these scripts in user directory is leading to inconsistent and sometimes erratic experience for the instructor. More over, the amount of work needed to bootstrap the first lab of a course is too much for a novice instructor to bear.

At the same time, we don't want to lose the testing flexibility gained with having custom scripts in lab_author's directory. We should follow UNIX philosophy here to have sensible defaults for reducing the threshold of setting up a fresh lab. Whoever wishes to have full control over scripts gets it. We can control the configuration using a yaml config file at the top level of lab_author's repository.

The present structure of lab_author repositories is as follows.    
```shell
    author_solution             ---> contains the complete solution to the lab
        /java                   ---> contains Java-language solutions
             /lib               ---> contains any third-party Java libraries you would like to use for evaluation
        /c                      ---> contains C-language solutions
        /cpp                    ---> contains C++ 2011 language solutions
        /cpp14                  ---> contains C++ 2014 language solutions
        /python2                ---> contains Python2 language solutions
        /python3                ---> contains Python3 language solutions

    test_cases/                 ---> contains testcases to be run against submitted code
        /checks                 ---> any sample input / output text files to be used for evaluation
        /c                      ---> test cases for C language
        /cpp                    ---> test cases for C++ language
        /cpp14                  ---> test cases for C++ 2014 language
        /python2                ---> test cases for Python2 language
        /python3                ---> test cases for Python3 language
        /java                   ---> test cases for Java language
            /setup              ---> compile, execute and test-setup bash shell scripts
                compile.sh      ---> script to compile the code for each test (DON'T CHANGE THIS)
                executeTest.sh  ---> script to execute the code for each test (DON'T CHANGE THIS)
                Test1.sh        ---> script to complete first test (calls compile.sh, executeTest.sh)
                (one script for each test case)

    Driver.java                 ---> Language driver for Java (DON'T CHANGE THIS)
    (one driver exists for each language)

    execute.sh                  ---> orchestrating script for one submission (DON'T CHANGE THIS)
    test_info.txt               ---> text file containing an enumeration of all tests to be run
```

Suggested repository structure for the lab_author is:
```
lab_author/lab_name
    author_solution/
    test_cases/
        checks/
        scripts/ (optional language-specific setup / compile / execute scripts; 
                  needed only if non-standard steps are used)
    test_info.txt
    config.yaml
```

The standard items such as language-specific drivers and scripts can be placed in evaluation sub-directory of execution_nodes/ directory.    
```
evaluation/
    execute.sh
    README.md
    unit_tests/
        drivers/   (language-specific drivers)
        README.md
        test_cases/
            scripts/ (language-specific setup / compile / execute scripts)
    io_tests/
        README.md
        test_cases/
            scripts/ (language-specific setup / compile / execute scripts)
```


***

#### Offloaded Evaluation ####
At present, we assume that the execution script `execute.sh` iterates over `test_info.txt` to execute one test case at a time. Another alternative is to offload the complete evaluation to userland. If user is willing to take care of individual test cases and directly provide the `results/` directory, that mode should be supported as well. Certain testing and evaluation frameworks like [JUnit](junit.org) make it possible to run multiple test cases in one run. Doing that would save us enormous amount of setup time for each test case.

If we are going to use JUnit for complete evaluation userland in one step, then the following JUnit classes would be useful.

* [org.junit.runner](http://junit.org/junit4/javadoc/latest/org/junit/runner/package-summary.html) package: [JUnitCore](http://junit.org/junit4/javadoc/latest/org/junit/runner/JUnitCore.html), [Request](http://junit.org/junit4/javadoc/latest/org/junit/runner/Request.html), [Result](http://junit.org/junit4/javadoc/latest/org/junit/runner/Result.html) classes
* Other interesting JUnit classes
    * [Categories](http://junit.org/junit4/javadoc/latest/org/junit/experimental/categories/package-summary.html) - to run different kinds of tests (easy, moderate, hard); very useful for DSA kind of courses
    * [Result](http://junit.org/junit4/javadoc/latest/org/junit/runner/Result.html#getRunTime()) - the getRunTime() method provides run-time information of a test.
    * [Test](https://github.com/junit-team/junit4/wiki/Timeout-for-tests) - We can timeout tests as well
    * [Description](http://junit.org/junit4/javadoc/4.12/org/junit/runner/Description.html) - hierarchical description of test suite tree
    * [Parameterized Tests](http://junit.org/junit4/javadoc/latest/org/junit/runners/parameterized/package-summary.html)
    * [Manipulation](http://junit.org/junit4/javadoc/latest/org/junit/runner/manipulation/package-summary.html) - sort and filter test methods of a class