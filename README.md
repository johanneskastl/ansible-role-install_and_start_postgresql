![Ansible Lint](https://github.com/johanneskastl/ansible-role-install_and_start_postgresql/workflows/Ansible%20Lint/badge.svg)

# install_and_start_postgresql

Role to just setup a postgreSQL database without much configuration.

## Requirements

Setting a password for the PostgreSQL superuser (normally called `postgres`)
requires a Python module called `psycopg2` to be installed.

If you tell the role to set a superuser password, the python module will be
installed automatically on the target system (not the Ansible control host).

## Role Variables

### Optional variables

- `only_listen_on_localhost` (Boolean): Set this to `false` to have this role
  adjust the settings, so PostgreSQL listens on all IP addresses, not just on
  `localhost`
- `postgresql_superuser_password` (String): If you set this variable (of course
  using some Ansible Vault encrypted file...), the role will install the
  psycopg2 python module and set a password for the PostgreSQL superuser
  (normally called `postgres`). If it is unset, then there will not be a
  password set for this user, as usual.

### OS-related variables

There are some variables that are depending on the operating system. For most
Linux distributions, those should be fine. In case you want to override them,
feel free to do so:

- `postgresql_package_name` (String): Name of the package containing the
  PostgreSQL server (defaults to `postgresql16-server`)
- `postgresql_service_name` (String): Name of the PostgreSQL systemd unit name
  (default: `postgresql.service`)
- `path_to_postgresql_conf` (String): Path to the `postgresql.conf` file, needed
  in case you want the database to not only listen on `localhost` (default:
  `/var/lib/pgsql/data/postgresql.conf`)
- `postgresql_system_user` (String): System user for the PostgreSQL database
  (default: `postgres`)
- `psycopg2_package_name` (String): Name of the package containing the psycopg2
  Python module (default: `python3-psycopg2`)

## Dependencies

None

## Example Playbook

```yaml
- hosts: servers
  roles:
    - role: 'johanneskastl.install_and_start_postgresql'
```

## License

BSD-3-Clause

## Author Information

I am Johannes Kastl, reachable via git@johannes-kastl.de
