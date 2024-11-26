# <ins>Capstone Project - Linux Administration and Shell Scripting</ins>

## <ins>Project Scenario</ins>

CloudOps Solutions is a growing company that recently adopted AWS to manage its cloud infrastructure. As the company scales, they have decided to automate the process of managing AWS Identity and Access Management (IAM) resources. This includes the creation of users, user groups, and the assignment of permissions for new hires, especially for their DevOps team.

### <ins>Set-Up</ins>

Before advancing with the project, i had to set up the right environment for the shell script to be executed efficiently. so below are a few steps i took to ensure the right environment:

  - <ins>Setting up an EC2 instance on AWS and Connecting to the Server on GitBash</ins>

Firstly, i created an EC2 instance on AWS named "Shell_Script_Project" and used the SSH link to connect to the server of the instance on GitBash.

![Screenshot (254)](https://github.com/user-attachments/assets/2697314f-423e-4304-9aab-886729d594ee)

![Screenshot (255)](https://github.com/user-attachments/assets/48e42f09-f5ea-4295-b6a6-add7fa78d8f9)

  - <ins>Installing Apache</ins>

After successfully connecting to the instance, i installed, started and enabled Apache on the server. I use the following commands to achieve this:




### <ins>Objectives</ins>

#### <ins>1.) Define IAM User Names Array</ins>
  - Store the names of the five IAM users in an array for easy iteration during user creation.


