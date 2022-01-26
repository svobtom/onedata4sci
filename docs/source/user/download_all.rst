Download a dataset
==================
There is posibility to download whole dataset at once. Following steps can be used also applied on a directory (to download it recursively) or on a single file. 

At first you should have a unique identifier of space, directory or file.

.. warning::

   Only files which were shared can be downloaded by this script. 

Get file identifier
-------------------
File ID can by found by left click on the name of space or by right click on the name of directory/file in menu item ``Information``.

.. image:: ../images/22_file_information.png
   :width: 500
   :align: center
   :alt: Information about file or directory

File ID is long string as you se bellow.

.. image:: ../images/21_file_id.png
   :width: 500
   :align: center
   :alt: File ID

Usage of the script
-------------------
Basic usage
***********
The script can be downloaded from URL https://raw.githubusercontent.com/CERIT-SC/onedata-downloader/master/download.py e.g. by this command

.. code:: bash

   curl -s --output download.py https://raw.githubusercontent.com/CERIT-SC/onedata-downloader/master/download.py

With appropriate identifier, you can download the data. Replace FILE_ID with the identifier.

.. code:: bash

   ./download.py FILE_ID

Script download whole file structure to recent directory. 

Direct usage
************
The script can be used directly from its repository

.. code:: bash

   curl -s https://raw.githubusercontent.com/CERIT-SC/onedata-downloader/master/download.py | python3 - FILE_ID
