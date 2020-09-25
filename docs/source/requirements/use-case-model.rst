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

Check against Conflicts
-----------------------

Brief Description
^^^^^^^^^^^^^^^^^
This use case checks for the compatibility between the packages presuming the proposal is accepted.

Actor: Contributor

Flow of Events
^^^^^^^^^^^^^^
This use case starts when distribution packages are submitted by contributors.

Basic Flow
""""""""""
1. Packages being updated(file addition/upgrade/removal).
2. Proposals are reviewed and automatically checked.
3. System provides solutions(modifications) to make sure that new updates do not cause conflicts within the package index.
4. Use case ends.

Actor: Maintainer 

Alternative Flows
"""""""""""""""""
* The proposal is not accepted *
1. System warnings.
2. System detects a functioning set of installs,or at least an install set that satisfies all projects' stated requirements.
2. System provides the latest compatible version of the packages.  

Special Requirements
^^^^^^^^^^^^^^^^^^^^

Pre-Conditions
^^^^^^^^^^^^^^
Packages are downloaded.

Post-Conditions
^^^^^^^^^^^^^^^

Extension Points
^^^^^^^^^^^^^^^^

Review Proposal
---------------

Brief Description
^^^^^^^^^^^^^^^^^
This use case describes how a system decides to approve or dismiss proposals presuming it has them.
Actor: Maintainer
Actor: Contributor

Flow of Events
^^^^^^^^^^^^^^
Use case starts when a proposal is uploaded.

Basic Flow
"""""""""".
1. Contributor/Maintainer uploads proposals.
2. System checks the proposals.
3. System approves/dismisses proposals.

Alternative Flows
"""""""""""""""""

Special Requirements
^^^^^^^^^^^^^^^^^^^^

Pre-Conditions
^^^^^^^^^^^^^^
The contributor/maintainer has internet connection.

Post-Conditions
^^^^^^^^^^^^^^^

Extension Points
^^^^^^^^^^^^^^^^