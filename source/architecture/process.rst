Process View
============

Processes
---------

The processes for IPPPI will be the following:

- One process for the forms, which runs on client-side.
- One process per business service controller:

  - RegistrationControllerProcess
  - LoginControllerProcess
  - ProposalControllerProcess
  - UpdateControllerProcess

  There is one process per controller because these activities
  will need to run concurrently with each other.
- One process per external system:

  - MetadataDBAccess
  - ProposalDBAccess
  - DistributedFileSystemConnector

  There is one process per external system.  These processes manage access to
  those systems.  Such access may be slow, so this allows other functionality
  to continue while the external system processes wait on the external system.
  These processes also synchronize access to the external systems
  from the other system processes.

In general, the above processes and threads were defined
to support faster response times and take advantage of multiple processors.

Design Element to Process Mapping
---------------------------------
