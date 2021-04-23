## VPC DNS setup

Setup VPC DNS for public access, othewise, VPN is required to access the cluster.

1. Login to IBM Cloud via the `ibmcloud CLI`

    ```
    ibmcloud login
    ``` 

    for federated account 

    ```
    ibmcloud login --sso
    ``` 

2. Get cluster

    ```
    ibmcloud oc cluster ls
    ```

    Sample output from CLI:
        ```
        Name                             ID                     State    Created      Workers   Location             Version                 Resource Group Name   Provider   
        ira-demo-sat-cluster-satellite   c1gmq42w0g3jucqlern0   normal   1 day ago    3         ira-demo-ibm-cloud   4.5.31_1531_openshift   default               satellite   
        ira-demo-sng01-b3c.4x16          c19bq46t0jcg8lonbseg   normal   1 week ago   2         sng01                4.5.31_1531_openshift   default               classic  
        ```

3. Connect to the Satellite cluster

    ```
    ibmcloud oc cluster config --admin -c ira-demo-sat-cluster-satellite
    ```
    Sample output from CLI:
    ```
    OK
    The configuration for ira-demo-sat-cluster-satellite was downloaded successfully.

    Added context for ira-demo-sat-cluster-satellite to the current kubeconfig file.
    You can now execute 'kubectl' commands against your cluster. For example, run 'kubectl get nodes'.
    If you are accessing the cluster for the first time, 'kubectl' commands might fail for a few seconds while RBAC synchronizes.

    ```

4. To get the `Satellite` location DNS for the cluster **ira-demo-ibm-cloud**. The IP addresses in the Records column are Private IP.

    ```
    ibmcloud sat location dns ls --location ira-demo-ibm-cloud
    ```

    Sample output from CLI:
    ```
    Hostname                                                                                        Records                                                                                         SSL Cert Status   SSL Cert Secret Name                                          Secret Namespace
    i1d21368ca9949e6876b6-6b64a6ccc9c596bf59a86625d8fa2202-c000.us-east.satellite.appdomain.cloud   10.245.64.5,10.245.64.6,10.245.64.8                                                             creating          i1d21368ca9949e6876b6-6b64a6ccc9c596bf59a86625d8fa2202-c000   default
    i1d21368ca9949e6876b6-6b64a6ccc9c596bf59a86625d8fa2202-c001.us-east.satellite.appdomain.cloud   10.245.64.5                                                                                     creating          i1d21368ca9949e6876b6-6b64a6ccc9c596bf59a86625d8fa2202-c001   default
    i1d21368ca9949e6876b6-6b64a6ccc9c596bf59a86625d8fa2202-c002.us-east.satellite.appdomain.cloud   10.245.64.8                                                                                     creating          i1d21368ca9949e6876b6-6b64a6ccc9c596bf59a86625d8fa2202-c002   default
    i1d21368ca9949e6876b6-6b64a6ccc9c596bf59a86625d8fa2202-c003.us-east.satellite.appdomain.cloud   10.245.64.6                                                                                     creating          i1d21368ca9949e6876b6-6b64a6ccc9c596bf59a86625d8fa2202-c003   default
    i1d21368ca9949e6876b6-6b64a6ccc9c596bf59a86625d8fa2202-ce00.us-east.satellite.appdomain.cloud   i1d21368ca9949e6876b6-6b64a6ccc9c596bf59a86625d8fa2202-c000.us-east.satellite.appdomain.cloud   creating          i1d21368ca9949e6876b6-6b64a6ccc9c596bf59a86625d8fa2202-ce00   default

    ```

5. Register DNS the Floating IP address for the control plane host.  Get the Floating IP address from the VPC console.

    ```
    ibmcloud sat location dns register --location ira-demo-ibm-cloud --ip 130.198.14.54 --ip 130.198.19.141 --ip 130.198.8.91
    ```

    Sample output from CLI:
    ```
    Registering a subdomain for control plane hosts...
    OK
    Subdomain                                                                                       Records
    i1d21368ca9949e6876b6-6b64a6ccc9c596bf59a86625d8fa2202-c000.us-east.satellite.appdomain.cloud   130.198.14.54, 130.198.19.141, 130.198.8.91
    i1d21368ca9949e6876b6-6b64a6ccc9c596bf59a86625d8fa2202-c001.us-east.satellite.appdomain.cloud   130.198.14.54
    i1d21368ca9949e6876b6-6b64a6ccc9c596bf59a86625d8fa2202-c002.us-east.satellite.appdomain.cloud   130.198.19.141
    i1d21368ca9949e6876b6-6b64a6ccc9c596bf59a86625d8fa2202-c003.us-east.satellite.appdomain.cloud   130.198.8.91
    i1d21368ca9949e6876b6-6b64a6ccc9c596bf59a86625d8fa2202-ce00.us-east.satellite.appdomain.cloud   i1d21368ca9949e6876b6-6b64a6ccc9c596bf59a86625d8fa2202-c000.us-east.satellite.appdomain.cloud
    ```

6. Get the `IBM NLB DNS` for the Red Hat OpenShift cluster worker nodes

    ```
    ibmcloud ks nlb-dns ls --cluster ira-demo-sat-cluster-satellite
    ```

    Sample output from CLI:
    ```
    OK
    Hostname                                                                                       IP(s)                                   Health Monitor   SSL Cert Status   SSL Cert Secret Name                                            Secret Namespace
    ira-demo-sat-cluster-sa-54cf26acc8196920b8b92e52d85dba7e-0000.upi.containers.appdomain.cloud   10.245.64.9,10.245.64.10,10.245.64.11   None             created           ira-demo-sat-cluster-sa-54cf26acc8196920b8b92e52d85dba7e-0000   openshift-ingress
    ```

7. To update the IP address, we need to remove the existing Private IP address

    ```
    ibmcloud ks nlb-dns rm classic --cluster ira-demo-sat-cluster-satellite --nlb-host ira-demo-sat-cluster-sa-54cf26acc8196920b8b92e52d85dba7e-0000.upi.containers.appdomain.cloud --ip 10.245.64.9 --ip 10.245.64.10 --ip 10.245.64.11
    ```

    Sample output from CLI:
    ```
    Deleting IP 10.245.64.11 from NLB host name ira-demo-sat-cluster-sa-54cf26acc8196920b8b92e52d85dba7e-0000.upi.containers.appdomain.cloud in cluster ira-demo-sat-cluster-satellite...
    OK
    ```

6. Add `IBM NLB DNS` for the Red Hat OpenShift cluster worker nodes

    ```
    ibmcloud ks nlb-dns add --cluster ira-demo-sat-cluster-satellite --nlb-host ira-demo-sat-cluster-sa-54cf26acc8196920b8b92e52d85dba7e-0000.upi.containers.appdomain.cloud --ip 130.198.19.169 --ip 130.198.8.105 --ip 130.198.14.65
    ```

    Sample output from CLI:
    ```
    Adding IP(s) 130.198.19.169, 130.198.8.105, 130.198.14.65 to NLB host name ira-demo-sat-cluster-sa-54cf26acc8196920b8b92e52d85dba7e-0000.upi.containers.appdomain.cloud in cluster ira-demo-sat-cluster-satellite ...
    ```




