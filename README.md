# Bastion-AWS
Construct a bastion in AWS

A/ Create a key pair
- Go on "EC2 Dashboard"
- Click "Key Pairs"
- Click "Create Key Pair"
- Add a key pair name and click on create
- Save the ".pem" file

=> Keep carefully the key as you will need it later to log on on your instances


B/ Launch a VPC
- Go on "VPC Dashboard"
- Click "Start VPC Wizard"
	Step 1: Select "VPC with Public and Private Subnets"
	Step 2: Add a VPC name
		Select the same "Availability Zone" for public and private subnet
		Use a NAT instance
		Select the "Instance type": "t2.nano"
		Select the key pair that you created
- Click "Create VPC"

=> You should see this message "Your VPC has been successfully created"


C/ Launch bastion
- Go on "EC2 Dashboard"
- Click "Launch Instance"
	Step 1: Select "Microsoft Windows Server 2016 Base"
	Step 2: Select "t2.micro"
	Step 3: On "Network", choose the VPC previously created
		On "Subnet", choose the "Public Subnet"
		On "Auto-assign Public IP", choose "Enable"
	Skip Step 4 and 5
	Step 6: Choose "Create a new security group"
		Add a "Security group name" and a "Description"
		Click on "Add rule"
			RULE 1:	Type: HTTP; Source 0.0.0.0/0
			RULE 2: Type: HTTPS; Source 0.0.0.0/0
			RULE 3: Type: RDP; Source: My IP
	Step 7: Review your instance
- Click on "Launch"
- Choose an existing key pair and select the key pair previously created. Tick the box and launch the instance
		
=> Your bastion is now created


D/ Launch private instance
- Go on "EC2 Dashboard"
- Click "Launch Instance"
	Step 1: Select "Microsoft Windows Server 2016 Base"
	Step 2: Select "t2.micro"
	Step 3: On "Network", choose the VPC previously created
		On "Subnet", choose the "Private Subnet"
		On "Auto-assign Public IP", choose "Use subnet setting (Disable)"
	Skip Step 4 and 5
	Step 6: Choose "Create a new security group"
		Add a "Security group name" and a "Description"
		Click on "Add rule"
			RULE 1:	Type: RDP
				Source: Custom
				And type your first security group created (of your bastion)
	Step 7: Review your instance
- Click on "Launch"
- Choose an existing key pair and select the key pair previously created. Tick the box and launch the instance

=> Your private instance is now created

E/ Connect to the bastion
- Go on "EC2 Dashboard"
- Click on "Running instances"
- Right click on your bastion instance, "connect" and "get password"
- On "Choose a file", select your key file and "Decrypt password"
- Keep the password 
- Open "Remote Desktop Connection"
	Computer: copy paste Public IP of the bastion
	Enter the password and connect

=> You are now connected to the bastion

F/ Connect to the private instance from the bastion
- Open "Remote Desktop Connection" in your bastion
- Follow the same steps as on E/ but doing connect to the private instance

=> You are now connected to the private instance

G/ Ping google.com
- Open "Command Prompt"
- Type "ping google.com"

