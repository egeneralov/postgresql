egeneralov.postgresql
=====================

Provision postgresql server installation with NORMAL configuration.

Requirements
------------

Debian-based system, supported by official repository.

Dependencies
------------

- [egeneralov.postgresql-repository](https://github.com/egeneralov/postgresql-repository)

Role Variables
--------------

See `defaults/main.yml` for full list.

- **pgdg_version**: 9.6

- **pgdg_users**:
  - user: root
    password: root
    database: root

- **pgdg_postgresql_conf**:
  - {
    "k": "listen_addresses",
    "v": "'*'"
  }
  - {
    "k": "max_connections",
    "v": "1000"
  }
  - {
    "k": "superuser_reserved_connections",
    "v": "10"
  }
  - {
    "k": "huge_pages",
    "v": "try"
  }

- **pgdg_pg_hba_conf**:
  - {
      "connection_type": "local",
      "database": "all",
      "user": "all",
      "address": "",
      "method": "peer"
    }
  - {
      "connection_type": "host",
      "database": "all",
      "user": "all",
      "address": "127.0.0.1/32",
      "method": "md5"
    }

Example Playbook
----------------

    - hosts: db
      vars:
        pgdg_users:
          - user: root
            password: root
            database: root
        pgdg_pg_hba_conf:
          - {
              "connection_type": "local",
              "database": "all",
              "user": "all",
              "address": "",
              "method": "peer"
            }
          - {
              "connection_type": "host",
              "database": "all",
              "user": "all",
              "address": "127.0.0.1/32",
              "method": "md5"
            }
          - {
              "connection_type": "host",
              "database": "all",
              "user": "all",
              "address": "192.168.0.0/24",
              "method": "md5"
            }
      roles:
         - egeneralov.postgresql

License
-------

MIT

Author Information
------------------

Eduard Generalov <eduard@generalov.net>
