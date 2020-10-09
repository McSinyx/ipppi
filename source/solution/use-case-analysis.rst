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
   
Login
--------

Interaction Diagrams
^^^^^^^^^^^^^^^^^^^^

Basic Flow
""""""""""

.. uml::

   actor user
   boundary loginform
   control logincontroller
   entity login

   loginform -> loginform: DisplayRequest
   user -> loginform: Login
   loginform -> logincontroller: SendAccountInfo
   logincontroller->login:Verify
   login->logincontroller:isValid(true)
   logincontroller->loginform:allowAccess
   loginform->loginform:DisplayAccess
   loginform->user:Access



Alternate Flow
""""""""""

.. uml::

   actor user
   boundary loginform
   control logincontroller
   entity login

   loginform -> loginform: DisplayRequest
   user -> loginform: Login
   loginform -> logincontroller: SendAccountInfo
   logincontroller->login:Verify
   login->logincontroller:isValid(false)
   logincontroller->loginform:Error
   loginform->loginform:DisplayRequest
   loginform->loginform:DisplayError
   user->loginform:Cancel

VOPC
""""""""""

.. uml::
   
   user(actor) .. login(boundary)..logincontroller(control)..login(entity)
   class user(actor){
   username
   password
   login()
   cancel()
   Access()
   }

   class login(boundary){
   DisplayRequest()
   DisplayError()
   SendAccountInfo()
   DisplayAccess()
   }

   class logincontroller(control){
   Verify()
   allowAccess()
   error()
   }
   
   class login(entity){
   isValid()
   }
