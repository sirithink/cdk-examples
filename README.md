# Cloudera Development Kit Examples

The CDK Examples project provides examples of how to use the CDK.

Each example is a standalone Maven module with associated documentation.

## Basic Examples

* `dataset` shows how to create datasets and perform streaming writes and reads over them.
* `dataset-staging` shows how to use two datasets to manage Parquet-formatted data
* `logging` is an example of logging events from a command-line programs to Hadoop via Flume, using log4j as the logging API.
* `logging-webapp` is like `logging`, but the logging source is a webapp.

## Advanced Examples

* `demo` is a full end-to-end example of a webapp that logs events using Flume and performs session analysis using Crunch and Hive.

## Getting Started

The easiest way to run the examples is on the
[Cloudera QuickStart VM](https://ccp.cloudera.com/display/SUPPORT/Cloudera+QuickStart+VM),
which has all the necessary Hadoop services pre-installed, configured, and
running locally. See the notes below for any initial setup steps you should take.

The current examples run on version 4.3.0 of the QuickStart VM.

Checkout the latest [branch](https://github.com/cloudera/cdk-examples/branches) of this repository in the VM:

```bash
git clone git://github.com/cloudera/cdk-examples.git
cd cdk-examples
git checkout <latest-branch>
```

(Alternatively, if you want to use the master branch, then build the [CDK](https://github.com/cloudera/cdk) locally first.)

Then choose the example you want to try and refer to the README in the relevant subdirectory.

### Setting up the QuickStart VM

There are two ways to run the examples with the QuickStart VM:

1. Logged in to the VM guest (username and password are both `cloudera`).
2. From your host computer.

The advantage of the first approach is that you don't need to install anything extra on
your host computer, such as Java or Maven, so there are no extra set up steps.

The second approach is preferable when you want to use tools from your own development
environment (browser, IDE, command line). However, there are a few extra steps you
need to take to configure the QuickStart VM, listed below.

* __Enable port forwarding__ For VirtualBox, open the Settings dialog for the VM,
select the Network tab, and click the Port Forwarding button. Map the following ports -
in each case the host port and the guest port should be the same.
    * 7180 (Cloudera Manager web UI)
    * 8020, 50010, 50020, 50070, 50075 (HDFS NameNode and DataNode)
    * 8021 (MapReduce JobTracker)
    * 8888 (Hue web UI)
    * 9083 (Hive/HCatalog metastore)
    * 41415 (Flume agent)
    * 11000 (Oozie server)
    * 21050 (Impala JDBC port)
* __Bind daemons to the wildcard address__ Daemons that are accessed from the host need
to listen on all network interfaces. In [Cloudera Manager]
(http://localhost:7180/cmf/services/status) for each of the services listed below,
select the service, click "View and Edit" under the Configuration tab then
search for "wildcard", check the box, then save changes.
    * HDFS NameNode and DataNode
    * Hue server
    * MapReduce JobTracker
* __Add a host entry for localhost.localdomain__ If you host computer does not have a
mapping for `localhost.localdomain`, then add a line like the following to `/etc/hosts`
```
127.0.0.1       localhost       localhost.localdomain
```
* __Sync the system clock__ For some of the examples it's important that the host and
guest times are in sync. To synchronize the guest, login and type
`sudo ntpdate pool.ntp.org`.
* __Restart the cluster__ Restart the whole cluster in Cloudera Manager.
