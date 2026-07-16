---
title: "Nextcloud"
---

Homepage: [https://nextcloud.com](https://nextcloud.com)

## Usage

Set `nextcloud_enabled: true` in your `inventories/<your_inventory>/group_vars/nas.yml` file.

Tread carefully.

External access may require that you manually configure your Fully Qualified Domain Name (FQDN) as a trusted domain within the application.  There is an environment variable set up for this in the "nextcloud task" which will most likely make manual configuration unnecessary.  If you get the following [screenshot](https://docs.nextcloud.com/server/14/admin_manual/installation/installation_wizard.html#trusted-domains) warning when trying to access nextcloud externally you'll need to manually set it up.

This can be accomplished in two commands.

```bash
# On the server where the docker containers are running
$ docker exec -it --user www-data nextcloud /bin/bash
$ php occ config:system:set trusted_domains INDEX_FOR_NEW_ENTRY_SEE_DOCS_LINK_BELOW --value=YOUR_FQDN_HERE --update-only
```

The above commands are documented in the administration guide for Nextcloud:

* [set array values](https://docs.nextcloud.com/server/14/admin_manual/configuration_server/occ_command.html#setting-an-array-configuration-value)

* [docker container docs, references environment variables](https://github.com/nextcloud/docker)

## File permissions on local/external storage (Samba shares)

Every `samba_shares` entry is bind-mounted into the Nextcloud container under `/external_storage/<name>`, and Nextcloud writes to it as `www-data`. The role creates the `ansible-nas` group inside the container with the same GID as on the host and adds `www-data` to it, and `permission_data.yml` marks each share directory setgid (`g+s`), so new files/folders that Nextcloud (or Samba, or any other app) creates under an existing share directory inherit the `ansible-nas` group instead of reverting to `www-data` or a mismatched GID. This does not affect Nextcloud's own internal storage (`nextcloud_data_directory/nextcloud`), only the external storage/share mounts.

If you still can't write to Nextcloud-created files on a share from Samba or another app in the `ansible-nas` group, it's usually because Apache's default `umask` (022) strips the group-write bit off newly created files. Fix it once with:

```bash
$ docker exec -it --user www-data nextcloud /bin/bash
$ php occ config:system:set localstorage.umask --type=integer --value=2
```

To (re)apply correct ownership/permissions to existing data (e.g. after enabling local/external storage for the first time), run the repermission playbook from the repo root, optionally scoped to a single share:

```bash
$ ansible-playbook permission_data.yml -e "permission_target=photos"
```
