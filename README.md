# Arch Linux with MATE Desktop

Provisions an Arch Linux VM with MATE Desktop via Ansible and Vagrant.

Requires Ansible 2.4+ and Vagrant with vagrant-reload plugin.

Vagrant provider is VirtualBox.

## Running

Just 

```
vagrant plugin install vagrant-reload
vagrant up
```
to run.

## Setting a default user password
Passwords passed to the Ansible user module need to be pre-hashed. This command can generate the hash:
```
ansible all -i localhost, -m debug -a "msg={{ 'mypassword' | password_hash('sha512', 'mysecretsalt') }}"
```


