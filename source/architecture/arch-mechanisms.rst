Architectural Mechanisms
========================

Analysis Mechanisms
-------------------

Persistency
   A means to make an element persistent
   (i.e. exist after the application that created it ceases to exist).

Security
   A means to control access to an element.

Analysis-to-Design-to-Implementation Mechanisms Map
---------------------------------------------------

==================  ================  ========================
Analysis Mechanism  Design Mechanism  Implementation Mechanism
==================  ================  ========================
Persistency         RDBMS             PostgreSQL
Distribution        XML-RPC           Python package xmlrpc
Security                              HTTPS
==================  ================  ========================

Implementation Mechanisms
-------------------------
