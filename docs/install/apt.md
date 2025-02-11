# Install Percona Server for MongoDB on Debian and Ubuntu

This document describes how to install Percona Server for MongoDB from Percona repositories on DEB-based distributions such as Debian and Ubuntu.

!!! note

    Percona Server for MongoDB should work on other DEB-based distributions,
    but it is tested only on platforms listed on the [Percona Software and Platform Lifecycle](https://www.percona.com/services/policies/percona-software-support-lifecycle#mongodb) page.

## Package contents

| Package                 | Contains                                 |
| ----------------------- | -----------------------------------------|
| `percona-server-mongodb`| The `mongo` shell, import/export tools, other client utilities, server software, default configuration, and `init.d` scripts. |
| `percona-server-mongodb-server`| The mongod` server, default configuration files, and `init.d` scripts|
| `percona-server-mongodb-shell` | The `mongo` shell |
| `percona-server-mongodb-mongos`| The `mongos` sharded cluster query router |
| `percona-server-mongodb-tools` | Mongo tools for high-performance MongoDB fork from Percona|
| `percona-server-mongodb-dbg`   | Debug symbols for the server|

## Procedure

### Configure Percona repository

Percona provides the [`percona-release`](https://www.percona.com/doc/percona-repo-config/index.html) configuration tool that simplifies operating repositories and enables to install and update both Percona Backup for MongoDB packages and required dependencies smoothly.

1. Fetch **percona-release** packages from Percona web:
    
    ```{.bash data-prompt="$"}
    $ wget https://repo.percona.com/apt/percona-release_latest.$(lsb_release -sc)_all.deb
    ```

2. Install the downloaded package with **dpkg**:

    ```{.bash data-prompt="$"}
    $ sudo dpkg -i percona-release_latest.$(lsb_release -sc)_all.deb
    ```

    After you install this package, you have the access to Percona repositories. You
    can check the repository setup in the `/etc/apt/sources.list.d/percona-release.list` file.


3. Enable the repository:

    ```{.bash data-prompt="$"}
    $ sudo percona-release enable psmdb-44 release
    ```

4. Remember to update the local cache:

    ```{.bash data-prompt="$"}
    $ sudo apt update
    ```

### Install Percona Server for MongoDB

=== "Install the latest version"

     Run the following command to install the latest version of Percona Server for MongoDB:

      ```{.bash data-prompt="$"}
      $ sudo apt install percona-server-mongodb
      ```

=== "Install a specific version"

     To install a specific version of Percona Server for MongoDB, do the following:


     1. List available versions:

         ```{.bash data-prompt="$"}
         $ sudo apt-cache madison percona-server-mongodb
         ```

         Sample output:

         ```{.text .no-copy}
         percona-server-mongodb | 4.4.17-17.jammy | http://repo.percona.com/psmdb-44/apt jammy/main amd64 Packages
         percona-server-mongodb | 4.4.16-16.jammy | http://repo.percona.com/psmdb-44/apt jammy/main amd64 Packages
         percona-server-mongodb | 4.4.15-15.jammy | http://repo.percona.com/psmdb-44/apt jammy/main amd64 Packages
         percona-server-mongodb |  4.4.17-17 | http://repo.percona.com/psmdb-44/apt jammy/main Sources
         percona-server-mongodb |  4.4.16-16 | http://repo.percona.com/psmdb-44/apt jammy/main Sources
         percona-server-mongodb |  4.4.15-15 | http://repo.percona.com/psmdb-44/apt jammy/main Sources
         ```

      2. Install a specific version packages. You must specify each package with the version number. For example, to install Percona Server for MongoDB 4.4.15-15, run the following command:

         ```{.bash data-prompt="$"}
         $ sudo apt install percona-server-mongodb=4.4.15-15.jammy percona-server-mongodb-mongos=4.4.15-15.jammy percona-server-mongodb-shell=4.4.15-15.jammy percona-server-mongodb-server=4.4.15-15.jammy percona-server-mongodb-tools=4.4.15-15.jammy
         ```

## Run Percona Server for MongoDB

By default, Percona Server for MongoDB stores data files in `/var/lib/mongodb/`
and configuration parameters in `/etc/mongod.conf`.

**Starting the service**

Percona Server for MongoDB is started automatically after installation unless it encounters errors during the installation process.

You can also manually start it using the following command:

```{.bash data-prompt="$"}
$ sudo systemctl start mongod
```

**Confirming that the service is running**

Check the service status using the following command:

```{.bash data-prompt="$"}
$ sudo systemctl status mongod
```

**Stopping the service**

Stop the service using the following command:

```{.bash data-prompt="$"}
$ sudo systemctl stop mongod
```

**Restarting the service**

Restart the service using the following command:

```{.bash data-prompt="$"}
$ sudo systemctl restart mongod
```


