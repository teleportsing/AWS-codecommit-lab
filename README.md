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
