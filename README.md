Role Name
=========

Use this role to add a mariadb service to your Ansible Container project.

Role Variables
--------------

MARIADB_DATABASE
> Name of the database. The first time the image is used it will creare a new database. Defaults to `mysql`.

MARIADB_USERNAME
> Database username. Defaults to admin.

MARIADB_PASSWORD
> Database password. Defaults to admin.

MARIADB_ROOT_PASSWORD
> Password for the `root` user. If a password is not supplied, a random password will be created and displayed the first time the container is started.

Dependencies
------------

None.


Example Playbook
----------------

This role will add a `mariadb` service to your Ansible Container project. See the `container.yml` for details. 

License
-------

GPLv3

Author Information
------------------

[@chouseknecht](https://twitter.com/chouseknecht)
