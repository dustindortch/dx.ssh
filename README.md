# dx.ssh

Setup SSH Key-Based Authentication

## Summary

Using key-based authentication streamlines working with remote hosts via Ansible.  This works for ad-hoc commands or playbooks.  To perform this operation, generate a new public/private key-pair with the `gen_keys.sh` script, or otherwise.  This will create the following files:

* `.ssh` - directory to hold keys
* `.ssh/id_rsa` - private key file (protect this file)
* `.ssh/id_rsa.pub` - public key file (uploaded to remote hosts)

## NOTE

This will remove any existing keys from the `~/authorized_keys` files.
## Execution

Modify the `ssh_vars.yml` file to contain the proper username and comment out the `ansible_ssh_private_key_file` property.

This can be added to an existing playbook directory and executed as its own playbook, first using the password:

```sh
# ansible-playbook ssh.yml --ask-pass
PLAY [ssh establish key-based authentication]

TASK [ssh make key directory]
...

TASK [ssh public key upload]
...

PLAY RECAP
...
#
```

After it has executed, uncomment the `ansible_ssh_private_key_file` property, then execute it again without the `--ask-pass` property:

```sh
# ansible-playbook ssh.yml
PLAY [ssh establish key-based authentication]

TASK [ssh make key directory]
...

TASK [ssh public key upload]
...

PLAY RECAP
...
#
```

Add the ssh_vars.yml file to your existing playbook.
