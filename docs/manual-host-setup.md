## Setup each Host Manually

## Assign unique ostname

SSH to each host and update the hostname. Use the command `hostnamectl` to update the hostname. Hostname will be updated however, terminal session hostname will be update upon next login or re-login to check if update. Ensure hostnames are unique to avoid conflict during setup.

    ```shell
    hostnamectl set-hostname ira-sat-on-prem-demo-zone-2
    ```

## Register host via subcription manager

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

## Attach host to Satellite location Control plane

After successful registration of host next attach the host to the subscription with command `subscription-manager attach`.

    ```shell
    [root@ira-on-prem-zone3 ira]# subscription-manager attach 
    Installed Product Current Status:
    Product Name: Red Hat Enterprise Linux for x86_64
    Status:       Subscribed
    ```

## Add RHEL repositories

Use the following `subscription-manager` commands to enable the following repositories:

    ```shell
    subscription-manager refresh
    subscription-manager repos --enable rhel-server-rhscl-7-rpms
    subscription-manager repos --enable rhel-7-server-optional-rpms
    subscription-manager repos --enable rhel-7-server-rh-common-rpms
    subscription-manager repos --enable rhel-7-server-supplementary-rpms
    subscription-manager repos --enable rhel-7-server-extras-rpms
    ```

    Sample output:

    ```shell
    [root@ira-sat-on-prem-demo ~]# subscription-manager repos --enable rhel-server-rhscl-7-rpms
    Repository 'rhel-server-rhscl-7-rpms' is enabled for this system.
    [root@ira-sat-on-prem-demo ~]# subscription-manager repos --enable rhel-7-server-optional-rpms
    Repository 'rhel-7-server-optional-rpms' is enabled for this system.
    [root@ira-sat-on-prem-demo ~]# subscription-manager repos --enable rhel-7-server-rh-common-rpms
    Repository 'rhel-7-server-rh-common-rpms' is enabled for this system.
    [root@ira-sat-on-prem-demo ~]# subscription-manager repos --enable rhel-7-server-supplementary-rpms
    Repository 'rhel-7-server-supplementary-rpms' is enabled for this system.
    [root@ira-sat-on-prem-demo ~]# subscription-manager repos --enable rhel-7-server-extras-rpms
    Repository 'rhel-7-server-extras-rpms' is enabled for this system.
    ```


