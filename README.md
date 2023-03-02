# Working with AWS CodeCommit
AWS CodeCommit is a highly scalable, managed source control service thathosts private Git repositories. Codecommit stores your data in Amazon S3 andAmazon Dynamodb giving your repositories high scalability, availability, anddurability. You simply create a repository to store your code. There is nohardware to provision and scale or software to install, configure, and operate

This hands-on lab gives you practice with AWS CodeCommit, part of AWSDeveloper Tools. In this lab, you first create a code repository in AWS Codecommit. Then you create a local repository on a Linux instance runningC2. After you create the local repo, you make some changes to it. Then yousynchronize( commit)your changes to the AWS Codecommit repository

# Topics covered

This lab demonstrates how to:

 * Create a code repository using AWS Code Commit via the Amazon Management Console
 
 * Create a local code repository on the Linux instance using git
 
 * Synchronize a local repository with an AWS Code Commit repository


# Prerequisites

Students should have some development experience and understand the principlesof source code repositories , and has some prior development experience . Studentsshould be comfortable with making SSH connections to instances running inAmazon EC2 , and using Linux commands and editors from the command line innux Students should have taken at a minimum Introduction to Amazon ElasticCompute Cloud ( EC2 ) prior to taking this lab

# Task 1: Create an AWS Codecommitrepository


In is task , you use the AWS Management Console to create an AWS Code Commitrepository

3. At the top of the AWS Management Console , in the search bar search for andchoose `Codecommit`

4. On the AWS Code Commit page , choose `Create repository`

5. On the Create repository page

 * For Repository name , enter `My-repo`
 * For Description enter `My first repository`
 
 6. Choose `Create`
 
 An empty repository named My-repo is created
 
 You should now be on the My-repo page , which contains the details to connect tothe repository


# Task 2 : Connect to the Amazon EC2 instance

An Amazon EC2 instance has been created for you as part of the lab environmentbuild process . In this task , you connect to the instance using AWS SystemsManager Session Manager

7. Copy the Ec2instancesessionurl value from the list to the left of thesestructions , and then paste it into a new web browser tab

A console connection is made to the instance inside your web browser window . Aset of commands are run automatically when you connect to the instance thachange to the users home directory and display the path of the working directory ,similar to this

```
cd HOME; pwd; bash
sh-4.2$ cd HOME; bash; pwd
/home/ec2-user
[ec2-user@ip-10-0-1-137 ~]$
```

# Task 3 : Create a local repository using Git

This task provides an example of how you would use AWS Code Commit tosynchronize to any local code repository that you might create in your normaproduction development environment

In the terminal session , run the following command to install the Git client

`sudo yum install -y git`

On a Windows-based computer , you might need to use Ctrl + Shift + V or openthe context menu ( right-click ) to paste text into a Session Manager console window

9. Run the following commands to configure the Git credential helper with theAWS credential profile , and allow the Git credential helper to send the path torepositories

```
git config --global credential.helper '!aws codecommit credential-helper $@'
git config --global credential.UseHttpPath true
```

✅ These commands have no output

Next,obtaintheHTTPSURLofyourAWSCodecommitrepository


10. Return to your web browser tab with the AWS Code Commit console , whichshould be on the ·My-repo· page

11. At the upper-right of the page , choose Clone URIand then `choose cloneHTTPS`

