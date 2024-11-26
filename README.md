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
    
    sudo yum install -y httpd
    sudo systemctl start httpd
    sudo systemctl enable httpd

![Screenshot (256)](https://github.com/user-attachments/assets/e0dcf032-5c9a-40c0-a0eb-08f0e0ba47cf)

![Screenshot (257)](https://github.com/user-attachments/assets/7309587c-6db8-4abc-bfd1-076e075cf81b)

![Screenshot (258)](https://github.com/user-attachments/assets/2509916e-f2dc-41cc-b05e-8b475139885e)

  - <ins>AWS CLI Authentication, Configuration and Confirmation</ins>

The first step i took in ensuring that the AWS CLI tool was ready on the server was to, first check and authenticate the version of AWS CLI that was already installed. This was done by using the following command line:

    aws --version

![Screenshot (259)](https://github.com/user-attachments/assets/20bdaf4a-be4d-407a-845a-8f289ca7e841)

After successfully checking that it had the updated version, i set the configuration of AWS Server to be linked to my IAM Console, this way any changes made on the terminal will be automatically sent and updated on my IAM Console.

First i used the following command to start the configuration process:

    aws configure

Secondly, i entered the access keys i created earlier, the region of the server and the Output format of my IAM Console.

![Screenshot (261)](https://github.com/user-attachments/assets/ce8335ee-ec77-4af0-99d4-f023f85c5b8c)

After completing the configuration, the last step was to confirm that my IAM Console was successfully linked to the Server. I used the following command to achieve this:

    aws sts get-caller-identity

![Screenshot (262)](https://github.com/user-attachments/assets/99d0ea27-3dd8-410a-ae0b-aafa7aab77e5)

Lastly, I created the Shell Script "aws_cloud_manager.sh" and changed the permissions to make the shell script executable. I used the following command to achieve this:

    touch aws_cloud_manager.sh
    chmod +x aws_cloud-manager.sh

![Screenshot (263)](https://github.com/user-attachments/assets/f659bb53-fd0b-4dda-a1cb-e55d7bc2e823)

Now that i have confirmed that AWS CLI is running on the server and my IAM console is linked, created the shell script and made it executable, i can advance to the objectives of the project.

### <ins>Objectives</ins>

#### <ins>1.) Define IAM User Names Array</ins>
  - Store the names of the five IAM users in an array for easy iteration during user creation.




