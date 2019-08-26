# VPN Setup

To log into the MGI cluster and access IT services on your personal laptop or offsite, you will need to set up a VPN. Instructions on downloading and setting up Cisco AnyConnect are here: https://wustl.app.box.com/s/o7lvu49qkrr20xauj1lq6bcgft2zu87a

Note: your VPN login credentials are your WUSTL Key and password

# Logging in to the MGI cluster

In order to log into the MGI cluster, you will need to have your MGI username and password set up. You can choose to connect to any of the following machines:
  * `virtual-workstation1`
  * `virtual-workstation2`
  * `virtual-workstation3`
  * `virtual-workstation4`
  * `virtual-workstation5`

To log in to `virtual-workstation3`:
```
ssh your-MGI-username@virtual-workstation3.gsc.wustl.edu
# your-MGI-username@virtual-workstation3.gsc.wustl.edu's password: [Enter your MGI password]
```

# Password-less log in
By default, you are required to enter in your password each time you access the cluster.
To save time, you can grant password-less access for your lab computer with RSA keys.

On your laptop:
```bash
cd ~/.ssh/

ssh-keygen -t rsa
# Generating public/private rsa key pair.
# Enter file in which to save the key (/Users/username/.ssh/id_rsa):
# Enter passphrase (empty for no passphrase):
# Enter same passphrase again:
# Your identification has been saved in /Users/username/.ssh/id_rsa.
# Your public key has been saved in /Users/username/.ssh/id_rsa.pub.
# The key fingerprint is:
# y8:20:3f:z9:ab:31:c9:94:3b:kc:e4:0d:4c:dd:3c:f9 username@laptop.local
# The key's randomart image is:
# +--[ RSA 2048]----+
# |                 |
# |                 |
# |                 |
# |       . o o .   |
# |    . o Z . =    |
# |     o X .   o   |
# |      * @     E  |
# |       O =       |
# |      ..=..      |
# +-----------------+

# Copy the contents of `id_rsa.pub` to your clipboard
cat id_rsa.pub
# ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC5JGfmgoqjwZs3S5v87Yph7hBwK046EPdAlJ4nxqUDT21kRSfrtdLvezhugg68CGjODCG91V9ABAQC5JGfmgoqjwZs3S5v87Yph7hBwKTx5Nok2tNoJUoMNSCyloNhtQGKFAugexhvcdz57wGzsWzmZGaxPZeLpUxcTWn3MljROT8oU52wUBcfTMSJQfCerqmw+DFVoSkSlO/mhP7tmZxzAL0baRKSZHhEf2vhMfJxLABhUFjeCyWp7MWzEQd+NZ4I1F8AcoxYepM1FaykreCEWC72fcQz9iz226dOrnsaNxj0dOC1sAY5ysSAkyD username@laptop.local

# Set the proper permissions on your keys
chmod 700 ~/.ssh && chmod 600 ~/.ssh/*
```

On the MGI cluster:
```bash
mkdir -p ~/.ssh
cd ~/.ssh

# edit the `authorized_keys` file on the server
vi ~/.ssh/authorized_keys
# Press i to enter Insert Mode, paste in the public key from above, then save and exit the file by pressing ESC followed by ZZ

# Set the proper permissions on your keys
chmod 700 ~/.ssh && chmod 600 ~/.ssh/*

```
