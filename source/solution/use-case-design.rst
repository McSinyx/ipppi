Use-Case Design
===============

Use-Case Realization
--------------------

Register
^^^^^^^^

Iteraction Diagrams
"""""""""""""""""""

Basic Flow
''''''''''

.. uml::

   skinparam defaultFontColor #a80036
   autonumber "#:"
   autoactivate on
   hide footbox

   actor Contributor
   participant "Registration Form" as RF
   participant "Registration Controller" as RC
   participant AccountData

   activate Contributor
   Contributor -> RF : request register()
   RF -> RF : prompt registration field()
   deactivate RF
   deactivate RF

   Contributor -> RF : register(input)
   RF -> RC : request input verification()
   RC -> AccountData : verify input()
   deactivate AccountData
   RC -> AccountData : add new account()
   deactivate AccountData
   deactivate RC
   deactivate RF
   deactivate Contributor

Basic Flow (with Security)
''''''''''''''''''''''''''

.. uml::

   skinparam defaultFontColor #a80036
   autonumber "#:"
   autoactivate on
   hide footbox

   actor Contributor
   participant "Registration Form" as RF
   participant "Registration Controller" as RC
   participant AccountData
   participant ISecureUser <<interface>>

   activate Contributor
   Contributor -> RF : request register()
   RF -> RF : prompt registration field()
   deactivate RF
   deactivate RF
   Contributor -> RF : enter username()
   deactivate RF
   Contributor -> RF : enter password()
   deactivate RF
   Contributor -> RF : register account()
   RF -> RC : request input verification()
   RC -> AccountData : verify input()
   deactivate AccountData
   RC -> AccountData : add new account()
   deactivate AccountData   
   RC -> RC : setup security context()
   RC -> ISecureUser : new(UserID)
   deactivate ISecureUser
   deactivate RC
   deactivate RC   
   deactivate RF
   deactivate Contributor

View of Participating Classes
"""""""""""""""""""""""""""""

Register
''''''''

.. uml::

   skinparam defaultFontColor #a80036

   class RegistrationForm {
      request register()
      prompt registration field()
      register(input)
   }

   class RegistrationController {
      request input verification()
   }

   class AccountData {
      verify input()
      add new account()
   }

   RegistrationForm "0..*" -- "1" RegistrationController
   RegistrationController "1" -- "1" AccountData

Register (with Security)
''''''''''''''''''''''''

.. uml::

   skinparam defaultFontColor #a80036

   class RegistrationForm {
      request register()
      prompt registration field()
      enter username()
      enter password()
      register account()
   }

   class RegistrationController {
      request input verification()
      setup security context()
   }

   class AccountData {
      verify input()
      add new account()
   }
   
   interface ISecureUser <<interface>> {
      new()
   }   

   RegistrationForm "0..*" -- "1" RegistrationController
   RegistrationController "1" -- "1" AccountData
   RegistrationController "1" -- "1" ISecureUser

Login
^^^^^

Propose Package Update
^^^^^^^^^^^^^^^^^^^^^^

Iteraction Diagrams
"""""""""""""""""""

.. uml::

   skinparam defaultFontColor #a80036
   autonumber "#:"
   autoactivate on
   hide footbox

   actor Contributor

   activate Contributor
   Contributor -> ProposalForm : create package update proposal()
   ProposalForm -> ProposalForm : prompt for package names()
   ProposalForm -> ProposalForm : prompt for update(package)
   ProposalForm -> ProposalController : add proposal(updates)
   ProposalController -> IMetadataSystem : check for conflicts(updates)
   ProposalController -> NotificationSystem : notify maintainers for reviews(updates)
   deactivate NotificationSystem
   deactivate IMetadataSystem
   deactivate ProposalController
   deactivate ProposalForm
   deactivate Contributor

View of Participating Classes
"""""""""""""""""""""""""""""

.. uml::

   skinparam defaultFontColor #a80036

   class ProposalForm {
      create package update proposal()
      prompt for package names()
      prompt for update(package)
   }

   class ProposalController {
      add proposal(updates)
   }

   interface IMetadataSystem <<interface>> {
      check for conflicts(updates)
   }

   class NotificationSystem {
      notify maintainers for reviews(updates)
   }

   ProposalForm "0..*" -- "1" ProposalController
   ProposalController "1" -- "1" IMetadataSystem
   ProposalController "1" -- "1" NotificationSystem

Review Proposal
^^^^^^^^^^^^^^^

Iteraction Diagrams
"""""""""""""""""""

.. uml::

   skinparam defaultFontColor #a80036
   autonumber "#:"
   autoactivate on
   hide footbox

   actor Maintainer
   activate Maintainer
   Maintainer -> ReviewForm : check proposal ()
   ReviewForm -> UpdateControl : request proposal ()
   UpdateControl -> Proposal : get proposal ()
   deactivate UpdateControl
   deactivate Proposal
   ReviewForm -> ReviewForm : display proposal ()
   deactivate ReviewForm
   deactivate ReviewForm
   Maintainer -> ReviewForm : approve proposal ()
   ReviewForm -> UpdateControl :approve proposal ()
   UpdateControl -> Proposal : change status to approved ()
   deactivate ReviewForm
   deactivate ReviewForm
   deactivate UpdateControl
   deactivate Maintainer
   deactivate ReviewForm
   deactivate Proposal

View of Participating Classes
"""""""""""""""""""""""""""""

.. uml::

   skinparam defaultFontColor #a80036

   class ReviewForm {
      check proposal ()
      display proposal ()
      approve proposal ()
   }

   class UpdateControl {
      get proposal ()
      change status to approved ()
   }

   class Proposal {
      change status()
      get proposal()
   }

   ReviewForm "0..*" -- "1" UpdateControl
   UpdateControl "1" -- "1" Proposal

Update
^^^^^^

Iteraction Diagrams
"""""""""""""""""""

Basic Flow
''''''''''

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
   
Basic Flow (with interface)
'''''''''''''''''''''''''''

.. uml::

   skinparam defaultFontColor #a80036
   autonumber "#: //"
   autoactivate on
   hide footbox

   participant UpdateController
   participant MetadataSystem
   participant IMetadataSystemInterface
   participant DFSConnector
   actor DistributedFileSystem
   participant IDFSinterface

   activate UpdateController
   UpdateController -> MetadataSystem : check against conflict()
   UpdateController -> DFSConnector : update package()
   DFSConnector -> MetadataSystem : update to Metadata()
   MetadataSystem -> IMetadataSystemInterface : run update()
   DFSConnector -> DistributedFileSystem : update to DFS()
   DistributedFileSystem -> IDFSinterface : show updated and stored package()
   deactivate MetadataSystem
   deactivate UpdateController
   deactivate DistributedFileSystem

View of Participating Classes
"""""""""""""""""""""""""""""

Update
''''''

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
  
Update (with interface)
'''''''''''''''''''''''

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
   
   interface DFSsubsystem <<interface>> {
      // display package()

Packages and Their Dependencies
-------------------------------
