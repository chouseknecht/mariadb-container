Role Name
=========

[![Build Status](https://travis-ci.org/chouseknecht/mariadb-container.svg?branch=master)](https://travis-ci.org/chouseknecht/mariadb-container)

Use this role to add a mariadb service to your Ansible Container project. The first time you start the container, a root user and a database will be created. See Role Variables below for how to set the database name, username, password, and the root password. Connect to the database on port 3306.

Run the following commands to install the service:

```
# Set the working directory to your Ansible Container project root
$ cd myproject

# Install the service
$ ansible-container install chouseknecht.mariadb-container-role 
```

Data Directory
--------------
The default data directory is */var/lib/mysql*. If you want to store the database outside of the container, which is generally a good idea, mount a host path or a named volume to this path. Otherwise, the database will be destroyed whenever the container is destroyed.

*WARNING:* During the `build` process, anything in the data directory will be destroyed, so be very carefule, if you're attempting to mount a pre-existing database. You'll want to do that post build. 

Role Variables
--------------

Set the following environment variables in container.yml:

MARIADB_DATABASE
> Name of the database. The first time the image is used it will creare a new database with this name. Defaults to `mysql`.

MARIADB_USERNAME
> Database username. Defaults to admin.

MARIADB_PASSWORD
> Database password. Defaults to admin.

MARIADB_ROOT_PASSWORD
> Password for the `root` user. If a password is not supplied, a random password will be created and displayed the first time the container is started.

The following variables are set in defaults/main.yml and can be overriden at execution time:

```
# Set the path to mysql data files
mariadb_datadir: /var/lib/mysql

# Set the location of the Unix socket file
mariadb_socket: /var/lib/mysql/mysql.sock

# Set the port on which mysqld listens. 
mariadb_port: 3306

# Set to 'no' during development to speed yum package installs
mariadb_clean_yum_cache: yes
```

Dependencies
------------

None.

License
-------

Apache v2

Author Information
------------------

[@chouseknecht](https://github.com/chouseknecht)

