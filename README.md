# Working with AWS CodeCommit on Windows

This lab provides you with practice on AWS Codecommit

# Objectives

In this lab , you will be able to do the following:

 * Create a code repository in AWS CodeCommit 
 * Connect to your Windows EC2 instance
 * Configure AWS Tools for Windows Powershell to enable connections to the AWS Codecommit service
 * Create your local repository by cloning your remote Codecommit repository
 * Make Your First Commit Using Visual Studio Code
 * Use the AWS Codecommit console to view the files you committed
 * Make a commit using the Code Commit console
 * Explore the Code Commit console

 Amazon EC2 Windows Server instance has been created for you to use in the labBoth Microsoft Visual Studio Code and the Git client have been installed on theWindows instance This lab takes about 10 minutes to launch


# Lab prerequisites

To get the most out of this lab , you should understand the principles of source coderepositories and have some prior development experience . Students should befamiliar With making RDP connections to Windows instances running in AmazonEC2

# Other AWS Services

Many AWS services that are not needed for this lab are disabled by LAM policyduring your access time in this lab . In addition , the capabilities of the services usedin this lab are limited to what , 's required by the lab . Expect errors when accessingother services or performing actions beyond those provided in this lab quide


# AWS Codecommit

AWS Codecommit is a highly scalable , managed source control service that hostsprivate Git repositories . Behind the scenes , Code Commit stores your data inAmazon S3 and Amazon Dynamodb giving your repositories high scalability ,availability , and durability . You simply create a repository to store your code . Thereis no hardware to provision and scale or software to install , configure , and operate


# Visual Studio Code

According to Microsofts website , Visual Studio Code combines the streamlined Uof a modern editor with rich code assistance and navigation , and an integrateddebugging experience - without the need for a full IDE . It is currently free and it runson Windows , Mac , and Linux . It includes features for working with Git coderepositories , so it is a convenient tool for learning AWS Codecommit , but numerousother Git tools are available ( free and commercial ) that work similarly with AWSCodecommit . This lab is not meant to be a complete introduction to Visual StudioCode


# Task 1 : Create an AWS Codecommit repository

In this task , you will create a Code Commit repository using the Code Commitconsole


3. At the top of the AWS Management Console , in the search bar , search for and choose `Codecommit`

4. If you see `Get started` , choose it.

5. Choose Create repository then configure

 * Repository name: `myrepo`
 * Choose `Create`.

This will create your Codecommit Repository

 A You can set up notifications for a repository so that repository users receiveemails about the repository event types you specify . When you configurenotifications . AWS Code Commit creates an Amazon Cloudwatch Events rule foryour repository . This rule responds to the event types you select from thepreconfigured options in the AWS Code Commit console . Notifications are sentwhen events match the rule settings . You can create an Amazon SNS topic to usefor notifications , or use an existing one in your AWS account.

In this lab , you will not configure notifications


6. If you see Configure email notifications page , choose Skip

A Connection steps page will appear . This page explains how to connect your computer toyour Code Commit repository . It lists the prerequisites for using Code Commit . It alsodisplays the steps that you need to run to clone the remote repository to your computer


7. Make sure you have selected the `HTTPS` tab

8. At the top-right of the screen , choose `Clone URL`

9.Select Clone HTTPS 

10. Paste the clone URL into your text editor

You will use this command later to clone your remote repository to your local repository


# Task 2 : Connect to the Windows EC2 instance

In this task , you will:

 * Connect to your EC2 Windows instance . You will use this instance to create alocal git repository . An instance profile is associated with your EC2 instance . TheIstance profile allows you to access Codecommit from your EC2 instance
 
 * Configure the AWS Tools for Windows Powershell to enable connections to the AWS Codecommit service
 
 * Create your local repository by cloning your remote Codecommit repository

The Git client and Visual Studio Code applications have been installed on yourWindows EC2 instance.

The Git client has been installed with all of the default options with exception of theollowing changes :


 * Adjusting your PATH environment : Use Git from the Windows CommandPromp
 
 * Configuring extra options : De-selected - enable Git Credential Manager ( Thisoption is not used . Instead the credential helper will be used in your lab )
 
 Connect to the Windows instance using Apache Guacamole

11. Copy the Guacamoleurl value from the list to the left of these instructions , andthen paste it into a new web browser tab

12. On the Apache Guacamole sign-in page

 * For Username . enter studentor Password , copy and paste the Administrat
 
 * For password value listed to the leftof these instructionsChoose Login
 
 
The connection to your remote instance should start momentarily . After you open aconnection , you will see an image of the dev instance desktop . You can interactwith this image just as you would your normal desktop or any remote desktopclient

You are now connected to the Windows instance in your web browser usingGuacamole

Note : If you prompted with a Networks pop-up window asking : Do you want toallow your PC to be discoverable by other Pcs and devices on this networkChoose No


13. Note : How to copy and paste when using Guacamole browser session

 * To open the clipboard editor:
 
   * On Windows , press `Ctrl + Alt + Shift`
   * On macos , press `command control shift`
   
 * Copy the appropriate text from the lab instructions and paste it to the clipboardedito
 * To close the clipboard edito
 
  * On Windows , press `Ctrl + Alt + Shift`
  * On macos , press `command control shift`
  
 * You can now use regular paste commands in your session from the clipboardYou can also edit or replace the contents of the Guacamole clipboard forsubsequent copies
 
Configure the AWS Tools for Windows Power she

14. In your remote session , choose the Windows Start = a button , then type Power Shell

15. In the list of programs , choose Windows Powershel

16. Set the default AWS region for running AWS CLI commands by doing thefollowing

 * Enter : set-defaultawsregion - region 
 
 * REGIONReplace REGION With REGION value located to the left of these instructions
 
 * Press Enter
 
 17. Enable the Git credential helper to send the path to repositories by entering:
 
 ```
git config --global credential.helper '!aws codecommit credential-helper $@'
git config --global credential.UseHttpPath true
 ```

The AWS Tools for Windows Powershell comes with a Git credential helper that youcan use with AWS CodeCommnit

18. Run the following command to configure the credential helper to use the defaultAWS credential profile

 `. "C:\\Program Files (x86)\\AWS Tools\\CodeCommit\\git-credential-awss4.exe"`
 
The dot space on the front of the command is required to run an EXE in Powersheland the double-quotes are required when working with paths and filenames thatcontain spaces

19. When prompted to install the Git credential helper to generate AWSSV4signatures , choose Yes

20. Run the following commands in Windows Powershell to create a new codefolder to use for the rest of this lab


```
cd \
md code
cd code
```

 * Paste `git clone CLONEURL`
 * Replace CLONEURL with the clone URL you copied earlier
 * Press Enter
 
You should see the following message

Git Cloning into `demo…… ` 

warning You appear to have cloned an empty repository


Next , you will set up your user name and email address to in the git configurationhis will make it easier to identify your commits

22. Configure your git username by doing the following：

 * Enter git config - -global user name NAME
 * Replace NAME With a username
 * Press Enter
 
 
23. Configure your git username by doing the following： 

 * Enter git config --global user.email EMAIL
 * Replace Email With a email
 * Press Enter
 
