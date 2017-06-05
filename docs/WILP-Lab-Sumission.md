# Instructions for using Autolab server #
 
1. **Create a new user**
    1. Go to the link https://13.71.115.222
    2. Create an account on GitLab with username as your BITS ID (11 digits). For illustration let us say your bits id is 2015ht12345 and email id is 2015ht12345@wilp.bits-pilani.ac.in. But please replace it with your username and email id approrpriately.  
 
2. **Create new project on Gitlab server:**
    1. Login on https://13.71.115.222  with your credentials created in step 1.
    2. Create a private repo (new project) with the name being exactly ec1lab.
 
3. **Create your work space for coding on your local machine**
    1. Open a terminal and execute the following three commands. Replace your username and email id in the commands.     
      ```shell
      git config --global user.name "2015ht12345" 
      git config --global user.email "2015ht12345@wilp.bits-pilani.ac.in"
      export GIT_SSL_NO_VERIFY=1 
      ```
    2. Clone the repo from git server to your local machine.
      ```shell
       git clone https://2015ht12345@13.71.115.222/2015ht12345/ec1lab.git
      ```
      The command will clone an empty git repository called ec1lab in your present working directory. You need to place all your code in ec1lab directory.
    3. Code and save! Autolab supports multiple languages and expects the code to be put in the correct language-specific directory.  For example if you are choosing c language, then create directory “c” in "ec1lab" and store your file in that directory. The file name of your program should also have appropriate extension. For example, it can be somename.c. The required directory structure for other languages is given below. 
    
    | Programming Language | Directory / Folder  |
    |-------- |:----------:|
    | C language | c/ |
    | C++ 2011 language | cpp/ |
    | C++ 2014 language | cpp14/ |
    | Java language | java/ |
    | Python2 language | python2/ |
    | Python3 language | python3/ |
 
4. **Upload your code on Gitlab server**    
    1. Stage and commit the latest files by executing the following commands in your terminal. 
      ```shell
      git add *
      git commit -m 'code commit message'
      git push -u origin master
      ```
 
5. **Evaluate of your code submission**
    1. Go to the Main server(https://13.71.115.222:9000) and click on submit for **ec1lab**.
    2. Enter your BITS ID (2015ht12345), leave the commit hash row blank, choose the correct language and click submit. 
    3. See your score. If necessary debug your code in the local machine, push it to the gitlab server and evaluate it again. If there are multiple attempts, the maximum score will be considered for grading.