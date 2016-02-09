# Devstack provisioning with VMware Fusion + Vagrant
Playbooks for building a virtualized devstack based on
Vagrant + VMware Fusion for openstack development.

## Clone the repo
```
cd ~/src
git clone git@github.com:wchrisjohnson/devstack-ansible.git devstack
```

## Create the VM & provision devstack
```
$ cd ~/devstack
$ vagrant up --provider vmware_fusion
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

    PYTHONUNBUFFERED=1 ANSIBLE_FORCE_COLOR=true ANSIBLE_HOST_KEY_CHECKING=false ANSIBLE_SSH_ARGS='-o UserKnownHostsFile=/dev/null -o IdentitiesOnly=yes -o ForwardAgent=yes -o ControlMaster=auto -o ControlPersist=60s' ansible-playbook --connection=ssh --timeout=30 --limit='default' --inventory-file=/Users/wchrisjohnson/src/webapps/devstack/.vagrant/provisioners/ansible/inventory -vv ansible/site.yml
    No config file found; using defaults
    1 plays in ansible/site.yml
    No config file found; using defaults
    1 plays in ansible/site.yml

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
