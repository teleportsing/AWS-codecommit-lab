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


# Task 1 : Create an AWS Codecommitrepository

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







