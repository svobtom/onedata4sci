fs2od utility
=============
Software fs2od (filesystem to Onedata) is separate part of the system packed into a Docker container, which simplified interaction with Onedata system. It can take list of directories which should by cloudified and periodically check them and import them into Onedata system. Each subdirectory of specified directory represents separate dataset. For each such dataset will be created Onedata space.   

Requirements
------------
It can be run on the same node as Oneprovider. It must have access to the directories which should be loaded to Onedata.

Downloading of software
-----------------------
For running the software, you need following to two files:

- docker-compose.yaml – Docker compose file containing recipe to downloading and run container with fs2od application. Download at https://raw.githubusercontent.com/CERIT-SC/fs2od/master/docker-compose.yaml
- config.yaml – configuration file of application. Download at https://raw.githubusercontent.com/CERIT-SC/fs2od/master/app/config.yaml

You can run software only with two files mentioned above. For some advance usage you can also download source code of the software from its git repository:

.. code:: bash

   git clone https://github.com/CERIT-SC/fs2od.git  .

Creating tokens
---------------
You must have tokens to be able to communicate with Onezone and your Oneprovider. 

Creating tokens:

.. centered::
   TOKENS > Create new token (plus sign on the top in the left menu)

You will need following three tokens:

1.	Oneprovider REST access token
2.	Oneprovider Onepanel REST access token
3.	Onezone REST access token

You can generate Oneprovider and Oneprovider Onepanel token in once. In following text, we will use such "two in one" token. To get ``Oneprovider REST access token`` and ``Onepanel REST access token`` click on icon ``ONEPROVIDER REST/CDMI ACCESS``. Select a name to your token or let the suggested one. Let the type ``Access``. To service field you have to be set to two values which are shown in the picture. You can choose specific instance of your Oneprovider or you can generate token for all of your Oneproviders. Interface leave set to REST. 

.. image:: ../images/08_OZ_clusters.png
   :width: 500
   :align: center
   :alt: Create Oneprovider and Oneprovider Onepanel Tokens

To get “Onezone REST access token” click on icon “ONEZONE REST ACCESS”. Select a name to your token or let the suggested one. Let the type “Access”. Service have to be set to your Onezone (EGI DATAHUB). Interface leave set to REST.

.. image:: ../images/08_OZ_clusters.png
   :width: 500
   :align: center
   :alt: Create Onezone token

For all tokens you can also set many other caveats – restrictions to token usage. For security reasons is in production recommended to restrict usage of tokens at least by IP access list to make token usable only from given set of IP address. If you limit usage by IP address you must include machine, where fs2od running to IP whitelist. 

.. image:: ../images/08_OZ_clusters.png
   :width: 500
   :align: center
   :alt: All caveats (restrictions) which token management support

Application configuration
-------------------------
Most of application configuration can be set in file ``config.yaml``. Attributes in config file are accompanied with self-standing documentation. 
Most important settings in config file:

-	``watchedDirectories`` - Set directories which should be monitored.   
- REST API hostnames and tokens to Onedata services:

EGI DATAHUB Onezone hostname is ``https://datahub.egi.eu``. Tokens you acquired in previous step, paste them to configuration file. Oneprovider and Oneprovider Onepanel hostnames are in our installation (one-node Oneprovider cluster) same.

Get hostname of Oneprovider:

.. centered::
   CLUSTERS > Select your cluster > Overview > Section INFO > Domain (copy to clipboard)

Running the application
-----------------------
Run the application  by docker-compose command:

.. code:: bash

   docker-compose up -d

Especially when you ran application in test mode, you can invoke application methods manually, e.g. by command

.. code:: bash

   docker-compose exec fs2od ./run-dirs-check.py

you can manually invoke the process of checking the directories. With command

.. code:: bash

   docker-compose exec fs2od ./test.py --remove_instances

you can remove all instances (spaces, storages, groups, …) which you have created during testing. 

Moving to production
--------------------
After you test application you can switch it to production. You do it by changing values of these variables:

- in ``config.yaml`` set up variable ``testMode`` to ``False``,
- in ``docker-compose.yaml`` set up variable ``RUN_PERIODICALLY`` to ``"true"``
