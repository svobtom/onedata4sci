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


Community/national storage site
-------------------------------


Compute site
------------
