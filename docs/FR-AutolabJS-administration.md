We want a single commandline interface with multiple options to perform routine administrative tasks of AutolabJS. The common operations performed are:

1. Install AutolabJS
1. Start/stop/restart the AutolabJS components on all machines.    
    A special case of this option is change the configuration and restart an AutolabJS component.
1. Update AutolabJS
1. Set / Change log levels
1. Get the status update on all the components    
    Status update contains live status of each of the components and their important performance metrics such as number of evaluations completed, health metrics.


We can implement a solution based on one of the following approaches.

1. Ansible commands
2. Shell script    
    The shell scripts themselves can be wrappers around Ansible commands we have now on the container maintenance page. A variation of shell script is a Make file used by [CS50](https://github.com/cs50/server/blob/master/Makefile). However, a make file-based approach is not as flexible as a shell script.

3. npm commands    
    An npm-based commands would integrate better with the rest of the application though. We can use the usual tricks of PM2, ShellJS to wrap shell scripts, ansible scripts etc. For a sample, see [whiteboard](https://github.com/prampey/Whiteboard).

4. dedicated npm package called AutolabJS which is similar to autolabcli    
    Since caporal.js implements all the best ideas of command-based interface, it is better to implement the autolabctl script using caporal.js. caporal.js is a library for building commandline apps in node.js [website](https://github.com/mattallty/Caporal.js), [tutorial](https://www.sitepoint.com/scaffolding-tool-caporal-js/)      

5. Web interface
    Apart from instructor section, we can also have a separate admin section where the administrative actions are performed are placed. Or we can merge the administrative work with instructor section.

### Architecture ###
We have to use an MVC architecture to separate the UI from controller and program logic. Done properly, we can easily change the view to make the autolabctl application work in GUI mode. Considering the choice of commandline / GUI mode usage, it is better to use electron-base to build the application.

One disadvantage of Electron-based application though is the initial startup size. As mentioned by @SebastinSanty, even a hello world Electron application is ~50MB in size. Such a huge size may be a deterrent for simple applications. Even more so, the faulty code base of 50MB coming into the application is certainly going to reduce the resilience of the application.

Questions to answer:

1. Why build another application? Why can't the administrative be part of autolabcli? A good example is azure crossplatform cli.
1. Why have two versions - CLI and GUI versions of the application?
1. What are the advantages of cli / GUI approach over web application approach?
1. Isn't the controller of MVC done Servlets way a simple control class forcing procedural programming paradigm on the whole MVC interaction?
