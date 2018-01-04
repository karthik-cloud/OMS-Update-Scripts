The script components to update OMS/OMI are:
1. remote_cmds.sh - bash script to execute commands on each target VM. The command syntax
./remote_cmds.sh -u <VM_USER_ID> -p "<VM_Password>" -f <Full path of vm list file> -c <Full path of commands file>
  
2. vmlist_qa2 - an example text file that list all VM names for the update/installation on qa2 env. This file needs be created for the target subscription env. This file can be passed as the third parameter of the command in 1. 

3. show_oms_omi_version - command file for checking the current OMS agent and OMI service version. This file can be passed as the last parameter of the command in 1. This file can be used to scan versions before updating to filter out those VMs that have older OMS and OMI version. This also can be used to verify the update status of each VM in the VM list

4. oms_update - command file to update OMS agent. To run the commands, pass the file to the last parameter of the command in 1. 

5. omi_update - command file to update OMI service. To run the commands, pass the file to the last parameter of the command in 1. 

Steps to update OMS and OMI:
1. connect to a jumpbox for a subscription env. 

2. Check if the remote_cmds.sh (the file name may slightly vary) already exist on the jumpbox. If not, create a new file for the script remote_cmds.sh. And copy the script code from remote_cmds.sh to the new script file on the jumpbox. Then run chmod +500 remote_cmds.sh

3. Create a vmlist file and copy/past all VM names to the file ( note: each VM name must end with a space)

4. Create the 3 commands files - show_oms_omi_version, oms_update and omi_update on the jumpbox if not exist

5. Run the remote_cmds.sh with show_oms_omi_version to find out the list of VMs that really needs to be updated for OMS or OMI

6. Run the remote_cmds.sh with oms_update and the vmlist that only contains those VM that really needs to be updated for OMS agent

7. Run the remote_cmds.sh with omi_update and the vmlist that only contains those VM that really needs to be updated for OMI service
