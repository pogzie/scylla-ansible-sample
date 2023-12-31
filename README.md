# Introduction

ScyllaDB documentation provides instructions on how to deploy via cloud or via Docker. For more advanced testing on-prem, this script provides the necessary bare minimum to run and configure a ScyllaDB cluster via Ansible as the documented steps were old.

# Pre-requisites

- Ansible on the machine you will use in this operation
- Centos 7 on the target servers (you are expected to provision this yourself) 
- SSH enabled and necessary keys set on the target servers
- 3 or more IP addresses assigned (to be used in inventory.yaml)
- Private key to be used by Ansible to connect to your severs

# How to run
After configuring the inventory file with the IPs, just punch it:

```
ansible-playbook -i inventory.yaml setup.yaml
```

You can ssh in one of the nodes and check the nodetool status again: 

```
[root@scylla1 ~]# nodetool status
Datacenter: datacenter1
=======================
Status=Up/Down
|/ State=Normal/Leaving/Joining/Moving
--  Address        Load       Tokens       Owns    Host ID                               Rack
UN  192.168.251.1  656 KB     256          ?       01ef6dc3-7f08-4638-a2b9-dcb7a2760c8a  rack1
UN  192.168.251.2  1.05 MB    256          ?       59dec004-78b1-4051-ae12-e0dbaaf6b55a  rack1
UN  192.168.251.3  1.34 MB    256          ?       2075b90f-cd22-4529-9170-405c41afd094  rack1

Note: Non-system keyspaces don't have the same replication settings, effective ownership information is meaningless
```

# Todo
- Fix the serialized run. For some reason if 1 isnt ready 2 and 3 gets stuck in limbo.
- Fix adding of repo. Use the built in function.
- Waiting for service and ports works fine but nodetool fails or reports incorrect number of nodes if not finished joining. Reassess just blazing through everything and waiting for nodetool to report the correct value.
- Take one step up the deployment to completely automate the process of provisioning.
- Provision 3 or more nodes via Ansible by only using the desired ISO in ESXi or vSphere. Use built in Ansible functions for this.
- Add a retry on checking the status in the event it doesnt start properly.
- Option to set desired IP addresses for the desired nodes (this is for the provisioning process).
- Option to choose any supported operating system (OS specific commands might need a tweak, using the universal installer should work).
- Option to choose any ScyllaaDB version (Easily doable with the flag).
- Option to load sample data.

# Issues
- Initial setup works but would need another check to make sure that initialization had completed before running the nodetool command. 
- For the meantime, `journalctl _COMM=scylla -f` on each of the nodes should show the process of initialization. You can run this before running the Ansible script and watch it go brrrr.

# Disclaimer

This is just a proof of concept deployment of ScyllaDB via Ansible and should not be used in production environments. The author is not liable for any loss of data or does not provide any support for any of the code in this repository.