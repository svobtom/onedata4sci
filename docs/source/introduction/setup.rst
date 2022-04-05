Distributed setup
=================

The following diagram illustrates how the compontents of are distributed over the sites forming the whole ecosystem
and how they interact with one another.

.. image:: schema.pdf


Experimental facility
---------------------

Besides the experimental equipment (microscope etc.) the site must provide storage for the acquired data.
Typically, it is organized as a standard POSIX filesystem, which is mounted on the computer(s) where the data 
are actually acquired. 

Datasets corresponding to individual experiments are stored in separate folders.

On top of the same filesystem, ``Oneprovider`` and ``fs2od`` must be run.

Once the experimental data should be published (either the experiment is finished or it is desirable to let 
the user "peak" into the data), the facility operator creates a metadata file in the same folder.
Typically, software specific to experimental data type is used to do so.

Existence of the metadata file triggers the activity of fs2od, which creates a corresponding space in Onedata, generates
its access link and invite token, and stores this information back to the metadata file.
This is an example how such metadata file can look afterwards (truncated):

.. literalinclude:: SPA.yml

Finaly, fs2od instructs Oneprovider to scan the folder, which populates the corresponding space effectively.

The facility operator is expected to deliver the access link and the invite token to the user.

The data storage size at the experimental facility is expected to be of a limited size, and it can guarantee the users
to keep the acquired data for a fairly short period (weeks to months).
The users are required to request replication of the data to a long term storage (community or national);
this is done by technical means of Onedata again.

Community/national storage site
-------------------------------

Typically, experimental facilities are not equipped to store huge volumes of user data for long term.
Therefore the users are required to negotiate data storage capacity elsewhere.
Possible candidates are storage sites operated by institutiona, national or international user community,
national e-infrastructure etc.

Besides the physical storage, the sites are required to run ``Oneprovider`` in stadard configuration (see `Onedata documentation <https://onedata.org/#/home/documentation/stable/index.html>`_).
The provider is required to join the `EGI Datahub <https://datahub.egi.eu>`_ Onezone instance.

The provider is strongly encouraged to use ``S3 storage backend``, which we support in turn in the compute client configuration (see bellow).
Otherwise the provider-client communication falls back to Onedata internal "poor man" protocol with serious to prohibitive impact on
performance with non-toy datasets. 


Compute site
------------

Extensive computational processing of the experimental data is expected to be done at a computing (cloud) site.
In order to achieve efficient access to the data, the site must install ``Oneclient`` including S3 libraries.

Currently, we support `Scipion <https://scipion.i2pc.es>`_ CryoEM software suite, configured in prepared Docker container
images ready to be used in Kubernetes. 
See our `Github project <https://github.com/CERIT-SC/scipion-docker/tree/k8s-test`_ for details and documentation.

This Scipion deployment is given a Oneprovider endpoint, the user's Onedata ``token``.
It uses Oneclient over S3 to mount the dataset (Onedata space), and it copies it to a local storage typically (for performance reasons).
Then the data are processed, and results can be uploaded to Onedata again for further sharing.



