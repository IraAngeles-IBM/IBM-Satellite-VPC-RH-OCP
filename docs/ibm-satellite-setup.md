## Create a Satellite Location


1. Click on the `Create a Satellite Location` button

    ![create_sat_loc](./images/create_sat_loc.png)

2. Enter the location details; 

    * Select Manual Setup (a)
    * Name of the Location (ira-demo-ibm-cloud) (b)
    * Select where the location is managed (Washington DC) (c)
    * Click on the `Create location` button (d)

    ![create_sat_loc_details](./images/create_sat_loc_details.png)

3. After creating the location, next add hosts. To add host, download the `attach host script` (e.g. attachHost-ira-demo-ibm-cloud1.sh) and run in host or upload in VPC setup. (see [VPC setup](vpc-setup.md))

    ![add-sat-host](./images/add-sat-host.png)

4. Once all the host has been attached to the location. Assign host to Control plane for Zone-1, Zone-2, Zone-3. It is required to assign host to all zones. The rest of the unassigned host will be assigned once the IBM Cloud serivce (OpenShift) is deployed.
    
    ![images/sat-assign-host](./images/sat-assign-host.png)

5. The following shows all assigned hosts.

    ![assign-sat-host](./images/assign-sat-host.png)

 