---
Title: Installation
aliases: null
alwaysopen: false
categories:
- docs
- integrate
- rs
- rdi
description: Learn how to install RDI ingest
group: di
hideListLinks: false
linkTitle: Installation
summary: Redis Data Integration keeps Redis in sync with the primary database in near
  real time.
type: integration
weight: 2
---

This guide explains how to install RDI and integrate it with your source database.

## Install RDI on VMs

You would normally install RDI on two VMs for high availability (HA) but you can also install
one just one VM if you don't need this. For example, you might not need HA during
development and testing.

The supported OS versions for RDI are:

- RHEL 8 & 9
- Ubuntu 18.04 & 20.04

You must run the RDI installer as a privileged user because it installs
[containerd](https://containerd.io/) and registers services. However, you don't
need any special privileges to run RDI processes for normal operation.

### Hardware sizing

RDI is mainly CPU and network bound. 
Each of the RDI VMs should have:

- CPU: A minimum of 4 CPU cores. You should consider adding
  2-6 extra cores on top of this if your dataset is big and you want to ingest the
  baseline snapshot as fast as possible.
- RAM: 2GB 
- Disk: 25GB of disk (this includes the OS footprint)
- 10GB or more network interface
  


### Installation steps

Follow the steps below for each of your VMs:

1.  Download the RDI installer from the [Redis download center](https://redis.io/downloads)
    and extract it to your preferred installation folder.

1. Go to the installation folder:

    ```bash
    cd rdi_install/$RDI_VERSION
    ```

1. Run the installer as a privileged user:

    ```bash
    sudo ./install.sh
    ```

The installer will ask you for Redis Enterprise cluster admin credentials. You should supply
these if you want the installer to create the RDI database for you.
 
{{<note>}}The installer does not create the RDI Redis database with
[TLS](https://en.wikipedia.org/wiki/Transport_Layer_Security)/
[mTLS](https://en.wikipedia.org/wiki/Mutual_authentication#mTLS).
If you want to use TLS or other advanced options then you must create the Redis database
yourself using the Redis Enterprise console.{{</note>}}

If you don’t want the installation to create the RDI database for you:

- Use the Redis console to create a database with 250MB RAM with 1 primary and 1 replica.
- If you are deploying RDI for a production environment then secure this database with a password
  and TLS.
- Provide the installation with the required RDI database details.

Once the installation is finished, RDI is ready for use.

{{<note>}}RDI gives you instructions to help you create secrets and create your pipeline.{{</note>}}

## Prepare your source database

You must also configure your source database to use the Debezium connector for CDC. See the
[Prepare source databases]({{< relref "/integrate/redis-data-integration/ingest/data-pipelines/prepare-dbs" >}})
section to learn how to do this.

## Uninstall RDI

If you want to remove your RDI installation, go to the installation folder and run
the uninstall script as a privileged user:

```bash
sudo ./uninstall.sh
```

The script will check you are sure before you proceed:

```
This will uninstall RDI and its dependencies, are you sure? [y, N]
```

If you type anything other than "y" here, the script will abort without making any changes
to RDI or your source database.
