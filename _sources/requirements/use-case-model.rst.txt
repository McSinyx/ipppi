Use-Case Model
==============

.. uml::

   actor User
   actor Contributor
   actor Maintainer
   actor IPFS
   actor Database

   usecase Download
   usecase Query

   usecase Register
   usecase Login
   usecase "Vote for New Maintainers" as Vote

   usecase "Propose Package Update" as Propose
   usecase "Check against Conflicts" as Check
   usecase "Review Proposal" as Review
   usecase Update

   User --> Download
   Download --> IPFS

   User --> Query
   Query -- Database

   Contributor --> Register
   Register -- Database

   Contributor --> Propose
   Propose ..> Login : <<include>>
   Propose ..> Check : <<include>>
   Check -- Database

   Maintainer --> Review
   Review -- Propose
   Review ..> Login : <<include>>

   Review ..> Update : <<extend>>
   Update ..> Check : <<include>>
   Update -- Database
   Update -- IPFS

   Maintainer --> Vote
   Vote -- Database
   Vote ..> Login : <<include>>
   Login -- Database
