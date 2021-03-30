IBM Virtual Private Cloud

![vpc-overview](./images/vpc-overview.png)

1. Create new virtual server instance for VPC. (a) Enter instance name (test-satellite), selection location (Sydney), Select Type of virtual server (Public).

![vpc-create-1](./images/vpc-create-1.png)

2. Select Operating System. For Satellite select Red Hat Enterprise Linux 7.x - Minimal Install

![vpc-create-os](./images/vpc-create-os.png)

3. Select Server Profile. Minimum Satellite requirement: 4 cores, 16GB memory, 100GB storage.

![vpc-create-profile](./images/vpc-create-profile.png)

4. For manual configuration of server instance, upload SSH keys.  For automated setup, upload the attach host scripts in the Import user data.

![vpc-create-sshkeys](./images/vpc-create-sshkeys.png)

5. Once the setup is confirmed, click on the Create virtual server instance

![vpc-create-intance](./images/vpc-create-intance.png)

6. After the creation of the server instances, select instances without Floating IP.

![vpc-created-new](./images/vpc-created-new.png)

7. To add Floating IP, select the host and edit the corresponding Network interfaces, either select an existing IP address or Reserve a new floating IP.   

![vpc-create-floating-ip](./images/vpc-create-floating-ip.png)