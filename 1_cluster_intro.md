# VPN setup

To log into the MGI cluster and access IT services on your personal laptop or offsite, you will need to set up a VPN. Instructions on downloading and setting up Cisco AnyConnect are here: https://wustl.app.box.com/s/o7lvu49qkrr20xauj1lq6bcgft2zu87a

Note: your VPN login credentials are your WUSTL Key and password

# Logging in to the MGI cluster

The MGI cluster is where we store data and do most of our computation.

In order to log into the MGI cluster, you will need to have your MGI username and password set up. You can choose to connect to any of the following machines:
  * `virtual-workstation1`
  * `virtual-workstation2`
  * `virtual-workstation3`
  * `virtual-workstation4`
  * `virtual-workstation5`

To log in to `virtual-workstation3`:
```bash
ssh your-MGI-username@virtual-workstation3.gsc.wustl.edu
# your-MGI-username@virtual-workstation3.gsc.wustl.edu's password: [Enter your MGI password]
```

# Password-less log in
By default, you are required to enter in your password each time you access the cluster.
To save time, you can grant password-less access for your lab computer with RSA keys.

**In a terminal on your laptop**:
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

**In a terminal after logging in to the MGI cluster:**
```bash
mkdir -p ~/.ssh
cd ~/.ssh

# edit the `authorized_keys` file on the server
vi ~/.ssh/authorized_keys
# Press i to enter Insert Mode, paste in the public key from above, then save and exit the file by pressing ESC followed by ZZ

# Set the proper permissions on your keys
chmod 700 ~/.ssh && chmod 600 ~/.ssh/*
```

# Directory setup
Create your own directory on disk `gc2802` as follows:
```
mkdir /gscmnt/gc2802/halllab/your-username
```

You are free to organize the contents of that directory as desired. However, we
recommend the following structure:

- projects
  - analysis projects, generally organized into separate publications
- src
  - external software as well as internal source code and git repositories
- bin
  - executable files that are symbolic linked to binaries in the `src` directory
- scratch
  - uncategorized and temporary analyses

You can create the above directories with the following command:
```bash
cd /gscmnt/gc2802/halllab/your-username
mkdir -p projects src bin scratch
```

# Environment setup
Add the following line to the end of this file: `~/.bashrc`  

```bash
export PATH=/gscmnt/gc2719/halllab/bin:/gscmnt/gc2719/halllab/src/anaconda-2.0.1/bin:$PATH
```

## Useful `.bashrc` lines

Add any or all of these to your `~/.bashrc` file to customize your environment.
The system will automatically run this file each time you log on. If you modify it,
your changes will appear after logging out and back in, or after you run `source ~/.bashrc`.

```bash
# terminal prompt as [username@blade14-4-10 current-dir]$
export PS1='[\u@\h \W]\$ '

# For less, don't fold long lines (-S), show detailed line data (-M), ignore case when searching (-i)
# also, use zless to open gzipped files
LESS="-SMi"
alias less='zless -S'

# make the "ls" colors more readable on a black background
export LS_COLORS="di=01;37;44:ln=01;36:pi=40;33:so=01;35:bd=40;33;01:cd=40;33;01:or=01;05;37;41:mi=01;05;37;41:ex=01;32"
LS_COLORS=$LS_COLORS:'*.tar=01;31'  # tar Archive             = Bold, Red
LS_COLORS=$LS_COLORS:'*.tgz=01;31'  # tar/gzip Archive        = Bold, Red
LS_COLORS=$LS_COLORS:'*.tbz2=01;31' # tar/bzip2 Archive       = Bold, Red
LS_COLORS=$LS_COLORS:'*.Z=01;31'    # compress Archive        = Bold, Red
LS_COLORS=$LS_COLORS:'*.gz=01;31'   # gzip Archive            = Bold, Red
LS_COLORS=$LS_COLORS:'*.bz2=01;31'  # bzip2 Archive           = Bold, Red
LS_COLORS=$LS_COLORS:'*.zip=01;31'  # zip Archive             = Bold, Red
LS_COLORS=$LS_COLORS:'*.dmg=01;31'  # Disk Image              = Bold, Red

# human readable directory listing sorted by recently modified
alias l='ls --color -lhtr'
```

---

# Submitting jobs
To start your work, the first step is to submit a job to an LSF queue. See: https://confluence.ris.wustl.edu/display/ITKB/LSF. Note that this link will only work while on the VPN. Consult the child pages to learn how to manage LSF jobs.
In order to submit a job (whether interactive or non-interactive), you must submit a `bsub` command.

### DO NOT do work on the virtual-workstation machines - use an interactive docker session instead

To start an interactive LSF job, execute the following command:
```bash
bsub -Is -q docker-interactive -R 'rusage[gtmp=1] select[gtmp>1]' -a 'docker(registry.gsc.wustl.edu/genome/genome_perl_environment)'  /bin/bash -l
```

To exit an interactive LSF job, type `exit`.

To submit a non-interactive job:
```bash
bsub -q long -g my_group -J my_name \
     -M 8000000 -N -u myemail@genome.wustl.edu \
     -a 'docker(registry.gsc.wustl.edu/genome/genome_perl_environment)' \
     -oo /gscmnt/gc2802/halllab/your-username/path/output_file \
     -R 'select[mem>8000 && gtmp>2] rusage[mem=8000, gtmp=2]' \
     /usr/bin/myprogram
```
For details on the meaning of these options, see https://confluence.ris.wustl.edu/display/ITKB/How+to+submit+LSF+jobs. This page does not include the `-a` option for specifying a Docker container, but this option is required for the job to run on the MGI cluster. Note that you must be on the VPN to view this page.

# Docker

The MGI cluster is Docker-enabled. This means that any job running on the cluster must be inside a "container". A good default Docker container for day-to-day use (used above) is: registry.gsc.wustl.edu/genome/genome_perl_environment.
You don't need to understand much about Docker to use the MGI cluster, but if you are interested in learning more about Docker, here is a reference: https://confluence.ris.wustl.edu/display/ITKB/Docker. Note that you must be on the VPN to view this page.

**Useful Docker images:**

A collection of useful Docker images can be found in this repository: https://github.com/hall-lab/docker-toolbox. Note that you will need to be added to the Hall lab GitHub group to be able to view this repository.

# Job groups
In order to make sure everyone can run jobs on the cluster, if launching a large number of jobs, you should limit the number of jobs running at once by using a job group. For more information on using job groups, see: https://confluence.ris.wustl.edu/pages/viewpage.action?pageId=27592450. Note that you must be on the VPN to view this page.

---

# Transferring files between the cluster and your local machine

To transfer files from your local machine to the cluster, type the following on your local machine:
```bash
rsync -avP /local/path/to/myfile your-MGI-username@virtual-workstation1.gsc.wustl.edu:/gscmnt/path/to/destination
```

To transfer files from the cluster to your local machine, type the following on your local machine:
```bash
rsync -avP your-MGI-username@virtual-workstation1.gsc.wustl.edu:/gscmnt/path/to/myfile /local/path/to/destination
```

---

# Basic cluster etiquette

A few things to keep in mind when working on the cluster:
* Do all of your work in your own directory
* Do not modify files in shared directories or other user's directories
* Do not launch large numbers of jobs at a time without limiting them with a job group
* We recommend launching a test job before launching many parallel jobs
* If you aren't sure about something, ask!
