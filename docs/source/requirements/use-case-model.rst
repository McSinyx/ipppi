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
