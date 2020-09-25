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

Propose Package Update
----------------------

Brief Description
^^^^^^^^^^^^^^^^^

The use case allows the Contributor to creat a proposal for update
one or many distribution packages.  This includes adding, removing
and upgrading/downgrading them as appropriate by the situation.

Flow of Events
^^^^^^^^^^^^^^

Basic Flow
""""""""""

This use case starts when the Contributor wishes to create
a *Package Update Proposal*.

#. The system requests that the Contributor specify
   the name of packages to be updated.
#. Once the Contributor selects the package names, the system requests
   that the Contributor provide the :term:`release <Release>` to be pinned.
   The Contributor may leave the field blank to remove the package
   from the index.
#. The system notify the Maintainer to review the proposal,
   while at the same time automatically check for conflicts
   within the new set of distributions.
#. If the Maintainer request changes or the automated check fails,
   the previous step is repeated.

Alternative Flows
"""""""""""""""""

Requested Information Unavailable
   If, in the Basic Flow, no package name is provided, the system will
   display an error message.  The Contributor can choose to either
   cancel the operation or provide at least one package name.

Special Requirements
^^^^^^^^^^^^^^^^^^^^

None.

Pre-Conditions
^^^^^^^^^^^^^^

The Contributor must be logged onto the system before this use case begin.

Post-Conditions
^^^^^^^^^^^^^^^

Success: The new proposal is either dismissed or approved.

Failure: The system state is unchanged.

Extension Points
^^^^^^^^^^^^^^^^

None.

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
