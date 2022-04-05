System components
=================

System is based on existing solution for distributed storing and sharing data called ``Onedata``. 

Onedata
-------
Onedata is distributed data management solution which allow users to store their data on multiple types of storages, access them by several ways, collaborate with other users, share them publicly and perform computation on the stored data. 

Space
*****
In Onedata all stored data is organized to spaces. It can be seen like virtual volume or directory. It contains files in a directory hierarchy. In addition, any metadata can be added to whole space, directories or even to each file. A space can be hosted by one or more providers (see below) and it can be migrated among them. It is basic unit of the access control system. 

Onezone
*******
Onezone is catalogue which holds information about users, groups, access tokens, spaces, permissions (ACL), etc. Whole Onedata environment can be divided into zones. Each zone is managed by an Onezone service.

We primary use Onezone `EGI Datahub <https://datahub.egi.eu>`_. This is a well-known instance of Onezone which is managed by authors of Onedata. As it supports login by `EGI Check-In <https://aai.egi.eu>`_, users can choose between many identity providers during login (including institutional or social identities). Although instructions in this documentation can be used to work with any Onezone. 

Oneprovider
***********
Oneprovider is service that stores the data itself. It is registered within a Onezone and support spaces by various storage resources. It is expected that this service is deployed near physical storage to have quick access to it. This is the part of system which store data and from users download (or also upload) data. It can be run on a single node or on multiple nodes in a cluster. 

Onedata Storage
***************
Named storage resource exposed via Oneprovider to support Onedata spaces. There are several possibilities where physical data can be stored. In this documentation we use following two:

- POSIX file system,
- S3 accessible object storage.

Oneclient
*********
Users can get their data simply with no setup through web browser. Users, who would like to work with data intensively, ca use client-side software ``Oneclient``. This is tool which allows access to data stored in Onedata throw command line interface (CLI). Required space are mounted to your local machine as common directory and you can work with in a very similar way. 

.. note::

    Oneclient can access data through Onedata or directly through built-in support for several common data transfer protocol (NFS, S3, Ceph, WebDAV, ...). Usage of direct access is faster and is recommended for transfers of data. 


fs2od
*****
Interactive software which communicates with Onedata system API and mediates following tasks:
- create space, set up ACL, set up support by CF Oneprovider,
- replicate spaces to another Oneprovider,
- monitor dates (publishing date, archive date, remove date),
- send e-mails when specified event occur.
