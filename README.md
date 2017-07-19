# Deploying Django App on remote Ubuntu EC2 instance with Ansible #

To ansible make SSH in remote system add ansible server public key ``(/home/ubuntu/.ssh/id_rsa.pub)`` into the ``/home/ubuntu/.ssh/authorized_keys`` file of each remote machine. Now, we need to make sure that no ssh key check prompt should take place while ansile SSH in any target server. Change the value of **host_key_checking** value in ``/etc/ansible/ansible.cfg`` file of ansible server to false.

```
[defaults]
host_key_checking = False
```

To deploy app first make sure that python 2.7 and simplejson are installed in the remote machine. If not then install the following in each of the remote mahcine.

```
$ sudo apt-get install python-setuptools
$ sudo easy_install simplejson
```

Then write down the target remote mahcine IP addresses in the **hosts** file as per the syntax.

```
[server]
192.168.0.100
172.16.0.156
192.168.2.100
```

Make sure that **requirements.txt** is placed in the app directory or you can change the location in the ansible file. Before deploying app you can also check ansible file for any syntax error. Finally, run ansible-playbook command to deploy the application.

```
$ ansible-playbook main.yml --syntax-check
$ ansible-playbook main.yml
```
