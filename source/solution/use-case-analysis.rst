Use-Case Analysis
=================

Register
----------------------

Interaction Diagrams
^^^^^^^^^^^^^^^^^^^^

Basic Flow
""""""""""

.. uml::
   
   autonumber "#: //"
   hide footbox
   
   actor Contributor
   boundary "Registration Form" as RF
   control "Registration Controller" as RC
   entity Database

   activate Contributor
   Contributor -> RF : request register

   activate RF
   RF -> RF : prompt registration field
   activate RF
   Contributor -> RF : register(input)

   RF -> RC : request input verification
   activate RC
   RC -> Database : verify input
   activate Database
   Database --> RC : return verification result
   RC -> Database : add new account 
   deactivate Database
   deactivate RC

   deactivate RF
   deactivate RF
   deactivate Contributor

View of Participating Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. uml::

   class RegistrationForm <<boundary>> {
      request register()
      prompt registration field()
      register(input)
   }

   class RegistrationController <<control>> {
      request input verification()      
      return verification result()
   }

   class Database <<entity>> {
      verify input()
      add new account()
   }

   RegistrationForm "0..*" -- "1" RegistrationController
   RegistrationController "1" -- "1" Database

Propose Package Update
----------------------

Interaction Diagrams
^^^^^^^^^^^^^^^^^^^^

Basic Flow
""""""""""

.. uml::

   autonumber "#: //"
   autoactivate on
   hide footbox

   actor Contributor
   boundary ProposalForm
   control ProposalController
   entity MetadataSystem
   boundary NotificationSystem

   activate Contributor
   Contributor -> ProposalForm : create package update proposal()
   ProposalForm -> ProposalForm : prompt for package names()
   ProposalForm -> ProposalForm : prompt for update(package)
   ProposalForm -> ProposalController : add proposal(updates)
   ProposalController -> MetadataSystem : check for conflicts(updates)
   ProposalController -> NotificationSystem : notify maintainers for reviews(updates)
   deactivate NotificationSystem
   deactivate MetadataSystem
   deactivate ProposalController
   deactivate ProposalForm
   deactivate Contributor

View of Participating Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. uml::

   class ProposalForm <<boundary>> {
      create package update proposal()
      prompt for package names()
      prompt for update(package)
   }

   class ProposalController <<control>> {
      add proposal(updates)
   }

   class MetadataSystem <<entity>> {
      check for conflicts(updates)
   }

   class NotificationSystem <<boundary>> {
      notify maintainers for reviews(updates)
   }

   ProposalForm "0..*" -- "1" ProposalController
   ProposalController "1" -- "1" MetadataSystem
   ProposalController "1" -- "1" NotificationSystem

Update
------

Interaction Diagrams
^^^^^^^^^^^^^^^^^^^^

Basic Flow
""""""""""

.. uml::

   autonumber "#: //"
   autoactivate on
   hide footbox

   control UpdateControl    
   entity MegadataSystem 
   boundary DFSConnector
   actor DistributedFileSystem
   
   activate UpdateControl
   UpdateControl -> MegadataSystem : Check against conflict
   UpdateControl -> DFSConnector : Update package
   DFSConnector -> MegadataSystem : Update to Megadata 
   DFSConnector -> DistributedFileSystem :Update to DFS
   deactivate MegadataSystem
   deactivate UpdateControl
   deactivate DistributedFileSystem

View of Participating Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. uml::

   class DFSConnector <<boundary>> {
      //UpdatetoDFS()
      //UpdatetoMegadata()
   }

   class UpdateControl <<control>> {
      //CheckConflict()
      //UpdatePackage()
   }

   class MegadataSystem <<entity>> {
      //Storepackage()
   }

   UpdateControl "1" -- "1" DFSConnector
   UpdateControl "1" -- "1" MegadataSystem