The repository URL is copied to your clipboard and should look similar to this:
[https://git-codecommit.us-east-1.amazonaws.com/v1/repos/my-repo](https://git-codecommit.us-east-1.amazonaws.com/v1/repos/my-repo)

12.Return to your web browser tab with the terminal session

13. Run the following command to clone the My-repo repository to the instance

 * ReplacetheCLONE_HTTPSURLplaceholdervaluewiththeCloneHTTPSURLthat you copied previously
 
 `git clone CLONE_HTTPS_URL`
 
 
 ✅ The output should indicate that you are cloning the My-repo repository , and thatthe repository is empty , similar to this:
 
 ```
Cloning into 'My-Repo'...
warning: You appear to have cloned an empty repository.
 ```

Next , you conclude with a short demonstration of making a change andsynchronizing the repositories . This is a mini example of the workflow ofsynchronizing code changes during the development process
 
 
 # Task 4 : Making a code change and firstcommit to the repo
 
In this task , you create your first commit in your local repo You create two examplefiles in your local repo , use Git to stage the changes to your local repo , and thencommit the changes
 
Run the following command to change to the My-repo directory:

`cd ~/My-Repo`

Run the following command to create two files in your local repo:

```
echo "The domestic cat (Felis catus or Felis silvestris catus) is a small, usually furry, domesticated, and carnivorous mammal." >cat.txt
echo "The domestic dog (Canis lupus familiaris) is a canid that is known as man's best friend." >dog.txt
```

✅ These commands have no output

Run the following command to list the files in the current directory

`ls`

The output should show the two files you created , similar to this

`cat.txt  dog.txt`

17. Run the following command to stage the changes in your local repo

`git add cat.txt dog.txt`

✅ This command has no output

18. Run the following command to view the status of your repo

`git status`

✅ The output should show the branch you are current working in ( master ) and thatthe two files are ready to be committed to the repository , similar to this

```
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   cat.txt
        new file:   dog.txt
```

19. Run the following command to commit the changes in your local repo

`git commit -m "Added cat.txt and dog.txt"`


✅ The output displays a message stating that the name and email address of thecommitter were configured automatically In a production environment , you woulduse the commands listed to set your name and email address , which are thenapplied to each commit you do . The output also shows that two files were changedand inserted . similar to this

```
Committer: EC2 Default User <ec2-user@ip-10-1-12-142.ec2.internal>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly:

    git config --global user.name "Your Name"
    git config --global user.email you@example.com

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

 2 files changed, 2 insertions(+)
 create mode 100644 cat.txt
 create mode 100644 dog.txt
```

20. Run the following command to view details about the commit you ust made

`git log`


✅ wthe output shows that there is one commit to the master branch , the name of theauthor , the date the commit was made . and the files that were added similar to this

```
commit 772d16037b2e0d7ee7e97aa9218e571346bebe0e (HEAD -> master)
Author: EC2 Default User <ec2-user@ip-10-1-12-142.ec2.internal>
Date:   Wed Jul 20 19:20:06 2022 +0000

    Added cat.txt and dog.txt
```

Now that you have an initial commit in your local repo , you can push the commitfrom your local repo to your AWS Codecommit repository


# Task 5 : Push your first commit

In this task , you push the commit from your local repo to your AWS Code Commit repository

21. Run the following command to push your commit through the default remotename Git uses for your AWS Code Commit repository ( origin ) , from the defaulbranch in your local repo ( master )

`git push -u origin master`

✅ The output displays the details of the process to create the branch and push thefiles to the remote repository similar to this

```
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 2 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 447 bytes | 447.00 KiB/s, done.
Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
To https://git-codecommit.us-east-1.amazonaws.com/v1/repos/My-Repo
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
```

After you have pushed code to your AWS Code Commit repository , you can view thecontents using the AWS Code Commit console

22. Return to your web browser tab with the AWS Code Commit console , whichshould be on the My-repo page

23. Choose your Web browsers refresh button to refresh the page

The two files that you added to your repository should be displayed

24. Choose the link for each file to view its contents

# Conclusion

 * Created a code repository using the AWS Code Commit Management Console
 
 * Created a local code repository on your Linux instance using git
 
 * Synchronized a local repository with an AWS Code Commit repository
 
 Consider how to bring AWS Code Commits features and capabilities to yourdevelopment workflow , including
 
 * Collaboration : AWS Codecommit is designed for collaborative softwaredevelopment . Codecommit allows you to commit , diff , and merge your codeallowing you to easily maintain control of your teams projects . You can create arepository from the AWS Management Console , AWS CLI , or AWS SDKS andstart working with the repository using Git
 
* Encryption:youcantransferyourfilestoandfromAWSCodecommitviaHTTPSand SSH . Your repositories are also automatically encrypted at rest throughAWS Key Management Service using customer-specific keys

* Access Control : AWS Code Commit uses AWS Identity and Access Managemento control and monitor who can access your data as well as how when andwhere they can access it

* Access Control : AWS Code Commit uses AWS Identity and Access Managementto control and monitor who can access your data as well as how when andwhere they can access it

* High Availability and Durability AWS Code Commit stores your repositories inAmazon S3 and Amazon Dynamodb Your data is redundantly stored acrossmultiple facilities . This architecture increases the availability and durability ofyour repository data

* Unlimited Repositories : AWS Code Commit allows you to create as manyrepositories as you need , with no size limits . You can store and version any kindf file , including application assets such as images and libraries alongside yourcode

* Easy Access and Integration : You can use the AWS Management Console , AWSCLL , and AWS SDKS to manage your repositories . You can also use Gitcommands or Git graphical tools to interact with your repository source filesAWS Code Commit supports all Git commands and works with your existing Gittools . You can integrate with your development environment plugins orcontinuous integration / continuous delivery systems

# Additional Resources

* [AWS Codecommit](https://aws.amazon.com/codecommit/resources/)
* [AWS Training and Certification](https://aws.amazon.com/training/)

