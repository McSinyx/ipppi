Use-Case Model
==============

.. uml::

   actor User
   actor Contributor
   actor Maintainer
   actor "Distributed File System" as IPFS

   usecase Download
   usecase Query

   usecase Register
   usecase Login
   usecase "Vote for New Maintainers" as Vote

   usecase "Propose Package Update" as Propose
   usecase "Check against Conflicts" as Check
   usecase "Review Proposal" as Review
   usecase Update

   User --> Query
   User --> Download
   Download --> IPFS

   Maintainer --> Vote
   Vote ..> Login : <<include>>

   Maintainer --|> Contributor
   Contributor --> Register

   Contributor --> Propose
   Propose ..> Login : <<include>>
   Propose ..> Check : <<include>>

   Maintainer --> Review
   Review ..> Login : <<include>>

   Update ..> Review : <<extend>>
   Update ..> Check : <<include>>
   Update --> IPFS

Download
--------

Brief Description
^^^^^^^^^^^^^^^^^

Flow of Events
^^^^^^^^^^^^^^

Basic Flow
""""""""""

Alternative Flows
"""""""""""""""""

Special Requirements
^^^^^^^^^^^^^^^^^^^^

Pre-Conditions
^^^^^^^^^^^^^^

Post-Conditions
^^^^^^^^^^^^^^^

Extension Points
^^^^^^^^^^^^^^^^

Query
-----

Brief Description
^^^^^^^^^^^^^^^^^

Flow of Events
^^^^^^^^^^^^^^

Basic Flow
""""""""""

Alternative Flows
"""""""""""""""""

Special Requirements
^^^^^^^^^^^^^^^^^^^^

Pre-Conditions
^^^^^^^^^^^^^^

Post-Conditions
^^^^^^^^^^^^^^^

Extension Points
^^^^^^^^^^^^^^^^

Register
--------

Brief Description
^^^^^^^^^^^^^^^^^

Flow of Events
^^^^^^^^^^^^^^

Basic Flow
""""""""""

Alternative Flows
"""""""""""""""""

Special Requirements
^^^^^^^^^^^^^^^^^^^^

Pre-Conditions
^^^^^^^^^^^^^^

Post-Conditions
^^^^^^^^^^^^^^^

Extension Points
^^^^^^^^^^^^^^^^

Login
-----

Brief Description
^^^^^^^^^^^^^^^^^

Flow of Events
^^^^^^^^^^^^^^

Basic Flow
""""""""""

Alternative Flows
"""""""""""""""""

Special Requirements
^^^^^^^^^^^^^^^^^^^^

Pre-Conditions
^^^^^^^^^^^^^^

Post-Conditions
^^^^^^^^^^^^^^^

Extension Points
^^^^^^^^^^^^^^^^

Vote for New Maintainers
------------------------

Brief Description
^^^^^^^^^^^^^^^^^
The maintainers of the database will vote for new maintainer when they need, replace, reduce maintainers

Flow of Events
^^^^^^^^^^^^^^
Maintainers need more/less maintainer for the job, they will vote for new maintainer 

Basic Flow
""""""""""
Maintainers need more/less maintainer for the job -> agree for human changes -> new maintainer login special account

Alternative Flows
"""""""""""""""""
alt 1.
Maintainers need more/less maintainer for the job -> disagree for the new maintainers -> vote for another candidates

Special Requirements
^^^^^^^^^^^^^^^^^^^^

Pre-Conditions
^^^^^^^^^^^^^^

Post-Conditions
^^^^^^^^^^^^^^^

Extension Points
^^^^^^^^^^^^^^^^

Propose Package Update
----------------------

Brief Description
^^^^^^^^^^^^^^^^^

Flow of Events
^^^^^^^^^^^^^^

Basic Flow
""""""""""

Alternative Flows
"""""""""""""""""

Special Requirements
^^^^^^^^^^^^^^^^^^^^

Pre-Conditions
^^^^^^^^^^^^^^

Post-Conditions
^^^^^^^^^^^^^^^

Extension Points
^^^^^^^^^^^^^^^^

Check against Conflicts
-----------------------

Brief Description
^^^^^^^^^^^^^^^^^

Flow of Events
^^^^^^^^^^^^^^

Basic Flow
""""""""""

Alternative Flows
"""""""""""""""""

Special Requirements
^^^^^^^^^^^^^^^^^^^^

Pre-Conditions
^^^^^^^^^^^^^^

Post-Conditions
^^^^^^^^^^^^^^^

Extension Points
^^^^^^^^^^^^^^^^

Review Proposal
---------------

Brief Description
^^^^^^^^^^^^^^^^^

Flow of Events
^^^^^^^^^^^^^^

Basic Flow
""""""""""

Alternative Flows
"""""""""""""""""

Special Requirements
^^^^^^^^^^^^^^^^^^^^

Pre-Conditions
^^^^^^^^^^^^^^

Post-Conditions
^^^^^^^^^^^^^^^

Extension Points
^^^^^^^^^^^^^^^^

Update
------

Brief Description
^^^^^^^^^^^^^^^^^
This use case describes how an update operate.
Actor: Distributed File System
Actor: Maintainer
Actor: Contributor
Flow of Events
^^^^^^^^^^^^^^
Use case start when a maintainer want to update package onto IFPS
The maintainer review the packages proposed by the contributor
The IFPS and maintainer will check for any conflict exist
Basic Flow
""""""""""
the package will be checked against conflicts the contributor.
next, the package will wait to be reviewed by the maintainer.
after that, the maintainer will decide to update the package to IFPS by schedule data, size, length, date of the update for the maintenance.
after maintenance the maintainer will check for any conflicts, bugs maintain.

Alternative Flows
"""""""""""""""""
Alt 1.
The package will be checked against conflicts the contributor -> found conflicts -> the package is fixed by the contributor

alt 2.
The package will wait to be reviewed by the maintainer -> the maintainer reject the package ->the package will not be updated -> the package is fixed by the contributor

alt 3.
After maintenance, maintain any bug and conflicts -> the maintainer continue the maintenance -> the package will be fixed by the contributor and maintainer

Special Requirements
^^^^^^^^^^^^^^^^^^^^

Pre-Conditions
^^^^^^^^^^^^^^

Post-Conditions
^^^^^^^^^^^^^^^

Extension Points
^^^^^^^^^^^^^^^^
