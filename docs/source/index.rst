CryoEM data cloudification
==========================

**CryoEM data cloudification** system should provide easy way to make data produced by Cryogenic electron microscopy available to scientist. It supports whole process beginning from store produced data from CryoEM device, its publishing according to required access policy and its archiving in permanent storage. 

Provided services are compatible with FAIR principles. Acquired data can be labelled by a set of metadata by which is possible to search in build-in or external tools (Findable). Each dataset has a unique identifier throughout the whole system. User should only know this identifier to get access the dataset assuming connection to provider which store required data is set and user authorization (Accessible). Data can by directly use in commonly used tools (Interoperable). User is able to get access to the data as long as there is at least one provider on which are the data stored (Reusable). 


.. note::

   This project is under active development.

Contents
--------

.. toctree::
    :maxdepth: 3
    :numbered:
    :caption: User documentation
    :hidden:

   user

.. toctree::
    :maxdepth: 3
    :numbered:
    :caption: Lab documentation
    :hidden:

    overview
    oneprovider
    fs2od
