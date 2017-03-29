# Bastion test setup

## Servers
this setup creates a private network 192.168.50.*
In that network, 3 hosts are created:

- web: 192.168.50.11
- db: 192.168.50.12

and a bastion host:

- bastion: 192.168.50.10

the bastion has a second network attached, the public network. It receives an ip using DHCP.

To find the assigned ip, I included a small VBoxManage script to fetch the assigned ip's to boxes.

run it as:

```bash
./findip.sh
```

## Access
To start the servers run `vagrant up`.

run findip.sh, get the assigned ip for the bastion host, add the ip to the sshconfig file.

Only the `bastion` host is accessible over the network through ssh.

e.g. from another laptop then yours you can ssh into the bastion using its public ip.

The `db` and `web` host are not accessible.

But as these servers have a copy of your public key, they can be reached through the `bastion`.

The `bastion` is setup as an ssh proxy for both web and db in the ssh config file.

To test: 

```bash
ssh -F sshconfig vagrant@192.168.50.11
```

This command read the ssh config, proxy the ssh through the bastion, forward your private key and connect into the web server without a passwords using your locallyy stored private key.

