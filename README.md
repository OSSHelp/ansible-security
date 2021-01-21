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
```

## Available parameters

| Param | Description |
| -------- | -------- |
| default_sshd_params | contains list of default params for sshd, doublecheck if you override it! |
| default_sysctl_params | contains list of default system params, doublecheck if you override it! |
| sshd_params | list for setting custom params for sshd, empty by default |
| security_disable_hidepid_changing | if set to "true" - hidepid setup will be skipped. This will not revert any of already made mount options or scripts |

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
