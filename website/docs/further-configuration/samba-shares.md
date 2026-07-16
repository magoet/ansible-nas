# Samba Shares

Ansible-NAS uses the awesome [vladgh.samba](https://github.com/vladgh/ansible-collection-vladgh-samba) Ansible role to configure Samba - check out [the Ansible Galaxy page](https://galaxy.ansible.com/vladgh/samba) for the many different options you can use to configure a share.

## Share Examples

Ansible-NAS shares are defined in the `samba_shares` section within `group_vars/all.yml`. The examples provided are "public" shares that anyone on your LAN can read and write to.

## File Permissions

Ansible-NAS creates an `ansible-nas` user and group on your server, which Samba will use to access the data in your shares. New data created will be permissioned correctly.

However, if you have existing data this will need to be repermissioned so that Samba (and apps like Nextcloud using local/external storage) can read and write it. A playbook is provided to do this for you - `permission_data.yml`. It is separated from the main Ansible-NAS playbook due to the time it can take to run with large amounts of data - you should only need to run this once per share.

It uses native `find`/`chown`/`chmod` (much faster than a recursive `ansible.builtin.file` on large media libraries) and sets the setgid bit on every directory, so files created later by any app running as a different user (Nextcloud, Samba, etc.) keep inheriting the `ansible-nas` group instead of drifting back to the wrong owner. It's safe to re-run at any time - it only touches entries that aren't already correct.

By default it repermissions every configured share. To target just one (useful after adding a new share, or fixing one app's storage), run:

```bash
$ ansible-playbook permission_data.yml -e "permission_target=movies"
```
