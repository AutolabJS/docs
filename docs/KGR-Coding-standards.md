# Model workflow for developers

* The project uses codeclimate to regulate the code quality standards of the entire project.
* All the commits were made through PR requests so that travis and code climate tests can be performed.
* It is advised to setup codeclimate on your local repository using the yml file from the main repository.

General tips:

1) Fork dev repository from https://github.com/AutolabJS/AutolabJS.git
2) Setup the vagrant VM using the instructions in [README.md](https://github.com/AutolabJS/AutolabJS/blob/master/deploy/dev_setup/README.md)
3) Also setup a local node system to write tests for travis for every new feature.(test driven development)
4) Use mocha chai for js testing and bats for shell scripts testing.
5) Before opening a PR make sure to check that the code climate score has not decreased.
6) Always run linting tests before commit.
7) Always commit indented code.
8) Never commit directly to the main repository.
9) Commit and push to the local repository and the open a PR to the main repository.
10) Never commit to master branch.


