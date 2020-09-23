Use-Case Model
==============

.. uml::

   actor User
   actor Contributor
   actor Maintainer
   actor IPFS

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

   Maintainer --> Review
   Review -- Propose
   Review ..> Login : <<include>>

   Update ..> Review : <<extend>>
   Update ..> Check : <<include>>
   Update --> IPFS

   Maintainer --> Vote
   Vote ..> Login : <<include>>

   Maintainer --|> Contributor
   Contributor --> Register

   Contributor --> Propose
   Propose ..> Login : <<include>>
   Propose ..> Check : <<include>>
