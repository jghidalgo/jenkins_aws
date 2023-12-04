# Deploy Jenkins on AWS in less than 5min
Introduction:

Are you looking to set up Jenkins, the popular open-source automation server, on Amazon Web Services (AWS) quickly and effortlessly? In this guide, we'll walk you through the steps to deploy Jenkins on AWS in less than 5 minutes, enabling you to streamline your continuous integration and continuous delivery (CI/CD) pipelines.

Prerequisites:

Before we begin, make sure you have the following prerequisites in place:

An AWS account.<br>
Familiarity with AWS services.<br>
Basic knowledge of Jenkins.<br>

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/a3t96ud4abxsefumgi19.jpg)

### Step 1: Create a key pair:

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/ and sign in.<br>
In the navigation pane, under NETWORK & SECURITY, select Key Pairs.<br>
Select Create key pair.<br>


![Alt Text](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ho735grgo2s1xw4g4z61.png)

- For Name, enter a descriptive name for the key pair. Amazon EC2 associates the public key with the name that you specify as the key name. A key name can include up to 255 ASCII characters. It cannot include leading or trailing spaces.<br>
- For File format, select the format in which to save the private key.<br>
- For OpenSSH compatibility, select pem.<br>
- For PuTTY compatibility, select ppk.<br>
- Select Create key pair.<br>
- The private key file downloads automatically. The base file name is the name you specified as the name of your key pair, and the file name extension is determined by the file format you chose. Save the private key file in a safe place.<br>
- This is the only chance for you to save the private key file.<br>
- If you use an SSH client on a macOS or Linux computer to connect to your Linux instance, run the following command to set the permissions of your private key file so that only you can read it.<br>

### Step 2: Create a key pair: Create a security group:

To create and configure your security group:<br>

- Decide who may access your instance. For example, a single computer or all trusted computers on a network. For this tutorial, you can use the public IP address of your computer.<br>
- To find your IP address, use the check IP service tools on the Internet.<br>
- This is unsafe for production environments because it allows everyone to access your instance using SSH.<br>
- Sign in to the AWS Management Console.<br>
- Open the Amazon EC2 console by selecting EC2 under Compute.<br>

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/f4z18wlu5qr2pvpa5qc5.png)

- In the left-hand navigation bar, select Security Groups, and then select Create Security Group.

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ndh9gl96iaqd9yx7x59n.png)

- In the Security group name, enter [JenkinsWebServerSG] or any preferred name of your choice, and provide a description.<br>
- Select your VPC from the list. You can use the default VPC.<br>
On the Inbound tab, add the rules as follows:<br>
- Select Add Rule, and then select SSH from the Type list.<br>
- Under Source, select Custom, and in the text box, enter the IP address from step 1, followed by /32 indicating a single IP Address.<br>
- Select Add Rule, and then select HTTP from the Type list.<br>
- Select Add Rule, and then select Custom TCP Rule from the Type list.<br>
- Under Port Range, enter 8080.<br>
- Select Create.<br>

### Step 3: Launch an EC2 Instance:

- Open the Amazon EC2 console by selecting EC2 under Compute.
- From the Amazon EC2 dashboard, select Launch Instance.  
