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
   autonumber "#: //"
   autoactivate on
   hide footbox

   actor Contributor
   boundary "Registration Form" as RF
   control "Registration Controller" as RC
   entity AccountData

   activate Contributor
   Contributor -> RF : request register()
   RF -> RF : prompt registration field()
   deactivate RF
   deactivate RF

   Contributor -> RF : register(input)
   RF -> RC : request input verification()
   RC -> AccountData : verify input()

   RC -> AccountData : add new account()
   deactivate AccountData
   deactivate RC
   deactivate RF
   deactivate Contributor

Basic Flow (with Security)
''''''''''''''''''''''''''

.. uml::

   skinparam defaultFontColor #a80036
   autonumber "#: //"
   autoactivate on
   hide footbox

   actor Contributor
   boundary "Registration Form" as RF
   control "Registration Controller" as RC
   entity AccountData
   boundary ISecureUser

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

   class RegistrationForm <<boundary>> {
      // request register()
      // prompt registration field()
      // register(input)
   }

   class RegistrationController <<control>> {
      // request input verification()
   }

   class AccountData <<entity>> {
      // verify input()
      // add new account()
   }

   RegistrationForm "0..*" -- "1" RegistrationController
   RegistrationController "1" -- "1" AccountData

Register (with Security)
''''''''''''''''''''''''

.. uml::

   skinparam defaultFontColor #a80036

   class RegistrationForm <<boundary>> {
      // request register()
      // prompt registration field()
      // enter username()
      // enter password()
      // register account()
   }

   class RegistrationController <<control>> {
      // request input verification()
      // setup security context()
   }

   class AccountData <<entity>> {
      // verify input()
      // add new account()
   }
   
   class ISecureUser <<interface>> {
      // new()
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
   autonumber "#: //"
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

   class ProposalForm <<boundary>> {
      // create package update proposal()
      // prompt for package names()
      // prompt for update(package)
   }

   class ProposalController <<control>> {
      // add proposal(updates)
   }

   interface IMetadataSystem <<interface>> {
      // check for conflicts(updates)
   }

   class NotificationSystem <<entity>> {
      // notify maintainers for reviews(updates)
   }

   ProposalForm "0..*" -- "1" ProposalController
   ProposalController "1" -- "1" IMetadataSystem
   ProposalController "1" -- "1" NotificationSystem

Review Proposal
^^^^^^^^^^^^^^^

Update
^^^^^^

Packages and Their Dependencies
-------------------------------
