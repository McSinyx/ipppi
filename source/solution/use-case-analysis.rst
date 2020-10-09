Use-Case Analysis
=================

Register
----------------------

Interaction Diagrams
^^^^^^^^^^^^^^^^^^^^

Basic Flow
""""""""""

.. uml::
   
   hide footbox
   
   actor Contributor
   boundary "Login Interface" as LI
   control "Registration Controller" as RC
   entity Database

   activate Contributor
   Contributor -> LI : 1: request register

   activate LI
   LI -> LI : 2: prompt registration field
   activate LI
   Contributor -> LI : 3: register(input)

   LI -> RC : 4: request input verification
   activate RC
   RC -> Database : 5: verify input
   activate Database
   Database --> RC : 6: return verification result
   RC -> Database : 7: add new account 
   deactivate Database
   deactivate RC

   deactivate LI
   deactivate LI
   deactivate Contributor

View of Participating Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. uml::

   class LoginPage <<boundary>> {
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

   LoginPage "0..*" -- "1" RegistrationController
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
   
