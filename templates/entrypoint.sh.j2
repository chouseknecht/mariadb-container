#!/bin/bash

function generate_passwd_file() {
  export USER_ID=$(id -u)
  export GROUP_ID=$(id -g)
  grep -v ^mysql/etc/passwd > "$HOME/passwd"
  echo "mysql:x:${USER_ID}:${GROUP_ID}:MariaDB Server:${HOME}:/bin/bash" >> "$HOME/passwd"
  export LD_PRELOAD=libnss_wrapper.so
  export NSS_WRAPPER_PASSWD=${HOME}/passwd
  export NSS_WRAPPER_GROUP=/etc/group
}

export HOME=/var/lib/mysql

generate_passwd_file
whoami

if [ -z "${MARIADB_DATABASE}" ]; then
    MARIADB_DATABASE=mysql
fi

if [ ! -d /var/lib/mysql/${MARIADB_DATABASE} ]; then
    cd /setup
    ansible-playbook -i inventory dbinit.yml
fi

exec "$@"
