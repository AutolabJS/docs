Adherence to the following coding standards would be good.

1. What counts finally are the **Tested Features in Use**. 
1. Three values of any software are: features, simple design and feedback. Testing is the only way to simplify the design. So consider improvement in all the three values.    
1. A stable release is mandatory for stable and predictable end-user installation.    
1. Design and code should clearly articulate the interactions / stories / metaphors of the problem domain. PRACTICE DESIGN and IMPLEMENTATION in DOMAIN.    
1. Adherence to java script coding standards as prescribed by eminent authorities.
    1.  Java Script : The Good Parts, [Douglas Crockford](http://javascript.crockford.com/) / [Eloquent Javascript](http://eloquentjavascript.net/), Marijn Haverbeke.    
Before each commit, a committer runs [ESLint](http://eslint.org/), [JSHint](http://jshint.com/docs/cli/) and [JSLint Errors](http://jslinterrors.com/) on the code-base and fixes all the error and warning messages. 
    1. Shell scripts : Shell script coding standard by [Kfir Lavi](http://www.kfirlavi.com/blog/2012/11/14/defensive-bash-programming/) and [Robert Muth](http://robertmuth.blogspot.in/2012/08/better-bash-scripting-in-15-minutes.html). Before each commit, a committer runs [shellcheck](https://www.shellcheck.net/) on the code-base and fixes all the error and warning messages.    
1. All the new code commits shall have at least the unit tests. For JS, use [mochai](https://mochajs.org/) and [chai](http://chaijs.com/). For shell script, use [Bats](https://github.com/sstephenson/bats).    
1. Creation and adherence to coding standard checklist. At the moment, we are following the [project checklist](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-170-software-studio-spring-2013/projects/MIT6_170S13_proj-chklst.pdf) from MIT course, [6.170 Software Studio](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-170-software-studio-spring-2013/index.htm)
1. An issue reported should have a detailed bug report that can help replicate the problem.
1. Always maintain clean separation of coding, testing, integration, deployment and production stages. 
    1. **NEVER EVER CODE ON THE PRODUCTION SYSTEM**.

#### References ####

1. [RTF : A Metric Leading to Agility](http://ronjeffries.com/xprog/articles/jatrtsmetric/), Ron Jeffries.
1. [Measuring Agile Projects Using Running Tested Features Metrics](https://www.scrumalliance.org/community/articles/2016/august/measuring-agile-projects-using-running-tested-feat), Priyanjana Deb and Abhik Datta
1. [The Joel Test: 12 steps to Better Code](http://www.joelonsoftware.com/articles/fog0000000043.html), Joel Spolsky    
1. [Brian W Kernighan on Testing](https://www.cs.princeton.edu/~bwk/testing.html)    
1. [Worse is Better](http://web.mit.edu/6.033/www/papers/Worse_is_Better.pdf) [History](http://www.dreamsongs.com/WorseIsBetter.html)    
1. [Twelve-factor apps](https://12factor.net/)    
1. [Agile Manifesto](http://agilemanifesto.org/principles.html)    
1. [Software project best practices checklist](https://kkovacs.eu/software-project-best-practices-checklist), Kristóf KOVÁCS
1. Development process - [Mike Perks @ IBM](http://www.ibm.com/developerworks/websphere/library/techarticles/0306_perks/perks2.html)     
1. JB Rainsberger - [An introduction to Agile Software Development](https://www.youtube.com/watch?v=oT-5eIsRixA), [Economics of Software Design](https://www.youtube.com/watch?v=7HecgbghFTk)    
1. [CI best practices check list - Piotr Oktaba](http://continuousdev.com/2015/07/continuous-integration-best-practices-checklist/)    
