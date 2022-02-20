Performance tests
=================

Datasets
--------
a. 100 GB - based on real data
b. 2 TB - based od real data

Nodes
-------------------------
1. OP Ceitec
  a. POSIX (gpfs)

2. OP Botanicka
  a. POSIX (gpfs)
  b. S3 (s3.cl2.du.cesnet.cz)
  c. S3 (object-store.cloud.muni.cz)

3. User node - Oneclient (OpenStack)
  a. Direct access
  b. Onedata protocol

4. User node - http/https (OpenStack)
  a. Download all
  
  Researcher download dataset.
  
Tests
-----
OP <---> Client
*************
- Lab OP to user.

Node 1.a <---> 4.

Node 2.b <---> 4.

Node 1.a <---> 3.b

Node 2.b <---> 3.a

OP <---> OP
*************
- Lab OP to user's OP
- Archiving OP to another OP

Node 1.a <---> 2. (GUI)

Node 1.a <---> 2. (API)
