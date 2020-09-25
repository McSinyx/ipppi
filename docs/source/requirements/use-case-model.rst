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
This use case is used to make sure that the representation of a client does not involve any concurrent conflict of interest.

Flow of Events
^^^^^^^^^^^^^^
This use case starts due to:
* Massive quantity of requirements can lead to conflicts
between them.
* Changes in requirements during system development
phases. 
* Complex system domain.

Basic Flow
""""""""""
1. Conflicts between stakeholders’ requirements.
2. System checks against conflicts using one of the three techniques: manual, automatic and general framework.
3. System gives solutions.
4. Use case ends.

Alternative Flows
"""""""""""""""""
No conflicts -> Use case ends
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
This use case describes how a system propose review comments and capture them.
Actor: Registered/Unregistered user
Actor: Distributed file system
Actor: Contributor

Flow of Events
^^^^^^^^^^^^^^
Use case starts when an user downloads the software and starts using it.

Basic Flow
"""""""""".
1. Software installed.
2. Software used.
3. Use case propose review comments.
4. Use case captures reviews.
5. Use case ends.

Alternative Flows
"""""""""""""""""
- Alt 1: 
1. User doesn't give comment.
2. System suggests user's explanation.
3. * If there is no explanations: Use case ends.
4. * If there is -> System captures -> Use case ends.

- Alt 2:
1. User doesn't install the software.
2. System suggests user's explanation (review).
3. * If there is no explanations: Use case ends.
4. * If there is -> System captures -> Use case ends.

Special Requirements
^^^^^^^^^^^^^^^^^^^^

Pre-Conditions
^^^^^^^^^^^^^^

Post-Conditions
^^^^^^^^^^^^^^^

Extension Points
^^^^^^^^^^^^^^^^