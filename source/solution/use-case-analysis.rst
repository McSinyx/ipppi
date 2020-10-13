Use-Case Analysis
=================

Register
--------

Interaction Diagrams
^^^^^^^^^^^^^^^^^^^^

Basic Flow
""""""""""

.. uml::
   
   autonumber "#: //"
   autoactivate on
   hide footbox
   
   actor Contributor
   boundary "Registration Form" as RF
   control "Registration Controller" as RC
   entity Database

   activate Contributor
   Contributor -> RF : request register
   RF -> RF : prompt registration field
   deactivate RF

   Contributor -> RF : register(input)
   RF -> RC : request input verification
   RC -> Database : verify input
   Database --> RC : return verification result

   RC -> Database : add new account 
   deactivate Database
   deactivate RC
   deactivate RF
   deactivate Contributor

View of Participating Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. uml::

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
   
Login
-----

Interaction Diagrams
^^^^^^^^^^^^^^^^^^^^

Basic Flow
""""""""""

.. uml::

   autonumber "#: //"
   autoactivate on
   hide footbox

   actor contributor
   boundary loginform
   control logincontroller
   entity account
	
   contributor -> loginform: access
   loginform -> loginform : display request
   contributor -> loginform : input
   loginform -> logincontroller : send account info
   logincontroller -> account :  verification request
   account->logincontroller: return verification result
   logincontroller -> loginform : allow access
   loginform -> loginform : display access
   deactivate account
   deactivate logincontroller
   deactivate loginform
   deactivate contributor

Alternate Flow
""""""""""""""

.. uml::

   actor contributor
   boundary loginform
   control logincontroller
   entity account

   contributor -> loginform:access
   loginform -> loginform : display request
   contributor -> loginform : input
   loginform -> logincontroller : send account info
   logincontroller -> account : verify request
   account -> logincontroller : return verification result
   logincontroller -> loginform : send error
   loginform -> loginform : display request
   loginform -> loginform : display error
   contributor -> loginform : cancel
   deactivate account
   deactivate logincontroller
   deactivate loginform
   deactivate contributor

View of Participating Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. uml::
   
   contributor(actor) .. login(boundary)..logincontroller(control)..account(entity)
   class contributor <<actor>> {
      username
      password
      input()
      cancel()
      access()
   }

   class Login <<boundary>> {
      // display request()
      // display error()
      // send account info()
      // display access()
   }

   class Logincontroller <<control>> {
      // verify request()
      // allow access()
      // send error()
      // allow access()
   }
   
   class Account <<entity>> {
      // return verification result()
   }   

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

   autonumber "#: //"
   autoactivate on
   hide footbox

   control UpdateControl    
   entity MetadataSystem 
   boundary DFSConnector
   actor DistributedFileSystem
   
   activate UpdateControl
   UpdateControl -> MetadataSystem : check against conflict
   UpdateControl -> DFSConnector : update package
   DFSConnector -> MetadataSystem : update to Metadata 
   DFSConnector -> DistributedFileSystem : update to DFS
   deactivate MetadataSystem
   deactivate UpdateControl
   deactivate DistributedFileSystem

View of Participating Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. uml::

   class DFSConnector <<boundary>> {
      //update to DFS()
      //update to Metadata()
   }

   class UpdateControl <<control>> {
      //check against conflict()
      //update package()
   }

   class MetadataSystem <<entity>> {
      //store package()
   }

   UpdateControl "1" -- "1" DFSConnector
   UpdateControl "1" -- "1" MetadataSystem
