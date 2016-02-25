# Devstack provisioning with VMware Fusion + Vagrant + Ansible
Build a virtualized devstack based on Vagrant + VMware Fusion +
Ansible for openstack development. Treat your devstack like cattle,
not your pet!

Note: There is now a branch for VirtualBox
(https://www.virtualbox.org/wiki/Downloads) although it is just a copy of
master at the moment and a work in progress. Check back soon to see if it is
ready for use.

## Prequisites
The requirements to make this work are:
- Vagrant (open source, https://www.vagrantup.com/)
- VMware Fusion v7 Professional (paid, https://www.vmware.com/products/fusion)
  (professional is necessary for some of the networking elements)
- The "vagrant-vmware-fusion" plugin (paid, https://www.vagrantup.com/vmware/)
  (necessary to allow vagrant to control Fusion)
- Ansible (open source, https://www.ansible.com, available via homebrew, pip)


## Clone the repo
Fork this repo and clone it locally. PRs welcome!
```
cd <folder>
git clone git@github.com:<your account>/devstack-ansible.git devstack
```

## Create the VM & provision devstack
```
$ cd <devstack folder>
$ vagrant up
Bringing machine 'default' up with 'vmware_fusion' provider...
==> default: Cloning VMware VM: 'puphpet/ubuntu1404-x64'. This can take some time...
==> default: Checking if box 'puphpet/ubuntu1404-x64' is up to date...
==> default: Verifying vmnet devices are healthy...
==> default: Preparing network adapters...
==> default: Starting the VMware VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 172.16.255.136:22
    default: SSH username: vagrant
    default: SSH auth method: private key
    default:
    default: Vagrant insecure key detected. Vagrant will automatically replace
    default: this with a newly generated keypair for better security.
    default:
    default: Inserting generated public key within guest...
    default: Removing insecure key from the guest if it's present...
    default: Key inserted! Disconnecting and reconnecting using new SSH key...
==> default: Machine booted and ready!
==> default: Forwarding ports...
    default: -- 80 => 8888
    default: -- 3333 => 3333
    default: -- 5000 => 5000
    default: -- 8000 => 8000
    default: -- 8004 => 8004
    default: -- 8080 => 8080
    default: -- 8773 => 8773
    default: -- 8774 => 8774
    default: -- 8776 => 8776
    default: -- 9292 => 9292
    default: -- 9696 => 9696
    default: -- 35357 => 35357
    default: -- 22 => 2222
==> default: Setting hostname...
==> default: Configuring network adapters within the VM...
==> default: Waiting for HGFS kernel module to load...
==> default: Enabling and configuring shared folders...
    default: -- /Users/wchrisjohnson/src/webapps/devstack: /vagrant
    default: -- /Users/wchrisjohnson/src/vagrant_data: /vagrant_data
    ==> default: Running provisioner: ansible...
        default: Running ansible-playbook...

    PYTHONUNBUFFERED=1 ANSIBLE_FORCE_COLOR=true ANSIBLE_HOST_KEY_CHECKING=false ANSIBLE_SSH_ARGS='-o UserKnownHostsFile=/dev/null -o IdentitiesOnly=yes -o ForwardAgent=yes -o ControlMaster=auto -o ControlPersist=60s' ansible-playbook --connection=ssh --timeout=30 --limit='default' --inventory-file=/Users/wchrisjohnson/src/webapps/devstack/.vagrant/provisioners/ansible/inventory -vv ansible/devstack-deploy.yml

    No config file found; using defaults
    1 plays in ansible/devstack-deploy.yml
    No config file found; using defaults
    1 plays in ansible/devstack-deploy.yml

    PLAY ***************************************************************************

    TASK [setup] *******************************************************************
    ok: [default]

    TASK [devstack : devstack | main | Update the apt-get cache] *******************
    ok: [default] => {"cache_update_time": 1454982002, "cache_updated": true, "changed": false}
    ...

```

## Check out your fresh devstack
If you review the log file (stack.log) on the devstack VM:
```
This is your host IP address: 172.16.40.128
This is your host IPv6 address: ::1
Horizon is now available at http://172.16.40.128/dashboard
Keystone is serving at http://172.16.40.128:5000/
The default users are: admin and demo
The password: stack
```

## Devstack customization
If you want to customize the way the devstack is installed, take a look at `ansible/host_vars/default` for a few vars you can change if you like.

These vars are merged with the devstack config template at `ansible/roles/devstack/templates/devstack.j2`. The merged version of this file is pushed over to the VM into the devstack foder such that when the `stack.sh` is run, it will stand up the devstack based on the options in this config file.

## To clean up
To reset back to a clean slate and start over:
```
vagrant destroy
```
