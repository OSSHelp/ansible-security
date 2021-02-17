# security

[![Build Status](https://drone.osshelp.ru/api/badges/ansible/security/status.svg)](https://drone.osshelp.ru/ansible/security)

Role that manages security settings. For now::

- manages sshd params
- ensures /root has strict permissions
- manages hidepid param for /proc
- disables auto-upgrades

## Deploy example (do not copy blindly!)

```yaml
    - role: security
      security_disable_hidepid_changing: true
      security_ssh_keys:
        - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCtwDaffh9xxl1I8Acb40iO6fSBcDf1w7rBwc1g+eFW1vqNPyZ9WqF9HcR17ekt5uucRCVRHbKF4YKyVxSw2THt+nfLplOazSSYqoHvTrhSix22QUUTQWi9mvOTOgvnazKsR7M2tgPvUcCI5osTuRNwD7mipZyIDGTZKvnqByjgG/qX8TvoSvoqYSf7BuGsUwElGm1My6hAF3zyysNxYikPVEHULacsPKti6xj+Sl3OW7RCH8MoXsArPhlBWyupgl3FWHVwOoMJ9Fp6izvuvOLUoACSPI2glX9KrjPOy9JK9X5tFuCYg+rzClTq956Nt1rsk4TvoVHYQkYp3VOtgg1l
```

## Available parameters

| Param | Description |
| -------- | -------- |
| `default_sshd_params` | contains list of default params for sshd, doublecheck if you override it! |
| `default_sysctl_params` | contains list of default system params, doublecheck if you override it! |
| `sshd_params` | list for setting custom params for sshd, empty by default |
| `security_disable_hidepid_changing` | if set to "true" - hidepid setup will be skipped. This will not revert any of already made mount options or scripts |
| `security_ssh_keys` | contains list of public ssh key to add to the server |

## FAQ

### Is there a way to skip some configuration entirely

You can skip only hidepid setup so far. Or you can override default lists of sshd params with empty ones.

## Useful links

- [Our article about security settings](https://oss.help/kb2656), links to other articles could be found there

## Known issues

- Hidepid doesn't work if nesting disabled for unprivileged container. [More information is here](https://oss.help/82781).

## TODO

- add skip option. for example: skip ssh configuration
- improve detection of installed unattended-upgrades after [this issue](https://github.com/ansible/ansible/issues/60889)
- improve tests (and clean out commented garbage)
- should we enforce Drone public key presence in authorized_keys?
