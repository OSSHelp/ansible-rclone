# rclone

[![Build Status](https://drone.osshelp.ru/api/badges/ansible/rclone/status.svg)](https://drone.osshelp.ru/ansible/rclone)

## Description

The role installs the [rclone](https://rclone.org/).

## Deploy examples

### Minimal

Example installs the latest rclone version with no configuration.

```yaml
  roles:
    - role: rclone
```

### With storages and rsa key

```yaml
  roles:
    - role: rclone
      storages:
        - {name: b2_storage1_name, type: b2, account: "{{ b2_storage1_account_from_vault }}", key: "{{ b2_storage1_key_from_vault }}"}
        - {name: b2_storage2_name, type: b2, account: "{{ b2_storage2_account_from_vault }}", key: "{{ b2_storage2_key_from_vault }}"}
        - {name: sftp_storage_name, type: sftp, host: storage_host, user: user_name, key_file: /root/.ssh/id_rsa.backup, md5sum_command: none, sha1sum_command: none }
        - {name: another_storage_name, type: another_type, some_key: some_value}
      backup_private_key: "{{ private_key_for_sftp_storage_from_vault }}"
```

The short universal example:

``` yaml
# vault
some_storage: {name: storage_name, type: storage_type, storage_param: param_value, storage_secret: "some_secret_here"}

# playbook
roles:
  - role: rclone
    storages:
      - "{{ some_storage }}"
```

The example with rsa key in vault:

``` yaml
# vault
backup_storage_private_key: |
  -----BEGIN RSA PRIVATE KEY-----
  MIIEogIBAAKCAQEAkbzwXuOIv0BCclEkMSNd57DIR64pLUiSZ1wCPY6bmSlg3aWX
  ...
  3kaa4TWqH9eO5hNxyJqymrXQcBj22bX+gRVOQRje6HxmBqGp8uU=
  -----END RSA PRIVATE KEY-----

# playbook
roles:
  - role: rclone
    backup_private_key: "{{ backup_storage_private_key }}"
```

### A custom url for the rclone package

```yaml
  roles:
    - role: rclone
      rclone_package_url: "https://downloads.rclone.org/v1.50.2/rclone-v1.50.2-linux-amd64.deb"
```

## FAQ

...

## Useful links

- [Official documentation](https://rclone.org/docs/)
- [Our article](https://oss.help/kb1026)

## TODO

...

## License

GPL3

## Author

OSSHelp Team, see <https://oss.help>
