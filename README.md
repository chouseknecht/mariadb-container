Role Name
=========

Use this role to add a mariadb service to your Ansible Container project. The first time you start the container, a root user and a database will be created. See Role Variables below for how to set the database name, username, password, and root password. Connect to the database on port 3306.

Run the following commands to install the service:

```
# Set the working directory to your Ansible Container project root
$ cd myproject

# Install the service
$ ansible-container install chouseknecht.mariadb-container-role 
```

Role Variables
--------------

MARIADB_DATABASE
> Name of the database. The first time the image is used it will creare a new database with this name. Defaults to `mysql`.

MARIADB_USERNAME
> Database username. Defaults to admin.

MARIADB_PASSWORD
> Database password. Defaults to admin.

MARIADB_ROOT_PASSWORD
> Password for the `root` user. If a password is not supplied, a random password will be created and displayed the first time the container is started.

Dependencies
------------

None.


License
-------

Apache v2

Author Information
------------------

[@chouseknecht](https://github.com/chouseknecht)

