## Create Satellite Locations, Attach and Assign host

## Create Satellite Location

Go to Satellite -> Locations, then `Create Location` button.  Select `Manual setup`, enter the preferred Satellite location `Name`, select the appropriate location where the host will be `Manage from` (e.g. London or Washington DC). Confirm all information then proceed to `Create Location`. 


![Create Sat Location](images/create-sat-loc.png)

## Attach host to the location

1. After successful creation of the Satellite location, proceed to the location, select `Host`, then `Attach host`.

    ![attach host](images/attach-host.png)

2. Download the script, labels can be added before downloading the script. 

    ![download-script](images/download-script.png)

3. Copy the script from your local machine to the host

    ```
    scp -i <filepath_to_key_file> <filepath_to_script> <username>@<IP_address>:/tmp/attach.sh
    ```

4. Log in to the host

    ```
    ssh -i <filepath_to_key_file> <username>@<IP_address>
    ```

5. Run the script.  Add sudo for rootless login.

    ```
    nohup bash /tmp/attach.sh &
    ```

6. Monitor the progress of the registration script

    ```
    journalctl -f -u ibm-host-attach
    ```

7. Check the host in the Satellite location

    ![host-ready](images/host-ready.png)

## Assign host to the Control plane

1. Select the `Ready` and `Unassigned` host to the Control plane. 

    ![select-host-assign](images/select-host-assign.png)

2. Assign host to the zone.

    ![assign-host](images/assign-host.png)

3. The host will be provisioned

    ![host-provision](images/host-provision.png)

