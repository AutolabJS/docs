List of tests to be implemented

1. Choice of testing libraries for the project

    | Kind of Tests | Library  |
    |-------- |:----------:|
    | Requirements tests | [cucumber](https://github.com/cucumber/cucumber-js) |
    | unit tests | [mocha](https://mochajs.org/) |
    | assertions library | [chai](http://chaijs.com/) |
    | test doubles | [sinon](http://sinonjs.org/), [jsmockito](http://jsmockito.org/), [mock-socket](https://github.com/thoov/mock-socket), [nock](https://github.com/node-nock/nock), [json-server](https://github.com/typicode/json-server) |
    | code coverage tool in travis | [istanbul](https://github.com/gotwarlost/istanbul) |
    | headless browser-based testing | nightmare.js |
    | (to be used with mocha and chai for functional tests) |  |
    | high-level selenium-driver with own assertions | nightwatch.js |
    | (easy to use; to be used with mocha for functional tests) |  |
    | low-level, but sensible selenium-driver | [webdriverIO](http://webdriver.io/) |
    | (to be used with mocha and chai for functional tests) |  |
    | Automation of browser tests | [Saucelabs](https://saucelabs.com/) |
    | Manual browser tests | [browserling](https://www.browserling.com/) |
    | Load tests | [artillery](https://artillery.io/) |
    | Web content layout tests | [reftests](http://web-platform-tests.org/writing-tests/reftests.html) |
 

See this [post](http://blog.strafenet.com/2014/07/03/end-to-end-javascript-testing-is-easy-the-minimal-way-to-do-it/) by Chris. It puts all the tools together. Another [comprehensive post](https://www.codementor.io/javascript/tutorial/javascript-testing-framework-comparison-jasmine-vs-mocha) by David Tang.


### References ###    
https://www.sitepoint.com/unit-test-javascript-mocha-chai/    
https://www.keithcirkel.co.uk/why-we-should-stop-using-grunt/    
https://www.keithcirkel.co.uk/how-to-use-npm-as-a-build-tool/    
https://www.npmjs.com/browse/keyword/load%20test    
https://www.npmjs.com/package/karma    
http://thejsguy.com/2015/01/12/jasmine-vs-mocha-chai-and-sinon.html    
https://www.codementor.io/nodejs/tutorial/unit-testing-nodejs-tdd-mocha-sinon    
https://www.codementor.io/nodejs/tutorial/unit-testing-tdd-node-js-nockjs-part-2    
http://thejsguy.com/2015/02/28/end-to-end-testing-with-phantomsjs-and-casperjs.html    
