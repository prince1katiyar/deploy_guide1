# deploy_guide1

# deploy_guide

1. Create an IAM User for GitHub Actions

Go to AWS IAM console
Create a new IAM user with programmatic access
Attach policies:

AmazonECR-FullAccess
AmazonEC2ContainerRegistryFullAccess


Save the Access Key ID and Secret Access Key



2. Create an ECR Repository

Go to AWS ECR console
Click "Create repository"
Enter a name for your repository (e.g., "streamlit-app")
Keep default settings and click "Create repository"
Note the repository URI



3. Launch an EC2 Instance

Go to EC2 console
Launch a new EC2 instance:

Choose Ubuntu Server 20.04 LTS
Select t2.micro (free tier) or appropriate size
Configure security groups:

Allow SSH (port 22)
Allow HTTP (port 80)
Allow HTTPS (port 443)
Allow Custom TCP (port 8501)


Launch with a new key pair (save the .pem file)




4. Create IAM Role for EC2

Go to IAM console
Create a new role for EC2
Attach policies:

AmazonECR-FullAccess (to pull images from ECR)


Attach this role to your EC2 instance



Step 5: Set Up GitHub Secrets
In your GitHub repository:

Go to Settings → Secrets → New repository secret
Add these secrets:
# credential need to add 

AWS_ACCESS_KEY_ID: Your IAM user access key
AWS_SECRET_ACCESS_KEY: Your IAM user secret key
AWS_REGION: Your AWS region (e.g., us-east-1)
ECR_REPOSITORY: Your ECR repository name
EC2_HOST: Your EC2 instance public IP or DNS
EC2_SSH_KEY: The private SSH key content (.pem file)



715841335868.dkr.ecr.ap-south-1.amazonaws.com/streamlit-apps

h
ok 
cat /path/to/your-key.pem

'/Users/myhome/Downloads/streamlit app.pem'


# run the app:

Install the runner as a service:
bashCopysudo ./svc.sh install

Start the runner service:
bashCopysudo ./svc.sh start

Verify the service is running:
bashCopysudo ./svc.sh status







 # stop and remove runner steps 

sudo docker stop streamlit-container
sudo docker rm streamlit-container


sudo ./svc.sh stop
sudo ./svc.sh uninstall


./config.sh remove --token ABCDEFGHIJKLMNOPQRSTUV




# new runner 

./config.sh --url https://github.com/your-username/your-new-repo --token YOUR_NEW_TOKEN
sudo ./svc.sh install
sudo ./svc.sh start