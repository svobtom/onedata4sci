CryoEM data cloudification
==========================

**CryoEM data cloudification** system should provide easy way to make data produced by Cryogenic electron microscopy available to scientist. It supports whole process beginning from store produced data from CryoEM device, its publishing according to required access policy and its archiving in permanent storage. 


.. seealso::

   Here will be a well organized scheme with overview of an application functionality.


Provided services are compatible with FAIR principles. Acquired data can be labelled by a set of metadata by which is possible to search in build-in or external tools (Findable). Each dataset has a unique identifier throughout the whole system. User should only know this identifier to get access the dataset assuming connection to provider which store required data is set and user authorization (Accessible). Data can by directly use in commonly used tools (Interoperable). User is able to get access to the data as long as there is at least one provider on which are the data stored (Reusable). 

.. note::

   This project is under active development.

Overview
--------

Introduction of system architecture.

.. toctree::
   :maxdepth: 2
   :hidden:
   :numbered:
   :caption: Overview

   introduction/index
   introduction/usecases
   introduction/roles
   introduction/components
   introduction/setup

User access to the data
-----------------------

Documentation for user who would like to access the data.

.. toctree::
   :maxdepth: 2
   :hidden:
   :numbered:
   :caption: User access to the data

   user/link
   user/download_all
   user/checkin
   user/mount
   user/replica
   user/scipion

Setup at facility
-----------------

Documentation for laboratory (core facility) staff.

.. toctree::
   :maxdepth: 2
   :hidden:
   :numbered:
   :caption: Setup at facility

   labs/oneprovider
   labs/fs2od
   labs/archiving_expiring
   labs/performance
   labs/metadata
