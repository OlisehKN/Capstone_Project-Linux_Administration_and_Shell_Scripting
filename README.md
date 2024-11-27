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

The names of the five new users are: Anna, Brad, Chris, Dave and Ella

Input:

    # Define IAM usernames array
    USERNAMES=("anna" "brad" "chris" "dave" "ella")

![Screenshot (269)](https://github.com/user-attachments/assets/e6462361-311b-4fbb-ab38-fc6903c8070e)

#### <ins>2.) Create IAM Users</ins>
  - Iterate through the IAM user names array and create IAM users for each employee using AWS CLI commands

Input:

        # Create IAM users
        for USERNAME in "${USERNAMES[@]}"; do
            echo "Creating IAM user: $USERNAME"
            aws iam create-user --user-name "$USERNAME"
        done

![Screenshot (270)](https://github.com/user-attachments/assets/3cdd9115-77b2-47c2-9976-699a3bd5a281)

#### <ins>3.) Create IAM Group</ins>
  - Define a function to create an IAM group named "admin" using the AWS CLI

Input:

        # Create an IAM group named 'admin'
        GROUP_NAME="admin"
        echo "Creating IAM group: $GROUP_NAME"
        aws iam create-group --group-name "$GROUP_NAME"

![Screenshot (271)](https://github.com/user-attachments/assets/1ad822f4-eb02-4570-a6c3-551a44a0895e)

#### <ins>4.) Attach Administrative Policy to Group</ins>
  - Attach an AWS-managed administrative policy (e.g., "AdministratorAccess") to the "admin" group to grant administrative privileges.

Input:

        # Attach AWS administrative policy to the group
        ADMIN_POLICY_ARN="arn:aws:iam::aws:policy/AdministratorAccess"
        echo "Attaching administrative policy to group: $GROUP_NAME"
        aws iam attach-group-policy --group-name "$GROUP_NAME" --policy-arn "$ADMIN_POLICY_ARN"

![Screenshot (272)](https://github.com/user-attachments/assets/a0eb0d41-f5d3-4498-bf9f-4f094880fa01)

#### <ins>5.) Assign Users to Group</ins>
  - Iterate through the array of IAM user names and assign each user to the "admin" group using AWS CLI commands.

Input:

        # Assign the created users to the group
        for USERNAME in "${USERNAMES[@]}"; do
            echo "Adding user $USERNAME to group $GROUP_NAME"
            aws iam add-user-to-group --user-name "$USERNAME" --group-name "$GROUP_NAME"
        done

![Screenshot (273)](https://github.com/user-attachments/assets/4a4ef85b-304f-49b5-b136-f2ab52e9805d)

Below is a screenshot of the entire shell script for the project.

![Screenshot (264)](https://github.com/user-attachments/assets/a653e5e3-3627-4dbd-a967-07320d3ffe9b)

### <ins>Output</ins>

When executing the Shell Script, the command line to use is:

    ./aws_cloud_manager.sh

After i input this in the terminal, this was the resulting output:

![Screenshot (265)](https://github.com/user-attachments/assets/41373ce0-8820-429b-80a1-ef5608060509)

![Screenshot (266)](https://github.com/user-attachments/assets/9255159a-4485-4b12-8feb-d7fc80b0fdbb)

As we can see the Shell Script automatically created new users for the five employees, created the group "admin", attached the administrative policy to it and added the newly created users to the group.

Lastly, I head over to my IAM console to confirm that the users and user group was automatically added to the console from the EC2 Instance server

Users:

![Screenshot (268)](https://github.com/user-attachments/assets/5589cdc5-e300-47d1-89e8-3a8142a90153)

User Group:

![Screenshot (267)](https://github.com/user-attachments/assets/0f4de9c3-307e-4c5e-adfc-0692639df3b1)

## END










