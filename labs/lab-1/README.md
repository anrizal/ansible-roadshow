# Getting started

You are the operator at tangible labs inc and tasked with setting up servers for the compagnys new application, based on wildfly-swarm. After attending several sessions on automation, you've decided to give Ansible a go.

The first lab will help you verifying the Ansible installation and getting aquainted with basic Ansible concepts.

First let's verify that Ansible has been installed. On the commandline run the following command:

```
$ansible --version
```

you should see an output like the following

```
$ansible --version
ansible 2.4.2.0
  config file = /etc/ansible/ansible.cfg
  configured module search path = [u\'/root/.ansible/plugins/modules\', u\'/usr/share/ansible/plugins/modules\']
  ansible python module location = /usr/lib/python2.7/site-packages/ansible
  executable location = /bin/ansible
  python version = 2.7.5 (default, May  3 2017, 07:55:04) [GCC 4.8.5 20150623 (Red Hat 4.8.5-14)]
```

As you can see Ansible uses python. If you inspect the config file (/etc/ansible/ansible.cfg) file, you will find the following configuration

```
[defaults]

# some basic default values...

#inventory      = /etc/ansible/hosts
#library        = /usr/share/my_modules/
#module_utils   = /usr/share/my_module_utils/
```

most important for a beginning is the default location of the inventory file. The inventory file contains a list of the servers, you are managing. The servers can be grouped in any way you like. For this lab, group the servers into load balancers (lbservers) and wildfly swarm application servers (wildflyservers). In this lab, you'll share the environment with other users, therefore, you can't write in the shared inventory file. Instead in the folder *$WORK_DIR* create a file named *hosts*. 

Please note, you got three servers assigned to you, it doesn't matter which one is put in the [lbservers] section and which remaining two are put in the [wildflyservers] section during lab 1.

Add the following text in the file:

```
[lbservers]
systemX.sudodemo.net

[wildflyservers]
systemX.sudodemo.net
systemX.sudodemo.net
```

where X are replaced by the numbers for servers assigned to you. You are now ready to run your first Ansible module. To do so, run the following command from *$WORK_DIR*:

```
ansible -i hosts -u root all -m ping
```

This command will run the ping command on all servers in the hosts file (specified by -i). The -u parameter is used to sign into the servers as the root user. You might be asked to accept the identity of the servers. Type yes for each server. After running the ping command, you'll have following output

```
35.159.18.245 | SUCCESS => {
    "changed": false, 
    "ping": "pong"
}
54.93.67.223 | SUCCESS => {
    "changed": false, 
    "ping": "pong"
}
54.93.150.126 | SUCCESS => {
    "changed": false, 
    "ping": "pong"
}
```

Congratulations! You've run your first Ansible command.
For a more detailed explanation of, what is going on, try running

```
ansible -vvv -i hosts -u root all -m ping
```

Basically the command will ssh to each host and run the ping module on the host. The result is captured by Ansible in a return variable. (If you are interested in the content of a module, see the source code for the ping module [in the github repo for modules](https://github.com/ansible/ansible-modules-core/blob/devel/system/ping.py). You don't have to. Modules will be covered in a later lab.)

In the next lab, you'll write your first playbook, using the ping module, to get a better understanding of how Ansible works.
