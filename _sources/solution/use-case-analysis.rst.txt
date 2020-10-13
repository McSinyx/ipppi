Use-Case Analysis
=================

Register
--------

Interaction Diagrams
^^^^^^^^^^^^^^^^^^^^

Basic Flow
""""""""""

.. uml::

   skinparam defaultFontColor #a80036
   autonumber "#: //"
   autoactivate on
   hide footbox

   actor Contributor
   boundary "Registration Form" as RF
   control "Registration Controller" as RC
   entity Database

   activate Contributor
   Contributor -> RF : request register()
   RF -> RF : prompt registration field()
   deactivate RF

   Contributor -> RF : register(input)
   RF -> RC : request input verification()
   RC -> Database : verify input()
   Database --> RC : return verification result()

   RC -> Database : add new account()
   deactivate Database
   deactivate RC
   deactivate RF
   deactivate Contributor

View of Participating Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. uml::

   skinparam defaultFontColor #a80036

   class RegistrationForm <<boundary>> {
      // request register()
      // prompt registration field()
      // register(input)
   }

   class RegistrationController <<control>> {
      // request input verification()
      // return verification result()
   }

   class Database <<entity>> {
      // verify input()
      // add new account()
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

   skinparam defaultFontColor #a80036
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

   skinparam defaultFontColor #a80036

   class ProposalForm <<boundary>> {
      // create package update proposal()
      // prompt for package names()
      // prompt for update(package)
   }

   class ProposalController <<control>> {
      // add proposal(updates)
   }

   class MetadataSystem <<entity>> {
      // check for conflicts(updates)
   }

   class NotificationSystem <<boundary>> {
      // notify maintainers for reviews(updates)
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

   skinparam defaultFontColor #a80036
   autonumber "#: //"
   autoactivate on
   hide footbox

   control UpdateControl
   entity MetadataSystem
   boundary DFSConnector
   actor DistributedFileSystem

   activate UpdateControl
   UpdateControl -> MetadataSystem : check against conflict()
   UpdateControl -> DFSConnector : update package()
   DFSConnector -> MetadataSystem : update to Metadata()
   DFSConnector -> DistributedFileSystem : update to DFS()
   deactivate MetadataSystem
   deactivate UpdateControl
   deactivate DistributedFileSystem

View of Participating Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. uml::

   skinparam defaultFontColor #a80036

   class DFSConnector <<boundary>> {
      // update to DFS()
      // update to Metadata()
   }

   class UpdateControl <<control>> {
      // check against conflict()
      // update package()
   }

   class MetadataSystem <<entity>> {
      // store package()
   }

   UpdateControl "1" -- "1" DFSConnector
   UpdateControl "1" -- "1" MetadataSystem
