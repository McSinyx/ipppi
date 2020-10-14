Distribution
============

Deployment Model
----------------

.. uml::

   skinparam defaultFontColor #a80036

   package "Client Machine" as Client <<Node>> {
   }

   package "IPPPI Server" as Server <<Node>> {
   }

   package "Database" as DB <<Node>> {
   }

   package IPFS <<Node>> {
   }

   Server -- Client: <<Internet>>
   Server -- DB: <<LAN>>
   Server -- IPFS: <<LAN>>
