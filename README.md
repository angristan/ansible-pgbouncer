# Ansible role for pgbouncer

This role will install pgbouncer for the [PGDG APT repository](https://wiki.postgresql.org/wiki/Apt) (optional), and handle configuration and users.

To generate the `userlist.txt`, I recommend using [this script](https://github.com/angristan/pgbouncer_userlist_generator).

## Sample playbook

```yaml
---

- hosts: myhost
  roles:
    - name: pgbouncer
      tags: pgbouncer
  vars:
    pgbouncer_install_from_pgdg: true
    pgbouncer_listen_addr: '*'
    pgbouncer_pool_mode: transaction
    pgbouncer_auth_type: md5
    pgbouncer_users:
      - name: blog
        md5password: "{{ vault_pgbouncer_password_blog }}"
    pgbouncer_databases:
      - name: blog
        user: blog
        password: "{{ vault_postgresql_password_blog }}"
```
