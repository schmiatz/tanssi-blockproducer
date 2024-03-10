# What does this Repo?
This Repo contains an ansible Playbook, that will install a Tanssi-Node/Blockproducer/Relayer on your Debian/Ubuntu Server.

# How to use this Playbook?

## Requirements:
To use this Playbook you need:
- ssh access to a Machine with a user that has root permissions
- ansible installed on the Machine you want to execute the Playbook from
- declare some Varibales
- open the TCP Ports 30334 and 30335 to the Internet

## Variables to declare
### In the file 'group_vars/all.yml' you can change this variables:
- version
- system_username
- tanssi_nodename
- tanssi_blockproducername
- tanssi_relaynodename
- dancebox_state_pruning
- dancebox_block_pruning
- westend_state_pruning
- westend_block_pruning

### Examples and explanation
#### version
The Version the Binary of Tanssi-Node will be pulled from GitHub.    
```
verion: latest
```

#### system_username
Thats the username of your Ubuntu/Debian User.
If you login into your System for example with the command 'ssh tanssi@<IP-ADDRESS>' your system_username is 'tanssi'.   
```
system_username: tanssi
```

#### tanssi_nodename and all the other tanssi_ names
Thats the Public Name your Node/Blockproducer/Relayer will have.     
You can find your Node here, using the Name you defined here for your Node.   
[Telemetry](https://telemetry.polkadot.io/#list/0x27aafd88e5921f5d5c6aebcd728dacbbf5c2a37f63e2eda301f8e0def01c43ea)
```
tanssi_nodename: tanssi-user
tanssi_blockproducername: tanssi-user
tanssi_relaynodename: tanssi-user
```

#### dancebox_state_pruning and westend_state_pruning
Setup the state Pruning for the dancebod and westend chain here.   
```
dancebox_state_pruning: 2000
westend_state_pruning: 100
```

#### dancebox_block_pruning and westend_block_pruning
Setup the block Pruning for the dancebod and westend chain here.   
```
dancebox_block_pruning: 2000
westend_block_pruning: 100
```

### In the file 'inventory.yml' you need to change this variables:
- ansible_host

### Examples and explanation
#### ansible_host
Thats the IP-Address of your Target Machine.
Your Machine needs to be accessable using ssh with that IP.
```
ansible_host: 192.168.1.10
```

# Run the Playbook
## Execute Ansible
cd into this Repo and run the Playbook with 'ansible-playbook playbook.yml'

## Check your Machine after the run
Have a look in the logs of your newly created Services with 'journalctl -fu tanssi'.   

# How to update my Tanssi Server?
Just run the playbook again.   
It will download the relase that is tagged as "latest" in the GitHub and will restart the tanssi Service afterwards if the downloaded Version is not the same that is already running.   