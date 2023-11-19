# Introduction

ScyllaDB documentation provides instructions on how to deploy via cloud or via Docker. For more advanced testing on-prem, this script provides the necessary bare minimum to run and configure a ScyllaDB cluster via Ansible.

# Pre-requisites

- Centos 7  (you are expected to provision this yourself) 
- SSH enabled and necessary keys set on the machines
- 3 IP addresses assigned (to be used in scylla_allnodes.yaml)
- Private key to be used by Ansible to connect to your severs

# How to run

# Todo
- Take one step up the deployment to completely automate the process
- 3 nodes via Ansible by only using the desired ISO
- Option for more nodes
- Option to set desired IP addresses for the desired nodes
- Option to choose any supported operating system
- Option to choose any ScyllaaDB version
- Option to load sample data

# Issues

# Disclaimer

This is just a proof of concept deployment of ScyllaDB via Ansible and should not be used in production environments. The author is not liable for any loss of data or does not provide any support for any of the code in this repository.
