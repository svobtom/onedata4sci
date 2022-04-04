Use cases
=========
Design of cryoem-fs2od was driven by serveral principal usecases the ecosystem is expected to address

Simple access
--------------------------
This is the most simple, staightforward scenario (from the dataflow point of view). 

#. The user defines the requested experiment, typically delivering a physical sample to the facility.
#. The facility performs the experiment, and stores the acquired dataset, together with the corresponding metadata.
#. The user is given ``access link`` (URL), via email typically, and he/she downlods the data for further processing.
#. If the dataset contains large number of files, they can be also downloaded in a batch.

Sharing data with other users
-----------------------------
In this scenario, the user who requests acquisition of the data, wants to collaborate with other users by granting access on the acquired 
data to them.

#. The experiment is requested and performed as in the previous use case.
#. Besides the access link, the user is also provided with an ``invite token`` (specific purpose Onedata credential).
#. The user distributes the invite token to his/her collaborators.
#. The collaborators provide the invite token to Onedata web interface, which grants them access to the dataset in turn, they can start using them in exactly the same way as the primary user.


Use in computing center
-------------------------------

The integration goes one step further. The user (either the primary one, who requested the experiment, or one of the collaborators)
perform demanding computation on the data, which must be executed in a computing centre (with a cloud computing provider, typically).

#. First, the users negotiate storage support at Onedata provider site which supports access protocols suitable for this scenario (S3, typically). Onedata is instructed to replicate the dataset to this site.
#. The user, using Onedata web interaface, generates a ``token`` to access the dataset with Onedata client.
#. The token is provided to ``Oneclient`` software running at the computing site, granting it the access to the dataset.
#. Depending on requirements of the computation, the dataset is either mirrored to the local storage at the computing site, or accessed by Oneclient on the fly.
#. The user either retrieves the results from the computing site directly, or they are also stored at Ondata (and can be shared in the same way as the experimental data).
