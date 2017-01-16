[![Build Status](https://travis-ci.org/chouseknecht/mariadb-container.svg?branch=master)](https://travis-ci.org/chouseknecht/mariadb-container)

# Role Name

Use this role to add a mariadb service to your Ansible Container project. 

Run the following commands to install the service:

```
# Set the working directory to your Ansible Container project root
$ cd myproject

# Install the service
$ ansible-container install chouseknecht.mariadb-container
```
### Database init

The first time you start a container, a new database will be created along with a database user, and a root user. See Role Variables below for how to set the database name, the username and password, and the root password.

### Database access

Access the database on exposed port 3306.

### Mariadb version

By default version 10.2.0 will be installed. View avaible version at the [mariadb yum index](http://yum.mariadb.org/), and update *mariadb_version* in `main.yml` with the version to be installed.

### Data directory

The data directory is */var/lib/mysql*. If you want to store the database outside of the container, which is generally a good idea, mount a host path or a named volume to this path. Otherwise, the database will be destroyed whenever the container is destroyed.

*NOTE*: During the image `build` process, anything in the data directory will be destroyed, so be careful when attempting to mount a pre-existing database.

Role Variables
--------------

Set the following environment variables in `container.yml`:

MARIADB_DATABASE: mysql
> Name of the database. The first time the container starts a new database with this name will be created.

MARIADB_USERNAME: admin
> Database username.

MARIADB_PASSWORD: admin
> Database password.

MARIADB_ROOT_PASSWORD
> Password for the `root` user. If a password is not supplied, a random password will be created, and displayed in the log the first time the container starts.

The following variables can be set in `main.yml`:

mariadb_vesion: 10.2.0
> Set the version of mariadb server to intall. See the [mariadb yum index](http://yum.mariadb.org/) for available versions.

mariadb_clean_yum_cache: yes
> Set to *no* during development to speed yum package installs.

Deploying to OpenShift
----------------------

The following is a suggested `container.yml` to use when deploying the mariadb service to OpenShift. Modifications include:
  
- Providing a default password for MARIADB_ROOT_PASSWORD
- Defining a named volume and persistent volume claim (PVC) that gets mounted to */var/lib/msyql* in the container, which makes sure the database will persist beyond the life of the container.

```
mariadb:
    image: centos:7
    entrypoint: [/usr/bin/entrypoint.sh]
    working_dir: /
    user: mysql
    command: [/usr/bin/dumb-init, mysqld]
    environment:
    - MARIADB_DATABASE=mysql
    - MARIADB_USERNAME=admin
    - MARIADB_PASSWORD=foo
    - MARIADB_ROOT_PASSWORD=sesame
    expose:
    - 3306
    volumes:
    - mysql-data:/var/lib/mysql:rw
    options:
      openshift:
        persistent_volume_claims:
        - volume_name: mysql-data
          claim_name: mysql-data
          access_modes:
          - ReadWriteOnce
```

The easiest way to create a local cluster, is by using the [cluster-up-role](https://galaxy.ansible.com/chouseknecht/cluster-up-role). To create the video mentioned below, we used this role to instantiate a local cluster prior to running the deployment steps.

Here is the complete list of commands to install the role, build the image, and deploy a mariadb service to a local OpenShift instance:

```
# Create a new project folder
$ mkdir mariadb

# Set the working directory 
$ cd mariadb 

# Initialize the Ansible Container directory 
$ ansible-container init

# Install the role
$ ansible-container install chouseknecht.mariadb-container

# Build the image
$ ansible-container build 

# Create the deployment role and playbook
$ ansible-continer shipit openshift --local-images 

# Set the working directory to ansible
$ cd ansible

# Run the playbook to complete the deployment
$ ansible-playbook shipit-openshift.yml 
```

Click on the following image to view a video of the deployment, and a look at the runnig service from inside the OpenShift console:

[![Deploy Mariadb](https://github.com/chouseknecht/mariadb-container/blob/images/images/deploy-mariadb.png)](http://www.youtube.com/watch?v=93YJGK-6nEo)

Dependencies
------------

None.

License
-------

Apache v2

Author Information
------------------

[@chouseknecht](https://github.com/chouseknecht)

