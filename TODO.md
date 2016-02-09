#====================================
# enable_outbound_guest_vms.yml
#====================================

# # turn on ip forwarding
# - shell: sudo -- sh -c "echo 1 >> /proc/sys/net/ipv4/ip_forward"

# # enable masqerade for eth0 (vagrant controlled) nic
# - shell: sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE


#====================================
# keypair.yml
#====================================

# Generate a new public key for demo
# - command: ssh-keygen -t rsa -N "" -f ~/.ssh/id_rsa creates=~/.ssh/id_rsa

# Creates a keypair with the running users public key
# - nova_keypair: state=present
#                 login_username=demo
#                 login_password={{password}}
#                 login_tenant_name=demo
#                 name=demo
#                 auth_url=http://{{host_ip}}:35357/v2.0/
#                 public_key="{{lookup('file','~/.ssh/id_rsa.pub')}}"


#====================================
# finalize.yml
#====================================

# Transfers the script to the remote host and runs it
# Setup DNS and open ports in the security group
# - script: finalize.sh

#====================================
# Upload images into glance from a local file store.
#====================================

# -----
#  Cirros images
# -----

# http://cdn.download.cirros-cloud.net/0.3.1/cirros-0.3.1-x86_64-disk.img
# - shell: "{{upload_script}} file:///{{vagrant_share}}/cirros-0.3.1-x86_64-disk.img"

# http://cdn.download.cirros-cloud.net/0.3.2/cirros-0.3.2-x86_64-disk.img
# - shell: "{{upload_script}} file:///{{vagrant_share}}/cirros-0.3.2-x86_64-disk.img"

# -----
#  Ubuntu 14.04 LTS images
# -----

# http://uec-images.ubuntu.com/trusty/current/trusty-server-cloudimg-i386-disk1.img
# - shell: "{{upload_script}} file:///{{vagrant_share}}/trusty-server-cloudimg-i386-disk1.img"

# http://uec-images.ubuntu.com/trusty/current/trusty-server-cloudimg-amd64-disk1.img
# - shell: "{{upload_script}} file:///{{vagrant_share}}/trusty-server-cloudimg-amd64-disk1.img"
