## Setup each Host Manually

The following steps are the setup required for each hosts.  For IBM Cloud host, follow the steps in [VPC Instance Group Setup](host-setup-instance-group.md)

## 1. Assign unique hostname

SSH to each host and update the hostname. Use the command `hostnamectl` to update the hostname. Hostname will be updated however, terminal session hostname will be update upon next login or re-login to check if update. Ensure hostnames are unique to avoid conflict during setup. If the host is already assigned with a unique hostname, this step can be skipped unless it is desired to assign a preferred hostname.

```shell
hostnamectl set-hostname ira-sat-on-prem-demo-zone-2
```

## 2. Host Red Hat Subcription Manager registration

The following steps are for IBM Cloud custom OS images or on-prem setup.  These steps can be skipped for instances using the IBM Cloud provided OS images.

### a. Register host via subscription manager

Ensure Red Hat subscription license covers Red Hat Software Collections.  Register host using subscription-manager and enter the username, password, and Pool ID when needed.

```
subscription-manager register
```

Sample output:

```shell
[root@localhost ~]# subscription-manager register 
Unregistering from: subscription.rhsm.redhat.com:443/subscription
Registering to: subscription.rhsm.redhat.com:443/subscription
Username: <username>
Password: 
The system has been registered with ID: 82076cd1-7f08-40fa-a536-d300c3a31f11
The registered system name is: ira-sat-on-prem-demo-zone-2
```

### b. Attach host to Satellite location to Red Hat Satellite Network (RHSN)

After successful registration of host next attach the host to the subscription with command `subscription-manager attach`.

```shell
[root@ira-on-prem-zone3 ira]# subscription-manager attach 
Installed Product Current Status:
Product Name: Red Hat Enterprise Linux for x86_64
Status:       Subscribed
```

## 3. Add RHEL repositories

Use the following `subscription-manager` commands to enable the following repositories:

Pull the latest subscription data from the server with the command `subscription-manager refresh`

```shell
subscription-manager refresh
```

Sample output:

```shell
All local data refreshed
```

Add repositories using command `subscription-manager repos --enable=*`

```shell
subscription-manager repos --enable=*
```

Sample output:

```shell
Repository 'rhel-ha-for-rhel-7-server-eus-rpms' is enabled for this system.
Repository 'rhel-server-rhscl-7-rpms' is enabled for this system.
Repository 'rhel-7-server-optional-rpms' is enabled for this system.
Repository 'rhel-7-server-eus-optional-rpms' is enabled for this system.
Repository 'rhel-7-server-rh-common-rpms' is enabled for this system.
Repository 'rhel-7-server-eus-rpms' is enabled for this system.
Repository 'rhel-7-server-devtools-rpms' is enabled for this system.
Repository 'rhel-ha-for-rhel-7-server-rpms' is enabled for this system.
Repository 'rhel-rs-for-rhel-7-server-eus-rpms' is enabled for this system.
Repository 'rhel-rs-for-rhel-7-server-rpms' is enabled for this system.
Repository 'rhel-7-server-rpms' is enabled for this system.
Repository 'rhel-7-server-supplementary-rpms' is enabled for this system.
Repository 'rhel-7-server-extras-rpms' is enabled for this system.
Repository 'rhel-7-server-eus-supplementary-rpms' is enabled for this system.
```
