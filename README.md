Ansible Role: SSH Key Rotation
=========

A role that can rotate SSH keys as frequently as daily. If a default provisioning key is supplied it will be removed after generating a new key.

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.


Default remote user used by ansible controller
```yaml
ssh_host_user: ansible
```

Path and file name for the master key, used for ongoing ansible controller's remote connection
```yaml
ssh_key_path: .keychain/ssh-master-key
```

Path and file name for the default dummy key, used for initial provisioning
```yaml
dummy_key_path: .keychain/dummy-default-key
```

Setting to "true" will remove all other public keys from the remote user's authorized_keys file
```yaml
exclusive: false
```

Setting to "true" will create .ssh directory and authorized_keys file, plus set permissions
```yaml
should_manage_dir: false
```

The length of the new key in bits
```yaml
ssh_key_bits: 2048
```

Comment to be added to the new public key
```yaml
date: "{{ lookup('pipe','date +%Y%m%d') }}"
ssh_key_comment: 'amk-{{ date }}-@ansible-controller' # Ansible Master Key (AMK)
```

Dependencies
------------

None

Example Playbook
----------------

```yaml
---
- hosts: all
  roles:
    - { role: joshrooz.ssh-key-rotation }
```

License
-------

MIT

Author Information
------------------

This role was created by Josh Roose in July 2020, and was originally forked from [nyambati/ssh-key-rotation](https://github.com/nyambati/ssh-key-rotation).