# Deploy Red Hat OpenShift Cluster in VPC Server Instance via Satellite Host 

Explore IBM Satellite capabilites in deploying Red Hat OpenShift Cluster utilizing Satellite host.  This method is only for demo or proof-of-concept (PoC).  For Red Hat OpenShift in production environment use IBM Red Hat OpenShift Kubernetes Service (ROKS) in IBM Cloud or via Satellite Host in other cloud providers (e.g. GCP, AWS, Azure, etc) or on-prem resources.

## IBM Cloud Services

* [IBM Satellite](https://cloud.ibm.com/docs/satellite?topic=satellite-about)
* [IBM Virtual Private Cloud - VPC](https://www.ibm.com/cloud/learn/vpc)
* [IBM Red Hat OpenShift in IBM Cloud](https://cloud.ibm.com/docs/openshift?topic=openshift-getting-started)


## Prerequisites 
* A Pay-As-You-Go or Subscription [IBM Cloud account](https://cloud.ibm.com/registration)
* Minimum of 6 hosts with 4 cores, 16GB memory and 100GB storage


## Steps

* [Create VPC Server Instance for Satellite Host](vpc-setup.md)
* [Manual Setup of Satellite Host](manual-host-setup.md)
* [Satellite Host Setup using Instance Group](host-setup-instance-group.md)
* [Create Satellite locations and attach hosts](attach-hosts.md)
* [Create Red Hat OpenShift Cluster using Satellite Infrastructure](roks-setup.md)
* [Setup VPC DNS for public access without VPN](vpc-dns-setup.md)

Note:
For on-prem host, skip `Create VPC Server Instance for Satellite Host`
