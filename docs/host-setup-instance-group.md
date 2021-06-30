# Setup host via VPC Intance Group

## 1. Create Instance templace for VPC

a. Select `Instance templates for VPC` in VPC Infastructure 
![vpc-instance-template](./images/vpc-instance-template.png)

b. Upload the attach script file and add the commands `subscription-manager refresh` and `subscription-manager repos --enable=*`

![vpc-upload-attach-script](./images/vpc-upload-attach-script.png)

c.  Select **Location**, **Operating System Image** `RHEL 7`, then proceed to the **Create Instance template**

![vpc-create-instance-template](./images/vpc-create-instance-template.png)

## 2. Create Intance Group

Select the **instance teamplate**, then choose **Static**, **Set instance group size** (enter 6 for minimum Satellite host) and **Create instance group**

![vpc-instance-group](./images/vpc-instance-group.png)

This is the diplay after creating the instance group
 
 ![vpc-creating-instance-group](./images/vpc-creating-instance-group.png)

 Check the status in the **Virtual server instances**, add the **Floating IP** for each hosts.

 ![vpc-creating-instance-group-status](./images/vpc-creating-instance-group-status.png)

## 3. Check the Satellite location host

![ibm-cloud-vpc-host-auto-sat](./images/ibm-cloud-vpc-host-auto-sat.png)

