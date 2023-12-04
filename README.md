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

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/z1byvnmxeacpe6lb7clg.png)

- The Choose an Amazon Machine Image (AMI) page displays a list of basic configurations called Amazon Machine Images (AMIs) that serve as templates for your instance. Select the HVM edition of the Amazon Linux AMI.

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ws6650uqzo7uxsoq9og5.png)  

- Scroll down and select the key pair you created in the "Create a key pair" section above or any existing key pair you intend to use.
- Select Select an existing security group.
- Select the JenkingsWebServerSG security group that you created.
- Select Launch Instance.

- In the left-hand navigation bar, choose Instances to view the status of your instance. Initially, the status of your instance is pending. After the status changes to running, your instance is ready for use.

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/g0l7dvb2g4maki5ezql8.png)  

### Step 4: Allocate Elastic IP address:

- In the EC2 Dashboard, navigate to the "Elastic IPs" section on the left-hand side.
- Click the "Allocate new address" button.
- A new Elastic IP address will be created and listed in the table below.

- In the EC2 Dashboard, click on "Instances" in the left-hand navigation pane.

- Select the EC2 instance to which you want to associate the Elastic IP address.

- Click on the "Actions" button at the top, then choose "Associate IP address."

- In the "Associate Elastic IP address" dialog, select the Elastic IP address you just allocated from the dropdown list.

- Choose the instance to associate it with from the "Instance" dropdown list.

- You can also specify a private IP address (optional), which can be useful in cases where the instance has multiple network interfaces.

- Click the "Associate" button.

- Once the association is complete, the Elastic IP address will be associated with your selected EC2 instance.

- Now the easy part, at this point, I only spent 3 minutes, let's do the rest.

### Step 5: Install Jenkins:

- Connecting to your Linux instance.

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/pevsa8qddq1i2ha5pl6n.png)

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/4uwcj4bs6g5lc9m8rs11.png)

- In the console, Add the Jenkins repo using the following command:

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/cuan9ktxdmzzopr5njcm.png)

- Import a key file from Jenkins-CI to enable installation from the package:

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/asyv4z5bwqwbozkupt9v.png)

- Install Java (Amazon Linux 2023):

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/c98wivtg38koi9hxbbxg.png)

- Install Jenkins:

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/233k837vm1dsi9bueo9v.png)

- Enable the Jenkins service to start at boot:

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/qb7godukx11225gwxvvs.png)

- Start Jenkins as a service:

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ehsgly97w1rxh0mihv2v.png)

- Connect to http://:8080 from your browser. You will be able to access Jenkins through its management interface

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/02jpdtw5lph5ucskyez6.png)

### Conclusion:

In less than 5 minutes, you have successfully deployed Jenkins on AWS. Now, you can use Jenkins to automate your software development processes, including building, testing, and deploying your applications. Explore Jenkins plugins, set up jobs, and integrate them with your version control system to make the most of this powerful tool.<br>

Now, you're ready to embark on your journey of automated, efficient CI/CD with Jenkins on AWS. Happy automating!<br>

### Additional Tips:

Remember to secure your Jenkins instance by configuring security settings and using strong authentication.<br>
Regularly back up your Jenkins configuration to prevent data loss.<br>
Explore Jenkins plugins to extend their functionality to suit your specific needs.<br>

Keep learning, and keep working hard. The Journey is the Reward.


