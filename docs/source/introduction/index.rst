Introduction
============

In many scientific disciplines the expensive equipment is shared nowadays.
The ``users`` -- scientists request specific experiments from ``facilities``, which perform the experiments 
on their behalf.
The outcome of such experiment is a ``dataset``, which can be quite huge in many cases.
The users process those datasets, draw scientific conclusions by their interpretation, and publish the resutls.
Recently, more emphasis is given on availability of the data so that any scientific results can be verified independently.
The scenario applies to growing nubmer of both users and facilities, amounts of generated data are increasing, 
and their availability should be ensured in long term.

**fs2od-cryoem** is an assembly of best practices, third-party software and services (`Onedata <http://onedata.org>`_ in particular),
and in-house "glue" software to handle the outlined scenario, with primary application domain of cryoelectron microscopy.
Its purpose can be summarized as follows:

* manage storage of experimental data over large-scale international e-infrastructure, including several tiers of physical data storage (the experimental facilities where data are acquired, national or scientific domain data storage services, computing facilities etc.)
* make the data easily available to the users -- scientists
* allow controlled data sharing among multiple users in collaborative projects
* provide efficient access to the data to be processed at computing facilities
* implement varying policies of handling the data (e.g. expriration at the acquisition facility, archiving in multiple copies, data publication after embargo period etc.)

The following parts of this section describe principal driving usecase, define the essential roles, and provide technical description
of the overal solution.
The furher sections are dedicated to details of installation and usage, and they are arranged according to the defined roles (users and administrators).
