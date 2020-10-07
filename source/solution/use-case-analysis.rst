Use-Case Analysis
=================

Register
----------------------

Interaction Diagrams
^^^^^^^^^^^^^^^^^^^^

Basic Flow
""""""""""

.. uml::

   actor Contributor
   boundary "Login Page" as LP
   control "Registration Controller" as RC
   entity Database
   boundary "Main Page" as MP

   activate Contributor
   Contributor -> LP : 1: request register

   activate LP
   LP -> LP : 2: prompt registration field
   activate LP
   Contributor -> LP : 3: register(input)

   LP -> RC : 4: request input verification
   activate RC
   RC -> Database : 5: verify input
   activate Database
   Database --> RC : 6: return verification result
   RC -> Database : 7: add new account 
   deactivate Database
   deactivate RC

   deactivate LP
   LP -> MP : redirect
   activate MP
   deactivate MP
   deactivate LP
   deactivate Contributor

View of Participating Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. uml::


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


